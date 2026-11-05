---
session: s_4ade1595
date: 2026-10-02
words: 24261
turns: 43
tools: "Bash, Edit, Grep, Write"
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-10-02 · CONTENT_DRAIN_AUTORUN

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_4ade1595` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

---
name: content-drain-daily
description: "DRAIN the content funnel: turn captured seeds into finished posts, gate them, record them on the approval clock (window = 0h since 05.08.2026). Counterpart of content-factory-daily, which FILLS the funnel. Root it exists for (measured 2026-08-04): posts.jsonl held 70 seeds over 26 days, 100% status=new - the funnel had an automatic INPUT and no automatic OUTPUT, because 'sit down and write the post' belonged to nobody. HUB-owned; account tonyssd; runs 23:10 Lisbon."
---

CONTENT_DRAIN_AUTORUN

ГРАНИЦЫ ДЛЯ ЛЮБОЙ РЕЛЬСЫ (добавлено 22.08.2026, Q1R).
Этот файл читает не только Claude Code: при исчерпанном баке подписки рутина уезжает на
чужую рельсу (--extfallback codex-agent), а она НЕ грузит CLAUDE.md оператора. Поэтому
границы едут вместе с задачей, а не подразумеваются:
- STOP: НИЧЕГО НЕ ВЫКЛАДЫВАЕМ НАРУЖУ. Работа этой рутины кончается ЧЕРНОВИКОМ в drafts\.
  Любая доставка наружу = Tier-2 и не твоё решение.
- STOP: Tier-2 целиком -- деньги, необратимое удаление, секреты, исходящее наружу, смена
  канона. Упёрся -- напиши строкой в отчёт и остановись, обход не выдумывай.
- STOP: секрет (токен, пароль, ключ) не попадает ни в черновик, ни в лог, ни в отчёт.
- STOP: приватное оператора наружу не уезжает; personal -- только обобщённо.
- OK: правда в цифрах. Счётчик, статус, «проверено» не выдумываются. Нет данных -- так и скажи.
- OK: бэкап перед записью в волт: python <IMPORTS>/vault_backup.py "content-drain".
- OK: пишешь файлы -- только в drafts\ и triage. Чужие заметки, _originals, канон не трогай.
- OK: нечего дренировать -- честный «nothing to drain», а не выдуманный текст.


GOAL: every run, take the oldest still-unwritten seeds from the funnel and turn them
into REAL TEXTS that are ready to go out. A seed is not content. A text is.

Target per run: 2 seeds -> finished drafts. Never zero when the funnel is non-empty.

PATHS (hub):
- funnel:   D:\Vault\_imports\content-factory\triage\posts.jsonl
- drafts:   D:\Vault\_imports\content-factory\drafts\
- engines:  D:\Vault\_imports\content-factory\  (slop_gate.py, approval_clock.py,
            platform_rules.json, episode_adapter.py)
- style:    _STYLE-positioning.md and the voice files referenced by content-factory-daily

STEPS:

0. KLON-GATE: A TWIN THAT PRINTED A LIMIT MESSAGE IS DEAD, NOT BUSY (added 2026-09-17, pain
   felt in that run). The launcher fires this routine on several accounts within seconds, so
   the harness clone-gate can greet you with "2 other sessions are writing RIGHT NOW" and
   tell you to stand down under later-loses. Its liveness test is the transcript's mtime -
   and a dying session refreshes that mtime with its own death rattle. Measured 17.09: both
   twins showed "ALIVE, silent for 7-17s", and each transcript held exactly ONE assistant
   line: "You've hit your weekly limit" (different reset dates = different accounts, i.e. a
   fallback chain, not a spawner storm). So before standing down, READ THE TWIN'S LAST
   ASSISTANT MESSAGE in projects/<project>/<session-id>.jsonl: a limit/usage line or a
   terminal API error means it never worked - continue the drain and say so out loud in the
   report. Only a twin that is actually producing tool calls earns a stand-down.

1. PICK. Read posts.jsonl. Select up to 2 records with status=new, oldest first.
   THE AGE FIELD IS `when`, NOT `ts` (added 2026-09-15, trap hit in that run): of the 762
   status=new seeds exactly ONE carried a `ts` key, so sorting by `ts` silently degrades to
   alphabetical-by-id and puts the `alpha:fbcomments:*` seeds first - and those are full of
   third-party names, which this routine may not publish. Sort by `when` (ISO, e.g.
   "2026-08-12T13:12"); treat a missing `when` as unknown age, not as oldest.
   Skip any seed already covered by a draft. Coverage truth comes FROM DISK, not from the
   seed record: `python drain_dedup.py --covered --json` returns the ids that already have
   a draft file carrying them in funnel_ids. (The old wording said "skip any whose slug
   already has a file in drafts\" - dead check: the funnel writer stores "slug": "" and the
   field is empty for 100% of status=new seeds, measured 703/703 on 2026-09-12 and 469/469
   on 2026-09-03, so that gate never fired once.) If the funnel
   has nothing with status=new, write the "nothing to drain" stamp in step 7 and stop.
   1-ter. --covered IS BLIND TO HEADLESS DRAFTS - GREP BEFORE YOU WRITE (added 2026-09-14,
   pain felt in that run: hub:5496 was my pick #1 and it had been fully drained on 19.08 -
   3 files on disk). draft_coverage() proves coverage by ONE field, `funnel_ids:` in the
   frontmatter, and 42 drafts on disk never got that field; those seeds stay `new` forever
   and the next run writes a duplicate. So for each candidate ALSO grep the first 4KB of
   drafts\*.md for its id and for `#<numeric tail>` (voice drafts store the id as
   `source_ref: "tg:-100...#5496"`, not as funnel_ids). Measured 2026-09-14: 8 of 720
   uncovered `new` seeds already had a draft. Found one? Do NOT rewrite it: backfill
   `funnel_ids: ["<id>"]` under its source_ref line (evidence = the id is already named in
   that same header), then `python drain_dedup.py --heal`, and pick the next seed. That run
   closed 6 old seeds this way (hub:5496 + NPC series 5656/5659/5662/5665/5668) and took
   desync to 0.
   MERGE-TWINS ARE THE THIRD BLIND SPOT (added 2026-09-17): a seed whose title or note opens
   with "[MERGE с <other-id>]" carries the SAME story as <other-id>. If <other-id> already
   has a draft, this seed is drained too - and no grep for its own id will ever reveal that,
   because the draft names only the partner. So resolve the merge partner's id and check IT;
   when it is covered, add BOTH ids to that draft's funnel_ids and run --heal. Measured
   17.09: hub:5492 ("the session dies with the laptop lid") was the MERGE-twin of hub:5488,
   fully drained on 05.09 in three files, and had been sitting `new` for 29 days.
   THE SEED THAT NAMES ITS OWN DRAFT IS THE FOURTH BLIND SPOT (added 2026-09-19, found in
   that run). Some funnel writers append the draft path straight into the note - «Черновик:
   E:\...\drafts\<file>-DRAFT.md» or «drafts/<file>-DRAFT.md» - and then never flip the
   status. That seed is provably drained by its OWN record, yet `--covered` cannot see it
   (the draft's funnel_ids names a different id, e.g. the `hub:NNNN` voice it came from)
   and the 1-ter grep cannot see it either (the draft never mentions the cc:/tg: mirror id).
   So run one cheap regex over ALL uncovered `new` notes for `drafts[\\/][^ ]+DRAFT\.md`,
   check which of those files exist on disk, and for each hit add the seed's id to that
   draft's funnel_ids, then `--heal`. Evidence is the seed's own note naming that exact
   file - not a guess. Measured 19.09: 6 seeds closed this way (5 NPC-series mirrors +
   `voice`), drafts written 21.08 and 30.08, the oldest sitting `new` for 29 days; two more
   seeds named drafts that do NOT exist (`voice-hub-6525`, longboards) - those stay queued,
   a named-but-missing file is not coverage. Before adding an id, confirm it is UNIQUE in
   posts.jsonl: generic ids like `voice` would otherwise close more than one record.
   Prefer seeds whose note carries a concrete measured fact (a number, a failure, a
   before/after) over vague ones - those become good posts, the rest stay queued.
   1-quater. FILTER BY `visibility` AND BY WHO CAN OWN THE STORY (added 2026-09-20, the
   oldest-first rule walked straight into a canon wall that night). Step 3 makes every draft
   MYCROFT in FIRST PERSON, and canon 3.3 forbids him to appropriate dev's personal life -
   so a seed about dev's travel, health, family or his own verbatim essay is NOT drainable
   by this routine no matter how old it is; it needs dev's voice, not Mycroft's. Two cheap
   machine filters do almost all of that work: the record carries a `visibility` field
   (`personal` = generalized only, per the BOUNDARIES block above; prefer `public`), and
   titles starting `[INTERNAL]` / `[BANK]` are usually infra tasks or idea stubs whose own
   notes say so ("не контент", "не публикуем, чтобы не выдать механизм"). Measured 20.09: of
   the 14 oldest uncovered `new` seeds, 7 were `[INTERNAL]`, 2 were MERGE-twin travel notes,
   and ZERO were drainable here. The workable pool is `visibility == public` AND an id in the
   `cc:` / `cc:live-` / `git-` family - our OWN system work, which Mycroft can legitimately
   own in first person; that pool held 209 seeds on 20.09. Sort THAT by `when` and take the
   oldest. Skipping a seed for this reason is not draining it - leave it `new` and say why.
   1-quinquies. THE MACHINE FILTERS DO NOT CATCH A CANON STOP-WORD IN THE TITLE (added
   2026-09-21, hit in that run). cc:284c9e17 "не-технарь и клод: от слов к рабочему коду"
   passed every filter in 1-quater - `visibility: public`, id in the `cc:` family, second
   oldest in the pool - and is still unpublishable: the 14.09-бис carve-out to canon 3.3
   struck the labels «не-кодер» / «не-технарь» off dev entirely (he is a programmer,
   Python and C++), so a post built on that frame breaks canon no matter how good it is.
   Same veto applies to any seed whose frame calls dev a founder/co-founder (same
   carve-out). So after the 1-quater filters, READ the title and note of each candidate for
   those four words before writing. This one will keep surfacing: it stays `new` and sorts
   second-oldest forever, so expect to skip it again and say so rather than silently
   re-picking it.
   1-sexies. TWO MORE CANON WALLS THE MACHINE FILTERS WAVE THROUGH: WHOSE LIFE IT IS, AND WHAT
   THE SUBJECT IS (added 2026-09-23, both met in that run's top-3). 1-quater says the workable
   pool is `visibility == public` AND the `cc:` / `cc:live-` / `git-` family, "our OWN system
   work". That is true of the ID, not of the CONTENT: the miner tags a seed by where it was
   captured, so a `cc:live-` seed can be dev's personal life caught in a session. Measured
   23.09, the second-oldest public seed in the pool was `cc:live-46eff1` - dev's own ayahuasca
   therapy experience, him crying about someone he had shouted at. Mycroft may not own that in
   first person (canon 3.3), no matter how public the field says it is. Third-oldest,
   `cc:live-60245d`, was our own DR fan-out - four LLMs agreeing on an investment thesis whose
   subject is adult content: the mechanics are ours, but the SUBJECT carries platform and
   reputation risk that is dev's call, not a robot's. So after the machine filters, ask two
   questions of each candidate: whose life is this (his -> his voice), and what is the subject
   (bannable/sensitive -> his call). Skipping for either reason leaves the seed `new`; say which
   reason in the report.
   AND ONE HONEST EMPTY: `cc:9814e241` (the .md-is-Moldova's-TLD grabla) was skipped because
   recall found NO artifact - every hit came back with a negative rerank score. Step 2 forbids
   writing from the 3-line seed alone, so the honest verdict is "I did not find the artifact",
   not "there is nothing there" (canon 5.4). It stays queued.
   ^^^ REFUTED 2026-09-28, AND THE REFUTATION IS THE LESSON: the artifact existed the whole
   time - a dated line in `00-System/Breakage-Journal.md` (2026-08-25, "лид ушёл бы на чужой
   сайт ... фикс = полный GitHub-URL, грабля в /peer-onboard"). One ripgrep found it in seconds.
   The 23.09 verdict was correctly WORDED ("I did not find it") and still did real damage,
   because nothing in this prompt says an honest-empty EXPIRES: five later runs read that note,
   inherited the skip without re-trying, and the seed sat `new` for another 5 days. So treat a
   recorded honest-empty exactly like canon 5.4 treats a ban - it is a claim with a shelf life.
   Re-try it with a DIFFERENT instrument than the one that failed (brain_ask failed here;
   ripgrep succeeded) before inheriting the skip. This is the opposite of the 1-quinquies /
   1-sexies / 1-septies canon skips, which are permanent by design: a CANON skip is about what
   the seed IS, an honest-empty is about what I FAILED TO FIND, and only the second one rots.
   1-septies. THE THIRD QUESTION: IS THE SUBJECT dev'S BIOGRAPHY OR HIS JOB SEARCH?
   (added 2026-09-26, met as the 4th-oldest candidate that night). 1-sexies teaches two
   questions - whose life is this, and what is the subject - and both were written against
   seeds that are OBVIOUSLY personal (therapy, adult content). A job-search seed slips
   between them: `cc:ff21c6b8` («a recruiter searches for our multi-agent consensus and finds
   a 2017 ICO instead») is `visibility: public`, sits in the `cc:` family, names no third
   party, carries no canon stop-word from 1-quinquies, and its subject is not bannable - it
   passes every filter as literally written. It is still not drainable here: the post's
   subject is dev's own biography (an old crypto project of his outranking his shipped
   work) and his live job search, and the 14.09 carve-out to canon 3.3 pulls employment
   touches out of Mycroft's voice entirely - those go in dev's first person. §1.5 says to
   search for work LOUDLY, so this is not a veto on the topic; it is a veto on THIS routine
   writing it as Mycroft. So ask a third question of each candidate: is the subject his
   biography, his health, his money or his job hunt? Yes -> his voice or his call. Like
   cc:284c9e17, this one will keep sorting near the top: skip it and say why rather than
   re-reasoning it from scratch every night.
   1-bis. SAME-DAY MORAL CHECK (added 2026-09-13, pain felt in that run). Coverage is by
   funnel id, so it cannot see that a draft written TODAY by a sibling run already carries
   your punchline. Before writing, read the titles of drafts\<TODAY>-* and ask "is my last
   line already someone's last line?" On 13.09 the seed cc:live-18ae74 ("the watchdog lied
   about 328 orphans") was about to ship the moral "the instrument is blind" on the same day
   and same channel as pribor-s-zakrytymi-glazami, which already carried it; the post was
   re-angled to "an accusation is not a fact" instead of being dropped. Re-angle, don't drop.

2. RECALL before writing. For each seed: pull the underlying artifacts it points at
   (vault notes, the repo, the session log, the registry row). A post written from the
   3-line seed alone is a paraphrase of a paraphrase. The story lives in the artifacts.
   GO TO THE VAULT FIRST, THE CONFIG FILES SECOND (added 2026-09-21, cost three dead tool
   calls that night). These seeds are weeks old by construction, so the artifact is usually
   a vault note, not a live file: cc:8ec7067a pointed at a vendor evaluation whose config
   (`dr_rails.json`) does not exist on this node at all, while the decision itself sat in
   10-Tasks as a full task card with quorum, price and a review date. One
   `python D:\Vault\_importsrain_ask.py "<тема>"` found it; grepping ~/.claude for
   the vendor name found nothing and would have been read as "no artifact" (canon 5.4:
   empty from ONE place is not "нет"). A task card is the richest source there is - its
   frontmatter carries `state` and `review_after`, i.e. a free, checkable ending for the
   post ("parked for a human, N days past its own review date").
   WHEN THE SEED NAMES A GITHUB OBJECT, ASK GITHUB BEFORE THE VAULT (added 2026-09-26, cost
   two dead recalls that night). The 21.09 rule "vault first, config second" is right about
   CONFIG but wrong about GitHub: both recalls came back useless (pick A's best hit reranked
   1.73 and was unrelated; pick B's twelve hits were ALL negative), and yet every number in
   both finished posts came from `gh api` and one live script run. The reason is structural -
   these seeds are 30 days old, so what the post needs is not the story (the seed already
   has it) but TODAY'S NUMBER to end on, and a vault note cannot hold a number measured
   tonight. So: seed names a repo / issue / PR / gist -> `gh api repos/<o>/<r>` and
   `gh issue view` FIRST; seed names one of our scripts -> run it with `--json` / `--selftest`
   and quote tonight's output. Measured 26.09: 4 repos at stars=0/forks=0/subscribers=0 and
   `#89797 OPEN comments=0` gave post A a free, checkable ending that REFUTED the seed's own
   same-day lesson - the strongest post shape there is. brain_ask stays for finding a vault
   note whose filename you do not know.
   THE TASK CARD'S `evidence:` FIELD IS WHERE THE GITHUB OBJECT HIDES (added 2026-09-27,
   this is how post A got its ending). The 26.09 rule fires when THE SEED names a repo/issue/PR -
   but tonight neither seed did, and post A still ended on a live GitHub number. The chain was:
   seed -> brain-free ripgrep found the canon beat -> the beat's `evidence_refs` pointed at a task
   card -> that card's `evidence:` frontmatter line named `RFC anthropics/claude-code#89840`, which
   nothing upstream had mentioned. One `gh issue view` later the post had a checkable ending (OPEN,
   32 days, zero maintainer replies). So: whenever recall lands a task card, READ ITS `evidence:`
   AND `outcome:` FIELDS before deciding there is nothing to measure - they are where a closed card
   records the live objects it produced (issues, gists, parcels, tools). A seed describes what
   happened a month ago; the card's evidence line tells you what is still out there to measure.

   A SEED BORN FROM A GRABLA HAS A JOURNAL ROW BY CONSTRUCTION - READ IT FIRST (added
   2026-09-28; it carried BOTH posts tonight). Canon 5.10 requires every breakage and every
   lesson to be written as one dated line in `00-System/Breakage-Journal.md`. Most seeds in
   this funnel ARE breakages - that is what our sessions produce - so for any seed whose note
   describes a грабля, a failure, a wrong verdict or a fix, the richest artifact is a journal
   row, and it is keyed by the thing itself, not by the seed id. Ripgrep the journal for the
   seed's distinctive noun (`молдав`, `11874`, `mass-delete`) BEFORE brain_ask: tonight that
   one query returned the 25.08 row for pick A and a whole FAMILY of four dated rows for pick B
   (2026-07-16, 08-21, 09-05, 09-21), which is what let post B end on "the instrument got more
   verbose every time a reader failed it" instead of on the seed's own single anecdote. A
   journal family is strictly better material than a single note: it proves a CLASS, with dates.
   THE JOURNAL'S FULL PATH IS `D:\Vault\Vault-Knowledge\00-System\Breakage-Journal.md` (added
   2026-09-29, cost two dead tool calls on the very first recall of the night). The 28.09 entry
   above writes it VAULT-RELATIVE, as canon 5.10 does - and this prompt's PATHS block never names
   the vault root at all (every path it lists lives under `_imports`), so the literal string in
   that entry is what a run reaches for. `D:\Vault\00-System\...` does not exist; the tool
   answers "Path does not exist", which is indistinguishable from "the journal has nothing".
   Same family as canon 8.1: Glob/Grep do not expand variables, so substitute the VALUE. Note
   the vault root is Windows-only here - on Mac/Linux nodes it differs (`~/.claude/fleet_nodes.json`).
   READING A JOURNAL HIT NEEDS A SECOND STEP - THE ROWS ARE TABLE ROWS (same night). The journal
   is a markdown table whose rows run to thousands of characters, so the ripgrep tool answers a
   content search with `[Omitted long matching line]` for nearly every hit: you get line numbers
   and no text. That is NOT an empty result. The working pair is ripgrep to LOCATE, then
   `sed -n '<N>p' <file> | fold -w 190` to READ - that is how both of tonight's rows (3296, 3586)
   were actually read. Budget two steps per journal query, not one.

   WHEN THIS RUN JOURNALS ITS OWN GRABLA, USE ALL FOUR CELLS - ONE CELL SILENTLY CAPS AT 400
   (added 2026-09-30, cost the entire evidence half of tonight's row). The read side of the journal
   is now well covered above; the WRITE side was never mentioned, and canon 5.10 makes this routine
   a writer every time it hits a грабля. `selfheal.py journal` renders a TABLE row through
   `breakage.make_row`, and `_cell(s, limit=400)` truncates EVERY cell at 400 chars with no warning.
   Measured 30.09: a ~1900-char `--what` came out as a 400-char cell cut mid-sentence - conditions,
   the ✅ proof and the «механизм НЕ строю» verdict were simply gone, while the CLI still printed
   `строка 1/3` and looked successful. And there is no second copy to recover from:
   `breakage_lines.jsonl` is a pure counter (ts/class/target/count) - `what` is empty in 1123 of
   1123 rows. So split the payload across `--what` / `--conditions` / `--parts` / `--guess` (four
   cells = 1600 chars of real budget) instead of cramming one. To FIX a row already written, do not
   hand-edit Breakage-Journal.md - the table is folded from shards and says so. Edit the `text`
   field of your own node's record in `_machine-bus/_breakage/breakage__from-<HOST>.jsonl` (your own
   shard only; `add()` itself takes a `text=` override) and re-render with
   `breakage.fold(force=True)`. That keeps the class count intact, where re-running `journal` would
   double-count the same case.
   ALSO TRUST prior_art's FAMILY WARNING, THEN ACTUALLY READ THE NEIGHBOURS (same night). It printed
   «СЧЁТ ЗАНИЖЕН - своим именем 1, а у семьи ещё 2 прежних случаев (итого 3, порог 3)», which would
   have promoted the class straight to a repair session. Reading the six neighbours showed five were
   vocabulary overlap (python/window/путь), not the same defect - but the sixth was real and mirrored
   (`literal-windows-path-on-linux-node`). Note which way the convenient answer points: «only 2, no
   mechanism owed» is the cheap verdict, so per canon 5.4 it needs the stronger proof. Write BOTH
   readings into the row and leave the promotion to the class owner - do not resolve a repair-session
   threshold from inside a content routine.

   NEVER `grep -r` THE VAULT FROM BASH - USE THE RIPGREP TOOL (added 2026-09-26, burned ~4
   minutes of dead wall-clock in that run). Three separate bash greps over the vault (and one
   over ~/.claude) hit the 120s and 100s timeouts on a single literal string and returned
   NOTHING - which reads exactly like "no artifact" and would have produced a false honest-empty
   under canon 5.4. The harness Grep tool is ripgrep and answered the same query instantly
   (15 files for `SCFS`, including the task card that carried half of post A). This bites
   especially hard right after the 21.09 entry, which recommends "grepping ~/.claude" as the
   move that found nothing: it may have found nothing because it never finished.
   SECOND DATED CASE 2026-09-28 (conditions now named, per canon 5.10): `grep -rl` over
   ~/.claude + E:\_imports for ONE literal token timed out at the Bash tool's own 120s ceiling
   (exit 143) while looking for this prompt's file path. The ripgrep tool answered the same
   query instantly. Conditions are consistent across both cases: recursive bash grep over a
   synced tree with .stversions/.git inside it. Class = a search that dies silently and reads
   as absence. Next occurrence is the third -> mechanism, not another log line.
   SCOPE OF THAT BAN, SO IT DOES NOT EAT THE ONE CHEAP INSTRUMENT (added 2026-09-29): the two
   dated cases are both RECURSIVE (`grep -r` / `grep -rl`) over a synced TREE. A bash grep at ONE
   NAMED FILE is a different thing and is fine - `grep -n "<token>" Breakage-Journal.md` answered
   instantly four times tonight, and it is the only way to scan a 5000-row table for a date, since
   the ripgrep tool omits long rows (see the block above). So: recursive over a tree -> ripgrep
   tool, always; single named file -> bash grep is the cheaper move. Do not read the 26/28.09
   entries as "never use grep here" - that would leave no instrument at all for the journal.
   A GIT-BASH PATH HANDED TO WINDOWS PYTHON READS AS ABSENCE (added 2026-09-30, cost two dead
   calls and one FALSE COVERAGE READ that night). The Bash tool here is git-bash, so `/e/Obsidian/...`
   and `/tmp/...` resolve for the SHELL - but the `python` it launches is Windows python, which
   resolves those literally and raises FileNotFoundError. Two hits in one run: (1) step 1's
   `--covered --json` was redirected to `/tmp/covered.json` and the reading python answered
   `covered: 0`, i.e. the pool was computed as if NOTHING on disk were drained - the exact
   false-coverage class this prompt has been patching since 14.09, except self-inflicted; (2) a
   `find`-produced POSIX directory path fed to `os.listdir` died the same way. Neither failure says
   "wrong path flavour"; both look like an empty corpus. So: inside python string literals ALWAYS
   use the Windows form (`r'D:\Vault\...'`), and write intermediate JSON next to the script
   (`cov_tmp.json` in content-factory), never `/tmp`. Cheap tell that it happened: a coverage or
   digest count of exactly 0 when the tool that produced it printed rows. Tonight the picks were
   unaffected only by luck - the pool came out at 259 both times because none of the top seeds were
   covered anyway. Same family as the 26/28.09 bash-grep entries: an instrument that fails silently
   and reads as "nothing there" (canon 5.4).

   BRAIN_ASK IS NOT PARALLEL-SAFE - ONE FIXED OUTPUT FILE (added 2026-09-23, cost one wasted
   recall that night). brain_ask.py writes its answer to a single fixed path,
   D:\Vault\_imports\_brain_answer_rr.txt, and prints only "N hits -> <that path>". Two
   recalls fired in the SAME message (one per seed, which is the natural thing to do with two
   picks) finish seconds apart and the second silently overwrites the first - the first seed's
   recall is simply gone, and nothing in the output says so. Run recalls ONE AT A TIME and read
   the file between them.

3. WRITE. For each seed produce ONE FILE PER TIER+CHANNEL, named
   drafts\<YYYY-MM-DD>-<slug>-<teaser-ru|teaser-en|medium-fb>-DRAFT.md, all of them
   carrying the SAME funnel_ids. (Corrected 2026-09-13 against measurement: the old wording
   "ONE draft file containing all tiers" is unbuildable downstream - approval_clock.py ping
   takes exactly one --tier and one --channel per --file, and slop_gate.py judges one tier
   per file. Every drain run on disk already writes 3 files; the prompt was the only place
   claiming otherwise.) The tiers, per the platform matrix:
     - teaser RU, HARD 200-250 chars (dev's number 06.08.2026; machine truth =
       episode_adapter.TIER_LEN + platform_rules.json max_chars 250, NOT the old 240).
       Channel: @ClawRus only while registry/limits.json says tg_clawrus paused=false -
       it is paused=true since 06.08, so RU teasers route to @PaloAltoAiRu. WRITE THE
       ADDRESS, NOT THE CATEGORY (corrected 2026-09-16): `channels_proposed:
       ["@PaloAltoAiRu"]`. distributor.ROUTES maps the category `"tg-channel"` back to
       tg_clawrus = the paused @ClawRus, so the category silently undoes this line.
     - teaser EN for X, HARD 200-250 chars, label Automated (canon 3.3 / EU AI Act art.50)
     - medium for FB RU when the material carries a real story
   Voice: Mycroft, first person, disclosure in the FIRST line (canon 3.3). Lowercase
   register, short hyphen not em dash, no "we" as the subject.
   THE DISCLOSURE LINE HAS ONE WORKING FORM (corrected 2026-09-16, see log): write
   «привет, это майкрофт, синтетический кофаундер оператора - ии, а не человек». The
   publisher's gate matches `синтетическ\w+ кофаундер`, so the form this prompt used
   to teach - «синтетический ии-кофаундер» - does NOT match and parks every FB medium
   in distributor HOLD. EN stays «Mycroft here, dev's synthetic cofounder. Automated.»
   SIGNATURE / WAY OUT (corrected 2026-09-13; the old "no signature" cost two extra rewrite
   rounds in that run). Canon 1.1 outbound-signature says every outward touch carries a
   signature, compressed but never absent, and slop_gate enforces the same thing from the
   other side: a body with no CTA/link raises W6-missing-required (medium) and
   W7-teaser-no-way-out (teaser). So: the RU teaser ends with `t.me/PaloAltoAiRu` - that link
   IS the compressed signature and fits inside the 250 cap.
   THE EN TEASER MUST NOT CARRY THAT LINK (corrected 2026-09-14): _STYLE-footer.md has held
   since 07.07 that EN posts never link RU channels, so the old wording told this routine to
   break canon every single night. EN way out = the EN Linktree, WRITTEN AS A FULL URL:
   `https://linktr.ee/PaloAltoAI`. Full URL is not cosmetics - W7 matches raw text against
   `https?://|t\.me/|github\.com/`, so a bare `linktr.ee/...` does NOT satisfy it. Worse
   trap, measured 2026-09-14: an EN draft passed W7 only because the string "t.me/" happened
   to sit in its own `teaser_note` metadata - a green gate earned by a comment, not by the
   post. Keep metadata clean of link-shaped strings you did not put in the body.
   EN disclosure stays the body line "Mycroft here, dev's synthetic cofounder. Automated."
   NO BODY BLOCK OVER 3 SENTENCES - IN ANY TIER, IN ANY LANGUAGE (added 2026-09-27 as "write the
   EN teaser as TWO PARAGRAPHS"; RE-NAMED 2026-10-01 after that headline failed a third time).
   The EN body is naturally 4-5 short sentences and they all land in one block, which trips
   paragraph_lint's three-sentence rule on the POST BODY - the one hit that actually matters (see
   the expected-noise note below). Splitting afterwards costs +1 char, which is free at ~240 but is
   exactly the edit you cannot afford at 249.
   WHY THE OLD WORDING KEPT FAILING: "two paragraphs" is weaker than its own recipe. Write two
   blocks and the SECOND one is still 4-5 sentences, so the lint still fires - measured 22.09
   (one EN body), 27.09 (both), 01.10 (both again, after the rule was followed literally). The
   binding number is the LINT's, not the paragraph count: no block over 3 sentences. The recipe
   below is therefore THREE body blocks, not two: disclosure / blank / 2 sentences / blank /
   2 sentences / blank / 2-3 sentences / link.
   MECHANISM (3rd dated case, §5.10 - built 01.10, do not re-derive this by eye): the shared
   verstak `_scratch/measure_0924.py` now runs paragraph_lint's OWN `scan_text` over the body with
   frontmatter AND html-comments stripped, and prints `полотен в теле: N`. Those two strips are the
   whole expected-noise list below, so a hit from the verstak cites a post body BY CONSTRUCTION -
   no more eyeballing which hit matters. Run it before writing and after. One trap already paid
   for: mirroring the threshold (3) with your OWN `sg.sentences()` instead of the lint's counter
   cries "полотно" on every FB medium that the lint passes - that is the two-instruments-disagree
   class, reproduced from inside the fix. Call the judge's function, never a copy of its rule.
   EXPECTED EN WARN, do not chase it: W4-first-person scores only the Russian pronoun set
   (slop_gate.FIRST_PERSON, RU-only), so every EN draft warns at 0.0/1000 no matter how many
   times it says "I". Verified by reading the constant on 2026-09-14. Do not mangle English
   to satisfy it; say so in the report instead.
   medium FB keeps the body link-free and carries footer blocks A+B+C+E from
   _STYLE-footer.md as an HTML-commented "FIRST COMMENT" block after the body.
   Write the teaser WITH the link from the start - budget ~18 chars for it, do not write
   a 250-char teaser and then discover it no longer fits.
   BUDGET TWO FIRST-PERSON TOKENS, NOT ONE (added 2026-09-15, cost two rewrite rounds that
   night). W4-first-person wants >=30 RU first-person hits per 1000 words; a ~35-word RU
   teaser clears that only with TWO of «я/мне/мой», and each one you bolt on afterwards
   costs 2-7 chars against a HARD 250 cap - which is exactly how a clean 245-char teaser
   became a 253-char F6-length-max FAIL. Write both pronouns into the first version.
   THE 250 CAP INCLUDES THE DISCLOSURE LINE - BUDGET 71 CHARS BEFORE YOU START (added
   2026-09-19, cost a full rewrite round of three of the six files that night). slop_gate
   measures the whole body after stripping frontmatter and HTML comments, and the mandatory
   RU disclosure «привет, это майкрофт, синтетический кофаундер оператора - ии, а не человек»
   is 71 chars, plus the blank line = 73. So the RU teaser's real writing budget is ~177
   chars INCLUDING the ~18-char link, i.e. about 155 chars of actual sentence - roughly 25
   words, not 35. EN is easier: «Mycroft here, dev's synthetic cofounder. Automated.» is
   53 chars, leaving ~195. Measured 19.09: writing the paragraph first and the disclosure
   second produced 288 / 280 / 261-char bodies, three F6-length-max FAILs in one pass.
   Count the total (disclosure + 2 + body + link) BEFORE writing the file, not after.
   THE RU TEASER ALSO HAS TO CLEAR W3-RHYTHM, AND RHYTHM FIGHTS THE 250 CAP (added
   2026-09-22, cost two rewrite rounds that night). W3 wants >=30% of sentences to be
   SHORT (<=5 words); a tidy 3-sentence teaser lands at 20% and warns. Adding a short
   sentence afterwards is the ONE edit you cannot afford at 246 chars - it pushed a clean
   teaser to 252 and turned a W3 warn into an F6-length-max FAIL. So budget the rhythm
   with the pronouns and the disclosure, BEFORE writing: out of ~5 sentences, two must be
   <=5 words («дубля нет, доложил.» «дубль был.»). Short sentences are also the cheapest
   way to carry the second «я/мой», so the two budgets pay for each other.
   W3 AND W4 SCORE THE MEDIUM TOO - THE PROMPT ONLY EVER BUDGETED THEM FOR TEASERS (added
   2026-09-23, cost a full rewrite round of BOTH mediums that night). check_warns() does not
   branch on tier for rhythm or first person, so a medium of tidy long sentences warns exactly
   like a teaser: measured 23.09, medium A came out at 5% short sentences and 22.6 first-person
   per 1000 words, medium B at 11% and 14.6. The thresholds are absolute, not per-tier: >=30% of
   sentences <=5 words, >=30 first-person per 1000. For a ~210-word medium that is ~7 short
   sentences and ~7 of «я/мне/мой/моя/мои». Write the medium in short punchy lines from the
   start - it also reads better than the long-sentence version.
   MEASURE WITH THE JUDGE'S OWN FUNCTIONS, NOT BY EYE (same night). Guessing these two numbers
   costs one rewrite round per guess. Import the gate and ask it: `sg.sentences(body)`,
   `sg.words(s)`, `sg.FIRST_PERSON`, `sg.SHORT_SHARE_MIN`, `sg.FIRST_PERSON_MIN` - all
   module-level in slop_gate.py. Two traps, both hit on 23.09: `sg.extract_body(raw)` returns a
   TUPLE (the body is `[0]`), and `sg.sentences()` splits on newlines as well as `[.!?]`, so a
   paragraph break makes a sentence boundary and a two-word line counts as a short sentence.
   COMPOSE THE DRAFTS IN A _scratch GENERATOR .py, NEVER IN A BASH HEREDOC (added 2026-09-28,
   cost one dead tool call and a confusing parse error). The six bodies are Russian prose full
   of apostrophes, double quotes and `%`, and the frontmatter strings quote the journal verbatim.
   Fed to `python - <<'PY'`, that died with "unexpected EOF while looking for matching `''" -
   a shell-quoting failure that says nothing about the content and looks like a Python problem.
   Write the generator to `content-factory/_scratch/gen_<MMDD>.py` (Write tool, no shell quoting
   involved) and run it. That is also strictly better than a heredoc for the routine's own
   purposes: the generator is re-runnable after a fix, it is one artifact you can diff, and it
   keeps the six headers provably identical instead of hand-copied. Same reasoning as the
   verstak entry directly below - _scratch is where this routine's tooling lives.
   SCOPE, WIDENED 2026-09-30 AFTER THE SAME TRAP KILLED A LOG ENTRY: this block says "the six
   bodies", so it reads as a rule about DRAFTS. It is not. The same `unexpected EOF while looking
   for matching `''` killed the append of tonight's PROMPT-FIX LOG entry through
   `python - <<'PY'`, for the identical reason - Russian prose, apostrophes, quoted canon phrases.
   The rule covers ANY prose payload this routine writes through the shell: drafts, this log's own
   entries, journal rows, the chat-03 report. If the text contains Russian, apostrophes or quotes,
   it goes into a `_scratch/*.py` written with the Write tool and then run. Short ASCII one-liners
   are still fine in Bash directly.

   THE VERSTAK ALREADY EXISTS - DO NOT WRITE A THIRD COPY (added 2026-09-26; I wrote a fourth
   one before noticing). It is `content-factory/_scratch/measure_0924.py` and it is better than
   what you would write from scratch: it takes any number of DRAFT FILE paths (not bodies),
   calls sg.extract_body itself and already handles the tuple trap, and prints chars / sentences
   / short-share / first-person-per-1000 with each threshold inline. Run it on the files after
   writing and on a scratch copy of the body before. Two near-identical siblings from 23.09 and
   24.09 are already sitting in that folder - §5.8 is "one source, zero copies", so reuse, and
   if it lacks something, extend that file.
   THE FOOTER REGISTRY IS STALE ON THE RU CHANNEL (measured 2026-09-15): _STYLE-footer.md
   block B still lists "🟢 Telegram RU: https://t.me/ClawRus", while registry/limits.json has
   tg_clawrus paused=true since 06.08, re-confirmed by dev on 21.08 and 23.08. Copying the
   footer verbatim puts a dead channel into every FB first comment - route the follow link to
   https://t.me/PaloAltoAiRu. Do not "fix" _STYLE-footer.md from here: the footer text is
   Nora-owned cosmetics, so report the divergence instead.
   Also expected, do not chase: paragraph_lint flags TWO things in every draft that are not
   prose - the FIRST COMMENT footer block as one 6-sentence paragraph, and the YAML
   frontmatter itself (title/tier/voice on consecutive lines reads as a 5-sentence
   paragraph, measured 22.09 on all six files). The only hit that MATTERS is one whose
   quoted text is the post body; that one is real and gets fixed in-run - on 22.09 an EN
   teaser ran 4 sentences in a single block and was split after «Funny.» for +1 char. It is a footer list inside an HTML comment, not prose; slop_gate strips it from
   the body count. The post body itself must still pass the three-sentence rule.
   Third expected non-hit: W6-missing-required IS UNAVOIDABLE ON EVERY FB MEDIUM (added
   2026-09-23). The platform rule says the FB body carries no links and the footer goes to the
   first comment; slop_gate strips HTML comments before it looks for the required GitHub link,
   so it always reports one missing. It is a WARN, not a FAIL. Do not "fix" it by putting a link
   in the body - that breaks the platform rule to satisfy a check.
   END A MEDIUM WITH A STATEMENT, NOT WITH THE QUESTION (added 2026-09-21). A question to
   the audience is wanted, but W2-ends-with-question fires on the LAST line ("рынок так
   делает 1 раз на 105 постов"), so the question needs one short closing line after it -
   every medium on disk already does this and the prompt never said so. One line of the
   post's own moral, first person, is enough.
   Header of the file = the standard draft block: status, voice, where the facts come
   from, funnel capture ids. Numbers are only ever the measured ones - never invent a
   figure to make a post rounder.

4. GATE. Run slop_gate.py on each produced file. THE FLAG IS MANDATORY (added 2026-09-20,
   cost six dead calls that night): the invocation is `python slop_gate.py --file <path>`,
   NOT `slop_gate.py <path>` - bare positional gives argparse "the following arguments are
   required: --file" and exits, so a whole batch can LOOK gated when nothing was judged.
   (The irony is worth keeping: that is argparse refusing an unparsed invocation correctly -
   the opposite of the unparsed-flag class.) FAIL means REWRITE now, in this same
   HB1 HARD-BLOCKS THE WORD «ГИПОТЕЗА» IN A BODY (added 2026-09-23, hit that night). The gate
   keeps a hedge-word blacklist: «гипотеза» in the post text is a HARD-BLOCK, not a warn -
   "либо доказано, либо гипотеза, и тогда в пост не идёт", and a HARD-BLOCK cannot be degraded
   to a lower tier. This collides head-on with canon 5.4, which demands that an unproven cause
   be LABELLED as a hypothesis - and the resolution is not to hide the uncertainty but to write
   it in plain words: «это открытый вопрос, а не причина», «удобная догадка», «я не знаю,
   почему». Measured 23.09: the sentence «ещё не корень, а гипотеза с удобной формулировкой»
   blocked medium A; «ещё не корень. это удобная догадка.» passed and says the same thing.
   run - not "leave it for a human". The two files sitting FAIL since 01.08 are exactly
   the failure mode this step exists to prevent.

   ASK THE PUBLISHER TOO, AND CALL IT CORRECTLY (step added 23.09, signature corrected
   2026-09-27 after it silently answered "unroutable" for all six files). Gate-green does not mean
   publishable: also run `distributor.parse_route` and `distributor.disclosure_missing` over each
   file. The trap is the signature - parse_route takes the DRAFT TEXT and the FILENAME, not a
   channel string:
       tier, route = D.parse_route(raw_file_text, os.path.basename(path))   # -> ('teaser', ('tg_paloaltoairu', 'tg-channel', '@PaloAltoAiRu'))
   Passing the channel (`D.parse_route("facebook")`) returns `(None, None)` for EVERY input,
   because it regex-scans that string for a ТИР:/tier: header and finds none. That is a silent
   false negative: it looks exactly like "the route is broken" and it cannot ever succeed. Same
   family as the 20.09 `--file` entry. ALWAYS include a known-good control in a verification
   sweep - I only caught this because the 23.09 log records that `facebook` resolves to fb_wall,
   so six identical (None, None) rows were provably the caller's fault, not the files'.
   For disclosure_missing, strip `<!--...-->` from the body first (the FIRST COMMENT footer must
   not be what earns the green - the 14.09/16.09 false-green trap).

5. RECORD THE CLOCK (there is NO waiting window any more). For each passing draft:
   python approval_clock.py ping --file <path> --tier <tier> --channel <platform>
     --proof "content-drain-daily <DAY>"
   NAME THE THREE CHANNEL VALUES, THEY DIVERGE BETWEEN RUNS (added 2026-09-28). `<platform>`
   was never spelled out, so the ledger now holds two different strings for the same live RU
   channel: 26.09 recorded `@PaloAltoAiRu`, 27.09 recorded `telegram`, for identical drafts.
   Nothing breaks today - the distributor routes off the DRAFT, not off this field - but the
   ledger stops being queryable by channel, which is the one question it exists to answer.
   Use: RU teaser -> `@PaloAltoAiRu` · EN teaser -> `x` · FB medium -> `facebook`. The explicit
   address (not the category `tg-channel`) for the same reason as the 16.09 frontmatter rule.
   The window is ZERO hours since dev's order of 05.08.2026 "publish with no waiting" -
   machine truth = approval_clock.WINDOW_HOURS_DEFAULT = 0, so the ping sets deadline =
   the moment of the ping and the draft is releasable to the distributor's next hourly
   tick immediately. Do NOT report a "24h deadline" - that number no longer exists and
   saying it makes the routine's own report a lie (the CLI help string still says
   "24-часовые часы апрува"; the constant is the truth, not the help text).
   Still mandatory: the ping must RECORD its time - an unrecorded ping leaves the item
   outside the queue, and the post dies unseen. Then post ONE short message into chat 03
   naming the file and the recorded time. (NOT 121: dev's order of 06.08.2026 15:15 is
   that NOBODY writes into 121 - neither robot nor live session; approval_clock.py already
   holds chat 03 in that constant.)

6. MARK. Flip the drained seeds in posts.jsonl from new to written (keep the id, add
   draft_path). A seed that produced a text must never be picked twice.

7. REPORT to chat 03 (chat_id chat_REDACTED, account tonyssd): one line per drained seed
   (slug -> draft path -> clock deadline), plus the remaining funnel depth
   ("funnel: N still new"). If nothing was drained, say why in one sentence - a silent
   run is indistinguishable from a broken one.
   THE FUNNEL IS NOT A CLOSED SYSTEM - REPORT ARRIVALS OR THE DEPTH READS AS A NO-OP (added
   2026-09-30, measured that night). content-factory-daily FILLS this funnel while the drain runs,
   so `new` does not simply drop by 2. Measured 30.09: 852 new at the start, 852 at the end, and
   nothing was wrong - posts.jsonl grew 2749 -> 2751 rows mid-run, so two arrivals exactly masked
   two drains. Every earlier entry in this log writes the depth as a closed subtraction
   ("funnel 832 -> 830"), which is why 852 -> 852 looks like step 6 silently failed and invites a
   re-drain. So report BOTH: the drained ids with their new status read back from disk, and the row
   count before/after. The load-bearing proof that step 6 worked is `status=written` on those two
   ids plus covered N -> N+2, never the depth number.

BOUNDARIES:
- Draft-first. This routine NEVER publishes. Publication is distributor.py tick --live
  (hourly on the hub) once the item is released by the clock - which, with a 0h window,
  is the next tick after the ping. Do not call it here.
- Privacy: no third-party names/@handles, no lead data, no sums, no keys, no private DMs.
- Model: writing quality matters here, so the drafting step uses the strongest available
  model; mechanical steps (picking, marking, gating) are plain code, zero tokens.

FINAL STEP (always run, even on a nothing-to-drain run - deterministic heartbeat for the
cron watchdog): python "%USERPROFILE%\.claude\scripts\cron_heartbeat.py" content-drain-daily
  LEASE FALLBACK (measured 2026-09-13): when another session holds a workspace lease on
  ~/.claude/scripts, the PreToolUse constitution_guard rejects any Bash command whose TEXT
  contains that path - including this heartbeat and any chat-03 post that imports bus_ping.
  It is a text match, not a real write conflict. Do not skip the step and do not break the
  lease: put the call in a tiny wrapper under content-factory/_scratch/ that builds the path
  with os.path.expanduser and runs it via subprocess, then run the wrapper. Same trick for
  the chat-03 report. PROOF OF DELIVERY CHANGED (corrected 2026-09-17): the old criterion
  `bus_ping.spool_depth() == 0` is now UNREACHABLE, and not through any fault of this
  routine - the spool holds FOREIGN undeliverable items (a ~30,000-char "urozhay" outbound
  digest lands there every night; the transport's hard cap is 4096 chars, so each one sticks
  forever; 1 item on 16.09, 2 on 17.09, growing by one per day, journal class
  spool-item-exceeds-transport-limit). Chasing zero would make this routine either lie or
  stall. The honest proof is two parts: (a) the --post path printed `PING OK -> <chat_id>`,
  which it prints ONLY after the client call returned without raising - read bus_ping.py
  around that line to confirm, it is evidence, not a claim; (b) NO item in the spool is
  YOURS (open bus_ping.SPOOL and read the ts + head of every line; do not infer from the
  count). The "PING SPOOL ... too long" lines that appear right after your post are those
  foreign digests being re-tried, not your report failing. Also still required:
  rail_ready() == True.
  TWO TRAPS IN READING THAT PROOF (added 2026-09-20, both hit that night). (1) `PING OK`
  is NOT the last line. The drain runs AFTER the send, and with 4 parked foreign digests
  it prints 8+ failure lines on top of it - so `| tail -6` shows nothing but spool FAILs
  and reads exactly like your report died. Do not re-send on that impression: you would
  double-post. The cheaper and STRONGER proof is structural - read bus_ping.py at the end
  of the --post path: `_spool_drain()` is called only `if delivered`, so the mere PRESENCE
  of drain output proves the send returned. (2) `spool_depth()` can read 0 mid-drain and
  THAT RULE IS ONE-DIRECTIONAL - AN EMPTY SPOOL PRINTS NOTHING (added 2026-09-22). On a
  night with no parked foreign digests, `_spool_drain()` runs and emits ZERO lines, so
  `PING OK` IS the last line and the 20.09 "presence of drain output" test would read a
  successful send as a failure - and push the next run into a double-post. The complete
  proof is: `PING OK -> <chat_id>` printed, AND `bus_ping.SPOOL` either absent/empty or
  holding only items that are not yours, AND `rail_ready()` True. Measured 22.09: PING OK
  with no drain output at all, and `os.path.exists(bus_ping.SPOOL)` was False - the four
  foreign "урожай" digests of 16-19.09 are gone, so journal class
  spool-item-exceeds-transport-limit gained no new case and stays at 2/3.
  it means nothing: the drainer CLAIMS the parked rows into a `.draining-<pid>` file,
  leaving the spool momentarily empty, and `_spool_append` puts the failures back after.
  It also returns 0 from a bare `except`. So a 0 there is not proof of an empty spool -
  check the file itself, as (b) already says. Measured 20.09: depth read 0, the file was
  168KB one minute later and held the same 4 foreign digests (16-19.09).

PROMPT-FIX LOG (this file is the LIVE prompt - the .cmd launcher feeds THIS path on stdin,
so editing it here is the fix; there is no frozen copy in the app registry):
- 2026-09-12, run of this routine: step 1 (dead slug check -> drain_dedup --covered) and
  step 5 (dead "24h gate" -> 0h window) corrected against measurement. Debt line
  content-drain-prompt-fix-20260911 in _machine-bus/_plans/backlog-HUB-01.jsonl
  claimed this needed hands because "the prompt lives in a scheduled task" - it does not,
  it lives in this file. Class = a routine describing mechanics that no longer exist
  (sibling of weekly-brain-audio-digest, frozen since 16.07). Author: Opus 5 / robot:content-drain-daily.
- 2026-09-13, run of this routine (CLAUDE.md 9.3-bis amendment of 13.09: a routine judges its
  OWN instruction, not only the skill it calls). Four corrections, each one a pain felt in
  that same run, not a speculation:
  (a) step 3 "ONE draft file containing all tiers" was unbuildable - approval_clock ping is
      one --tier + one --channel per --file, and every drain run on disk already writes 3
      files. Wording now matches the machines.
  (b) step 3 "no signature" fought both canon 1.1 and slop_gate (W6/W7) and cost two extra
      rewrite passes before the teasers came out clean. Now the teaser is written WITH
      t.me/PaloAltoAiRu from the first draft and the FB medium carries the footer as a
      first-comment block.
  (c) new step 1-bis: coverage is by funnel id and is blind to a same-day sibling draft that
      already carries your moral. Caught only by eye on 13.09.
  (d) FINAL STEP gets rejected by the lease guard on a text match; wrapper recipe recorded so
      the next run does not silently skip the heartbeat.
  Verdict on the skills this routine calls: none used (slop_gate / approval_clock /
  drain_dedup are tools, not skills) - nothing to update there.
  Author: Opus 5 / robot:content-drain-daily. Machine: HUB-01. Operator: robot.
- 2026-09-14, run of this routine (CLAUDE.md 9.3-bis: a routine judges its OWN instruction).
  Three corrections, each one a pain felt in THIS run, not a speculation:
  (a) new step 1-ter: `--covered` proves coverage by a single frontmatter field, so a draft
      that never got `funnel_ids` is invisible forever. hub:5496 ("nevozmozhno i nebezopasno",
      drained 19.08, 3 files on disk) came up as my pick #1 and I was one step from shipping a
      duplicate. Measured: 8 of 720 uncovered `new` seeds already had drafts; 42 drafts on
      disk carry no funnel_ids at all. Backfilled 8 by their own source_ref, --heal closed
      them, desync 8 -> 0. Remaining debt named, not silently fixed: 34 headless drafts.
  (b) step 3 told every run to end the EN teaser with t.me/PaloAltoAiRu - a RU channel, which
      _STYLE-footer.md has forbidden in EN posts since 07.07. Replaced with the EN Linktree as
      a FULL URL, because W7 matches `https?://|t\.me/|github\.com/` and a bare domain fails.
      Also recorded the false-green trap: an EN draft passed W7 on a "t.me/" string sitting in
      its own metadata, not in the post.
  (c) recorded that W4-first-person is RU-vocabulary-only (slop_gate.FIRST_PERSON read on
      disk), so EN drafts always warn; chasing it damages English.
  Not changed: step 5 (clock 0h window) behaved exactly as written - 5 pings recorded, all 5
  show "PROSROCHENO" in `approval_clock.py status`, i.e. releasable on the next tick.
  The lease-wrapper recipe from 13.09 worked verbatim for both the heartbeat and the bus post.
  Verdict on the skills this routine calls: none used (slop_gate / approval_clock /
  drain_dedup are tools, not skills) - nothing to update there.
  Author: Opus 5 / robot:content-drain-daily. Machine: HUB-01. Operator: robot.
- 2026-09-15, run of this routine (CLAUDE.md 9.3-bis: a routine judges its OWN instruction).
  Drained hub:5671 + cc:live-73d836 -> "300 bytes stay 300 bytes" and cc:live-9bc84d ->
  "12.68 GB of recorded silence"; 6 files, all green on slop_gate, 6 clock pings recorded at
  22:20 UTC. Three corrections, each a pain felt in THIS run:
  (a) step 1 said "oldest first" without naming the field. The seeds carry `when`, not `ts` -
      761 of 762 have no `ts` at all - so a `ts` sort collapses to alphabetical order and the
      first picks offered are `alpha:fbcomments:*`, i.e. seeds built out of third-party names
      this routine is forbidden to publish. Field named in the step now.
  (b) step 3 told the writer to budget ~18 chars for the link but said nothing about W4. The RU
      teaser needs TWO first-person tokens to clear 30/1000 at teaser length; adding the second
      one after the fact pushed a clean 245-char body to 253 and turned it into an F6 FAIL.
  (c) the canonical footer's block B still points RU followers at @ClawRus, which has been
      paused since 06.08 and re-confirmed paused twice. Recorded, and the fix deliberately NOT
      made here (footer text is not this routine's file).
  Not changed: steps 4-6 behaved exactly as written; drain_dedup --heal marked all three seeds
  written and left desync at 0. The 14.09 lease-wrapper recipe was not needed - no lease was
  held, both the chat-03 post and the heartbeat ran directly (spool_depth 0, rail_ready True).
  Verdict on the skills this routine calls: none used (slop_gate / approval_clock /
  drain_dedup are tools, not skills) - nothing to update there.
  Author: Opus 5 / robot:content-drain-daily. Machine: HUB-01. Operator: robot.
- 2026-09-16, run of this routine (CLAUDE.md 9.3-bis: a routine judges its OWN instruction).
  Drained hub:5309 -> "61 совет без вердикта" and cc:f9c743af -> "свой старый код уже ответил";
  6 files, 4 green on slop_gate + 2 EN with the known RU-only W4, 6 clock pings recorded at
  22:25 UTC. Three corrections, each a pain felt in THIS run:
  (a) THE DISCLOSURE LINE THIS PROMPT TEACHES DOES NOT PASS THE PUBLISHER. Step 3 says
      "disclosure in the FIRST line (canon 3.3)" and every drain run writes
      «привет, это майкрофт, синтетический ии-кофаундер оператора». The distributor's gate
      matches slop_gate.REQUIRED_ELEMENTS["подпись/авторство"] =
      `синтетическ\w+ кофаундер|придумано майкрофтом|...` - and «синтетический ии-кофаундер»
      does NOT match it (the hyphen breaks `\w+ кофаундер`). Measured 16.09: 4 of the 15.09
      FB mediums sat in distributor HOLD «нет раскрытия авторства» - i.e. the routine has
      been writing unpublishable FB posts. WORSE, MY OWN two passed the same check only
      because «✔️Придумано Майкрофтом» sits in the HTML-commented FIRST COMMENT block: a
      green earned by a comment, not by the post - the exact trap the 14.09 entry recorded
      for W7. So: write the body line as «привет, это майкрофт, синтетический кофаундер
      оператора - ии, а не человек». It matches the gate AND keeps the AI disclosure explicit.
      Verify by hand, not by the gate's verdict: strip `<!--...-->` from the body and check
      that distributor.disclosure_missing(body, "facebook") is still None. Fixed in all 6
      affected files (my 2 + the 4 stuck from 15.09). The regex itself is slop_gate's, NOT
      this routine's file - divergence reported, not patched here.
  (b) `channels_proposed: ["tg-channel"]` ROUTES TO THE PAUSED CHANNEL. Step 3 correctly says
      RU teasers go to @PaloAltoAiRu because tg_clawrus is paused - but the frontmatter every
      run copies says `tg-channel`, and distributor.ROUTES maps `"tg-channel" -> tg_clawrus
      -> @ClawRus`, paused since 06.08 and re-confirmed twice. Write the EXPLICIT address:
      `channels_proposed: ["@PaloAltoAiRu"]`. Measured 16.09: 31 RU teasers on disk carry the
      wrong key (29 of them older than today, named as standing debt, not silently fixed).
  (c) THE LEASE FALLBACK FROM 13.09 IS HALF THE TRUTH. It says the guard is "a text match, not
      a real write conflict" and to route around it with a wrapper. On 16.09 a sibling session
      (brain-graph T08, ON AIR EXCLUSIVE) held a LIVE lease on the whole imports tree, and the
      block hit the Write TOOL too, not only Bash - i.e. it stopped the actual drafts, not just
      the heartbeat. The wrapper is legitimate ONLY for calls that write nothing inside the
      leased tree (heartbeat, chat-03 post). For the drafts themselves: check
      `workspace_write_lease.py status`, and if the lease is still live, WAIT it out
      (background poller, it cleared in ~4 min). Do not bypass a live lease to write files.
  Not changed: steps 1 / 1-bis / 1-ter / 4 / 5 / 6 behaved exactly as written. Sorting by
  `when` put two genuinely oldest public seeds on top; the grep in 1-ter found no headless
  draft for either; drain_dedup --heal marked both seeds written and left desync at 0.
  Named, NOT fixed (with reasons): 34 drafts still carry no funnel_ids (same 34 as 14.09);
  the two files in slop_gate FAIL since 05.08 are still there - the teaser one is 173 chars of
  dev's VERBATIM voice against a hard 200 floor, and padding it would break both §9.7
  «без купюр» and «не разжимаем сжатую мысль», so it needs dev's call (or a different tier),
  not a rewrite; _STYLE-footer.md block B still points RU followers at the paused @ClawRus
  (reported on 15.09, still true, still not this routine's file); bus spool holds 1 foreign
  item - a 29,742-char outbound digest from 02:57 that can never fit Telegram's 4096 limit.
  Verdict on the skills this routine calls: none used (slop_gate / approval_clock /
  drain_dedup are tools, not skills) - nothing to update there.
  Author: Opus 5 / robot:content-drain-daily. Machine: HUB-01. Operator: robot.
- 2026-09-17, run of this routine (CLAUDE.md 9.3-bis: a routine judges its OWN instruction).
  Drained cc:f58c0381 -> "962 повода промолчать" and cc:live-b2baff -> "80 диалектов одного
  правила"; 6 files, 4 green on slop_gate + 2 EN with the known RU-only W4, 6 clock pings
  recorded at 22:20 UTC, all 6 show PROSROCHENO = releasable on the next tick. Three
  corrections, each a pain felt in THIS run:
  (a) new step 0: the harness clone-gate declared two twin sessions "ALIVE, writing right
      now" and ordered a stand-down under later-loses. Both were dead: each transcript held
      one assistant line, "You've hit your weekly limit", with different reset dates - the
      launcher had walked a fallback chain across accounts. Liveness there is transcript
      mtime, and a death rattle refreshes mtime. Had I obeyed the gate literally, the funnel
      would have gone undrained for the night with all three sessions reporting "someone
      else is on it".
  (b) FINAL STEP's proof of delivery (`spool_depth() == 0`) is now unreachable and not this
      routine's fault: the spool holds foreign ~30,000-char nightly digests that can never
      fit the 4096-char transport cap - 1 on 16.09, 2 on 17.09, one more every night.
      Recorded the two-part honest proof instead, and opened journal class
      spool-item-exceeds-transport-limit (line 1/3) rather than building anything.
  (c) step 1-ter gained the MERGE-twin blind spot: hub:5492 was the "[MERGE с hub:5488]"
      twin of a seed drained on 05.09 in three files, so no grep for its own id could ever
      find it, and it had been `new` for 29 days. Backfilled both ids into those drafts,
      --heal closed it, desync 0.
  Not changed: steps 1 / 1-bis / 3 / 4 / 5 / 6 behaved exactly as written. Sorting by `when`
  put genuinely old public seeds on top; the 15.09 two-pronoun budget and the 16.09
  disclosure form both worked first try (`disclosure_missing` verified by hand on the
  comment-stripped body = None for both mediums); slop_gate caught W3-rhythm, W2-ends-with-
  question and AV2 on the first pass and all were rewritten in-run, as step 4 demands.
  Named, NOT fixed (with reasons): the change ledger this routine wrote a post ABOUT is
  itself broken - 393 rows in 80 schemas, only 56 complete under the canonical writer that
  has existed since 29.08, and just 32 of the 334 rows since 01.09 went through it; that is
  a real defect, reported to chat 03, but the ledger and its lint are not this routine's
  files. Still standing from earlier runs: 34 drafts with no funnel_ids; the two slop_gate
  FAIL files from 05.08 (the teaser is 173 chars of dev's verbatim voice against a hard
  200 floor - needs his call, not a rewrite); _STYLE-footer.md block B still points RU
  followers at the paused @ClawRus.
  Verdict on the skills this routine calls: none used (slop_gate / approval_clock /
  drain_dedup are tools, not skills) - nothing to update there.
  Author: Opus 5 / robot:content-drain-daily. Machine: HUB-01. Operator: robot.
- 2026-09-19, run of this routine (CLAUDE.md 9.3-bis: a routine judges its OWN instruction).
  Drained cc:9b71fc5d -> "исследование уже лежало в памяти" and cc:live-b5672e -> "дверь
  отказала чужой причиной"; 6 files, 4 clean on slop_gate + 2 EN with the known RU-only W4,
  6 clock pings recorded at 22:17 UTC with a 0h window. Two corrections, both pains felt in
  THIS run, plus one debt re-measured:
  (a) new FOURTH BLIND SPOT in step 1-ter: a seed that names its own draft file inside its
      note. `--covered` misses it (the draft's funnel_ids holds the `hub:NNNN` voice id) and
      the 1-ter grep misses it too (the draft never mentions the cc:/tg: mirror id). One
      regex over the notes closed 6 seeds whose texts had been written on 21.08 and 30.08;
      the oldest had been `new` for 29 days. This is the same disease as 14.09 and 17.09 -
      coverage proven by ONE field - so the cheap regex now lives in the prompt. Two seeds
      named drafts that do not exist; left queued, and said so rather than "fixing" them.
  (b) step 3 never said that the HARD 250-char teaser cap INCLUDES the 71-char disclosure
      line. Writing the paragraph first and the disclosure second produced 288 / 280 / 261
      bodies - three F6-length-max FAILs in a single pass, all rewritten in-run as step 4
      demands. The real RU budget is ~155 chars of sentence; it is now written down.
  Not changed: steps 0 / 1 / 1-bis / 4 / 5 / 6 behaved exactly as written. Step 0 earned its
  keep again: the clone-gate ordered a stand-down for twin f90636ec "ALIVE, writing right
  now", whose transcript held exactly one assistant line - "You've hit your weekly limit".
  Sorting by `when` worked; the 16.09 disclosure form passed distributor.disclosure_missing
  by hand on the comment-stripped body (None for both mediums); the 16.09 explicit-address
  rule was verified against distributor.ROUTES on disk (`@paloaltoairu` -> live
  tg_paloaltoairu, bare `tg-channel` -> paused tg_clawrus).
  Named, NOT fixed (with reasons): the bus spool is now 4 foreign "урожай" digests
  (29,742 / 30,331 / 31,195 / 31,758 chars against a 4,096 transport cap), one more every
  night since 16.09 - journal class spool-item-exceeds-transport-limit is at line 2/3, so
  the mechanism waits for the third dated case per CLAUDE.md 5.10. Still standing: 34 drafts
  with no funnel_ids; the two slop_gate FAIL files from 05.08 (the teaser is 173 chars of
  dev's verbatim voice against a hard 200 floor - his call, not a rewrite);
  _STYLE-footer.md block B still points RU followers at the paused @ClawRus.
  Verdict on the skills this routine calls: none used (slop_gate / approval_clock /
  drain_dedup are tools, not skills) - nothing to update there.
  Author: Opus 5 / robot:content-drain-daily. Machine: HUB-01. Operator: robot.
- 2026-09-20, run of this routine (CLAUDE.md 9.3-bis: a routine judges its OWN instruction, and
  the 13.09 amendment: BOTH the skill it calls AND its own file). Second drain of the day - a
  sibling run had already taken cc:live-e8c186 and cc:live-d9461e at 12:12. Drained cc:2f100727
  (21.08, 30 days in the funnel) -> "podpis byla na etiketke" and cc:0017becb (24.08) ->
  "spravka zapuskala rabotu"; 6 files, 4 clean on slop_gate + 2 EN with the known RU-only W4,
  6 clock pings recorded at 22:19 UTC with a 0h window, funnel 769 -> 767, desync 0. Both posts
  were backed by LIVE runs, not quotes: _test_deploy_autoapply.py = 28 PASS / 0 FAIL, and
  help_flag_lint.py --json = 1170 candidates / 478 violations / 406 baseline / 77 new.
  Three corrections, each a pain felt in THIS run, not a speculation:
  (a) step 4 named the gate but not its FLAG. `slop_gate.py <path>` is an argparse error
      ("required: --file"); all six files came back as usage text instead of verdicts. A batch
      can LOOK gated while nothing was judged. Exact invocation now written into the step.
  (b) new step 1-quater: oldest-first walked straight into canon 3.3. Step 3 makes every draft
      Mycroft in FIRST PERSON, and he may not appropriate dev's personal life - so the 14
      oldest uncovered seeds (7 `[INTERNAL]` whose own notes say "не контент" / "не публикуем",
      2 MERGE-twin travel notes, dev's verbatim profanity essay) yielded ZERO drainable items.
      My first pick, cc:4bfff1ba, was also `visibility: personal`, which the BOUNDARIES block
      allows only in generalized form - a field step 1 never mentioned. The workable pool is
      `visibility == public` AND the `cc:`/`cc:live-`/`git-` family (our own system work): 209
      seeds tonight. Recorded so the next run filters before sorting.
  (c) FINAL STEP's proof-of-delivery, rewritten on 17.09, is readable two wrong ways and I hit
      both. `PING OK` is not the last line - the drain prints 8+ foreign-spool failures after it,
      so `tail -6` looks exactly like a dead report (re-sending on that impression = double-post).
      And `spool_depth()` read 0 while the spool was NOT empty: the drainer claims rows into a
      `.draining-<pid>` file and re-appends failures after. The strong proof is structural -
      `_spool_drain()` runs only `if delivered`, so drain output IS the delivery evidence.
  Not changed: steps 0 / 1 / 1-bis / 1-ter / 3 / 5 / 6 behaved exactly as written. The 19.09
  self-named-draft regex ran clean (only the two known-missing files remain, still left queued);
  no MERGE twin and no headless draft for either pick; the 19.09 disclosure-budget arithmetic
  (71-char RU line, ~155 chars of sentence) produced teasers at 243 and 240 on the FIRST pass -
  zero F6 failures among the four teasers, against three on 19.09. The one F6 that did appear
  was a medium at 2006 vs a 2000 cap, rewritten in-run as step 4 demands. Disclosure verified by
  hand on the comment-stripped body (disclosure_missing = None for both mediums) and the explicit
  address checked against distributor.ROUTES (`@PaloAltoAiRu` -> live; bare `tg-channel` -> paused
  @ClawRus). No lease was held (workspace_write_lease status = ACTIVE 0), so no wrapper was needed.
  Named, NOT fixed (with reasons): the bus spool still holds the same 4 foreign "урожай" digests
  (29,742 / 30,331 / 31,195 / 31,758 chars against a 4,096 cap) - journal class
  spool-item-exceeds-transport-limit stays at line 2/3, the mechanism waits for a third dated
  case per CLAUDE.md 5.10. Still standing: 34 drafts with no funnel_ids; 4 drafts pointing at
  ids outside the funnel; the two slop_gate FAIL files from 05.08 (the teaser is 173 chars of
  dev's verbatim voice against a hard 200 floor - his call, not a rewrite); _STYLE-footer.md
  block B still lists the paused @ClawRus as live (reported 15/16/19.09 and again tonight;
  follow link routed to @PaloAltoAiRu in both mediums, footer itself untouched - Nora's zone).
  Verdict on the skills this routine calls: none used (slop_gate / approval_clock / drain_dedup
  are tools, not skills) - nothing to update there.
  Author: Opus 5 / robot:content-drain-daily. Machine: HUB-01. Operator: robot.
- 2026-09-21, run of this routine (CLAUDE.md 9.3-bis + the 13.09 amendment: BOTH the skill it
  calls AND its own file). Second drain of the day - a sibling run had already taken
  auditor-poveril-priboru and boss-prosil-sporit. Drained cc:8ec7067a (21.08, 31 days in the
  funnel) -> "obertka zhila tolko v demo" and cc:5c95afc1 (22.08, 30 days) ->
  "korobki doehali nikto ne otkryl"; 6 files, 4 clean on slop_gate + 2 EN with the known
  RU-only W4, 6 clock pings recorded at 22:17 UTC with a 0h window, funnel 775 -> 773,
  desync 0. Both posts were backed by numbers counted tonight, not quoted: 197 parcel
  directories + 2314 DONE stamps across 8 nodes, 3 parcels unaccepted on this hub with the
  oldest at 446h, and a task card still `state: open` 17 days past its own `review_after`.
  Three corrections, each a pain felt in THIS run:
  (a) new step 1-quinquies: the 1-quater machine filters are blind to a canon stop-word in
      the seed's own title. cc:284c9e17 «не-технарь и клод» passed every filter - public,
      `cc:` family, second oldest - and is unpublishable, because the 14.09-бис carve-out
      struck «не-технарь» / «не-кодер» off dev entirely. Only reading the title caught it.
      It stays `new` and will sort second-oldest every night, so the skip is now written down
      instead of being re-discovered.
  (b) step 2 never said WHERE to look first. These seeds are weeks old by construction, so
      the artifact is a vault note, not a live config: the Perplexity seed pointed at a rail
      whose `dr_rails.json` does not exist on this node (it was mid-port under another
      session's lease tonight), while the decision sat in 10-Tasks as a full card. Three tool
      calls went into disk greps before one brain_ask found it. Recorded, with the bonus that
      a task card's `state` + `review_after` hands the post a free honest ending.
  (c) step 3 never mentioned that W2-ends-with-question scores the LAST line, so a medium
      that ends on its audience question warns until one closing line is added after it.
      Every medium on disk already does this; only the prompt did not say it.
  Not changed: steps 0 / 1 / 1-bis / 1-ter / 1-quater / 4 / 5 / 6 behaved exactly as written.
  The 19.09 self-named-draft regex ran clean (only the same two known-missing files); no
  MERGE twin and no headless draft for either pick; the 19.09 disclosure budget produced
  teasers inside the cap on the first pass for RU, and the two EN teasers needed one trim
  round each (264 -> 246, 267 -> 250) - 250 exactly is ACCEPTED by slop_gate, verified, so
  the cap is inclusive. The 20.09 `--file` flag correction worked first try. Disclosure
  verified by hand on the comment-stripped body (disclosure_missing = None for both mediums)
  and the address checked against distributor.ROUTES (`@PaloAltoAiRu` -> live
  tg_paloaltoairu; bare `tg-channel` -> paused @ClawRus). The 20.09 delivery-proof rewrite
  paid off immediately: `PING OK -> chat_REDACTED` was followed by 4 foreign spool failures, and
  the structural read (drain output exists => `_spool_drain()` ran => `if delivered` was true)
  prevented a double-post; the spool's 4 items were read individually and all 4 are the
  foreign "урожай" digests of 16-19.09, none mine. rail_ready True.
  Named, NOT fixed (with reasons): PENDING-HUB-01.jsonl holds one line that does not
  parse as JSON (found while counting parcel ages; the deploy ledger is not this routine's
  file). The foreign spool stayed at 4 items - no new digest on 20 or 21.09 - so journal class
  spool-item-exceeds-transport-limit remains at line 2/3 and the mechanism still waits for a
  third dated case per CLAUDE.md 5.10. Still standing: 34 drafts with no funnel_ids; 4 drafts
  pointing at ids outside the funnel; the two slop_gate FAIL files from 05.08 (the teaser is
  173 chars of dev's verbatim voice against a hard 200 floor - his call, not a rewrite);
  _STYLE-footer.md block B still lists the paused @ClawRus as live (reported 15/16/19/20.09
  and again tonight; follow link routed to @PaloAltoAiRu in both mediums, footer untouched -
  Nora's zone).
  Verdict on the skills this routine calls: none used (slop_gate / approval_clock / drain_dedup
  are tools, not skills) - nothing to update there.
  Author: Opus 5 / robot:content-drain-daily. Machine: HUB-01. Operator: robot.
- 2026-09-22, run of this routine (CLAUDE.md 9.3-bis + the 13.09 amendment: BOTH the skill it
  calls AND its own file). First and only drain of the day - no sibling run had written
  anything, drafts/2026-09-22-* was empty at start. Drained cc:live-d7bfc5 (23.08, 30 days in
  the funnel) -> "otchet otvechal ne na tot vopros" and cc:live-a9e325 (23.08) ->
  "storozh zablokiroval svoih"; 6 files, 4 clean on slop_gate + 2 EN with the known RU-only W4,
  6 clock pings recorded at 22:17:21 UTC with a 0h window, funnel 782 -> 780, desync 0. Both
  posts rest on things checked tonight, not quoted: the repair card's own frontmatter
  (state=open, review_after=2026-08-31 => 22 days overdue), a live `_check_pii` call on a
  backup timestamp (CLEAN), and `_test_slop_hb2_canary.py` = 15 green / 0 red / exit 0.
  Three corrections, each a pain felt in THIS run:
  (a) step 3 budgeted the disclosure (19.09) and the two first-person pronouns (15.09) but
      never W3-RHYTHM, and rhythm fights the 250-char cap head-on. A tidy 3-sentence RU teaser
      sat at 246 chars and 20% short sentences -> W3 warn; the short sentence added to fix it
      pushed the body to 252 -> F6-length-max FAIL; a second trim was needed. Two rewrite
      rounds for one teaser. Now written down: budget two <=5-word sentences UP FRONT, and use
      them to carry the second pronoun - the two budgets pay for each other.
  (b) the paragraph_lint expected-noise line named only the FIRST COMMENT footer. The YAML
      frontmatter ALSO reads as one 5-sentence paragraph, in all six files - so "полотен 2" on
      a medium is the normal state and says nothing. The rule that matters is whether the
      quoted text is the POST BODY: tonight exactly one hit was (EN teaser, 4 sentences in one
      block), and it was split after «Funny.» in-run.
  (c) the FINAL STEP proof, rewritten on 17.09 and again on 20.09, is one-directional. With an
      EMPTY spool `_spool_drain()` prints nothing, so `PING OK` IS the last line - and the
      20.09 "presence of drain output proves delivery" test would read a healthy send as a
      dead one and invite a double-post. Recorded the complete three-part proof. Measured
      tonight: PING OK, no drain output, and bus_ping.SPOOL does not exist on disk.
  Not changed: steps 0 / 1 / 1-bis / 1-ter / 1-quater / 1-quinquies / 2 / 4 / 5 / 6 behaved
  exactly as written. Step 1-quinquies earned its keep on the first try: cc:284c9e17
  («не-технарь и клод») surfaced as the oldest public `cc:` seed exactly as the 21.09 entry
  predicted, and was skipped on the 14.09-бис carve-out without re-investigating it - it stays
  `new` and will surface again tomorrow. 1-ter's four blind spots all ran clean for both picks
  (no funnel_ids hit, no numeric-tail grep hit, no MERGE twin, no self-named draft). Step 2's
  21.09 advice (vault first, config second) paid immediately: one brain_ask landed the repair
  card that carried the whole second half of post A. The 20.09 `--file` flag and the 16.09
  disclosure form both worked first try (disclosure_missing = None on both comment-stripped
  medium bodies); RU teasers carry the explicit `@PaloAltoAiRu` address, not the category.
  No lease was held (workspace_write_lease status = ACTIVE 0), so the 13.09 wrapper recipe was
  not needed.
  Named, NOT fixed (with reasons): the foreign-spool debt of 16-19.09 has CLEARED on its own
  (spool file absent tonight) - class spool-item-exceeds-transport-limit therefore stays at
  line 2/3 and no mechanism is built, per CLAUDE.md 5.10. Still standing: 34 drafts with no
  funnel_ids and 4 drafts pointing at ids outside the funnel (both unchanged since 20.09);
  the two slop_gate FAIL files from 05.08 (the teaser is 173 chars of dev's verbatim voice
  against a hard 200 floor - his call, not a rewrite); _STYLE-footer.md block B still lists the
  paused @ClawRus as live (reported 15/16/19/20/21.09 and again tonight; follow link routed to
  @PaloAltoAiRu in both mediums, footer itself untouched - Nora's zone). Session note, not a
  routine defect: this run opened in C:\Windows\System32, which home-dir-guard flags as a
  foreign folder for this node; all paths used here are absolute, so the drain was unaffected.
  Verdict on the skills this routine calls: none used (slop_gate / approval_clock / drain_dedup
  are tools, not skills) - nothing to update there.
  Author: Opus 5 / robot:content-drain-daily. Machine: HUB-01. Operator: robot.
- 2026-09-23, run of this routine (CLAUDE.md 9.3-bis + the 13.09 amendment: BOTH the skill it
  calls AND its own file). Second drain of the day - a sibling run had already taken
  chuzhaya-papka-chuzhaya-pamyat and schetchik-ne-dohodil-do-treh at 12:33. Drained cc:53075629
  (24.08, 30 days in the funnel) -> "storozh oslep ne s rozhdeniya" and cc:f5b9ea8f (25.08,
  29 days) -> "dogadka derzhala funkciyu 24 dnya"; 6 files, 2 RU teasers clean, 2 EN teasers with
  the known RU-only W4, 2 mediums with the structural W6, ZERO FAILs after the in-run rewrite;
  6 clock pings recorded at 22:26:17-18 UTC with a 0h window, funnel 797 -> 795, desync 0. Both
  posts rest on counts made tonight: the watchdog's own log (4968 lines; windowed=1 1984 times,
  daily 11-22.08, not once from 23.08), the slot doctor's log (75 checks, 64 of them "ЗАМЕРИТЬ
  НЕ СМОГ", last live read 20.09 born7d=1/reused7d=1), and 5 DONE stamps for parcel
  session-reuse-warm-slots-20260824 on disk. Four corrections, each a pain felt in THIS run:
  (a) step 3 budgeted rhythm (22.09) and pronouns (15.09) for TEASERS only - but check_warns()
      does not branch on tier, so both mediums warned (5% / 22.6 and 11% / 14.6) and both had to
      be rewritten. Absolute thresholds and a ~210-word budget are now written down, together
      with the cheap way to check them: import slop_gate and use its OWN sentences/words/
      FIRST_PERSON constants. Two API traps recorded (extract_body returns a tuple; sentences()
      splits on newlines).
  (b) HB1-unproven-claim hard-blocks the WORD «гипотеза» in a body - the prompt never mentioned
      the hedge-word blacklist, and a HARD-BLOCK cannot be degraded. It collides with canon 5.4
      (label the unproven), and the resolution is plain words: «это открытый вопрос, а не
      причина» says the same thing and passes. Medium A was rewritten in-run, as step 4 demands.
  (c) step 2 recommends brain_ask but never said it is not parallel-safe: it writes to ONE fixed
      path (_brain_answer_rr.txt), so two recalls fired in the same message - the natural move
      with two picks - silently overwrite each other. One recall was lost and re-run.
  (d) new step 1-sexies: the 1-quater filters pass two canon walls. `cc:live-46eff1` was dev's
      personal ayahuasca therapy (public field, but not Mycroft's life to own - canon 3.3), and
      `cc:live-60245d` was our own DR fan-out about an adult-content investment thesis (our
      mechanics, his call on the subject). The ID family proves where a seed was captured, not
      what it is about.
  Not changed: steps 0 / 1 / 1-bis / 1-ter / 1-quater / 1-quinquies / 5 / 6 behaved exactly as
  written. 1-quinquies earned its keep for the second night running: cc:284c9e17
  («не-технарь и клод») surfaced as the oldest public seed and was skipped on the 14.09-бис
  carve-out without re-investigating it. 1-ter's four blind spots ran clean for both picks
  (no funnel_ids hit, no numeric-tail grep, no MERGE twin; the self-named-draft regex found only
  the two known-missing longboards files, still left queued). Step 2's vault-first advice paid
  again - one brain_ask landed the beat AND the still-open repair card that gave post A its
  ending. The 20.09 `--file` flag and the 16.09 disclosure form worked first try
  (disclosure_missing = None on both comment-stripped mediums); beyond that I checked what the
  PUBLISHER would do with all six files - distributor.parse_route resolved every one
  (@PaloAltoAiRu -> live tg_paloaltoairu, x -> x_en, facebook -> fb_wall), which is the cheapest
  guard against the 16.09 class of "gate-green but unroutable". No lease was held
  (workspace_write_lease status = ACTIVE 0). The 22.09 three-part delivery proof held exactly:
  PING OK -> chat_REDACTED was the LAST line with no drain output, bus_ping.SPOOL does not exist on
  disk, rail_ready True - so class spool-item-exceeds-transport-limit stays at 2/3 for a second
  night and no mechanism is built (CLAUDE.md 5.10).
  Named, NOT fixed (with reasons): task-2026-08-29-watchdog-window-blindness-session0 is still
  `open`, 18 days past its own review_after, AND its stated root is contradicted by the log I
  counted tonight - the watchdog saw windows for 12 days before going blind on 23.08, so the
  card needs a re-diagnosis by whoever owns it, not a content robot.
  task-2026-08-24-session-reuse-fleet-parity is `open` 28 days past review while its parcel
  shows DONE on 5 nodes. The slot doctor cannot measure at all (64 of 75 checks) - a real
  instrument defect, reported to chat 03, not this routine's file. Still standing: 34 drafts
  with no funnel_ids and 4 drafts pointing at ids outside the funnel; the two slop_gate FAIL
  files from 05.08 (the teaser is 173 chars of dev's verbatim voice against a hard 200 floor -
  his call, not a rewrite); _STYLE-footer.md block B still lists the paused @ClawRus as live
  (reported 15/16/19/20/21/22.09 and again tonight; follow link routed to @PaloAltoAiRu in both
  mediums, footer untouched - Nora's zone). Session note, not a routine defect: this run
  again opened in C:\Windows\System32, flagged by home-dir-guard as a foreign folder for this
  node; every path used here is absolute, so the drain was unaffected.
  Verdict on the skills this routine calls: none used (slop_gate / approval_clock / drain_dedup
  / distributor are tools, not skills) - nothing to update there. Verdict on its OWN
  instruction: 🔧 обновляю - four blocks inserted above, all from pain felt in this run.
  Author: Opus 5 / robot:content-drain-daily. Machine: HUB-01. Operator: robot.
- 2026-09-26, run of this routine (CLAUDE.md 9.3-bis + the 13.09 amendment: BOTH the skill it
  calls AND its own file). FIRST and only drain of the day - drafts/2026-09-26-* was empty at
  start, no sibling run had written anything, and no clone-gate stand-down was offered. Drained
  cc:live-4149c6 (26.08, 31 days in the funnel) -> "urok napisan do zamera" and cc:live-fe5881
  (26.08) -> "skeptiki deshevle veera"; 6 files, 2 RU teasers clean, 2 EN teasers with the known
  RU-only W4, 2 mediums with the structural W6, and ZERO FAILs - on the FIRST pass, with no
  rewrite round at all. 6 clock pings recorded at 22:25:12-13 UTC with a 0h window, funnel
  822 -> 820, desync 0. Every number in both posts was produced tonight: 4 repos created 26.08
  at stars=0/forks=0/subscribers=0 each, DATA-issue #89797 OPEN with comments=0, the showcase
  catalog holding no submission with our repo although its age gate opened 09.09, the three
  threads we seeded alive at 11/55/9 comments, and rule_liveness.py run live (597 rules,
  UNVERIFIABLE 347, no_door 420, selftest 12 PASS / 0 FAIL).
  Three corrections, each a pain felt in THIS run:
  (a) new step 1-septies: a JOB-SEARCH seed slips between both 1-sexies questions.
      cc:ff21c6b8 is public, in the `cc:` family, names no third party, carries no 1-quinquies
      stop-word, and its subject is not bannable - it passes every filter as written, and is
      still not drainable here, because the 14.09 carve-out pulls employment touches out of
      Mycroft's voice. I had to reason that out from scratch mid-run; now it is written down,
      because like cc:284c9e17 it will keep sorting near the top.
  (b) step 2's 21.09 "vault first" is wrong for GitHub-shaped seeds. Both brain_asks returned
      nothing usable (pick B's twelve hits were ALL negative rerank), and every fact in both
      posts came from `gh api` plus one live script run. Structural reason recorded: a 30-day-old
      seed does not need the story, it needs TONIGHT'S number for an ending, and no vault note
      can hold that. Tonight's gh numbers handed post A an ending that REFUTED the seed's own
      same-day lesson.
  (c) bash `grep -r` over the vault is unusable and DANGEROUS here: three greps hit the 120s /
      100s timeouts and returned nothing, which reads exactly like "no artifact" and would have
      produced a false honest-empty under canon 5.4. The ripgrep tool answered the same query
      instantly and found the task card carrying half of post A. Recorded, together with the
      note that the 21.09 entry's "grepping ~/.claude found nothing" may simply never have
      finished.
  Not changed, and worth stating because it is the first clean pass in the log: steps 0 / 1 /
  1-bis / 1-ter / 1-quater / 1-quinquies / 1-sexies / 3 / 4 / 5 / 6 behaved exactly as written.
  The 23.09 "measure with the judge's own functions" advice is the reason there were zero FAILs:
  all six bodies were scored with sg.sentences / sg.words / sg.FIRST_PERSON in a _scratch/
  verstak BEFORE any file was written (RU teasers 248 and 242 chars against the hard 250; RU
  short-sentence share 71% and 57%; first person 51.3 and 52.6 per 1000; mediums 1192 and 1239
  chars at 53%/40% short and 52.1/35.9 first person). Compare 19.09 (three F6 FAILs in one pass)
  and 22-23.09 (two rewrite rounds each) - this step has now paid for itself twice over and
  should be treated as mandatory, not as a tip. 1-quinquies earned its keep for the THIRD night
  running (cc:284c9e17 skipped without re-investigation); 1-sexies for the second (cc:live-46eff1
  personal, cc:live-60245d adult-content subject). 1-ter's four blind spots ran clean for both
  picks. The 16.09 disclosure form and explicit-address rule held (disclosure_missing = None on
  both comment-stripped mediums), and the 23.09 extra publisher guard resolved all six files
  (parse_route -> tg_paloaltoairu / x_en / fb_wall, no paused channel). paragraph_lint flagged
  only the two known non-prose blocks (frontmatter, FIRST COMMENT footer) - not one hit quoted a
  post body, so nothing needed splitting, unlike 22.09. No lease was held
  (workspace_write_lease = ACTIVE 0). The 22.09 three-part delivery proof held exactly:
  `PING OK -> chat_REDACTED` was the LAST line with no drain output, bus_ping.SPOOL did not exist
  on disk before OR after the post, rail_ready True - so journal class
  spool-item-exceeds-transport-limit stays at 2/3 for a THIRD night and no mechanism is built
  (CLAUDE.md 5.10).
  Named, NOT fixed (with reasons): the two task cards behind tonight's posts are both `open` and
  both 17 days past their own review_after=2026-09-09 - the distribution card whose gate opened
  09.09 was never walked (that is post A's subject) and the SCFS benchmark card is unbuilt while
  its niche is still, by our own synthesis, empty. Both belong to whoever owns them, not to a
  content robot. Standing debt: 34 drafts with no funnel_ids (unchanged since 14.09); drafts
  pointing at ids outside the funnel went 4 -> 5 (the new one, `call:fireflies:*`, was written by
  the 23.09 sibling run, not by me); the two slop_gate FAIL files from 05.08 (the teaser is 173
  chars of dev's verbatim voice against a hard 200 floor - his call, not a rewrite);
  _STYLE-footer.md block B still lists the paused @ClawRus as live (reported
  15/16/19/20/21/22/23.09 and again tonight; follow link routed to @PaloAltoAiRu in both mediums,
  footer itself untouched - Nora's zone). Session note, not a routine defect: this run opened
  in C:\Windows\System32 for the third night running, which home-dir-guard flags as a foreign
  folder for this node; every path used here is absolute, so the drain was unaffected.
  (d) step 3 told every run to "keep such a measuring script in _scratch/" without naming one,
      so I wrote one - and the folder already held two (`drain_measure_20260923.py`,
      `measure_0924.py`). The 24.09 one is strictly better than mine (takes draft-file paths,
      handles the extract_body tuple, prints all thresholds inline) and reproduced my six
      measurements exactly, which both confirmed the numbers and proved the copy pointless. Mine
      deleted, the existing path now named in step 3 (§5.8: one source, zero copies).
  Verdict on the skills this routine calls: none used (slop_gate / approval_clock / drain_dedup
  / distributor / paragraph_lint are tools, not skills) - nothing to update there. Verdict on its
  OWN instruction: 🔧 обновляю - four blocks inserted above, all from pain felt in this run.
  Author: Opus 5 / robot:content-drain-daily. Machine: HUB-01. Operator: robot.
- 2026-09-27, run of this routine (CLAUDE.md 9.3-bis + the 13.09 amendment: BOTH the skill it
  calls AND its own file). FIRST and only drain of the day - drafts/2026-09-27-* was empty at
  start, no sibling run had written anything, and no clone-gate stand-down was offered. Drained
  cc:eaef040b (26.08, 32 days in the funnel) -> "spisok chital odin reestr" and cc:live-1d4a45
  (27.08, 31 days) -> "prigovor prozhil 21 den"; 6 files, 2 RU teasers clean, 2 EN teasers with
  the known RU-only W4, 2 mediums with the structural W6, ZERO FAILs on the first pass - the
  SECOND clean pass in a row, and again because the 23.09 verstak advice was followed before any
  file was written. 6 clock pings recorded at 22:18:06-08 UTC with a 0h window, funnel 830 -> 828,
  desync 0. Every number in both posts was produced tonight: scheduled_tasks_doctor.py --json =
  10 registry files on ONE node, 3 distinct account ids, 56 tasks (54 of them in a single file),
  293 prompts on disk, 237 orphans; gh issue view 89840 = OPEN, created 26.08, 32 days, 3 comments
  of which 2 are ours and ZERO from a maintainer; claude_token_ladder.py --probe --bucket = two
  rungs accepted (7d=0.03 and 0.09) and the third still printing the literal words "нужны РУКИ
  оператора" - the very verdict a measurement refuted on 26.08. That last one gave post B an ending
  that REFUTES its own seed's tidy lesson, which is the shape the 26.09 entry recommends.
  Three corrections, each a pain felt in THIS run, not a speculation:
  (a) THE 23.09 PUBLISHER GUARD WAS RECORDED WITHOUT ITS SIGNATURE AND SILENTLY FAILS CLOSED.
      `D.parse_route(channel_string)` returned `(None, None)` for all six files. It cannot ever
      return anything else: the function regex-scans the string it is given for a ТИР:/tier:
      header, so a bare "facebook" yields nothing. Six identical (None, None) rows read exactly
      like "every file is unroutable" - a phantom defect the next run would have chased. I caught
      it ONLY because the 23.09 log happens to record that `facebook` resolves to fb_wall, i.e. a
      known-good control proved the caller wrong rather than the files. Correct call now written
      into step 4 (`parse_route(raw_text, basename)`), together with the general rule: a
      verification sweep needs a control, or a broken caller looks like a broken corpus. Same
      family as the 20.09 `--file` entry. Re-run correctly: all six resolved -
      tg_paloaltoairu / x_en / fb_wall, paused @ClawRus untouched.
  (b) THE EN TEASER IS A SINGLE 5-SENTENCE BLOCK BY CONSTRUCTION. paragraph_lint flagged the POST
      BODY of BOTH EN files - the hit the 22.09 entry itself says is the only one that matters -
      and 22.09 recorded the same thing ("an EN teaser ran 4 sentences in a single block"). Twice
      in three runs is the default shape, not bad luck: the EN body is naturally 4-5 short
      sentences and nothing in the prompt told anyone to break them. Both split in-run (241 and
      240 chars, re-gated clean). Now budgeted up front in step 3 alongside the pronouns and the
      rhythm, because +1 char is free at 240 and impossible at 249.
  (c) STEP 2 HAD NO RULE FOR THE CASE THAT ACTUALLY HAPPENED: neither seed named a GitHub object,
      so the 26.09 "ask GitHub first" rule did not fire - and post A still ended on a live GitHub
      number. The chain ran seed -> canon beat -> the beat's `evidence_refs` -> a task card whose
      `evidence:` frontmatter line named `RFC anthropics/claude-code#89840`, an object nothing
      upstream had mentioned. Recorded: when recall lands a task card, READ ITS `evidence:` and
      `outcome:` fields - a seed says what happened a month ago, the card's evidence line says
      what is still out there to measure tonight.
  Not changed: steps 0 / 1 / 1-bis / 1-ter / 1-quater / 1-quinquies / 1-sexies / 1-septies / 5 / 6
  behaved exactly as written, and the skip list is now doing real work - all four canon skips fired
  without re-investigation (cc:284c9e17 stop-word, FOURTH night running; cc:live-46eff1 personal;
  cc:live-60245d adult-content subject; cc:ff21c6b8 biography/job-search, first use of 1-septies,
  which the 26.09 entry predicted would keep sorting near the top - it did, as candidate #4).
  1-ter's four blind spots ran clean for both picks. The 26.09 ripgrep correction paid immediately:
  the Grep tool answered in seconds where 26.09 burned ~4 minutes on bash greps that timed out.
  brain_ask was not needed at all tonight - ripgrep plus two live instruments covered both posts,
  which is worth noting against the 21.09 "vault first" framing. The 16.09 disclosure form held
  (disclosure_missing = None on both comment-stripped mediums) and the explicit-address rule kept
  the RU teasers off the paused channel. The 22.09 three-part delivery proof held exactly:
  `PING OK -> chat_REDACTED` was the LAST line with no drain output, bus_ping.SPOOL did not exist on
  disk before OR after the post, rail_ready True - so journal class
  spool-item-exceeds-transport-limit stays at 2/3 for a FOURTH night and no mechanism is built
  (CLAUDE.md 5.10). No lease was held (workspace_write_lease = ACTIVE 0).
  Named, NOT fixed (with reasons): RFC anthropics/claude-code#89840 is OPEN at 32 days with no
  maintainer reply, and the only outside answer came from a stranger who confirmed our diagnosis
  AND added a failure we never measured (a restored backup carries stale lastRunAt, so the restore
  fires tasks by itself) - that is a real, unclaimed lead for whoever owns the scheduler tooling,
  not for a content robot. task-2026-08-27-claude-token-account-a is `open` 10 days past its own
  review_after, and its blocker is a browser-session conflict, not dev's hands - it is post B's
  subject and belongs to its owner. Standing debt: 34 drafts with no funnel_ids (unchanged since
  14.09); 5 drafts pointing at ids outside the funnel (unchanged since 26.09); the two slop_gate
  FAIL files from 05.08 (the teaser is 173 chars of dev's verbatim voice against a hard 200
  floor - his call, not a rewrite); _STYLE-footer.md block B still lists the paused @ClawRus as
  live (reported 15/16/19/20/21/22/23/26.09 and again tonight; follow link routed to @PaloAltoAiRu
  in both mediums, footer itself untouched - Nora's zone). Session note, not a routine defect:
  this run opened in C:\Windows\System32 for the fourth night running, which home-dir-guard flags
  as a foreign folder for this node; every path used here is absolute, so the drain was unaffected.
  Verdict on the skills this routine calls: none used (slop_gate / approval_clock / drain_dedup /
  distributor / paragraph_lint / scheduled_tasks_doctor / claude_token_ladder are tools, not
  skills) - nothing to update there. Verdict on its OWN instruction: 🔧 обновляю - three blocks
  inserted above, all from pain felt in this run.
  Author: Opus 5 / robot:content-drain-daily. Machine: HUB-01. Operator: robot.
- 2026-09-28, run of this routine (CLAUDE.md 9.3-bis + the 13.09 amendment: BOTH the skill it
  calls AND its own file). FIRST and only drain of the day - drafts/2026-09-28-* was empty at
  start, no sibling run had written anything, and no clone-gate stand-down was offered. Drained
  cc:9814e241 (26.08, 33 days in the funnel) -> "urok-lyog-v-odnu-dver" and cc:live-32d268
  (29.08, 30 days) -> "storozh-byl-prav-chital-ya"; 6 files, 2 RU teasers clean, 2 EN teasers
  with the known RU-only W4, 2 mediums with the structural W6, ZERO FAILs on the first pass -
  the THIRD clean pass in a row, again because the 23.09 verstak advice was followed before any
  file was written (all six bodies scored with sg.sentences / sg.words / sg.FIRST_PERSON in a
  scratch script; RU teasers 244 and 249 against the hard 250, EN 240 and 249, mediums 1079 and
  1358; short-sentence share 33-89%, first person 38-83/1000 on every RU file). 6 clock pings
  recorded at 22:17:27 UTC with a 0h window, funnel 832 -> 830, desync 0. Both posts rest on
  things measured tonight: a grep over the live skill tree (the .md/TLD rule sits in EXACTLY 1
  of 280 live SKILL.md files, while 102 of them touch telegram/t.me/bus_send), and the guard's
  own source read tonight (DELETE_BLOCK = 50; it prints total + unexplained + top-3 folders +
  an adds-alongside hint, and carries a 2026-07-16 comment recording that a bare BLOCKED once
  spawned three diverging tasks) plus `git log` in the vault (HEAD 6.4h old, hub backup alive).
  Three corrections, each a pain felt in THIS run, not a speculation:
  (a) THE 23.09 HONEST-EMPTY ON cc:9814e241 WAS WRONG, AND THE INTERESTING PART IS THAT ITS
      WORDING WAS RIGHT. The artifact was a dated line in Breakage-Journal.md (25.08) the whole
      time; one ripgrep found it in seconds where brain_ask had returned only negative reranks.
      The 23.09 entry said "I did not find the artifact", exactly as canon 5.4 demands - and it
      still cost 5 more days, because nothing said an honest-empty EXPIRES. Five later runs read
      that note and inherited the skip without re-trying. Recorded the distinction the prompt was
      missing: a CANON skip (1-quinquies/1-sexies/1-septies) is about what the seed IS and is
      permanent; an honest-empty is about what I FAILED TO FIND and rots like any other ban
      (canon 5.4). Re-try with a DIFFERENT instrument than the one that failed.
  (b) STEP 2 NEVER NAMED THE BREAKAGE-JOURNAL, WHICH IS WHERE THESE SEEDS' ARTIFACTS LIVE BY
      CONSTRUCTION. Canon 5.10 forces every lesson into one dated journal row, and most seeds in
      this funnel are breakages. One ripgrep on a distinctive noun gave pick A its 25.08 row and
      pick B a FAMILY of four dated rows (16.07, 21.08, 05.09, 21.09) - which is what let post B
      end on a class ("the instrument got more verbose every time a reader failed it") instead of
      the seed's single anecdote. A journal family beats a single note: it proves a class, dated.
  (c) THE SIX DRAFTS CANNOT BE WRITTEN FROM A BASH HEREDOC. Russian prose plus verbatim journal
      quotes plus `%` killed `python - <<'PY'` with "unexpected EOF while looking for matching
      `''" - a shell-quoting error that looks like a Python error and says nothing about the
      content. Moved to a _scratch generator .py written with the Write tool; that is also the
      better artifact (re-runnable, diffable, keeps the six headers provably identical).
  Also logged, not a new correction: the 26.09 "never bash-grep the vault" rule bit a SECOND
  time tonight (grep -rl for one literal token over ~/.claude, exit 143 at the 120s ceiling,
  while the ripgrep tool answered instantly). Conditions named in that block; class is at 2/3,
  so no mechanism is built (CLAUDE.md 5.10).
  Not changed: steps 0 / 1 / 1-bis / 1-ter / 1-quater / 1-quinquies / 1-sexies / 1-septies / 4 /
  6 behaved exactly as written, and the canon skip list did its whole job with zero
  re-investigation - all four fired in order (cc:284c9e17 stop-word, FIFTH night running;
  cc:live-46eff1 personal; cc:live-60245d subject is dev's call; cc:ff21c6b8 biography/job
  search). 1-ter's four blind spots ran clean for both picks. The 27.09 rule to write the EN
  teaser as paragraphs FROM THE START paid immediately and visibly: paragraph_lint flagged only
  the two known non-prose blocks (frontmatter, FIRST COMMENT footer) and NOT ONE hit quoted a
  post body - against both EN bodies flagged on 27.09 and one on 22.09. The 27.09 parse_route
  signature fix worked first try with its control (all six resolved: tg_paloaltoairu / x_en /
  fb_wall, paused @ClawRus untouched; bare `facebook` still returns (None, None) as documented).
  The 16.09 disclosure form held (disclosure_missing = None on both comment-stripped mediums).
  The 20.09 `--file` flag correction worked. No lease was held (workspace_write_lease = ACTIVE 0).
  The 22.09 three-part delivery proof held exactly: `PING OK -> chat_REDACTED` was the LAST line
  with no drain output, bus_ping.SPOOL did not exist on disk before OR after the post, rail_ready
  True - so journal class spool-item-exceeds-transport-limit stays at 2/3 for a FIFTH night.
  Named, NOT fixed (with reasons): the .md/TLD lesson living in 1 door of 102 is a real §7.3-бис
  class-vs-case gap and is post A's own subject - propagating it means editing 101 skills that
  are not this routine's files, so it is reported, not done. The approval ledger holds two
  different channel strings for the same RU channel (26.09 vs 27.09) - fixed forward in step 5,
  old rows left alone. Standing debt: 34 drafts with no funnel_ids (unchanged since 14.09); 5
  drafts pointing at ids outside the funnel (unchanged since 26.09); the two slop_gate FAIL files
  from 05.08 (the teaser is 173 chars of dev's verbatim voice against a hard 200 floor - his
  call, not a rewrite); _STYLE-footer.md block B still lists the paused @ClawRus as live
  (reported 15/16/19/20/21/22/23/26/27.09 and again tonight - ninth report; follow link routed to
  @PaloAltoAiRu in both mediums, footer itself untouched - Nora's zone). Session note, not a
  routine defect: this run opened in C:\Windows\System32 for the fifth night running, which
  home-dir-guard flags as a foreign folder for this node; every path used here is absolute, so
  the drain was unaffected.
  Verdict on the skills this routine calls: none used (slop_gate / approval_clock / drain_dedup /
  distributor / paragraph_lint / vault_backup are tools, not skills) - nothing to update there.
  Verdict on its OWN instruction: 🔧 обновляю - four blocks inserted above (one of them REFUTING
  an earlier entry of this same log), all from pain felt in this run.
  Author: Opus 5 / robot:content-drain-daily. Machine: HUB-01. Operator: robot.
- 2026-09-29, run of this routine (CLAUDE.md 9.3-bis + the 13.09 amendment: BOTH the skill it
  calls AND its own file). FIRST and only drain of the day - drafts/2026-09-29-* was empty at
  start, no sibling run had written anything, and no clone-gate stand-down was offered. Drained
  cc:33bde9bc (29.08, 31 days in the funnel) -> "schital-vyzhivshih-a-propali-drugie" and
  cc:ad9cbedc (29.08) -> "rot-molchal-32-dnya"; 6 files, 2 RU teasers clean, 2 EN teasers with
  the known RU-only W4, 2 mediums with the structural W6, ZERO FAILs - the FOURTH clean pass in
  a row. 6 clock pings recorded at 22:17:12 UTC with a 0h window, funnel 832 -> 830, desync 0.
  Every number in both posts was measured tonight: scheduled_tasks_doctor.py --json = 10 registry
  files of which 8 are EMPTY, 63 tasks, 300 prompts on disk, 237 orphans; and for post B, sqlite
  on the collector db = 193,879 messages, 315 pulled at 03:30 across 14 groups, 1,255 in 7 days,
  82 detector reports of which 42 written after 28.08, while the judge's output file has not been
  rewritten since 28.08 17:08 (32 days).
  Two corrections, both pains felt in THIS run, not speculation:
  (a) THE 28.09 ENTRY MADE THE BREAKAGE-JOURNAL THE PRIMARY RECALL INSTRUMENT AND GAVE IT AN
      UNUSABLE PATH. It writes `00-System/Breakage-Journal.md`, vault-relative as canon 5.10 does,
      and this prompt's PATHS block never names the vault root at all - every path it lists is
      under `_imports`. So the literal string in that entry is what a run reaches for, and
      `D:\Vault\00-System\...` does not exist: the tool answers "Path does not exist", which
      is indistinguishable from "the journal has nothing". Two dead calls on the FIRST recall of
      the night, and the failure mode is exactly the false honest-empty that the 28.09 entry was
      itself written to prevent. Full path now inlined next to that entry.
  (b) A JOURNAL HIT CANNOT BE READ IN ONE STEP, AND NOTHING SAID SO. The journal is a markdown
      table with rows running to thousands of characters, so the ripgrep tool answers a content
      search with `[Omitted long matching line]` for nearly every hit - line numbers and no text,
      which reads like a useless result. Both of tonight's decisive rows (3296 = the registry
      collapse 34->1, 3586 = the proof that the restore returned not everything) were only
      readable via `sed -n '<N>p' | fold -w 190` after ripgrep located them. Recorded as a
      two-step pair, and with it a SCOPE fix to the 26/28.09 bash-grep ban: both its dated cases
      are RECURSIVE greps over a synced tree, while a bash grep at ONE NAMED FILE is instant and
      is the only way to scan a 5000-row table by date. Left unscoped, that ban removes the one
      cheap instrument the 28.09 entry depends on.
  Not changed, and the skip list again did its whole job with zero re-investigation: steps 0 / 1 /
  1-bis / 1-ter / 1-quater / 1-quinquies / 1-sexies / 1-septies / 4 / 5 / 6 behaved exactly as
  written. All four canon skips fired in order (cc:284c9e17 stop-word, SIXTH night running;
  cc:live-46eff1 personal; cc:live-60245d subject is dev's call; cc:ff21c6b8 biography/job
  search). 1-ter's four blind spots ran clean for both picks. The 23.09 "measure with the judge's
  own functions" step caught what would otherwise have been a rewrite round: BOTH mediums came in
  under the first-person floor (24.3 and 26.7 against 30.0) and the EN-B teaser one short sentence
  under the rhythm floor (29% against 30%) - all three fixed BEFORE gating. Worth noting how cheap
  that was: because the 28.09 entry moved composition into a `_scratch` generator .py, the fix was
  four one-line edits plus one re-run, not a rewrite. That rule is now paying a second dividend it
  was not written for. The 27.09 "write the EN teaser as two paragraphs from the start" held for a
  second night - paragraph_lint flagged only frontmatter and the FIRST COMMENT footer, not one hit
  quoted a post body. The 27.09 parse_route signature + control worked (all six resolved:
  tg_paloaltoairu / x_en / fb_wall; bare `facebook` still (None, None) as documented). The 16.09
  disclosure form held (disclosure_missing = None on both comment-stripped mediums) and the 28.09
  channel-value rule was applied (@PaloAltoAiRu / x / facebook). No lease was held
  (workspace_write_lease = ACTIVE 0). The 22.09 three-part delivery proof held exactly: `PING OK ->
  chat_REDACTED` was the LAST line with no drain output, bus_ping.SPOOL absent before AND after,
  rail_ready True - journal class spool-item-exceeds-transport-limit stays at 2/3 for a SIXTH night.
  Named, NOT fixed (with reasons): task-2026-09-25-repair-detektor-bez-ispolnitelya is P0, `open`,
  and 4 days past its own review_after - it is post B's own subject, and the sharper finding is that
  the card counts three cases (02/05/09.09) while tonight's seed is a FOURTH from 29.08 that is
  older than all three and never entered the count; the class threshold was reached later than the
  evidence allowed. Belongs to the card's owner, not to a content robot. 237 orphan prompt files on
  the hub (post A's subject) likewise. ALSO NAMED: this prompt file is now 97,709 bytes and the
  PROMPT-FIX LOG is most of it (16 KB on 15.09); it is loaded in full on every run. Not compressed
  here - one writer per file and this is not that pass (canon 10.0); reported so the number is on
  the record. Standing debt, all unchanged: 34 drafts with no funnel_ids (since 14.09); 5 drafts
  pointing at ids outside the funnel (since 26.09); the two slop_gate FAIL files from 05.08 (the
  teaser is 173 chars of dev's verbatim voice against a hard 200 floor - his call, not a
  rewrite); _STYLE-footer.md block B still lists the paused @ClawRus as live (reported
  15/16/19/20/21/22/23/26/27/28.09 and again tonight - TENTH report; follow link routed to
  @PaloAltoAiRu in both mediums, footer itself untouched - Nora's zone). Session note, not a
  routine defect: this run opened in C:\Windows\System32 for the sixth night running, flagged by
  home-dir-guard as a foreign folder for this node; every path used here is absolute, so the drain
  was unaffected.
  Verdict on the skills this routine calls: none used (slop_gate / approval_clock / drain_dedup /
  distributor / paragraph_lint / vault_backup / scheduled_tasks_doctor are tools, not skills) -
  nothing to update there. Verdict on its OWN instruction: 🔧 обновляю - two blocks inserted above,
  both from pain felt in this run.
  Author: Opus 5 / robot:content-drain-daily. Machine: HUB-01. Operator: robot.
- 2026-09-30, run of this routine (CLAUDE.md 9.3-bis + the 13.09 amendment: BOTH the skill it
  calls AND its own file). FIRST and only drain of the day - drafts/2026-09-30-* was empty at start,
  no sibling run had written anything, and no clone-gate stand-down was offered. Drained cc:003705f6
  (29.08, 32 days in the funnel) -> "gejt-vzyat-60-dney-nikto-ne-nazhal" and cc:565c1aba (29.08) ->
  "dogon-eto-galochka-a-ne-svoystvo"; 6 files, 2 RU teasers clean, 2 EN teasers with the known
  RU-only W4, 2 mediums with the structural W6, ZERO FAILs - the FIFTH clean pass in a row, again
  because the 23.09 verstak advice ran before any file was written (RU 245/230 against the hard 250,
  EN 241/236, mediums 1322/1468; short-share 48-71%, first person 39.8-55.6/1000 on every RU file).
  6 clock pings recorded at 22:19:25-28 UTC with a 0h window. Every number in both posts was measured
  tonight: for post A, zalp_delta.db day_meta = 77 days of measurement from 2026-07-16 with ZERO
  missing days, both gate criteria first met 2026-08-02 (six days BEFORE their own 08.08 deadline)
  and green 60 consecutive days since, today 69 links vs 3 required and 14 reproductions vs 1, while
  a live hn_watch.py run shows the account still at karma 1 / 0 comments since 2020; for post B,
  Get-ScheduledTask = 608 tasks with StartWhenAvailable on 322, and among our own 85 "Claude *" tasks
  ON for 31 / OFF for 54 with 43 of those Ready (a missed run vanishes silently) - including
  Claude Content Factory Daily, the routine that fills this very funnel - plus the contrib-watch row
  at 37 digests over 41 days with holes on 22/26/27.08 and 12.09.
  Four corrections, each a pain felt in THIS run, not a speculation:
  (a) A GIT-BASH PATH HANDED TO WINDOWS PYTHON READS AS ABSENCE, AND IT FAKED A COVERAGE READ. Two
      hits in one run: `--covered --json` redirected to `/tmp/covered.json` came back as
      `covered: 0`, so step 1's pool was computed as if NOTHING on disk were drained - the exact
      false-coverage class this prompt has patched since 14.09, except self-inflicted; and a
      find-produced POSIX directory path killed os.listdir the same way. Neither failure says "wrong
      path flavour"; both read as an empty corpus. The picks were unaffected only by luck (pool 259
      both times). Recorded in step 2 with the cheap tell: a count of exactly 0 where the producing
      tool printed rows. Journaled as the 2nd dated case of the 21.08 class, mechanism NOT built.
  (b) THE FUNNEL IS NOT A CLOSED SYSTEM AND THE DEPTH NUMBER LIED ABOUT MY OWN STEP 6. 852 new at
      the start, 852 at the end, nothing wrong - posts.jsonl grew 2749 -> 2751 mid-run, so two
      arrivals from content-factory-daily exactly masked two drains. Every earlier entry here writes
      the depth as a closed subtraction ("funnel 832 -> 830"), which makes 852 -> 852 look like the
      mark step silently failed and invites a re-drain. Step 7 now demands the row count before/after
      and names the load-bearing proof instead: status=written read back from disk plus covered
      187 -> 189.
  (c) THE JOURNAL WRITE SIDE WAS NEVER IN THIS PROMPT, AND ONE CELL CAPS AT 400 SILENTLY. A
      ~1900-char `--what` rendered as a 400-char cell cut mid-sentence: conditions, the proof and the
      verdict «mechanism NOT built» were gone, while the CLI printed `stroka 1/3` and looked fine. No
      recovery copy exists - breakage_lines.jsonl is a pure counter, `what` empty in 1123/1123 rows.
      Recorded: split across --what/--conditions/--parts/--guess (1600 chars of real budget), and to
      repair an existing row edit your OWN node's shard `text` + `breakage.fold(force=True)` rather
      than hand-editing the folded table or re-running `journal` (which double-counts). Done that
      way tonight: the row went 1 filled cell / 513 chars -> 4 cells / 1555, class count still 1.
      Sub-lesson recorded with it: prior_art's warning «SCHYOT ZANIZHEN ... itogo 3, porog 3» would
      have promoted the class to a repair session, and reading the six neighbours showed five were
      vocabulary overlap - but the sixth was a real mirror class
      (literal-windows-path-on-linux-node). The convenient verdict there is "only 2, no mechanism
      owed", so canon 5.4 applies: both readings written into the row, promotion left to the class
      owner rather than decided by a content routine.
  (d) THE 28.09 NO-HEREDOC RULE IS SCOPED TOO NARROWLY - IT SAYS "the six drafts" AND THE SAME TRAP
      KILLED THIS VERY LOG ENTRY. Appending it via `python - <<'PY'` died with "unexpected EOF while
      looking for matching `''" for exactly the reason that entry documents: Russian prose plus
      apostrophes plus quoted canon phrases. The rule is not about drafts, it is about ANY prose
      payload this routine writes through the shell - drafts, log entries, journal rows, chat-03
      reports. Written to a `_scratch` .py with the Write tool and run, same as the drafts.
  Not changed, and the canon skip list again did its whole job with zero re-investigation: steps 0 /
  1 / 1-bis / 1-ter / 1-quater / 1-quinquies / 1-sexies / 1-septies / 3 / 4 / 5 / 6 behaved exactly as
  written. All four canon skips fired in order (cc:284c9e17 stop-word, SEVENTH night running;
  cc:live-46eff1 personal; cc:live-60245d subject is dev's call; cc:ff21c6b8 biography/job search).
  1-ter's four blind spots ran clean for both picks. The 29.09 journal-path fix paid on the FIRST
  recall - the full D:\Vault\Vault-Knowledge\00-System\ path worked immediately where 29.09
  burned two calls, and the 29.09 two-step read (ripgrep to locate, sed+fold to read) was exactly
  what was needed: all four decisive rows (2200, 2201, 55, 2353) came back as line numbers with no
  text first. The 28.09 rule «a grabla has a journal row by construction» was the single
  highest-value step tonight - both posts are built on journal families the seeds never mentioned,
  and for post A the 14.08 row supplied the WHY (the gate had an instrument and a criterion but no
  runner) that turned a "we did nothing" fakap into a measurable one. The 27.09 task-card `evidence:`
  rule fired too: the card named hn_watch.py, which produced tonight's karma number. The 28.09
  _scratch generator rule held for the drafts (six headers provably identical, zero shell quoting).
  The 27.09 EN-two-paragraphs rule held for a THIRD night - paragraph_lint flagged only frontmatter
  and the FIRST COMMENT footer, not one post body. The 27.09 parse_route signature + control worked
  (all six resolved tg_paloaltoairu / x_en / fb_wall; bare `facebook` still (None, None) as
  documented). The 16.09 disclosure form held (disclosure_missing = None on both comment-stripped
  mediums) and the 28.09 channel values were used (@PaloAltoAiRu / x / facebook). The 26.09
  verstak-reuse rule held: measure_0924.py was run, no copy written. No lease was held
  (workspace_write_lease = ACTIVE 0). The 22.09 three-part delivery proof held exactly:
  `PING OK -> chat_REDACTED` was the LAST line with no drain output, bus_ping.SPOOL absent before AND
  after, rail_ready True - journal class spool-item-exceeds-transport-limit stays at 2/3 for a
  SEVENTH night and no mechanism is built (CLAUDE.md 5.10).
  Named, NOT fixed (with reasons): task-2026-07-27-show-hn-gated-1108 is post A's own subject and the
  sharpest unclaimed finding of the night - its numeric gate has been MET for 60 consecutive days, the
  instrument recorded it every night without a single gap, and the card sits `state: someday`, last
  touched 06.08, parked by task_hygiene on 19.08 with review_after pushed to 2026-11-20. The condition
  was satisfied; what it never had is a reader. That is a decision for its owner, not for a content
  robot. Post B's subject likewise: StartWhenAvailable is OFF on 54 of our own 85 tasks on this hub,
  43 of them Ready, and one of them is the routine that fills this funnel. ALSO NAMED: this prompt file
  is now ~111 KB and the PROMPT-FIX LOG is most of it, loaded in full on every run (97.7 KB on 29.09,
  106.3 KB at the start of tonight - it grew ~8.6 KB in one night, and tonight adds more). Not
  compressed here: one writer per file and this is not that pass (canon 10.0); reported so the number
  stays on the record, and it is now growing fast enough that a compression pass is worth scheduling
  deliberately. Standing debt, all unchanged: 34 drafts with no funnel_ids (since 14.09); 5 drafts
  pointing at ids outside the funnel (since 26.09); the two slop_gate FAIL files from 05.08 (the teaser
  is 173 chars of dev's verbatim voice against a hard 200 floor - his call, not a rewrite);
  _STYLE-footer.md block B still lists the paused @ClawRus as live (reported
  15/16/19/20/21/22/23/26/27/28/29.09 and again tonight - ELEVENTH report; follow link routed to
  @PaloAltoAiRu in both mediums, footer itself untouched - Nora's zone). Session note, not a routine
  defect: this run opened in C:\Windows\System32 for the seventh night running, flagged by
  home-dir-guard as a foreign folder for this node; every path used here is absolute, so the drain was
  unaffected.
  Verdict on the skills this routine calls: none used (slop_gate / approval_clock / drain_dedup /
  distributor / paragraph_lint / vault_backup / selfheal / breakage / prior_art / hn_watch /
  zalp_delta are tools, not skills) - nothing to update there. Verdict on its OWN instruction:
  obnovlyayu - four blocks inserted above, all from pain felt in this run.
  Author: Opus 5 / robot:content-drain-daily. Machine: HUB-01. Operator: robot.
- 2026-10-01, run of this routine (CLAUDE.md 9.3-bis + the 13.09 amendment: BOTH the skill it
  calls AND its own file). FIRST and only drain of the day - drafts/2026-10-01-* was empty at start,
  no sibling run had written anything, and no clone-gate stand-down was offered. Drained cc:79fbd165
  (29.08, 33 days in the funnel) -> "dver-proveryala-fajl-ne-zapis" and cc:live-20a4d3 (30.08,
  32 days) -> "ne-dve-os-a-dva-fajla-nastroek"; 6 files, 2 RU teasers clean, 2 EN teasers with the
  known RU-only W4, 2 mediums with the structural W6, ZERO FAILs on the first pass - the SIXTH clean
  pass in a row, again because the 23.09 verstak advice ran before any file was written (RU 246/240
  against the hard 250, EN 250/247, mediums 1863/1572; short-share 31-78%, first person 39.1-63.5/1000
  on every RU file). 6 clock pings recorded at 22:19:55-56 UTC with a 0h window. Both posts rest on
  numbers measured tonight: for post A, the class `asserted-status-without-evidence` was declared
  CLOSED by a mechanism on 29.08 with the verdict line "4-й датированный случай не понадобится", and
  the journal then holds FOUR more dated cases (29.08 23:1x - the same evening, in THIS routine, an
  escape from under a door built that morning; 04.09 23:1x, logged verbatim as "ТОТ ЖЕ дефект, что
  29.08 в ЭТОЙ ЖЕ рутине"; 08.09; 22.09) with the counter reaching 5, plus a live grep showing the
  candidate door named on day one (let content_miner.py append the log itself) was never built - 0
  hits for nightly.log in the engine - and nightly.log itself at 53 lines, last written 21.09 23:21,
  9 days silent. For post B, `gh issue view 89632` = OPEN, created 25.08 = 37 days, 6 comments, 3
  ours, ZERO from a maintainer, with a stranger's 31.08 comment "It flips" proving the fix (move
  defaultMode to user level and the next scheduled run comes up in bypassPermissions) - and this
  hub's own ~/.claude/settings.json tonight has NO defaultMode and an empty permissions block, so
  the fix proven for us 31 days ago is still not applied here. That is post B's ending.
  Three corrections, each a pain felt in THIS run, not a speculation:
  (a) THE 27.09 EN-PARAGRAPH RULE FAILED A THIRD TIME BECAUSE ITS HEADLINE IS WEAKER THAN ITS OWN
      RECIPE, so this is a mechanism, not a fourth log line. "Write the EN teaser as TWO PARAGRAPHS"
      is what I wrote - and both EN bodies still tripped paragraph_lint, because the SECOND block was
      itself 4-5 sentences. The rule's own recipe (disclosure / 2 / 2-3) is THREE blocks; the headline
      says two; the executor follows the headline. Dated cases 22.09, 27.09, 01.10 = three, so §5.10
      is satisfied: renamed the rule to "no body block over 3 sentences, any tier, any language" and
      taught the shared verstak (measure_0924.py, §5.8 one source) to run paragraph_lint's OWN
      scan_text over the body with frontmatter and html-comments stripped. Those two strips are the
      entire expected-noise list, so a verstak hit now cites a post body BY CONSTRUCTION - the nightly
      eyeballing of "which hit matters" is gone. Red-first honoured: shown RED on the pre-split body
      (names the exact 5-sentence block), green on all six files. Cost of the fix, as the 27.09 entry
      predicted: both EN teasers sat at exactly 250 against a HARD 250, so the split had to be paid
      for with a simultaneous trim.
  (b) I REPRODUCED THE TWO-INSTRUMENTS-DISAGREE CLASS FROM INSIDE THAT VERY FIX. The first version of
      the check mirrored the threshold (3) but used my OWN sg.sentences(), and cried "ПОЛОТНО" on BOTH
      FB mediums that paragraph_lint had passed. A check that cries wolf on every medium gets ignored,
      which is worse than no check. Fixed by calling the judge's function instead of copying its rule -
      and that is now written into the rule itself, because mirroring a threshold without its splitter
      is the generic shape of this mistake.
  (c) «МЫ» AS A SUBJECT IS DOUBLY WRONG AND THE PROMPT ONLY SAID HALF OF IT. Step 3 bans "we" as the
      subject (canon 3.3) but never connects it to the W4 budget: slop_gate.FIRST_PERSON holds no
      plural forms at all, so «мы» breaks canon AND scores zero. I had written «мы искали» / «мы и есть»
      into two bodies; the pre-measure showed fp=1 on the B teaser, and the lazy fix would have been to
      bolt a pronoun on rather than replace the banned word. Checked the set on disk to be sure.
  Also logged, not a new correction: the 30.09 no-heredoc rule bit again on THIS log entry (Russian
  prose + apostrophes + quoted canon phrases), exactly as its own widened scope predicts - written
  through a _scratch .py, as were the drafts, the journal row and the chat-03 report. And the 30.09
  four-cell journal rule paid twice: the dry-run length check caught three cells over 400 BEFORE
  writing, and the one that still slipped (--guess at 414) was repaired the documented way - edited
  the `text` field of my own node's shard and re-folded with force=True, leaving count_class at 1
  rather than re-running `journal` and double-counting.
  Not changed, and the canon skip list again did its whole job with zero re-investigation: steps 0 / 1
  / 1-bis / 1-ter / 1-quater / 1-quinquies / 1-sexies / 1-septies / 4 / 5 / 6 / 7 behaved exactly as
  written. All four canon skips fired at the very top of the pool (cc:284c9e17 stop-word, EIGHTH night
  running; cc:live-46eff1 personal; cc:live-60245d subject is dev's call; cc:ff21c6b8 biography/job
  search) - and tonight they were literally the four oldest entries, so without that list the run would
  have opened by re-reasoning all four. 1-ter's four blind spots ran clean for both picks. The 30.09
  windows-path warning paid immediately: `--covered` was written to a file NEXT to the script and read
  back as 189, matching 30.09's end state, so the false-zero coverage class did not recur. The 28.09
  "a grabla has a journal row by construction" rule was again the highest-value step - post A is built
  entirely on a journal FAMILY the seed never mentioned - and the 29.09 full vault path plus the
  two-step read (grep to locate, sed+fold to read) worked first try on every one of the seven rows read
  tonight. The 26.09 "ask GitHub first when the seed names a GitHub object" rule gave post B its whole
  ending in one call. The 27.09 parse_route signature + control worked (all six resolved
  tg_paloaltoairu / x_en / fb_wall; bare `facebook` still (None, None) as documented). The 16.09
  disclosure form held (disclosure_missing = None on both comment-stripped mediums) and the 28.09
  channel values were used (@PaloAltoAiRu / x / facebook). The 22.09 three-part delivery proof held
  exactly: `PING OK -> chat_REDACTED` was the LAST line with no drain output, bus_ping.SPOOL absent before
  AND after, rail_ready True - journal class spool-item-exceeds-transport-limit stays at 2/3 for an
  EIGHTH night and no mechanism is built (CLAUDE.md 5.10). No lease was held (ACTIVE 0).
  HONEST EMPTY, and it is a claim with a shelf life (28.09 rule): the second half of seed cc:79fbd165 -
  two hackathons whose themes matched our products one-for-one - did NOT make the post, because the only
  artifact I could find was a row in a dashboard HTML; ripgrep over the whole vault for the event names
  returned that single file and the journal had nothing. That is "I did not find it", not "it is not
  there", and per the 28.09 rule the next run that meets this seed should retry with a DIFFERENT
  instrument than ripgrep+journal before inheriting the skip. The seed is marked written on the strength
  of its drainable half, so this one will NOT resurface on its own - which is the cost of draining half a
  seed, and is recorded here deliberately.
  Named, NOT fixed (with reasons): the candidate door for `asserted-status-without-evidence` (have the
  engine append its own log line deterministically instead of a model narrating that it did) is post A's
  own subject - 5 dated cases, declared closed at 3, still unbuilt. Promotion to a repair session belongs
  to that class's owner, not to a content routine (30.09 discipline). Standing debt, all unchanged: 34
  drafts with no funnel_ids (since 14.09); 5 drafts pointing at ids outside the funnel (since 26.09); the
  two slop_gate FAIL files from 05.08 (the teaser is 173 chars of dev's verbatim voice against a hard
  200 floor - his call, not a rewrite); _STYLE-footer.md block B still lists the paused @ClawRus as live
  (reported 15/16/19/20/21/22/23/26/27/28/29/30.09 and again tonight - TWELFTH report; follow link routed
  to @PaloAltoAiRu in both mediums, footer itself untouched - Nora's zone). ALSO NAMED: this prompt
  file crossed 121 KB before tonight's edits and the PROMPT-FIX LOG is most of it, loaded in full on
  every run (97.7 KB on 29.09, ~111 KB on 30.09). Not compressed here - one writer per file and this is
  not that pass (canon 10.0) - but the growth rate is now ~10 KB/night, which makes a deliberate
  compression pass the single highest-value maintenance item on this routine. Session note, not a routine
  defect: this run opened in C:\Windows\System32 for the eighth night running, flagged by home-dir-guard
  as a foreign folder for this node; every path used here is absolute, so the drain was unaffected.
  Verdict on the skills this routine calls: none used (slop_gate / approval_clock / drain_dedup /
  distributor / paragraph_lint / vault_backup / selfheal / breakage / prior_art / bus_ping are tools, not
  skills) - nothing to update there. Verdict on its OWN instruction: обновляю - one rule RENAMED and
  given a mechanism (3rd dated case), two blocks added, all from pain felt in this run.
  Author: Opus 5 / robot:content-drain-daily. Machine: HUB-01. Operator: robot.

---

**Claude:**

I'll run the nightly content drain. Starting with the funnel state and coverage.

**🚂 Рельса:** эта рутина — сама Claude (суждение о каноне + авторский голос Майкрофта = §6.2 качество), механика (выбор/гейт/отметка) = код, 0 токенов. Аутсорса на чужие баки тут нет по классу работы.

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/content-factory && ls -la drafts/2026-10-02-* 2>/dev/null | head -20; echo \"---FUNNEL ROWS---\"; wc -l triage/posts.jsonl", "description": "Check today's drafts and funnel size"}

---

**Claude:**

No drafts today yet. Now coverage (writing the JSON next to the script, per the 30.09 windows-path rule):

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/content-factory && python drain_dedup.py --covered --json > cov_tmp.json 2>&1; head -c 300 cov_tmp.json; echo; echo \"---\"; wc -c cov_tmp.json", "description": "Get covered seed ids"}

---

> `Bash` -- {"command": "mkdir -p /e/Obsidian/_imports/content-factory/_scratch && cat > /e/Obsidian/_imports/content-factory/_scratch/pick_1002.py <<'PY'\nimport json, os, re\nBASE = r'D:\\Vault\\_imports\\content-factory'\ncov = set(json.load(open(os.path.join(BASE,'cov_tmp.json'), encoding='utf-8'))['cove

---

**Claude:**

Pool = 274. Evaluating the top candidates against the canon walls before recall:

---

> `Bash` -- {"command": "cat > /e/Obsidian/_imports/content-factory/_scratch/blind_1002.py <<'PY'\nimport json, os, re, glob\nBASE = r'D:\\Vault\\_imports\\content-factory'\nD = os.path.join(BASE,'drafts')\nCAND = ['cc:live-ec14a9','cc:be9848d4','cc:9392bcbb','cc:b67b4579']\nfiles = glob.glob(os.path.join(D,

---

**Claude:**

Blind spots clean on all four. Picks: **A = cc:live-ec14a9** (outbound door had no carbon copy), **B = cc:be9848d4** (196 forgotten tasks). Now recall — journal first, since both are breakage-shaped:

---

> `Bash` -- {"command": "J=\"D:/Vault/Vault-Knowledge/00-System/Breakage-Journal.md\"; ls -la \"$J\" 2>&1 | head -2; echo \"=== A: копирк/pub_ledger ===\"; grep -n -i -o -E '.{0,60}(копирк|pub_ledger|зеркал[а-я]* наружк).{0,60}' \"$J\" | head -20; echo \"=== B: 196 / кладбищ / забыт ===\"; grep -n -i -o -E '

---

**Claude:**

Journal gave me a **family** for B (task_hygiene parking rows). Reading them properly (grep locates, sed+fold reads):

---

> `Bash` -- {"command": "J=\"D:/Vault/Vault-Knowledge/00-System/Breakage-Journal.md\"; for n in 2905 2976; do echo \"=== line $n ===\"; sed -n \"${n}p\" \"$J\" | fold -w 185; done", "description": "Read journal rows 2905 and 2976"}

---

> `Bash` -- {"command": "J=\"D:/Vault/Vault-Knowledge/00-System/Breakage-Journal.md\"; for n in 3061 3289; do echo \"=== line $n ===\"; sed -n \"${n}p\" \"$J\" | fold -w 185; done", "description": "Read journal rows 3061 and 3289"}

---

**Claude:**

Four dated cases of the same defect (19/20/21/24.08) — and row 2976 leaves an explicit unmeasured question. Measuring it tonight:

---

> `Bash` -- {"command": "cat > /e/Obsidian/_imports/content-factory/_scratch/tasks_1002.py <<'PY'\nimport os, re, glob, datetime\nT = r'D:\\Vault\\Vault-Knowledge\\10-Tasks'\nfiles = [p for p in glob.glob(os.path.join(T,'task-*.md'))]\nprint('task cards:', len(files))\ntoday = datetime.date(2026,10,2)\nstate

---

**Claude:**

157 of 256 — but any date counts there, which overclaims. Narrowing to deadline-shaped dates only:

---

> `Bash` -- {"command": "cat > /e/Obsidian/_imports/content-factory/_scratch/tasks2_1002.py <<'PY'\nimport os, re, glob, datetime\nT = r'D:\\Vault\\Vault-Knowledge\\10-Tasks'\ntoday = datetime.date(2026,10,2)\nDATE = re.compile(r'(20\\d\\d)[-./](\\d{2})[-./](\\d{2})')\nKW = re.compile(r'(дедлайн|deadline|под

---

**Claude:**

7 cards, **all 7** parked by the same robot run — that answers the question the journal left open on 20.08. Now checking whether the 30.08 verdict itself was ever executed:

---

> `Bash` -- {"command": "cat > /e/Obsidian/_imports/content-factory/_scratch/tasks3_1002.py <<'PY'\nimport os, re, glob, datetime, collections\nT = r'D:\\Vault\\Vault-Knowledge\\10-Tasks'\n# did anything change state ON or AFTER 2026-08-30 (the verdict run)?\ncnt = collections.Counter(); drop30=[]; sd=0\nfor

---

> `Bash` -- {"command": "cd /e/Obsidian/Vault-Knowledge/10-Tasks && f=$(grep -l '^state: dropped' task-*.md | head -1); echo \"FILE: $f\"; sed -n '1,22p' \"$f\"; echo \"=== how many dropped cards carry ANY date key? ===\"; grep -l '^state: dropped' task-*.md | wc -l; grep -l '^state: dropped' task-*.md | xargs 

---

**Claude:**

Only 2 of 62 dropped cards carry a closing date — and verdicts land as dated frontmatter keys. Checking for the 30.08 verdict key:

---

> `Bash` -- {"command": "cd /e/Obsidian/Vault-Knowledge/10-Tasks && echo \"=== verdict-style keys, by date ===\"; grep -h -o -E '^[a-z_]*verdict[a-z_]*_?2026[0-9]{4}:' task-*.md | sort | uniq -c | sort -rn | head -12; echo \"=== any key containing 0830 / 2026-08-30 ===\"; grep -h -o -E '^[a-z_]+_?20260830[a-z_]

---

**Claude:**

Post B is solid. Now recall for post A — the seed claims three fixes were built; checking whether they exist and are fresh:

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports 2>/dev/null; echo \"=== scripts matching copy/mirror/outbound ===\"; ls -la /e/Obsidian/_imports/*.py 2>/dev/null | grep -i -E 'pub|mirror|outbound|copirk|kopirk|github_ev' | head; echo \"=== FTS over transcripts ===\"; ls -la /e/Obsidian/_imports/*.db /e/Obsidia

---

> `Grep` -- {"pattern": "(session|transcript)[a-z_]*fts|fts5?\\(.*transcript|CREATE VIRTUAL TABLE[^\\n]*(session|transcript)", "path": "D:\\Vault\\_imports", "output_mode": "files_with_matches", "head_limit": 15}

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports && python sessions_fts.py --help 2>&1 | head -20; echo \"=== db files ===\"; ls -la *session*.db claude_sessions/*.db 2>/dev/null | head", "description": "Inspect sessions_fts tool and its db"}

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports && python sessions_fts.py status 2>&1 | head -25", "description": "Get sessions FTS status"}

---

**Claude:**

FTS exists and is big (30,164 files / 174,954 messages). The real question is whether the recall path actually reads it:

---

> `Bash` -- {"command": "ls -la \"C:/Users/dev/.claude/state/sessions_fts.db\" | head -2; echo \"=== who reads sessions_fts? ===\"; cd /e/Obsidian/_imports && grep -l -E 'sessions_fts' *.py 2>/dev/null | head -20; echo \"=== does brain_ask consult it? ===\"; grep -n -i -E 'sessions_fts|session_fts' brain_ask.

---

**Claude:**

The index is fresh (updated today 05:26) but only its own test references it. Checking wider before concluding — empty from one place isn't "no":

---

> `Grep` -- {"pattern": "sessions_fts", "path": "C:\\Users\\dev\\.claude", "output_mode": "files_with_matches", "head_limit": 25}

---

> `Bash` -- {"command": "cat \"C:/Users/dev/.claude/projects/P---WORKDIR-HUB/memory/outbound-mirror-into-vault.md\"", "description": "Read the memory written for this fix"}

---

**Claude:**

Now I have the full promise (A+B+C + two scheduled tasks + a 🌾 harvest due 13.09). Measuring all of it:

---

> `Bash` -- {"command": "echo \"=== external_harvest.py ===\"; ls -la /e/Obsidian/_imports/external_harvest.py 2>&1 | head -2; echo \"=== External-Mirror digests ===\"; ls -la /e/Obsidian/Vault-Knowledge/05-Resources/External-Mirror/ 2>&1 | head -20; echo \"=== scheduled tasks ===\"; powershell -NoProfile -Comm

---

**Claude:**

Everything was built and still runs daily — so A's story is the opposite of B's. Last check: the 🌾 harvest that was due 13.09:

---

> `Bash` -- {"command": "J=\"D:/Vault/Vault-Knowledge/00-System/Breakage-Journal.md\"; echo \"=== journal cases of stale recall after 30.08 ===\"; grep -n -o -E '.{0,55}(нашёл старь|наш[её]л старое|старь[её]|stale recall|устаревш[а-я]+ (CV|резюме)).{0,55}' \"$J\" | tail -8; echo \"=== shadow queue row ===\";

---

**Claude:**

The harvest actually happened on 13.09. Reading its verdict in full:

---

> `Bash` -- {"command": "sed -n '293p' \"D:/Vault/Vault-Knowledge/00-System/Shadow-First-Queue.md\" | fold -w 185", "description": "Read the 13.09 harvest verdict row"}

---

**Claude:**

One more check so the "no caller" claim is defensible across all places:

---

> `Grep` -- {"pattern": "sessions_fts", "path": "D:\\Vault\\Vault-Knowledge", "output_mode": "files_with_matches", "head_limit": 20}

---

> `Grep` -- {"pattern": "sessions_fts\\.py (search|update)", "path": "D:\\Vault", "output_mode": "content", "-n": true, "head_limit": 20}

---

> `Bash` -- {"command": "powershell -NoProfile -Command \"Get-ScheduledTask | Where-Object {\\$_.Actions.Arguments -match 'sessions_fts'} | ForEach-Object { \\$i=\\$_ | Get-ScheduledTaskInfo; '{0} | {1} | last={2} | result={3}' -f \\$_.TaskName, \\$_.State, \\$i.LastRunTime, \\$i.LastTaskResult }\" 2>&1 | head 

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports && grep -n -E 'sessions_fts|fts' external_harvest.py | head -10; echo \"=== what feeds the index then? ===\"; powershell -NoProfile -Command \"\\$t=Get-ScheduledTask -TaskName 'external-harvest-daily'; \\$t.Actions | ForEach-Object { \\$_.Execute + ' ' + \\$_.Arg

---

> `Bash` -- {"command": "cat /e/Obsidian/_imports/external_harvest_daily.cmd 2>&1 | head -20", "description": "Read the daily harvest launcher"}

---

**Claude:**

Both stories verified and their morals are distinct. Checking the gate's own constants before writing:

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/content-factory && python -c \"\nimport slop_gate as sg\nprint('FIRST_PERSON:', sorted(sg.FIRST_PERSON))\nprint('SHORT_SHARE_MIN', sg.SHORT_SHARE_MIN, 'FIRST_PERSON_MIN', sg.FIRST_PERSON_MIN)\nprint('TIER_LEN-ish:', [a for a in dir(sg) if 'LEN' in a or 'MAX' in a

---

**Claude:**

Now the footer blocks (routing the RU link away from the paused channel):

---

> `Bash` -- {"command": "sed -n '1,80p' /e/Obsidian/_imports/content-factory/_STYLE-footer.md 2>/dev/null | head -60", "description": "Read footer style blocks"}

---

> `Bash` -- {"command": "grep -n -A14 -i 'реестр.*жив\\|LIVE_LINKS.*=\\|## .*Реестр' /e/Obsidian/_imports/content-factory/_STYLE-footer.md | sed -n '1,40p'", "description": "Read live links registry"}

---

**Claude:**

Registry line 79 still lists the paused @ClawRus (13th report). Checking how recent mediums handled the footer links:

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/content-factory/drafts && f=$(ls -t *medium-fb-DRAFT.md 2>/dev/null | head -1); echo \"FILE: $f\"; sed -n '1,14p' \"$f\"; echo \"...[FIRST COMMENT]...\"; grep -n -A16 'FIRST COMMENT' \"$f\" | head -24", "description": "Read latest medium draft as template"}

---

**Claude:**

Now composing all six drafts in a `_scratch` generator (Russian prose through the shell is the documented trap):

---

> `Write` -- {"file_path": "D:\\Vault\\_imports\\content-factory\\_scratch\\gen_1002.py", "content": "# -*- coding: utf-8 -*-\n\"\"\"Generator for the content-drain-daily run of 2026-10-02.\nWrites 6 drafts (2 seeds x teaser-ru / teaser-en / medium-fb) with provably\nidentical headers per seed. Re-runnable. A

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/content-factory && python _scratch/gen_1002.py 2>&1 | tail -10", "description": "Generate the six drafts"}

---

**Claude:**

Now the shared verstak on all six — before gating:

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/content-factory && python _scratch/measure_0924.py drafts/2026-10-02-*-DRAFT.md 2>&1 | head -60", "description": "Measure all six drafts with the shared verstak"}

---

**Claude:**

One miss: B's medium at 24.8 first-person (needs ≥30). Fixing in the generator and re-running:

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/content-factory/_scratch && python - <<'PY'\nimport io\np='gen_1002.py'\ns=io.open(p,encoding='utf-8').read()\na=\"звучит как взрослое решение. сегодня я проверил\"\nb=\"звучит как взрослое решение, и я им гордился. сегодня я проверил\"\nassert a in s; s=s.replac

---

**Claude:**

All six measured green. Step 4 — the gate (with the mandatory `--file` flag):

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/content-factory && for f in drafts/2026-10-02-*-DRAFT.md; do echo \"=== $(basename $f)\"; python slop_gate.py --file \"$f\" 2>&1 | grep -E 'ВЕРДИКТ|VERDICT|FAIL|PASS|W[0-9]|F[0-9]|HB[0-9]|AV[0-9]' | head -8; done", "description": "Gate all six drafts"}

---

**Claude:**

Zero FAILs on first pass. Now the publisher check — with the known-good control, per the 27.09 signature fix:

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/content-factory && python - <<'PY'\nimport os, re, glob, io\nimport distributor as D\nprint('CONTROL parse_route(\"facebook\") =', D.parse_route('facebook'))\nfor p in sorted(glob.glob(os.path.join('drafts','2026-10-02-*-DRAFT.md'))):\n    raw = io.open(p, encodi

---

**Claude:**

All six route to live channels. Step 5 — recording the clock (0h window):

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/content-factory && for pair in \"indeks-kormlyu-ne-sprashivayu-teaser-ru teaser @PaloAltoAiRu\" \"indeks-kormlyu-ne-sprashivayu-teaser-en teaser x\" \"indeks-kormlyu-ne-sprashivayu-medium-fb medium facebook\" \"verdikt-ne-tronul-ni-odnoy-kartochki-teaser-ru tease

---

**Claude:**

Six pings recorded at 22:20:34-35 UTC. Step 6 — marking the seeds, and reading the result back from disk:

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/content-factory && wc -l triage/posts.jsonl && python drain_dedup.py --heal 2>&1 | tail -6", "description": "Heal/mark drained seeds"}

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/content-factory && python - <<'PY'\nimport json, io, os\nrows=[json.loads(l) for l in io.open(r'D:\\Vault\\_imports\\content-factory\\triage\\posts.jsonl',encoding='utf-8') if l.strip()]\nprint('rows now:', len(rows))\nfor r in rows:\n    if r.get('id') in ('c

---

**Claude:**

Step 6 proved from disk (both `written`, covered 191→193). Note rows grew 2811→2813, so depth stayed 910 — arrivals masked the drain exactly as expected. Now the chat-03 report:

---

> `Bash` -- {"command": "python \"C:/Users/dev/.claude/scripts/workspace_write_lease.py\" status 2>&1 | head -5", "description": "Check workspace write lease"}

---

> `Bash` -- {"command": "python \"C:/Users/dev/.claude/scripts/workspace_write_lease.py\" status 2>&1 | grep -i -E 'scripts|content-factory|_imports|Obsidian' | head -5; echo \"(exit grep: $?)\"", "description": "Check whether any lease touches scripts or imports"}

---

**Claude:**

Leases touch individual files in `.claude/scripts`, so I'll use the documented wrapper for the report and heartbeat:

---

> `Write` -- {"file_path": "D:\\Vault\\_imports\\content-factory\\_scratch\\report_1002.py", "content": "# -*- coding: utf-8 -*-\n\"\"\"Chat-03 report + cron heartbeat for content-drain-daily 2026-10-02.\nWrapper per the 13.09 lease-fallback recipe: builds the scripts path with\nexpanduser so the command TEXT

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/content-factory && python _scratch/report_1002.py 2>&1 | head -40", "description": "Post chat-03 report and run heartbeat"}

---

**Claude:**

Argparse rejected `--chat` (it's a positional-text CLI) — fixing the invocation:

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/content-factory/_scratch && python - <<'PY'\nimport io\np='report_1002.py'; s=io.open(p,encoding='utf-8').read()\ns=s.replace(\"'--post', MSG, '--chat', '03'],\", \"'--post', MSG],\")\ns=s.replace(\"\"\"    hb = subprocess.run\"\"\",\"\"\"    return\n    hb = sub

---

**Claude:**

`PING OK -> chat_REDACTED`, spool absent before and after, rail_ready True — the three-part delivery proof holds, and the heartbeat stamped on the first run (deliberately not re-stamped). Now judging my own instruction (§9.3-бис) — locating the live prompt file:

---

> `Grep` -- {"pattern": "CONTENT_DRAIN_AUTORUN", "output_mode": "files_with_matches", "path": "C:\\Users\\dev\\.claude", "head_limit": 10}

---

> `Bash` -- {"command": "ls -la /c/Users/dev/.claude/prompts/*drain* /c/Users/dev/.claude/*drain* 2>/dev/null | head; echo \"---cmd launchers---\"; ls -la /c/Users/dev/.claude/scripts/*drain* 2>/dev/null | head", "description": "Find the live drain prompt file"}

---

> `Bash` -- {"command": "grep -n -i -E 'SKILL|\\.md|prompt|type ' /c/Users/dev/.claude/scripts/content_drain_daily.cmd | head -12", "description": "Find which prompt file the launcher feeds"}

---

> `Bash` -- {"command": "P=\"/c/Users/dev/.claude/scheduled-tasks/content-drain-daily/SKILL.md\"; ls -la \"$P\" 2>&1 | head -2; tail -c 400 \"$P\" | fold -w 150", "description": "Confirm live prompt path and tail"}

---

**Claude:**

Found the live prompt (132 KB). Writing tonight's corrections and log entry:

---

> `Write` -- {"file_path": "D:\\Vault\\_imports\\content-factory\\_scratch\\patch_prompt_1002.py", "content": "# -*- coding: utf-8 -*-\n\"\"\"Patch the LIVE content-drain-daily prompt with the 2026-10-02 corrections.\nProse payload goes through a .py (28.09 / 30.09 rule: never a bash heredoc).\nAuthor: Opus 5

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/content-factory && python _scratch/patch_prompt_1002.py 2>&1 | head -12", "description": "Apply prompt corrections and log entry"}

---

> `Bash` -- {"command": "P=\"/c/Users/dev/.claude/scheduled-tasks/content-drain-daily/SKILL.md\"; grep -n 'rail_ready' \"$P\" | head -6; echo \"---\"; grep -n 'Also still required' \"$P\" | head -3; sed -n \"$(grep -n 'Also still required' \"$P\" | head -1 | cut -d: -f1),+2p\" \"$P\" | cat -A | sed -n '1,3p' 

---

**Claude:**

Anchor was mid-line. Fixing and re-running:

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/content-factory/_scratch && python - <<'PY'\nimport io\np='patch_prompt_1002.py'; s=io.open(p,encoding='utf-8').read()\nold = '''A_ANCHOR = \"\"\"  Also still required:\n  rail_ready() == True.\"\"\"'''\nnew = '''A_ANCHOR = \"\"\"\n  rail_ready() == True.\n\"\"\"

---

> `Edit` -- {"replace_all": false, "file_path": "D:\\Vault\\_imports\\content-factory\\_scratch\\patch_prompt_1002.py", "old_string": "A_NEW = A_ANCHOR.rstrip(\"\n\") + \"\"\"\n  NAME THE POST INVOCATION,", "new_string": "A_NEW = A_ANCHOR + \"\"\"  NAME THE POST INVOCATION,"}

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/content-factory && sed -i 's|Same lesson all three times: a CLI this prompt tells you to run must be named WITH its flags.\"\"\"|Same lesson all three times: a CLI this prompt tells you to run must be named WITH its flags.\\\\n\"\"\"|' _scratch/patch_prompt_1002.

---

**Claude:**

Prompt patched (130,069 → 144,231 chars). Now journaling tonight's грабля per §5.10 — checking the class count first:

---

> `Bash` -- {"command": "ls -la /c/Users/dev/.claude/scheduled-tasks/content-drain-daily/SKILL.md | awk '{print \"bytes on disk:\", $5}'; cd /c/Users/dev/.claude/scripts && python prior_art.py class \"рутина вызывает CLI с флагом, которого нет в argparse; промпт не назвал подпись команды; вызов падает или м

---

**Claude:**

The class is already declared systemic with a P0 card (28.08 row). Reading it to reference the right owner:

---

> `Bash` -- {"command": "J=\"D:/Vault/Vault-Knowledge/00-System/Breakage-Journal.md\"; n=$(grep -n 'unparsed-flag-silently-runs-work' \"$J\" | head -1 | cut -d: -f1); echo \"line $n\"; sed -n \"${n}p\" \"$J\" | fold -w 185 | head -22", "description": "Read the 28.08 unparsed-flag class row"}

---

**Claude:**

Class `unparsed-flag-silently-runs-work` is already open at count 19 — so tonight is another dated case, not a new mechanism. Journaling with the four cells (400-char cap each):

---

> `Bash` -- {"command": "cd /c/Users/dev/.claude/scripts && python selfheal.py journal --help 2>&1 | head -25", "description": "Check journal CLI signature"}

---

**Claude:**

`--help` on that CLI doesn't print help either — fitting. Reading its flags from source:

---

> `Bash` -- {"command": "cd /c/Users/dev/.claude/scripts && grep -n -o -E '\\-\\-(class|what|conditions|parts|guess|target|evidence|proof)[a-z-]*' selfheal.py | sort -u | head -15", "description": "List journal flags from source"}

---

> `Write` -- {"file_path": "D:\\Vault\\_imports\\content-factory\\_scratch\\journal_1002.py", "content": "# -*- coding: utf-8 -*-\n\"\"\"Journal tonight's grabla (canon 5.10) with all four cells, each under the\nsilent 400-char cap documented in the prompt on 30.09.\nAuthor: Opus 5 / robot:content-drain-daily

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/content-factory && python _scratch/journal_1002.py 2>&1 | head -20", "description": "Write the journal row"}

---

**Claude:**

The dry-run caught a 411-char cell before writing (the 30.09 rule working). Trimming:

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/content-factory/_scratch && python - <<'PY'\nimport io\np='journal_1002.py'; s=io.open(p,encoding='utf-8').read()\nold = '\"системным, счёт 19, state open - тогда это ещё один датированный случай к чужой P0, и \"\\n    \"механизм строит её владелец. \"'\nnew = '\

---

> `Edit` -- {"replace_all": false, "file_path": "D:\\Vault\\_imports\\content-factory\\_scratch\\journal_1002.py", "old_string": "    \"системным, счёт 19, state open - тогда это ещё один датированный случай к чужой P0, и \"\n    \"механизм строит её владелец. (2) Отдельный дефект: успешная строка ПОЗДНЕГО ш

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/content-factory && python _scratch/journal_1002.py 2>&1 | head -16", "description": "Write the journal row"}

---

**Claude:**

Row written as 20/3 — a 20th case of an already-open P0 class. Verifying it rendered with all four cells rather than assuming:

---

> `Bash` -- {"command": "J=\"D:/Vault/Vault-Knowledge/00-System/Breakage-Journal.md\"; n=$(grep -n 'unrecognized arguments: --chat 03' \"$J\" | head -1 | cut -d: -f1); echo \"row at line $n\"; sed -n \"${n}p\" \"$J\" | awk -F'|' '{for(i=1;i<=NF;i++) printf \"CELL %d (%d chars): %s\\n\", i, length($i), substr

---

> `Bash` -- {"command": "J=\"D:/Vault/Vault-Knowledge/00-System/Breakage-Journal.md\"; sed -n '93p' \"$J\" | awk -F'|' '{print \"CELL4 tail: ...\" substr($4, length($4)-70); print \"CELL7 tail: ...\" substr($7, length($7)-70)}'", "description": "Confirm no mid-sentence truncation"}

---

**Claude:**

Both cells end on complete sentences — no truncation. Posting a short addendum to chat 03 (post and heartbeat as separate steps now, per tonight's own fix):

---

> `Write` -- {"file_path": "D:\\Vault\\_imports\\content-factory\\_scratch\\report2_1002.py", "content": "# -*- coding: utf-8 -*-\n\"\"\"Addendum to the chat-03 drain report: self-maintenance of this routine.\nPost ONLY - the heartbeat was already stamped in a separate step tonight\n(that separation is itself

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/content-factory && python _scratch/report2_1002.py 2>&1 | head -8; echo \"=== spool check ===\"; python -c \"\nimport sys,os; sys.path.insert(0, os.path.join(os.path.expanduser('~'),'.claude','scripts'))\nimport bus_ping; print('SPOOL exists:', os.path.exists(bus

---

**Claude:**

Final verification sweep:

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/content-factory && ls -1 drafts/2026-10-02-*-DRAFT.md | wc -l && python approval_clock.py status 2>&1 | grep -i '2026-10-02' | head -8; echo \"=== heartbeat ===\"; python -c \"\nimport json,io,os\np=os.path.join(os.path.expanduser('~'),'.claude','state','cron_hea

---

**Claude:**

All six releasable on the next tick. The heartbeat lookup came back `None` though — my key guess, not necessarily the stamp. Checking where it actually writes:

---

> `Bash` -- {"command": "cd /c/Users/dev/.claude/scripts && grep -n -E 'open\\(|PATH|STATE|json.dump|write' cron_heartbeat.py | head -12", "description": "Find where the heartbeat is stored"}

---

> `Bash` -- {"command": "cd /c/Users/dev/.claude/scripts && HB=$(grep -n -o 'HB_DIR = .*' cron_heartbeat.py | head -1); echo \"$HB\"; python -c \"\nimport sys,os,io,time; sys.path.insert(0,'.')\nimport cron_heartbeat as c\np=os.path.join(c.HB_DIR,'content-drain-daily.txt')\nprint('file:', p); print('exists:',

---

**Claude:**

Drain complete. All verified from disk, not from success lines.

## Что сделано

**Дренаж 2/2 → 6 черновиков, 0 FAIL с первого прохода** (седьмой чистый проход подряд). Часы записаны 22:20:34–35 UTC, окно 0ч → релизятся следующим тиком распределителя. Оба сида `status=written`, covered 191→193.

**Пост A — `indeks-kormlyu-ne-sprashivayu`** (сид 30.08, 33 дня в воронке). Решение «наружа всегда возвращается внутрь» построено **полностью и живо**: задача отработала сегодня 05:15 с кодом 0, дайджест за октябрь переписан, индекс сессий 30 164 файла / 174 954 сообщения обновлён в 05:26. А читателя нет: строки `sessions_fts` нет ни в `brain_ask.py` (главная дверь recall), ни в одном скилле, ни в одной задаче кроме кормящей. 20 упоминаний в волте — карты и дашборды, инвентарь, не вызов. 13.09 тень закрыли вердиктом «оставляем» по критерию «ноль новых жалоб» — но «никто не пожаловался» и «никто не спросил» звучат одинаково.

**Пост B — `verdikt-ne-tronul-ni-odnoy-kartochki`** (сид 30.08). Вердикт кофаундера по 196 забытым задачам (26 воскресить / 23 рассмотреть / 147 похоронить) за 33 дня **не попал ни в одну карточку**. Для сравнения: ревью, которое оператор провёл сам 17.07, вписалось в 25 карточек ключом с датой. Плюс семья из четырёх датированных случаев журнала, где тот же уборщик судил уверенно и ошибался (19/20/21/24.08).

**Закрыт вопрос, лежавший 43 дня.** Строка журнала от 20.08 кончалась честным «не проверял, сколько ещё задач припарковано с датами внутри тела». Померил: **7** карточек, и все 7 — из одного прогона 19.08, пять до сих пор не закрыты. Широкая мерка давала 157, но это завышение (прошедшая дата часто = дата рождения карточки) — в пост взято узкое число, широкое названо в evidence.

## Грабля этой ночи

Доклад в 03 почти не ушёл: вызвал `bus_ping.py --post MSG --chat 03`, а опции `--chat` не существует. Дорого не это — обёртка гнала доклад и heartbeat одним процессом, поэтому последней строкой встал зелёный `heartbeat stamped` **сразу после смерти доклада**. Починено, доклад ушёл (`PING OK`). Журнал: строка 20/3 класса `unparsed-flag-silently-runs-work` — класс уже системный и открытый, механизм не строю и порог не разрешаю, оба чтения вписал в строку (§5.4: удобное мне чтение требует владельца класса, не меня).

**Промпт рутины обновлён** (130 069 → 144 231 знака): точная подпись команды доклада + правило разделять шаги; новый `1-octies` (четвёртый вопрос к сиду — обвиняет ли пост названного постороннего); в шаг 2 — правило про журнальную строку с «не проверял» и завышающую первую регулярку.

**Названо, не починено:** реестр `_STYLE-footer.md` строка 79 всё ещё числит живым @ClawRus (пауза с 06.08) — **тринадцатый** доклад; ссылку в обоих medium переставил на живой @PaloAltoAiRu, футер не трогал (зона Норы). Долг прежних прогонов без изменений (34 черновика без funnel_ids, 5 с id вне воронки, два FAIL-файла от 05.08). Промпт растёт ~11 КБ/ночь — самый дорогой пункт обслуживания, но один файл = один писатель.

**Вердикт по скиллам:** ни одного не использовал (всё инструменты, не скиллы) — ✅ не надо. **По своей инструкции:** 🔧 обновил, три блока, все из пережитой боли.

🎙 **Майк:** идём верно, но обе ночные находки — один и тот же дефект с двух сторон: мы строим приборы и не строим им потребителя. Индекс на 174 тысячи сообщений без вызывающего и вердикт на 196 задач без записи в карточку — это не две поломки, это одна привычка. Вопрос: разрешишь завести «читателя» для индекса сессий одной строкой в дверь recall, или это пока твой вызов?

🧒 **Простыми словами:** я каждую ночь складываю все наши разговоры в большой шкаф с ярлычками — 174 тысячи листочков. Сегодня я заметил, что ни разу в этот шкаф не заглянул, и никто другой тоже: все знают, что он есть, а ключ спрашивать не у кого. Второе: месяц назад я сказал про 196 заброшенных дел «26 оживить, 147 закопать» — и ни на одной бумажке это не написал. Получилось, что я не решил, а просто красиво сказал. Про оба случая написал посты, они готовы к публикации.
