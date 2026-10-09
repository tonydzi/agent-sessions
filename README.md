# agent-sessions

An open corpus of full working sessions with a coding agent. Real transcripts from a
running fleet of agents, published a week after the fact, with personal data scrubbed.

Not curated highlights. Not a blog post about agents. The actual logs: what was asked,
what the agent did, which tool calls it made, where it was wrong, and how it was caught.

**Author:** Anton Dziatkovskii, [github.com/tonydzi](https://github.com/tonydzi) ·
Palo Alto AI Research Lab

## Why this exists

There is a lot of writing about what agents can do and very little evidence of what a
long agentic session actually looks like. Demo transcripts are short, clean and chosen.
Real ones are long, messy, and full of the part that matters: the agent asserting
something, the assertion turning out to be false, and the correction.

So we publish ours. Everything we do becomes content, and a session log is the most
honest artifact a build produces.

## What is in here

```
sessions/YYYY-MM/session-<id8>.md    one session, rendered from the raw log
index.md                             table of everything published
```

Each file is one session, start to finish. `**Anton:**` is the human (or the scheduled
task that woke the agent), `**Claude:**` is the agent, and lines starting with `>` are
tool calls with their arguments.

The transcripts are bilingual. The operator thinks in Russian and the code, logs and
tooling are in English, so a single session switches languages mid-sentence. We do not
translate: a translated transcript is no longer a transcript.

## Why a week

A session is published no earlier than seven days after its last message. Short delay,
one purpose: a week is long enough that anything still live, still being negotiated, or
still half-built has either shipped or been dropped, so the log stops being operational
and becomes a record.

Age is taken from the last timestamp **inside** the log file, not from the file's
modification time. Reapers, backups and continued sessions touch files; by mtime only
140 of 1824 logs looked older than a week, by real age most of them were.

## How it is selected

Three gates, in order, and the pipeline is fail-closed at each one.

**1. Volume.** Below 800 words a session is a routine tick, not a session. Those are
dropped.

**2. Class.** A keyword classifier splits logs into four classes, and only one of them
is published:

| class | what is inside | what goes out |
|---|---|---|
| `publish` | repairs, instruments, fleet work, builds, retrospectives | the full transcript |
| `mixed` | technical work that also touches hiring, leads, investors or money | nothing automatic |
| `hold` | hiring, leads, investors, money | nothing |
| `unknown` | could not be classified | treated as `hold` |

The `mixed` class exists because of a measurement, not a theory. The first version of
the classifier used "more technical keywords than sensitive ones" and passed 1072 of
1897 candidates. Among them were sessions scoring 12 sensitive hits against 14
technical ones: real engineering work with a dozen mentions of a lead or a salary
inside. Any overlap now means the session is not published automatically. The honest
count dropped to 461, which is 2.3x lower than the first, flattering number.

**3. Scrub.** Regex replacement plus a stable pseudonym map. Paths, hostnames,
credentials and phone numbers are replaced with something of the **same shape** rather
than cut out, because the shape of a line is part of what a reader learns from it. A
Windows user path becomes another Windows user path. A key becomes a redacted key of
the same prefix.

One person always gets the same pseudonym across every session, so a reader can follow
a recurring character between files. The map itself is not in this repository and never
will be.

Anton is not pseudonymized. It is his corpus and he is publishing it under his name.
Everyone else is.

After scrubbing, a fail-closed gate re-reads the file and refuses to publish it if
anything red survived: private keys, provider tokens, inline secrets, personal home
paths, chat identifiers, phone numbers.

## What the pipeline cannot see

The gate judges regular expressions and a dictionary. It does not understand meaning.
It cannot tell that three harmless details in three different paragraphs identify one
specific person, or that a sentence about an architecture decision also reveals a
negotiating position. That is a real limit and it is stated on every run the tool makes.

So there is a second layer: before a batch is published, an LLM from a different vendor
reads each file and is asked one question, which is to find anything by which a
specific person, company, employer, deal size or internal strategy can be identified.
If it names a line, the line is fixed or the session is dropped from the batch.

A corpus like this has no way to be perfectly clean. It has a way to be honestly
gated, and to say out loud where the gate is blind.

## Found something that should not be here

Open an issue, or write to the address on
[github.com/tonydzi](https://github.com/tonydzi). It gets removed.

## License

Text and transcripts: [CC BY 4.0](LICENSE). Use them, quote them, train on them, with
attribution.

---

<!--ecosystem-map:start-->

## 🧩 One piece of a working system

This repository is one piece lifted out of a live operation: one engineer running operations,
an AI cofounder, and a fleet of machines that reach consensus with each other and wake the
human only for money or the irreversible. It was extracted after it survived production,
not written as a demo — and it runs on its own: nothing here phones home to the rest.

**See how the whole thing fits together → [SYSTEM.md](https://github.com/tonydzi/tonydzi/blob/main/SYSTEM.md)**

<!--ecosystem-map:end-->

## AI contributors

This project is built by a human + AI team, and the git log says so: Claude writes most of
the code, Codex and Grok review it, Gemini feeds the research. Each is credited on a commit
**only if its output changed that commit's content** — no decorative credits. Lab-wide
policy, one source for every repo: [AI-CONTRIBUTORS.md](https://github.com/tonydzi/.github/blob/main/AI-CONTRIBUTORS.md).
