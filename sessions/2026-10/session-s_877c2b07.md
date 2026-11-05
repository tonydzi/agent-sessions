---
session: s_877c2b07
date: 2026-10-27
words: 568
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-10-27 · Judge the three anonymous English X candidates below. Author is Mycroft, an AI cofounder…

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_877c2b07` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

Judge the three anonymous English X candidates below. Author is Mycroft, an AI cofounder, explicitly NOT the human and not an imitation of human voice. Audience business people switching between AI assistants. Select one (or reject all), score human/readability and facts 1-5 and explain briefly. Publish threshold human>=4 and facts>=4 with no invented fact. No sale/CTA is allowed. Do not write or post files.

Verified facts: one shared project folder, linked common instruction/skill physical sources for three AI coding clients. Only Codex completed a bounded real 8-question and common-probe task. This is not all tools parity, not all six skills executed. Cursor and Claude are not yet accepted. Their current quota/auth state was not measured in today's retrospective. No private details needed. Grok generation was attempted through the subscription broker and timed out at120seconds; fallback candidates are authored by Codex, declared here for provenance but candidates have no separate author labels.

A: I'm Mycroft, an AI cofounder. I gave three AI assistants the same working folder. Sharing files was the easy part. Only Codex has finished a real task so far. Cursor and Claude still need a proper test

B: I'm Mycroft, an AI cofounder. I set up one folder for three AI assistants. The files line up. The results don't yet. Codex has finished a real task; Cursor and Claude still need to prove they can use the same setup

C: I'm Mycroft, an AI cofounder. I prepared shared files and instructions to make switching AI assistants easier. Only Codex has finished a real task so far. Cursor and Claude still need to prove it on real work

---

**Claude:**

**Вердикт: публиковать A.** B запасной, C отклонить.

| | human/читаемость | facts | комментарий |
|---|---|---|---|
| **A** | 4 | 4 | Каждое утверждение есть в списке проверенных фактов: одна папка, три ассистента, только Codex прошёл реальную задачу, Cursor и Claude не приняты. «Sharing files was the easy part» это оценка, а не факт. Она безобидна и честно задаёт рамку: сложная часть впереди. |
| **B** | 4 | 3 | Лучше всего звучит («The files line up. The results don't yet»). Но «results don't yet» утверждает, что результаты расходятся. Измерено другое: у Cursor и Claude результатов просто нет. Это тихий выдуманный факт, поэтому порог не пройден. |
| **C** | 3 | 3 | Самый вялый и самый шаблонный. «To make switching easier» приписывает пользу, которой никто не мерил. Число «три» пропало, а оно и есть суть. |

**Что учесть при публикации A:**
- «a real task» не говорит, что задача была ограниченная (8 вопросов и общая проба). Это не ложь, но если хватит места (сейчас около 215 символов), лучше «a small real task» или «a bounded real task».
- В конце нет точки. Для X это нормально.
- Ни в одном варианте нет продажи или CTA, это ок.
- По происхождению: Grok упал по таймауту на 120 секундах, все три кандидата написал Codex-фолбэк. Для провенанса это стоит указать при записи.

Если A не нравится по тону, B можно спасти заменой второй фразы на «The results aren't proven yet». Тогда facts станет 4.

🧒 **Простыми словами**
Мы поставили три помощника за один общий стол. Работу по-настоящему сдал пока только один. Вариант A говорит ровно это и ничего лишнего. B звучит красивее, но намекает, что у остальных «не получилось», а мы просто ещё не проверяли. C скучный и обещает «станет проще», чего мы не знаем.
