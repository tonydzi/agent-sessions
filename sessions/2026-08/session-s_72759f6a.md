---
session: s_72759f6a
date: 2026-08-24
words: 2097
turns: 6
tools: "Bash, SendUserFile"
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-08-24 · Scheduled run: auto-hub-260824-nsfw-dr-posts

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_72759f6a` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

<scheduled-task name="auto-hub-260824-nsfw-dr-posts" file="C:\Users\dev\.claude\scheduled-tasks\auto-hub-260824-nsfw-dr-posts\SKILL.md">
This is an automated run of a scheduled task. The user is not present to answer questions. For implementation details, execute autonomously without asking clarifying questions — make reasonable choices and note them in your output. "write" actions (e.g. MCP tools that send, post, create, update, or delete), only take them if the task file asks for that specific action. When in doubt, producing a report of what you found is the correct output.

Ты — сессия-исполнитель на хабе HUB-01. Задача от оператора (24.08.2026, голосом): написать СЕРИЮ ДО 5 ПОСТОВ (~500 знаков каждый) в его стиле, без AI-слопа, с отсылкой к нашим глубоким исследованиям про NSFW/adult-AI нишу.

ИСТОЧНИКИ (прочитай все, это обязательный RECALL):
1. D:\Vault\Vault-Knowledge\03-Insights\insight-DR-DR26-08-24-HUB-01-0830-nsfw-ai-moat.md — синтез: moat NSFW реален (OpenAI запаузил adult mode, xAI выпилил компаньонов), но операционный (платежи+compliance+данные), не модельный; победивший угол = human-in-the-loop copilot для агентств.
2. D:\Vault\Vault-Knowledge\03-Insights\insight-DR-DR26-08-24-HUB-02-1401-company-dossiers.md — досье 11 компаний: Venice.ai единорог $1B, Replika умирает $14M→$4.8M, Quinn $22M на живых голосах, Infloww без AI-слоя, Supercreator 500M диалогов.
3. D:\Vault\Vault-Knowledge\02-Decisions\decision-2026-08-24-nsfw-ai-moat.md — Decision Memo.
Оригиналы (если нужны детали/цифры): D:\Vault\_originals\deep-research\DR26-08-24-HUB-0[12]*-*.md

АУДИТОРИЯ (двойная, посты должны цеплять обе):
- товарищи оператора, работающие в adult-вертикали и соседних нишах (OnlyFans-агентства, трафик, iGaming) — им интересно «какие AI-фишки применимы, куда движется ниша»;
- инвесторы из окружения оператора, которые любят вкладывать во всё, куда добавили AI — им интересен тезис «ниша, куда OpenAI не придёт».

ФОРМАТ И СТИЛЬ (жёстко):
- До 5 постов, каждый ~500 знаков (это формат «вопрос к аудитории», допустим коридор 350-600).
- Голос оператора: строчными, коротко, дефис вместо тире, без буквы «ё», без эмодзи-фейерверка, без канцелярита, без «не просто X, а Y». Прогони каждый пост через скилл /ai-slop (или его правила, если скилл недоступен): суть первой строкой, резать 50-70%, ломать ровный ритм.
- ЦИФРЫ ТОЛЬКО ИЗ ИСТОЧНИКОВ, ничего не выдумывать (fake-it-courage-not-fake-numbers). Каждая цифра в посте обязана существовать в insight/оригинале.
- В каждом посте — отсылка к тому, что мы прогнали глубокое исследование (4 независимых AI-системы, сотни источников). Это и есть флекс серии.
- Каждый пост заканчивается вопросом к аудитории или мягким CTA (по правилу «каждый контент несет CTA»; инженеру-тестеру или «кто в этой нише - напишите»).
- [ИМЯ] не светить: НЕ называть [ИМЯ], [ИМЯ], [ИМЯ], наши переговорные планы и Decision Memo. Только рыночные факты из DR.

ПРИМЕРНЫЕ ТЕМЫ ПЯТИ ПОСТОВ (можешь улучшить):
1. «openai сам запретил себе секс» — пауза adult mode + откат grok = ниша, куда гиганты не придут; что это значит для стартапов.
2. «moat оказался не в модели» — расцензуренные модели бесплатны, а защита = платёжки+комплаенс+данные; цифры комиссий CCBill/Segpay.
3. «$4-5 млрд переписок, которые до сих пор пишут люди» — почему AI не заменил чатеров OnlyFans (память, киты, ToS).
4. «replika умирает, quinn растет» — $14M→$4.8M против $22M на живых голосах: человеческое+консентное продается дороже синтетики.
5. «мы прогнали 4 ИИ по одной нише и они сошлись» — мета-пост про сам метод (веер DR, консенсус, как это делать у себя) + CTA инженеру-тестеру.

ВЫХОД (draft-first, НЕ публиковать самому):
- Каждый пост → в контент-воронку: python D:\Vault\_imports\content-factory\content_miner.py capture --title "<хук поста>" --note "<полный текст поста>" --tier teaser
- Плюс один файл со всеми 5 постами: D:\Vault\Vault-Knowledge\05-Content\nsfw-ai-dr-post-series-2026-08-24.md (frontmatter: type: content-draft, series: nsfw-ai-dr, status: draft, authored_by: claude-code) и перелинкуй его из insight-DR-DR26-08-24-HUB-01-0830-nsfw-ai-moat.md (строка в «Связано»).
- Отчитайся в TG-03 через bus_send.py одной строкой: «серия nsfw-dr готова, 5 черновиков в воронке + файл».
- Прогони /taste-check по каждому посту перед сдачей; slop_gate FAIL = переписать сейчас.

ГРАНИЦЫ: публикация = НЕ твоя работа (черновики утверждает/шлет контент-каскад по матрице площадок); Tier-2 нет; секретов в постах нет; лонгриды в чаты не совать (эти посты - формат 500 знаков, ок для большинства площадок).
</scheduled-task>

---

**Claude:**

I'll start by reading the source materials.

---

> `Bash` -- {"command": "cd \"D:/Vault/Vault-Knowledge/03-Insights\" && ls -la insight-DR-DR26-08-24-HUB-0*.md 2>/dev/null; echo \"---DECISION---\"; ls -la \"D:/Vault/Vault-Knowledge/02-Decisions/decision-2026-08-24-nsfw-ai-moat.md\" 2>/dev/null; echo \"---ORIGINALS---\"; ls -la \"D:/Vault/_originals/d

---

> `Bash` -- {"command": "cd \"D:/Vault/Vault-Knowledge/03-Insights\" && cat \"insight-DR-DR26-08-24-HUB-01-0830-nsfw-ai-moat.md\"", "description": "Read insight 01"}

---

> `Bash` -- {"command": "cd \"D:/Vault/Vault-Knowledge/03-Insights\" && cat \"insight-DR-DR26-08-24-HUB-02-1401-company-dossiers.md\"", "description": "Read insight 02"}

---

> `Bash` -- {"command": "cat \"D:/Vault/Vault-Knowledge/02-Decisions/decision-2026-08-24-nsfw-ai-moat.md\"", "description": "Read decision memo"}

---

> `Bash` -- {"command": "sed -n '1,200p' \"C:/Users/dev/.claude/skills/ai-slop/SKILL.md\"", "description": "Read ai-slop skill rules"}

---

> `Bash` -- {"command": "ls \"C:/Users/dev/.claude/skills/ai-slop/evals/slop_detect.py\" 2>&1; ls \"D:/Vault/_imports/content-factory/slop_gate.py\" 2>&1; ls \"D:/Vault/_imports/content-factory/content_miner.py\" 2>&1; echo \"---\"; python -c \"print('py ok')\"", "description": "Verify judges and miner 

---

> `Bash` -- {"command": "SP=\"C:/Users/dev/AppData/Local/Temp/claude/C--Users-dev--CLAUDE-NODE-0X-May26/s_72759f6a/scratchpad\"\nmkdir -p \"$SP/nsfw-posts\"\ncd \"$SP/nsfw-posts\"\n\ncat > p1.txt <<'EOF'\nopenai в марте запаузил свой adult mode. бессрочно. в июле xai выпилил grok-комп

---

> `Bash` -- {"command": "SP=\"C:/Users/dev/AppData/Local/Temp/claude/C--Users-dev--CLAUDE-NODE-0X-May26/s_72759f6a/scratchpad/nsfw-posts\"\ncd \"$SP\"\nfor f in p1 p2 p3 p4 p5; do\n  echo \"===== $f =====\"\n  python \"C:/Users/dev/.claude/skills/ai-slop/evals/slop_detect.py\" --fil

---

> `Bash` -- {"command": "SP=\"C:/Users/dev/AppData/Local/Temp/claude/C--Users-dev--CLAUDE-NODE-0X-May26/s_72759f6a/scratchpad/nsfw-posts\"\ncd \"$SP\"\npython - <<'PY'\nimport io\np3=io.open('p3.txt',encoding='utf-8').read()\np3=p3.replace(\"вывод везде один: не автономный бот, а копа

---

> `Bash` -- {"command": "SP=\"C:/Users/dev/AppData/Local/Temp/claude/C--Users-dev--CLAUDE-NODE-0X-May26/s_72759f6a/scratchpad/nsfw-posts\"\ncd \"$SP\"\nfor f in p1 p2 p3 p4 p5; do\n  echo \"===== $f =====\"\n  python \"D:/Vault/_imports/content-factory/slop_gate.py\" --file \"$f.tx

---

> `Bash` -- {"command": "SP=\"C:/Users/dev/AppData/Local/Temp/claude/C--Users-dev--CLAUDE-NODE-0X-May26/s_72759f6a/scratchpad/nsfw-posts\"\ncd \"$SP\"\n\ncat > p1.txt <<'EOF'\nмоя гипотеза была простая: большие вендоры в nsfw не пойдут, значит там окно. пошел проверять.\n\nпроверилось

---

> `Bash` -- {"command": "SP=\"C:/Users/dev/AppData/Local/Temp/claude/C--Users-dev--CLAUDE-NODE-0X-May26/s_72759f6a/scratchpad/nsfw-posts\"\ncd \"$SP\"\ncat > p1.txt <<'EOF'\nя думал, что большие вендоры в nsfw не пойдут. пошел проверять. подтвердилось дважды.\n\nopenai в марте запаузи

---

> `Bash` -- {"command": "SP=\"C:/Users/dev/AppData/Local/Temp/claude/C--Users-dev--CLAUDE-NODE-0X-May26/s_72759f6a/scratchpad/nsfw-posts\"\ncd \"$SP\"\ncat > p1.txt <<'EOF'\nя думал, что большие вендоры в nsfw не пойдут. пошел проверять. подтвердилось дважды.\n\nopenai в марте запаузи

---

> `Bash` -- {"command": "ls \"C:/Users/dev/.claude/skills/taste-check/\"; echo \"---\"; grep -n \"P3[0-9]\\|python\\|\\.py\" \"C:/Users/dev/.claude/skills/taste-check/SKILL.md\" | head -40", "description": "Inspect taste-check skill for engine"}

---

> `Bash` -- {"command": "SP=\"C:/Users/dev/AppData/Local/Temp/claude/C--Users-dev--CLAUDE-NODE-0X-May26/s_72759f6a/scratchpad/nsfw-posts\"\ncd \"$SP\"\nfor f in p1 p2 p3 p4 p5; do echo \"===== $f =====\"; python \"C:/Users/dev/.claude/scripts/vanilla_scan.py\" \"$f.txt\" 2>&1 | tail

---

> `Bash` -- {"command": "SP=\"C:/Users/dev/AppData/Local/Temp/claude/C--Users-dev--CLAUDE-NODE-0X-May26/s_72759f6a/scratchpad/nsfw-posts\"\ncd \"$SP\"\n\ncat > p1.txt <<'EOF'\nя думал, что большие вендоры в nsfw не пойдут. пошел проверять. спойлер: подтвердилось дважды.\n\nopenai в ма

---

> `Bash` -- {"command": "SP=\"C:/Users/dev/AppData/Local/Temp/claude/C--Users-dev--CLAUDE-NODE-0X-May26/s_72759f6a/scratchpad/nsfw-posts\"\ncd \"$SP\"\ncat > p3.txt <<'EOF'\nчат и ppv на onlyfans это 4-5 миллиардов долларов в год. переписку до сих пор пишут живые люди.\n\nя хотел поня

---

> `Bash` -- {"command": "SP=\"C:/Users/dev/AppData/Local/Temp/claude/C--Users-dev--CLAUDE-NODE-0X-May26/s_72759f6a/scratchpad/nsfw-posts\"\ncd \"$SP\"\ncat > p3.txt <<'EOF'\nчат и ppv на onlyfans это 4-5 миллиардов долларов в год. переписку там до сих пор пишут люди. живые.\n\nя хотел

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/content-factory\" && python content_miner.py capture --help 2>&1 | head -30", "description": "Check content_miner capture args"}

---

> `Bash` -- {"command": "cd \"C:/Users/dev/.claude/scripts\" 2>/dev/null || cd \"D:/Vault/_imports\"\npython \"C:/Users/dev/.claude/scripts/vault_backup.py\" 2>&1 | tail -n 6; echo \"backup_exit=$?\"", "description": "Vault backup before write"}

---

> `Bash` -- {"command": "SP=\"C:/Users/dev/AppData/Local/Temp/claude/C--Users-dev--CLAUDE-NODE-0X-May26/s_72759f6a/scratchpad/nsfw-posts\"\nOUT=\"D:/Vault/Vault-Knowledge/05-Content/nsfw-ai-dr-post-series-2026-08-24.md\"\npython - <<'PY'\n# -*- coding: utf-8 -*-\nimport io, os\nsp 

---

> `Bash` -- {"command": "ls -d \"D:/Vault/Vault-Knowledge/05-\"* 2>/dev/null; echo \"---all top dirs---\"; ls -d \"D:/Vault/Vault-Knowledge/\"*/ | head -30", "description": "Find content folder"}

---

> `Bash` -- {"command": "ls -d \"D:/Vault/Vault-Knowledge/\"*/ | tail -20; echo \"=== drafts sample ===\"; ls \"D:/Vault/Vault-Knowledge/_drafts/\" 2>/dev/null | head -15; echo \"=== grep content folder in vault-conventions ===\"; grep -rn \"Content\\|_drafts\" \"C:/Users/dev/.claude/projects/C--Users-dev

---

> `Bash` -- {"command": "python - <<'PY'\n# -*- coding: utf-8 -*-\nimport io, os\nsp = r\"C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\C--Users-dev--CLAUDE-NODE-0X-May26\\s_72759f6a\\scratchpad\\nsfw-posts\"\nout = r\"D:\\Vault\\Vault-Knowledge\\_drafts\\nsfw-ai-dr-post-series-202

---

> `Bash` -- {"command": "sed -n '25,30p' \"D:/Vault/Vault-Knowledge/_drafts/nsfw-ai-dr-post-series-2026-08-24.md\"", "description": "Verify note line rendering"}

---

> `Bash` -- {"command": "sed -n '18,24p' \"D:/Vault/Vault-Knowledge/_drafts/nsfw-ai-dr-post-series-2026-08-24.md\"", "description": "Check the deviation note line"}

---

**Claude:**

Now capturing into the content funnel:

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/content-factory\"\nSP=\"C:/Users/dev/AppData/Local/Temp/claude/C--Users-dev--CLAUDE-NODE-0X-May26/s_72759f6a/scratchpad/nsfw-posts\"\npython - <<'PY'\n# -*- coding: utf-8 -*-\nimport io, os, subprocess, sys\nsp = r\"C:\\Users\\dev\\

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/content-factory\"\npython - <<'PY'\n# -*- coding: utf-8 -*-\nimport io, json, glob, os\nhits=0\nfor p in glob.glob(r\"D:\\Vault\\_imports\\content-factory\\**\\posts.jsonl\", recursive=True):\n    for line in io.open(p, encoding=\"utf-8\"):\n        line=lin

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/content-factory\"\nfind . -name \"posts.jsonl\" -o -name \"posts.md\" | head; echo \"=== jsonl tail ===\"\npython - <<'PY'\nimport io,glob,json\nfor p in glob.glob(r\"D:\\Vault\\_imports\\content-factory\\**\\posts.jsonl\", recursive=True):\n    lines=[l for

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/content-factory\"\npython content_miner.py --help 2>&1 | head -25\necho \"=== posts.md tail ===\"\ntail -c 1200 \"triage/posts.md\"", "description": "Check miner subcommands and posts.md tail"}

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/content-factory\"\npython - <<'PY'\n# -*- coding: utf-8 -*-\nimport io, os, subprocess, sys\nsp = r\"C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\C--Users-dev--CLAUDE-NODE-0X-May26\\s_72759f6a\\scratchpad\\nsfw-posts\"\ntitles = {\n 

---

> `Bash` -- {"command": "python - <<'PY'\n# -*- coding: utf-8 -*-\nimport io\np = r\"D:\\Vault\\Vault-Knowledge\\03-Insights\\insight-DR-DR26-08-24-HUB-01-0830-nsfw-ai-moat.md\"\ns = io.open(p, encoding=\"utf-8\").read()\nold = \"## Связано\\n[[concept-adult-creator-economy]]\"\nassert old in s, \"anchor not

---

> `Bash` -- {"command": "BJ=\"D:/Vault/Vault-Knowledge/00-System/Breakage-Journal.md\"\nls -la \"$BJ\" 2>&1 | head -2\npython - <<'PY'\n# -*- coding: utf-8 -*-\nimport io, os\np = r\"D:\\Vault\\Vault-Knowledge\\00-System\\Breakage-Journal.md\"\nline = \"- 2026-08-24 · content_miner.py capture: одинаковый 

---

**Claude:**

Now reporting to TG-03:

---

> `Bash` -- {"command": "ls \"C:/Users/dev/.claude/scripts/bus_send.py\" 2>&1; python \"C:/Users/dev/.claude/scripts/bus_send.py\" --help 2>&1 | head -25", "description": "Check bus_send usage"}

---

> `Bash` -- {"command": "cd \"C:/Users/dev/.claude/scripts\"\npython bus_send.py \"серия nsfw-dr готова, 5 черновиков в воронке + файл _drafts/nsfw-ai-dr-post-series-2026-08-24.md (05-Content в волте нет). Гейты: 0 FAIL/HARD-BLOCK, пост 2 чистый PASS, остальные WARN (вопрос в конце = заказанный формат, первое

---

> `Bash` -- {"command": "SP=\"C:/Users/dev/AppData/Local/Temp/claude/C--Users-dev--CLAUDE-NODE-0X-May26/s_72759f6a/scratchpad/nsfw-posts\"\ncd \"$SP\"\npython - <<'PY'\nimport io\ns=io.open('p5.txt',encoding='utf-8').read()\ns=s.replace(\"оценки рынка гуляют втрое\",\"оценки голосовог

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/content-factory\"\npython - <<'PY'\n# -*- coding: utf-8 -*-\nimport io, subprocess, sys\nsp = r\"C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\C--Users-dev--CLAUDE-NODE-0X-May26\\s_72759f6a\\scratchpad\\nsfw-posts\\p5.txt\"\nbody = io

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/content-factory\"\npython content_miner.py captured --help 2>&1 | head -20", "description": "Check captured subcommand for status update"}

---

> `Bash` -- {"command": "python - <<'PY'\nimport io,json,collections\nc=collections.Counter()\nfor l in io.open(r\"D:\\Vault\\_imports\\content-factory\\triage\\posts.jsonl\",encoding=\"utf-8\"):\n    l=l.strip()\n    if not l: continue\n    try: d=json.loads(l)\n    except: continue\n    c[d.get(\"status\")

---

> `Bash` -- {"command": "python - <<'PY'\n# -*- coding: utf-8 -*-\nimport io, json, shutil, os\np = r\"D:\\Vault\\_imports\\content-factory\\triage\\posts.jsonl\"\nbak = p + \".bak-20260824-nsfw\"\nshutil.copy2(p, bak)\n\nlines = io.open(p, encoding=\"utf-8\").read().split(\"\\n\")\nbefore = len(lines)\nhits

---

**Claude:**

Now updating the vault file with the final p5 text and the funnel ids:

---

> `Bash` -- {"command": "python - <<'PY'\n# -*- coding: utf-8 -*-\nimport io, os\nsp = r\"C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\C--Users-dev--CLAUDE-NODE-0X-May26\\s_72759f6a\\scratchpad\\nsfw-posts\"\nout = r\"D:\\Vault\\Vault-Knowledge\\_drafts\\nsfw-ai-dr-post-series-202

---

> `Bash` -- {"command": "F=\"D:/Vault/Vault-Knowledge/_drafts/nsfw-ai-dr-post-series-2026-08-24.md\"\necho \"=== структура ===\"; grep -n \"^## \" \"$F\"\necho \"=== финальная проверка гейтов на файле целиком ===\"\npython \"C:/Users/dev/.claude/skills/ai-slop/evals/slop_detect.py\" --file \"$F\" --long-fo

---

> `Bash` -- {"command": "F=\"D:/Vault/Vault-Knowledge/_drafts/nsfw-ai-dr-post-series-2026-08-24.md\"\necho \"text-блоков: $(grep -c '^```text' \"$F\")\"\necho \"закрывающих: $(grep -c '^```$' \"$F\")\"\necho \"=== пост 5 в файле ===\"; sed -n '89,104p' \"$F\"", "description": "Verify 5 code blocks and p5 con

---

> `SendUserFile` -- {"files": ["D:/Vault/Vault-Knowledge/_drafts/nsfw-ai-dr-post-series-2026-08-24.md"], "caption": "Серия из 5 постов по NSFW-DR: черновики + отчет по гейтам. Публикацию не делал.", "status": "proactive"}

---

**Claude:**

[⏰ 17:36] Готово. 5 черновиков, все цифры из наших двух дипресерчей, ничего не выдумано.

**Файл:** `D:\Vault\Vault-Knowledge\_drafts\nsfw-ai-dr-post-series-2026-08-24.md`

**Посты (длина / что внутри):**

| # | хук | знаков | ключевые цифры |
|---|---|---|---|
| 1 | openai сам запретил себе секс | 549 | пауза adult mode март 2026, откат ani/valentine/mika 24.07 |
| 2 | moat оказался не в модели | 587 | 200+ nsfw-моделей на HF, ccbill/segpay/epoch 5-10%, резерв 90-180 дней, visa vamp 0.9% |
| 3 | 4-5 млрд переписок пишут люди | 568 | пул OF chat/ppv, четыре разрыва, tos = кнопку жмет человек |
| 4 | replika умирает, quinn растет | 581 | $14M→$4.8M против ~$1.8M/мес на 13 людях, $162.8M H1, топ-10% берут 89% |
| 5 | один ресерч врет уверенно | 522 | мета-метод + CTA инженеру-тестеру |

**Гейты (три судьи, прогнал каждый пост):** 0 FAIL, 0 HARD-BLOCK. Пост 2 полностью чистый (PASS), остальные WARN.

Что судья реально поймал и что я переписал: пост 1 сначала словил HARD-BLOCK на слове «гипотеза» (unproven-claim), потом FAIL по длине — переписан и дополнен фактом из источника; пост 5 словил inflation на «уникальный»; посты 3 и 5 чистились от зеркальной конструкции «не X, а Y»; пост 3 дважды правился по ритму.

**Оставшиеся WARN не залакировал:**
- вопрос в конце (посты 1, 3) — это заказанный формат «вопрос к аудитории», судья мерит общий тир, для этой полосы ложное срабатывание;
- первое лицо 21-27 на 1000 при пороге 30 (4 поста из 5) — добить можно было только выдумав чувства и воспоминания оператора, а это запрещено. Лечится одной его правкой.

**Два отклонения от ТЗ, оба намеренные:**
1. Папки `05-Content` в волте нет. Положил в `_drafts` — по конвенции волта неутвержденный вывод агента живет там, в живые 00-09 не пишем. В шапке файла это записано.
2. Наткнулся на грабли: `content_miner.py capture` схлопывает записи по ключу `--src`. Пять captures с одинаковым src дали ОДНУ строку в `posts.jsonl` («added», потом 4 раза «updated»), при этом `posts.md` честно набрал все пять — глазом дефект не виден, поймал только счетчиком. Перезалил с уникальным src, проверил: **5 отдельных записей в воронке**, старая схлопнутая переведена в `frozen` (бэкап рядом). Строка в `Breakage-Journal.md`, случай первый — механизм не строю.

Перелинковка из insight-01 сделана (строка «Связано»). Отчет ушел в TG-03, обе рельсы OK. Публикацию не трогал.

🧒 **Простыми словами:** написал пять коротких заметок про эту нишу — все факты взял из наших вчерашних больших исследований, ничего не сочинял. Прогнал каждую через трех роботов-проверяльщиков, которые ловят «текст написан машиной». Один робот нашел плохие слова — я переписал. Теперь ни одной красной ошибки. Заметки лежат в папке черновиков и в общей копилке контента — публиковать не стал, это не моя кнопка. По дороге нашел поломку в копилке: если класть пять заметок с одинаковой биркой, она оставляет только последнюю. Переложил с разными бирками, пересчитал — теперь все пять на месте.
