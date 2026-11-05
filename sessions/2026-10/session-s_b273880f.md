---
session: s_b273880f
date: 2026-10-02
words: 2403
turns: 1
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-10-02 · READ-ONLY INDEPENDENT REVIEW. Do not edit files, launch other reviewers, or send messages…

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_b273880f` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

READ-ONLY INDEPENDENT REVIEW. Do not edit files, launch other reviewers, or send messages. Return ACCEPT or COUNTER with specific file:line findings. Read the following local files yourself. This is revision 2, superseding revision 1.
Author Codex; reviewer must independently try to disprove correctness.
Repository C:/Users/dev/.claude/scripts
Commits 84cd120d9 and 81e1a18da; compare 84cd120d9^..81e1a18da, scoped to registry_wake.py, _test_registry_wake_dependencies.py, docs/registry_wake.md.
registry_wake.py sha256 0ca874e36b95d7d6bde48f30e8ed10d0e1c46502d2aa6eb85d607262e98c8e1d
_test_registry_wake_dependencies.py sha256 5bec954f053c4aed7d7174610711370d3bb1909a93fc423699c8718938fbe67c
docs/registry_wake.md sha256 c49314b43e3d6441c6bb58eab0e7e2ab64f7dc6ce6234cf76c96af07c4602581
Requirements: quoted YAML dependency arrays, scalar wikilinks and multiline lists resolve. Every dependency must be found and final before UNBLOCKED. Missing/open/invalid dependency must not disappear. Empty [] means no dependencies. DUE policy remains unchanged: date means review, not unconditional execution.
Revision 2 corrects a P1: a blank multiline item formerly terminated parsing and hid later open dependencies. It now preserves invalid sentinels and continues reading. Seven isolated unittest cases and legacy registry selftest pass. Tests use temp cards and fresh repair_items lambda lists; negative control proves old shared return_value list contamination.
Also inspect E:/!CLAUDE-HUBPC-June26/_scratch/canon-debts-20261001/6/verify.py. It must not write production task cards or start sessions. Observational dispatcher selection can be false because queue capacity is occupied; isolated selection must pass. Behavioral canon acceptance remains open.
Look especially for silent dropping of unresolved blockers, quote/comment/list parsing bugs, tests that falsely pass, and accidental production mutations. Report what you actually inspected and any verification limitations. Do not claim fleet deployment or behavioral acceptance.

ALL SOURCE BELOW. Answer with final review, not a plan or promise. Do not use tools; inspect included source.

FILE registry_wake.py
#!/usr/bin/env python3
# -*- coding: utf-8 -*-
"""registry_wake.py -- БУДИЛЬНИК реестра: поднимает задачи, у которых наступил срок или закрылись зависимости.

ЗАЧЕМ (приказ dev 05.08.2026, голосом): «мы решили померить через месяц и через месяц однозначно
забудем». Замер того же дня показал, что это не гипотеза, а факт: в реестре 592 карточки, схема почти
полная (state/priority/owner/review_after/blocked_by/blocks/related/born_from/evidence/supersedes) --
и при этом **57 задач с НАСТУПИВШИМ `review_after`, которых никто не разбудил**, самая старая ждала с
12 июля. Поле было, дверь была, будильника не было: `tasks_index.py` читает `review_after` только чтобы
нарисовать «припаркована до X», а на саму дату не реагирует никто.

ЧЕМ ЭТО НЕ ЯВЛЯЕТСЯ. Это НЕ новый реестр. Пятая свалка рядом с четырьмя существующими -- ровно тот
исход, из-за которого гниют нынешние (78 задач без хода). Источник истины остаётся один:
`$OBSIDIAN_VAULT/10-Tasks/task-*.md`. Витрину по-прежнему строит ТОЛЬКО `tasks_index.py` на Маяке
(один писатель на дериват), этот робот НИЧЕГО не пишет в дерево задач -- он читает и будит.

ЧТО ПОДНИМАЕТ (4 корзины, по убыванию срочности):
  🔔 DUE        -- `review_after` <= сегодня, задача жива. Пора: проверить / замерить / запустить /
                   отменить / перенести. Это главный класс, ради которого робот и написан.
  🔓 UNBLOCKED  -- в `blocked_by` перечислены задачи, и ВСЕ они уже done/dropped => можно делать.
                   Реализует «после A, B, C можно делать D» без ручного обхода.
  🥀 ROTTING    -- open/wip, нет `review_after`, `touched_at` старше ROT_DAYS. Задача без даты и без
                   хода = задача, о которой забыли; молчание тут неотличимо от порядка.
  ⏰ SOON       -- `review_after` в ближайшие SOON_DAYS: предупреждение, чтобы срок не наступал внезапно.

ВЫХОД. Печатает дайджест; `--post` шлёт ОДНО сообщение в шину (bus_send -> TG 03 + файловая рельса).
Кулдаун COOLDOWN_H защищает от «сторож, который орёт каждый тик» -- но КРАСНЫЙ остаётся красным:
кулдаун глушит мегафон, не вердикт.

КОДЫ ВЫХОДА. 0 = будить некого (тишина заслужена) · 1 = есть что будить · 3 = будить надо, но обе
рельсы шины мертвы (громко в лог, иначе сбой доставки выглядит как «всё тихо»).

ГРАНИЦА ЧЕСТНОСТИ. Робот НЕ решает судьбу задачи и не двигает даты сам: он приносит список и варианты
действия. Решение (проверить/замерить/запустить/отменить/перенести) остаётся за человеком или за
сессией, которую он поднимет. Автоматически двигать `review_after` = тихо хоронить задачу второй раз.

ЗАПУСК: ежедневно ~05:00 Лиссабон (утренний слот, задача «Claude Registry Wake»).
Тест: scripts/_test_registry_wake.py · паспорт: scripts/docs/registry_wake.md
"""
from __future__ import annotations

import argparse, ast, datetime, glob, io, os, re, subprocess, sys, time

try:
    sys.stdout.reconfigure(encoding="utf-8"); sys.stderr.reconfigure(encoding="utf-8")
except Exception:
    pass

HOME = os.path.expanduser("~")
BUS = os.path.join(HOME, ".claude", "scripts", "bus_send.py")
HEARTBEAT = os.path.join(HOME, ".claude", "scripts", "cron_heartbeat.py")
TASK = "registry-wake"
MUTE = os.path.join(HOME, ".claude", "scripts", "_%s.mute" % TASK)
COOLDOWN_H = 20          # один будильник в сутки; тот же список дважды за день никто не читает

ROT_DAYS = 30            # open/wip без даты и без движения дольше этого = забыли
SOON_DAYS = 3            # предупреждаем за столько дней до срока
FINAL = {"done", "dropped", "archived"}

DATE_RE = re.compile(r"(\d{4}-\d{2}-\d{2})")


def vault():
    v = os.environ.get("OBSIDIAN_VAULT")
    if v and os.path.isdir(v):
        return v
    # пер-машинный запас: скрипты читают machine.env, когда env сессии недоступен
    menv = os.path.join(HOME, ".claude", "machine.env")
    if os.path.exists(menv):
        for line in io.open(menv, encoding="utf-8", errors="ignore"):
            if line.strip().startswith("OBSIDIAN_VAULT"):
                cand = line.split("=", 1)[1].strip().strip('"')
                if os.path.isdir(cand):
                    return cand
    return None


def parse_front(path):
    """Read scalar metadata and dependency lists (inline or block), stdlib only.

    Dependency parsing is deliberately separate from scalar display fields:
    quoted YAML arrays must not turn into unresolvable quoted wikilinks.
    """
    try:
        with io.open(path, encoding="utf-8-sig", errors="ignore") as stream:
            txt = stream.read()
    except Exception:
        return None
    if not txt.startswith("---"):
        return None
    end = txt.find("\n---", 3)
    fm = txt[3:end if end > 0 else 2000]
    out = {"file": os.path.basename(path), "path": path, "body": txt}
    for key in ("state", "status", "priority", "prio", "owner", "title", "review_after",
                "touched_at", "created_at", "date", "type"):
        m = re.search(r"^%s:\s*(.+)$" % key, fm, re.M)
        if m:
            out[key] = m.group(1).split("#")[0].strip().strip('"').strip("'")
    m = re.search(r"^blocked_by:[ \t]*(.*)$", fm, re.M)
    if m:
        raw = m.group(1).strip()
        if not raw or raw.startswith('#'):
            items = []
            for line in fm[m.end():].splitlines():
                if not line.strip() or line.lstrip().startswith('#'):
                    continue
                if re.match(r'^[^ \t-][^:]*:', line):
                    break
                item = re.match(r"^[ \t]*-(?:[ \t]+(.*))?$", line)
                if item:
                    refs = dependency_refs(item.group(1) or '')
                    items.extend(refs or ['<invalid-empty-dependency>'])
                else:
                    items.append('<invalid-dependency-line>')
            out['blocked_by'] = items
        else:
            out['blocked_by'] = dependency_refs(raw)
    out["state"] = (out.get("state") or out.get("status") or "open").lower()
    out["priority"] = out.get("priority") or out.get("prio") or "P2"
    return out


def as_date(val):
    if not val:
        return None
    m = DATE_RE.search(str(val))
    if not m:
        return None
    try:
        return datetime.date.fromisoformat(m.group(1))
    except Exception:
        return None


def slug_of(ref):
    """Из `[[task-...]]` / `task-....md` / голого слага делает сравнимый ключ."""
    s = str(ref).strip().strip('"\'').strip()
    if s.startswith('[[') and s.endswith(']]'):
        s = s[2:-2].split('|', 1)[0].split('#', 1)[0].strip()
    if s.endswith('.md'):
        s = s[:-3]
    return s.rsplit("/", 1)[-1].strip().lower()


def dependency_refs(raw):
    """Supported card notation: quoted arrays, block items, legacy scalar refs.

    Preserve malformed/unknown entries instead of dropping them: collect may
    unblock only when EVERY reference is found and final. No general YAML eval.
    """
    if isinstance(raw, (list, tuple)):
        return [str(x) if str(x).strip() else '<invalid-empty-dependency>' for x in raw]
    text = str(raw or '').strip()
    text = re.sub(r'\s+#.*$', '', text).strip()
    if not text or text in ('[]', 'null', '~'):
        return []
    if text.startswith('[') and not text.startswith('[['):
        try:
            values = ast.literal_eval(text)
        except (SyntaxError, ValueError):
            return [text]
        if not isinstance(values, list):
            return [text]
        return [str(x) for x in values]
    return [x.strip().strip('"\'') for x in re.split(r'[,;]', text) if x.strip()]


def collect(today, root=None):
    root = root or vault()
    if not root:
        return None
    cards = []
    for p in sorted(glob.glob(os.path.join(root, "10-Tasks", "task-*.md"))):
        fm = parse_front(p)
        if fm:
            cards.append(fm)
    by_slug = {slug_of(c["file"]): c for c in cards}

    due, unblocked, rotting, soon, prose_blockers = [], [], [], [], []
    for c in cards:
        if c["state"] in FINAL:
            continue
        ra = as_date(c.get("review_after"))
        if ra and ra <= today:
            due.append(c)
        elif ra and (ra - today).days <= SOON_DAYS:
            soon.append(c)

        blockers = dependency_refs(c.get("blocked_by", ""))
        if blockers:
            resolved, known = [], []
            for b in blockers:
                tgt = by_slug.get(slug_of(b))
                if tgt:
                    known.append(tgt)
                    if tgt["state"] in FINAL:
                        resolved.append(tgt)
            # Every declared dependency must exist and be final, including missing refs.
            if len(resolved) == len(blockers) and c["state"] in ("open", "blocked", "someday", "inbox"):
                unblocked.append(c)
            # Блокер, записанный ПРОЗОЙ («решение оператора», «синк не доехал»), машине не виден:
            # он никогда не «закроется» сам и задача будет ждать вечно. Молчать об этом нельзя,
            # иначе пустая корзина 🔓 читается как «зависимостей нет» вместо «их нечем проверить».
            if len(known) != len(blockers):
                prose_blockers.append(c)

        if c["state"] in ("open", "wip") and not ra:
            moved = as_date(c.get("touched_at")) or as_date(c.get("created_at")) or as_date(c.get("date"))
            if moved and (today - moved).days >= ROT_DAYS:
                rotting.append(c)

    order = {"P0": 0, "P1": 1, "P2": 2, "P3": 3}
    key = lambda c: (order.get(c.get("priority", "P2"), 9), as_date(c.get("review_after")) or today)
    return {"due": sorted(due, key=key), "unblocked": sorted(unblocked, key=key),
            "rotting": sorted(rotting, key=key), "soon": sorted(soon, key=key),
            "prose_blockers": sorted(prose_blockers, key=key), "total": len(cards)}


def line(c, today):
    ra = as_date(c.get("review_after"))
    age = (" · просрочен %d дн" % (today - ra).days) if ra and ra <= today else ""
    title = (c.get("title") or c["file"]).strip('"')[:58]
    return "  [%s] %s%s · %s" % (c.get("priority", "P2"), title, age, c["file"])


def render(res, today):
    out = []
    out.append("== БУДИЛЬНИК РЕЕСТРА %s · карточек %d ==" % (today.isoformat(), res["total"]))
    if res["due"]:
        out.append("🔔 СРОК НАСТУПИЛ (%d) -- проверить / замерить / запустить / отменить / перенести:" % len(res["due"]))
        out += [line(c, today) for c in res["due"][:12]]
        if len(res["due"]) > 12:
            out.append("  ... ещё %d (полный список: --json)" % (len(res["due"]) - 12))
    if res["unblocked"]:
        out.append("🔓 ЗАВИСИМОСТИ ЗАКРЫТЫ (%d) -- можно делать:" % len(res["unblocked"]))
        out += [line(c, today) for c in res["unblocked"][:8]]
    if res["rotting"]:
        out.append("🥀 БЕЗ ДАТЫ И БЕЗ ХОДА >%dдн (%d) -- дать дату или закрыть:" % (ROT_DAYS, len(res["rotting"])))
        out += [line(c, today) for c in res["rotting"][:6]]
        if len(res["rotting"]) > 6:
            out.append("  ... ещё %d" % (len(res["rotting"]) - 6))
    if res["soon"]:
        out.append("⏰ срок в ближайшие %d дн: %d" % (SOON_DAYS, len(res["soon"])))
    if res.get("prose_blockers"):
        out.append("🧱 блокер записан прозой, машина его не проверит (%d) -- заменить на ссылку [[task-...]], "
                   "иначе задача ждёт вечно" % len(res["prose_blockers"]))
    if not (res["due"] or res["unblocked"] or res["rotting"]):
        out.append("тихо: будить некого")
    return "\n".join(out)


def _muted():
    try:
        return os.path.exists(MUTE) and (time.time() - os.path.getmtime(MUTE)) / 3600.0 < COOLDOWN_H
    except Exception:
        return False


def _mark():
    try:
        io.open(MUTE, "w", encoding="utf-8").write(time.strftime("%Y-%m-%dT%H:%M"))
    except Exception:
        pass


def _heartbeat():
    try:
        subprocess.run([sys.executable, HEARTBEAT, TASK], capture_output=True, timeout=30)
    except Exception:
        pass


def main(argv=None):
    ap = argparse.ArgumentParser(description="будильник реестра задач")
    ap.add_argument("--post", action="store_true", help="отправить дайджест в шину (TG 03)")
    ap.add_argument("--json", action="store_true")
    ap.add_argument("--selftest", action="store_true")
    a = ap.parse_args(argv)

    if a.selftest:
        return selftest()

    today = datetime.date.today()
    res = collect(today)
    if res is None:
        print("НЕ НАЙДЕН ВОЛТ: ни OBSIDIAN_VAULT, ни machine.env не дали существующий путь")
        return 3
    if a.json:
        import json as _j
        print(_j.dumps({k: ([c["file"] for c in v] if isinstance(v, list) else v)
                        for k, v in res.items()}, ensure_ascii=False, indent=1))
    else:
        print(render(res, today))

    need = bool(res["due"] or res["unblocked"] or res["rotting"])
    if not need:
        _heartbeat()
        return 0
    if not a.post:
        _heartbeat()
        return 1
    if _muted():
        print("[cooldown] будильник уже звонил за последние %d ч" % COOLDOWN_H)
        _heartbeat()
        return 1
    msg = "⏰ БУДИЛЬНИК РЕЕСТРА\n" + render(res, today) + \
          "\n\nдействие на каждую: проверить · замерить · запустить · отменить · перенести (review_after в будущее с причиной)"
    sent = False
    try:
        r = subprocess.run([sys.executable, BUS, msg], capture_output=True, text=True,
                           encoding="utf-8", errors="replace")
        sent = r.returncode in (0, 1)
    except Exception as e:
        print("bus_send failed: %s" % e)
    if sent:
        _mark()
    _heartbeat()
    if not sent:
        print("БУДИТЬ НАДО, НО ОБЕ РЕЛЬСЫ ШИНЫ МЕРТВЫ")
        return 3
    return 1


# ---------------------------------------------------------------- самотест
def selftest():
    import tempfile, shutil
    today = datetime.date(2026, 8, 5)
    tmp = tempfile.mkdtemp(prefix="regwake-")
    tdir = os.path.join(tmp, "10-Tasks")
    os.makedirs(tdir)

    def card(name, **fm):
        body = "---\n" + "".join("%s: %s\n" % (k, v) for k, v in fm.items()) + "---\ntext\n"
        io.open(os.path.join(tdir, name), "w", encoding="utf-8").write(body)

    card("task-2026-06-01-overdue.md", state="open", priority="P1", title="просроченный замер",
         review_after="2026-07-01")
    card("task-2026-08-01-future.md", state="open", priority="P2", title="будущий замер",
         review_after="2026-09-01")
    card("task-2026-08-04-soon.md", state="open", priority="P2", title="скоро", review_after="2026-08-06")
    card("task-2026-05-01-blocker.md", state="done", priority="P1", title="блокер закрыт")
    card("task-2026-05-02-blocked.md", state="blocked", priority="P0", title="ждал блокера",
         blocked_by="[[task-2026-05-01-blocker]]")
    card("task-2026-05-03-stillblocked.md", state="blocked", priority="P1", title="блокер жив",
         blocked_by="[[task-2026-08-01-future]]")
    card("task-2026-01-01-rot.md", state="open", priority="P3", title="гниёт без даты",
         touched_at="2026-01-05")
    card("task-2026-08-05-fresh.md", state="open", priority="P2", title="свежая", touched_at="2026-08-05")
    card("task-2026-04-01-donedate.md", state="done", priority="P1", title="закрытая с датой",
         review_after="2026-06-01")

    r = collect(today, root=tmp)
    fails = []
    names = lambda k: {c["file"] for c in r[k]}

    if "task-2026-06-01-overdue.md" not in names("due"):
        fails.append("не разбудил просроченную задачу -- ради этого робот и написан")
    if "task-2026-04-01-donedate.md" in names("due"):
        fails.append("будит ЗАКРЫТУЮ задачу: шум, из-за которого будильник выключат")
    if "task-2026-08-01-future.md" in names("due"):
        fails.append("будит задачу с будущей датой")
    if "task-2026-05-02-blocked.md" not in names("unblocked"):
        fails.append("не заметил, что все блокеры закрыты (правило 'после A,B,C можно D')")
    if "task-2026-05-03-stillblocked.md" in names("unblocked"):
        fails.append("объявил разблокированной задачу с живым блокером -- ложный вызов")
    if "task-2026-01-01-rot.md" not in names("rotting"):
        fails.append("не поймал гниющую задачу без даты")
    if "task-2026-08-05-fresh.md" in names("rotting"):
        fails.append("объявил свежую задачу гниющей")
    if "task-2026-08-04-soon.md" not in names("soon"):
        fails.append("не предупредил о сроке через день")

    # пустой реестр: тишина заслужена, но не должна падать
    empty = os.path.join(tmp, "empty")
    os.makedirs(os.path.join(empty, "10-Tasks"))
    e = collect(today, root=empty)
    if e is None or e["due"] or e["rotting"]:
        fails.append("пустой реестр не даёт чистую тишину")

    shutil.rmtree(tmp, ignore_errors=True)
    print("SELFTEST: due=%d unblocked=%d rotting=%d soon=%d (на фикстурах)" %
          (len(r["due"]), len(r["unblocked"]), len(r["rotting"]), len(r["soon"])))
    if fails:
        for f in fails:
            print("  ❌", f)
        return 1
    print("SELFTEST: ✅ будит просроченное и разблокированное, молчит про закрытое, будущее и свежее")
    return 0


if __name__ == "__main__":
    # CRASH-GUARD (§5.5, класс «Regression Nightly 29.07», повтор 11.08.2026). exit=1 у этого
    # робота вписан в карту сигналов как «есть кого будить И дайджест доставлен». Python на
    # НЕОБРАБОТАННОМ исключении выходит РОВНО С ТЕМ ЖЕ кодом 1 — значит без обёртки смерть
    # будильника (нет волта, битый machine.env) читалась бы табло как штатная находка =
    # ложная тишина. 4 = «сам упал», в signal НЕ вписан -> табло краснеет громко.
    # Порядок принципиален: сначала guard, потом строка в expected_exit_codes.json.
    # Гейт: scripts/_test_crash_guard.py
    try:
        sys.exit(main())
    except SystemExit:
        raise
    except BaseException as exc:
        try:
            sys.stderr.write("CRASH registry_wake: %r\n" % (exc,))
        except Exception:
            pass
        sys.exit(4)

FILE _test_registry_wake_dependencies.py
"""Isolated dependency-reader/dispatcher regressions. No network or live writes."""
import datetime
from pathlib import Path
import tempfile
import unittest
from unittest.mock import patch

import registry_wake as W
import registry_dispatch as D


class Dependencies(unittest.TestCase):
    def setUp(self):
        self.tmp = tempfile.TemporaryDirectory(prefix='registry-dependencies-')
        self.addCleanup(self.tmp.cleanup)
        self.root = Path(self.tmp.name)
        (self.root / '10-Tasks').mkdir()
        self.today = datetime.date(2026, 10, 2)
        self.card('task-a', 'done')
        self.card('task-b', 'open')

    def card(self, name, state='open', dependency='[]', date='2026-10-17'):
        p = self.root / '10-Tasks' / (name + '.md')
        p.write_text(f'---\nstate: {state}\npriority: P2\ntype: infra\nreview_after: {date}\nblocked_by: {dependency}\n---\nbody\n', encoding='utf-8')
        return p

    def buckets(self):
        return {k: {c['file'] for c in v} for k, v in W.collect(self.today, str(self.root)).items() if isinstance(v, list)}

    def test_resolved_forms(self):
        for dep in ('["[[task-a]]"]', "['[[task-a]]']", '[[task-a]]', 'task-a.md', '\n  - "[[task-a]]"', '["[[task-a]]"] # resolved'):
            with self.subTest(dep=dep):
                self.card('task-target', dependency=dep)
                self.assertIn('task-target.md', self.buckets()['unblocked'])

    def test_missing_and_open_never_unblock(self):
        for dep in ('["[[task-a]]", "[[task-missing]]"]', '[[task-a]], [[task-missing]]', '["[[task-a]]", "[[task-b]]"]'):
            with self.subTest(dep=dep):
                self.card('task-target', dependency=dep)
                self.assertNotIn('task-target.md', self.buckets()['unblocked'])

    def test_unknown_visible(self):
        self.card('task-target', dependency='["[[task-a]]", "[[task-missing]]"]')
        self.assertIn('task-target.md', self.buckets()['prose_blockers'])

    def test_invalid_middle_block_item_fails_closed(self):
        for middle in ('  -', '  - null', '  - # empty', '    unsupported: value'):
            with self.subTest(middle=middle):
                self.card('task-target', dependency='\n  - "[[task-a]]"\n' + middle + '\n  - "[[task-b]]"')
                b = self.buckets()
                self.assertNotIn('task-target.md', b['unblocked'])
                self.assertIn('task-target.md', b['prose_blockers'])

    def test_empty_not_blocked(self):
        self.card('task-target', dependency='[]', date='2026-10-01')
        b = self.buckets()
        self.assertIn('task-target.md', b['due'])
        self.assertNotIn('task-target.md', b['prose_blockers'])

    def test_dispatch_fresh_calls(self):
        self.card('task-target', dependency='["[[task-a]]"]')
        # Fresh list per call: pick appends to repair_items() output.
        with patch.object(D, 'repair_items', side_effect=lambda: []), patch.object(D, 'load_ledger', return_value={}), patch.object(D, 'seen_on_disk', return_value={}):
            first = D.pick(self.today, str(self.root))
            second = D.pick(self.today, str(self.root))
        self.assertEqual([x['card'] for x in first], ['task-target.md'])
        self.assertEqual(first, second)
        self.assertIsNot(first, second)

    def test_mutable_mock_negative_control(self):
        self.card('task-target', date='2026-10-01')
        with patch.object(D, 'repair_items', return_value=[]), patch.object(D, 'load_ledger', return_value={}), patch.object(D, 'seen_on_disk', return_value={}):
            first = D.pick(self.today, str(self.root))
            second = D.pick(self.today, str(self.root))
        self.assertIs(first, second)  # reproduces the old fixture's shared state


if __name__ == '__main__':
    unittest.main()
