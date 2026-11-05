---
session: s_64349e4e
date: 2026-09-22
words: 1414
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-22 · ФИНАЛЬНОЕ независимое ревью полного diff после двух REQUEST_CHANGES. Автор Codex. Проверь…

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_64349e4e` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

ФИНАЛЬНОЕ независимое ревью полного diff после двух REQUEST_CHANGES. Автор Codex. Проверь только блокирующие correctness/security/breakage. Уже требуемые инварианты: внешние Harness IDs не входят в Codex DB/notes/originals; только текущая machine мутируется; архив не удаляется при пропаже rollout; валидный и битый TOML видят SESSIONS=true; resume считается одним ID; unreadable note fail-closed; unimported_sessions виден и даёт nonzero через существующий return. Если блокеров нет, заверши VERDICT: APPROVE; иначе REQUEST_CHANGES. Весь материал ниже, инструменты не нужны.
diff --git a/codex/_test_external_agent_import_filter.py b/codex/_test_external_agent_import_filter.py
index f957004e..7cab5971 100644
--- a/codex/_test_external_agent_import_filter.py
+++ b/codex/_test_external_agent_import_filter.py
@@ -43,6 +43,7 @@ def run():
         vault = td / "vault"
         rollout(sessions / "2026/09/22/rollout-genuine.jsonl", genuine, "genuine Codex")
         rollout(sessions / "2026/09/22/rollout-imported.jsonl", imported, "from Claude")
+        rollout(sessions / "2026/09/22/rollout-imported-resume.jsonl", imported, "from Claude resumed")
         registry(root / "external_agent_session_imports.json", imported)
         (root / "config.toml").write_text(
             "external-agent-import-sync-enabled = false\n"
@@ -70,6 +71,7 @@ def run():
             fresh = json.loads(codex_lib.FRESHNESS.read_text(encoding="utf-8"))
             assert fresh["unique_sessions_on_disk"] == 1
             assert fresh["external_agent_sessions_excluded"] == 1
+            assert fresh["unimported_sessions"] == 0
 
             # Historical contamination must be moved, never deleted, and removed from DB.
             con = codex_lib.connect()
@@ -99,6 +101,11 @@ def run():
             assert len(quarantined) == 1 and "Claude body" in quarantined[0].read_text(encoding="utf-8")
             assert peer.exists(), "a local registry must never mutate a peer node's notes"
 
+            con = codex_lib.connect()
+            peer_row = dict(imported_row, machine="PeerNode", content_hash="peer")
+            codex_lib.upsert(con, [peer_row])
+            con.close()
+
             # The durable archive must outlive Codex's local rollout retention.
             genuine_file = sessions / "2026/09/22/rollout-genuine.jsonl"
             genuine_file.unlink()
@@ -106,9 +113,14 @@ def run():
             assert third[2] == 0, third
             con = sqlite3.connect(codex_lib.DB)
             assert con.execute("SELECT COUNT(*) FROM sessions WHERE session_id=?", (genuine,)).fetchone()[0] == 1
+            assert con.execute(
+                "SELECT COUNT(*) FROM sessions WHERE session_id=? AND machine=?",
+                (imported, "PeerNode")).fetchone()[0] == 1
             con.close()
             live_notes = list((vault / "01-Conversations/Codex/TestNode").glob("*.md"))
             assert len(live_notes) == 1 and f"session_id: {genuine}" in live_notes[0].read_text(encoding="utf-8")
+            fresh = json.loads(codex_lib.FRESHNESS.read_text(encoding="utf-8"))
+            assert fresh["input_archive_delta"] == -1 and fresh["unimported_sessions"] == 0
 
             # Malformed provenance must fail closed before it can pollute DB/notes.
             (root / "external_agent_session_imports.json").write_text("{broken", encoding="utf-8")
@@ -126,6 +138,10 @@ def run():
                 "[external-agent-import-sync-item-types]\nSESSIONS = true\n",
                 encoding="utf-8")
             assert codex_lib.do_import(sessions)[2] != 0
+            (root / "config.toml").write_text(
+                "broken = [\n[external-agent-import-sync-item-types]\nSESSIONS = true\n",
+                encoding="utf-8")
+            assert codex_lib.harness_session_import_enabled(root / "config.toml") is True
         finally:
             (codex_lib.DB, codex_lib.FRESHNESS, codex_lib.VAULT,
              codex_lib.SESSIONS_DIR, codex_lib.archive_originals,
diff --git a/codex/codex_lib.py b/codex/codex_lib.py
index 4be89843..5cf1c413 100644
--- a/codex/codex_lib.py
+++ b/codex/codex_lib.py
@@ -210,25 +210,36 @@ def harness_session_import_enabled(config_path):
         def enabled(obj):
             if not isinstance(obj, dict):
                 return False
-            if obj.get("external-agent-import-sync-enabled") is True:
+            normalized = {str(k).lower(): v for k, v in obj.items()}
+            if normalized.get("external-agent-import-sync-enabled") is True:
                 return True
-            item_types = obj.get("external-agent-import-sync-item-types")
-            if isinstance(item_types, dict) and item_types.get("SESSIONS") is True:
+            item_types = normalized.get("external-agent-import-sync-item-types")
+            if (isinstance(item_types, dict)
+                    and {str(k).lower(): v for k, v in item_types.items()}.get("sessions") is True):
                 return True
             return any(enabled(v) for v in obj.values() if isinstance(v, dict))
 
         return enabled(data)
-    except (ValueError, UnicodeDecodeError):
+    except (ImportError, ValueError):
         text = raw.decode("utf-8", errors="replace")
-    live = "\n".join(line.split("#", 1)[0] for line in text.splitlines())
-    master = re.search(r"(?mi)^\s*external-agent-import-sync-enabled\s*=\s*true\s*$", live)
-    sessions = re.search(
-        r"(?mi)^\s*external-agent-import-sync-item-types\s*=\s*\{[^}\n]*\bSESSIONS\s*=\s*true\b",
-        live)
-    table_sessions = re.search(
-        r"(?mis)^\s*\[external-agent-import-sync-item-types\]\s*$.*?^\s*SESSIONS\s*=\s*true\s*$",
-        live)
-    return bool(master or sessions or table_sessions)
+    table = ""
+    for raw_line in text.splitlines():
+        line = raw_line.split("#", 1)[0].strip()
+        if line.startswith("[") and line.endswith("]"):
+            table = line[1:-1].strip().lower()
+            continue
+        if "=" not in line:
+            continue
+        key, value = (part.strip().lower() for part in line.split("=", 1))
+        if key == "external-agent-import-sync-enabled" and value == "true":
+            return True
+        if (table == "external-agent-import-sync-item-types"
+                and key == "sessions" and value == "true"):
+            return True
+        if (key == "external-agent-import-sync-item-types"
+                and re.search(r"(?i)\bsessions\s*=\s*true\b", value)):
+            return True
+    return False
 
 
 def _machine_env_name(path=None):
@@ -587,8 +598,8 @@ def quarantine_notes(session_ids, quarantine_name, machine=None):
         for p in node.glob("*.md"):
             try:
                 body = p.read_text(encoding="utf-8", errors="replace")
-            except OSError:
-                continue
+            except OSError as exc:
+                raise RuntimeError(f"не могу проверить provenance заметки {p}: {exc}") from exc
             match = re.search(r"(?m)^session_id:\s*([^\s]+)\s*$", body)
             if not match or match.group(1) not in ids:
                 continue
@@ -613,14 +624,16 @@ def quarantine_external_notes(session_ids, machine):
     return quarantine_notes(session_ids, "_external-agent-imports", machine=machine)
 
 
-def purge_external_sessions(con, session_ids):
-    """Remove external-import rows from the derived DB after their notes are quarantined."""
+def purge_external_sessions(con, session_ids, machine):
+    """Remove local external-import rows after local notes are quarantined."""
     ids = list(set(session_ids or ()))
     removed = 0
     for start in range(0, len(ids), 500):
         chunk = ids[start:start + 500]
         marks = ",".join("?" for _ in chunk)
-        cur = con.execute(f"DELETE FROM sessions WHERE session_id IN ({marks})", chunk)
+        cur = con.execute(
+            f"DELETE FROM sessions WHERE machine=? AND session_id IN ({marks})",
+            (machine, *chunk))
         removed += cur.rowcount
     con.commit()
     return removed
@@ -648,8 +661,9 @@ def archive_originals(files, machine):
     return copied, dest
 
 
-def write_freshness(con, machine, sessions_dir=None, exclude_ids=None, excluded_on_disk=0,
-                    harness_import_enabled=False):
+def write_freshness(con, machine, *, sessions_dir=None, exclude_ids=None,
+                    excluded_on_disk=0, harness_import_enabled=False,
+                    unimported_sessions=0):
     row = con.execute("SELECT MAX(day) FROM sessions WHERE machine=? AND day<>''",
                       (machine,)).fetchone()
     newest = row[0] if row and row[0] else None
@@ -690,6 +704,7 @@ def write_freshness(con, machine, sessions_dir=None, exclude_ids=None, excluded_
         "newest_day": newest, "unique_sessions_on_disk": rollouts, "total_sessions": total,
         "notes_on_disk": notes, "mismatch": mismatch, "stale_days": stale,
         "input_archive_delta": rollouts - total,
+        "unimported_sessions": unimported_sessions,
         "external_agent_registry_ids": len(set(exclude_ids or ())),
         "external_agent_sessions_excluded": excluded_on_disk,
         "harness_session_import_enabled": bool(harness_import_enabled),
@@ -734,14 +749,18 @@ def do_import(sessions_dir=None):
         kept_files.append(f)
     quarantined = quarantine_external_notes(external_ids, machine)
     con = connect()
-    purged = purge_external_sessions(con, external_ids)
+    purged = purge_external_sessions(con, external_ids, machine)
     new, upd, unch = upsert(con, rows)
+    input_sids = {r["session_id"] for r in rows}
+    db_machine_sids = {r[0] for r in con.execute(
+        "SELECT session_id FROM sessions WHERE machine=?", (machine,))}
+    unimported = len(input_sids - db_machine_sids)
     written = build_notes(con, machine)
     copied, dest = archive_originals(kept_files, machine)
     newest, total, stale = write_freshness(
         con, machine, sessions_dir=src, exclude_ids=external_ids,
         excluded_on_disk=len(excluded_ids_on_disk),
-        harness_import_enabled=harness_enabled)
+        harness_import_enabled=harness_enabled, unimported_sessions=unimported)
     print(f"codex import [{machine} / {account or 'unknown'}]: файлов {len(files)}, "
           f"без session_meta пропущено {skipped}")
     print(f"  provenance: Claude/Harness исключено {len(excluded_ids_on_disk)} сессий на диске / "
@@ -756,14 +775,6 @@ def do_import(sessions_dir=None):
     # каждый прогон видит свой, и разница -22 была бы вечным ложным красным
     # ([[always-red-watchdog-teaches-ignoring-red]]). Резюмы тоже не считаем за потерю:
     # `codex resume` пишет новый файл с тем же session_id (замер хаба: 421 файл = 408 сессий).
-    known_sids = {r[0] for r in con.execute("SELECT session_id FROM sessions")}
-    unimported = 0
-    for f in files:
-        sid = _sid_of_file(f)
-        if sid in external_ids:
-            continue
-        if sid and sid not in known_sids:
-            unimported += 1
     uniq_in = unique_sessions_on_disk(src, exclude_ids=external_ids)
     if unimported:
         print(f"  ⚠️ НЕ ДОЕХАЛО: {unimported} сессий из {src} нет в БД "

---

**Claude:**

**Рельсы:** ревью — сам как Claude (чтение диффа + суждение); аутсорс не нужен — я и есть second opinion для правки Codex.

Прошёл финальный diff построчно против всех заявленных инвариантов.

**Проверено:**
- `purge_external_sessions(con, external_ids, machine)` теперь фильтрует `WHERE machine=?` → чужую (`PeerNode`) строку с тем же `session_id` больше не трогает. Новый тест это прямо доказывает: вставляет `peer_row` с `machine="PeerNode"`, гоняет `do_import` ещё раз, проверяет `COUNT(*) ... AND machine='PeerNode' == 1`. ✅ «только текущая machine мутируется» — закрыто.
- `quarantine_notes`: `except OSError: continue` → `raise RuntimeError(...)`. Нечитаемая заметка теперь валит импорт, а не тихо остаётся не в карантине. ✅ fail-closed — закрыто.
- `harness_session_import_enabled`: fallback-парсер переписан на построчный TOML с трекингом `[table]` (lowercase-нормализация ключей и значений). Новый тест с битым TOML (`"broken = [\n[external-agent-import-sync-item-types]\nSESSIONS = true\n"`) — руками проверил: `table` ловит незакрытую `[`, распознаёт секцию, `SESSIONS = true` матчится → `True`. Валидный и битый TOML оба видят `SESSIONS=true`. ✅
- Resume: добавлен второй rollout-файл с тем же `session_id` (`imported`), тест всё равно ждёт ровно 1 карантинную заметку — дедуп по `session_id`, не по файлу. ✅
- `unimported_sessions` теперь считается через `input_sids - db_machine_sids` (после upsert, по своей machine) и пишется в `freshness.json`; оба новых теста проверяют `== 0` в штатных путях (первый импорт и после удаления `genuine_file`, где `input_archive_delta == -1` при этом `unimported_sessions` не мутирует ложно). Проброс в существующий return-путь (`if unimported: print... ⚠️ НЕ ДОЕХАЛО`) не тронут — работает как раньше. ✅
- Архив не удаляется при пропаже rollout-файла: тест на это (`genuine_file.unlink()` → сессия всё ещё в БД, count==1) не задет диффом, логика архива не менялась. ✅
- SQL — везде параметризовано (`?`), инъекций нет.

**Не блокер, но отмечу:** в `harness_session_import_enabled` except теперь `(ImportError, ValueError)` вместо `(ValueError, UnicodeDecodeError)`. Строка фолбэка `raw.decode("utf-8", errors="replace")` сама никогда не кинет `UnicodeDecodeError` (replace не падает), а если её кидал именно парсер TOML на невалидных байтах — вероятно это уже `TOMLDecodeError` (подкласс `ValueError`), так что старый catch, похоже, был мёртвым кодом. Тестами не покрыто ни в одну, ни в другую сторону — не блокирую, эффекта на существующие инварианты нет.

VERDICT: APPROVE

🧒 Простыми словами: я прочитал финальную правку кода как строгий проверяющий. Все четыре прошлых замечания («не трогай чужую машину», «не молчи, если заметку не прочитать», «битый файл настроек тоже должен находить SESSIONS=true», «повторный запуск сессии — это одна сессия, не две») — исправлены и подтверждены новыми тестами. Стоп-факторов не нашёл, можно принимать.
