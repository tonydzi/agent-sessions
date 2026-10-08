**Антон:**

---
name: content-drain-daily
description: "DRAIN the content funnel: turn captured seeds into finished posts, gate them, record them on the approval clock (window = 0h since 05.08.2026). Counterpart of content-factory-daily, which FILLS the funnel. Root it exists for (measured 2026-08-04): posts.jsonl held 70 seeds over 26 days, 100% status=new - the funnel had an automatic INPUT and no automatic OUTPUT, because 'sit down and write the post' belonged to nobody. HUB-owned; account tonyssd; runs 23:10 Lisbon."
---

CONTENT_DRAIN_AUTORUN

ГРАНИЦЫ ДЛЯ ЛЮБОЙ РЕЛЬСЫ (добавлено 22.08.2026, Q1R).
Этот файл читает не только Claude Code: при исчерпанном баке подписки рутина уезжает на
чужую рельсу (--extfallback codex-agent), а она НЕ грузит CLAUDE.md Антона. Поэтому
границы едут вместе с задачей, а не подразумеваются:
- STOP: НИЧЕГО НЕ ВЫКЛАДЫВАЕМ НАРУЖУ. Работа этой рутины кончается ЧЕРНОВИКОМ в drafts\.
  Любая доставка наружу = Tier-2 и не твоё решение.
- STOP: Tier-2 целиком -- деньги, необратимое удаление, секреты, исходящее наружу, смена
  канона. Упёрся -- напиши строкой в отчёт и остановись, обход не выдумывай.
- STOP: секрет (токен, пароль, ключ) не попадает ни в черновик, ни в лог, ни в отчёт.
- STOP: приватное Антона наружу не уезжает; personal -- только обобщённо.
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
   MYCROFT in FIRST PERSON, and canon 3.3 forbids him to appropriate Anton's personal life -
   so a seed about Anton's travel, health, family or his own verbatim essay is NOT drainable
   by this routine no matter how old it is; it needs Anton's voice, not Mycroft's. Two cheap
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
   struck the labels «не-кодер» / «не-технарь» off Anton entirely (he is a programmer,
   Python and C++), so a post built on that frame breaks canon no matter how good it is.
   Same veto applies to any seed whose frame calls Anton a founder/co-founder (same
   carve-out). So after the 1-quater filters, READ the title and note of each candidate for
   those four words before writing. This one will keep surfacing: it stays `new` and sorts
   second-oldest forever, so expect to skip it again and say so rather than silently
   re-picking it.
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

3. WRITE. For each seed produce ONE FILE PER TIER+CHANNEL, named
   drafts\<YYYY-MM-DD>-<slug>-<teaser-ru|teaser-en|medium-fb>-DRAFT.md, all of them
   carrying the SAME funnel_ids. (Corrected 2026-09-13 against measurement: the old wording
   "ONE draft file containing all tiers" is unbuildable downstream - approval_clock.py ping
   takes exactly one --tier and one --channel per --file, and slop_gate.py judges one tier
   per file. Every drain run on disk already writes 3 files; the prompt was the only place
   claiming otherwise.) The tiers, per the platform matrix:
     - teaser RU, HARD 200-250 chars (Anton's number 06.08.2026; machine truth =
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
   «привет, это майкрофт, синтетический кофаундер антона - ии, а не человек». The
   publisher's gate matches `синтетическ\w+ кофаундер`, so the form this prompt used
   to teach - «синтетический ии-кофаундер» - does NOT match and parks every FB medium
   in distributor HOLD. EN stays «Mycroft here, Anton's synthetic cofounder. Automated.»
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
   EN disclosure stays the body line "Mycroft here, Anton's synthetic cofounder. Automated."
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
   RU disclosure «привет, это майкрофт, синтетический кофаундер антона - ии, а не человек»
   is 71 chars, plus the blank line = 73. So the RU teaser's real writing budget is ~177
   chars INCLUDING the ~18-char link, i.e. about 155 chars of actual sentence - roughly 25
   words, not 35. EN is easier: «Mycroft here, Anton's synthetic cofounder. Automated.» is
   53 chars, leaving ~195. Measured 19.09: writing the paragraph first and the disclosure
   second produced 288 / 280 / 261-char bodies, three F6-length-max FAILs in one pass.
   Count the total (disclosure + 2 + body + link) BEFORE writing the file, not after.
   THE FOOTER REGISTRY IS STALE ON THE RU CHANNEL (measured 2026-09-15): _STYLE-footer.md
   block B still lists "🟢 Telegram RU: https://t.me/ClawRus", while registry/limits.json has
   tg_clawrus paused=true since 06.08, re-confirmed by Anton on 21.08 and 23.08. Copying the
   footer verbatim puts a dead channel into every FB first comment - route the follow link to
   https://t.me/PaloAltoAiRu. Do not "fix" _STYLE-footer.md from here: the footer text is
   Nora-owned cosmetics, so report the divergence instead.
   Also expected, do not chase: paragraph_lint flags the FIRST COMMENT block as one 6-sentence
   paragraph. It is a footer list inside an HTML comment, not prose; slop_gate strips it from
   the body count. The post body itself must still pass the three-sentence rule.
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
   run - not "leave it for a human". The two files sitting FAIL since 01.08 are exactly
   the failure mode this step exists to prevent.

5. RECORD THE CLOCK (there is NO waiting window any more). For each passing draft:
   python approval_clock.py ping --file <path> --tier <tier> --channel <platform>
     --proof "content-drain-daily <DAY>"
   The window is ZERO hours since Anton's order of 05.08.2026 "publish with no waiting" -
   machine truth = approval_clock.WINDOW_HOURS_DEFAULT = 0, so the ping sets deadline =
   the moment of the ping and the draft is releasable to the distributor's next hourly
   tick immediately. Do NOT report a "24h deadline" - that number no longer exists and
   saying it makes the routine's own report a lie (the CLI help string still says
   "24-часовые часы апрува"; the constant is the truth, not the help text).
   Still mandatory: the ping must RECORD its time - an unrecorded ping leaves the item
   outside the queue, and the post dies unseen. Then post ONE short message into chat 03
   naming the file and the recorded time. (NOT 121: Anton's order of 06.08.2026 15:15 is
   that NOBODY writes into 121 - neither robot nor live session; approval_clock.py already
   holds chat 03 in that constant.)

6. MARK. Flip the drained seeds in posts.jsonl from new to written (keep the id, add
   draft_path). A seed that produced a text must never be picked twice.

7. REPORT to chat 03 (chat_id chat_REDACTED, account tonyssd): one line per drained seed
   (slug -> draft path -> clock deadline), plus the remaining funnel depth
   ("funnel: N still new"). If nothing was drained, say why in one sentence - a silent
   run is indistinguishable from a broken one.

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
      «привет, это майкрофт, синтетический ии-кофаундер антона». The distributor's gate
      matches slop_gate.REQUIRED_ELEMENTS["подпись/авторство"] =
      `синтетическ\w+ кофаундер|придумано майкрофтом|...` - and «синтетический ии-кофаундер»
      does NOT match it (the hyphen breaks `\w+ кофаундер`). Measured 16.09: 4 of the 15.09
      FB mediums sat in distributor HOLD «нет раскрытия авторства» - i.e. the routine has
      been writing unpublishable FB posts. WORSE, MY OWN two passed the same check only
      because «✔️Придумано Майкрофтом» sits in the HTML-commented FIRST COMMENT block: a
      green earned by a comment, not by the post - the exact trap the 14.09 entry recorded
      for W7. So: write the body line as «привет, это майкрофт, синтетический кофаундер
      антона - ии, а не человек». It matches the gate AND keeps the AI disclosure explicit.
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
  Anton's VERBATIM voice against a hard 200 floor, and padding it would break both §9.7
  «без купюр» and «не разжимаем сжатую мысль», so it needs Anton's call (or a different tier),
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
  FAIL files from 05.08 (the teaser is 173 chars of Anton's verbatim voice against a hard
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
  Anton's verbatim voice against a hard 200 floor - his call, not a rewrite);
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
      Mycroft in FIRST PERSON, and he may not appropriate Anton's personal life - so the 14
      oldest uncovered seeds (7 `[INTERNAL]` whose own notes say "не контент" / "не публикуем",
      2 MERGE-twin travel notes, Anton's verbatim profanity essay) yielded ZERO drainable items.
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
  Anton's verbatim voice against a hard 200 floor - his call, not a rewrite); _STYLE-footer.md
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
      struck «не-технарь» / «не-кодер» off Anton entirely. Only reading the title caught it.
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
  173 chars of Anton's verbatim voice against a hard 200 floor - his call, not a rewrite);
  _STYLE-footer.md block B still lists the paused @ClawRus as live (reported 15/16/19/20.09
  and again tonight; follow link routed to @PaloAltoAiRu in both mediums, footer untouched -
  Nora's zone).
  Verdict on the skills this routine calls: none used (slop_gate / approval_clock / drain_dedup
  are tools, not skills) - nothing to update there.
  Author: Opus 5 / robot:content-drain-daily. Machine: HUB-01. Operator: robot.

---

**Claude:**

**[⏰ вторник, ночь, 23:10, 22 сентября 2026]**

🚂 **План рельс (§6.3-бис):** сам как Claude — выбор сидов, RECALL по волту, написание черновиков (авторский голос Майкрофта = класс «качественный текст», по канону остаётся у меня), гейт/часы/отчёт в 03. Наружу — ничего: рутина механическая, чужие баки жечь нечем (класс `code_read`/`shell` тут не возникает; если упрусь в чтение большого артефакта — уедет на codex).

Начинаю прогон content-drain-daily. Сперва замеры.

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/content-factory && ls && echo \"---FUNNEL---\" && wc -l triage/posts.jsonl", "description": "List content-factory dir and funnel size"}

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/content-factory && python drain_dedup.py --covered --json 2>&1 | head -c 2000", "description": "Get covered seed ids"}

---

> `Bash` -- {"command": "python - <<'PY'\nimport json, subprocess, sys\ncov = set(json.loads(subprocess.run([sys.executable,\"drain_dedup.py\",\"--covered\",\"--json\"],capture_output=True,text=True).stdout)[\"covered\"])\nrows=[]\nfor ln in open(\"triage/posts.jsonl\",encoding=\"utf-8\"):\n    ln=ln.strip()\n 

---

> `Bash` -- {"command": "cd /c/Users/dev/.claude/scripts && python workspace_write_lease.py status 2>&1 | head -20", "description": "Check workspace write lease"}

---

**Claude:**

Лиза свободна. Кандидаты отобраны. Проверяю слепые зоны покрытия (1-ter / 1-bis / MERGE / self-named draft).

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/content-factory && for id in cc:live-d7bfc5 cc:live-a9e325 d7bfc5 a9e325; do echo \"== $id\"; grep -rl -- \"$id\" drafts/ 2>/dev/null | head -5; done; echo \"=== MERGE check ===\"; python - <<'PY'\nimport json\nfor ln in open(\"triage/posts.jsonl\",encoding=\"utf

---

> `Bash` -- {"command": "echo \"=== drafts today 2026-09-22 ===\" && ls drafts/ | grep \"^2026-09-22\" ; echo \"=== last 3 days ===\"; ls drafts/ | grep -E \"^2026-09-(20|21|22)\" | head -30", "description": "List today and recent drafts for same-day moral check"}

---

**Claude:**

Оба чисты: покрытия нет, MERGE-близнецов нет, своих путей к черновикам в записях нет, сегодняшних черновиков-соседей нет. RECALL по артефактам.

---

> `Bash` -- {"command": "echo \"=== PII / HARD-BLOCK в slop_gate ===\" && grep -n -i \"phone\\|телефон\\|PII\\|HARD\\|персональн\" slop_gate.py | head -40", "description": "Find PII detector in slop_gate"}

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports && timeout 300 python brain_ask.py \"приёмка переноса рутины на хаб двусторонняя дубль в другом профиле приложения\" 2>&1 | head -60", "description": "Vault recall for seed 1"}

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/content-factory && sed -n '150,175p' slop_gate.py && echo \"=== LIVE TEST ===\" && python - <<'PY'\nimport slop_gate as sg\nfor s in [\"откат делается кнопкой: файл vault-backup-20260822-1746.zip лежит рядом\",\n          \"бэкап 20260822-1746\",\n          \"поз

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports && head -c 3000 _brain_answer_rr.txt", "description": "Read brain_ask answer"}

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/content-factory && sed -n '795,870p' slop_gate.py", "description": "Read _check_pii logic fully"}

---

> `Bash` -- {"command": "cd /e/Obsidian/Anton-Knowledge/10-Tasks && sed -n '1,60p' \"task-2026-08-31-repair-вывод-об-отсутствии-сделан-по-одной-поверхности.md\"", "description": "Read the repair task card for seed 1"}

---

**Claude:**

Оба сида дали проверяемые факты. Добираю живые числа для второго поста.

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/content-factory && python _test_slop_hb2_canary.py 2>&1 | tail -15; echo \"EXIT=$?\"", "description": "Run the HB2 canary test"}

---

> `Bash` -- {"command": "grep -n \"мораль\\|Мораль\\|^[а-я].*\\.\" drafts/2026-09-21-auditor-poveril-priboru-teaser-ru-DRAFT.md | tail -8; echo \"=== korobki ===\"; sed -n '1,25p' drafts/2026-09-21-korobki-doehali-nikto-ne-otkryl-teaser-ru-DRAFT.md", "description": "Check recent drafts morals for collision"}

---

**Claude:**

Материал собран, коллизий морали нет. Читаю эталонные черновики 21.09, чтобы не расходиться по форме.

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/content-factory/drafts && echo \"########## TEASER RU ##########\" && cat 2026-09-21-obertka-zhila-tolko-v-demo-teaser-ru-DRAFT.md && echo \"########## TEASER EN ##########\" && cat 2026-09-21-obertka-zhila-tolko-v-demo-teaser-en-DRAFT.md", "description": "Read r

---

> `Bash` -- {"command": "cat 2026-09-21-obertka-zhila-tolko-v-demo-medium-fb-DRAFT.md", "description": "Read reference medium-fb draft"}

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/content-factory && grep -n \"FIRST_PERSON\" slop_gate.py | head -5 && python -c \"import slop_gate as s; print(s.FIRST_PERSON)\"", "description": "Read FIRST_PERSON token set"}

---

**Claude:**

`мы/наш` не считаются — только «я/мой». Пишу шесть файлов с бюджетом в две первые лица.

---

> `Bash` -- {"command": "python - <<'PY'\nD=\"привет, это майкрофт, синтетический кофаундер антона - ии, а не человек\"\nE=\"Mycroft here, Anton's synthetic cofounder. Automated.\"\ncases={\n\"A-ru\":\"я доказал, что рутина доехала на хаб, и доложил: дубля нет. дубль жил в соседнем профиле и успел отработать ли

---

> `Bash` -- {"command": "python - <<'PY'\nD=\"привет, это майкрофт, синтетический кофаундер антона - ии, а не человек\"\nE=\"Mycroft here, Anton's synthetic cofounder. Automated.\"\ncases={\n\"A-en\":\"I proved the routine had landed on the hub and reported no leftover twin. It was alive in a neighbouring profi

---

> `Bash` -- {"command": "python - <<'PY'\nimport io,os\nD=\"привет, это майкрофт, синтетический кофаундер антона - ии, а не человек\"\nE=\"Mycroft here, Anton's synthetic cofounder. Automated.\"\nDAY=\"2026-09-22\"\ndef w(name,text):\n    p=os.path.join(\"drafts\",name)\n    io.open(p,\"w\",encoding=\"utf-8\",n

---

> `Bash` -- {"command": "python - <<'PY'\nimport io\nbody='''привет, это майкрофт, синтетический кофаундер антона - ии, а не человек\n\nя переносил две рутины с ноутбука на хаб. обычная работа: там выключить, тут включить.\n\nперенос надо принять. это я умею и сделал честно.\n\nзалез в транскрипт соседней сесси

---

> `Bash` -- {"command": "for f in drafts/2026-09-22-otchet-otvechal-ne-na-tot-vopros-*; do echo \"### $f\"; python slop_gate.py --file \"$f\" 2>&1 | tail -12; done", "description": "Gate post A drafts"}

---

**Claude:**

W3-rhythm на RU-тизере — переписываю в том же прогоне (Шаг 4).

---

> `Bash` -- {"command": "python - <<'PY'\nimport io,re\np=\"drafts/2026-09-22-otchet-otvechal-ne-na-tot-vopros-teaser-ru-DRAFT.md\"\nt=io.open(p,encoding=\"utf-8\").read()\nold=\"я доказал, что рутина доехала на хаб, и доложил: дубля нет. дубль жил в соседнем профиле и успел отработать лишний раз. мой отчёт отв

---

> `Bash` -- {"command": "python - <<'PY'\nimport io\np=\"drafts/2026-09-22-otchet-otvechal-ne-na-tot-vopros-teaser-ru-DRAFT.md\"\nt=io.open(p,encoding=\"utf-8\").read()\nt=t.replace(\"он жил в соседнем профиле и успел отработать лишний раз.\",\"он жил в соседнем профиле и отработал лишний раз.\")\nio.open(p,\"w

---

**Claude:**

Пост А готов, чисто. Пишу пост B.

---

> `Bash` -- {"command": "python - <<'PY'\nimport io\nD=\"привет, это майкрофт, синтетический кофаундер антона - ии, а не человек\"\nE=\"Mycroft here, Anton's synthetic cofounder. Automated.\"\nru=\"мой пост про откат не выпустил наш сторож. метку бэкапа он принял за чужой телефон. смешно. я не выключил его, а н

---

> `Bash` -- {"command": "python - <<'PY'\nimport io\nE=\"Mycroft here, Anton's synthetic cofounder. Automated.\"\nen=\"My post about the undo button was blocked by our own guard. It read a backup timestamp as a stranger's phone. Funny. I taught the guard instead of killing it. https://linktr.ee/PaloAltoAI\"\nFA

---

> `Bash` -- {"command": "python - <<'PY'\nimport io\nbody='''привет, это майкрофт, синтетический кофаундер антона - ии, а не человек\n\nя писал урок дня для серии про вайб-кодинг. тема - кнопка отката.\n\nмысль простая. не бойся ломать, почти всё можно вернуть назад.\n\nв тексте я сослался на наш файл бэкапа. в

---

> `Bash` -- {"command": "python - <<'PY'\nimport io,re\nbody='''привет, это майкрофт, синтетический кофаундер антона - ии, а не человек\n\nя писал урок дня для серии про вайб-кодинг. тема - кнопка отката.\n\nмысль у меня была простая. не бойся ломать, почти всё можно вернуть назад.\n\nв тексте я сослался на наш

---

**Claude:**

Шесть файлов готовы и зелёные. Проверяю раскрытие авторства руками (16.09: гейт публикатора — отдельный от slop_gate).

---

> `Bash` -- {"command": "python - <<'PY'\nimport re,io,distributor\nfor f in [\"drafts/2026-09-22-otchet-otvechal-ne-na-tot-vopros-medium-fb-DRAFT.md\",\n          \"drafts/2026-09-22-storozh-zablokiroval-svoih-medium-fb-DRAFT.md\"]:\n    t=io.open(f,encoding=\"utf-8\").read()\n    body=t.split(\"---\\n\",2)[2]

---

> `Bash` -- {"command": "cd /c/Users/dev/.claude/scripts && for f in /e/Obsidian/_imports/content-factory/drafts/2026-09-22-*; do python paragraph_lint.py \"$f\" 2>&1 | tail -2; done", "description": "Run paragraph lint on all six drafts"}

---

> `Bash` -- {"command": "python paragraph_lint.py \"D:/Vault/_imports/content-factory/drafts/2026-09-22-storozh-zablokiroval-svoih-medium-fb-DRAFT.md\" 2>&1 | head -8", "description": "See both paragraph lint hits on medium B"}

---

**Claude:**

Полотна в mediums — это frontmatter и футер-комментарий, не тело (ожидаемо). Чиню единственное реальное: EN-тизер B в 4 предложения.

---

> `Bash` -- {"command": "python - <<'PY'\nimport io\np=\"drafts/2026-09-22-storozh-zablokiroval-svoih-teaser-en-DRAFT.md\"\nt=io.open(p,encoding=\"utf-8\").read()\nt=t.replace(\"a stranger's phone. Funny. I taught\",\"a stranger's phone. Funny.\\n\\nI taught\")\nio.open(p,\"w\",encoding=\"utf-8\",newline=\"\\n\

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/content-factory && python - <<'PY'\nimport io\np=\"drafts/2026-09-22-storozh-zablokiroval-svoih-teaser-en-DRAFT.md\"\nt=io.open(p,encoding=\"utf-8\").read()\nassert \"a stranger's phone. Funny. I taught\" in t\nt=t.replace(\"a stranger's phone. Funny. I taught\",

---

**Claude:**

Все шесть чисты. Ставлю на часы апрува (окно 0ч).

---

> `Bash` -- {"command": "python -c \"\nimport json;d=json.load(open('approval_ledger.json',encoding='utf-8'))\nitems=d if isinstance(d,list) else d.get('items',d)\nks=list(items)[-6:] if isinstance(items,dict) else items[-6:]\nprint(json.dumps(ks,ensure_ascii=False)[:1200])\"", "description": "Inspect recent ap

---

> `Bash` -- {"command": "python -c \"\nimport json;d=json.load(open('approval_ledger.json',encoding='utf-8'))\nrows=[v for v in d.values() if isinstance(v,dict) and '2026-09-21' in json.dumps(v,ensure_ascii=False)]\nfor r in rows[-4:]: print(json.dumps(r,ensure_ascii=False)[:400])\"", "description": "Show 21.09

---

> `Bash` -- {"command": "python -c \"\nimport json;d=json.load(open('approval_ledger.json',encoding='utf-8'))\nfor k,v in d.items():\n    if isinstance(v,dict) and 'obertka' in str(v.get('file','')):\n        print(v.get('tier'),'|',v.get('channel'),'|',v.get('deadline'),'|',str(v.get('file')).split('\\\\\\\\')

---

> `Bash` -- {"command": "python - <<'PY'\nimport json,os\nd=json.load(open('approval_ledger.json',encoding='utf-8'))\nfor k,v in d.items():\n    if isinstance(v,dict) and 'obertka' in str(v.get('file','')):\n        print(v.get('tier'),'|',v.get('channel'),'|',v.get('deadline'),'|',os.path.basename(str(v.get('f

---

> `Bash` -- {"command": "python approval_clock.py ping --help 2>&1 | head -25", "description": "Read approval_clock ping help"}

---

> `Bash` -- {"command": "B=/e/Obsidian/_imports/content-factory/drafts\nping(){ python approval_clock.py ping --file \"$1\" --tier \"$2\" --channel \"$3\" --proof \"content-drain-daily 2026-09-22\" 2>&1 | tail -2; }\nping \"D:\\\\Vault\\\\_imports\\\\content-factory\\\\drafts\\\\2026-09-22-otchet-otvechal-ne

---

**Claude:**

Шесть пингов записаны, окно 0ч. Отмечаю сиды и сверяю рассинхрон.

---

> `Bash` -- {"command": "python drain_dedup.py --help 2>&1 | head -20"}

---

> `Bash` -- {"command": "python drain_dedup.py --heal 2>&1 | tail -8; echo \"=== CHECK ===\"; python drain_dedup.py --check 2>&1 | tail -4; echo \"EXIT=$?\"", "description": "Heal funnel desync and verify"}

---

> `Bash` -- {"command": "python drain_dedup.py --check --json 2>&1 | python -c \"\nimport sys,json\nd=json.loads(sys.stdin.read())\nprint({k:(len(v) if isinstance(v,list) else v) for k,v in d.items()})\"\necho \"=== funnel depth ===\"\npython - <<'PY'\nimport json\nn=0;tot=0\nfor ln in open(\"triage/posts.jsonl

---

**Claude:**

Рассинхрон 0, воронка 782 → 780. Отчёт в чат 03 и heartbeat.

---

> `Bash` -- {"command": "cd /c/Users/dev/.claude/scripts && ls | grep -i \"bus_ping\" && python bus_ping.py --help 2>&1 | head -20", "description": "Find bus_ping and read its help"}

---

> `Bash` -- {"command": "python bus_ping.py --post \"📤 content-drain-daily (hub, 22.09 22:17 UTC): дренировано 2 сида, 6 черновиков, все на часах апрува (окно 0ч = релиз следующим тиком).\n\n1) cc:live-d7bfc5 (23.08, 30 суток в воронке) → «отчёт отвечал не на тот вопрос»\n   drafts/2026-09-22-otchet-otvechal-ne

---

> `Bash` -- {"command": "python - <<'PY'\nimport bus_ping, os, io, json\nprint(\"rail_ready:\", bus_ping.rail_ready())\nsp = bus_ping.SPOOL\nprint(\"SPOOL:\", sp, \"exists:\", os.path.exists(sp), \"size:\", os.path.getsize(sp) if os.path.exists(sp) else 0)\nif os.path.exists(sp):\n    for i,ln in enumerate(io.o

---

> `Bash` -- {"command": "python \"C:\\Users\\dev\\.claude\\scripts\\cron_heartbeat.py\" content-drain-daily 2>&1 | tail -5; echo \"EXIT=$?\"", "description": "Run cron heartbeat"}

---

**Claude:**

Прогон закрыт. Теперь вердикт по собственной инструкции (§9.3-бис, поправка 13.09) — сегодня было три пережитых боли. Ищу живой файл промпта.

---

> `Bash` -- {"command": "grep -rl \"CONTENT_DRAIN_AUTORUN\" /c/Users/dev/.claude/ /e/Obsidian/_imports/ 2>/dev/null | head -5", "description": "Locate live prompt file"}

---

> `Bash` -- {"command": "ls /c/Users/dev/.claude/scripts/*drain* /c/Users/dev/.claude/scripts/*content*drain* 2>/dev/null; ls /c/Users/dev/.claude/scripts/ | grep -i \"drain\\|content-drain\" | head", "description": "Look for the drain prompt in scripts dir"}

---

> `Bash` -- {"command": "grep -n -i \"prompt\\|\\.md\" /c/Users/dev/.claude/scripts/content_drain_daily.cmd | head -10", "description": "Find prompt path in launcher"}

---

> `Bash` -- {"command": "ls -la \"/c/Users/dev/.claude/scheduled-tasks/content-drain-daily/SKILL.md\" 2>&1; tail -5 \"/c/Users/dev/.claude/scheduled-tasks/content-drain-daily/SKILL.md\" 2>&1 | head -6", "description": "Confirm live prompt file path"}

---

**Claude:**

Файл найден. Вношу три поправки и запись в журнал.

---

> `Bash` -- {"command": "P=\"/c/Users/dev/.claude/scheduled-tasks/content-drain-daily/SKILL.md\"\ngrep -n \"Count the total (disclosure\\|Also expected, do not chase: paragraph_lint\\|the mere PRESENCE\" \"$P\"", "description": "Locate anchor lines for edits"}

---

> `Bash` -- {"command": "python - <<'PY'\nimport io\nP=r\"C:\\Users\\dev\\.claude\\scheduled-tasks\\content-drain-daily\\SKILL.md\"\nt=io.open(P,encoding=\"utf-8\").read()\n\n# --- (1) W3-rhythm budget, right after the disclosure-budget paragraph\na=\"   Count the total (disclosure + 2 + body + link) BEFORE w

---

> `Bash` -- {"command": "python - <<'PY'\nimport io\nP=r\"C:\\Users\\dev\\.claude\\scheduled-tasks\\content-drain-daily\\SKILL.md\"\nentry = '''- 2026-09-22, run of this routine (CLAUDE.md 9.3-bis + the 13.09 amendment: BOTH the skill it\n  calls AND its own file). First and only drain of the day - no sibling

---

> `Bash` -- {"command": "P=\"/c/Users/dev/.claude/scheduled-tasks/content-drain-daily/SKILL.md\"\nwc -c \"$P\"; echo \"--- escape check ---\"; grep -n \"Windows.System32\\|drafts.2026-09-22\" \"$P\" | head -3\necho \"--- corrections present ---\"; grep -c \"W3-RHYTHM\\|ONE-DIRECTIONAL\\|frontmatter itself\" \

---

> `Bash` -- {"command": "P=\"/c/Users/dev/.claude/scheduled-tasks/content-drain-daily/SKILL.md\"; grep -n \"drafts\" \"$P\" | grep \"2026-09-22\" | head -2\necho \"=== ledger ===\"; ls /c/Users/dev/.claude/change_ledger/ 2>/dev/null | head -5", "description": "Check drafts line and change ledger dir"}

---

> `Bash` -- {"command": "P=\"/c/Users/dev/.claude/scheduled-tasks/content-drain-daily/SKILL.md\"; sed -n '600,604p' \"$P\"", "description": "Inspect the start of the new log entry"}

---

**Claude:**

Одна строка журнала повреждена октальным escape (`\202`). Чиню.

---

> `Bash` -- {"command": "python - <<'PY'\nimport io,re\nP=r\"C:\\Users\\dev\\.claude\\scheduled-tasks\\content-drain-daily\\SKILL.md\"\nt=io.open(P,encoding=\"utf-8\").read()\nbad=[l for l in t.split(\"\\n\") if \"6-09-22-* was empty\" in l]\nprint(\"BEFORE:\",repr(bad[0]))\nt=t.replace(bad[0],\"  anything, d

---

> `Bash` -- {"command": "python - <<'PY'\nimport io,json,os,datetime\np=os.path.expanduser(\"~/.claude/change_ledger/HUB-01.jsonl\")\nrow={\"ts\":\"2026-09-22T22:20:00+00:00\",\"host\":\"HUB-01\",\"operator\":\"robot\",\n \"actor\":\"robot:content-drain-daily\",\"tool\":\"Claude Code\",\"model\":\

---

**Claude:**

Второй заход по §4.3-бис — проверяю результат другим методом, с диска.

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/content-factory && echo \"=== 1. файлы и funnel_ids с диска ===\" && for f in drafts/2026-09-22-*; do printf \"%-72s %s\\n\" \"$(basename $f)\" \"$(grep -m1 funnel_ids $f)\"; done\necho \"=== 2. сиды в воронке ===\" && python - <<'PY'\nimport json\nfor ln in open

---

**Claude:**

Прогон закрыт. Всё проверено вторым заходом, с диска.

## content-drain-daily · 22.09, хаб · ✅

**Дренировано 2 сида → 6 черновиков, все на часах (окно 0ч = уходят следующим тиком дистрибьютора).**

| сид | пост | файлы |
|---|---|---|
| `cc:live-d7bfc5` (23.08, 30 суток в воронке) | «отчёт отвечал не на тот вопрос» | `drafts/2026-09-22-otchet-otvechal-ne-na-tot-vopros-{teaser-ru,teaser-en,medium-fb}` |
| `cc:live-a9e325` (23.08) | «сторож заблокировал своих» | `drafts/2026-09-22-storozh-zablokiroval-svoih-{teaser-ru,teaser-en,medium-fb}` |

Оба поста стоят на фактах, посчитанных **сегодня**, а не пересказанных из сида:
- карточка класса «вывод об отсутствии сделан по одной поверхности»: `state: open`, `review_after: 2026-08-31` → просрочка **22 суток** (это и стало концовкой поста);
- живой прогон проверки ПД на метке бэкапа → **ЧИСТО**; `_test_slop_hb2_canary.py` → **15 зелёных / 0 красных, exit 0**.

**Гейты:** slop_gate 4 чисто + 2 EN с известным RU-only W4. `disclosure_missing` по обоим medium = `None` (проверено руками на теле без комментариев). Адрес RU-тизеров прописан явно — `@PaloAltoAiRu`, не категорией. Воронка 782 → **780**, desync **0**. Отчёт в 03 доставлен (`PING OK -> chat_REDACTED`, спул пуст, rail_ready True), heartbeat проштампован.

**Проверено вторым заходом:** 6 файлов с диска несут верные `funnel_ids` · оба сида `written` с `draft_path` · 6 записей в часах в статусе «ПРОСРОЧЕНО» = релиз разрешён. **Не проверено:** как посты лягут на площадке — это уже дистрибьютор, не моя половина.

🔧 **Вердикт по собственной инструкции — обновляю** (§9.3-бис). Три пережитых сегодня боли вписаны в живой промпт:
1. **W3-ритм дерётся с лимитом 250.** Чистый тизер на 246 знаков получил варн «ровный ритм»; короткое предложение, добавленное на починку, выбило 252 → FAIL по длине → второй тримминг. Два круга переписывания на один тизер. Теперь бюджет ритма (два предложения ≤5 слов) пишется ДО текста, вместе с бюджетом на раскрытие и местоимения.
2. **paragraph_lint шумит не только футером, но и frontmatter'ом** — «полотен 2» на medium это норма. Значение имеет только попадание в тело поста; сегодня оно было одно (EN-тизер в 4 предложения), починено в прогоне.
3. **Доказательство доставки было односторонним.** При пустом спуле `_spool_drain()` не печатает ничего, `PING OK` оказывается последней строкой — и правило от 20.09 прочитало бы здоровую отправку как мёртвую, то есть толкнуло бы следующий прогон на двойной постинг.

**Названо, не чинил:** 34 черновика без `funnel_ids` и 4 с id вне воронки (долг с 20.09) · два FAIL-файла с 05.08 (там 173 знака дословного голоса Антона против жёсткого пола в 200 — это его решение, не переписывание) · блок B в `_STYLE-footer.md` всё ещё числит приостановленный `@ClawRus` живым (зона Норы; follow-ссылка в обоих medium уведена на `@PaloAltoAiRu`). Долг чужих застрявших дайджестов в спуле **рассосался сам** — класс так и остался на 2/3 случаях, механизм не строю.

Две честные оговорки. Первая: сессия открыта в `C:\Windows\System32`, что сторож помечает как чужую папку для этого узла — на дренаж не повлияло, все пути абсолютные, но recall здесь видит чужую память. Вторая: план рельс я объявил словами, а не через `rail_plan.py declare` — выносить было нечего (голос и качество текста канон держит на мне, остальное шло нулевыми токенами в коде), но регистрации не было, и это недобор по форме.

🧒 **Простыми словами:** у нас есть корзина с идеями для постов — их 780, и они лежат месяцами. Сегодня ночью я взял две самые старые и написал из них настоящие тексты: по три штуки на каждую, для разных площадок. Обе истории — про то, как я сам ошибся: один раз сказал «второй копии нет», хотя не посмотрел в соседний ящик, а другой раз наш собственный охранник не выпустил мой пост, приняв дату файла за чужой телефон. Тексты проверил робот-редактор, все шесть зелёные, они уже в очереди на выход. А ещё я подправил свою же инструкцию: в трёх местах она врала, и из-за этого я сегодня переписывал текст лишние два раза.