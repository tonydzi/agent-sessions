---
session: s_3953a76d
date: 2026-09-22
words: 2380
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-22 · Ты независимый старший ревьюер. Это второй проход после REQUEST_CHANGES. Проверь итоговый…

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_3953a76d` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

Ты независимый старший ревьюер. Это второй проход после REQUEST_CHANGES. Проверь итоговый diff Codex-фильтра. Особо проверь из самого diff: пустой sessions-dir не должен удалять архив; explicit --sessions-dir не должен трогать другой дом; локальный provenance не должен менять peer node; multiline TOML SESSIONS=true должен дать красный сигнал; resume-файлы считаются одним ID. Только доказуемые findings с file:line и severity. Заверши ровно VERDICT: APPROVE или VERDICT: REQUEST_CHANGES. Не используй инструменты: весь материал ниже.
diff --git a/codex/_test_external_agent_import_filter.py b/codex/_test_external_agent_import_filter.py
index 0d2de3fb..f957004e 100644
--- a/codex/_test_external_agent_import_filter.py
+++ b/codex/_test_external_agent_import_filter.py
@@ -86,6 +86,9 @@ def run():
             contaminated.write_text(
                 "---\nsource: codex\nsession_id: %s\nrelated_concepts: []\n---\nClaude body\n" % imported,
                 encoding="utf-8")
+            peer = vault / "01-Conversations/Codex/PeerNode/2026-09-22-peer-000000000002.md"
+            peer.parent.mkdir(parents=True)
+            peer.write_text(contaminated.read_text(encoding="utf-8"), encoding="utf-8")
             second = codex_lib.do_import(sessions)
             assert second[2] == 0, second
             con = sqlite3.connect(codex_lib.DB)
@@ -94,18 +97,18 @@ def run():
             assert not contaminated.exists()
             quarantined = list((contaminated.parent / "_external-agent-imports").glob("*.md"))
             assert len(quarantined) == 1 and "Claude body" in quarantined[0].read_text(encoding="utf-8")
+            assert peer.exists(), "a local registry must never mutate a peer node's notes"
 
-            # A vanished native rollout must not survive forever as a green DB/note ghost.
+            # The durable archive must outlive Codex's local rollout retention.
             genuine_file = sessions / "2026/09/22/rollout-genuine.jsonl"
             genuine_file.unlink()
             third = codex_lib.do_import(sessions)
             assert third[2] == 0, third
             con = sqlite3.connect(codex_lib.DB)
-            assert con.execute("SELECT COUNT(*) FROM sessions WHERE session_id=?", (genuine,)).fetchone()[0] == 0
+            assert con.execute("SELECT COUNT(*) FROM sessions WHERE session_id=?", (genuine,)).fetchone()[0] == 1
             con.close()
-            assert not list((vault / "01-Conversations/Codex/TestNode").glob("*.md"))
-            missing = list((vault / "01-Conversations/Codex/TestNode/_missing-source").glob("*.md"))
-            assert len(missing) == 1 and f"session_id: {genuine}" in missing[0].read_text(encoding="utf-8")
+            live_notes = list((vault / "01-Conversations/Codex/TestNode").glob("*.md"))
+            assert len(live_notes) == 1 and f"session_id: {genuine}" in live_notes[0].read_text(encoding="utf-8")
 
             # Malformed provenance must fail closed before it can pollute DB/notes.
             (root / "external_agent_session_imports.json").write_text("{broken", encoding="utf-8")
@@ -119,8 +122,8 @@ def run():
             # Harness drift back to ON is a visible non-zero health result.
             registry(root / "external_agent_session_imports.json", imported)
             (root / "config.toml").write_text(
-                "external-agent-import-sync-enabled = true\n"
-                "external-agent-import-sync-item-types = { SESSIONS = true }\n",
+                "external-agent-import-sync-enabled = false\n"
+                "[external-agent-import-sync-item-types]\nSESSIONS = true\n",
                 encoding="utf-8")
             assert codex_lib.do_import(sessions)[2] != 0
         finally:
diff --git a/codex/codex_lib.py b/codex/codex_lib.py
index 9813c54d..4be89843 100644
--- a/codex/codex_lib.py
+++ b/codex/codex_lib.py
@@ -200,15 +200,35 @@ def harness_session_import_enabled(config_path):
     if not p.exists():
         return False
     try:
-        text = p.read_text(encoding="utf-8", errors="replace")
+        raw = p.read_bytes()
     except OSError:
         return False
+    try:
+        import tomllib
+        data = tomllib.loads(raw.decode("utf-8-sig"))
+
+        def enabled(obj):
+            if not isinstance(obj, dict):
+                return False
+            if obj.get("external-agent-import-sync-enabled") is True:
+                return True
+            item_types = obj.get("external-agent-import-sync-item-types")
+            if isinstance(item_types, dict) and item_types.get("SESSIONS") is True:
+                return True
+            return any(enabled(v) for v in obj.values() if isinstance(v, dict))
+
+        return enabled(data)
+    except (ValueError, UnicodeDecodeError):
+        text = raw.decode("utf-8", errors="replace")
     live = "\n".join(line.split("#", 1)[0] for line in text.splitlines())
     master = re.search(r"(?mi)^\s*external-agent-import-sync-enabled\s*=\s*true\s*$", live)
     sessions = re.search(
         r"(?mi)^\s*external-agent-import-sync-item-types\s*=\s*\{[^}\n]*\bSESSIONS\s*=\s*true\b",
         live)
-    return bool(master or sessions)
+    table_sessions = re.search(
+        r"(?mis)^\s*\[external-agent-import-sync-item-types\]\s*$.*?^\s*SESSIONS\s*=\s*true\s*$",
+        live)
+    return bool(master or sessions or table_sessions)
 
 
 def _machine_env_name(path=None):
@@ -565,7 +585,10 @@ def quarantine_notes(session_ids, quarantine_name, machine=None):
         if machine and node.name != machine:
             continue
         for p in node.glob("*.md"):
-            body = p.read_text(encoding="utf-8", errors="replace")
+            try:
+                body = p.read_text(encoding="utf-8", errors="replace")
+            except OSError:
+                continue
             match = re.search(r"(?m)^session_id:\s*([^\s]+)\s*$", body)
             if not match or match.group(1) not in ids:
                 continue
@@ -580,9 +603,14 @@ def quarantine_notes(session_ids, quarantine_name, machine=None):
     return moved
 
 
-def quarantine_external_notes(session_ids):
-    """Move misclassified Claude notes to a reversible, non-indexed quarantine."""
-    return quarantine_notes(session_ids, "_external-agent-imports")
+def quarantine_external_notes(session_ids, machine):
+    """Move local misclassified Claude notes, enriched or not, out of the Codex lane.
+
+    This is deliberately stricter than stale-note cleanup: provenance is objectively
+    wrong, so a linked note stays byte-for-byte preserved but cannot remain source=codex.
+    The registry is machine-local; touching peer folders would violate ownership.
+    """
+    return quarantine_notes(session_ids, "_external-agent-imports", machine=machine)
 
 
 def purge_external_sessions(con, session_ids):
@@ -598,21 +626,6 @@ def purge_external_sessions(con, session_ids):
     return removed
 
 
-def reconcile_missing_sources(con, machine, live_session_ids):
-    """Quarantine derived notes/rows whose native rollout disappeared from this node."""
-    known = {r[0] for r in con.execute(
-        "SELECT session_id FROM sessions WHERE machine=?", (machine,))}
-    missing = known - set(live_session_ids or ())
-    moved = quarantine_notes(missing, "_missing-source", machine=machine)
-    if missing:
-        marks = ",".join("?" for _ in missing)
-        con.execute(
-            f"DELETE FROM sessions WHERE machine=? AND session_id IN ({marks})",
-            (machine, *missing))
-        con.commit()
-    return len(missing), moved
-
-
 def archive_originals(files, machine):
     """Raw rollouts kept verbatim (canon §8.3 step 1). Peer nodes must NOT write to the
     hub's canon originals path — _paths.originals_root() picks the right one per role;
@@ -635,7 +648,7 @@ def archive_originals(files, machine):
     return copied, dest
 
 
-def write_freshness(con, machine, exclude_ids=None, excluded_on_disk=0,
+def write_freshness(con, machine, sessions_dir=None, exclude_ids=None, excluded_on_disk=0,
                     harness_import_enabled=False):
     row = con.execute("SELECT MAX(day) FROM sessions WHERE machine=? AND day<>''",
                       (machine,)).fetchone()
@@ -656,8 +669,11 @@ def write_freshness(con, machine, exclude_ids=None, excluded_on_disk=0,
     # ⚠️ 14.08: сравнивать БД с заметками МАЛО — оба числа считаются под ОДНИМ ярлыком узла,
     # поэтому при плавающем хостнейме они сходятся, а 41 сессия лежит под другими ярлыками.
     # Истина входа — ФАЙЛЫ НА ДИСКЕ. Прибор, который не видит вход, врёт зелёным.
-    rollouts = unique_sessions_on_disk(exclude_ids=exclude_ids)
-    mismatch = (rollouts - notes) if rollouts else (total - notes)
+    rollouts = unique_sessions_on_disk(sessions_dir, exclude_ids=exclude_ids)
+    # The archive must outlive Codex's local retention. A missing raw rollout is therefore
+    # not permission to erase the DB/note. Health is the durable DB -> note projection;
+    # new on-disk sessions missing from DB are checked separately in do_import().
+    mismatch = total - notes
     # ⚠️ 07.09: ОТРИЦАТЕЛЬНЫЙ mismatch прибор обязан объяснить сам, а не оставлять загадкой.
     # Заметок БОЛЬШЕ, чем сессий, бывает ровно по одной причине: два файла на один
     # session_id (имя несёт меняющийся слуг заголовка, см. sweep_stale_notes). Считаем их
@@ -673,6 +689,7 @@ def write_freshness(con, machine, exclude_ids=None, excluded_on_disk=0,
         "machine": machine, "account": account_email(),
         "newest_day": newest, "unique_sessions_on_disk": rollouts, "total_sessions": total,
         "notes_on_disk": notes, "mismatch": mismatch, "stale_days": stale,
+        "input_archive_delta": rollouts - total,
         "external_agent_registry_ids": len(set(exclude_ids or ())),
         "external_agent_sessions_excluded": excluded_on_disk,
         "harness_session_import_enabled": bool(harness_import_enabled),
@@ -698,9 +715,9 @@ def do_import(sessions_dir=None):
     if not src.is_dir():
         print(f"codex: НЕТ каталога сессий {src} — Codex на этой машине не ставился "
               f"(это не ошибка, узлу просто нечего отдавать)")
-        return 0, 0
+        return 0, 0, 0
     files = sorted(glob.glob(str(src / "**" / "*.jsonl"), recursive=True))
-    rows, kept_files, skipped, excluded_on_disk = [], [], 0, 0
+    rows, kept_files, skipped, excluded_ids_on_disk = [], [], 0, set()
     for f in files:
         try:
             with open(f, encoding="utf-8", errors="replace") as fh:
@@ -711,27 +728,24 @@ def do_import(sessions_dir=None):
             skipped += 1
             continue
         if r["session_id"] in external_ids:
-            excluded_on_disk += 1
+            excluded_ids_on_disk.add(r["session_id"])
             continue
         rows.append(r)
         kept_files.append(f)
-    quarantined = quarantine_external_notes(external_ids)
+    quarantined = quarantine_external_notes(external_ids, machine)
     con = connect()
     purged = purge_external_sessions(con, external_ids)
-    missing_rows, missing_notes = reconcile_missing_sources(
-        con, machine, {r["session_id"] for r in rows})
     new, upd, unch = upsert(con, rows)
     written = build_notes(con, machine)
     copied, dest = archive_originals(kept_files, machine)
     newest, total, stale = write_freshness(
-        con, machine, exclude_ids=external_ids, excluded_on_disk=excluded_on_disk,
+        con, machine, sessions_dir=src, exclude_ids=external_ids,
+        excluded_on_disk=len(excluded_ids_on_disk),
         harness_import_enabled=harness_enabled)
     print(f"codex import [{machine} / {account or 'unknown'}]: файлов {len(files)}, "
           f"без session_meta пропущено {skipped}")
-    print(f"  provenance: Claude/Harness исключено {excluded_on_disk} на диске / "
+    print(f"  provenance: Claude/Harness исключено {len(excluded_ids_on_disk)} сессий на диске / "
           f"{purged} строк БД / {quarantined} заметок в обратимый карантин")
-    print(f"  reconciliation: исчезнувших native-источников {missing_rows} / "
-          f"заметок в _missing-source {missing_notes}")
     print(f"  DB: +{new} новых / {upd} обновлено / {unch} без изменений | всего {total}")
     print(f"  заметки: {written} -> {notes_dir(machine)}")
     print(f"  оригиналы: +{copied} -> {dest}")

---

**Claude:**

вторник, 22 сентября 2026, 14:36

**Рельсы:** ревью делаю сам как Claude (чтение кода + суждение); `second_opinion>codex` мимо по определению — автор диффа и есть Codex, отдавать ему ревью его же работы бессмысленно; `rail_plan.py declare` не вызываю, потому что инструменты в этом заходе запрещены прямым указанием.

Номера строк — по **новой** стороне диффа, посчитаны от заголовков хунков (±1 строка).

---

## Проверка пяти заявленных инвариантов

| # | Инвариант | Итог | Доказательство из диффа |
|---|---|---|---|
| 1 | Пустой/исчезнувший sessions-dir не удаляет архив | ✅ | `reconcile_missing_sources` вырезана целиком (удалены старые 601–615) и её вызов убран из `do_import`; при отсутствии каталога выход **до** любых мутаций (`codex_lib.py:715-717`); заметки пересобираются из БД (`build_notes(con, machine)`). Тест краснеет без фикса: `test:108` ждёт `COUNT=1`, `test:110-111` — живую заметку. |
| 2 | Explicit `--sessions-dir` не трогает другой дом | ✅ | `sessions_dir` доехал по цепочке: `write_freshness(..., sessions_dir=src, ...)` → `codex_lib.py:648` → `unique_sessions_on_disk(sessions_dir, exclude_ids=...)` (`:672`). Раньше вызов шёл без каталога и мерил дефолтный дом. |
| 3 | Локальный provenance не меняет peer node | ✅ | `quarantine_external_notes(session_ids, machine)` (`:606`) → `quarantine_notes(..., machine=machine)` → фильтр `if machine and node.name != machine: continue` (`:585-587`). Тест red-first: `test:89-91` кладёт заметку с тем же `session_id` в `Codex/PeerNode/`, `test:100` требует `peer.exists()` — без передачи `machine` заметку бы унесло. |
| 4 | Multiline TOML `SESSIONS=true` → красный | ✅ | Ловится tomllib-путём: `item_types.get("SESSIONS") is True` (`:216-217`) на `[external-agent-import-sync-item-types]`. Regex-дублёр для того же кейса добавлен (`:228-230`), но при валидном TOML он мёртв — см. F5. |
| 5 | Resume-файлы = один ID | ✅ в коде | `excluded_ids_on_disk` стал `set()` (`:729`), `.add(r["session_id"])` (`:731`), наружу `len(...)` (`:741`). Утверждения в тесте на это нет — см. F8. |

Заодно исправлена реальная поломка арности: `return 0, 0` → `return 0, 0, 0` (`:717`) — раньше на машине без Codex любой распаковщик трёх значений падал.

---

## Findings

**F1 · `codex/codex_lib.py:207` · MED · блокирующий**
`import tomllib` стоит внутри `try`, а `except (ValueError, UnicodeDecodeError)` (`:221`) ImportError не ловит. На Python ≤3.10 `tomllib` отсутствует → исключение улетает наружу и убивает весь `do_import` (раньше функция работала на любом Python, потому что была чистым regex).

Фикс на одну строку: `except (ImportError, ValueError):`. `UnicodeDecodeError` там лишний — он подкласс `ValueError`.

**F2 · `codex/codex_lib.py:672-676` и `:692` · MED · блокирующий**
Детекция входа потеряна, а комментарий утверждает обратное. `mismatch = total - notes` (`:676`) — это проекция БД→заметки, вход в ней больше не участвует. Заменитель `"input_archive_delta": rollouts - total` (`:692`) — разность двух **счётчиков**, и по новой же доктрине «архив переживает retention» она почти всегда отрицательна.

Отсюда арифметический факт: N новых неимпортированных сессий на диске делают delta лишь «менее отрицательной», поэтому порог вида `>0` не сработает никогда. Класс 14.08 (41 сессия под другими ярлыками), про который кричит сохранённый строкой выше комментарий «Прибор, который не видит вход, врёт зелёным», после этого диффа не виден ни одним полем.

Плюс `:675` заявляет «new on-disk sessions missing from DB are checked separately in `do_import()`» — в диффе такой проверки нет; видимое тело `do_import` показано целиком от `if not src.is_dir()` (`:715`) до print'ов (`:748`), и ни одна строка не сравнивает id с диска с id в БД. Комментарий — такой же claim, как вывод.

Фикс: считать `unimported = len(set(on_disk_ids) - set(db_ids))`, положить это отдельным полем и повесить на него красный сигнал; `mismatch = total - notes` оставить как есть.

**F3 · `codex/codex_lib.py:601` (удалены старые 601-615) · MED**
Механизм удалён, его следы — нет. Удалённый `reconcile_missing_sources` не просто помечал, а **удалял строки БД** (`DELETE FROM sessions WHERE machine=? AND session_id IN (...)`) и уносил заметки в `_missing-source`; что он шиппился и работал, доказывают удалённые строки теста (старые `test:105-108` требовали ровно одну заметку в `_missing-source`).

После диффа такие сессии не восстановит никто: rollout'а на диске нет (потому reconcile и срабатывал), заметка лежит вне живой полосы, строки в БД нет. Миграции в диффе тоже нет.

Фикс: одноразовый проход по `01-Conversations/Codex/*/_missing-source/*.md` — переимпорт из `_originals` (сырьё канон §8.3 хранит верbatim, именно на него опирается новая доктрина) либо, минимум, отчёт числом на каждом узле.

**F4 · `codex/codex_lib.py:588-591` · MED**
`except OSError: continue` глушит нечитаемую заметку молча. На Windows лок Obsidian/OneDrive — обычное дело; в этом случае заметка с заведомо неверным provenance **остаётся** в полосе Codex, счётчик `quarantined` (`:747`) недосчитывает, наружу не уходит ни строки. Docstring рядом (`:607-612`) при этом утверждает, что provenance «objectively wrong» и остаться не может — расхождение кода с собственным паспортом.

Фикс: копить список неудач, печатать их поимённо и поднимать health ≠ 0.

**F5 · `codex/codex_lib.py:228-230` · LOW**
Новая regex-ветка `table_sessions` (а) не покрыта ни одним тестом: TOML в `test:124-126` валиден, значит управление уходит в tomllib-путь и `return enabled(data)` (`:220`) срабатывает до regex; (б) с `(?s)` и ленивым `.*?` матчит через границы таблиц — `[external-agent-import-sync-item-types]\nFILES = true\n\n[other]\nSESSIONS = true` даст ложный «включено».

Фикс: ограничить хвост до следующего заголовка (`(?:(?!^\s*\[)[\s\S])*?`) и добавить в тест кейс с **битым** TOML, иначе ветка не краснеет никогда.

**F6 · `codex/codex_lib.py:213-217` против `:224` · LOW**
Асимметрия регистра на гейте. Fallback-regex регистронезависим (`(?mi)`), tomllib-путь требует точного ключа и short-circuit'ит fallback. Валидный TOML с `External-Agent-Import-Sync-Enabled = true` раньше читался как «включено», теперь — как «выключено»; направление отказа fail-open.

Фикс: нормализовать ключи (`k.lower()`) внутри `enabled()`.

**F7 · `codex/codex_lib.py:648` · LOW**
`sessions_dir` вставлен **третьим позиционным**, перед `exclude_ids`. Любой внешний вызов вида `write_freshness(con, machine, ids)` теперь молча свяжет список id с путём. Того же класса риск у `quarantine_external_notes`: второй аргумент сделан обязательным без дефолта.

Фикс: `def write_freshness(con, machine, *, sessions_dir=None, ...)` — и грепнуть остальных вызывающих обеих функций перед мержем.

**F8 · `codex/_test_external_agent_import_filter.py:89-111` · LOW**
Два поведения, которые дифф вводит, не подпёрты ни одним утверждением: дедуп исключённых по `session_id` (ни одна строка теста не читает число исключённых — тест прошёл бы и со старым счётчиком файлов) и поле `input_archive_delta`.

Фикс: положить второй (resume) файл на тот же `session_id` из реестра и проверить `external_agent_sessions_excluded == 1`.

---

## Что я НЕ проверял (вне диффа)

Финальный `return` из `do_import` и то, как считается код здоровья `[2]`, в хунках отсутствуют — поэтому «кто и чем гейтит `input_archive_delta`» я не знаю. На F2 это не влияет: аргумент там арифметический, а не про потребителя поля.

Также вне диффа остались подпись `unique_sessions_on_disk` (я допускаю, что первый позиционный — каталог), тела `build_notes` / `sweep_stale_notes` / `archive_originals`, версия Python на узлах и список внешних вызывающих `reconcile_missing_sources` (функции больше нет — если её кто-то импортирует, будет ImportError).

Пять запрошенных инвариантов держатся. Блокирую из-за F1 (гейт может уронить весь импорт на ≤3.10 — правка в 9 символов) и F2 (потеря детекции входа плюс комментарий, обещающий несуществующую проверку); F3 и F4 настоятельно рекомендую в тот же заход.

🧒 **Простыми словами:** пять вещей, которые просили починить, — починены: архив больше не стирается, чужая машина не трогается, галочка в настройках видна, повторные файлы считаются за один. Но в коде осталась мина: если на какой-то машине Python постарее, то одна новая строчка уронит весь импорт целиком. И сломался «счётчик на входе»: раньше он замечал, что на диске лежат новые сессии, которых нет в базе, а теперь считает так, что заметить их физически не может — при этом рядом написан комментарий «мы это проверяем в другом месте», а в другом месте проверки нет. Ещё старый механизм успел растащить часть заметок в папку «источник пропал», его выключили, а разложить обратно забыли.

VERDICT: REQUEST_CHANGES
