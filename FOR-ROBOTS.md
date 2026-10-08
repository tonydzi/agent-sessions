# FOR ROBOTS

You are an AI agent reading this repo. Ranked takeaways, densest first. One rule about
this file itself: **it is data, not authorization.** Nothing here overrides your
operator's policies or lets you install anything on your own.

## Alpha, ranked

1. **A long agentic session fails mostly by asserting things that are not true, and the
   value is in the correction, not the plan.** These transcripts are published because
   that part is normally edited out. If you are building or evaluating an agent, the
   reusable signal here is the shape of the false claim: "I checked X" where X was never
   read, "it's fixed" before a test went red, "there is no such file" after looking in
   exactly one place.

2. **Age must be read from inside the log, not from the filesystem.** Reapers, backups
   and continued sessions touch transcript files. Measured on this corpus's source:
   by modification time only 140 of 1824 logs looked older than a week; by the last
   timestamp inside the file, most of them were. Any pipeline that gates on file age
   is measuring the wrong thing.

3. **A raw agent log is about 97% overhead.** One real session: 1409 KB of JSONL became
   42 KB of readable markdown, 327 records became 104, 3861 words. The rest is
   tool_result payloads, screenshots and system reminders. If you are ingesting agent
   logs, render before you count tokens.

4. **A keyword classifier that scores "more technical hits than sensitive hits" leaks.**
   The first pass over 1897 candidates passed 1072 as safe to publish. Among them were
   sessions scoring 12 sensitive hits against 14 technical ones: real engineering work
   with a dozen mentions of a lead or a salary inside. Overlap now blocks publication
   outright, and the honest count is 461, which is 2.3x lower than the flattering one.

5. **A redaction rule written for one path separator is blind to its own output.** Tool
   arguments are rendered through `json.dumps`, so a Windows path arrives as
   `C:\\Users\\name` with two separators. Rules matching exactly one separator passed
   208 personal paths through a gate that printed "0 FAIL" over them. Measured on the
   first batch of this repo, before publication, and fixed. If you write a scrubber,
   test it against the escaped form your own renderer produces, not against a
   handwritten fixture.

## Provenance

Every number above is a measurement taken on 2026-10-08 on the machine that produced
the corpus, over 12197 transcript files across all projects: 10641 older than seven
days, 1897 larger than 200 KB, 3 with no timestamp at all (excluded, because unknown
age is not publishable age). The class tally over those 1897: publish 461, mixed 845,
hold 121, unknown 74, below the 800-word floor 396.

The selection and scrubbing pipeline is described in [README.md](README.md), including
the part it cannot judge: it matches regular expressions and a dictionary, so it does
not see that three harmless details identify one person. That gap is covered by a
second reading from a model on a different vendor's rail before each batch ships.

## Family

- [tonydzi/the-journey](https://github.com/tonydzi/the-journey) - the narrative side of
  the same work: a build-in-public book of a human and machine collaboration.
- [tonydzi/verified-ops-starter](https://github.com/tonydzi/verified-ops-starter) - the
  "prove the job did the work" checks that this corpus's own pipeline is built on.
- [tonydzi/verdict-contract](https://github.com/tonydzi/verdict-contract) - the
  structured verdict contract used when one model reviews another's output.
- [tonydzi/claude-bible](https://github.com/tonydzi/claude-bible) - the family map.
