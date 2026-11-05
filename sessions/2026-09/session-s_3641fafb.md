---
session: s_3641fafb
date: 2026-09-22
words: 1753
turns: 2
tools: "Bash, Write"
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-22 · Ты независимый старший ревьюер. Это второй проход после REQUEST_CHANGES. Проверь итоговый…

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_3641fafb` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

Ты независимый старший ревьюер. Это второй проход после REQUEST_CHANGES. Проверь итоговый diff Codex-фильтра. Особо попробуй снова: пустой sessions-dir не должен удалять архив; explicit --sessions-dir не должен трогать другой дом; локальный provenance не должен менять peer node; multiline TOML SESSIONS=true должен дать красный сигнал; resume-файлы считаются одним ID. Запусти тесты/ломатели если нужно. Только доказуемые findings с file:line и severity. Заверши ровно VERDICT: APPROVE или VERDICT: REQUEST_CHANGES.
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

[⏰ вторник, день, 14:25, 22 сентября 2026]

**Рельсы:** ревью делаю сам как Claude (чтение кода + суждение). `second_opinion>codex` мимо — автор диффа и есть Codex.

Смотрю фактический код на диске, а не только diff.

---

> `Bash` -- {"command": "sed -n '180,260p' codex/codex_lib.py", "description": "Read harness_session_import_enabled"}

---

> `Bash` -- {"command": "grep -n \"unique_sessions_on_disk\\|def do_import\\|def write_freshness\\|def sweep_stale_notes\\|def build_notes\\|def upsert\\|def notes_dir\\|def quarantine_notes\\|def archive_originals\" codex/codex_lib.py", "description": "Locate key functions"}

---

> `Bash` -- {"command": "sed -n '120,175p' codex/codex_lib.py; echo ---; sed -n '425,545p' codex/codex_lib.py", "description": "Read unique_sessions_on_disk and notes fns"}

---

> `Bash` -- {"command": "sed -n '560,800p' codex/codex_lib.py", "description": "Read quarantine/freshness/do_import"}

---

> `Bash` -- {"command": "grep -rn \"reconcile_missing_sources\\|write_freshness\\|do_import\\|_missing-source\" --include=*.py --include=*.md --include=*.cmd --include=*.ps1 . | grep -v \"^./codex/codex_lib.py\" | head -40; echo \"=== DB/paths ===\"; sed -n '1,60p' codex/codex_lib.py", "description": "Find call

---

> `Bash` -- {"command": "python -c \"import sys;print(sys.version)\"; grep -rn \"tomllib\\|toml\" --include=*.py codex/ | head", "description": "Check python version and tomllib usage"}

---

> `Bash` -- {"command": "timeout 100 grep -rn \"reconcile_missing_sources\\|write_freshness(\\|do_import(\\|_missing-source\" --include=*.py codex/ *.py 2>/dev/null | head -30", "description": "Grep callers in codex dir and root"}

---

> `Bash` -- {"command": "sed -n '1,60p' codex/codex_lib.py", "description": "Read header/paths"}

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/codex && ls -la | head -20 && python -c \"\nimport sqlite3\nc=sqlite3.connect('codex_sessions.db')\nprint(c.execute('select machine,count(*) from sessions group by machine').fetchall())\n\"", "description": "Inspect codex DB machines"}

---

> `Bash` -- {"command": "timeout 300 python _test_external_agent_import_filter.py; echo \"EXIT=$?\"", "description": "Run the filter test"}

---

> `Bash` -- {"command": "sed -n '1,135p' /e/Obsidian/_imports/codex/_test_external_agent_import_filter.py", "description": "Read full test"}

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports && sed -n '900,1045p' codex/codex_lib.py", "description": "Read selftest and main"}

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports && timeout 200 grep -rln \"external_agent_sessions_excluded\\|input_archive_delta\\|codex_lib\\|_freshness.json\" --include=*.py --include=*.ps1 --include=*.cmd . 2>/dev/null | head -20", "description": "Find consumers of freshness and codex_lib"}

---

> `Bash` -- {"command": "cat .stignore 2>/dev/null | head -30; echo \"=== freshness check ===\"; grep -n \"codex\\|mismatch\\|unique_sessions\" chatgpt/chatgpt_freshness_check.py | head -40", "description": "Check stignore and freshness watchdog"}

---

> `Bash` -- {"command": "timeout 120 grep -rn \"version_info\" --include=*.py . 2>/dev/null | grep -v stversions | head -20; echo \"=== fleet nodes ===\"; python -c \"\nimport json,os\np=os.path.expanduser('~/.claude/fleet_nodes.json')\nd=json.load(open(p,encoding='utf-8'))\nprint(json.dumps(d,ensure_ascii=Fals

---

> `Bash` -- {"command": "cat > _scratch/breaker_codex_r2.py <<'EOF'\n# -*- coding: utf-8 -*-\nimport importlib.util, json, sqlite3, tempfile, builtins, sys\nfrom pathlib import Path\nHERE = Path(\"D:/Vault/_imports/codex\")\ndef load():\n    spec = importlib.util.spec_from_file_location(\"cl_%d\" % len(sys.m

---

> `Write` -- {"file_path": "C:\\Users\\dev\\AppData\\Local\\Temp\\breaker_codex_r2.py", "content": "# -*- coding: utf-8 -*-\nimport importlib.util, json, sqlite3, tempfile, builtins, sys, shutil\nfrom pathlib import Path\nHERE = Path(\"D:/Vault/_imports/codex\")\ndef load():\n    spec = importlib.util.spec_

---

> `Bash` -- {"command": "cd /c/Users/dev/AppData/Local/Temp && timeout 300 python breaker_codex_r2.py 2>&1 | grep -Ev \"^codex import|^  |^codex:\"", "description": "Run breaker suite"}

---

> `Bash` -- {"command": "cd /c/Users/dev/AppData/Local/Temp && sed -i 's|/r%d.jsonl|/rollout-r%d.jsonl|; s|/mine.jsonl|/rollout-mine.jsonl|; s|/o%d.jsonl|/rollout-o%d.jsonl|; s|/a.jsonl|/rollout-a.jsonl|; s|/b-resume.jsonl|/rollout-b-resume.jsonl|; s|/g.jsonl|/rollout-g.jsonl|' breaker_codex_r2.py && timeout 

---

> `Bash` -- {"command": "timeout 300 python codex/codex_lib.py --selftest 2>&1 | tail -25", "description": "Run codex_lib selftest"}

---

> `Bash` -- {"command": "timeout 120 grep -rln \"codex/_freshness\\|codex._freshness\\|codex_sessions.db\\|codex_lib.py\" /c/Users/dev/.claude/scripts /c/Users/dev/.claude/skills 2>/dev/null | head -15", "description": "Find external consumers of codex freshness"}

---

> `Bash` -- {"command": "timeout 90 grep -rhoE \"[Pp]ython ?3\\.(9|10|11|12|13)[0-9.]*\" /c/Users/dev/.claude/*.md /c/Users/dev/.claude/*.json 2>/dev/null | sort | uniq -c | sort -rn | head; echo \"=== bus health ===\"; timeout 60 grep -rhoE \"\\\"python\\\": *\\\"[^\\\"]+\\\"|python_version[^,]*\" /e/Obsid

---

> `Bash` -- {"command": "grep -n \"import tomllib\\|except (ValueError, UnicodeDecodeError)\\|table_sessions = re.search\\|(?mis)\\|if machine and node.name != machine\\|input_archive_delta\\|mismatch = total - notes\" codex/codex_lib.py", "description": "Get exact line numbers"}
