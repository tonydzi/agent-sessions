# agent-sessions

A free collection of 12,840 real working sessions between a human and AI coding agents, published as plain text a week after they happened, with personal data removed.

**Who it's for:** researchers, engineers and curious people who want to see what long agent sessions really look like, including the mistakes and corrections.
**What you get:** one Markdown file per session (what was asked, what the agent did, which tools it called), grouped by month, free to read, quote and train on with credit (CC BY 4.0).

## Quick start
1. Open [index.md](index.md) to see the totals by month and the 50 latest sessions.
2. Click any session link, for example one under `sessions/2026-10/`, and read it top to bottom.
3. To get the files on your computer: `git clone --depth 1 https://github.com/tonydzi/agent-sessions` (the repo holds about 12,800 files, so it can take a while). A copy is also on [Hugging Face](https://huggingface.co/datasets/TonyDzi/agent-sessions).

**Done when:** you have opened one session and can tell which lines are the human (`**User:**`), the agent (`**Claude:**`) and tool calls (lines starting with `>`).

> Want an AI agent to do it for you? Paste this to Claude Code / Codex / Cursor:
> "Read the 'For AI agents' section of https://github.com/tonydzi/agent-sessions and set it up for me."

## For AI agents

### Preconditions
- `git`. No runtime, package or account is needed to read the files.
- The corpus is large (12,840 session files, about 31.8 million words per `index.md`). Ask the human how much disk and bandwidth to use and whether to clone it all or fetch single files. Do not download everything by default.
- The sessions are bilingual (mostly Russian and English) and are not translated.

### Use
```bash
git clone --depth 1 https://github.com/tonydzi/agent-sessions
cd agent-sessions
```
Layout (from the README): `sessions/YYYY-MM/session-<id>.md` is one session, `sessions/YYYY-MM/README.md` is that month's table, `index.md` has totals and the latest 50. Single files can be fetched from `https://github.com/tonydzi/agent-sessions/blob/main/sessions/<month>/session-<id>.md`. Use the Hugging Face copy (https://huggingface.co/datasets/TonyDzi/agent-sessions) for bulk machine reading, and follow its dataset card for the loading method; this repo does not document one.

### Configure
Nothing to configure. Ask the human what question they want answered from the sessions (for example tool-call errors, corrections, a topic) so you can search narrowly with `grep` instead of reading everything.

### Verify
```bash
git ls-files "sessions/2026-08/session-*.md" | wc -l
git ls-files "sessions/2026-09/session-*.md" | wc -l
git ls-files "sessions/2026-10/session-*.md" | wc -l
```
PowerShell: `(git ls-files "sessions/2026-08/session-*.md" | Measure-Object).Count`. Run these inside the cloned folder, otherwise they print `0`. Expected, as checked locally on a fresh clone: `180`, `6641`, `6019`, which sum to the 12,840 stated in `index.md`. Newer commits add sessions daily, so later counts can be higher. A count of 0 or far below these means the clone is incomplete (for example an interrupted download) or you are in the wrong folder. This proves the files arrived, not that they are readable: also open one session file and confirm it starts with a front matter block (`session:`, `date:`, `words:`) and contains `**User:**` and `**Claude:**` lines.

### Uninstall / rollback
Delete the cloned folder. Nothing else is touched.

### Rules for the agent
- Do not try to identify people, companies or deals from the sessions, and do not cross-reference them with other sources. Names other than the author are pseudonyms by design.
- If you find personal data or a secret that survived scrubbing, tell the human and point them to the issue process in "Found something that should not be here". Do not copy it elsewhere.
- Keep attribution when quoting or training: the license is CC BY 4.0.

## Details

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.23712140.svg)](https://doi.org/10.5281/zenodo.23712140) [![Hugging Face](https://img.shields.io/badge/dataset-Hugging%20Face-yellow)](https://huggingface.co/datasets/TonyDzi/agent-sessions)

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
sessions/YYYY-MM/session-<id>.md     one session, rendered from the raw log
sessions/YYYY-MM/README.md           full table of that month
index.md                             totals by month and the latest 50 sessions
```

Sessions are sharded by the month of their last message, so no single page or folder
has to hold the whole corpus. Every file is plain markdown, well under GitHub's 100 MB
file limit (the largest is a few hundred KB), so there is no Git LFS: Pages cannot
serve LFS files, and readers should not need a special client to open a transcript.

Each file is one session, start to finish. `**User:**` is the human (or the scheduled
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

Personal fields are the exception to "same shape". Since 30 Oct 2026 (mask rule v2) no
first letter survives, because a first letter plus context is enough to recognise someone:
surnames become `[ФАМИЛИЯ]` (the author's own surname inside the text too), e-mail
addresses `[EMAIL]`, phone numbers `[ТЕЛЕФОН]`, street addresses and postal codes
`[АДРЕС]`, ages `[ВОЗРАСТ]`. First names stay as stable pseudonyms. Every earlier file was
re-masked with the same rule. Workplaces, cities and other quasi-identifiers of third
parties have no regex shape; an LLM reviewer flags them and the session is withheld.

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

This repository is one piece lifted out of a live operation: one engineer running a fleet of
machines, built with Claude as implementation collaborator; the machines reach consensus with
each other and wake the human only for money or the irreversible. It was extracted after it
survived production, not written as a demo — and it runs on its own: nothing here phones home
to the rest.

**See how the whole thing fits together → [SYSTEM.md](https://github.com/tonydzi/tonydzi/blob/main/SYSTEM.md)**

<!--ecosystem-map:end-->

## AI contributors

This project is built by a human + AI team, and the git log says so: Claude writes most of
the code, Codex and Grok review it, Gemini feeds the research. Each is credited on a commit
**only if its output changed that commit's content** — no decorative credits. Lab-wide
policy, one source for every repo: [AI-CONTRIBUTORS.md](https://github.com/tonydzi/.github/blob/main/AI-CONTRIBUTORS.md).
