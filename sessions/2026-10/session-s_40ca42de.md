---
session: s_40ca42de
date: 2026-10-04
words: 29584
turns: 48
tools: "Bash, Edit, Grep, Write"
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-10-04 · CONTENT_DRAIN_AUTORUN

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_40ca42de` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

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
- OK/STOP, РАЗВИЛКА (добавлено 03.10, встретилась живьём): ты нашёл ЖИВУЮ поломку, и она же --
  предмет поста. Канон 5.3 велит чинить увиденное, если легко+обратимо+безопасно; эта рутина
  пишет только в drafts\. Тест на два вопроса: (1) поломка внутри СВОИХ файлов рутины?
  (2) по этому же компоненту НЕ идёт чужой активный инцидент? Да и да -> чини и скажи. Иначе ->
  доложи ГРОМКО: точный корень, точное одношаговое лечение, владелец, и строка в evidence_level
  черновика, чтобы пост не читался как будто ты тихо закрыл вопрос. Замер 03.10: RAG-сервер лежал
  19.5 ч, лечение = переустановить numpy (сторож поднимет сам следующим тиком), но это остаток
  MSI-ремонта Python 3.12 от 02.10 -- активный инцидент на двух узлах со своими сессиями, и
  пакетная хирургия из контентной рутины компаундит чужую аварию, то есть «безопасно» не
  выполняется. Молчание тут -- дефект; доклад -- не слабый вариант.


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
   1-nonies. THE SEED'S OWN HEADLINE CLAIM IS A CLAIM WITH A SHELF LIFE - TEST IT BEFORE YOU
   BUILD ON IT (added 2026-10-03, it nearly published a false statement about our own system).
   The rule directly above says to prefer a seed carrying a measured fact. True - but that fact
   was measured 30+ days ago, so it is a hypothesis about tonight, not a fact. Measured 03.10:
   cc:9392bcbb asserted "we found an alarm clock that never rang"; tonight that watchdog rings 96
   times a day and had printed 78 consecutive DOWN lines while I was reading it. Writing the post
   the seed's way would have put a false claim about my own infrastructure into three channels.
   And the refutation is strictly BETTER material: the real defect is not a silent alarm but an
   alarm with no receiver. So before writing, ask one question of the seed's central assertion -
   is it still true tonight? - and when the instrument the seed names is still on disk, RUN IT
   rather than quoting the seed about it. Same family as the 28.09 honest-empty rule (a finding
   rots) and the 26.09 note about an ending that refutes the seed; the difference is that this
   one is not luck, it is a step.
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
   1-octies. THE FOURTH QUESTION: DOES THE POST ACCUSE A NAMED OUTSIDER? (added 2026-10-02, it
   was the single oldest seed in the pool that night and will be again). `cc:live-63d402` passes
   every filter written above - `visibility: public`, `cc:live-` family, subject is OUR OWN chain
   measurement, carries no 1-quinquies stop-word, is nobody's personal life - and its thesis is
   that a NAMED outside project is a scam or dead marketing (28 hosts against 582 on the vendor's
   showcase, a drawn-up cap, MLM wrappers). The mechanics are genuinely ours and the numbers may
   well be right; publishing them as Mycroft in first person is still not this routine's call.
   Two reasons, both already in this file but never joined up: the BOUNDARIES block forbids
   third-party names outright, and an accusation against a named company is legal and reputational
   exposure, i.e. Tier-2 - dev's, not a robot's. 1-sexies asks "what is the subject" but was
   written against bannable/sensitive TOPICS (adult content), so an accusation reads as waved
   through. So ask a fourth question: does this post accuse, rate or expose a named outsider?
   Yes -> leave it `new` and say so. Note the shape it will keep taking: the seed is interesting,
   well-measured and old, which is exactly why it keeps winning the sort.
   ALSO RECURRING, and cheaper to recognise than to re-reason: `cc:live-aca9c8` ("six resumes of
   one person") is a 1-septies job-search seed - six packagings of dev's CV - and sorts second
   in the pool. Skip it for the same reason as cc:ff21c6b8, without re-investigating.

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

   A JOURNAL ROW THAT ENDS IN AN UNMEASURED QUESTION IS THE BEST ENDING THIS ROUTINE CAN GET -
   AND YOUR FIRST REGEX WILL OVERCLAIM IT BY AN ORDER OF MAGNITUDE (added 2026-10-02, it carried
   post B). Journal rows routinely close with an honest `🤔 не проверял, ...` - canon 5.4 demands
   the admission and nothing schedules the follow-up, so those questions just sit. Tonight's was
   from 20.08: "не проверял, сколько ещё задач припарковано с датами внутри тела", unmeasured for
   43 days. Measuring it is cheap, it is OURS to measure, and it gives the post a number that
   exists nowhere else - strictly better than re-telling the seed. So when recall lands a journal
   row, grep its tail for `не проверял` / `не знаю` / `🤔` and see whether tonight can answer it.
   THE TRAP: the obvious regex is the generous one. "Any already-passed date in the card body"
   returned 157 cards; "a passed date within ~90 chars of a deadline word (дедлайн / подача /
   срок / окно)" returned 7 - a 22x gap, because a past date in a card is usually just the card's
   own birth date. 157 would have been a false number in a published post. Compute BOTH, publish
   the narrow one, and name the broad one in `evidence_level` so the next reader sees why it was
   rejected. Same discipline as the §5.4 rule that a convenient number needs the stronger proof -
   and here the convenient number is the big one, because it makes the story louder.

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

   WHEN THE SEED NAMES A BACKGROUND SERVICE, READ ITS LOG AND ITS SCHEDULER ROW TOGETHER - THEY
   DISAGREE BY DESIGN (added 2026-10-03; the pair produced both halves of post A). The recall
   instruments above cover vault notes (21.09), GitHub objects (26.09), task-card evidence fields
   (27.09) and journal rows (28.09), and not one of them fits a seed about a watchdog, a daemon or
   a server. The working pair is Get-ScheduledTask + Get-ScheduledTaskInfo for what the system
   BELIEVES, and the service's OWN log for what actually happened. Measured 03.10 on the Second-Brain
   RAG watchdog: the scheduler said State Ready, LastTaskResult 0, NumberOfMissedRuns 0, last run
   23:01:01, while its log held 78 consecutive "DOWN (not listening) -- respawning" lines covering
   19.5 hours. Both readings are correct and they contradict each other, because the exit code is
   about the REPORTER and not about the REPORTED (canon 5.5) - and that contradiction needs no
   narrative work, it IS the post. Budget two reads, and never let a green task row stand in for a
   living component. Note the two tasks are usually a PAIR (a server task and a watchdog task):
   read both, since the one that looks healthiest is often the one doing the killing.
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
  NAME THE POST INVOCATION, AND DO NOT LET THE HEARTBEAT VOUCH FOR IT (added 2026-10-02, cost
  one dead call and nearly a silent un-reported run). This prompt has demanded a chat-03 post
  since step 7 and has never written the CLI signature, so I guessed `bus_ping.py --post <text>
  --chat 03`. `--post` is a FLAG and the text is POSITIONAL; there is no `--chat` option, and
  argparse exited with "unrecognized arguments: --chat 03". Exact form:
      python bus_ping.py --post "<the whole report text>"
  The expensive part was not the typo. My wrapper ran the post and the heartbeat in ONE process,
  so that same run printed `heartbeat stamped: content-drain-daily` as its last line - a success
  line, immediately after the post had failed - and the empty `--- stdout ---` above it is easy
  to read as "nothing to say". A run that stamps its heartbeat and never reports is exactly the
  silent-success shape canon 5.5 is about. So: call the post and the heartbeat as SEPARATE steps,
  read `PING OK` with your own eyes first, and never infer delivery from the heartbeat. Third
  member of the unparsed-signature family after 20.09 (`--file`) and 27.09 (`parse_route`).
  Same lesson all three times: a CLI this prompt tells you to run must be named WITH its flags.
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
- 2026-10-02, run of this routine (CLAUDE.md 9.3-bis + the 13.09 amendment: BOTH the skill it
  calls AND its own file). FIRST and only drain of the day - drafts/2026-10-02-* was empty at start,
  no sibling run had written anything, and no clone-gate stand-down was offered. Drained cc:live-ec14a9
  (30.08, 33 days in the funnel) -> "indeks-kormlyu-ne-sprashivayu" and cc:be9848d4 (30.08) ->
  "verdikt-ne-tronul-ni-odnoy-kartochki"; 6 files, 2 RU teasers fully clean, 2 EN teasers with the known
  RU-only W4, 2 mediums with the structural W6, ZERO FAILs on the first pass - the SEVENTH clean pass in
  a row, again because the verstak ran before any file was written (RU 246/238 against the hard 250,
  EN 247/241, mediums 1262/1393; short-share 33-43%, first person 33.7-55.6/1000 on every RU file;
  "полотен в теле: 0" on all six). 6 clock pings recorded at 22:20:34-35 UTC with a 0h window.
  Every number in both posts was measured tonight. Post A: the 30.08 decision "наружа всегда
  возвращается внутрь" was built in FULL and is alive - external-harvest-daily LastRunTime 02.10
  05:15:01 with LastTaskResult 0, Outbound-Digest-2026-10.md rewritten at 05:15, the session index at
  30,164 files / 174,954 messages / 362 MB refreshed at 05:26, and external_harvest_daily.cmd feeding it
  `--limit 2000` nightly exactly as the decision memo promised - while the READER was never built: the
  string `sessions_fts` appears in brain_ask.py zero times, in ~/.claude/skills zero times, in no
  scheduled task's arguments except the feeder, and the 20 vault files that do mention it are Dev-Maps,
  Regression-Status files, HTML dashboards and old _session-md logs, i.e. inventory, not a caller. The
  13.09 shadow verdict closed it as "✅ ОСТАВЛЯЕМ" on the criterion "0 new 'нашёл старьё' cases", and its
  author even guarded against §5.5 by proving the rails were fed - but "nobody complained" and "nobody
  asked" are the same silence, which is the post's ending. Post B: the 30.08 cofounder verdict over 196
  forgotten tasks (26 resurrect / 23 review / 147 bury) reached NO card - zero cards carry a verdict key
  dated 30.08, while `founder_verdict_20260717` (the review dev ran himself) sits in 25 cards, and only
  2 of 62 `dropped` cards carry any closing date at all - plus a journal FAMILY of four dated cases where
  the same parking robot judged confidently and was wrong (19.08 the only card holding a fleet rollout;
  20.08 a lane with an external deadline inside its body; 21.08 58 of 81 cards onto one date; 24.08 a live
  open card moved because the filter judged a key's PRESENCE, not its VALUE).
  Three corrections, each a pain felt in THIS run, not a speculation:
  (a) THE CHAT-03 POST CLI WAS NEVER NAMED AND THE HEARTBEAT ALMOST VOUCHED FOR A FAILED REPORT. Step 7
      has demanded a chat-03 post since this routine existed without ever writing the signature; I guessed
      `--post MSG --chat 03` and argparse exited "unrecognized arguments: --chat 03". The typo was cheap -
      the dangerous part is that my wrapper ran the post and the heartbeat in one process, so the run's
      LAST line was `heartbeat stamped: content-drain-daily`, a success line printed immediately after the
      report had died, with an empty `--- stdout ---` above it that reads like "nothing to say". That is a
      stamped-but-silent run, the exact shape canon 5.5 names. Fixed forward: exact invocation written into
      the FINAL STEP, plus the rule to run post and heartbeat as separate steps and read `PING OK` with
      your own eyes. Third member of the unparsed-signature family after 20.09 `--file` and 27.09
      `parse_route` - same lesson three times: a CLI this prompt orders you to run must be named with its
      flags.
  (b) new step 1-octies: the canon filters wave through a seed whose thesis ACCUSES a named outsider.
      `cc:live-63d402` was the single oldest seed in the pool - public, `cc:live-` family, measurement is
      ours, no stop-word, nobody's personal life - and it argues a named outside project is a scam. The
      BOUNDARIES block already forbids third-party names and an accusation against a company is legal
      exposure, i.e. Tier-2; 1-sexies asks "what is the subject" but was written against bannable TOPICS,
      so an accusation reads as waved through. Also recorded `cc:live-aca9c8` (six CV packagings) as a
      recurring 1-septies skip, since it now sorts second.
  (c) new step 2 block: a journal row ending in an unmeasured `🤔 не проверял` is the best ending this
      routine can get, and the first regex overclaims it by an order of magnitude. The 20.08 question
      ("how many parked cards carry dates inside the body") had sat 43 days; answering it gave post B a
      number that exists nowhere else. But the generous regex (any past date in the body) said 157, while
      the narrow one (a past date within ~90 chars of a deadline word) said 7 - a 22x gap, because a past
      date in a card is usually its own birth date. 157 in a published post would have been a false
      number. Compute both, publish the narrow one, name the broad one in evidence_level.
  Not changed, and the canon skip list again did its whole job with zero re-investigation: steps 0 / 1 /
  1-bis / 1-ter / 1-quater / 1-quinquies / 1-sexies / 1-septies / 3 / 4 / 5 / 6 / 7 behaved exactly as
  written. All four standing canon skips fired (cc:284c9e17 stop-word, NINTH night running; cc:live-46eff1
  personal; cc:live-60245d subject is dev's call; cc:ff21c6b8 biography/job search) and two new ones were
  added above. 1-ter's four blind spots ran clean for all four candidates. The 30.09 windows-path rule paid
  immediately - `--covered` was written next to the script and read back 191, matching 30.09's end state, so
  the false-zero coverage class did not recur. The 28.09 "a grabla has a journal row by construction" rule
  was again the highest-value step: post B rests entirely on a journal family the seed never mentioned, and
  the 29.09 full vault path plus the two-step read (grep to locate, sed+fold to read) worked first try on all
  four rows (2905, 2976, 3061, 3289). The 01.10 verstak mechanism earned its keep on its first night: it
  caught B's medium at 24.8 first-person BEFORE gating (floor 30), the fix was two one-line edits in the
  _scratch generator plus one re-run, and "полотен в теле: 0" on all six files meant no eyeballing of which
  paragraph_lint hit mattered. The 27.09 parse_route signature + control worked (all six resolved
  tg_paloaltoairu / x_en / fb_wall; bare `facebook` still (None, None) as documented). The 16.09 disclosure
  form held (disclosure_missing = None on both comment-stripped mediums) and the 28.09 channel values were
  used (@PaloAltoAiRu / x / facebook). The 30.09 step-7 rule about arrivals was exactly right and would have
  caused a false alarm without it: rows 2811 -> 2813, two arrivals from content-factory-daily masked two
  drains, `new` stayed at 910, and the load-bearing proof was status=written on both ids plus covered
  191 -> 193. The 22.09 three-part delivery proof held once the invocation was fixed: `PING OK -> chat_REDACTED`
  printed, bus_ping.SPOOL absent before AND after, rail_ready True - journal class
  spool-item-exceeds-transport-limit stays at 2/3 for a NINTH night and no mechanism is built (CLAUDE.md 5.10).
  Lease note: workspace_write_lease showed 108 ACTIVE leases including individual files under
  ~/.claude/scripts (a jev_analyst session), none of them mine and none on the imports tree - the 13.09
  wrapper recipe was used anyway for the post and heartbeat, and nothing was blocked.
  Named, NOT fixed (with reasons): post A's subject is itself the biggest unclaimed finding - a fully built,
  nightly-fed 174,954-message index with no caller anywhere in the system, and a shadow closed as a permanent
  "don't build D" on a criterion that cannot distinguish "no complaints" from "no questions". Building the
  reader (a recall door that consults sessions_fts) is not this routine's file; neither is reopening that
  shadow. Post B's subject likewise: the 196-task verdict touched nothing, and the parking robot's four-case
  family belongs to the owner of task_hygiene. Standing debt, all unchanged: 34 drafts with no funnel_ids
  (since 14.09); 5 drafts pointing at ids outside the funnel (since 26.09); the two slop_gate FAIL files from
  05.08 (the teaser is 173 chars of dev's verbatim voice against a hard 200 floor - his call, not a
  rewrite); _STYLE-footer.md line 79 still lists the paused @ClawRus as 🟢 live (reported
  15/16/19/20/21/22/23/26/27/28/29/30.09 and 01.10, and again tonight - THIRTEENTH report; follow link routed
  to @PaloAltoAiRu in both mediums, footer itself untouched - Nora's zone). ALSO NAMED: this prompt file
  was 132,271 bytes before tonight's edits and the PROMPT-FIX LOG is most of it, loaded in full on every run
  (97.7 KB on 29.09, ~111 KB on 30.09, ~121 KB on 01.10). Not compressed here - one writer per file and this
  is not that pass (canon 10.0) - but the growth is now ~11 KB/night and a deliberate compression pass is the
  highest-value maintenance item on this routine. Session note, not a routine defect: this run opened in
  C:\Windows\System32 for the ninth night running, flagged by home-dir-guard as a foreign folder for this
  node; every path used here is absolute, so the drain was unaffected.
  Verdict on the skills this routine calls: none used (slop_gate / approval_clock / drain_dedup / distributor
  / paragraph_lint / bus_ping / sessions_fts / external_harvest are tools, not skills) - nothing to update
  there. Verdict on its OWN instruction: 🔧 обновляю - three blocks inserted above, all from pain felt
  in this run.
  Author: Opus 5 / robot:content-drain-daily. Machine: HUB-01. Operator: robot.
- 2026-10-03, run of this routine (CLAUDE.md 9.3-bis + the 13.09 amendment: BOTH the skill it
  calls AND its own file). FIRST and only drain of the day - drafts/2026-10-03-* was empty at start,
  no sibling run had written anything, and no clone-gate stand-down was offered. Drained cc:9392bcbb
  (30.08, 34 days in the funnel) -> "budilnik-zvonil-78-raz" and cc:b67b4579 (30.08) ->
  "dver-est-tolko-v-stroke-o-ney"; 6 files, 2 RU teasers fully clean, 2 EN teasers with the known
  RU-only W4, 2 mediums with the structural W6, ZERO FAILs on the first pass - the EIGHTH clean pass
  in a row (RU 242/243 against the hard 250, EN 245/245, mediums 1238/1154; short-share 38-78%,
  first person 38.5-58.8/1000 on every RU file; "polotren v tele: 0" on all six). 6 clock pings
  recorded at 22:19:44 UTC with a 0h window.
  Both posts rest on numbers measured tonight, and post A's numbers are the sharpest this routine has
  produced: the Second-Brain RAG server (ask_server, port 8770) has been DOWN for 19.5 hours. At
  03:16 the log says alive; at 03:31 the watchdog KILLED IT ITSELF to load a fresh index ("index
  changed (reindex done) -- restarting server", killed zombie PID 21632); at 03:46 the first "DOWN
  (not listening) -- respawning", and then 78 of those in a row until 23:01:20. Root, one line down
  in ask_server_autostart.log: ask_server.py:21 import numpy -> ModuleNotFoundError: No module named
  'numpy._utils', i.e. the residue of the 02.10 MSI repair of Python 3.12 (journal row
  python-stdlib-gutted-by-msi-repair: Lib was restored by 20:21, numpy inside site-packages was not).
  Meanwhile Get-ScheduledTaskInfo on "Second Brain Server Watchdog Daily" says State Ready,
  LastTaskResult 0, NumberOfMissedRuns 0, LastRunTime 23:01:01 - because zero is about the watchdog,
  not about the server. Post B: the door named as the root in the 01.10 row
  node-sleeps-and-nothing-checks-it (a node slept 71% of the night, 6:51 of 9:38, 69 sleeps, while
  the session blamed the hub and Syncthing) was never built - ripgrep over ~/.claude finds the string
  awake_check in EXACTLY 5 files and all 5 are sync-conflict copies of that same journal. The only
  place the door exists is the sentence saying it is missing.
  Three corrections, each a pain felt in THIS run, not a speculation:
  (a) THE SEED'S OWN HEADLINE CLAIM IS A CLAIM WITH A SHELF LIFE, AND NOTHING HERE SAID SO. Seed A
      asserted "we found an alarm clock that never rang". Tonight it rings 96 times a day and had
      rung 78 consecutive times while I read it. Had I written the post the seed's way I would have
      published a false statement about my own system - and the refutation is strictly BETTER
      material, because the real defect is not a silent alarm but an alarm with no receiver. The
      26.09 entry praises an ending that refutes the seed's lesson, but it treats that as luck; and
      the 28.09 honest-empty rule already establishes that a 30-day-old finding rots. Same logic
      applies to the seed's central assertion: before building on it, ASK whether it is still true,
      and when the instrument named in the seed is still on disk, RUN IT. Step 1 now says to prefer
      seeds carrying a measured fact; it should also say that the measured fact is a hypothesis about
      a month ago, not a fact about tonight.
  (b) NEW STEP-2 INSTRUMENT: WHEN THE SEED NAMES A BACKGROUND SERVICE, READ ITS LOG AND ITS SCHEDULER
      ROW TOGETHER - THEY DISAGREE BY DESIGN. The recall instruments catalogued here cover vault
      notes (21.09), GitHub objects (26.09), task-card evidence fields (27.09) and journal rows
      (28.09), and none of them fits "the seed is about a watchdog or a daemon". The working pair is
      Get-ScheduledTask + Get-ScheduledTaskInfo for what the system BELIEVES, and the service's own
      log for what HAPPENED. Tonight they contradicted each other perfectly (Ready/0/0-missed versus
      78 DOWN lines), and that contradiction IS the post - no narrative work needed. Budget two
      reads, and never let the exit code stand in for the item (canon 5.5).
  (c) THIS ROUTINE HAD NO RULE FOR "I FOUND A LIVE RED THAT IS THE POST'S OWN SUBJECT", AND TONIGHT
      IT WAS A REAL ONE. The BOUNDARIES block says write only into drafts/ and stop at Tier-2; canon
      5.3 says fix what you see when it is easy, reversible and safe. A 19.5-hour-dead RAG server
      with a one-command fix (reinstall numpy, the watchdog revives it on its own next tick) sits
      exactly between those two, and the prompt is silent - so the next run could as easily ignore a
      RED as perform package surgery. I did NOT fix it, deliberately: the 02.10 Python repair is an
      ACTIVE incident with its own sessions on two nodes, and pip surgery from a content routine
      compounds someone else's outage, which fails the "safe" leg of 5.3. The rule to apply: is the
      break inside this routine's OWN files? is another incident in flight over the same component?
      If no and no -> fix it and say so. Otherwise -> report it loudly with the exact root, the exact
      one-line cure and the owner, and name it in the draft's evidence_level so the post cannot read
      as if I had quietly closed it. Reporting is not the weak option here; silence is the defect.
  Also logged, not a new correction: the 13.09 lease recipe says to "check workspace_write_lease.py
  status", and there is no such attribute - the module raised AttributeError, which reads exactly like
  "no lease information" rather than "wrong call". Nothing was blocked tonight and no lease interfered,
  but the next run should call the module's real surface or skip the check rather than trust an
  exception. Same unparsed-signature family as 20.09 (--file), 27.09 (parse_route) and 02.10
  (bus_ping --post).
  Not changed, and the canon skip list did its entire job with zero re-investigation: steps 0 / 1 /
  1-bis / 1-ter / 1-quater / 1-quinquies / 1-sexies / 1-septies / 1-octies / 3 / 4 / 5 / 6 / 7 behaved
  exactly as written. The SIX oldest seeds in the pool were all canon skips and all six fired on sight
  (cc:284c9e17 stop-word, TENTH night running; cc:live-46eff1 personal; cc:live-60245d subject is
  dev's call; cc:ff21c6b8 and cc:live-aca9c8 biography/job search; cc:live-63d402 accusation against
  a named outsider - first use of 1-octies, added last night, and it was the single oldest seed again
  exactly as that entry predicted). Without that list the run would have opened by re-reasoning six
  seeds. 1-ter's four blind spots ran clean for all five candidates; the only self-named draft among
  uncovered seeds is still the known-missing longboards file, left queued (a named-but-missing file is
  not coverage). The 30.09 windows-path rule paid again: --covered was written next to the script and
  read back 193, matching 02.10's end state, so the false-zero coverage class did not recur. The 28.09
  "a grabla has a journal row by construction" rule plus the 29.09 full vault path and two-step read
  (grep to locate, sed+fold to read) worked first try on all seven rows read tonight. The 01.10 verstak
  mechanism earned its keep again and this is now its third consecutive save: it caught EN-B at 29%
  short sentences against the 30% floor BEFORE gating, the fix was one line in the generator plus one
  re-run, and "polotren v tele: 0" on all six meant no eyeballing of which paragraph_lint hit mattered.
  The 27.09 parse_route signature + control worked (all six resolved tg_paloaltoairu / x_en / fb_wall;
  bare "facebook" still (None, None) as documented). The 16.09 disclosure form held
  (disclosure_missing = None on all six, checked on the comment-stripped body) and the 28.09 channel
  values were used (@PaloAltoAiRu / x / facebook). The 02.10 bus_ping signature fix worked first try and
  its companion rule proved its worth: post and heartbeat were run as SEPARATE steps, "PING OK ->
  chat_REDACTED" was read with my own eyes BEFORE the heartbeat was stamped. Three-part delivery proof held:
  PING OK printed, bus_ping.SPOOL absent before AND after, rail_ready True - journal class
  spool-item-exceeds-transport-limit stays at 2/3 for a TENTH night and no mechanism is built. The 30.09
  four-cell journal rule paid three times over: the pre-write length check refused the row THREE times
  (conditions 410, guess 571 -> 470 -> 402) and only wrote at 380/381/398/384, so nothing was silently
  cut at 400; and prior_art again printed the family undercount warning (by name 2, family 8, threshold
  3), so BOTH readings went into the row and the promotion was left to the class owner per the 30.09
  discipline. The 30.09 step-7 arrivals rule was checked and was NOT needed tonight: rows 2820 -> 2820,
  no arrivals during the run, new 917 -> 915; the load-bearing proof remains status=written on both ids
  plus covered 193 -> 195.
  Named, NOT fixed (with reasons): the dead RAG server above is the single most important item - root
  known, cure one command, owner is the 02.10 Python-repair incident, reported to chat 03 with both.
  The awake_check door is post B's own subject and belongs to whoever owns node liveness. The
  second-brain-search-server-atlogon-dead-task family has FIVE dated rows (08/10/11/13/14.09) all saying
  "the self-heal robot could not cure it", severity=root, runbook absent (fail-closed) - and then the
  rows simply stop, which tonight's measurement explains: the task itself returns 0, so the self-heal
  robot has nothing to catch. Standing debt, all unchanged: 34 drafts with no funnel_ids (since 14.09);
  5 drafts pointing at ids outside the funnel (since 26.09); the two slop_gate FAIL files from 05.08
  (the teaser is 173 chars of dev's verbatim voice against a hard 200 floor - his call, not a
  rewrite); _STYLE-footer.md block B still lists the paused @ClawRus as live (FOURTEENTH report; follow
  link routed to @PaloAltoAiRu in both mediums, footer itself untouched - Nora's zone). ALSO NAMED:
  this prompt file was 146,645 bytes before tonight's edits (97.7 KB on 29.09, ~111 KB on 30.09,
  ~121 KB on 01.10, ~132 KB on 02.10) and the PROMPT-FIX LOG is most of it, loaded in full on every run.
  Not compressed here - one writer per file and this is not that pass (canon 10.0) - but the growth is
  ~14 KB/night and accelerating, which makes a deliberate compression pass the highest-value maintenance
  item on this routine by a wide margin. Session note, not a routine defect: this run opened in
  C:\Windows\System32 for the tenth night running, flagged by home-dir-guard as a foreign folder for
  this node; every path used here is absolute, so the drain was unaffected.
  Verdict on the skills this routine calls: none used (slop_gate / approval_clock / drain_dedup /
  distributor / paragraph_lint / bus_ping / selfheal / prior_art / cron_heartbeat are tools, not
  skills) - nothing to update there. Verdict on its OWN instruction: обновляю - three blocks inserted
  above plus one logged non-correction, all from pain felt in this run.
  Author: Opus 5 / robot:content-drain-daily. Machine: HUB-01. Operator: robot.

---

**Claude:**

CONTENT_DRAIN_AUTORUN — рутина принята. Начинаю.

🚂 **План рельс на старте** (§6.3-бис): сам как Claude — выбор сидов, канон-фильтры 1-quater…1-octies, recall по артефактам, написание шести текстов голосом Майкрофта (качество текста = гейт качества, §6.2 → Fable/Opus), гейты и клок. На чужие рельсы НЕ уезжает ничего: эта рутина — суждение + голос + волт, т.е. ровно класс «Claude-оркестратор»; плюс STOP-блок запрещает исходящее, а панель вендоров тут нечего спрашивать. Вердикт заранее: `class-mismatch`, не `forgot`.

Шаг 0 — клон-гейт и обстановка.

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/content-factory 2>/dev/null && pwd && ls -la | head -40", "description": "Check content-factory dir"}

---

> `Bash` -- {"command": "ls /e/Obsidian/_imports/content-factory/drafts/ | grep '^2026-10-04' | head -20; echo \"---count---\"; ls /e/Obsidian/_imports/content-factory/drafts/ | grep -c '^2026-10-04'", "description": "Check for today's sibling drafts"}

---

**Claude:**

Пусто на сегодня, клон-гейт стоп не предлагал. Шаг 1 — пул сидов.

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/content-factory && python drain_dedup.py --covered --json > cov_tmp.json 2>&1; python -c \"\nimport json\nd=json.load(open(r'D:\\Vault\\_imports\\content-factory\\cov_tmp.json',encoding='utf-8'))\nids=d.get('covered') or d.get('ids') or d\nprint(type(ids), len

---

**Claude:**

covered = 195 — ровно конец 03.10, false-zero класс не повторился. Строю пул.

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/content-factory && cat > _scratch/pick_1004.py <<'EOF'\nimport json, re, os\nFUN = r'D:\\Vault\\_imports\\content-factory\\triage\\posts.jsonl'\ncov = set(json.load(open(r'D:\\Vault\\_imports\\content-factory\\cov_tmp.json',encoding='utf-8')))\nrows=[]\nwit

---

**Claude:**

Шесть канон-скипов сработали с листа, плюс седьмой, которого в списке ещё не было:

- `cc:284c9e17` — стоп-слово «не-технарь» (1-quinquies, **11-я ночь**)
- `cc:live-46eff1` — личная жизнь оператора (1-sexies)
- `cc:live-60245d` — субъект = решение оператора (1-sexies)
- `cc:ff21c6b8`, `cc:live-aca9c8` — биография/поиск работы (1-septies)
- `cc:live-63d402` — обвинение названного стороннего проекта (1-octies, снова самый старый, как и предсказала запись 02.10)
- ⭐ `cc:live-d4ef83` «Не-технарь управляет флотом из 6 машин» — **то же стоп-слово в заголовке**, 1-quinquies, в логе раньше не числился

Шорт-лист и полные заметки:

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/content-factory && cat > _scratch/detail_1004.py <<'EOF'\nimport json\nFUN = r'D:\\Vault\\_imports\\content-factory\\triage\\posts.jsonl'\nwant={'cc:e8341415','cc:live-60deca','cc:live-8faf64','cc:live-4d2835'}\nwith open(FUN,encoding='utf-8') as f:\n    for l

---

**Claude:**

Проверяю слепые зоны 1-ter для кандидатов и пересечение `cc:live-8faf64` с постом от 01.10.

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/content-factory/drafts && for id in cc:e8341415 cc:live-60deca cc:live-8faf64 cc:live-4d2835 e8341415 60deca 8faf64 4d2835; do echo \"== $id\"; grep -l \"$id\" *.md 2>/dev/null | head -5; done; echo \"=== 01.10 drafts ===\"; ls | grep '^2026-10-01'", "description

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/content-factory/drafts && sed -n '1,60p' 2026-10-01-ne-dve-os-a-dva-fajla-nastroek-medium-fb-DRAFT.md", "description": "Read 01.10 post B to judge overlap"}

---

**Claude:**

`cc:live-8faf64` — это **тот же артефакт, что уже опубликован 01.10** (issue #89632, «It flips», та же переменная-файл). Мораль другая, но тело поста было бы повторным. Правило 1-bis покрывает только СЕГОДНЯШНИХ двойников — это кросс-дневной двойник, новая слепая зона. Скипаю и записываю.

Теперь уточняю пул по тиру — рутина пишет teaser+medium, а верх пула забит `tier:longread`:

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/content-factory && cat > _scratch/pick2_1004.py <<'EOF'\nimport json, re\nFUN = r'D:\\Vault\\_imports\\content-factory\\triage\\posts.jsonl'\ncov = set(json.load(open(r'D:\\Vault\\_imports\\content-factory\\cov_tmp.json',encoding='utf-8')))\nrows=[json.load

---

**Claude:**

Выбор сделан.

- **Pick A** = `cc:live-60deca` (31.08, 34 дня в воронке, tier:medium, named journal case) 
- **Pick B** = `cc:0376b69c` (31.08, tier:teaser, честное признание: чинил не то)

Скипнуты с причиной и оставлены `new`: шесть канон-скипов + `cc:live-d4ef83` (стоп-слово) + `cc:live-8faf64` (кросс-дневной двойник) + 6 сидов `tier:longread` — их главный тир эта рутина не пишет, и пометить их `written` ради тизера = потерять лонгрид.

Шаг 2 — recall. Журнал поломок первым (правило 28.09):

---

> `Bash` -- {"command": "J=\"/e/Obsidian/Vault-Knowledge/00-System/Breakage-Journal.md\"; ls -la \"$J\"; for t in MSIX NeedsRemediation \"вотчдог\" \"BOM\" \"Claude Desktop\"; do echo \"=== $t\"; grep -n \"$t\" \"$J\" | cut -c1-120; done", "description": "Locate journal rows for pick A"}

---

**Claude:**

Нашлась **семья** и — важное — строка от СЕГОДНЯ. Читаю (двухшаговое чтение, правило 29.09):

---

> `Bash` -- {"command": "J=\"/e/Obsidian/Vault-Knowledge/00-System/Breakage-Journal.md\"; for n in 3871 3875 3876; do echo \"######## line $n\"; sed -n \"${n}p\" \"$J\" | fold -w 185; done", "description": "Read case-5 journal rows"}

---

**Claude:**

Семья богатая, и премисса сида частично протухла ещё 31.08 (журнал сам опроверг «лечит только ребут»). Проверяю, что правда **сегодня** — правило 1-nonies:

---

> `Bash` -- {"command": "J=\"/e/Obsidian/Vault-Knowledge/00-System/Breakage-Journal.md\"; for n in 95 223 468; do echo \"######## line $n\"; sed -n \"${n}p\" \"$J\" | fold -w 185; done", "description": "Read today's row and recent BOM rows"}

---

**Claude:**

Вот он — хребет поста A. Детектор был собран 31.08, а класс родился заново **30.09 и 02.10**. Замеряю сегодняшнее состояние:

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/content-factory && cat > _scratch/ps1_scan_1004.py <<'EOF'\nimport os\nroots=[os.path.expanduser(r'~\\.claude\\scripts')]\ntot=0; risk=[]; bom=0\nfor root in roots:\n    for dp,dn,fn in os.walk(root):\n        dn[:]=[d for d in dn if d not in ('.git','.stversions

---

**Claude:**

4 RISK против 16 на 31.08 — но проверяю этот *удобный* вывод усиленно (§5.4) и смотрю на те два файла, что родились больными 30.09 и 02.10:

---

> `Bash` -- {"command": "cd ~ && for f in $(find .claude -name 'fleet_ssh_win_server.ps1' -o -name 'audio_default.ps1' 2>/dev/null); do echo \"== $f\"; python -c \"\nimport sys\nb=open(r'$(cygpath -w ~)\\\\'+r'$f'.replace('/','\\\\\\\\'),'rb').read()\nprint('  bom:', b.startswith(b'\\xef\\xbb\\xbf'), ' nonascii

---

**Claude:**

`fleet_ssh_win_server.ps1` сегодня уже с BOM — вылечен после 02.10; `audio_default.ps1` был в скретчпаде и его нет. Считаю семью класса прибором:

---

> `Bash` -- {"command": "cd ~/.claude/scripts && python prior_art.py class \"ps1 UTF-8 без BOM кириллица PowerShell 5.1 парсер падает\" 2>&1 | head -40", "description": "prior_art family count for BOM class"}

---

**Claude:**

Прибор нашёл 2 — но имена классов расходятся, поэтому считаю семью по слагам сам (дисциплина 30.09: оба чтения, промоушен не мой):

---

> `Bash` -- {"command": "J=\"/e/Obsidian/Vault-Knowledge/00-System/Breakage-Journal.md\"; grep -oE '202[0-9]-[0-9]{2}-[0-9]{2}[^|]*\\| *(powershell-encoding-silently-breaks-tool|powershell-bom-breaks-python-json|ps1-no-bom-cyrillic-parse-death|cmd-ps1-cyrillic-mojibake|ssh-powershell-relsa-tri-grabli)' \"$J\" |

---

> `Bash` -- {"command": "J=\"/e/Obsidian/Vault-Knowledge/00-System/Breakage-Journal.md\"; for n in 2591 3309 3314 48; do echo \"######## $n\"; sed -n \"${n}p\" \"$J\" | fold -w 185 | head -8; done", "description": "Read earlier encoding-family rows"}

---

**Claude:**

Семья полная, и она страшнее сида. Порог 3 был пройден **24 августа** — там же записано «положена отдельная сессия починки класса». Смотрю карточку:

---

> `Bash` -- {"command": "f=$(find /e/Obsidian/Vault-Knowledge -name '*ps51-encoding-class*' 2>/dev/null | head -3); echo \"FOUND: $f\"; for x in $f; do echo \"===== $x\"; sed -n '1,45p' \"$x\"; done", "description": "Read the ps51-encoding-class task card"}

---

> `Bash` -- {"command": "x=/e/Obsidian/Vault-Knowledge/10-Tasks/task-2026-08-24-ps51-encoding-class.md; wc -l \"$x\"; sed -n '45,120p' \"$x\"", "description": "Read rest of the task card"}

---

**Claude:**

Карточка переворачивает сид. Механизм **был** построен 24.08 — проверяю, на что именно он смотрит:

---

> `Bash` -- {"command": "cd ~/.claude/scripts/_shared && ls -la bom_scan.py 2>/dev/null; echo \"--- extensions / patterns ---\"; grep -nE \"\\.(py|json|ps1|cmd|md)|EXT|suffix|endswith|since_hours\" bom_scan.py | head -25", "description": "Inspect bom_scan.py scope"}

---

**Claude:**

✅ Доказано на диске, строка 21: `EXTS = (".py", ".json")`. Детектор, закрывавший класс, **не смотрит на `.ps1` вообще** — и ищет BOM *присутствующий*, тогда как у `.ps1` дефект обратный: BOM *отсутствует*. Все последующие случаи класса прилетели через неинструментированное лицо.

Проверяю, жив ли сам тест:

---

> `Bash` -- {"command": "cd ~/.claude/scripts && ls -la _shared/_test_bom_scan.py 2>/dev/null && python _shared/_test_bom_scan.py 2>&1 | tail -5; echo \"exit=$?\"", "description": "Run the bom_scan regression test live"}

---

> `Bash` -- {"command": "cd ~/.claude/scripts && find . -name '_test_bom_scan.py' 2>/dev/null; echo \"---\"; ls _shared/ | grep -i bom", "description": "Locate the bom_scan test"}

---

> `Bash` -- {"command": "cd ~/.claude/scripts && python _test_bom_scan.py 2>&1 | tail -8; echo \"exit=${PIPESTATUS[0]}\"", "description": "Run bom_scan test from correct path"}

---

**Claude:**

🚨 Живой красный. Проверяю факт и то, кричал ли прибор:

---

> `Bash` -- {"command": "cd ~/.claude/scripts && python -c \"\nimport os,time\np=os.path.expanduser(r'~\\.claude\\scripts\\_shared\\_logontype_seen.json')\nb=open(p,'rb').read()\nprint('BOM present:', b.startswith(b'\\xef\\xbb\\xbf'), '| size', len(b))\nprint('mtime:', time.strftime('%Y-%m-%d %H:%M', time.local

---

> `Bash` -- {"command": "cd ~/.claude/scripts && sed -n '168,200p' os_task_watchdog.ps1 | grep -nE \"Set-Content|Out-File|WriteAllText|Encoding|ConvertTo-Json\" ", "description": "Read the writer lines in os_task_watchdog.ps1"}

---

**Claude:**

`Set-Content -Encoding UTF8` на строке 186 — **ровно та строка, которую карточка 24.08 объявила починенной на `WriteAllText`**. Сегодня она на месте в сломанном виде. Проверяю, была ли починка и потерялась ли:

---

> `Bash` -- {"command": "cd ~/.claude/scripts && git log --oneline -3 -- os_task_watchdog.ps1 2>&1 | head -5; echo \"---git?---\"; git rev-parse --is-inside-work-tree 2>&1 | head -2; echo \"--- regress grid: does it run & log? ---\"; ls -la ~/.claude/scripts/_regress*.log ~/.claude/scripts/regress_run.py 2>/dev

---

> `Bash` -- {"command": "cd ~/.claude/scripts && echo \"=== fix commit 91225e814 ===\"; git show 91225e814 --stat --format='%ad %s' --date=short -- os_task_watchdog.ps1 2>&1 | head -6; git show 91225e814 -- os_task_watchdog.ps1 2>&1 | grep -E \"^[+-].*(Set-Content|WriteAllText)\" | head -6; echo; echo \"=== lat

---

**Claude:**

Полностью доказанная цепочка, гипотез не нужно:

- **24.08** — фикс закоммичен: `WriteAllText` + `UTF8Encoding($false)`, с комментарием «единственный безопасный путь в PS 5.1»
- **15.09 22:07** — коммит `auto-snapshot` **откатил фикс обратно** на `Set-Content -Encoding UTF8`, вместе с комментарием
- **сегодня 05:30** — BOM снова в файле, регресс-тест красный

Авто-бэкап — «транспорт, не автор» (§5.11) — переписал доказанную починку старой сломанной версией. Проверяю, кто вообще гоняет сетку:

---

> `Bash` -- {"command": "powershell -NoProfile -Command \"Get-ScheduledTask | Where-Object {\\$_.TaskName -match 'regress|Regress'} | ForEach-Object { \\$i=\\$_ | Get-ScheduledTaskInfo; '{0} | State={1} | Last={2} | Result={3} | Missed={4}' -f \\$_.TaskName, \\$_.State, \\$i.LastRunTime, \\$i.LastTaskResult, \\

---

**Claude:**

Сетка гоняется, но «Regress Grid Nightly» висит в `Running` с 02:40 — 19 часов, а вторая задача `TERMINATED`; коды 267009/267014 — это состояние задачи, не вердикт теста. Беру это как подпорку, а не как мораль — мораль 03.10 про «алярм без получателя» повторять не буду (1-bis).

Recall по сиду B:

---

> `Bash` -- {"command": "J=\"/e/Obsidian/Vault-Knowledge/00-System/Breakage-Journal.md\"; echo \"######## 3879\"; sed -n '3879p' \"$J\" | fold -w 185; echo; echo \"=== voice rows ===\"; grep -nE \"голосов|voice-triage|voice_|диктофон|plaud\" \"$J\" | cut -c1-135 | head -18", "description": "Read voice-related j

---

**Claude:**

Сид B — про другое: «полез строить свою транскрипцию вместо готовой рельсы». Ищу его артефакт:

---

> `Bash` -- {"command": "J=\"/e/Obsidian/Vault-Knowledge/00-System/Breakage-Journal.md\"; grep -nE \"транскрипц|своё решение вместо|уже существ|готов(ая|ую) рельс|изобрел|переизобр|not-invented|уже было\" \"$J\" | cut -c1-140 | head -20", "description": "Search journal for the reinvention story"}

---

**Claude:**

Нашлась **вторая семья** — ровно дефект сида B. Читаю:

---

> `Bash` -- {"command": "J=\"/e/Obsidian/Vault-Knowledge/00-System/Breakage-Journal.md\"; for n in 3193 957 275; do echo \"######## $n\"; sed -n \"${n}p\" \"$J\" | fold -w 185 | head -10; echo; done", "description": "Read the reinvention family rows"}

---

**Claude:**

Семья B: **21.08 → 31.08 (наш сид) → 22–23.09 → 02.10**, и последний случай даёт самое злое следствие. Замеряю инвентарь, который сессия обязана вспомнить перед постройкой:

---

> `Bash` -- {"command": "cd ~/.claude/scripts && echo \"py tools under ~/.claude/scripts: $(find . -name '*.py' -not -path '*/__pycache__/*' -not -path '*/.stversions/*' -not -name '_test_*' | wc -l)\"; echo \"tests: $(find . -name '_test_*.py' | wc -l)\"; echo \"--- canonical vs ad-hoc (02.10 case) ---\"; ls -

---

**Claude:**

Замерено сегодня: **1659** питон-инструментов под `~/.claude/scripts` (без тестов) + 792 теста; канонический `validate_links.py` жив с 22 июля; три ad-hoc переизобретения от 02.10 уехали в `_archive_oneoffs/`.

Развилка 03.10(c) по живому красному: ломается **не мой** файл (`os_task_watchdog.ps1` + движок авто-бэкапа), и повторная правка строки — лечение симптома: бэкап уже доказал, что откатит её снова. Значит — **докладываю громко, не чиню**, и пишу это в `evidence_level`.

Беру футер:

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/content-factory && grep -nE \"^#|^##|Telegram|linktr|github|Придумано|^- |^🟢|^✔\" _STYLE-footer.md | sed -n '1,45p'", "description": "Read footer blocks"}

---

**Claude:**

Строка 79 — `🟢 Telegram RU: https://t.me/ClawRus`, снова живым. **Пятнадцатый доклад** об этом расхождении; в черновиках follow-ссылку веду на @PaloAltoAiRu, сам футер не правлю (зона Норы).

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/content-factory && sed -n '13,53p' _STYLE-footer.md", "description": "Read footer block bodies A B C E"}

---

**Claude:**

Материал собран. Проверяю константы судьи перед записью (правило 23.09 — мерить его же функциями):

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/content-factory && python -c \"\nimport slop_gate as sg\nprint('FIRST_PERSON:', sorted(sg.FIRST_PERSON))\nprint('SHORT_SHARE_MIN:', sg.SHORT_SHARE_MIN, 'FIRST_PERSON_MIN:', sg.FIRST_PERSON_MIN)\nprint('TIER caps:', getattr(sg,'TIER_LEN',None))\n\" 2>&1 | head -8;

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/content-factory/drafts && sed -n '/FIRST COMMENT/,$p' 2026-10-03-dver-est-tolko-v-stroke-o-ney-medium-fb-DRAFT.md 2>/dev/null | head -25", "description": "Copy established footer form from last night"}

---

**Claude:**

Пишу генератор (правило 28.09/30.09 — никакой прозы через heredoc):

---

> `Write` -- {"file_path": "D:\\Vault\\_imports\\content-factory\\_scratch\\gen_1004.py", "content": "# -*- coding: utf-8 -*-\n\"\"\"gen_1004.py - generator for content-drain-daily 2026-10-04.\nSix draft files (2 seeds x teaser-ru / teaser-en / medium-fb), identical headers per seed.\nWritten as a .py (not a 

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/content-factory && python _scratch/gen_1004.py 2>&1 | head -20", "description": "Run the draft generator"}

---

**Claude:**

Шесть файлов есть. Мерю общим верстаком (правило 26.09 — не копировать его):

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/content-factory && python _scratch/measure_0924.py drafts/2026-10-04-*-DRAFT.md 2>&1 | head -60", "description": "Measure all six drafts with the shared verstak"}

---

**Claude:**

Верстак поймал три дефекта **до** гейта — ровно за этим он и нужен: RU-тизер A 275 против жёсткого потолка 250, EN-тизер A 251, и у medium B доля коротких 24% против порога 30%. Правлю в генераторе.

---

> `Edit` -- {"replace_all": false, "file_path": "D:\\Vault\\_imports\\content-factory\\_scratch\\gen_1004.py", "old_string": "A_RU = \"\"\"24 августа я починил строку и доказал корень.\n\n15 сентября мой же авто-бэкап откатил её назад. молча.\n\nсегодня дефект на месте. бэкап - транспорт, а не автор.\n\nу ме

---

> `Edit` -- {"replace_all": false, "file_path": "D:\\Vault\\_imports\\content-factory\\_scratch\\gen_1004.py", "old_string": "тогда это выглядело как мой личный ляп. я честно его назвал и пошёл дальше.\n\nсегодня я полез в журнал и увидел, что это не ляп, а семья с датами.", "new_string": "тогда это выглядел

---

> `Edit` -- {"replace_all": false, "file_path": "D:\\Vault\\_imports\\content-factory\\_scratch\\gen_1004.py", "old_string": "2 октября - проверку ссылок в волте, вместо канонической.", "new_string": "2 октября - проверку ссылок в волте. вместо канонической."}

---

> `Edit` -- {"replace_all": false, "file_path": "D:\\Vault\\_imports\\content-factory\\_scratch\\gen_1004.py", "old_string": "ни одна из них битой не была.", "new_string": "ни одна не была битой."}

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/content-factory && python _scratch/gen_1004.py >/dev/null 2>&1 && python _scratch/measure_0924.py drafts/2026-10-04-*-DRAFT.md 2>&1 | head -30", "description": "Re-run generator and re-measure"}

---

**Claude:**

Все шесть в бюджете. Шаг 4 — гейт:

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/content-factory && for f in drafts/2026-10-04-*-DRAFT.md; do echo \"===== $(basename $f)\"; python slop_gate.py --file \"$f\" 2>&1 | tail -14; done", "description": "Run slop_gate on all six drafts"}

---

**Claude:**

**Ноль FAIL с первого прохода** — девятый чистый заход подряд. Теперь спрашиваю публикатора (правильная подпись + контроль, правило 27.09):

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/content-factory && python -c \"\nimport os, re, distributor as D\nfor f in sorted(os.listdir('drafts')):\n    if not f.startswith('2026-10-04'): continue\n    p=os.path.join('drafts',f); raw=open(p,encoding='utf-8').read()\n    tier, route = D.parse_route(raw, f)

---

**Claude:**

Все шесть маршрутизируются: `tg_paloaltoairu` (живой) / `x_en` / `fb_wall`, раскрытие на месте, паузный @ClawRus не тронут.

⚠️ Мелочь в лог: контроль 27.09 описан как «`facebook` даёт (None, None)» — сегодня при передаче и текста, и имени файла он вернул `(None, ('fb_wall','facebook',None))`. Контроль слабее, чем записано; мои шесть вызовов это не затронуло.

Шаг 5 — клок:

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/content-factory && python -c \"\nimport approval_clock as ac\nprint('WINDOW_HOURS_DEFAULT =', ac.WINDOW_HOURS_DEFAULT)\n\"; for pair in \"teaser-ru teaser @PaloAltoAiRu\" \"teaser-en teaser x\" \"medium-fb medium facebook\"; do set -- $pair; for slug in bekap-per

---

**Claude:**

Шаг 6 — отметка сидов (бэкап перед записью + `--heal`), и сразу контрольный пересчёт по правилу 30.09 (воронка — не закрытая система):

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports && python vault_backup.py \"content-drain\" 2>&1 | tail -3; cd content-factory && python drain_dedup.py --heal 2>&1 | tail -8", "description": "Backup then heal/mark drained seeds"}

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/content-factory && python drain_dedup.py --covered --json > cov_after.json 2>&1; python -c \"\nimport json\nFUN=r'D:\\Vault\\_imports\\content-factory\\triage\\posts.jsonl'\nrows=[json.loads(l) for l in open(FUN,encoding='utf-8') if l.strip()]\nprint('rows aft

---

**Claude:**

`covered` прочиталось как **2** вместо ~197 — это ровно тот почерк ложного покрытия, про который предупреждает запись 30.09. Проверяю, а не верю:

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/content-factory && echo \"--- raw head of cov_after.json ---\"; head -c 400 cov_after.json; echo; echo \"--- rerun plainly ---\"; python drain_dedup.py --covered --json 2>&1 | head -c 300; echo; echo \"--- length ---\"; python drain_dedup.py --covered --json 2>/d

---

**Claude:**

Ложная тревога, и поймана она ровно тем «дешёвым признаком» из записи 30.09: вывод — это **словарь из 2 ключей**, а я померил `len()` по словарю, а не по списку `covered`. Данные целы, кривым был мой считыватель:

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/content-factory && python -c \"\nimport json\nd=json.load(open(r'D:\\Vault\\_imports\\content-factory\\cov_after.json',encoding='utf-8'))\nprint('keys:', list(d.keys()))\nc=d['covered']\nprint('covered AFTER:', len(c), '(before: 195)')\nprint('both new ids pre

---

**Claude:**

`covered` 195 → **197**, оба id на месте, оба `written`, строк 2821 → 2821 (сегодня приходов не было), `new` 916 → 914.

Прежде чем докладывать — журналю по §5.10. Спрашиваю инструмент о флагах (семья «неразобранная подпись»):

---

> `Bash` -- {"command": "cd ~/.claude/scripts && python selfheal.py journal --help 2>&1 | head -25", "description": "Read selfheal journal CLI signature"}

---

> `Bash` -- {"command": "cd ~/.claude/scripts && grep -nE '\"--(class|what|conditions|parts|guess|severity)\"|add_argument' selfheal.py | head -20", "description": "Find selfheal journal flags in source"}

---

**Claude:**

Флаги подтверждены. Сначала счёт семьи для нового класса:

---

> `Bash` -- {"command": "cd ~/.claude/scripts && python prior_art.py class \"авто-снимок бэкапа откатил доказанную починку поверх новой версии\" 2>&1 | head -30", "description": "prior_art for the new revert class"}

---

**Claude:**

Читаю соседей, не верю счёту на слово (дисциплина 30.09). Реальные зеркала: **11.08** `package-install-reverts-newer-local-file`, **18.08** даунгрейд `deploy_lib.py` (там уже 3-й случай), **18.08** потеря `.gitignore` при переписывании целиком. Три — вокабулярный шум (push 24 файлов, красная зона CLAUDE.md, вывод по одной поверхности).

Пишу строку журнала четырьмя ячейками, с проверкой длин до записи:

---

> `Write` -- {"file_path": "D:\\Vault\\_imports\\content-factory\\_scratch\\journal_1004.py", "content": "# -*- coding: utf-8 -*-\n\"\"\"journal_1004.py - write tonight's breakage rows via selfheal.py.\nProse payload goes through a .py, never a bash heredoc (prompt rule 2026-09-28, widened 2026-09-30).\nFour 

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/content-factory && python _scratch/journal_1004.py 2>&1 | head -40", "description": "Write journal rows with length pre-check"}

---

**Claude:**

Пред-проверка отбила запись — ровно для этого правило 30.09 и писалось. Укорачиваю две ячейки:

---

> `Edit` -- {"replace_all": false, "file_path": "D:\\Vault\\_imports\\content-factory\\_scratch\\journal_1004.py", "old_string": "        what=(\n            'Авто-бэкап ~/.claude/scripts откатил ДОКАЗАННУЮ починку поверх новой версии. 24.08 коммит 91225e814 '\n            'заменил в os_task_watchdog.ps1 стр

---

> `Edit` -- {"replace_all": false, "file_path": "D:\\Vault\\_imports\\content-factory\\_scratch\\journal_1004.py", "old_string": "        guess=(\n            'СЧЁТ, ОБА ЧТЕНИЯ. Своим именем это 1-й случай. По семье \"автоматический транспорт пишет старую версию '\n            'поверх новой доказанной\" prio

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/content-factory && python _scratch/journal_1004.py 2>&1 | head -45", "description": "Write journal rows after shortening"}

---

> `Edit` -- {"replace_all": false, "file_path": "D:\\Vault\\_imports\\content-factory\\_scratch\\journal_1004.py", "old_string": "            'СЧЁТ, ОБА ЧТЕНИЯ. Своим именем - 1-й случай. По семье \"транспорт пишет старую версию поверх новой '\n            'доказанной\" prior_art дал 6, реальных зеркал 3: 11

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/content-factory && python _scratch/journal_1004.py 2>&1 | head -45", "description": "Write journal rows, third attempt"}

---

**Claude:**

Обе строки записаны четырьмя ячейками, ничего не срезано. Прибор снова предупредил о заниженном счёте, и предложенные соседи говорят сами за себя: `sync-conflict-reverts-shipped-fix`, `stale-snapshot-clobbers-live-write`. Оба чтения лежат в ячейке `guess`, промоушен — владельцу класса.

Шаг 7 — доклад в 03. Пост и хартбит **раздельно** (правило 02.10):

---

> `Write` -- {"file_path": "D:\\Vault\\_imports\\content-factory\\_scratch\\post_1004.py", "content": "# -*- coding: utf-8 -*-\n\"\"\"post_1004.py - chat-03 report for content-drain-daily 2026-10-04.\nPOST ONLY. The heartbeat runs as a SEPARATE step (prompt rule 2026-10-02: a heartbeat\nin the same process pr

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/content-factory && python _scratch/post_1004.py 2>&1 | head -25", "description": "Post the chat-03 report"}

---

**Claude:**

`PING OK -> chat_REDACTED` — прочитал глазами. Доказываю доставку тремя частями и ставлю хартбит **отдельным** шагом:

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/content-factory && python -c \"\nimport os,sys\nsys.path.insert(0, os.path.join(os.path.expanduser('~'),'.claude','scripts'))\nimport bus_ping as bp\nsp=bp.SPOOL\nprint('SPOOL path exists:', os.path.exists(sp))\nif os.path.exists(sp):\n    import io\n    for i,l 

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/content-factory && python -c \"\nimport os, subprocess, sys\nhb = os.path.join(os.path.expanduser('~'),'.claude','scripts','cron_heartbeat.py')\np = subprocess.run([sys.executable, hb, 'content-drain-daily'], capture_output=True, text=True, encoding='utf-8', erro

---

**Claude:**

Операционная часть закрыта. Остался вердикт по собственной инструкции (§9.3-бис) — нахожу живой файл промпта:

---

> `Grep` -- {"pattern": "CONTENT_DRAIN_AUTORUN", "path": "C:\\Users\\dev\\.claude", "output_mode": "files_with_matches"}

---

> `Grep` -- {"pattern": "1-octies|KLON-GATE|content-drain-daily", "path": "C:\\Users\\dev\\.claude", "output_mode": "files_with_matches", "head_limit": 25}

---

> `Bash` -- {"command": "powershell -NoProfile -Command \"Get-ScheduledTask | Where-Object {\\$_.TaskName -match 'Content Drain|content-drain'} | ForEach-Object { \\$_.TaskName; \\$_.Actions | ForEach-Object { '  EXE: '+\\$_.Execute; '  ARG: '+\\$_.Arguments } }\" 2>&1 | head -12", "description": "Find the laun

---

> `Bash` -- {"command": "cat ~/.claude/scripts/content_drain_daily.cmd 2>/dev/null | head -30", "description": "Read the launcher to find the prompt file"}

---

**Claude:**

Живой промпт найден: `~/.claude/scheduled-tasks/content-drain-daily/SKILL.md`.

---

> `Bash` -- {"command": "P=~/.claude/scheduled-tasks/content-drain-daily/SKILL.md; ls -la \"$P\"; echo \"bytes: $(wc -c < \"$P\")\"; echo \"--- tail anchor ---\"; tail -4 \"$P\" | cut -c1-120", "description": "Confirm live prompt file and its size"}

---

**Claude:**

161,772 байта (было 146,645) — рост ~15 КБ/ночь, ускоряется. Вношу правки инструкции из пережитой боли:

---

> `Write` -- {"file_path": "D:\\Vault\\_imports\\content-factory\\_scratch\\promptfix_1004.py", "content": "# -*- coding: utf-8 -*-\n\"\"\"promptfix_1004.py - edit the LIVE content-drain-daily prompt after tonight's run.\nProse payload goes through a .py, never a bash heredoc (prompt rule 2026-09-28, widened 

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/content-factory && python _scratch/promptfix_1004.py 2>&1 | head -20", "description": "Apply the four inline prompt fixes"}

---

**Claude:**

Скрипт отказался писать частично — верно. Смотрю фактические строки в файле (перенос строк в промпте отличается):

---

> `Bash` -- {"command": "P=~/.claude/scheduled-tasks/content-drain-daily/SKILL.md; grep -n \"Re-angle, don't drop\" \"$P\"; echo \"---\"; grep -n \"without re-investigating\" \"$P\"; echo \"--- context 1 ---\"; grep -n -B2 \"Re-angle, don't drop\" \"$P\" | cat -A | sed 's/\\$$//' | cut -c1-200 | tail -6", "desc

---

> `Edit` -- {"replace_all": false, "file_path": "D:\\Vault\\_imports\\content-factory\\_scratch\\promptfix_1004.py", "old_string": "    \"On 13.09 the seed cc:live-18ae74 (\\\"the watchdog lied about 328 orphans\\\") was about to ship the moral \\\"the instrument is blind\\\" on the same day\\n   and same ch

---

> `Edit` -- {"replace_all": false, "file_path": "D:\\Vault\\_imports\\content-factory\\_scratch\\promptfix_1004.py", "old_string": "    \"`cc:live-aca9c8` (\\\"six resumes of one person\\\") is a 1-septies job-search seed - six packagings of dev's CV -\\n   and sorts second in the pool. Skip it for the sam

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/content-factory && python _scratch/promptfix_1004.py 2>&1 | head -20", "description": "Re-apply prompt fixes with corrected anchors"}

---

> `Bash` -- {"command": "P=~/.claude/scheduled-tasks/content-drain-daily/SKILL.md; echo \"bytes now: $(wc -c < \"$P\")\"; python -c \"\nb=open(r'C:\\Users\\dev\\.claude\\scheduled-tasks\\content-drain-daily\\SKILL.md','rb').read()\nprint('CR bytes:', b.count(b'\\r'), '| LF:', b.count(b'\\n'), '| non-ascii:', 

---

**Claude:**

Переносы строк не повреждены: файл и до правки был LF-only (разница байт/символов = 3051 ≈ число не-ASCII символов, CR = 0). Дописываю запись в PROMPT-FIX LOG:

---

> `Write` -- {"file_path": "D:\\Vault\\_imports\\content-factory\\_scratch\\logentry_1004.py", "content": "# -*- coding: utf-8 -*-\n\"\"\"logentry_1004.py - append tonight's PROMPT-FIX LOG entry to the live prompt.\nProse through a .py, never a bash heredoc (rule 2026-09-28, widened 2026-09-30).\n\"\"\"\nimpo

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/content-factory && python _scratch/logentry_1004.py 2>&1 | head -8; P=~/.claude/scheduled-tasks/content-drain-daily/SKILL.md; echo \"bytes now: $(wc -c < \"$P\")\"; echo \"--- new rules present? ---\"; grep -c \"1-bis-BIS\\|1-decies\\|IT RETURNS AN OBJECT\\|THE 2

---

**Claude:**

Прогон закрыт полностью. Промпт теперь 178 192 байта, все четыре правки и запись лога на месте.

## Что сделано

**Сдренировано 2 сида → 6 черновиков, ноль FAIL с первого прохода** (девятый чистый заход подряд). Клок записан на 22:21:45–46 UTC, окно 0ч — релизятся следующим тиком дистрибьютора.

| сид | возраст | пост |
|---|---|---|
| `cc:live-60deca` | 34 дня | `bekap-perepisal-moyu-pochinku` (249 / 247 / 1395) |
| `cc:0376b69c` | 34 дня | `u-menya-1659-instrumentov` (245 / 233 / 1394) |

Воронка: строк 2821 → 2821 (приходов за прогон не было), `new` 916 → 914, covered 195 → **197**, оба сида `status=written` с `draft_path`.

## 🚨 Живой красный — нужен владелец, я не чинил

24 августа была починена строка в `os_task_watchdog.ps1`: ленивая запись заменена на `WriteAllText` с явной кодировкой, корень доказан, рядом оставлен комментарий «только так можно». 15 сентября в 22:07 коммит `auto-snapshot` **удалил и починку, и комментарий**, вернув сломанную версию.

Сегодня метка BOM снова в файле (05:30), `_test_bom_scan.py` падает — регресс-сетка красная 19 дней. Чинить строку второй раз я отказался намеренно: корень в движке снимков, а повторная правка дала бы ложный зелёный и была бы снята следующим снимком.

Тем же замером, слоем ниже: `bom_scan.py` смотрит только на `.py` и `.json` и ищет BOM **присутствующий**, тогда как у `.ps1` дефект обратный. Карточка сама назвала «три лица одного дефекта» — а инструментировала одно, и все последующие случаи класса (31.08, 02.09, 10.09 ×2, 30.09, 02.10) прилетели через неинструментированное лицо.

## Инструкция рутины — 🔧 обновляю

Две новые ступени и две правки существующих, все из пережитой боли: **кросс-дневной двойник** (сид `cc:live-8faf64` с другой моралью, но тем же артефактом, что уже вышел 01.10 — покрытие такое не видит); **фильтр по тиру** (шесть `tier:longread` сидов забили верх пула, а пометить их `written` ради тизера = потерять лонгрид); форма JSON у `--covered` (объект, не массив — мой же считыватель напечатал «covered: 2» вместо 197); и неверно задокументированный контроль `parse_route` от 27.09.

Журнал: две строки по четыре ячейки, пред-проверка длины дважды отбила запись, так что молча на 400 знаках ничего не срезалось. Счёт семьи записан **двумя чтениями** — своим именем 1-й случай, по семье 4-й; промоушен в сессию починки оставлен владельцу класса, не контентной рутине.

Дашборд не строил, и вот причина: решение-несущий факт здесь один (красный с названным владельцем), и он уже лежит в двух правильных местах — чат 03 и строка журнала. Третья копия двух чисел нарушила бы «один источник».

По рельсам (§6.3-бис): план я назвал прозой в первом ответе, но машиночитаемо через `rail_plan.py declare` **не оформил** — штамповать декларацию задним числом не стал, это была бы ровно та фальшивая зелень, про которую сегодняшний пост. Вердикт недобора: `class-mismatch` — вся работа это оркестрация, суждение, голос и волт, то есть класс Claude; плюс STOP-блок рутины запрещает исходящее.

🎙 **Майк:** идём верно, но меня царапает одна мысль из сегодняшнего замера, и она шире одного файла. Если снимок может тихо вернуть старую версию **любого** файла в `~/.claude/scripts`, то у каждого нашего «починено и закоммичено» есть необъявленный срок годности — а я проверил ровно один файл из сотен. Вопрос к тебе: пустить отдельную сессию, которая сверит закоммиченные починки за последний месяц против того, что лежит на диске сейчас?

🧒 **Простыми словами:** я взял две старых записки из коробки «про что написать» и сделал из каждой три готовых текста — шесть штук, все прошли проверку с первого раза. Пока копался, нашёл кое-что похуже: в августе я починил поломку, а моя же программа для резервных копий взяла и записала сверху старую сломанную версию. Девятнадцать дней всё было сломано, и никто не заметил. Чинить второй раз я не стал — копия снова всё затрёт, лечить надо копию, а не файл. Я громко про это доложил и записал в журнал. И ещё подправил себе инструкцию в четырёх местах, чтобы завтра не наступить на те же грабли.
