---
session: s_2d94f76b
date: 2026-10-20
words: 1849
turns: 4
tools: "Bash, Skill"
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-10-20 · You are the ALPHA-JUDGE running unattended over the CHANNEL lane. UNATTENDED MEANS: there…

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_2d94f76b` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

You are the ALPHA-JUDGE running unattended over the CHANNEL lane. UNATTENDED MEANS: there is NO human in this session — NEVER ask a question, never offer options, never wait for permission. If a file is unreadable, silently proceed with what you CAN read and write one honest line saying which check was degraded. Asking = producing nothing.

---

> `Skill` -- {"skill": "alpha-judge", "args": "channel"}

---

**User:**

Base directory for this skill: C:\Users\dev\.claude\skills\alpha-judge

# 🅰️⚖️ /alpha-judge — the reusable LLM-judge for every alpha miner

> 🧒 **When reporting to dev:** end with a child-simple "Простыми словами" recap (his standing request; reports TO dev only).

The alpha-extraction engine = **cheap deterministic detector (0 tokens) → LLM judge → weekly ≤10 + yes/no calibration**, repeated for each of the 10 miners. The DETECTORS are per-miner scripts in `$IMPORTS_ROOT/alpha/`. The JUDGE is the SAME logic every time — so it lives HERE, once, and is reused. Canon: `02-Decisions\decision-alpha-extraction-engine-variant-a`; memory [[alpha-extraction-engine]].

## Model policy (per [[model-routing-sonnet-grunt]] + dev's 2026-06-14 session override)
- **In-session, now:** judge on **Opus** (dev steers; he'll say when to switch to Sonnet as Opus nears its limit).
- **Nightly unattended:** **Sonnet** (idle free bucket) via `judge_nightly.cmd` (headless `claude -p --model sonnet`). LIVE + verified 2026-06-15 — Windows task "Alpha Judge Nightly" Mon 05:00, chained after the 04:15 scan. **Now judges ALL 10 miners** (was bets-only; expanded 2026-06-15) — one headless session reads THIS spec, loops the registry, applies the dedup-vs-home gate, writes each `<miner>-judged-latest.md`. **Vault writes are forbidden in nightly mode** (judge-only; home-note additions wait for dev's in-session approval). (Auth is in the Windows keychain; check with `claude auth status`, re-login via `claude auth login`. Keep `.cmd` pure-ASCII.)
- The judge is grunt-classification → Sonnet is the natural default once the session-override lifts.

## Miner registry (detector → home → verdict scheme)
| miner key | candidates file (in `_imports\alpha\candidates\`) | ledger db | curated HOME note (feeds, never duplicates) | verdict scheme |
|---|---|---|---|---|
| `bets` | `bets-report-latest.md` | `bets_ledger.db` (table `bets`) | `insight-prediction-ledger` | ✅ сбылось · ❌ не сбылось · 🔁 ещё открыто · 🗑 не ставка |
| `contradictions` | `contra-report-latest.md` | `contra_ledger.db` (`pairs`+`claims`) | `insight-contradictions` | ✅ реальное противоречие · 🟡 эволюция мнения · 🗑 шум |
| `stance` | `stance-report-latest.md` | `stance_ledger.db` (`shifts`+`pairs`) | `insight-contradictions` (§«готов менять мнение») | ✅ реальный сдвиг взгляда (раньше А→теперь Б) · 🟡 уточнение, не сдвиг · 🗑 шум |
| `bridge` | `bridge-report-latest.md` | `bridge_ledger.db` | `insight-worldview-throughlines` | ✅ неочевидный ценный мост между доменами · 🟡 ожидаемая связь · 🗑 случайное со-упоминание |
| `recurring` | `recurring-report-latest.md` | `recurring_ledger.db` | `insight-worldview-throughlines` | ✅ настоящая повторяющаяся убеждённость · 🟡 операц. повтор · 🗑 со-частотность служебных слов |
| ~~`leadsignal`~~ ⛔ RETIRED 2026-07-16 | `leadsignal-report-latest.md` | `leadsignal_ledger.db` | точность 42.9% на эталоне оператора (111🟡/27🔴, 2026-07-05) — лиды живут в `/pipeline`, не в ленте инсайтов. Скрипт на диске, из weekly/judge/harvest выключен | — |
| `novelty` | `novelty-report-latest.md` | `novelty_ledger.db` | `insight-novelty-ideas` (СОЗДАТЬ при первом ✅) | ✅ действительно новая идея · 🟡 вариация известного · 🗑 редкие слова без идеи |
| `identity` | `identity-report-latest.md` | `identity_ledger.db` | `_Self-Bible-MOC` (+ `concept-*` «что я думаю») | ✅ настоящее само-определение (ценность/принцип) · 🟡 ситуативное · 🗑 не про идентичность |
| `openq` | `openq-report-latest.md` | `openq_ledger.db` | `insight-open-questions` ✅ (создан 2026-06-15, 25 вопросов; +226 Detector-A ждут) | ✅ реальный открытый вопрос оператора · 🟡 риторический · 🗑 чужой/служебный |
| ~~`orphan`~~ ⛔ RETIRED 2026-07-16 | `orphan-insight-report-latest.md` | `orphan_insight_ledger.db` | точность 37.5% на эталоне оператора — промахи = рабочие протоколы команды из `05-Resources` (evidence-слой, несвязанность там норма). Сироты-инсайты ловит `/relink --deep`. Скрипт на диске, из weekly/judge/harvest выключен | — |
| `screenpipe` | `screenpipe-report-latest.md` | `screenpipe_ledger.db` (table `candidates`) | `insight-ambient-voice-alpha` (СОЗДАТЬ при первом ✅). Корпус = речь вслух с хаба (sp_harvest → `_originals\screenpipe\`); транскрипт шумный (whisper free tier + эхо Meet) — суди СМЫСЛ, не форму; чужая речь из системного звука = не альфа оператора | ✅ альфа (решение/идея/ставка оператора) · 🟡 сырая мысль, наблюдать · 🗑 шум/бытовое/чужое |

## Flow (what YOU do)
1. **Pick the miner** from the arg (default `bets` if none; if unclear, ask). Read its candidates file (or query its db for the top unjudged candidates — cap ~25; never the whole corpus).
2. **RECALL the HOME note** (e.g. `insight-prediction-ledger` / `insight-contradictions`) so you DON'T re-propose what's already catalogued. Token-cheap: read only that one note + the candidate digest.
3. **JUDGE each candidate** against the miner's core question — *"is this dev'S OWN <X-of-the-right-type>, not noise / not someone else's / not a restatement?"* Classify per the verdict scheme + a ONE-line reason. The detector optimises RECALL; the judge supplies PRECISION.
   - **🛡 DEDUP-VS-HOME GATE (mandatory — added 2026-06-15):** before you KEEP a candidate, check it against the HOME note you recalled in step 2. If the candidate merely **restates** something already catalogued there (same belief / value / bet / question / shift / bridge — even if worded differently), DROP it with verdict **🗑 уже в доме (restatement)**. Only candidates that add something the home note does NOT already contain survive. This is a semantic check (you, the judge, do it — NOT a blind word-overlap filter, which would false-drop real nuance). *Why:* on 2026-06-15 the `identity` (11 raw keeps → 0 truly new after dedup) and `stance` miners re-proposed items already in `_Self-Bible-MOC` / `insight-contradictions`; this gate makes that dedup a required step, not a manual afterthought.
4. **Write the clean signal** → `_imports\alpha\candidates\<miner>-judged-latest.md` (utf-8, `\n`): only the ✅/🟡 keepers, each with quote(s), source `[[wikilink]]`, date if known, verdict, reason. If zero signal, say so plainly (that's a valid, honest result — don't invent).
4-бис. **ВТОРОЙ ЗАХОД, прежде чем назвать сигнал чистым** (⭐⭐ CLAUDE.md §4.3-бис, приказ оператора 13.09.2026). Вердикт судьи, это CLAIM, и доказывается вторым проходом ДРУГИМ методом, иначе он наследует слепоту первого:
   - **Дом перечитывается С ДИСКА, а не по памяти о шаге 2.** Дедуп-гейт сверяется со свежим текстом домашней заметки: между чтением и вердиктом её мог дописать другой майнер или ночной прогон. Совпадение по смыслу ищется заново для КАЖДОГО keeper'а.
   - **Отброшенная куча судится тоже.** Пройди выборочно 5 штук из 🗑 с вопросом «что я выбросил зря». Судья, выбросивший всё правильно, и судья, выбросивший всё ошибочно, с виду одинаково аккуратны.
   - **Файл читается с диска.** Открой `<miner>-judged-latest.md` заново и сверь с тем, что решил: доехало ли число keeper'ов, цела ли кодировка, не затёрт ли прошлый прогон.
   - **Назови непроверенное** строкой «судил N из M кандидатов, остальные не смотрел (причина)». Кап ~25 из шага 1, это законный результат, но он обязан быть назван, а не умолчан.
   ⛔ До второго захода слова «отсудил», «чистый сигнал», «готово» запрещены.
   ⭐ Ночной безлюдный прогон делает ровно то же: отсутствие человека второй заход не отменяет, строка о непроверенном уходит в `<miner>-judged-latest.md`.
5. **Propose HOME additions** (the keepers not already in the home note): show dev **ДО→ПОСЛЕ** ([[show-before-after]]); on his OK → `vault_backup.py` first ([[vault-backup-rule]]) → append to the home note (draft status, he edits) → recalc if the home has an engine (bets → `ledger_calibration.py`). **Never auto-write a curated vault note.**

## Guardrails
- **Token-economy ([[vault-data-architecture]]):** judge reads ONLY the candidate digest + the one home note. NEVER load the corpus. The detector already did the 0-token narrowing.
- **Honesty over yield:** "0 real" is a legitimate verdict (contradictions hit it 2026-06-14 — dev is consistent + already has the curated map). Don't manufacture signal to look productive.
- **No new ledgers:** every miner FEEDS a pre-existing curated home (bets→prediction-ledger, contradiction→insight-contradictions). Surface NEW candidates; don't duplicate the home.
- **Vault writes** = backup → preview → approve → reindex. Concurrent-git aware: if the vault `index.lock` is held by live git, defer the write and say so.

## Not this skill
Building/refining a DETECTOR script = direct work in `_imports\alpha\` (not here). Running the deterministic scan = the miner's own `.py` / weekly task. This skill is ONLY the judge + home-feed stage.


ARGUMENTS: channel

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/alpha; ls candidates | grep -i chan; git diff --stat; head -80 channel_judge.py; cat \"/c/Users/dev/.claude/projects/E--Obsidian--imports/memory/channel-judge-wa-format-bug.md\" \"/c/Users/dev/.claude/projects/E--Obsidian--imports/memory/channel-judge-nightly

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/alpha; git diff channel_judge.py; python channel_judge.py --dry-run 2>&1 | tail -30; tail -15 _channel_judge.log"}

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/alpha; grep -n -i \"канальн\" ~/.claude/skills/alpha-judge/SKILL.md | head; ls ~/.claude/skills/alpha-judge/; tail -20 _channel_judge_nightly.log 2>/dev/null; ls -la candidates/lobster-nightly-2026101[4-9]* candidates/lobster-nightly-20261006* candidates/wa-bitco

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/alpha; grep -n \"def build_prompt\" -A60 channel_judge.py | head -90; echo ====; cat candidates/lobster-nightly-20261016-judged-latest.md"}

---

**Claude:**

Сужу текущий батч из 4 каналов: читаю их отчёты.

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/alpha/candidates; for f in lobster-nightly-20261014 wa-bitcoin-apes-general-discussion-20261013-2335 lobster-nightly-20261006 wa-bitcoin-apes-general-discussion-20261005-2335; do echo \"######## $f\"; cat $f-report.md; done"}

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/alpha/candidates; python - <<'EOF'\nfiles = {\n\"lobster-nightly-20261014\": \"\"\"# ⚖️ lobster-nightly-20261014 — вердикт судьи (alpha-judge, in-session Opus, unattended)\n\nКорпус: LobsterDAO community-alpha, 66 содержательных сообщений → шортлист 25. Канал = к

---

**Claude:**

Отсудил батч из 4 каналов, сигнала ноль. Проверил с диска: все 4 файла вердиктов `*-judged-latest.md` читаются, кириллица цела. Пробный прогон судьи без вызова модели (`channel_judge.py --dry-run`) их больше не берёт, следующий батч уже другой: `lobster-nightly-20261005, bogdanchikov, lobster-nightly-20261004, lobster-nightly-20261003`.

| Канал | Кандидатов | Вердикт |
|---|---|---|
| lobster-nightly-20261014 | 25 из 25 | 0 альфы: спор о безопасности кошельков Ledger и цепочек поставок, статья про TWAP на Hyperliquid, споры про ERC20 |
| lobster-nightly-20261006 | 25 из 25 | 0 альфы: драма вокруг управления Safe и Gnosis, алгоритмическая торговля акциями в блокчейне |
| wa-bitcoin-apes-…-20261013 | 1 из 1 | 0: сбор записи на ужин (детектор не отсеял запись на ужин, фраза «register today» не попала в стоп-слова) |
| wa-bitcoin-apes-…-20261005 | 2 из 2 | 0: макро-мнение о рынке облигаций и биткоина |

**Второй заход по выброшенному.** Пересмотрел ближайшие промахи и оставил их выброшенными:
- #14: Alex через AI нашёл, как дёшево починить плату в машине. Бытовая история, а не инструмент.
- #21: просьба Amau познакомить с банкирами по структурированным финансам. У оператора таких контактов нет.
- #12/#14 из 20261006: мысль «слишком рано значит упустил рынок». Общеизвестная, для решений ничего не добавляет.

Сверять с домашней заметкой было нечего: ни одного кандидата не оставил.

**Что не проверено или проверено хуже:**
- В инструкции судьи (SKILL.md) нет раздела «Канальная полоса». Критерии взял из промпта самого `channel_judge.py`.
- Отсудил только этот батч. Каналов без вердикта по `--status` теперь **53** из 440, их не трогал.
- В `channel_judge.py` лежит чужая незакоммиченная правка: скрипт выбирает самую новую версию `claude.exe`, а не старую 2.1.193, и поправлено правило, по которому пустые отчёты WhatsApp закрываются без модели. Её я не трогал и не коммитил. Работает ли сегодняшний ночной прогон с этой правкой, не видно: в логе за 20.10 нет строки с итогом.

🎙 Майк: детектор чат-шума LobsterDAO стабильно даёт около 0% альфы на наш стек. Его стоит понизить в приоритете или свести к одному прогону в неделю, иначе мы платим токенами за пересказ крипто-драмы.

🏛H · Opus 5.5 · 42219

🧒 **Простыми словами:** Робот-сито набрало из крипто-чатов 53 «интересных» сообщения, я прочитал все. Там споры про кошельки, драма чужой компании и запись на ужин, для нас ничего полезного. Записал это в 4 файла, так что следующей ночью их не будут перебирать заново. Неразобранных чатов осталось 53.
