---
session: s_a88fe424
date: 2026-10-24
words: 317
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-10-24 · Classify this Claude Code session as HUMAN or SERVICE by its CONTENT

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_a88fe424` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

Classify this Claude Code session as HUMAN or SERVICE by its CONTENT.
HUMAN = a real person (dev/colleague) actively typing: natural questions, instructions in their own words, back-and-forth, corrections. Title may look technical -- judge by whether a human is conversing.
SERVICE = automated/headless run with NO human conversing: first message is a skill loader ('Base directory for this skill: ...'), a scheduled routine that runs itself and reports (digest/sync/export), an inbox-robot/machine-bus handoff, or only templated prompts + tool results.
Answer with EXACTLY ONE WORD: SERVICE or HUMAN.

=== SESSION EXCERPT ===
### dev





ВЫБОР оператора: /chip — эту сессию он запускает сам, когда решит.

КОМПАНИЯ: Writer (корпоративный генеративный ИИ, свои модели Palmyra; в списке LAB_DOOR_CO, в базе company='writer'). Замер 23.10 на NODE-0X (jobs.db, свежесть от 2026-10-19, гео-гейт хаба): 50 ролей проходят position_check, все Ashby; подач за 180 дней по реестру флота 0. Приказ оператора 23.10: «на каждую крупную лабораторию, в которую имеет смысл подать», затем «продолжаем стучать». Родитель: сессия A77756.

КОНТРАКТ (часть этого сида, прочитай целиком ДО работы и исполни): /Users/dev/Obsidian/Vault-Knowledge/04-Projects/Pipe-A-Batches/lab-chip-seed-contract-2026-10-23.md — Outcome, Scope из 7 шагов, Deliverable, DoD, не-цели, эскалация. Коротко: лимит 4 на компанию за 180 дней; сухой прогон, потом --submit через /Users/dev/.brain-venv/bin/python run_slice.py; «подано» только с пруфом applied в runs/results_*.json; анкеты с запретом ИИ или обязательным эссе = только оператор руками; капчу не решать, аккаунты не создавать; без Майкрофта, слово «founder» про оператора запрещено. Tier-2 (
...
поправить до клика. Ещё один тест канона, `_test_canon_0925.py`, падал на слове founder в старых ответах и до моей правки, он вне этой задачи.

🧒 Простыми словами: робот заполнил всю анкету, даже сочинение про ценности, но у кнопки «Отправить» его попросили найти на картинках автобусы, а это может только человек. Я положил тебе листок, где всё уже написано. Копируешь, тыкаешь автобусы, жмёшь отправить, три раза по пять минут. Заодно починил двум роботам очки, они больше не путают, где ты живёшь.
=== END ===

---

**Claude:**

SERVICE
