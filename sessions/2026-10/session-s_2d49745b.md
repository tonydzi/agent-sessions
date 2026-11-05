---
session: s_2d49745b
date: 2026-10-18
words: 2805
turns: 14
tools: "Agent, Bash, Read, Write"
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-10-18 · После того, как мы познакомились с кучей ребят с салона Карак Контерсона, и потом в пятниц…

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_2d49745b` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

После того, как мы познакомились с кучей ребят с салона Карак Контерсона, и потом в пятницу, им стоит всем в Signal написать сообщение, и то же самое сообщение про Twitter, там, бла-бла-бла, рация, там, познакомиться, пересечься и так далее. И каждому из них, учитывая то, что мы видим, что они пишут в Signal, в Twitter, на GitHub, можно что-то написать еще такое личное, типа вот посмотрел бы вот я GitHub, у тебя где-то или ты делаешь гитхаб, мне интересно, что ты делаешь. Нам нужно каждому из них отправить по одному сообщению, по одной пользе. У нас же было где-то правило, перед тем, как мы какого-то попросить, мы должны дать ему пользу. В идеале дать ему три пользы. В любом случае нам нужно каждому из них дать хотя бы одну пользу. Лучше дать три пользы. И только после трех польз мы чего-то просим. Сейчас пока, чтобы контакты не протухли, Нам нужно дать по одному сообщению в Твиттере сигналы. Но нам нужно склеить то, что мы знаем про них, что они уже делают. То, что мы узнали про них, что они говорили голосом на тех этапах. Плюс то, что они строят у себя на Гитхабе. И то, о чем они говорят в Твиттере. Каждый книг написать по сообщению в твиттере плюс сигнал. Сообщения должны быть короткие по делу, по существу и человеческие. Пока тебе задача изучать всех этих лидов, по ним все это склеивать. и написать мне, в общем, 50 черняков. Там, окей, там не было, может, 50 человек, но 20, точно, скорее всего, 20-30. Значит, по всем видам написать им сообщение, ну и попробовать идентифицировать, идентифицировать предвидов.

---

**Claude:**

Начинаю с RECALL: ищу, что это был за салон, кто там был и что о них уже лежит в волте, CRM и записях.

---

> `Bash` -- {"command": "cd \"D:/Vault/Vault-Knowledge\"; date; python \"D:/Vault/_imports/brain_ask.py\" \"салон пятница знакомства Signal Twitter\" 2>&1 | head -40; echo ---; grep -rli -E \"салон|salon\" --include=*.md . 2>/dev/null | xargs ls -t 2>/dev/null | head -30", "description": "Recall vault for

---

> `Read` -- {"file_path": "C:\\Users\\dev\\.claude\\projects\\P---WORKDIR-HUB\\memory\\three-gifts-before-an-ask.md"}

---

> `Bash` -- {"command": "cd \"D:/Vault/Vault-Knowledge\"; find . -name \"*.md\" -newermt \"2026-10-14\" -not -path \"./.obsidian/*\" 2>/dev/null | xargs grep -li -E \"salon|салон|signal|kontersen|konterson|carrick|karak|контерсон\" 2>/dev/null | head -40", "description": "Find recent vault notes mentioning s

---

**Claude:**

"character-salon" ретро 09.10. Читаю его и результат brain_ask.

---

> `Bash` -- {"command": "cd \"D:/Vault/Vault-Knowledge\"; cat \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_2d49745b/tasks/bpu03le8q.output\" | head -60; echo ======; cat \"01-Conversations/Claude/Retros/retro-2026-10-09-character-salon-people-and-diariza

---

**Claude:**

Это салон Character Design (08.10, SF) плюс пятница. Читаю решение 16.10, заметку вечера и Signal-группу.

---

> `Bash` -- {"command": "cd \"D:/Vault/Vault-Knowledge\"; cat \"02-Decisions/_Inbox/2026-10-16--poisk-github-x-kontaktov-s-salona-sf-08-09-10-pr-v-proekty.md\" | head -120; echo =====; find . -iname \"*character-underground*\" -not -path \"./.obsidian/*\" 2>/dev/null; echo ====; grep -rl \"\\[signal\\]-crm\"

---

**Claude:**

Таблица на 64 человека уже есть. Читаю её и Signal-чат.

---

> `Bash` -- {"command": "cd \"D:/Vault/Vault-Knowledge\"; wc -c \"03-Insights/insight-2026-10-16-sf-salon-people-x-github-pr-targets.md\" \"01-Conversations/Signal/2026-10-12-signal-character-underground.md\"; cat \"03-Insights/insight-2026-10-16-sf-salon-people-x-github-pr-targets.md\"", "description": "Rea

---

> `Bash` -- {"command": "cd \"D:/Vault/Vault-Knowledge\"; cat \"01-Conversations/Signal/2026-10-12-signal-character-underground.md\"; echo ====; sed -n 1,80p \"02-Decisions/_Inbox/2026-10-14--crm-analiz-signal-chata-character-underground-persony-ssylki-i-investo.md\"", "description": "Read Signal group note 

---

**Claude:**

Карточек 64, плюс Signal-участники. Смотрю объём карточек и прошлые касания, чтобы не писать тем, кому уже писали.

---

> `Bash` -- {"command": "cd \"D:/Vault/Vault-Knowledge/07-People\"; grep -o \"\\[\\[person-[a-z0-9-]*\" \"../03-Insights/insight-2026-10-16-sf-salon-people-x-github-pr-targets.md\" | sed 's/\\[\\[//' | sort -u > /tmp/salon_slugs.txt; echo person-yatharth-askyatharth >> /tmp/salon_slugs.txt; wc -l < /tmp/salo

---

> `Bash` -- {"command": "cd \"D:/Vault/Vault-Knowledge/07-People\"; cat person-felix-binder.md | head -120; ls ../../../Obsidian/Vault-Knowledge/04-Projects/plaud-recordings/ 2>/dev/null | grep -i -E \"2026-10-0[89]|2026-10-1\" ", "description": "Inspect a sample person card"}

---

> `Bash` -- {"command": "cd \"D:/Vault/Vault-Knowledge/07-People\"; SP=\"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_2d49745b/scratchpad\"; mkdir -p \"$SP/leads\"; sort -u /tmp/salon_slugs.txt > \"$SP/leads/all.txt\"; split -n l/3 -d \"$SP/leads/all.txt\"

---

> `Agent` -- {"description": "Lead facts batch 00", "subagent_type": "general-purpose", "model": "sonnet", "prompt": "You are collecting facts for personalized outreach drafts. READ-ONLY task: never send messages, never post, never comment on GitHub, never edit vault files. Write only to the output file named be

---

> `Agent` -- {"description": "Lead facts batch 01", "subagent_type": "general-purpose", "model": "sonnet", "prompt": "You are collecting facts for personalized outreach drafts. READ-ONLY task: never send messages, never post, never comment on GitHub, never edit vault files. Write only to the output file named be

---

> `Agent` -- {"description": "Lead facts batch 02", "subagent_type": "general-purpose", "model": "sonnet", "prompt": "You are collecting facts for personalized outreach drafts. READ-ONLY task: never send messages, never post, never comment on GitHub, never edit vault files. Write only to the output file named be

---

> `Bash` -- {"command": "cd \"D:/Vault/Vault-Knowledge\"; grep -rl -i \"vie mccoy\\|viemccoy\" --include=*.md 01-Conversations/Claude 02-Decisions 04-Projects 2>/dev/null | xargs ls -t 2>/dev/null | head -8; grep -n -i -A12 \"Касание\\|draft\\|черновик\" 07-People/person-v-openai-red-team.md | head -60", "de

---

> `Bash` -- {"command": "cd \"D:/Vault/Vault-Knowledge\"; wc -c 04-Projects/2026-10-09-viechat-vivarium-guests.md; sed -n 1,200p 04-Projects/2026-10-09-viechat-vivarium-guests.md | cut -c1-300", "description": "Read Vivarium guests list"}

---

> `Bash` -- {"command": "cd \"D:/Vault/Vault-Knowledge/07-People\"; for f in \"Anna Mikeda\" person-rachel-chaotictransfem person-celeste-vmfunc person-rowan-rogesterone person-jazear-brooks; do p=$(find . -name \"$f.md\" | head -1); echo \"######## $p\"; sed -e '/^Machine:/d' \"$p\" | grep -v \"^$\" | cut -

---

> `Bash` -- {"command": "cd \"D:/Vault/Vault-Knowledge/07-People\"; sed -e '/^Machine:/d' person-luka-vivarium.md | grep -v \"^$\" | cut -c1-350 | head -40; cd \"E:/!CLAUDE-HUBPC-June26\"; gh pr view 2 -R lukalotl/polyp.observer --json state,comments,reviews -q '{s:.state,c:[.comments[].body[0:200]]}' 2

---

> `Bash` -- {"command": "ls \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_2d49745b/scratchpad/leads/\"; sed -n 1,60p \"C:/Users/dev/.claude/projects/P---WORKDIR-HUB/memory/dev-voice-profile-pointer.md\" | cut -c1-400", "description": "Check 

---

> `Bash` -- {"command": "grep -n -i -A3 \"english\\|англ\\|en:\" \"D:/Vault/Vault-Knowledge/06-Concepts/concept-dev-voice-profile.md\" | head -60", "description": "Read English part of dev voice profile"}

---

> `Bash` -- {"command": "wc -c \"D:/Vault/Vault-Knowledge/06-Concepts/concept-dev-voice-profile.md\"; grep -v \"^$\" \"D:/Vault/Vault-Knowledge/06-Concepts/concept-dev-voice-profile.md\" | sed -n 10,70p | cut -c1-300", "description": "Skim dev voice profile"}

---

**Claude:**

Статус: голос оператора для коротких сообщений взял из профиля (имя в первой строке, строчными, коротко, один вопрос в конце). Жду три пачки фактов от субагентов, потом сам пишу черновики.

---

**User:**

<task-notification>
<task-id>a7dff6a8b84259c6a</task-id>
<tool-use-id>toolu_01DLWc7pF4LYvgReGfu6vUWZ</tool-use-id>
<output-file>C:\Users\dev\AppData\Local\Temp\claude\P---WORKDIR-HUB\s_2d49745b\tasks\a7dff6a8b84259c6a.output</output-file>
<status>completed</status>
<summary>Agent "Lead facts batch 02" finished</summary>
<note>A task-notification fires each time this agent stops with no live background children of its own. The user can send it another message and resume it, so the same task-id may notify more than once.</note>
<result>The facts file is written for all 21 slugs in batch_02: `C:\Users\dev\AppData\Local\Temp\claude\P---WORKDIR-HUB\s_2d49745b\scratchpad\leads\facts_02.json`. Nothing was sent, posted or commented, and the vault was not edited. `worth_messaging` is stored as an object `{value, reason}`, not a bare true/false.

- **Counts:** `signal=true` for 8 people (Celeste/Computer-10, Vie McCoy, Uzay Girit, Will DePue, Yatharth, Shubham Chandel, Clément Dumas, Tim Kostolansky). Tim's is only a heart reaction on your salon photos, and the "tim" in Signal is matched to him by first name only. 10 have `github_now` (the 8 above minus Yatharth and Uzay, plus Rahul Tarak, Rahul Chhabra, Sinclair Chen and Ziqian Zhong). 10 are marked `worth_messaging=true`; the other 11 are bare Partiful RSVPs with nothing beyond a display name. Rune Kvist is false because he belongs to the AIUC interview rail.
- **Prior touch, Clément Dumas (Butanium):** your PR https://github.com/science-of-finetuning/diffing-toolkit/pull/87 ("Fix missing layer norms after re-running ADL on a new layer, and raise a clear error") was merged by him on 16.10 with the comment "Thank you!". This is the best zero-ask hook in the batch. The old "Truthful AI researcher from France" card is now confirmed as Clément Dumas, from his Signal sender name and the X screenshot.
- **Rahul Tarak:** you have a local clone of his repo CryogenicPlanet/chirp (an agent message board) at `_oss\chirp`, but no issue or PR from you there. Your open PR https://github.com/ComposioHQ/composio/pull/4938 is in his employer's repo, not his personal one. His Partiful RSVP was "maybe", so don't claim you met.
- **Rune Kvist:** AIUC co-founder and interviewer, with an intro call booked for 12.10 12:00 PT. Keep him out of this outreach batch and check the interview debrief first.
- **Cautions:**
  - Celeste's "Philip" in the Plaud transcript is likely a speech-recognition error.
  - Speaker attribution in Plaud is unreliable, so every voice hook is marked with its confidence.
  - Vie McCoy is a senior OpenAI person who gets many DMs, so keep contact short with no ask.
  - Will DePue's employer is unconfirmed.
  - Samuel Hammond's identity is not established.</result>
<usage><subagent_tokens>205648</subagent_tokens><tool_uses>31</tool_uses><duration_ms>470844</duration_ms></usage>
</task-notification>

---

**Claude:**

Первая пачка готова (21 человек, 10 стоят сообщения). Жду две оставшиеся.

---

**User:**

<task-notification>
<task-id>aa0d9988973bf7822</task-id>
<tool-use-id>toolu_01JDMBK1qPZXFY1skoWmuVvu</tool-use-id>
<output-file>C:\Users\dev\AppData\Local\Temp\claude\P---WORKDIR-HUB\s_2d49745b\tasks\aa0d9988973bf7822.output</output-file>
<status>completed</status>
<summary>Agent "Lead facts batch 00" finished</summary>
<note>This agent stopped with background work of its own still running. It may resume on its own when that work completes or reports, and the same task-id notifies again if it does; the result below may be interim.</note>
<result>I wrote `facts_00.json` with 21 person objects; the batch is mostly thin, because 10 of the 21 cards are Partiful-list entries with nothing known about them. The file is `C:\Users\dev\AppData\Local\Temp\claude\P---WORKDIR-HUB\s_2d49745b\scratchpad\leads\facts_00.json`.

1. **Counts:** 21 people. `signal` is true for 6: Antra, Arthur, Asterism, Caithrin, clu and Felix. `github_now` is filled for 7: Andrew Blinn, Antra, Dünya, Carolyn Zou (stale, last push 2025-12), Christina Lu (stale, last push 2026-04), Felix (stale, last push 2024-12) and Arthur (org only, no personal handle).
2. **Prior touches:** Antra's org already has two of our PRs. `anima-research/connectome-host#283` was merged on 17.10 by the maintainer nissa-seru. `anima-research/agent-framework#402` (BOM in gate.json) is still open; nissa-seru wrote "the fix is right" and asked for two small changes, which we pushed as 9a4178f on 16.10. Antra herself has not reacted that I can see. We also followed Andrew Blinn on X and GitHub on 09.10.
3. **Open promises:** Arthur's public request for DMs with speaker ideas and event feedback is the cheapest zero-ask gift. Felix's "Will you send that to me?" (232:36) is unresolved, and the content is unknown.
4. **worth_messaging true (7):** Andrew Blinn, dev Balitskyi, Antra, Arthur, Dünya, Christina Lu and Felix. Christina Lu (Anthropic) and Felix (Meta Superintelligence Labs) are flagged as senior lab staff, so go gently.
5. **worth_messaging false (14):** the Partiful-only guests, Asterism and clu (Signal handles only), Drew and Char (first names only), Caithrin and Carolyn Zou. dev Balitskyi's X account says "Founding Designer @opalapp", which may not be the same person you met, so the card says to reconcile that before messaging.

I found the Signal export under `D:\Vault\_originals\signal\character-underground\`, not under `Vault-Knowledge`. The Partiful-only guests did not appear in any of the three transcripts, so their `voice_hooks` are empty.</result>
<usage><subagent_tokens>207468</subagent_tokens><tool_uses>25</tool_uses><duration_ms>508518</duration_ms></usage>
</task-notification>

---

**Claude:**

Вторая пачка готова (7 стоят сообщения). Жду последнюю.

---

**User:**

<task-notification>
<task-id>ae4f739c3fafbb960</task-id>
<tool-use-id>toolu_01NiQQWE7xxk4zpDjiLbF7mT</tool-use-id>
<output-file>C:\Users\dev\AppData\Local\Temp\claude\P---WORKDIR-HUB\s_2d49745b\tasks\ae4f739c3fafbb960.output</output-file>
<status>completed</status>
<summary>Agent "Lead facts batch 01" finished</summary>
<note>A task-notification fires each time this agent stops with no live background children of its own. The user can send it another message and resume it, so the same task-id may notify more than once.</note>
<result>I wrote `facts_01.json` with 23 entries, one per slug in `batch_01`. The JSON parses cleanly. I did not send or post anything.

- **Counts:** 7 have `signal` true: gwern, Luxia, Mc S, Jan Kulveit, Nick Levine, Larissa, and Glenn Matlin (his only trace is a heart reaction to dev's photos). 12 have `github_now`, but only about 8 of those show activity in the last month. 11 are marked `worth_messaging` true.
- **Louis Arge:** he wrote `claude-peers-mcp` (2,206 stars), which lets Claude Code instances message each other, like our bus. It has 65 open issues, many about Windows and lost messages, and the last push was 26 April. A 16.10 session wrongly called his repos weak targets. Because the queue looks stale, the entry suggests commenting on an existing issue with evidence from our fleet, not a cold PR.
- **Prior touches:** nothing was ever sent to anyone in this batch.
  - Gwern: dev's X follow request is still pending, and the plan to ask him for the Matt Mandel intro was never carried out. The entry says to give him something first and keep the intro for later.
  - Oscar Moxon: the two Prime Intellect PRs (prime-rl #3936 and #3937) were planned on 16.10 but not opened.
  - Glenn Matlin, Hunter Glenn, Louis Arge, Jack blue: dev looked at or followed their X profiles.
- **Time-sensitive:** Jan Kulveit's draft intro to LLM psychology is open for comments, and he plans to publish this week. Commenting before then is the cheapest real gift in the batch.
- **Caveats:**
  - Most Vivarium guests (Jacob Ajit, Kate Thoreson, Lisa Soder, Matthew Dowd, Max Poppers, Luke Drago, Mian Irtiza Aftab, Joe Krisciunas, Horvat Smith) are known only from Partiful RSVPs. Nothing shows dev met them, so I marked them false or low confidence. Matthew Dowd, Joe Krisciunas and Mian Irtiza Aftab had also dropped off the guest list by 10.10.
  - Voice-hook speaker labels in the Plaud transcripts are shared across people. Only Glenn's introduction is confirmed; the Gwern lines are probable and the rest unconfirmed. Timecodes are in the entries.
  - The raw Signal export is at `D:\Vault\_originals\signal\...`, not under `Vault-Knowledge`. Its times are UTC+1.

File is at `C:\Users\dev\AppData\Local\Temp\claude\P---WORKDIR-HUB\s_2d49745b\scratchpad\leads\facts_01.json`

🧒 Простыми словами: Я собрал на 23 человек по справке: кто что делает, что говорил и что им можно подарить без просьб. Про многих мало что известно, они просто записались на встречу, поэтому им писать пока рано. Самые полезные: Ян (его черновик ещё открыт для комментариев), Луи (у него программа, похожая на нашу шину) и Олег (его сайт про институты для ИИ).

18.10.2026</result>
<usage><subagent_tokens>216300</subagent_tokens><tool_uses>35</tool_uses><duration_ms>570538</duration_ms></usage>
</task-notification>

---

**Claude:**

Все три пачки готовы. Вытаскиваю тех, кому стоит писать, в сжатом виде.

---

> `Bash` -- {"command": "cd \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_2d49745b/scratchpad/leads\"; python -c \"\nimport json\nfor i in ['00','01','02']:\n  for p in json.load(open(f'facts_{i}.json',encoding='utf-8')):\n    w=p.get('worth_messaging'); v=w

---

> `Read` -- {"file_path": "C:\\Users\\dev\\.claude\\projects\\P---WORKDIR-HUB\\s_2d49745b\\tool-results\\b8zm2tw94.txt"}

---

> `Bash` -- {"command": "python ~/.claude/scripts/machine_stamp.py line --agent \"Claude Opus 5.5\" 2>&1; date '+%H:%M %Z'; TZ=Europe/Lisbon date '+%H:%M Lisbon'; TZ=America/Los_Angeles date '+%H:%M PDT'", "description": "Get machine stamp and current time"}

---

> `Write` -- {"file_path": "D:\\Vault\\Vault-Knowledge\\04-Projects\\outreach-2026-10-18-character-salon-drafts.md", "content": "---\ntitle: \"Черновики: первое касание людям салона Character Design (08.10) и Vivarium (09.10)\"\ntype: outreach-drafts\nstage: draft\ndate: 2026-10-18\nauthored_by: claude\nmachi

---

> `Bash` -- {"command": "f=\"D:/Vault/Vault-Knowledge/04-Projects/outreach-2026-10-18-character-salon-drafts.md\"; echo \"drafts: $(grep -c '^### ' $f)\"; echo \"signal: $(grep '^### ' $f | grep -c Signal)\"; echo \"✅: $(grep '^### ' $f | grep -c '✅')  🛠: $(grep '^### ' $f | grep -c '🛠')\"; grep -c '[—–]' $f

---

> `Bash` -- {"command": "python -c \"t=open(r'D:/Vault/Vault-Knowledge/04-Projects/outreach-2026-10-18-character-salon-drafts.md',encoding='utf-8').read();print(t.count('\\u2014'),t.count('\\u2013'))\"", "description": "Count real em and en dashes"}

---

**Claude:**

Готово: 32 человека, 47 черновиков (17 в Signal, 30 в X). Ничего не отправлено. Файл: [outreach-2026-10-18-character-salon-drafts.md](D:/Vault/Vault-Knowledge/04-Projects/outreach-2026-10-18-character-salon-drafts.md)

**Кто это.** «Салон Карак Контерсона» оказался салоном Character Design в четверг 08.10 (Time Being Tea House, SF). Пятница: встреча Vie в Vivarium 09.10. Всего в CRM 65 карточек плюс 6 человек, которых не было в таблице.

**Как склеивал.** Три субагента прошли каждую карточку. Для каждого собрали: что человек говорил на записях Plaud (с таймкодами), что писал в Signal-группе Character Underground, что пушил на GitHub на этой неделе (`gh api` сегодня), его био в X и наши прошлые касания. 33 человека отсеяны: про них есть только RSVP в Partiful, и встреча с ними ничем не подтверждена.

**Правило трёх подарков.** Подарков (🎁) в карточках не было ни у кого. Поэтому в каждом черновике одна польза и ни одной просьбы. Три примера:
- **Clément Dumas.** Наш PR в его diffing-toolkit смержен 16.10 с «Thank you!». Плюс ответ на его вопрос в группе про хакатон персонажей.
- **Antra.** PR в connectome-host смержен 17.10, второй PR (#402) обновлён по замечаниям ревьюера.
- **Arthur.** Ровно то, что он сам просил написать в личку: отзыв о вечере и идеи спикеров. Плюс ответ на его вопрос, где искать гранты на исследования характера.

**Готовность:**
- ✅ 23 можно слать сразу. В двух (Arthur, Vie) сверь отзыв и факт про нашего агента со своим впечатлением.
- 🛠 9 требуют сначала сделать подарок. Самое срочное: Jan Kulveit публикует введение в психологию LLM на этой неделе, комментарии в его документ нужны до публикации. Ещё gwern: он сам просил список канонических текстов про характеры, из трёх существующих списков можно собрать один.
- 🤔 Отмечены люди, с кем встреча или личность не доказаны. Например, у dev Balitskyi в X написано «Founding Designer @opalapp», это может быть другой человек.

**Неопознанные.** Отдельная таблица: Asterism, clu, Mc S, Drew, Melissa, Char и 17 скрытых гостей салона. По каждому записал, как его опознать.

**Не включены, и почему:**
- **Anna Mikeda.** Ей уже обещаны черновики 5 писем для визы O-1, этот подарок сильнее любого сообщения.
- **Rune Kvist.** С ним собеседование, это отдельная полоса.
- **Интро gwern к инвестору Matt Mandel.** Это просьба, до трёх подарков gwern рано.

**Проверено:** 32 блока в файле, 17 из них с Signal, длинных тире 0 (подсчёт python). **Не проверено:** что Signal-ники «tim» и «Jan Kulveit» это именно эти люди. Ленты X прочитать нельзя: x.com отдаёт 402, поэтому про X использовал только био из карточек.

🎙 Майк: я бы начал с девяти подготовок. Подарок, который человек сам просил (правки в каталог Shubham, комментарии в документ Jan), запоминается сильнее любого «nice to meet you». Могу сделать их сам следующим заходом.

🧒 **Простыми словами:** познакомился с людьми, а теперь каждому нужна открытка с маленьким подарком внутри: ссылкой, исправленной ошибкой или ответом на вопрос, который он сам задавал. 32 открытки подписаны и лежат в папке. Девяти не хватает подарка, его надо сначала смастерить. Ни одна открытка ещё не отправлена, отправляешь ты.
