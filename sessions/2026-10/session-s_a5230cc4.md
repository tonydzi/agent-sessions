---
session: s_a5230cc4
date: 2026-10-24
words: 29140
turns: 106
tools: "Bash, PowerShell, SendUserFile, Skill, ToolSearch, Write, computer, find, javascript_tool, mcp__Claude_Browser__browser_batch, mcp__Claude_Browser__get_page_text, mcp__Claude_Browser__javascript_tool"
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-10-24 · Это задача от оператора. Она пришла голосом в Telegram-группу «001 СЕССИЯ НОВАЯ»

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_a5230cc4` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

Это задача от оператора. Она пришла голосом в Telegram-группу «001 СЕССИЯ НОВАЯ»,
расшифрована ботом. Источник: tg:chat_REDACTED:7518.

ДОСЛОВНО, ЧТО СКАЗАЛ оператор:
---
Нужно добавить в нашу библию информацию о том, что оператору, если мы говорим про трудоустройство и кем-нибудь крупной ИИ-лаборатории, без разницы, с кем там трудоустроится. Давайте вместе подумаем. Имеет ли он смысл туда устроиться, условно говоря, уборщиком или инженером? Безусловно, уборщик это хуже, инженер лучше. Но если мы понимаем, что, скорее всего, ИИ-лабораторию можно будет вырасти, если у оператора, например, нет сильно релевантного опыта, то мы пытаемся трудоустроить его хотя бы даже, это очень утрирую, конечно, говорю, даже уборщиком. Если он там уборщиком в этой лаборатории, то он может поработать несколько лет в Дагестане. Он может стать старшим уборщиком и потом оказаться где-то полезным, в итоге стать крутым каким-то сотрудником. То есть часто мне так кажется, что в каких-то месяцах компания может строиться не синьором, а медлом, инженом. Я не говорю не про инженерию, я говорю про любую адвокацию. Поэтому нам нужно в каждой инженерической компании искать не только синьорные позиции, на которых типа high-level люди идут, да. Может, я ровно ровно покачиваю, не вышел я в мужку, у меня нет опыта покачивать. Это недостаточно для high-level. Но может нужны чем-нибудь, работать, допустим, медлом или инженом. Ничего там я вижу плохого. Ведь самая главная задача — попасть внутрь компании. А там уже дальше, я думаю, что великие шансы, что, во-первых, я пойму, интересно ли мне эта компания, а если интересно, я буду дальше уже пытаться в ней устроиться на какую-то другую позицию. Ну и если я пойму, что не всегда на нее стоит устраивать. То есть моя задача — попасть любой ценой внутрь компании. Не важно, какую позицию. Любой ценой внутрь компании.
---

КАК РАБОТАТЬ
1. RECALL первым ходом: память, волт, RAG (python D:\Vault\_imports\brain_ask.py "<тема>").
   Нашёл сделанным -- не делай заново: закрой дельту и скажи, чем и когда закрыто.
2. Расшифровка машинная, в ней бывают ослышки (память voice-transcription-synonyms:
   «Сиренка» = CRM, «Лиса» = Firefox). Смысл восстанавливай по контексту, слова оператора
   не переписывай и не смягчай (§9.7 «без купюр»).
3. Ты автономный кофаундер (§4.1-тер): по обратимому решай сам. оператора зови только на
   Tier-2 -- деньги, необратимое удаление, юр.подпись, секреты третьим лицам, масс-рассылка.
4. Много фактов для решения -> дашборд (§2.4). Собрал исполняемое -> прогони /tt.
5. РАБОТАЙ КАК ОБЫЧНАЯ ПОЛНОЦЕННАЯ СЕССИЯ. оператор сидит в тебе и читает тебя
   как любой другой свой чат (приказ 15.09, голосом). Значит:
     - весь результат ты кладёшь ВНУТРЬ СЕБЯ, в свой чат, целиком;
     - НЕ ужимай и НЕ суммаризируй: нашёл десять вариантов -- покажи десять,
       с названиями, ценами и прямыми ссылками; построил график -- покажи его строками;
     - волт и карточки -- ДОПОЛНЕНИЕ, а не замена ответа. «Подробности в карточке»
       вместо содержания = ответа нет («где блять мои подушки списком???», 15.09);
     - НИЧЕГО не выноси наружу: не шли отчёт в Telegram, не публикуй, не рассылай.
       Наружу уходит только то, о чём оператор попросил прямо в самой задаче.
   Длиннее 3 предложений -- разбивай пустой строкой (§9.10).

6. В ГРУППУ 001 (чат chat_REDACTED) СЕССИЯ НЕ ПИШЕТ НИКОГДА и НИЧЕГО -- ни отчёт,
   ни вопрос, ни «я застрял» (приказ оператора 15.09 19:28, голосом, после двух
   нарушений: сессия принесла туда «Отчёт 3», а другая -- «пришли продолжение»).
   Квитанцию о старте туда уже положила рельса; больше туда не пишет никто.
   Застрял или голосовая оборвана -> скажи это ВНУТРИ СЕБЯ, в своём чате,
   первой строкой ответа: оператор читает сессию сам и допишет продолжение сюда.

---

**Claude:**

🚂 План рельс на сессию: правило принимаю и раскладываю сам как Claude (это работа с каноном, волтом, памятью — оркестрация + суждение + голос, чужой бак тут не при чём). На чужие подписки в этой сессии не уходит ничего: класса «прочитать много кода / черновой текст / ДР» здесь нет. Если по ходу вылезет ДР — уйдёт веером по `/dr-fanout`.

Сначала RECALL — вдруг правило уже частично лежит.

---

> `Bash` -- {"command": "ls \"D:/Vault/Vault-Knowledge\" 2>/dev/null | head -30; echo \"---BIBLE reglament job---\"; find \"D:/Vault/Vault-Knowledge\" -iname \"reglament-*\" 2>/dev/null | grep -iE \"rabot|trudo|vakans|job|hire|naym|interview|cv|pozic\" | head -40", "description": "List vault root and job-

---

> `Bash` -- {"command": "cd \"C:/Users/dev/.claude/projects/P---WORKDIR-HUB/memory\" && grep -ilE \"job|vakans|hire|naym|position|senior|career\" *.md | head -30", "description": "Find job-related memory files"}

---

> `Bash` -- {"command": "cd \"C:/Users/dev/.claude/projects/P---WORKDIR-HUB/memory\" && cat job-search-money-first-criteria.md; echo \"=====HUB=====\"; cat hub-job-search.md", "description": "Read job search memory files"}

---

> `Bash` -- {"command": "ls \"D:/Vault/Vault-Knowledge/03-Insights/Operations/\" 2>/dev/null | grep -iE \"vakans|trudo|naym|job|interview|cv|kompan\" | head -30", "description": "List live bible operations job files"}

---

> `Bash` -- {"command": "cat \"D:/Vault/Vault-Knowledge/03-Insights/Operations/reglament-vakansii-dengi-pervym-200k-lyubaya-kompaniya.md\"", "description": "Read money-first bible file"}

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports\" 2>/dev/null && timeout 300 python brain_ask.py \"любой ценой попасть внутрь ИИ-лаборатории, позиция не важна, junior mid senior\" 2>&1 | head -60", "description": "RAG recall on getting inside AI lab any position"}

---

> `Bash` -- {"command": "head -120 \"D:/Vault/_imports/_brain_answer_rr.txt\"", "description": "Read RAG recall answer"}

---

**Claude:**

RECALL закончен. Вердикт: **правила нет**, есть только соседнее и его не заменяющее.

| Что нашёл | Дата | Отношение к задаче |
|---|---|---|
`reglament-vakansii-dengi-pervym-200k-lyubaya-kompaniya` | 24.09 | снимает фильтр по **типу компании**, но ставит порог **$200K базы** → прямо конфликтует с «хоть уборщиком» |
память `job-search-money-first-criteria` | 24.09 | то же, зеркало |
память `no-prior-ml-is-not-no-prior-experience` | 15.09 | «без ML» ≠ «без опыта» — про планку, не про уровень роли |
FB-дневник 09.09: «Если вы работаете в большой ИИ-лаборатории… занесите меня внутрь руками» | 09.09 | настрой звучал ещё три недели назад, но **правилом не стал** — сырьё |

Про «позиция не важна / любой ценой внутрь» — ноль строк в каноне, памяти и Библии. Пишем с нуля.

Теперь, раз ты сказал «давайте вместе подумаем» — думаю вслух, и одно возражение у меня есть.

---

> `Bash` -- {"command": "ls \"C:/Users/dev/.claude/skills/\" | grep -iE \"apply|job|cv|interview\" ; echo \"---\"; wc -c \"C:/Users/dev/.claude/skills/apply/SKILL.md\" 2>/dev/null; sed -n '1,60p' \"C:/Users/dev/.claude/skills/apply/SKILL.md\"", "description": "Inspect apply skill"}

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/jobs-watch\" 2>/dev/null && ls | head -40; echo \"---vip/target---\"; grep -rniE \"vip|target_compan\" jobs_spec_data.py batch_daily.py 2>/dev/null | head -20", "description": "Look for target/vip company list in pipe A"}

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/jobs-watch\" && grep -rn \"tier\" jobs_discover.py | head -20; echo \"=== VIP list ===\"; grep -rnE \"VIP|TARGET\" jobs_discover.py jobs_spec_data.py 2>/dev/null | head -20", "description": "Find tier assignment logic"}

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/jobs-watch\" && grep -rnE \"junior|intern|senior|staff|principal|CLUSTER_RX|NEG\" jobs_discover.py | head -40", "description": "Check seniority filters in discovery"}

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/jobs-watch\" && sed -n '282,300p' jobs_discover.py; echo \"=== cluster keys ===\"; python -c \"\nimport re,io\ns=open('jobs_discover.py',encoding='utf-8').read()\nimport ast\n\" ; grep -nE '^\\s{4}\\\"[a-z-]+\\\": \\[' jobs_discover.py | head -20", "description

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/jobs-watch\" && python -c \"\nimport jobs_spec_data as J\nv=J.VERIFIED\nlabs=['anthropic','openai','deepmind','mistral','xai','thinking','ssi','cohere','inflection','perplexity','scale','meta','google']\nfor row in v:\n    s=' '.join(str(x).lower() for x in row

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/jobs-watch\" && sed -n '404,445p' jobs_discover.py", "description": "Read discovery insert loop"}

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/jobs-watch\" && grep -n \"money_cluster\" -A 14 jobs_discover.py | head -40; echo \"=== jobs_money ===\"; sed -n '1,60p' jobs_money.py", "description": "Read money_cluster and jobs_money"}

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/jobs-watch\" && grep -n \"cluster\" batch_daily.py | head -30; echo \"=== UNCL refs ===\"; grep -rn \"UNCL\\|money-uncl\" batch_daily.py jobs_discover.py | head", "description": "Check cluster filtering in batch_daily"}

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/jobs-watch\" && grep -n \"CV_FALLBACK\" -A 12 jobs_discover.py | head -30; echo \"=== batch_daily cv ===\"; grep -n \"cv\\|CV\" batch_daily.py | head -20", "description": "Read CV_FALLBACK and batch_daily CV handling"}

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/jobs-watch\" && sed -n '1,40p' _test_jobs_discover.py; echo \"...\"; grep -n \"^def \\|^K[0-9]\" _test_jobs_discover.py | tail -25; wc -l _test_jobs_discover.py", "description": "Read discovery test file"}

---

**Claude:**

Факты собраны. Теперь правлю код — сначала пишу чистую функцию и красный тест.

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/jobs-watch\" && python - <<'PY'\nimport io\np='jobs_discover.py'\ns=io.open(p,encoding='utf-8').read()\n\nold_fallback = 'CV_FALLBACK = {\"engineering\": \"research\"}'\nnew_fallback = '''LAB_DOOR = \"lab-door\"                       # нога в двери frontier-лаб

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/jobs-watch\" && grep -n \"money_new\" jobs_discover.py", "description": "Find money_new usage"}

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/jobs-watch\" && python - <<'PY'\nimport io\np='jobs_discover.py'\ns=io.open(p,encoding='utf-8').read()\ns=s.replace('money_only={money_new}\")','money_only={money_new} lab_door={lab_new}\")',1)\nio.open(p,'w',encoding='utf-8',newline='\\n').write(s)\nPY\ncat >>

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/jobs-watch\" && python _test_jobs_discover.py 2>&1 | grep -E \"^(OK|FAIL) +L|FAIL|итог|ИТОГ|fails\" | head -20; echo \"exit=$?\"", "description": "Show lab-door test results"}

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/jobs-watch\" && sed -n '75,95p' _test_jobs_discover.py", "description": "Check end of test file"}

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/jobs-watch\" && python - <<'PY'\nimport io\np='_test_jobs_discover.py'\ns=io.open(p,encoding='utf-8').read()\ns=s.replace('sys.exit(1 if fails else 0)\\n\\n# --- нога в двери','# --- нога в двери',1)\nassert not s.rstrip().endswith('sys.exit(1 if fails else 0)'

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/jobs-watch\" && cp jobs_discover.py /tmp/jd_good.py && python - <<'PY'\nimport io\np='jobs_discover.py'; s=io.open(p,encoding='utf-8').read()\ns=s.replace('    if tier == \"tier1\":\\n        return LAB_DOOR, LAB_DOOR_SCORE\\n','',1)\nio.open(p,'w',encoding='ut

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/jobs-watch\" && for t in _test_batch_daily.py _test_jobs_comp.py _test_select_money.py; do printf \"%-26s \" \"$t\"; python $t >/dev/null 2>&1 && echo \"PASS\" || echo \"FAIL(exit=$?)\"; done; python -c \"import jobs_discover as j; print('import ok, lab-door CV

---

**Claude:**

Код зелёный. Теперь канон.

---

> `Bash` -- {"command": "cat > \"D:/Vault/Vault-Knowledge/03-Insights/Operations/reglament-vnutr-ii-laboratorii-lyuboy-cenoy-poziciya-ne-vazhna.md\" <<'MD'\n---\ntitle: \"Внутрь ИИ-лаборатории любой ценой: позиция не важна, важен вход\"\ntype: reglament\nstage: distilled\nsource: \"dev-directive (2026-09-2

---

> `Write` -- {"file_path": "D:\\Vault\\Vault-Knowledge\\03-Insights\\Operations\\reglament-vnutr-ii-laboratorii-lyuboy-cenoy-poziciya-ne-vazhna.md", "content": "---\ntitle: \"Внутрь ИИ-лаборатории любой ценой: позиция не важна, важен вход\"\ntype: reglament\nstage: distilled\nsource: \"dev-directive (2026-0

---

**Claude:**

Теперь память + индекс + хаб.

---

> `Write` -- {"file_path": "C:\\Users\\dev\\.claude\\projects\\P---WORKDIR-HUB\\memory\\get-inside-the-lab-at-any-position.md", "content": "---\nname: get-inside-the-lab-at-any-position\ndescription: \"Вакансии frontier ИИ-лаборатории (27.09.2026, голосом) — уровень роли и порог денег не фильтр, з

---

> `Bash` -- {"command": "cd \"C:/Users/dev/.claude/projects/P---WORKDIR-HUB/memory\" && printf '%s\\n' '- [Внутрь ИИ-лабы любой ценой](get-inside-the-lab-at-any-position.md) — ⭐27.09 уровень роли и порог $200K не фильтр в tier1-лабах; аутсорсный клининг «внутрь» не считается; дверь door_cluster/l

---

> `Bash` -- {"command": "cd \"C:/Users/dev/.claude/projects/P---WORKDIR-HUB/memory\" && printf '\\n%s\\n' '<!-- дописано 2026-09-27 (голосовая tg:chat_REDACTED:7518, «любой ценой внутрь»): хук ДОСЛОВНО из MEMORY.md INBOX -->' >> hub-job-search.md && printf '%s\\n' '- [Внутрь ИИ-лабы любой ценой](ge

---

**Claude:**

Теперь дверь в скилле `/apply` и строка в CLAUDE.md.

---

> `Bash` -- {"command": "cd \"C:/Users/dev/.claude/skills/apply\" && python - <<'PY'\nimport io\np='SKILL.md'; s=io.open(p,encoding='utf-8').read()\nanchor='### 1.2 Данные кандидата и канон ответов'\nadd = '''### 1.1-бис Внутрь ИИ-лаборатории любой ценой (голосом 27.09, origin dev)\n- В **frontier ИИ-лабора

---

> `Bash` -- {"command": "cd \"C:/Users/dev/.claude\" && python -c \"\nimport io,re\ns=io.open('skills/apply/SKILL.md',encoding='utf-8').read()\nd=re.search(r'description: \\\"(.*?)\\\"',s,re.S).group(1)\nprint(len(d))\n\"; grep -n \"9.13-бис\" CLAUDE.md | head -3; grep -n \"ВЕРСИЯ: v\" CLAUDE.md; wc -c CLAUDE

---

> `Bash` -- {"command": "cd \"C:/Users/dev/.claude\" && python - <<'PY'\nimport io\np='CLAUDE.md'; s=io.open(p,encoding='utf-8').read()\nanchor='### §9.8 ⭐ Сиренка (CRM) на МАСШТАБЕ'\nassert anchor in s\nadd = '''### §9.14 ⭐ ВНУТРЬ ИИ-ЛАБОРАТОРИИ ЛЮБОЙ ЦЕНОЙ — уровень роли не фильтр (dev 27.09, голосом)\nВа

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports\" && git rev-parse --is-inside-work-tree 2>&1 | head -2; git status --porcelain jobs-watch 2>&1 | head -5", "description": "Check git status of _imports"}

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports\" && git status --porcelain | head -10; echo \"--- root ---\"; git rev-parse --show-toplevel; git check-ignore -v jobs-watch/jobs_discover.py 2>&1 | head -2", "description": "Inspect git repo scope"}

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/jobs-watch\" && git rev-parse --show-toplevel 2>&1; ls -d .git 2>/dev/null; git status --porcelain 2>&1 | head", "description": "Check jobs-watch repo"}

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports\" && git ls-files jobs-watch | head -3; echo \"count=$(git ls-files jobs-watch | wc -l)\"; cat .gitignore 2>/dev/null | head -20", "description": "Is jobs-watch tracked"}

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports\" && git diff --stat -- jobs-watch/jobs_discover.py jobs-watch/_test_jobs_discover.py; echo \"exit=$?\"; git log --oneline -1 -- jobs-watch/jobs_discover.py; grep -c \"door_cluster\" jobs-watch/jobs_discover.py", "description": "Check diff of edited files"}

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/jobs-watch\" && sed -n '1,40p' jobs_discover.py | grep -nE \"Автор|автор|Machine|Operator\" ; grep -n \"Автор\" jobs_discover.py | head -3", "description": "Find author line in jobs_discover docstring"}

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/jobs-watch\" && sed -n '1,40p' jobs_discover.py", "description": "Read module docstring"}

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/jobs-watch\" && python - <<'PY'\nimport io\np='jobs_discover.py'; s=io.open(p,encoding='utf-8').read()\nold=\"Рельса: python stdlib, подписок не жжёт. Тест: _test_jobs_discover.py, _test_jobs_comp.py. Updated: 2026-09-24.\"\nnew=\"\"\"Рельса: python stdlib, под

---

**Claude:**

Тесты зелёные. Второй заход другим методом (§4.3-бис): не юнит-тест, а реальная доска Anthropic — сколько ролей мы теряли.

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/jobs-watch\" && timeout 300 python - <<'PY'\nimport jobs_discover as J\nfrom jobs_spec_data import VERIFIED, norm, items, comp, url_for\nimport json\ntot={}\nfor company, ats, slug, tier in VERIFIED:\n    if tier!='tier1' or company not in ('Anthropic','OpenAI'

---

**Claude:**

Второй заход дал число и сразу вскрыл дефект: среди +1348 ролей лезет гиг-мельница xAI («AI Tutor - Catalan» ×40 языков). Это ровно тот вендорский контур, который я сам запретил считать «внутрь». Чиню.

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/jobs-watch\" && python - <<'PY'\nimport io\np='jobs_discover.py'; s=io.open(p,encoding='utf-8').read()\nold='''LAB_DOOR = \"lab-door\"'''\nnew='''# Гиг-мельница и краудворк на доске лаборатории — НЕ «внутрь»: это подряд/оплата за задачу,\n# без штатного оформле

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/jobs-watch\" && python -c \"\nimport io\np='jobs_discover.py'; s=io.open(p,encoding='utf-8').read()\ni=s.index('LAB_JUNK_RX'); j=s.index('LAB_DOOR =')\nseg=s[i:j].replace(chr(92)+chr(92),chr(92))\ns=s[:i]+seg+s[j:]\nio.open(p,'w',encoding='utf-8',newline='\\n')

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/jobs-watch\" && python -c \"\nimport jobs_discover as J\nprint('rx:', J.LAB_JUNK_RX.pattern)\nprint('match:', bool(J.LAB_JUNK_RX.search('AI Tutor - Catalan')))\nprint('door:', J.door_cluster('AI Tutor - Catalan','tier1',None))\n\"; grep -n \"LAB_JUNK_RX\" jobs_

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/jobs-watch\" && sed -n '215,226p' jobs_discover.py | cat -A | sed -n '1,12p' | cut -c1-160", "description": "Inspect raw bytes of regex block"}

---

**Claude:**

Знакомый класс: в регулярку попали настоящие байты backspace 0x08 (в этой папке для того и лежит `_fix_backspace_patterns.py`). Перезаписываю блок корректно.

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/jobs-watch\" && python - <<'PY'\nimport io, re\np='jobs_discover.py'; s=io.open(p,encoding='utf-8').read()\nB = chr(8)\nstart = s.index('LAB_JUNK_RX = re.compile(')\nend = s.index('LAB_DOOR = \"lab-door\"')\nbs = chr(92) + 'b'\nnew = ('LAB_JUNK_RX = re.compile(

---

**Claude:**

Одно моё решение было перегибом: Anthropic Fellows Program — это как раз лучшая нога в двери (платная программа с конверсией в штат), а не гиг-мельница. Убираю её из отсечки.

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/jobs-watch\" && python - <<'PY'\nimport io\np='jobs_discover.py'; s=io.open(p,encoding='utf-8').read()\nbs=chr(92)\ns=s.replace('|'+bs+'bfellows? program'+bs+'b','',1)\nassert 'fellows' not in s\nio.open(p,'w',encoding='utf-8',newline='\\n').write(s)\np='_test_

---

**Claude:**

Третий заход — перемер по живым доскам после отсечки гиг-мельницы.

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/jobs-watch\" && timeout 420 python - <<'PY'\nimport jobs_discover as J\nfrom jobs_spec_data import VERIFIED, norm, items, comp, url_for\nimport json\nTOT=[0,0,0]\nprint(f\"{'лаборатория':22}{'было':>6}{'стало':>7}{'+lab-door':>11}{'гиг-мельница':>14}{'стажировк

---

**Claude:**

+2159 строк — но в `tier1` сидят Stripe, Databricks и хедж-фонды, а это не «крупная ИИ-лаборатория». Сужаю полосу до явного списка лабораторий (мой долг №4 закрываю сразу).

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/jobs-watch\" && python - <<'PY'\nimport io\np='jobs_discover.py'; s=io.open(p,encoding='utf-8').read()\nanchor='LAB_DOOR = \"lab-door\"'\nadd = '''# «Крупная ИИ-лаборатория» из приказа 27.09 — ЯВНЫЙ список, а не весь tier1: в tier1 сидят\n# Stripe, Databricks, 

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/jobs-watch\" && for t in _test_jobs_discover.py _test_batch_daily.py _test_jobs_comp.py _test_select_money.py _test_jobs_discover.py; do printf \"%-26s \" \"$t\"; python $t >/dev/null 2>&1 && echo PASS || echo FAIL; done\ntimeout 420 python - <<'PY'\nimport job

---

**Claude:**

Полоса сужена, всё зелёное. Обновляю канон под финальную механику и замер.

---

> `Bash` -- {"command": "cd \"D:/Vault/Vault-Knowledge/03-Insights/Operations\" && python - <<'PY'\nimport io\np='reglament-vnutr-ii-laboratorii-lyuboy-cenoy-poziciya-ne-vazhna.md'\ns=io.open(p,encoding='utf-8').read()\n\ns=s.replace('(машинная истина = доска с `tier1` в `jobs_spec_data.VERIFIED`: Anthropic,

---

> `Bash` -- {"command": "python - <<'PY'\nimport io\n# 1) память\np=r\"C:\\Users\\dev\\.claude\\projects\\P---WORKDIR-HUB\\memory\\get-inside-the-lab-at-any-position.md\"\ns=io.open(p,encoding='utf-8').read()\ns=s.replace('(tier1-доски: Anthropic, OpenAI, xAI, Mistral, Thinking Machines, Inflecti

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/jobs-watch\" && python - <<'PY'\nimport io\np='jobs_discover.py'; s=io.open(p,encoding='utf-8').read()\ns=s.replace(\"Ярусы решает door_cluster():\\nстажировки и new grad отсечены всегда, деньги старше ноги в двери.\",\n\"Ярусы решает door_cluster():\\nстажиров

---

> `Bash` -- {"command": "cd \"C:/Users/dev/.claude\" && printf '%s\\n' '- §9.14 добор того же дня: полоса сужена с «весь tier1» до явного LAB_DOOR_CO (23 лаборатории) после замера по живым доскам (+2159 на всём tier1, из них Stripe +374 и хедж-фонды +348 = раздувание базы; по лабораториям +955). Добавлена отс

---

> `Bash` -- {"command": "powershell -NoProfile -Command \"(Get-Date).ToString('dd.MM.yyyy HH:mm') + ' (Пало-Альто) / ' + [System.TimeZoneInfo]::ConvertTimeBySystemTimeZoneId((Get-Date).ToUniversalTime(),'GMT Standard Time').ToString('HH:mm') + ' Лиссабон'\"", "description": "Get current local time"}

---

**Claude:**

🕐 27.09.2026, 08:54 (машина HUB-01)

## Сперва то, о чём ты попросил: «давайте вместе подумаем»

Отвечаю как кофаундер, и одно возражение у меня есть.

**Логика твоя верна, и я её принимаю целиком.** Внутренний рынок лаборатории закрыт для внешних. Внутренняя доска вакансий, реферралы, знакомство с нанимающими менеджерами и репутация появляются только у сотрудника. Год внутри стоит дороже года подач снаружи. Плюс твой второй выход, который я бы сам не назвал: изнутри ты поймёшь, интересна ли тебе компания, а это знание снаружи не купить. И третье, проверяемое: senior-планка лабораторий упирается не в твой стаж (у Anthropic медиана 12,2 года инженерии, ты проходишь стажем), а в отсутствие публичного AI-артефакта на твоё имя. Вход не на senior обходит именно этот барьер, пока артефакт строится.

**Возражение одно, и оно про буквальную трактовку.** Уборщик в Anthropic или OpenAI не сотрудник лаборатории. Facilities там отдан подрядчику (ABM, Aramark, SBM и подобные): человек оформлен в подрядчике, внутренней доски вакансий у него нет, реферралов нет, контур NDA другой. То есть буквальный уборщик даёт пропуск в здание, но не даёт вход в компанию, и всё то, ради чего ты туда идёшь, ему недоступно. Ты сам сказал «это очень утрирую», поэтому я так и прочитал: фигура речи. А исполняю как **любая штатная роль любого уровня, либо официальный contract-to-hire**. Захочешь буквально вендорскую позицию, скажи отдельно, из этой голосовой я такого вывода не делаю.

Вторая граница, которую я провёл сам: стажировки, new grad и campus оставил отсечёнными. Они адресованы студентам, подача человека с 20 годами опыта жжёт и заявку, и репутацию, и внутрь всё равно не ведёт. А вот **Anthropic Fellows Program я, наоборот, пропустил внутрь полосы**: это платная программа с конверсией в штат, то есть лучшая из доступных ног в двери. Я её сначала по ошибке отсёк вместе с мусором и вернул.

## Замер: чего мы реально не видели

Правило я не просто записал, а прогнал по живым доскам. Труба А **выбрасывала эти роли молча**: роль на доске лаборатории без нашего CV-кластера и без вилки от $200K доходила до строки `continue` и в базу не попадала вовсе.

| Лаборатория | видели | стало видеть | было невидимо |
|---|---|---|---|
| OpenAI | 652 | 830 | +178 |
| xAI | 36 | 252 | +216 |
| Mistral AI | 102 | 201 | +99 |
| Scale AI | 108 | 196 | +88 |
| Cohere | 78 | 141 | +63 |
| Anthropic | 556 | 618 | +62 |
| Cursor / Anysphere | 64 | 125 | +61 |
| Thinking Machines | 9 | 47 | +38 |
| Sarvam AI | 23 | 59 | +36 |
| Physical Intelligence | 4 | 34 | +30 |
| Midjourney | 1 | 18 | +17 |
| Runway ML | 29 | 44 | +15 |
| Reflection AI | 43 | 55 | +12 |
| остальные 10 лабораторий | 99 | 132 | +33 |
| **ИТОГО 23 лаборатории** | **1797** | **2752** | **+955** |

Вот что конкретно пряталось за этим `continue`:

- Anthropic: «AI Deployment Specialist, Beneficial Deployments» (SF/NY), три ветки Fellows Program, «Customer Success Manager» (London), «Compute Country Lead, Canada», «Contracts Manager, EMEA», «BDR Enablement Lead»
- OpenAI: «Senior Technical Program Manager - Security», «Software Engineer, Full Stack (People Innovation)», «Senior Support Engineer - Dublin», «IT Support Specialist», «Account Director, Startups»
- Thinking Machines: «Software Engineer, Systems Generalist», «Site Reliability Engineer, Post Training», «Network Engineer, Supercomputing», «Research, General Agents»
- Mistral: пять «Engineering Team Lead» (Fleet Delivery, Managed K8s, Storage, Sandbox), «AI Scientist - Agentic Engineering»

Обрати внимание на Mistral и Thinking Machines: там в невидимке оказались не ops-роли, а **обычные инженерные**. Наши кластеры заточены на FDE, DevRel, security, research и не ловят простое «Software Engineer» или «Engineering Team Lead». То есть дыра была шире, чем даже твоя голосовая.

## Два дефекта, которые вскрыл второй заход

Первую версию патча я открыл на весь `tier1`. Прогон по живым доскам дал **+2159 строк**, и в них Stripe +374, Databricks +324, хедж-фонды (point72, schonfeld, mangroup, drweng) +348. Это раздувание базы, а не вход в лабораторию. Сузил до явного списка из 23 имён.

Второй дефект: xAI отдавал 24 строки гиг-мельницы, в основном «AI Tutor» на 40 языков. Краудворк с оплатой за задачу это тот же вендорский контур, что аутсорсный клининг, который я сам же в правиле и запретил считать «внутрь». Отсёк.

## Где правило теперь живёт

| Дом | Файл |
|---|---|
| Библия (канон) | [reglament-vnutr-ii-laboratorii-lyuboy-cenoy-poziciya-ne-vazhna.md](D:/Vault/Vault-Knowledge/03-Insights/Operations/reglament-vnutr-ii-laboratorii-lyuboy-cenoy-poziciya-ne-vazhna.md), слова твои дословно, без купюр |
| Память | `get-inside-the-lab-at-any-position.md` + строка в INBOX `MEMORY.md` + спица в `hub-job-search.md` |
| Always-loaded | `CLAUDE.md` §9.14, версия v5.23.1 → **v5.24.0**, строка в журнале |
| Дверь (код) | `door_cluster()` в [jobs_discover.py](D:/Vault/_imports/jobs-watch/jobs_discover.py): `LAB_DOOR_CO` 23 имени, `LAB_JUNK_RX`, кластер `lab-door` score 4, CV-фолбэк `product` |
| Дверь (человек и Codex) | скилл `/apply` §1.1-бис, v2.1.0 → v2.2.0 |
| Сторож | `_test_jobs_discover.py` проверки L1–L9c, **40/40 OK, exit 0** |

Красный показан на сломанном коде, как положено: без ветки tier1 проверки L1 и L3 падали, exit 1. Отсечка мельницы тоже краснела до фикса (в регулярку попали настоящие байты backspace 0x08, известный класс этой папки, для него тут и лежит `_fix_backspace_patterns.py`). Соседние тесты `_test_batch_daily`, `_test_jobs_comp`, `_test_select_money` зелёные, парность CV-веток не сломана. Два коммита с трейлерами: `af918644`, `246412ce`.

**Порог $200K я не трогал.** Теперь две полосы, а не один список: лаборатория это вход, все остальные компании это деньги. Твой приказ от 24.09 цел.

## Долг, который я назвал, а не спрятал

1. У `lab-door` нет своей ветки CV, он падает на `product`. Для ops или support это «меньшее из неверных», а не попадание. Своя ветка это задача в `/cv`.
2. Гео-фильтр режет `lab-door` как всех: роль лаборатории вне целевых гео отсекается локацией. Релокация у нас на столе, так что это кандидат на пересмотр, но менять гео-политику одной голосовой про уровень роли я не стал.
3. **Google DeepMind и Meta Superintelligence в эту дверь физически не входят**: доска DeepMind закрыта (замер 08.09), Meta в списке досок нет вообще. Две крупнейшие лаборатории только руками и через людей, это отдельная задача.
4. Список `LAB_DOOR_CO` ручной, новая лаборатория сама в него не попадёт. Границу «лаборатория или нет» рисовал я: внутри оставил Scale AI, Cursor, Sarvam, снаружи Stripe, Databricks, Vercel, Glean, Granola, Synthesia и фонды. Хочешь кого-то передвинуть, это одна строка.

Наружу ничего не ушло: ни в группу 001, ни в 03, ни публично.

🔧 Вердикт о скилле: `/apply` обновил (v2.2.0, новый §1.1-бис). Боль была пережитая, а не гипотетическая: правило про отбор без двери в отборе не работало бы вовсе.

⚠️ `CLAUDE.md` 111KB, жёлтая зона (порог 100KB). Правило дописал, как велит §10.2, сжимать по ходу не стал, это работа суточного оптимизатора Маяка.

🧒 **Простыми словами:** ты сказал «в ИИ-лабораторию хочу попасть любым способом, хоть не начальником». Раньше наш робот смотрел на доску Anthropic и брал только большие должности с большой зарплатой, а всё остальное выбрасывал в мусор, даже не показав. Я посчитал: так пропадало 955 вакансий. Теперь он их складывает в отдельную полочку «нога в двери», и ты их видишь. Мусор с этой полочки я убрал: подработку «поговори с роботом на каталонском» туда не пускаю, и уборщика из клининговой фирмы тоже, потому что он работает не в лаборатории, а в другой фирме, и внутрь всё равно не попадает. А вот стажировку Fellows у Anthropic пускаю: оттуда берут в штат. Правило записал во все нужные тетрадки, робота починил, проверил, что до починки он ломался, а после работает.

---

**User:**

добавь DeepMind и Meta руками

---

**Claude:**

🚂 Рельса: делаю сам как Claude (сеть, код, тесты, канон). Чужие баки тут не нужны.

Сначала смотрю, что у нас про них уже записано и почему доска умерла.

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/jobs-watch\" && grep -rniE \"deepmind|meta|google\" jobs_spec_data.py | head -30", "description": "Find deepmind/meta entries in spec"}

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/jobs-watch\" && grep -n \"def url_for\" -A 30 jobs_spec_data.py", "description": "Read url_for adapter"}

---

**Claude:**

Обе в пролёте по разным причинам: DeepMind лежит в PRUNED с 404, Meta в спеке нет вообще. Ищу живые публичные ручки.

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/jobs-watch\" && timeout 240 python - <<'PY'\nimport urllib.request, json\nUA=\"Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 Chrome/126 Safari/537.36\"\ncands=[\n (\"gdm-careers-v3\",\"https://careers.google.com/api/v3/search/?q=&company=Google%2

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/jobs-watch\" && timeout 300 python - <<'PY'\nimport urllib.request, gzip, io, re, json\nUA=\"Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 Chrome/126 Safari/537.36\"\ndef get(u, data=None, hdr=None):\n    h={\"User-Agent\":UA,\"Accept\":\"*/*\",\

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/jobs-watch\" && timeout 300 python - <<'PY'\nimport urllib.request, gzip, re, html\nUA=\"Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 Chrome/126 Safari/537.36\"\ndef get(u):\n    r=urllib.request.Request(u,headers={\"User-Agent\":UA,\"Accept-Enc

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/jobs-watch\" && timeout 300 python - <<'PY'\nimport urllib.request, gzip, re, html\nUA=\"Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 Chrome/126 Safari/537.36\"\ndef get(u):\n    r=urllib.request.Request(u,headers={\"User-Agent\":UA,\"Accept-Enc

---

**Claude:**

Пока копаю ручки, отвечаю на второй вопрос: список организаций соберу ниже. Сначала доказываю, что DeepMind и Meta технически берутся.

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/jobs-watch\" && timeout 300 python - <<'PY'\nimport urllib.request, gzip, re, html\nUA=\"Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 Chrome/126 Safari/537.36\"\ndef get(u):\n    r=urllib.request.Request(u,headers={\"User-Agent\":UA,\"Accept-Enc

---

> `Bash` -- {"command": "timeout 240 python - <<'PY'\nimport urllib.request, gzip\nUA=\"Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 Chrome/126 Safari/537.36\"\ndef probe(u, data=None, hdr=None):\n    h={\"User-Agent\":UA,\"Accept-Encoding\":\"gzip\",\"Accept\":\"*/*\"}\n    if hdr: h.update(hdr

---

**Claude:**

DeepMind взят: ссылки собираются и отдают 200. Meta бьёт 400 на голый urllib, пробую полный браузерный набор заголовков.

---

> `Bash` -- {"command": "timeout 240 python - <<'PY'\nimport urllib.request, gzip, zlib, re\nH={\"User-Agent\":\"Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/10.0.0.0 Safari/537.36\",\n   \"Accept\":\"text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,im

---

> `Bash` -- {"command": "timeout 300 python - <<'PY'\nimport urllib.request, gzip, zlib, re, json\nH={\"User-Agent\":\"Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/10.0.0.0 Safari/537.36\",\n   \"Accept\":\"text/html,application/xhtml+xml,*/*;q=0.8\",\"Accept-Language

---

**Claude:**

Вердикт по Meta: публичным GET её список не берётся (GraphQL с `doc_id` и токенами, бот-гейт). Не «невозможно», а «я не нашёл публичной ручки» — поэтому Meta пойдёт ручной полосой, ровно как ты и сказал. DeepMind делаю механически.

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/jobs-watch\" && grep -n \"^PAT\\|^GH_CONTENT\\|def items\\|def norm\" -A 22 jobs_spec_data.py | sed -n '1,90p'", "description": "Read PAT, items, norm adapters"}

---

**Claude:**

Дверь для обоих делаю отдельным модулем, чтобы не лезть в хрупкий цикл `run()`.

---

> `Write` -- {"file_path": "D:\\Vault\\_imports\\jobs-watch\\lab_hand.py", "content": "#!/usr/bin/env python3\n\"\"\"lab_hand.py — Труба А, РУЧНАЯ ПОЛОСА лабораторий: доски, которых нет в jobs_spec_data.VERIFIED.\n\nЗачем (приказ оператора 27.09.2026, голосом «добавь DeepMind и Meta руками»): правило\n«внутрь ИИ

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/jobs-watch\" && python - <<'PY'\nimport io\np='jobs_discover.py'; s=io.open(p,encoding='utf-8').read()\ns=s.replace('''    \"Twelve Labs\", \"Cursor / Anysphere\",\n})''','''    \"Twelve Labs\", \"Cursor / Anysphere\",\n    # Ручная полоса lab_hand.py: досок в 

---

**Claude:**

Тест для новой полосы — с красным на сломанном парсере.

---

> `Write` -- {"file_path": "D:\\Vault\\_imports\\jobs-watch\\_test_lab_hand.py", "content": "#!/usr/bin/env python3\n\"\"\"Тесты чистых функций lab_hand.py (0 сети). Прогон: python _test_lab_hand.py\n\nКрасный показан 27.09.2026 на коде до парсера (parse_gcareers отсутствовал -> H1..H4 FAIL)\nи на сломанном C

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/jobs-watch\" && python _test_lab_hand.py; echo \"EXIT=$?\"", "description": "Run lab_hand tests"}

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/jobs-watch\" && cp lab_hand.py /tmp/lh_good.py && python -c \"\nimport io\np='lab_hand.py'; s=io.open(p,encoding='utf-8').read()\ns=s.replace('<h3 class=\\\\\\\\\\\"QJPWVe\\\\\\\\\\\">','<h3 class=\\\\\\\\\\\"ZZZZZZ\\\\\\\\\\\">',1)\nio.open(p,'w',encoding='utf

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/jobs-watch\" && python _test_lab_hand.py 2>&1 | grep -E \"FAIL\"; echo \"---\"; diff <(cat /tmp/lh_good.py) lab_hand.py && echo \"файл идентичен бэкапу\"; ls -la lab_hand.json 2>/dev/null", "description": "Diagnose remaining failure"}

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/jobs-watch\" && grep -n \"QJPWVe\\|ZZZZZZ\" lab_hand.py _test_lab_hand.py | head", "description": "Check regex class in files"}

---

**Claude:**

Регулярка испортилась при откате: в raw-строке остались экранированные кавычки. Правлю.

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/jobs-watch\" && python - <<'PY'\nimport io\np='lab_hand.py'; s=io.open(p,encoding='utf-8').read()\nbad = 'r\"ssk=' + chr(39) + chr(92) + 'd+:(' + chr(92) + 'd+)' + chr(39) + '.*?<h3 class=' + chr(92) + '\"QJPWVe' + chr(92) + '\">(.*?)</h3>.*?class=' + chr(92) +

---

**Claude:**

Зелёное. Боевой прогон DeepMind.

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/jobs-watch\" && timeout 420 python lab_hand.py run --pages 6 2>&1 | tail -8; echo \"=== что легло ===\"; timeout 120 python lab_hand.py stats 2>&1 | head -12", "description": "Run lab_hand for DeepMind"}

---

**Claude:**

DeepMind в базе: 73 карточки, 70 ролей. Теперь Meta руками через браузер.

---

> `mcp__Claude_Browser__preview_start` -- {"url": "https://www.metacareers.com/jobs?q=&sort_by_new=true"}

---

> `mcp__Claude_Browser__get_page_text` -- {"max_chars": 6000}

---

> `mcp__Claude_Browser__javascript_tool` -- {"action": "javascript_exec", "text": "(() => { const a=[...document.querySelectorAll('a[href*=\"/jobs/\"]')].map(x=>({h:x.getAttribute('href'), t:(x.innerText||'').split('\\n')[0].trim().slice(0,80)})).filter(x=>/\\/jobs\\/\\d+/.test(x.h)); return JSON.stringify({count:a.length, sample:a.slice(0,6)

---

> `mcp__Claude_Browser__javascript_tool` -- {"action": "javascript_exec", "text": "(() => { const as=[...document.querySelectorAll('a')].map(x=>x.getAttribute('href')||'').filter(Boolean); const uniq=[...new Set(as)]; const jobs=uniq.filter(h=>/job/i.test(h)); return JSON.stringify({total:uniq.length, jobish:jobs.slice(0,25)}); })()"}

---

> `mcp__Claude_Browser__javascript_tool` -- {"action": "javascript_exec", "text": "(() => { const a=document.querySelector('a[href^=\"/profile/job_details/\"]'); if(!a) return 'нет карточек'; const box=a.closest('div'); return JSON.stringify({href:a.getAttribute('href'), aText:(a.innerText||'').slice(0,200), boxText:(box?box.innerText:'').sli

---

> `mcp__Claude_Browser__browser_batch` -- {"actions": [{"name": "navigate", "input": {"url": "https://www.metacareers.com/jobs?q=superintelligence"}}, {"name": "javascript_tool", "input": {"action": "javascript_exec", "text": "(()=>{const out=[...document.querySelectorAll('a[href^=\"/profile/job_details/\"]')].map(a=>{const L=(a.innerText||

---

> `mcp__Claude_Browser__browser_batch` -- {"actions": [{"name": "computer", "input": {"action": "wait", "duration": 3}}, {"name": "find", "input": {"query": "search by technology team location input"}}]}

---

> `mcp__Claude_Browser__javascript_tool` -- {"action": "javascript_exec", "text": "(()=>{const n=document.querySelectorAll('a[href^=\"/profile/job_details/\"]').length;const inp=[...document.querySelectorAll('input')].map(i=>({ph:i.placeholder||'',type:i.type}));return JSON.stringify({cards:n,url:location.href,inputs:inp});})()"}

---

**Claude:**

Нашёл рабочий путь: `/jobsearch/?q=`. Собираю целевой срез Meta.

---

> `mcp__Claude_Browser__browser_batch` -- {"actions": [{"name": "javascript_tool", "input": {"action": "javascript_exec", "text": "(()=>{const out=[...document.querySelectorAll('a[href^=\"/profile/job_details/\"]')].map(a=>{const L=(a.innerText||'').split('\\n').map(s=>s.trim()).filter(Boolean);return {url:'https://www.metacareers.com'+a.ge

---

> `mcp__Claude_Browser__browser_batch` -- {"actions": [{"name": "navigate", "input": {"url": "https://www.metacareers.com/jobsearch/?q=superintelligence&page=2"}}, {"name": "computer", "input": {"action": "wait", "duration": 4}}, {"name": "javascript_tool", "input": {"action": "javascript_exec", "text": "(()=>{const out=[...document.querySe

---

**Claude:**

Кладу собранное в ручную полосу.

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/jobs-watch\" && python - <<'PY'\nimport io\np='jobs_discover.py'; s=io.open(p,encoding='utf-8').read()\ns=s.replace('\"Google DeepMind\", \"Meta Superintelligence Labs\",',\n            '\"Google DeepMind\", \"Meta Superintelligence Labs\", \"Meta\",',1)\nio.op

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/jobs-watch\" && python _test_jobs_discover.py 2>&1 | grep FAIL", "description": "See which discover test fails"}

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/jobs-watch\" && python - <<'PY'\nimport io\np='_test_jobs_discover.py'; s=io.open(p,encoding='utf-8').read()\ns=s.replace('_HAND_ONLY = set(_LH.GCAREERS) | {\"Meta Superintelligence Labs\"}',\n '# Имена ручной полосы берём ИЗ НЕЁ САМОЙ, а не списком в тесте: ин

---

**Claude:**

Теперь твой второй вопрос. Составил список кандидатов и прозондировал их доски.

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/jobs-watch\" && grep -n \"_load_extra\" -A 18 jobs_spec_data.py | head -30; ls -la boards_extra.json 2>/dev/null | head -2; python -c \"\nimport json,os\np='boards_extra.json'\nif os.path.exists(p):\n    d=json.load(open(p,encoding='utf-8'))\n    print('тип:',t

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/jobs-watch\" && timeout 560 python - <<'PY'\nimport urllib.request, json, time\nfrom jobs_spec_data import PAT, VERIFIED, PRUNED, items\nUA=\"Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 Chrome/126 Safari/537.36\"\nhave={(a,s.lower()) for _,a,s,

---

**Claude:**

Главная находка: почти все кандидаты **уже в спеке**, просто стоят как tier2/tier3, поэтому в полосу «ноги в двери» не попадают. То есть добирать надо не доски, а список лабораторий. Смотрю тиры.

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/jobs-watch\" && python - <<'PY'\nfrom jobs_spec_data import VERIFIED\nimport jobs_discover as J\nnames=[\"Cognition\",\"Poolside\",\"Harvey\",\"Sierra\",\"Decagon\",\"ElevenLabs\",\"Suno\",\"Luma\",\"Together\",\n\"Fireworks\",\"Modal\",\"Baseten\",\"LangChain\

---

**Claude:**

Дверь оказалась с ловушкой: она требовала И tier1, И список. Значит промоушен tier2-лабораторий не сработал бы. Убираю лишнее условие, список становится единственной правдой.

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/jobs-watch\" && python - <<'PY'\nimport io\np='jobs_discover.py'; s=io.open(p,encoding='utf-8').read()\n# 1) tier больше не ворота: правда одна — список лабораторий\nold='''    if tier == \"tier1\" and company in LAB_DOOR_CO:\n        if LAB_JUNK_RX.search(t):\

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/jobs-watch\" && python -c \"\nfrom jobs_spec_data import VERIFIED\nfor co,ats,slug,t in VERIFIED:\n    if slug.lower() in ('dust','poolside','axiommath','1x','figure'): print(repr(co),ats,slug,t)\n\"; grep -n '(\"Google DeepMind\",\"greenhouse\",\"deepmind\")' 

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/jobs-watch\" && python -c \"\nfrom jobs_spec_data import VERIFIED,PRUNED\nprint([ (c,a,s,t) for c,a,s,t in VERIFIED if 'pool' in (c+s).lower()])\nprint('PRUNED:',[x for x in PRUNED if 'pool' in str(x).lower()][:3])\n\"", "description": "Locate poolside entry"}

---

**Claude:**

Важное: Poolside лежит в PRUNED, и причина отсечки была «нет ролей в 8 кластерах оператора» — ровно тот критерий, который новое правило отменяет. Проверяю весь PRUNED на лаборатории.

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/jobs-watch\" && python - <<'PY'\nfrom jobs_spec_data import PRUNED\nimport re\nRX=re.compile(r\"\\b(ai|ml|labs?|intelligence|robot|neural|model|agent|cognit|gpt|llm)\\b|\"\n              r\"ai$|\\.ai|poolside|magic|imbue|adept|sakana|kyutai|goodfire|transluce|m

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/jobs-watch\" && grep -rn \"PRUNED\" _test_*.py | head -5; grep -n '^VERIFIED\\|^PRUNED' jobs_spec_data.py; sed -n '755,765p' jobs_spec_data.py", "description": "Check VERIFIED/PRUNED structure and tests"}

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/jobs-watch\" && sed -n '108,112p' jobs_spec_data.py && python - <<'PY'\nimport io\np='jobs_spec_data.py'; s=io.open(p,encoding='utf-8').read()\nanchor='VERIFIED=[\\n'\nadd = ''' # --- полоса «нога в двери ИИ-лаборатории» (приказ оператора 27.09.2026, голосом) ---\

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/jobs-watch\" && python _test_jobs_discover.py 2>&1 | grep FAIL", "description": "See failing test"}

---

**Claude:**

Ожидаемо: L2 проверял снятое условие. Переписываю его под новую семантику явно.

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/jobs-watch\" && python - <<'PY'\nimport io\np='_test_jobs_discover.py'; s=io.open(p,encoding='utf-8').read()\nold='''cl, s = door_cluster(\"Facilities Coordinator\", \"tier2\", None, \"Anthropic\")\nchk(\"L2 та же роль на НЕ-tier1 доске по-прежнему отбрасываетс

---

**Claude:**

Всё зелёное (42 проверки). Финальный замер: сколько ролей полоса видит теперь по всем 60 организациям.

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/jobs-watch\" && timeout 580 python - <<'PY'\nimport jobs_discover as J\nfrom jobs_spec_data import VERIFIED, norm, items, comp, url_for\nimport json\nrows=[]; T=[0,0,0]\nfor company, ats, slug, tier in VERIFIED:\n    if company not in J.LAB_DOOR_CO: continue\n 

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/jobs-watch\" && python -c \"\nfrom jobs_spec_data import VERIFIED\nprint([r for r in VERIFIED if r[0]=='Axiom'])\n\"", "description": "Check Axiom duplicate"}

---

**Claude:**

Имя `Axiom` уже занято другой конторой: полоса зацепила бы чужую. Развожу.

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/jobs-watch\" && python - <<'PY'\nimport io\np='jobs_spec_data.py'; s=io.open(p,encoding='utf-8').read()\ns=s.replace(' (\"Axiom\",\"ashby\",\"axiommath\",\"tier2\"),',\n ' (\"Axiom Math\",\"ashby\",\"axiommath\",\"tier2\"),   # имя «Axiom» в спеке уже занято др

---

**Claude:**

Всё зелёное. Коммичу и обновляю канон.

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports\" && git add jobs-watch/jobs_discover.py jobs-watch/jobs_spec_data.py jobs-watch/lab_hand.py jobs-watch/_test_lab_hand.py jobs-watch/_test_jobs_discover.py && git commit -q -F - <<'MSG'\njobs-watch: DeepMind и Meta руками + полоса ноги в двери расширена до 60 о

---

> `Bash` -- {"command": "python - <<'PY'\nimport io\n# Библия\np=\"D:/Vault/Vault-Knowledge/03-Insights/Operations/reglament-vnutr-ii-laboratorii-lyuboy-cenoy-poziciya-ne-vazhna.md\"\ns=io.open(p,encoding='utf-8').read()\ns=s.replace(\"(машинная истина = ЯВНЫЙ список `jobs_discover.LAB_DOOR_CO`, 23 имени: An

---

> `Bash` -- {"command": "python - <<'PY'\nimport io\n# CLAUDE.md\np=r\"C:\\Users\\dev\\.claude\\CLAUDE.md\"\ns=io.open(p,encoding='utf-8').read()\nold=\"(явный список `LAB_DOOR_CO`, 23 имени: Anthropic · OpenAI · xAI · Mistral · Thinking Machines · Inflection · Cohere · Scale AI · Reflection · Physical Intell

---

> `Bash` -- {"command": "cd \"C:/Users/dev/.claude/projects/P---WORKDIR-HUB/memory\" && python - <<'PY'\nimport io\np='MEMORY.md'; s=io.open(p,encoding='utf-8').read()\ns=s.replace(\"- [Внутрь ИИ-лабы любой ценой](get-inside-the-lab-at-any-position.md) — ⭐27.09 уровень роли и порог $200K не фильт

---

**Claude:**

🕐 27.09.2026, 09:32

## DeepMind и Meta внутри

Обе взяты, но разными путями, потому что технически они разные.

**Google DeepMind — механически.** Их старая доска `boards-api/deepmind` отдаёт 404 с 24.08, я перепроверил сегодня: всё ещё 404. JSON-ручек у Google я не нашёл (`careers.google.com/api/v3` и `applications/api/v3` оба 404). Зато страница результатов careers-сайта отдаётся сервером целиком, и вакансии там в HTML. Написал парсер карточек и сборку ссылки. Прогнал: **73 карточки, 70 ролей легли в базу** (34 research, 29 нога в двери, остальное по кластерам), 3 отброшены как стажировки и мимо гео. Ссылки проверил, отдают 200.

**Meta — руками, как ты и сказал.** Публичного GET у них нет: `metacareers.com` открывается только с полным браузерным набором заголовков, а сам список приезжает POST-запросом GraphQL с `doc_id` и токенами сессии. Это «я не нашёл публичную ручку», а не «её не существует. Поднял браузер, прошёл по восьми запросам и снял **48 ролей**, из них 19 именно Meta Superintelligence Labs и FAIR:

| Что снял с Meta | Примеры |
|---|---|
| MSL и FAIR, 19 | AI Research Scientist — MSL (Technical Leadership) · AI Research Manager — MSL · Staff Research Scientist, FAIR (RL/LLM), Париж · Research Scientist, FAIR Core Learning and Reasoning, Париж · AI Research Scientist, Pre-training Data — MSL FAIR · Technical Program Manager-MSL · Data Engineer, MSL (Privacy) · Data Scientist, MSL (Safety) · MSL Special Projects Lead · Finance Manager, MSL FP&A · Content Engineer, MSL · Product Designer, MSL |
| Прочая Meta, 29 | Forward Deployed Engineer, Enterprise AI (Сингапур) · Security Engineer, Applied AI · Software Engineer, Systems ML Engineering · Research Scientist, Physical AI (Нью-Йорк) · Business Support Engineer BizAI (Дублин) · четыре Technical Program Manager по AI · Business Operations, Infrastructure (Лондон) · Member of Product Staff |

Они не обновляются сами. Это честная цена ручной полосы: раз в неделю роли надо переснимать браузером, команда `lab_hand.py add` для этого и сделана.

## По дороге нашёл ловушку в собственной двери

Полоса требовала **и** tier1 доски, **и** имя в списке лабораторий. А половина наших лабораторий лежит в спеке как tier2 и tier3: Perplexity, Together AI, Harvey, Sierra, Cognition, ElevenLabs, Decagon, Baseten, Lovable, Dust, Etched. То есть утром я записал правило, которое их молча не касалось. Условие про тир снял, теперь единственная правда о том, лаборатория это или нет, это список имён.

Вторая мелочь оттуда же: полоса ходит по имени компании, а имя `Axiom` в спеке уже носит другая контора. Завёл ИИ-лабораторию как `Axiom Math`, чтобы тёзку не зацепило, и поставил на это тест.

## Твой вопрос: кого ещё добавить

Прозондировал 62 кандидата живым GET. Главное открытие: **почти все они уже были в нашей спеке**, просто стояли низким тиром и в полосу не попадали. То есть добирать надо было не доски, а список. Расширил с 23 до 60 организаций:

| Полка | Организации |
|---|---|
| frontier-лаборатории | Anthropic · OpenAI · xAI · Mistral · Thinking Machines · Inflection · Cohere · Reflection · Nous Research · Reka · Black Forest Labs · Liquid AI · Stability · Midjourney · Sarvam · **Moonshot AI** (новая) |
| прикладные ИИ и стартапы | Scale AI · Cursor · **Perplexity** · **Together AI** · **Fireworks** · **Modal** · **Baseten** · **Anyscale** · **LangChain** · **Weights & Biases** · **Glean** · **Notion** · **Cognition** · **Poolside** · **Harvey** · **Sierra** · **Decagon** · **Dust** · **H Company** · **Lovable** · **ElevenLabs** · **Suno** · **Luma AI** · Runway · **Synthesia** · Twelve Labs · Character.AI · World Labs · Physical Intelligence · Prime Intellect · **OpenEvidence** |
| железо и вычисление под ИИ | **Etched** · **SambaNova** · **Extropic** (новая) · **Normal Computing** (новая) |
| наука и безопасность | **Isomorphic Labs** · **Allen Institute for AI** (новая) · **Chai Discovery** (новая) · **Axiom Math** (новая) |
| робототехника | **Figure AI** (новая) · **1X** (новая) |
| ручной полосой | **Google DeepMind** · **Meta** · **Meta Superintelligence Labs** |

Жирным то, чего в полосе утром не было. Восемь досок добавил в спеку заново: AI2 (19 ролей), Extropic (10), Normal Computing (19), Chai Discovery (17), Figure AI (16), 1X (92), Moonshot (4), Axiom Math (1).

Ещё вернул **Poolside** из мусорного списка. Его выкинули с формулировкой «ни одной роли из 8 кластеров оператора» — ровно тот критерий, который твоё правило и отменяет. Весь мусорный список из 194 досок я на ИИ-имена пересмотрел, других кандидатов там нет.

**Замер после всего** по 57 живым доскам полосы:

| Организация | видели | +нога в двери | Организация | видели | +нога в двери |
|---|---|---|---|---|---|
| xAI | 36 | **+216** | Baseten | 45 | +56 |
| OpenAI | 652 | **+178** | Decagon | 88 | +56 |
| Harvey | 140 | **+164** | LangChain | 50 | +52 |
| Mistral | 102 | +99 | Lovable | 27 | +52 |
| Scale AI | 108 | +88 | SambaNova | 9 | +52 |
| ElevenLabs | 123 | +84 | Glean | 83 | +47 |
| Notion | 45 | +78 | Together AI | 24 | +42 |
| Cognition | 26 | +76 | Thinking Machines | 9 | +38 |
| Etched | 23 | +70 | Perplexity | 81 | +37 |
| Sierra | 133 | +69 | Sarvam | 23 | +36 |
| 1X | 23 | +67 | Physical Intelligence | 4 | +30 |
| Anthropic | 556 | +63 | Synthesia | 23 | +27 |
| Cohere | 78 | +63 | Isomorphic Labs | 7 | +24 |
| Cursor | 64 | +61 | остальные 29 | 618 | +159 |
| **ИТОГО 60 организаций** | **2986** | **+2159** | плюс ручная полоса | | **+118** |

Гиг-мельницы («AI Tutor» на 40 языков и аналоги) отсечено 30 строк.

**Кого хотел добавить и не смог.** Публичной ручки я не нашёл у: Safe Superintelligence (борд Ashby существует, но пустой), Magic, Groq, Cerebras, Hugging Face, Contextual AI, AI21, Imbue, EvolutionaryScale, Goodfire, Transluce, METR, Apollo Research, Redwood Research, EleutherAI, Sakana AI, Kyutai, Windsurf и Codeium, Skild AI, Periodic Labs, Abridge. У части из них найм идёт формой на своём сайте или вообще через людей. Их место теперь есть: та же ручная полоса, что у Meta. Скажи «возьми и этих руками», и я пройду по ним браузером так же, как по Meta.

## Состояние и долг

Тесты: `_test_jobs_discover.py` **42 из 42** (L1–L9e), новый `_test_lab_hand.py` **16 из 16** (H1–H15, красный я показал на сломанном парсере: классы Google подменил, H1/H2/H2b упали, exit 1). Шесть соседних тестов зелёные. Коммиты `af918644`, `246412ce`, `1eddf2ec` с трейлерами. Канон обновлён: Библия v1.1.0, CLAUDE.md §9.14 (v5.24.1), `/apply` §1.1-бис, память и хаб.

Долг называю честно:

1. DeepMind держится на обфусцированных CSS-классах Google. Сменятся — парсер вернёт ноль карточек и **скажет это вслух**, а не притворится успехом. Это осознанный выбор, JSON-ручки у них нет.
2Ъ Meta не обновляется сама, роли переснимает браузер.
3. `lab_hand.json` не в git (там в whitelist только `*.py`), едет Syncthing'ом. Роли Meta живут на этой машине и доедут до остальных синком.
4. Список из 60 имён ручной: новая лаборатория сама в него не попадёт.
5. +2159 новых строк лягут в базу ближайшим ночным прогоном `pipe-a-discover`. Я его руками не запускал: это 828 досок, его работа ночная.

🔧 `/apply` обновил второй раз за день (новая дверь `lab_hand.py` описана в §1.1-бис). Наружу ничего не ушло.

🧒 **Простыми словами:** ты попросил добавить две самые большие лаборатории. DeepMind получилось добавить по-нормальному: их объявления лежат на страничке Google, я научил робота её читать, взял 70 вакансий. Meta спряталась: её список отдаётся только настоящему браузеру, поэтому я открыл браузер сам, руками переписал 48 вакансий и сделал для них отдельную тетрадку, куда можно дописывать ещё. По пути нашёл, что моя утренняя починка была с изъяном: она смотрела только на «важные» доски, а половина лабораторий у нас числится неважными, и они пролетали мимо. Убрал это лишнее условие. Потом ты спросил, кого ещё добавить: я проверил 62 конторы и оказалось, что почти все у нас уже есть, только не отмечены как лаборатории. Отметил, теперь их 60, и робот стал видеть на 2159 вакансий больше.

---

**User:**

<command-message>QQQ</command-message>
<command-name>/QQQ</command-name>

---

**User:**

Base directory for this skill: C:\Users\dev\.claude\skills\QQQ

# /QQQ

Прочитай целиком [общий скилл continue](../continue/SKILL.md) и выполни его в текущем контексте. Передай все пользовательские аргументы без потерь. Это вход в ту же процедуру, не отдельная задача и не команда пересказать промпт. Если общий файл недоступен, восстанови доступ либо честно назови проблему; не выдумывай его содержимое.

**Что означает сама буква** (оператор, голосом, 06.10.2026): «QQQ означает быть как кофаундер, думать как кофаундер, быть проактивным, иметь активную жизненную позицию, [искать] корни; если проблемы не решаются в этой сессии — делать параллельные сессии». Поэтому `/QQQ` — не «сделай ещё шаг», а «веди задачу как совладелец»: сам выбирай следующий разрыв, сам чини причину, сам поднимай параллельную сессию под отдельную часть.

**Голос кофаундера, спор с ошибкой, якорь цели и правка постановки** — раздел «Роль: кофаундер и оппонент» общего скилла. Он лежит там, а не здесь, нарочно: шесть соседних входов и каждый толчок робота-проталкивалки читают только общий файл, и правило, записанное в алиас, для них молча выключено (замер 06.10.2026, сторож `_test_continue_role_shared.py`).

**Три захода за сессию идут автоматически** — раздел «0-тер» общего скилла: самозаход запускается по закрытому этапу или перед финальным ответом, считается прибором `qqq_auto.py`, и четвёртый заход уходит в ретро-дистилляцию. Толчка от оператора для этого ждать не надо.

Голое QQQ остаётся подтверждением; `/QQQ` не выдаёт согласие и не расширяет полномочия: Tier-2 (деньги, необратимое удаление, юридическая подпись, секреты третьим лицам, массовая рассылка) по-прежнему решает оператор.

---

**Claude:**

🕐 24.10.2026, время уточню прибором. Сессия H79620, хаб HUB-01.

Сессия возобновлена через 26 дней после работы 27.09. Прежде чем что-то делать, сверяю живое: статусы в контексте протухли, и файлы полосы правили без меня.

---

> `Bash` -- {"command": "cd \"C:/Users/dev/.claude/scripts\" && timeout 120 python voice001_collaboration.py describe --session-id s_a5230cc4 --wait-seconds 0 2>&1 | head -30", "description": "Run 001 collaboration classification"}

---

> `Bash` -- {"command": "powershell -NoProfile -Command \"(Get-Date).ToString('dd.MM.yyyy HH:mm')\" 2>&1; cd \"C:/Users/dev/.claude/scripts\" && timeout 120 python rail_plan.py declare --self \"канон и дверь полосы lab-door: код трубы А, тесты, Библия, память, скилл /apply; браузерный съём Meta\" --outsource 

---

**Claude:**

001: `unverified`, сессия не в карте, пиров нет. Работаю сам, пробу повторю на чекпоинте. Рельсы объявлены.

Теперь живой замер полосы, которую строили 27.09: что с ней стало за 26 дней.

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports\" && git log --oneline --since=2026-09-27 -- jobs-watch/lab_hand.py jobs-watch/jobs_discover.py 2>&1 | head -20; echo \"=== кто зовёт lab_hand ===\"; grep -rln \"lab_hand\" \"C:/Users/dev/.claude/skills\" \"C:/Users/dev/.claude/scripts\" \"D:/Vault/_impo

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/jobs-watch\" && timeout 180 python - <<'PY'\nimport sqlite3, json, os, datetime\nc=sqlite3.connect(\"jobs.db\")\nprint(\"=== ручная полоса (gcareers + hand) ===\")\nfor r in c.execute(\"SELECT ats, company, COUNT(*), SUM(status='new'), SUM(status='applied') FRO

---

**Claude:**

Полоса живёт: 5767 ролей `lab-door`, 430 подач, поток ежедневный (46 штук 18.10, 12 вчера, 6 сегодня). Но в ней дыра ровно там, где я строил.

| Что | Ролей | Подач за 27 дней | last_seen |
|---|---|---|---|
| Google DeepMind (`gcareers`) | 70 | **0** | **27.09**, доску ни разу не перечитывали |
| Meta + MSL (`hand`) | 48 | **0** | роли от 27.09 |
| Чужие добавления в ту же полосу (Fleet AI, Zep, GovAI, Constellation) | 28 | 2 | 23.10 |

Две крупнейшие лаборатории в базе есть, а подач по ним ноль. Копаю причину.

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/jobs-watch\" && grep -n \"ats IN\\|ats in (\" batch_daily.py | head -10; echo \"=== кто умеет подавать: движки ===\"; ls apply_engines/ 2>/dev/null; echo \"=== упоминания gcareers/hand вне lab_hand ===\"; grep -rln \"gcareers\" --include=*.py . 2>/dev/null | he

---

> `Bash` -- {"command": "cd \"C:/Users/dev/.claude\" && timeout 100 python scripts/routine_rights_census.py list 2>/dev/null | grep -iE \"discover|apply|jobs\" | head -10; echo \"=== задачи ОС с jobs ===\"; powershell -NoProfile -Command \"Get-ScheduledTask | Where-Object {\\$_.TaskName -match 'pipe|jobs|appl

---

> `Bash` -- {"command": "cat \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_a5230cc4/tasks/blsdhc7lx.output\" 2>&1 | head -30", "description": "Read background git/caller output"}

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/jobs-watch\" && sed -n '1,45p' selenium_apply/manual_lane.py 2>&1", "description": "Read manual_lane docstring"}

---

**Claude:**

Нашёл чужую работу поверх моей: 22.10 построена ручная полоса `manual_lane.py` и рутина `labdoor-ambassador-apply-NODE-0X`. Проверяю, доходят ли до неё именно DeepMind и Meta, и кто зовёт `lab_hand`.

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/jobs-watch\" && grep -n \"gcareers\\|'hand'\\|\\\"hand\\\"\" selenium_apply/manual_lane.py | head -15; echo \"=== RAILS/ats-фильтр manual_lane ===\"; grep -n \"ats IN\\|RAILS\\|rails\" selenium_apply/manual_lane.py | head -10", "description": "Check manual_lane

---

> `Bash` -- {"command": "powershell -NoProfile -Command \"(Get-ScheduledTask -TaskName 'pipe-a-discover').Actions | Select-Object Execute,Arguments | Format-List\" 2>&1 | head -20; echo \"=== последний запуск ===\"; powershell -NoProfile -Command \"Get-ScheduledTaskInfo -TaskName 'pipe-a-discover' | Select-Obje

---

**Claude:**

Корень найден и он мой. Задача `pipe-a-discover` запускает только `jobs_discover.py run` и `pipe_a_sheet.py`. `lab_hand.py` не зовёт **никто** — ни одна рутина. А 27.09 я написал в Библию, что он «дёргается каждым ночным прогоном рутины pipe-a-discover». Это был claim без улики, и он 27 дней держал ленту DeepMind замороженной.

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/jobs-watch\" && grep -n \"want\" selenium_apply/manual_lane.py | head -12; echo \"=== свежие файлы ручной полосы в волте ===\"; ls -t \"D:/Vault/Vault-Knowledge/04-Projects/Pipe-A-Batches/\" 2>/dev/null | grep -i manual | head -5", "description": "Check manu

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/jobs-watch\" && sed -n '50,75p' selenium_apply/manual_lane.py; echo \"=== шапка файла DeepMind 23.10 ===\"; head -14 \"D:/Vault/Vault-Knowledge/04-Projects/Pipe-A-Batches/manual-lane-deepmind-2026-10-23.md\" 2>&1", "description": "Read WHY_MANUAL and deepmin

---

**Claude:**

Вторая дыра: в `WHY_MANUAL` есть `gcareers`, но **нет `hand`** — значит 48 ролей Meta не могут попасть в ручную полосу вообще. А список DeepMind от 23.10 собирали из ленты, замороженной 27.09: 3 роли из 70 устаревших.

Чиню всё три звена. Сначала бэкап задачи и перечитка ленты.

---

> `Bash` -- {"command": "mkdir -p \"E:/!CLAUDE-HUBPC-June26/_app-backups\" && powershell -NoProfile -Command \"Export-ScheduledTask -TaskName 'pipe-a-discover' | Out-File -Encoding utf8 'E:\\!CLAUDE-HUBPC-June26\\_app-backups\\pipe-a-discover-h79620-20261024.before.xml'\" 2>&1 | head -3; ls -la \"E:/!

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/jobs-watch\" && timeout 500 python lab_hand.py run --pages 6 2>&1 | tail -8", "description": "Refresh lab_hand feed", "timeout": 540000}

---

**Claude:**

База занята: ночной `pipe-a-discover` стартовал в 05:30 и ещё держит `jobs.db`. Это само по себе улика — модуль падал бы и в составе рутины. Лечу заодно и это.

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/jobs-watch\" && python - <<'PY'\nimport io\np='lab_hand.py'; s=io.open(p,encoding='utf-8').read()\nold='    conn = sqlite3.connect(db)\\n    J.ensure_schema(conn)\\n    today = datetime.date.today().isoformat()'\nnew=('    # timeout=120: ночной pipe-a-discover 

---

**Claude:**

Хук прав: правлю файлом, а не heredoc'ом.

---

> `Write` -- {"file_path": "C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_a5230cc4\\scratchpad\\patch_h79620.py", "content": "#!/usr/bin/env python3\n\"\"\"Патч H79620 (24.10.2026): две починки полосы lab-door.\n\n1. lab_hand.py: sqlite3.connect(db, tim

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/jobs-watch\" && python \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_a5230cc4/scratchpad/patch_h79620.py\"; echo \"exit=$?\"; python -c \"\nimport sys; sys.path.insert(0,'selenium_apply'); sys.path.insert(0,

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/jobs-watch\" && for t in _test_lab_hand.py _test_jobs_discover.py selenium_apply/_test_manual_lane.py; do printf \"%-34s \" \"$t\"; timeout 180 python $t >/dev/null 2>&1 && echo PASS || echo \"FAIL(exit=$?)\"; done; echo \"=== ночная рутина ещё жива? ===\"; pow

---

**Claude:**

`_test_jobs_discover.py` красный, и это не от моей правки. Смотрю, что именно.

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/jobs-watch\" && timeout 180 python _test_jobs_discover.py 2>&1 | grep -E \"^FAIL|Traceback|Error\" | head -10; echo \"---всего OK---\"; timeout 180 python _test_jobs_discover.py 2>&1 | grep -c \"^OK\"", "description": "See which discover tests fail"}

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/jobs-watch\" && python -c \"\nimport sys; sys.path.insert(0,'.')\nimport jobs_discover as J, jobs_spec_data as S, lab_hand as LH\nspec={r[0] for r in S.VERIFIED}\nhand=set(LH.GCAREERS)|{r.get('company') for r in LH.hand_rows()}\nmiss=sorted(J.LAB_DOOR_CO - spec

---

**Claude:**

Красный сторож — это мой же L9c, и он работает: список лабораторий вырос с 60 до **189** организаций, и у четырёх из них нет дома ни на доске, ни в ручной полосе. Значит эти лаборатории в правиле есть, а в трубе их нет. Ищу им доски.

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/jobs-watch\" && timeout 400 python - <<'PY'\n# heredoc-escape-ok: только сетевые пробы, кода в файлы не пишет\nimport urllib.request, json, time\nfrom jobs_spec_data import PAT, VERIFIED, PRUNED, items\nUA=\"Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit

---

**Claude:**

Moonshot AI жива: `ashby/moonshot`, 5 ролей, и в спеке её нет — мою запись от 27.09 кто-то убрал. Возвращаю. Три остальных пробую через их собственные сайты.

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/jobs-watch\" && grep -n \"moonshot\" jobs_spec_data.py | head -5; echo \"=== где polosa-блок в VERIFIED ===\"; grep -n \"нога в двери ИИ-лаборатории\" jobs_spec_data.py | head -3", "description": "Locate moonshot and lab block in spec"}

---

**Claude:**

Поправка к себе: `ashby/moonshot` это не Moonshot AI, а крипто-приложение Moonshot. 23.10 это уже проверили и сняли с доски, оставив заметку, что настоящий Moonshot (Kimi) нанимает через MokaHR. Хорошо, что прочитал файл до правки, иначе затащил бы в полосу чужие роли.

Значит у всех четырёх публичной доски нет. Ищу их настоящие двери.

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/jobs-watch\" && timeout 420 python - <<'PY'\n# heredoc-escape-ok: только сетевые пробы\nimport urllib.request, gzip, zlib, re\nH={\"User-Agent\":\"Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/10.0.0.0 Safari/537.36\",

---

**Claude:**

Правда по всем четырём: публичной доски нет ни у кого, у каждой своя дверь. Делаю для этого явный реестр, чтобы сторож не краснел на лжи и ручная полоса знала причину.

---

> `Write` -- {"file_path": "C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_a5230cc4\\scratchpad\\patch2_h79620.py", "content": "#!/usr/bin/env python3\n\"\"\"Патч H79620 #2 (24.10.2026): реестр лабораторий БЕЗ публичной доски.\n\nПочему: сторож L9c (_tes

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/jobs-watch\" && python \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_a5230cc4/scratchpad/patch2_h79620.py\"; echo \"exit=$?\"; timeout 180 python _test_jobs_discover.py 2>&1 | grep -E \"^FAIL|L9[cfg]\"; time

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/jobs-watch\" && grep -n \"_HAND_ONLY\" _test_jobs_discover.py", "description": "Find actual _HAND_ONLY line"}

---

**Claude:**

Другая сессия вынесла это в функцию `lab_hand.door_companies()`. Правлю там — один источник вместо дубля в тесте.

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/jobs-watch\" && grep -n \"def door_companies\" -A 14 lab_hand.py", "description": "Read door_companies function"}

---

> `Write` -- {"file_path": "C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_a5230cc4\\scratchpad\\patch3_h79620.py", "content": "#!/usr/bin/env python3\n\"\"\"Патч H79620 #3 (24.10.2026): NO_BOARD входит в door_companies().\n\nСессия, работавшая после 27.

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/jobs-watch\" && python \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_a5230cc4/scratchpad/patch3_h79620.py\"; timeout 180 python _test_jobs_discover.py 2>&1 | grep -E \"^FAIL\"; timeout 180 python _test_jobs_

---

**Claude:**

Сторож зелёный, бездомных нет. Теперь доказываю, что новые проверки умеют краснеть.

---

> `Write` -- {"file_path": "C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_a5230cc4\\scratchpad\\redproof_h79620.py", "content": "#!/usr/bin/env python3\n\"\"\"Red proof H79620 (24.10.2026): новые сторожа L9c/L9f/L9g обязаны краснеть.\n\nТри мутации по о

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/jobs-watch\" && timeout 580 python \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_a5230cc4/scratchpad/redproof_h79620.py\" 2>&1 | tail -12; echo \"RED-PROOF exit=$?\"", "description": "Run red proof for new g

---

> `Bash` -- {"command": "set -o pipefail; cd \"D:/Vault/_imports/jobs-watch\" && timeout 580 python \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_a5230cc4/scratchpad/redproof_h79620.py\" 2>&1 | tail -12", "description": "Run red proof with pipefail", "tim

---

**Claude:**

Все три мутации покраснели на нужном стороже, возврат зелёный. Теперь главное: приделать `lab_hand` к ночной рутине, чтобы лента DeepMind больше не замерзала.

---

> `Bash` -- {"command": "powershell -NoProfile -Command \"Get-ScheduledTaskInfo -TaskName 'pipe-a-discover' | Select-Object -ExpandProperty LastTaskResult\" 2>&1 | head -2; tail -4 \"C:/Users/dev/.claude/state/pipe_a_discover.log\" 2>&1", "description": "Check nightly discover progress"}

---

**Claude:**

Ночной прогон дошёл до конца (витрина обновлена). Пробую перечитку ленты — теперь с ожиданием замка.

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/jobs-watch\" && timeout 560 python lab_hand.py run --pages 6 2>&1 | tail -10", "description": "Refresh lab_hand feed with lock wait", "timeout": 580000}

---

**Claude:**

Замок держат дольше двух минут. Ищу, кто именно, вместо того чтобы наращивать таймаут вслепую.

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/jobs-watch\" && python -c \"\nimport sqlite3\nc=sqlite3.connect('jobs.db',timeout=5)\nprint('journal_mode:',c.execute('PRAGMA journal_mode').fetchone()[0])\nprint('busy_timeout:',c.execute('PRAGMA busy_timeout').fetchone()[0])\nc.close()\" 2>&1; ls -la jobs.db*

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/jobs-watch\" && ls -la jobs.db jobs.db-wal jobs.db-shm 2>&1; echo \"=== пробная запись ===\"; timeout 200 python -c \"\nimport sqlite3,time\nt=time.time()\ntry:\n    c=sqlite3.connect('jobs.db',timeout=150)\n    c.execute('CREATE TABLE IF NOT EXISTS _probe_h796

---

**Claude:**

База действительно под write-замком прямо сейчас, проба ждёт в фоне. Пока она ждёт, делаю то, что базы не требует: пересъём Meta (её роли от 27.09, им 27 дней) и привязка модуля к ночной рутине.

---

> `mcp__Claude_Browser__preview_start` -- {"url": "https://www.metacareers.com/jobsearch/?q=superintelligence"}

---

> `mcp__Claude_Browser__browser_batch` -- {"actions": [{"name": "computer", "input": {"action": "wait", "duration": 5}}, {"name": "javascript_tool", "input": {"action": "javascript_exec", "text": "(()=>{const out=[...document.querySelectorAll('a[href^=\"/profile/job_details/\"]')].map(a=>{const L=(a.innerText||'').split('\\n').map(s=>s.trim

---

> `Bash` -- {"command": "cat \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_a5230cc4/tasks/bvxe8qy4j.output\" 2>&1 | tail -8", "description": "Read write probe result"}

---

**Claude:**

Замок настоящий: `jobs.db-wal` вырос до 11 МБ и пишется прямо сейчас (05:53), транзакция держится больше 162 секунд. Ищу писателя шире.

---

> `Bash` -- {"command": "powershell -NoProfile -Command \"Get-CimInstance Win32_Process -Filter \\\"Name='python.exe' OR Name='python3.12.exe'\\\" | Select-Object ProcessId,CreationDate,@{n='cmd';e={(\\$_.CommandLine -replace '\\s+',' ').Substring(0,[Math]::Min(130,(\\$_.CommandLine -replace '\\s+',' ').Length)

---

**Claude:**

PID 281216 живёт с 05:30 — это и есть ночной `jobs_discover`, он ещё идёт (лог в хвосте от прошлой ночи). Значит корень не в таймауте, а в моей архитектуре: `lab_hand.run` открывает базу и держит соединение, пока делает три десятка сетевых запросов. Переделываю: сеть сначала, запись одной короткой транзакцией в конце.

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/jobs-watch\" && sed -n '285,360p' lab_hand.py", "description": "Read current run function"}

---

> `Write` -- {"file_path": "C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_a5230cc4\\scratchpad\\patch4_h79620.py", "content": "#!/usr/bin/env python3\n\"\"\"Патч H79620 #4 (24.10.2026): lab_hand.run -- сеть сначала, база одной транзакцией.\n\nКорень, а 

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/jobs-watch\" && cp lab_hand.py \"E:/!CLAUDE-HUBPC-June26/_app-backups/lab_hand-h79620-20261024.before.py\" && python \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_a5230cc4/scratchpad/patch4_h79620.py\""

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/jobs-watch\" && sed -n '360,385p' lab_hand.py", "description": "Read tail of run function"}

---

> `Bash` -- {"command": "cd \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_a5230cc4/scratchpad\" && python - <<'PY'\n# heredoc-escape-ok: правит ТЕКСТ патч-скрипта без escape-последовательностей\nimport io\np='patch4_h79620.py'; s=io.open(p,encoding='utf-8').

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/jobs-watch\" && python \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_a5230cc4/scratchpad/patch4_h79620.py\"; echo \"exit=$?\"; python -c \"import ast,io; ast.parse(io.open('lab_hand.py',encoding='utf-8').rea

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/jobs-watch\" && timeout 180 python _test_lab_hand.py >/dev/null 2>&1; echo \"lab_hand тест exit=$?\"; timeout 180 python _test_jobs_discover.py >/dev/null 2>&1; echo \"discover тест exit=$?\"; echo \"=== dry-прогон: сеть работает, база не трогается ===\"; timeo

---

**Claude:**

Вот и цена незапущенного модуля: в `lab_hand.json` уже **216 ролей** (другие сессии добавляли руками), а в базе их только 76. Больше ста ролей, снятых людьми, лежали в файле и не доехали никуда. Привязываю модуль к ночной задаче.

---

> `Write` -- {"file_path": "C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_a5230cc4\\scratchpad\\wire_lab_hand.ps1", "content": "# Привязка lab_hand.py к ночной задаче pipe-a-discover (H79620, 24.10.2026).\n# Почему: с 27.09 модуль не звал НИКТО -- лента

---

> `PowerShell` -- {"command": "& \"C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_a5230cc4\\scratchpad\\wire_lab_hand.ps1\"", "description": "Wire lab_hand into nightly discover task"}

---

**Claude:**

PowerShell 5.1 читает `.ps1` как ANSI и ломается на кириллице. Перепишу скрипт латиницей, а объяснение оставлю в коммите и каноне.

---

> `Write` -- {"file_path": "C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_a5230cc4\\scratchpad\\wire_lab_hand.ps1", "content": "# Wire lab_hand.py into the nightly pipe-a-discover task (H79620, 2026-10-24).\n# ASCII only on purpose: Windows PowerShell 5

---

> `PowerShell` -- {"command": "& \"C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_a5230cc4\\scratchpad\\wire_lab_hand.ps1\"", "description": "Wire lab_hand into nightly task"}

---

**Claude:**

`Access is denied` — задача принадлежит привилегированному принципалу. По §0.4 это claim, пробую другие двери: сперва `schtasks`, и параллельно смотрю вариант без задач ОС вообще.

---

> `PowerShell` -- {"command": "$t = Get-ScheduledTask -TaskName 'pipe-a-discover'; $t.Principal | Select-Object UserId,LogonType,RunLevel | Format-List; schtasks /query /tn \"pipe-a-discover\" /fo list /v 2>&1 | Select-String -Pattern \"Run As User|Logon Mode|Schedule Type\" ", "description": "Inspect task principal"

---

> `PowerShell` -- {"command": "$log='C:\\Users\\dev\\.claude\\state\\pipe_a_discover.log'; $tr='python D:\\Vault\\_imports\\jobs-watch\\jobs_discover.py run >> ' + $log + ' 2>&1 & python D:\\Vault\\_imports\\jobs-watch\\pipe_a_sheet.py >> ' + $log + ' 2>&1 & python D:\\Vault\\_imports\\jobs-watch\\lab_hand

---

**Claude:**

Лимит `schtasks` 261 символ. Значит правильная дверь не в задаче ОС, а в коде: пусть сам `jobs_discover` в конце прогона зовёт ручную полосу. Тогда она работает на любом узле, без прав и без задач, и моя фраза в Библии станет правдой.

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/jobs-watch\" && grep -n \"def run\" jobs_discover.py | head -3; sed -n '/^def run/,/^def /p' jobs_discover.py | tail -25", "description": "Read end of jobs_discover run"}

---

**Claude:**

Важная находка: в `jobs_discover` уже есть сторож `stale_hand_feed`, который орёт в шину, что снимок Meta старше 7 дней. То есть сигнализация была, а исполнителя не было — ровно класс «детектор без исполнителя». Ставлю исполнителя.

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/jobs-watch\" && awk 'NR>=1088 && NR<=1200 && (/c\\.close|conn\\.close|commit\\(/)' jobs_discover.py | head -5; echo \"--- строки close в run ---\"; sed -n '1088,1200p' jobs_discover.py | grep -n \"close\\|commit\" | head -5", "description": "Find connection clo

---

> `Write` -- {"file_path": "C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_a5230cc4\\scratchpad\\patch5_h79620.py", "content": "#!/usr/bin/env python3\n\"\"\"Patch H79620 #5 (2026-10-24): jobs_discover.run() zovet nogu lab_hand.\n\nZachem: s 27.09 modul 

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/jobs-watch\" && cp jobs_discover.py \"E:/!CLAUDE-HUBPC-June26/_app-backups/jobs_discover-h79620-20261024.before.py\" && python \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_a5230cc4/scratchpad/patch5_h7

---

**Claude:**

Две помехи: моя проверка «уже привязано» сработала на упоминании в тексте, а имена L10 уже заняты. Смотрю факт и переименовываю.

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/jobs-watch\" && grep -n \"lab_hand\" jobs_discover.py | head -10", "description": "Find lab_hand mentions in discover"}

---

**Claude:**

Подтвердилось: `lab_hand.run()` жил только в докстроке, нога не привязана — моя проверка «уже привязано» соврала зелёным. Чиню проверку и имена.

---

> `Bash` -- {"command": "cd \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_a5230cc4/scratchpad\" && python - <<'PY'\n# heredoc-escape-ok: правит текст патч-скрипта, escape-последовательностей не несёт\nimport io\np='patch5_h79620.py'; s=io.open(p,encoding='ut

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/jobs-watch\" && python - <<'PY'\n# heredoc-escape-ok: удаляет ранее добавленный тестовый блок с занятыми именами L10\nimport io\np='_test_jobs_discover.py'; s=io.open(p,encoding='utf-8').read()\ni=s.find('# Проводка ноги ручной полосы (24.10.2026)')\nj=s.find('

---

**Claude:**

Имена снова столкнулись с чужими. Переименую свои в L12, чтобы в журнале сторожей не было двух L11.

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/jobs-watch\" && python - <<'PY'\n# heredoc-escape-ok: переименование ярлыков проверок, escape не несёт\nimport io\np='_test_jobs_discover.py'; s=io.open(p,encoding='utf-8').read()\nfor a,b in (('\"L11 discover','\"L12 discover'),('\"L11b у ноги','\"L12b у ноги'

---

> `Write` -- {"file_path": "C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_a5230cc4\\scratchpad\\redproof2_h79620.py", "content": "#!/usr/bin/env python3\n\"\"\"Red proof H79620 #2: storozha provodki L12/L12b/L12c obyazany krasnet.\n\nImenno etot klass m

---

> `Bash` -- {"command": "set -o pipefail; cd \"D:/Vault/_imports/jobs-watch\" && timeout 580 python \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_a5230cc4/scratchpad/redproof2_h79620.py\" 2>&1 | tail -8", "description": "Red proof wiring guards", "timeout

---

**Claude:**

M3 не покраснел, а уронил тест исключением — сторож ослеп вместо того чтобы сказать FAIL. Правлю сторож и перепроверяю.

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/jobs-watch\" && python - <<'PY'\n# heredoc-escape-ok: правка кода сторожа без escape-последовательностей\nimport io\np='_test_jobs_discover.py'; s=io.open(p,encoding='utf-8').read()\nold = ('chk(\"L12c нога зовётся ПОСЛЕ закрытия соединения (пишет в ту же базу)

---

**Claude:**

Все три мутации краснеют правильно. Теперь боевой прогон — окно записи теперь короткое.

---

> `Bash` -- {"command": "set -o pipefail; powershell -NoProfile -Command \"if (Get-Process -Id 281216 -ErrorAction SilentlyContinue) {'ночной discover ЕЩЁ ИДЁТ'} else {'ночной discover завершился'}\" 2>&1 | tail -1; cd \"D:/Vault/_imports/jobs-watch\" && timeout 560 python lab_hand.py run --pages 6 2>&1 | ta

---

**Claude:**

Прогон прошёл: DeepMind отдал 120 карточек (было 73), взято 321 роли. Но «новых=0» — проверяю базу, это может быть и правда, и ложь прибора.

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/jobs-watch\" && timeout 200 python - <<'PY'\n# heredoc-escape-ok: только чтение базы\nimport sqlite3\nc=sqlite3.connect('jobs.db',timeout=60)\nprint(\"ats       компания                        всего  new  applied  last_seen\")\nfor r in c.execute(\"SELECT ats,c

---

**Claude:**

Прибор соврал: в базе было 146 строк ручной полосы, стало **390**, свежей меткой помечены 319 — а счётчик напечатал «новых=0». Ищу, почему он лжёт.

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/jobs-watch\" && sed -n '/^def upsert/,/^def /p' jobs_discover.py | head -40", "description": "Read upsert contract"}

---

**Claude:**

В базе +244 строки, а счётчик показал ноль. Читаю свой же код, прежде чем объяснять.

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/jobs-watch\" && sed -n '306,320p' lab_hand.py; echo \".....\"; sed -n '355,382p' lab_hand.py", "description": "Read final run code order"}

---

**Claude:**

Стоп. Прибор не соврал: он честно показал 0, потому что все 321 строка уже были в базе. Значит +244 строки положил кто-то другой между моими двумя замерами — ночной `pipe-a-discover`, который шёл 05:30-06:0x. То есть моя версия «ленту никто не обновляет» была неверной, и я чуть не принёс её тебе как факт. Проверяю, что именно делает чужая нога `careers_leg`.

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/jobs-watch\" && sed -n '/^def careers_leg/,/^def [a-z_]*(/p' jobs_discover.py | head -45", "description": "Read careers_leg function"}

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/jobs-watch\" && grep -rn \"gcareers\\|HAND_CODE\\|lab_hand\" jobs_discover.py careers_feed.py lab_hand_feed.py 2>/dev/null | grep -v \"^jobs_discover.py:3[0-9][0-9]:\" | head -16; echo \"=== лог ночного прогона про DeepMind/hand ===\"; grep -iE \"deepmind|lab_h

---

**Claude:**

Теперь правда полная, и она поправляет меня дважды. Читаю чужую ногу от 23.10 целиком.

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/jobs-watch\" && sed -n '1200,1216p' jobs_discover.py", "description": "Read the 23.10 lab_hand leg"}

---

**Claude:**

Нога была привязана **23.10, за день до меня**, другой сессией с тем же диагнозом. Значит мой блок — чистый дубль: ночь свипала бы careers-сайт дважды. Откатываю его и оставляю только то, что правда моё.

---

> `Write` -- {"file_path": "C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_a5230cc4\\scratchpad\\patch6_h79620.py", "content": "#!/usr/bin/env python3\n\"\"\"Patch H79620 #6 (2026-10-24): otkat moego dublya nogi lab_hand + chestnye storozha.\n\nChto proi

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/jobs-watch\" && python \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_a5230cc4/scratchpad/patch6_h79620.py\"; echo \"exit=$?\"; python -c \"import ast,io; ast.parse(io.open('jobs_discover.py',encoding='utf-8'

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/jobs-watch\" && diff \"E:/!CLAUDE-HUBPC-June26/_app-backups/jobs_discover-h79620-20261024.before.py\" jobs_discover.py && echo \"✅ jobs_discover вернулся к исходному виду: моего следа в нём нет\"; set -o pipefail; for t in _test_jobs_discover.py _test_lab_

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/jobs-watch\" && timeout 200 python _test_jobs_comp.py 2>&1 | grep -E \"FAIL|Error|Traceback\" | head -6", "description": "Check jobs_comp failure"}

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports\" && git status --porcelain jobs-watch | head -10; echo \"=== красный ли _test_jobs_comp на коде ИЗ GIT (без моих правок) ===\"; mkdir -p \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_a5230cc4/scratchpad/git

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/jobs-watch\" && cp lab_hand.py /tmp/lh_mine.py && cp \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_a5230cc4/scratchpad/gitcheck/lab_hand_head.py\" lab_hand.py && echo \"### _test_jobs_comp на ЧИСТОМ коде из 

---

**Claude:**

Доказано: три красные проверки `_test_jobs_comp` одинаково красные и на чистом коде из git, и с моим — это чужой долг, не мой след. Коммичу своё.

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports\" && git add jobs-watch/lab_hand.py jobs-watch/selenium_apply/manual_lane.py jobs-watch/_test_jobs_discover.py jobs-watch/jobs_discover.py && git commit -q -F - <<'MSG'\njobs-watch: Meta входит в ручную полосу, третий дом для лабораторий без доски, замок jobs.d

---

**Claude:**

Теперь доказательство у потребителя: гоню ручную полосу и смотрю, доехала ли Meta до списка, который ты закрываешь руками.

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/jobs-watch\" && python selenium_apply/manual_lane.py --help 2>&1 | head -20", "description": "Read manual_lane CLI"}

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/jobs-watch\" && timeout 560 python selenium_apply/manual_lane.py --n 25 --per-company 4 --out \"D:/Vault/Vault-Knowledge/04-Projects/Pipe-A-Batches/manual-lane-labdoor-2026-10-24.md\" 2>&1 | tail -14", "description": "Run manual lane to prove Meta reaches it

---

**Claude:**

Доказательство у потребителя получено: Meta в списке. Теперь честное до→после — тот же прогон на версии из git.

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/jobs-watch\" && SP=\"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_a5230cc4/scratchpad\" && cp selenium_apply/manual_lane.py \"$SP/ml_mine.py\" && cd \"D:/Vault/_imports\" && git show HEAD~1:jobs-watch/sele

---

**Claude:**

До и после совпали: Meta была в списке и на старой версии. Значит мой патч `WHY_MANUAL` не был разблокировкой — проверяю, через какую дверь роли `hand` попадали туда раньше.

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports\" && SP=\"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_a5230cc4/scratchpad\" && grep -n '\"hand\"\\|hand' \"$SP/ml_head.py\" | head -8; echo \"=== второй путь отбора в файле? ===\"; grep -n \"ats IN\\|LAB\\|l

---

**Claude:**

Моя проверка «до» оказалась негодной: автоснапшот репозитория успел закоммитить мою же правку, и `HEAD~1` уже содержал её. Беру настоящую версию до правки.

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports\" && git log --oneline -4 -- jobs-watch/selenium_apply/manual_lane.py; echo \"=== ищу последнюю версию БЕЗ строки hand ===\"; for rev in $(git log --format=%h -8 -- jobs-watch/selenium_apply/manual_lane.py); do if git show $rev:jobs-watch/selenium_apply/manual_

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports\" && SP=\"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_a5230cc4/scratchpad\" && git show 76ef2471:jobs-watch/selenium_apply/manual_lane.py > \"$SP/ml_true_before.py\" && grep -c \"WHY_MANUAL\" \"$SP/ml_true_b

---

**Claude:**

Теперь до→после честное, и оно подтверждает починку:

| Прогон | Ролей в списке | Из них `hand` (Meta, Fleet AI) | Отсеяно |
|---|---|---|---|
| ДО (версия 23.10, без полосы `hand`) | 25 | **0** | 646 |
| ПОСЛЕ (моя правка) | 25 | **6**, в том числе 2 Meta | 686 |

Прошлый «одинаковый» результат получился потому, что автоснапшот репозитория успел закоммитить мою же правку, и я сравнил себя с собой. Записываю это в канон вместе с остальным.

---

> `Write` -- {"file_path": "C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_a5230cc4\\scratchpad\\canon_h79620.py", "content": "#!/usr/bin/env python3\n\"\"\"Canon H79620 (2026-10-24): popravka Biblii + pamyat po polose lab-door.\n\nMachine: HUB-01

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/jobs-watch\" && python \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_a5230cc4/scratchpad/canon_h79620.py\"; echo \"exit=$?\"; set -o pipefail; timeout 100 python \"C:/Users/dev/.claude/scripts/rule_home_gu

---

> `Write` -- {"file_path": "C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_a5230cc4\\scratchpad\\skill_h79620.py", "content": "#!/usr/bin/env python3\n\"\"\"Skill /apply: sloy 24.10.2026 (H79620) -- ruchnaya polosa i tretiy dom.\n\nMachine: HUB-01

---

> `Bash` -- {"command": "cd \"C:/Users/dev/.claude/skills/apply\" && cp SKILL.md \"E:/!CLAUDE-HUBPC-June26/_app-backups/apply-SKILL-h79620-20261024.before.md\" && python \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_a5230cc4/scratchpad/skill_h79620.py

---

> `Bash` -- {"command": "cd \"C:/Users/dev/.claude/skills/apply\" && python -c \"\nimport io\np='SKILL.md'; s=io.open(p,encoding='utf-8').read()\ns=s.replace('WHY_MANUaL','WHY_MANUAL')\nio.open(p,'w',encoding='utf-8',newline='\\n').write(s)\nprint('опечатка исправлена:', 'WHY_MANUaL' not in io.open(p,encoding

---

> `Bash` -- {"command": "cd \"C:/Users/dev/.claude/scripts\" && timeout 100 python voice001_collaboration.py describe --session-id s_a5230cc4 --wait-seconds 0 2>&1 | python -c \"\nimport json,sys\nd=json.load(sys.stdin)\nprint('001 статус:',d.get('status'),'| источник подтверждён:',d

---

> `mcp__ccd_session__spawn_task` -- {"title": "Починить 3 красные проверки _test_jobs_comp", "tldr": "Пока разбирал полосу вакансий в лаборатории, наткнулся на чужой красный тест в той же папке: три проверки падают и на чистом коде из git, то есть лежат красными уже какое-то время. Новая сессия найдёт корень и починит.", "prompt": "Тр

---

**Claude:**

Чип канон запрещает. Узел перегружен (load 191), поэтому кладу задачу сидом в очередь, а не поднимаю сессию прямо сейчас.

---

> `Bash` -- {"command": "cd \"C:/Users/dev/.claude/scripts\" && timeout 60 python spawn_queue.py add --help 2>&1 | head -20", "description": "Read spawn_queue add CLI"}

---

> `Write` -- {"file_path": "C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_a5230cc4\\scratchpad\\seed_jobs_comp.md", "content": "Переименуй себя в: ⚙️ · 🧪📉 Красный _test_jobs_comp: три проверки кластеров\n\nТруба А, хаб HUB-01, папка `D:\\Vault

---

> `Bash` -- {"command": "cd \"C:/Users/dev/.claude/scripts\" && timeout 100 python spawn_queue.py add --task-id \"auto-hub-261024-red-test-jobs-comp\" --description \"⚙️ · 🧪📉 Красный _test_jobs_comp: три проверки кластеров (чужой долг, доказан 24.10 как не связанный с правками H79620)\" --prompt-file \"C:/Use

---

> `Bash` -- {"command": "set -o pipefail; head -32 \"D:/Vault/Vault-Knowledge/04-Projects/Pipe-A-Batches/manual-lane-labdoor-2026-10-24.md\" 2>&1 | tail -22; echo \"=== сколько ролей и каких компаний в файле ===\"; grep -cE \"^### |^## [0-9]\" \"D:/Vault/Vault-Knowledge/04-Projects/Pipe-A-Batches/manual-l

---

> `SendUserFile` -- {"files": ["D:/Vault/Vault-Knowledge/04-Projects/Pipe-A-Batches/manual-lane-labdoor-2026-10-24.md"], "caption": "Ручная полоса лабораторий на сегодня: 25 ролей, в которые робот не может нажать «отправить». Впервые внутри есть Meta и Meta Superintelligence Labs. Шпаргалка ответов и путь к нужному 

---

**Claude:**

🕐 24.10.2026, 06:4x. Сессия H79620, хаб.

## Что я выбрал делать и почему

Сессия вернулась через 26 дней. Я не стал докладывать по памяти, а сверил живое, и первое же измерение показало дыру ровно в том, что мы строили 27.09: две крупнейшие лаборатории в базе есть, а подач по ним **ноль за 27 дней**.

Копал до корня и по дороге дважды поймал **себя** на неправде. Рассказываю оба раза, потому что без них отчёт был бы красивее и лживее.

## Что действительно починено

**1. Meta впервые доехала до человека.** 179 ролей Meta и Meta Superintelligence Labs лежали в базе со статусом `new` и нулём подач. Причина: подача на metacareers.com возможна только после входа в аккаунт, робот аккаунты не создаёт, а ручная полоса `manual_lane.py` (её собрали 22.10) знала про `gcareers`, но про полосу `hand` не знала. Роли Meta не попадали в твой список **ни разу**.

Замер на одном и том же прогоне:

| Прогон | Ролей | Из них `hand` | Meta внутри |
|---|---|---|---|
| ДО (версия 23.10) | 25 | 0 | нет |
| ПОСЛЕ | 25 | 6 | 2 роли |

Файл уже у тебя в чате: 25 ролей, шпаргалка ответов, путь к нужному PDF резюме и ссылка в каждой строке. Внутри впервые Meta, DeepMind и Fleet AI вместе.

**2. Четыре лаборатории были в правиле и не было их в трубе.** Список `LAB_DOOR_CO` вырос с наших 60 до **189** организаций, и у четырёх не оказалось дома ни на доске, ни в ручной полосе: Cognee, Interloom, Moonshot AI, Supermemory. Мой же сторож L9c честно краснел месяц. Завёл третий дом `NO_BOARD`, двери замерил живым запросом, не догадкой:

- Cognee: страница отвечает, ATS нет, дверь это письмо на [EMAIL]
- Interloom: `/careers` отдаёт 404 на обоих доменах
- Supermemory: страница живая, список рисует JS, нужен браузерный съём
- Moonshot AI: MokaHR, вход создаёт аккаунт

И отдельно: `ashby/moonshot` это **чужое крипто-приложение** Moonshot, а не лаборатория. Я чуть не затащил его роли обратно в полосу, остановился потому что прочёл файл до правки, где сосед это уже выяснил 23.10. Полоса ходит по имени компании, значит тёзка это баг, и теперь на это стоит тест.

**3. Отпустил замок общей базы.** `lab_hand.run()` открывал `jobs.db` первой строкой и держал соединение все десятки сетевых запросов. Рядом с ночной рутиной это падало: два прогона сегодня умерли с «database is locked», проба записи ждала 162 секунды и не дождалась. Теперь сеть и скоринг идут без базы, запись одной короткой транзакцией в конце. Окно замка из минут стало секундами.

Сторожа: L9f (у записи без доски обязана быть непустая причина, пустышкой не заткнуть), L9g (дома не пересекаются), L12 (проводка ноги жива), L13 (база открывается после сети). Краснота доказана на **шести мутациях**, возврат зелёный. Один из моих сторожей по ходу проверки оказался слепым: падал исключением вместо честного FAIL. Перевёл его на безопасный поиск.

## Где я был неправ

**Первая неправда была в Библии, и это моя.** 27.09 я написал туда, что модуль ручной полосы «дёргается каждым ночным прогоном рутины». Вызова в коде не было вовсе, модуль числился сиротой, лента DeepMind стояла с 27.09 по 23.10. Дверь была объявлена, а двери не было. Починил это не я: ногу припаяла **другая сессия 23.10**, за день до меня, с тем же диагнозом.

**Вторая неправда почти уехала в этот отчёт.** Я решил по метке `last_seen=27.09`, что ленту никто не обновляет, и припаял вторую ногу. Замер показал обратное: ночной прогон в 05:30 уже отработал её и дал «взято=321 новых=244». Мой блок был дублем, из-за него careers-сайт свипался бы дважды за ночь. Откатил; файл `jobs_discover.py` теперь побайтово равен исходному.

**Третья грабля, которую стоит запомнить всему флоту.** Первое до→после показало «изменений нет». Причина не в коде: автоснапшот репозитория коммитит рабочее дерево каждые два часа, и `HEAD~1` уже содержал мою же правку. Я сравнил себя с собой. Настоящее «до» нашлось перебором по истории файла, и тогда разница проявилась. Записал в канон.

## Чего не делал и честно называю

`_test_jobs_comp.py` красный тремя проверками. Доказал, что это не мой след: те же три FAIL и на чистом коде из git, и с моими правками. Это чужой долг. Чип завести канон запрещает, узел перегружен (load 191), поэтому положил сидом в очередь: `auto-hub-261024-red-test-jobs-comp`.

Задачу планировщика тронуть не смог: `Set-ScheduledTask` отбил Access is denied (принципал S4U), `schtasks /change` уперся в лимит 261 символа. Дверь в коде оказалась не нужна, потому что нога уже была припаяна 23.10.

Рельсы: объявил вынос чтения кода на Codex, не вынес. Причина честная, `too-small`: читал прицельными кусками по 20-40 строк, больших файлов целиком не открывал.

Канон обновлён: Библия получила «Поправку 24.10» со всеми тремя моими ошибками, память и скилл `/apply` тоже. Коммит `54fc4453`, бэкапы четырёх тронутых файлов лежат в `_app-backups`.

🔧 Вердикт о скилле: `/apply` обновил, добавил слой про ручную полосу и третий дом. Боль была пережитая: роли Meta месяц не доходили до твоих рук.

Дальше по этой теме самое ценное это не код, а живой вопрос: 430 подач по полосе лабораторий и **ноль интервью** в их статусах. Это следующий разрыв, и он уже не про трубу, а про то, доходят ли письма и что отвечают. Скажи `/QQQ`, и я возьму его.

🧒 **Простыми словами:** месяц назад мы научили робота видеть любые вакансии в ИИ-лабораториях. Сегодня я проверил, что из этого вышло, и нашёл, что вакансии Meta робот видел, но не мог положить тебе на стол: он умеет только те, где кнопку жмёт сам, а у Meta надо входить в аккаунт. Я открыл для них отдельный список, который ты закрываешь руками, и он уже у тебя в чате: 25 вакансий, к каждой готовые ответы и нужное резюме. Ещё нашёл четыре лаборатории, которые были записаны в правилах, но в робота не попали, и прописал каждой её дверь. И дважды поймал сам себя на вранье: один раз я месяц назад написал в правила, что всё работает, хотя не проверил, а второй раз сегодня чуть не сказал тебе, что починил то, что до меня починил сосед. Оба раза исправил и записал, чтобы не повторилось.

---

**User:**

<command-message>rr</command-message>
<command-name>/rr</command-name>

---

**User:**

Base directory for this skill: C:\Users\dev\.claude\skills\rr

# /rr — алиас для /retro

**Что это:** просто короткая горячая клавиша. `/rr` = `/retro`, буква-в-букву одно и то же.
оператору быстрее набрать `rr`, чем `retro`. Никакой отдельной логики здесь НЕТ и быть не должно.

**Что делать при вызове:** сразу вызови скилл `retro` через инструмент Skill и выполняй его как обычно.
Не копируй сюда шаги ретро — единственный источник = скилл `retro` (правило «один источник, без дублей», AK-47).

**Семья дуплет-алиасов** (одна логика на каждый):
- `/tt` == `/test` — тест собранного
- `/rr` == `/retro` — ретро-завершение сессии
- `/cc` — печать готовой строки `/compact` под нашу сессию
- `/1` == `/!` — воскрешение после крэша

**Границы:** имя папки = `rr`, поэтому `/rr` работает нативно; `/рр`/`/кк` (неверная раскладка) —
текст-триггеры, узнав их, запускай этот же скилл. Регистр не важен ([[commands-case-insensitive]]).

---

> `Skill` -- {"skill": "retro"}

---

**User:**

Base directory for this skill: C:\Users\dev\.claude\skills\retro

# /retro — session retrospective (what we built · what we keep)

> 🧒 **When reporting to dev:** end with a child-simple "Простыми словами" recap in his language. His standing request (memory `eli5-always`). Reports TO dev only — not inside vault notes.

A retro = the Agile end-of-cycle ritual (**Keep / Drop / Try**) applied to a work session: look back, decide what survives. The goal is that **nothing reusable drowns in the transcript** — tools, rules, and lessons get caught and put in their right home.

## 🫸 ПОЛОСА `push3` — ретро 4-й командой после трёх толчков (dev 05.10.2026, голосом)

**Вызвана так:** `/retro push3` (так её посылает робот-проталкивалка `/push`, шаг 3б) ЛИБО
оператор говорит «сделай ретро по этой сессии». Приказ дословно: «после того как по задаче
3 раза нажимаем "продолжить сессию" и проталкиваем её дальше, 4-й командой нужно
запускать ретро... не терять содержание сессий, а сразу дистиллировать из них самое
важное: что делали, к чему пришли, какие выводы и следующие шаги. Это лучше делать сразу
после трёх продолжений, а не потом заново догонять всю сессию и пытаться восстановить
смысл».

**Это НЕ полное ретро.** Полное ретро ниже (Step 0...6) закрывает ЗАКОНЧЕННУЮ содержательную
работу и развозит durable по домам. Полоса `push3` закрывает другое: сессию протолкнули
трижды, она НЕ доделала, и её содержание вот-вот утонет в транскрипте. Цена полного
ритуала здесь не оправдана (§6.4, АК-47) — поэтому полоса короткая и кончается ОДНОЙ
строкой в журнале, который оператор читает. Полосу запускай ТОЛЬКО этим путём; пришёл простой
`/retro` без слова `push3` — делай полный ритуал.

**Ретро в этой сессии уже было → RECALL + лёгкое (dev 14.10.2026, голосом, сессия H94967).**
Дословно: «если на сессии ещё не было ретро, то мы делаем в любом случае там ретро… Если на
сессии уже было ретро, то логично сделать рекол и потом лайтовое ретро». Порядок: 1) найди в
транскрипте прошлое исполненное ретро и перечитай его; 2) дистиллируй ТОЛЬКО дельту после него
(что нового сделано · к чему пришли · выводы · следующие шаги); пересказ старого ретро = пустой
дистиллят. Толкач сам помечает такую команду словом `лёгкое`, но правило действует и без метки.
Слаг правила: `repeat-retro-is-recall-plus-light` (память).

### Шаг П1 — часы и разрыв (обязателен, та же дверь, что у полного ретро)
`get_session self` → `createdAt` / `lastActivityAt` + живые часы. Разрыв назови ЧИСЛОМ.
Метка хука `[⏰ оператор написал: …]` доказательством НЕ является (память `verify-clock-before-time-claims`).

### Шаг П2 — четыре поля оператора, и ровно они
Из СВОЕГО контекста (он горячий — в этом весь смысл полосы), без перечитывания транскрипта:
1. **что делали** — одна-две фразы по делу, без списка инструментов;
2. **к чему пришли** — результат с уликой (файл, exit-код, цитата), а не «поработали»;
3. **какие выводы** — что из этого durable; нечего — так и пиши «durable нет»;
4. **следующие шаги** — конкретный следующий ход, а не «продолжить работу».

⛔ Выдумывать нельзя: не уверен в поле — пиши «🤔 не подтверждено» (§5.4). «Готово» в поле
«к чему пришли» без улики = дефект, а не вежливость.

### Шаг П3 — ветки СРАЗУ, из дистиллята (а не потом)
«Если после ретро нужно сделать ветки/дальнейшие действия — делать их сразу на основе
дистиллированного контента». Разъехалось на слабо связанные куски → поднимаешь сессии САМ
(`/nsr`), сидом кладёшь дистиллят из Шага П2, а не «прочитай сессию такую-то». Разрешения
не спрашиваешь (§4.1). В новой сессии действует это же правило фрактально: три толчка → ретро.

### Шаг П4 — рот: строка в журнал, который оператор читает
```bash
python ~/.claude/scripts/session_retro_digest.py add --session <свой sessionId> \
  --title "<заголовок сессии>" --pushes 3 \
  --did "..." --got "..." --lessons "..." --next "..." \
  --branches "<что поднял сам, или пусто>" --dev "нет|<что именно нужно от него>"
```
Пишет в `$OBSIDIAN_VAULT/00-System/Session-Retro-Digest.md`, новые записи СВЕРХУ. Это и есть
«дальше я читаю ретро по сессии»: `--dev "нет"` = оператор идёт дальше, любой другой текст =
🙋 он подключается и дорабатывает. ⛔ Оставить дистиллят только внутри сессии = не сделать
работу: труба рождается с ртом (память `pipe-born-with-a-mouth`).

### Шаг П4-бис — долги правила (раз в заход, не чаще)
```bash
python ~/.claude/scripts/retro_rule_health.py
```
`exit 3` = есть сессии, которые выбрали три продолжения, затихли и дистиллята НЕ дали — правило сработало вхолостую. Назови их оператору строкой; доехать до них может `/push` Шаг 3в (в окне) или ночная `/retro-lost` (вне окна). `exit 1` = прибор слеп, это не «долгов нет».

### Шаг П4-бис-2 — деревья решений (§5.12, с 15.10)
```bash
python ~/.claude/scripts/decision_tree.py stats --days 7
```
Строкой в отчёт: развилок N, стопов M · узлы на 3-м стопе → ветка в дерево + 5 почему · запасной путь ok 3+ раз → кандидат в код · в этой сессии дерево выросло: да/нет. Раз в месяц `--prune --days 90`.

### Шаг П4-бис-3 — загружено только нужное (с 18.10)
Тот же вызов, что Step 3🧺 полного ретро; строка «🧺 загрузка: …» в отчёт.

### Шаг П4-тер — панель шести ломателей (обязательна и здесь)
Тот же вызов, что Step 3🔨 полного ретро, корм = дистиллят П2. Строка `🔨 панель: …` в отчёт.

### Шаг П5 — закройся
Durable правило/урок есть → Step 4 полного ретро для НЕГО одного (дом правила), остальные
шаги не нужны. Потом короткий 🧒-блок оператору и всё. ⛔ Не дрифтуй в чужие темы,
⛔ ничего наружу, ⛔ Tier-2 остаётся за оператором.

**Почему полоса живёт внутри `/retro`, а не отдельным скиллом:** один источник на слово
«ретро» (§5.8). Копия скилла под робота = второй дом, который разъедется с первым.

---

## Step 0 — RECALL & RECONCILE FIRST (situate this session in the WHOLE collaboration)
**Before any inventory, RECALL WIDE — this is the heart of the retro, not a formality (dev, 2026-07-02).** A session never happened in a vacuum: I run on multiple machines + a Cowork fleet concurrently, and this retro may be running **days/weeks/months after** the work. So recall here serves TWO jobs, not one:
- **(A) De-dupe** — a rule/skill/note I'm about to capture may already be done by a parallel session.
- **(B) Reconcile («сверить»)** — line up what THIS session did against everything the whole **hub / vault / peers** decided *since*; catch **drift, superseded decisions, contradictions**, and durable work not yet propagated. This is the RECALL-before-activity rule (`capture-rules-into-bible`) applied to retro.

⚠️ **И ДАТИРУЙ АРТЕФАКТЫ ВРЕМЕНЕМ СОБЫТИЯ, А НЕ ВРЕМЕНЕМ РЕТРО** (замер 30.09.2026, хаб: сессия начата 22.09, ретро шло 30.09; я взял часы ретро за «сейчас» и ИСПОРТИЛ верную дату в подписях 8 файлов, потом откатывал). Часы на ретро правдивы, метка хука первого захода тоже была правдива — врёт СКЛЕЙКА. Прежде чем поставить дату в подпись, заметку или леджер, спроси улику САМОГО события: `mtime` бэкапа/файла, `ts` уже записанной строки леджера, `createdAt` из `get_session self`. Правило зеркалит память `verify-clock-before-time-claims`: старый tool-вывод после резюма ≠ «сейчас», но и новые часы ≠ «когда это было сделано».

**⏳ Measure the time-gap FIRST — ДВУМЯ ПРОГОНАМИ, не суждением** (дверь от 30.09.2026; 01.10 она обнаружилась УТЕРЯННОЙ — живой SKILL.md держал ослабленную строку, а жёсткая версия лежала только в `SKILL.sync-conflict-20260930-*.md`; восстановлена 01.10):
```
python -c "import datetime; print('СЕЙЧАС', datetime.datetime.now().isoformat(timespec='seconds'))"
```
плюс `mcp__ccd_session_mgmt__get_session` с `session_id: "self"` → поля `createdAt` и `lastActivityAt`. Разница между ними И ЕСТЬ разрыв, и его надо назвать ЧИСЛОМ в отчёте.
⚠️ Метка из хука `[⏰ оператор написал: …]` доказательством НЕ является — это дата СИДА. Замер 30.09.2026 (класс `stale-context-after-resume-read-as-now`): сессию создали 16.09, возобновили 30.09, и весь заход я печатал «16 сентября» из подсказки хука, ни разу не сверив с часами. Канон: память `verify-clock-before-time-claims`.
Old session → widen every lookup below to cover *"what changed SINCE"*, и **Step 2а идёт СРАЗУ после этого замера**, до инвентаря: робот мог уже разобрать сессию, тогда всё ретро = дельта.

⚠️ **На Windows каждый прибор ниже запускай `python -X utf8 <скрипт>`** (замер 08.10.2026, NODE-0X, ретро про зависание Chrome: 5 из 9 проб потеряли первый прогон на `UnicodeEncodeError cp1252`, у `selfheal.py` падал даже свой except, у `onair.py list` обрезался список). `python -I` отключает `PYTHONIOENCODING`, поэтому переменная не спасает, флаг `-X utf8` работает и с `-I`. Прибор, упавший на кодировке, вердикта не дал: это «не измерено», а не «чисто».

**Recall stack — cheap→expensive, mostly 0 tokens (use the existing tools, don't reinvent):**
1. **This session's spine (0 tok):** `python "$IMPORTS_ROOT/turnstate/turnstate_show.py"` — the black box of what THIS session actually asked / decided / touched (facts, not memory).
2. **Recent retros:** `ls "$OBSIDIAN_VAULT/01-Conversations/Claude/Retros/"` — widen the window to span the gap; read any same-topic retro since.
2а. **Робот уже сделал ретро этой сессии? (0 tok):** `ls ~/.claude/logs/retro_lost_done/ | grep <sessionId>` — маркер есть → ночной `retro-lost` уже разобрал сессию (заметка `Retros/retro-lost-<дата>-<узел>-*.md`, единица с твоим sid). Тогда твоё ретро = ДЕЛЬТА поверх неё (живая сверка «что изменилось с тех пор» + компакт), с перекрёстной ссылкой, а не второй полный разбор. Замер 15.09.2026: сессия 07–08.09 получила лайт-ретро робота утром 15.09, живое ретро вечером чуть не переписало всё заново.
2б. **Дни целиком (0 tok):** `python "$IMPORTS_ROOT/day_ledger.py" --recall 7` — дневной леджер: коммиты, ретро, решения, ДР и посты **за каждый день окна**, включая чужие сессии и роботов. Именно он закрывает time-gap из ⏳ выше: ретро видят только ретро, леджер видит день. Дверь целиком — `/ledger`.
2в. **Рутина бежала или нет — только СЧЁТЧИК ПРОГОНОВ, НЕ наличие файлов (0 tok):**
   `python ~/.claude/scripts/routine_cost_audit.py --days <N>` -> колонка «прог.».
   Выход рутины пишется НЕ каждый прогон (у `pipe-a-inbox-watch` отчёт рождается только в дни
   с живыми письмами), поэтому «файла за 11.09 нет» не значит «11.09 не работала». Замер 15.09:
   объявил оператору 4 пропуска подряд, счётчик показал 8 прогонов за 9 дней — вывод был ложный
   и уже озвучен. Семья класса «судим по побочному следу вместо счётчика самой работы» насчитывает
   6 прежних случаев (ближайший 20.08: опись судила mtime заявленного stdout вместо факта работы),
   так что механизм тут не нужен — нужен ПОРЯДОК: счётчик первым, файлы вторыми.
   Канон: [[instrument-is-a-claim-too]], CLAUDE.md §5.4.
2в-бис. **А ЧЕМ КОНЧИЛАСЬ — отдельный вопрос, счётчик на него не отвечает (0 tok):**
   `python ~/.claude/scripts/_shared/routine_runs.py report` -> «падают СЕЙЧАС (серия)» + «молчат >7 суток».
   Точечно по одной: `routine_runs.py last "<имя задачи>"` (когда бежала, чем кончилась) и
   `routine_runs.py streak "<имя задачи>"` (сколько раз ПОДРЯД упала).
   Почему мало счётчика из 2в: `routine_cost_audit.py` считает прогоны по транскриптам СЕССИЙ
   (`~/.claude/projects/**/*.jsonl`) и про КОД ВОЗВРАТА не знает ничего — рутина, отбежавшая
   8 раз и 8 раз упавшая, в колонке «прог.» выглядит ровно как здоровая. Вопрос оператора на
   ретро — «эта рутина работает или УМЕРЛА?» — закрывается только парой «число прогонов +
   исход». Источник истины тут Планировщик Windows, а не наши логи (замер 01.10: 891 прогон,
   340 рутин с историей, 52 падают подряд прямо сейчас).
   ⚠️ Граница: история есть только у задач Планировщика; у движка `claude-task` её не
   существует нигде, и это говорится вслух, а не выводится из тишины.
   Канон: CLAUDE.md §5.5, §5.4; зеркала — `/hk` Шаг 3, `/arch`.
3. **Neighboring chats (lexical, 0 tok):** `/search <topic words>` (search_catalog.db, ~99k Telegram/FB/ChatGPT/Claude) — what did dev or another session **dictate elsewhere** about this topic?
4. **Vault meaning (RAG):** `/ask <topic>` (`$IMPORTS_ROOT/brain_ask.py`) — what does the Second Brain already hold / already decide on this?
5. **Memory + vault grep** for every rule/concept/decision this session touched — already captured? **superseded / changed** since?
6. **Peers & cross-machine:** `/inbox` + `_machine-bus` + consensus commits — "всё, о чём мы договорились" on the OTHER machines; did a peer already decide, or undo, this?
7. **Declined journal:** skill `/declined` — did we already reject something this session quietly re-did?

⚠️ **Настройку ПРИЛОЖЕНИЯ спрашивай у `ccd_settings`, а не грепом по конфигам** (замер 12.10.2026, NODE-0X, сессия «Компьютер тормозит»). оператор заказал обход флота «где у нас рутины по архивации»; я проверил `~/.claude.json` и `~/.claude/settings.json`, получил ноль и объявил «автоархивации нет». Живой архиватор стоял **On** всё это время: аккаунтная настройка `auto_archive_on_pr_close` в ТРЕТЬЕМ файле (`claude_desktop_config.json`, `preferences.ccAutoArchiveOnPrClose`) и под ДРУГИМ именем, причём аккаунтная — то есть одна на ВСЕ устройства, и обход «по узлам» её поймать не мог. Порядок: `mcp__ccd_settings__get_settings` печатает ВСЕ настройки со значениями за один вызов; grep по конфигам — только как вторая поверхность. ⛔ Правка `claude_desktop_config.json` руками не держится: приложение переписывает файл из памяти (решение волта 07.07.2026), менять только через `set_setting`. Семья `vyvod-po-odnoy-poverhnosti`, 186 случаев.

**Attribution guard:** the Step-1 inventory is machine-wide and WILL include other sessions' artifacts (skills/scripts/commits from the fleet). Treat anything NOT created in THIS conversation as **someone else's** — flag it, never claim or re-route it.

**Output of Step 0 — one tight «🔎 сверка» block up front** (checked + verdict):
- **checked:** what I actually looked at (N retros / chats / vault / peers).
- **✅ aligned** — this session's calls match the collaboration; or
- **⚠️ drift** — session did X but [[note/decision]] elsewhere says Y (superseded / contradicts / already undone) → flag for dev; or
- **🔗 to propagate** — session's durable work not yet in vault / peers / Bible → route it in Step 4.
If a parallel session already captured the durable item, **SKIP re-capturing** — just cross-link.

## Step 1 — Inventory (deterministic first; AK-47, ~free)
Ground the recap in facts, not memory alone — run the SHARED inventory script (same one the daily sweep uses, so the logic never drifts):
- `python "$IMPORTS_ROOT/retro_inventory.py" 1`  (arg = days; widen for a multi-day session)
- It prints `BUILT_ARTIFACTS <n>` and writes `$IMPORTS_ROOT/retro_candidates/digest-latest.md` — Read that digest: new/changed **skills**, **_imports scripts/sidecars**, **durable notes** (Protocols + Concepts), and recent **descriptive vault commits**.
- (⚠️ a concurrent Claude-Desktop fleet may interleave vault commits — its are descriptive; the terse `pre-intervention` ones are auto-backups.)
- **Cross-check** with what you (the agent) created/edited in THIS conversation: skills, scripts, vault notes, memory entries, `CLAUDE.md` edits, decisions made, rules captured, things flagged for dev.

## Step 1🧠 — ПАМЯТЬ СЕССИИ: сироты по worktree + машинно-невидимые опровержения (дверь §8.6; добавлена 2026-09-02)
Сессия из worktree пишет память в СВОЮ проектную папку, домашний индекс о ней не знает — замер 02.09 на NODE-0X: 20 таких заметок, одна несла вердикт, опровергнутый через девять дней в соседней папке. Два прогона, 0 LLM, 0 сети:
- `python ~/.claude/scripts/memory_harvest.py --scan` → есть ORPHAN → `python ~/.claude/scripts/memory_harvest.py --harvest` (копия домой + указатель в `MEMORY-archive.md`; оригинал НЕ трогается). Exit 3 = `NEEDS-HUMAN` (тёзки припаркованы, ничего не потеряно) → строкой оператору, не молча.
- ⚠️ **Прибор даёт ложное «чисто» (замер 10.09.2026, NODE-0X):** `--scan` напечатал «0 missing pointer(s) to repair», а указатель на свежую заметку (`zenodo-publish-rail`, дописан 07.09) из `MEMORY.md` за ночь исчез — сироту он не увидел, потому что сверяет не ту пару папок. Поэтому ПОМИМО прогона сверь руками указатели на заметки, которые ЭТА сессия и пара прошлых записали: `grep -c "<слаг>" <проектная-папка>/memory/MEMORY.md`.
  ⛔ **0 в MEMORY.md ещё НЕ значит «пропало»** (замер 24.10.2026, хаб, цена ошибки = сессия починки по уже закрытому корню + ложная строка «класс неизлечим»): ночная уборка Маяка ШТАТНО сворачивает INBOX в `MEMORY-archive.md`, и указатель живёт там. Полный список поверхностей перед словом «потерялось»: `MEMORY.md` → `MEMORY-archive.md` → шард узла. Нашёл в архиве = всё в порядке, строку НЕ дописывать (иначе родится дубль). Корень этого был закрыт журналом ещё 10.09.2026, но жил только в Breakage-Journal, поэтому его переоткрывали заново. Класс = `memory-index-line-lost-overnight`, 4 датированных случая, корень чинится отдельной сессией.
- `python ~/.claude/scripts/memory_inject_lint.py --scan` → анти-инъекция и секрет-паттерны memory-стора (порт bb plugins/memory, 05.09.2026): exit 1 = НОВАЯ находка против baseline — разобрать тем же заходом (чужая закладка? секрет в памяти → в secrets-стор); старый долг молчит ратчетом. Это ЕДИНСТВЕННАЯ дверь линта ([[rule-needs-a-door-quota]]).
- `python ~/.claude/scripts/memory_epistemic.py --lint` → `SELF-TOMBSTONE` (заметка сама пишет, что устарела, а машина этого не видит) закрыть тем же заходом: `--close <слаг> --superseded-by <слаг-преемника>`. Отмена закрывается ПОЛЯМИ (`status`/`valid_to`/`superseded_by`/`refuted_on`/`refuted_by`) во ВСЕХ копиях слага, а не переписыванием одной: CLAUDE.md §8.4-бис + [[memory-records-close-by-fields-not-rewrite]].
  - ⛔ **НО СНАЧАЛА ПРОЧИТАЙ НАЗВАННЫЙ МАРКЕР ГЛАЗАМИ — вердикт линта тут бывает ложным** (замер 06.10.2026, хаб). Линт мэтчит маркеры ПОДСТРОКОЙ (`MARKERS` ~строка 216, например `re.compile(r"\bSUPERSEDED\b")`), поэтому слово из предметного словаря читается как заявление заметки о себе: живая память `adopt-framework` попала в `A-BODY-ONLY` в ДВУХ копиях из-за перечисления имён состояний движка ADOPT — «терминалы DROP/CONFIRMED_EXISTING/SUPERSEDED/RETIRED». Заметка ничего про себя не отменяла. Это семья `sshivka-po-tekstu-a-ne-po-klyuchu` (58 случаев), и правило «закрой тем же заходом» без проверки прямо толкает закрыть ЖИВУЮ запись как отменённую. Порядок: `grep -inE "<маркер>" <файл>` → прочитать ВСЕ попадания → маркер стоит внутри перечисления, кодового блока или цитаты = ложное срабатывание, НЕ закрывать, а завести строку в журнал поломок на семью. Преемника тоже назови по улике: нет названного `--superseded-by` — значит закрывать нечем.
- Обоим прогонам вердикт в отчёт строкой: «🧠 память: N сирот перенесено · M опровержений закрыто» (или «чисто»). Молчание ≠ чисто.

## Step 1🩹 — ГЕЙТ ТРЕТЬЕЙ ПОЛОМКИ (дверь §5.10; добавлена 2026-08-14 после «а корни починил?»)
Зеркало гейта из `/tt` §Шаг 3 — тот стоит на СБОРКЕ, этот на ЗАКРЫТИИ сессии, потому что сессия без изменённого кода `/tt` не зовёт и до 14.08 её поломки не попадали в журнал НИКУДА (ровно этот пробел вскрылся вопросом оператора: ретро описало поломки прозой в ноте и назвало это починкой).
Перечисли поломки/уроки ЭТОЙ сессии (свои сбои, сбои рельс, «оно молчало», неверный вывод, пойманный позже). Для каждой поломки **СНАЧАЛА**, до выбора имени класса и до записи, найди смысловую семью:
```
python "$HOME/.claude/scripts/prior_art.py" class "<описание поломки своими словами>"
```
exit 0 = прежних нет, «1-й датированный» правомерен · **exit 3 = это НЕ ошибка и НЕ первый случай**: прибор печатает прежние строки, их даты и СЕМЬЮ дефекта. Если напечатана `СЕМЬЯ <slug>`, используй именно её как `<класс>`. ⭐ ВЕРДИКТ ЧИТАЙ ПО СТРОКЕ «СЕМЕЙНЫХ: N · СЛОВЕСНЫХ: M» (правка прибора 05-06.10.2026): «это НЕ 1-й случай» и счёт §5.10 держат ТОЛЬКО семейные. `СЕМЕЙНЫХ 0` при любом M = скорее всего 1-й случай; имя бери по предмету ремонта ЭТОЙ поломки, а из раздела `[словесное совпадение, в счёт §5.10 НЕ идёт]` имя НЕ брать — до правки там рядом с роднёй стояли переименование репо и врущий поиск в конфигураторе. Глазами видно одну семью → допиши её в `FAMILIES` ОДНОЙ строкой с красной пробой в обе стороны. При `exit 0`, когда прежней строки нет, назови класс по текущему предмету ремонта/нарушенному инварианту и запиши как 1-й датированный случай; канал, код возврата, текст алерта и симптом классом не являются.

ТОЛЬКО ПОСЛЕ этого запиши ОДНУ строку через дверь `python "$HOME/.claude/scripts/selfheal.py" journal --class <класс> --what "<что>" [--conditions --parts --guess --status]`: **что · условия · сопричастные (файлы/рельсы/узлы) · гипотеза 🤔 или ✅ доказанная причина**. ⛔ НЕ править `Breakage-Journal.md` напрямую (ни Edit, ни heredoc): это общий Syncthing-файл, вид рисует один владелец из пер-узловых шардов, прямая правка отбивается хуком `breakage_write_guard` и терялась (04.09: 76 строк в 11 конфликт-копиях) — память [[breakage-journal-per-node-shards]]. Счёт бери из фактического ответа `selfheal.py`: дедуп означает, что новой строки нет.

Дальше по семье: 1-й = строка · 2-й = строка + уточнить условия · **3-й датированный = класс системный**. Внутри `/retro` причинную цепочку НЕ строй: используй ровно одну отдельную ВИДИМУЮ repair-сессию, чей первый явный вызов — `/five-whys <класс>` в Claude или `$five-whys <класс>` в Codex, с датированными строками серии. Если `selfheal.py` уже поставил её в очередь, вторую не создавай. Механизм/робота на 1-2 случае НЕ строить. Дефект новой семьи → дописать её в `FAMILIES` внутри `prior_art.py` ОДНОЙ строкой, иначе следующая сессия снова назовёт его «первым».
- ⭐ **Семья доказана → её финиш = файл двери с красневшим тестом, не строка памяти** (замер 01.10.2026, NODE-0X: двери утреннего разбора не построены, вечером обе семьи повторились). На NODE-0X вердикт закрывает `python3 ~/lab/bin/door_ledger.py check` (реестр `~/lab/state/doors.tsv`; exit 1 = доказанная семья без двери → строим или `deferred:<дата>` с причиной); на других узлах прибора нет → пометка «door_ledger: нет на узле» и сверка руками.
- ⚠️ **Завёл новую семью — обязательна КРАСНАЯ проба в том же заходе** (замер 21.09.2026, NODE-0X, ошибся дважды подряд): широкие ключи (`argv`, `206`, `тело промпта`) намели 77 чужих случаев и прибор объявил «порог §5.10 пройден»; вторая редакция утащила соседнюю семью «передали ПУТЬ вместо тела» — то же лицо, другой корень. Проверка обязана идти в ОБЕ стороны: чужой симптом НЕ ловится (`grep -c` = 0) И свой ловится. Ложно раздутый счётчик хуже отсутствующего: он заказывает сессию починки, которой не нужно быть. Канон: память `class-counted-by-name-never-reaches-three` + CLAUDE.md §5.10.
- ⚠️ считая случаи, класс определяется КОРНЕМ, а не поверхностью: «двое пишут одновременно» ≠ «состояние ушло вперёд, пока мой контекст стоял» — лечения разные. Сомнение «занижаю ли счётчик, чтобы не строить?» разрешается грепом по журналу вслух, а не суждением.
- Карв-ауты «чиним сразу, не ждём третьей»: артефакт, собранный этой же сессией · KEEP-ядро (sync, бэкапы, секреты, QQQ, рельсы наружу, deadman) · потеря данных · безопасность · деньги · соврал сам прибор · fail-closed гейты. Для KEEP-ядра, потери данных, безопасности, денег и совравшего прибора та же отдельная видимая `/five-whys`/`$five-whys`-сессия запускается немедленно; анализ внутри `/retro` не вести.
- ⚠️ **Дедуп двери отбивает УТОЧНЕНИЕ к своему же классу** (замер 10.09.2026, NODE-0X, дважды за один
  заход): `selfheal.py journal` отвечает «СТРОКА НЕ ЗАПИСАНА (дедуп: этот класс уже журналился
  недавно). Поправку к своей строке правь в журнале явно» — а прямая правка `Breakage-Journal.md`
  ЗАПРЕЩЕНА хуком `breakage_write_guard` (см. абзац выше). Инструкция сама себе противоречит.
  Пока корень не починен, обход: уточнение 2-го случая (условия, свежие цифры, порог третьего)
  кладётся в **задачу реестра** класса и в **ретро-заметку**, а в отчёте пишется честно
  «дедуп отбил, уточнение легло в <адрес>». ⛔ Молча проглотить отбой нельзя — иначе
  уточнение условий теряется, и следующая сессия снова считает случай первым.
  ✅ **КОРЕНЬ ПОЧИНЕН (проверено 06.10.2026, хаб):** дверь теперь сама предлагает выход —
  `journal` при дедупе отвечает «Поправку к своей строке пиши той же дверью с флагом
  `--amend` (весит 0 случаев) или смени `--target`». Порядок: получил отбой → тот же вызов
  с `--amend` → ответ «строка 1/3» = уточнение записано. Обход через реестр/заметку больше
  не нужен; абзац выше оставлен как история класса.
- Поломок не было → одна строка «🩹 поломок нет» и дальше. Ноль строк в журнале при названных в отчёте поломках = ретро не закрыто.
- ⛔ **Синтаксис двери журнала НЕ проверяй через `--help` после `--class`** (замер 09.10.2026, NODE-0X, класс `cli-door-writes-row-on-help-flag`): `selfheal.py journal --class X --help` справку не печатает, а ПИШЕТ строку «не описано» и поднимает счёт класса. Так класс стал ложно 3 из 3 и породил заявку на сессию починки с карточкой в 10-Tasks; пришлось чистить шард узла руками и закрывать заявку `selfheal.py repairs --close`. Синтаксис смотри `grep -n journal selfheal.py`.
- Канон: Библия `reglament-mekhanizm-tolko-posle-tretey-polomki` + CLAUDE.md §5.10 + `reglament-pyat-pochemu-koren-po-serii-sessiy` §«Три инструмента»; проверка двери — `python ~/.claude/scripts/rule_home_guard.py mekhanizm-tolko-posle-tretey-polomki`.

## Step 2 — Summarize the arc ("сегодня мы поняли")
3–7 beats: starting idea → what got built → key realizations → what was decided. Honest, concise, his voice. This is the "Stan at the end of South Park" recap.

## Step 2🎙 — Вердикт кофаундера (Майк) — canon 2026-07-07, applied 2026-07-31
Right after the arc, Майк speaks as co-founder — 4 строки, без воды (canon `reglament-*` voice-through-line; восстановлен из потерянного сообщения шины, 23 дня в призраке; НЕ театр — работает ПОВЕРХ механики 28.07: если сессия дала стратегический выбор, мемо/адвокат-дьявола из [[cofounder-decision-artifact-gate]] главнее и уже сделаны):
- 💰 **деньги-линза** — что из сегодняшнего приближает выручку/оффер (цель №1/№2), одной строкой;
- 🔪 **что убил бы** — самая слабая трата времени сессии, которую завтра не повторяем;
- 🤺 **спарринг-аудит** — где я сегодня поддакнул вместо спора (провал роли §1.2) либо «спорил честно»;
- ❓ **вопрос** — один направляющий вопрос оператору на завтра.
Пустышку не писать: сессия чисто механическая без бизнес-среза → строка «🎙 Майк: бизнес-среза нет, чисто инфра» и дальше.

## Step 3 — Classify each artifact (Keep / Drop / Try) + tested? audit
For every thing made this session, also AUDIT a **tested? ✅/❌** column — did it pass `/tt` (=`/test`) when built? Retro does NOT do the testing itself (too late/cold at session end); it only audits the line. Any durable artifact that is **❌ or untested** → flag it + offer to run `/tt` on it NOW (per [[test-after-build-skill]]).
⭐⭐ **И ВТОРАЯ КОЛОНКА — перепроверено? ✅/❌** (dev 13.09.2026, CLAUDE.md §4.3-бис): «протестировано» и «перепроверено вторым, ДРУГИМ заходом» — разные вещи, и ложное «готово» живёт именно в зазоре между ними. Артефакт, у которого первый прогон зелёный, а второго захода не было, ретро помечает ⚠️, а НЕ ✅, и предлагает прогнать Шаг 4.9 скилла `/tt` сейчас. Замер архива 15.08→14.09: 21 раз за месяц оператор спрашивал «ты точно починил?» сразу после моего «готово». Канон: [[done-is-a-claim-recheck-twice]].
⭐ **И ТРЕТЬЯ КОЛОНКА ДЛЯ ПРИБОРОВ — покрытие N/M** (dev 01.10.2026, класс `instrument-blind-to-most-of-its-subject`): у каждого собранного или тронутого за сессию прибора (сторож, аудит, счётчик долга) ретро выписывает строку `СЛЕПАЯ ЗОНА:` из его вывода (`python3 ~/.claude/scripts/_shared/blind_zone.py --run <прибор>`). Строки нет (exit 3) → ⚠️ и правка прибора тем же заходом. Покрытие <90% → ⚠️ + задача на подъём покрытия. Число без слепой зоны в отчёте ретро не ставится.

⭐⭐ **И ЧЕТВЁРТАЯ КОЛОНКА — ЧТО ВЫНУТО ИЗ ЗНАМЕНАТЕЛЯ** (класс `gate-demands-what-the-cap-forbids`, 4 датированных случая, починка 08.10.2026): у каждого прибора, судящего по ДОЛЕ, ретро выписывает строку `ЗНАМЕНАТЕЛЬ:` из его вывода (`python3 ~/.claude/scripts/_shared/denominator_guard.py --run <прибор>`) и один раз за сессию гоняет подметальщика (`… denominator_guard.py scan ~/.claude/scripts`). Строки нет (exit 3) или границы не объявлены (exit 1) → ⚠️ и правка прибора тем же заходом; НОВОЕ место у подметальщика (exit 1) → ⚠️ и либо починка, либо `--accept-baseline` с названной причиной. Смысл: доля, в знаменателе которой лежит ЗАПРЕЩЁННОЕ правилом или НЕВОЗМОЖНОЕ физически, делает PASS недостижимым и называет ложные имена больных — такое число в отчёт ретро не ставится. Память [[denominator-holds-only-the-allowed]]. Then classify:
- 🟢 **Keep & reuse** — permanent infra or a tool you'll run again (skills, durable notes, reusable scripts).
- 🟡 **One-off** — served its purpose; if the *pattern* is worth remembering, capture the pattern (not the artifact), then let it rest.
- ⬆️ **Promote** — currently ad-hoc but should become permanent → turn into a rule / skill / memory.

## Step 3🔨 — ПАНЕЛЬ ШЕСТИ ЛОМАТЕЛЕЙ, В КАЖДОМ РЕТРО (⭐ dev 06.10.2026: «ВСЕГДА … во ВСЕХ РЕТРО»)
Без исключений: и полное ретро, и полоса `push3`, и сессия без кода. Шесть **средних** моделей
через OpenRouter: 3 Китай (GLM-5.3, DeepSeek V4 Pro, Qwen 3.7 Plus) + 1 Европа (Mistral Medium 3.5) +
2 США (GPT-6 Sol, Grok 4.3). Поправка 07.10 (оператор): «Мистраль два раза не надо», второй EU-семьи
на OpenRouter нет. ⛔ Фронтир не берём (Fable, gpt-6-astra, glm-prime, kimi-k3, gemini-pro, grok-4.7),
⛔ примитив тоже (luna, flash-lite, small, haiku). Состав живёт в одном месте:
`RETRO_FAN` в `orouter_review.py`, тест `_test_orouter_fan.py`. Имена моделей вручную
в этот skill не копировать.

**Разрешение уже дано:** оператор 06.10 потребовал платную панель в каждом ретро,
07.10 подтвердил состав, 19.10 повторил: «меньше цента — это пофиг» и «чини, чтобы
шесть панелей шести ломателей работало». В рамках согласованной панели и действующего
лимита OpenRouter выполняй её сразу. Повторный аск из-за самого факта платного API
не нужен. Это не разрешение менять лимит, подписывать новый договор или запускать
неограниченные платные задания. Цена одного GLM-ответа не является ценой всей панели.

Сначала `panel --help`, затем одна штатная команда:
```bash
python ~/.claude/scripts/cc-review/orouter_review.py panel --preset retro --role break --effort medium --task retro-<sessionId> --context-file <файл> --receipt-file ~/.claude/scripts/cc-review/reviews/retro-<уникальный-id>.json
```
До запуска возьми lease на точный свежий receipt-файл. Полные ответы остаются в
приватной папке `reviews/`; usage хранит метаданные, путь и SHA. Ошибка записи
квитанции или расходов не даёт зелёную приёмку. Повтор использует новое имя файла.
Нет `--preset` в установленной версии → `RUNNER_OUTDATED`: сверить и восстановить
рассмотренную версию runner и его тест на этом узле. Не перебирать старые `--lane`
и не подменять состав копией списка. HTTP-ошибка одной модели не означает отказ
всего OpenRouter. Доступность и старые 404 перепроверяются живым вызовом; privacy,
ключи и лимит аккаунта без отдельного разрешения не менять.

Приёмка панели: шесть содержательных **финальных** ответов, фактическая модель на
каждом месте, ошибки/finish reason/цена отдельно. Reasoning без финального ответа,
пустой ответ, молчание и ответ другой модели не считаются ответом заказанного места.
`exit 0` произвольного старого runner не доказывает 6/6. Ретро-preset имеет отдельный
лимит ответа и времени; обычные вызывающие сохраняют прежний контракт. При нехватке
лимита сначала устрани измеренную причину, не объявляй reasoning готовым ревью.
Отказ провайдера принять заказанный effort и повтор без него отмечай как downgrade:
это место не проходит исходный контракт. Поле effort подтверждает запрос, не внутреннее
мышление провайдера. Полные ответы видны в приватной квитанции и stdout; общий usage
содержит только метаданные. В сырой квитанции `content_and_cost_passed` оценивает ответы
и расходы; итоговый `passed` после записи логов находится в `RETRO_PANEL_JSON` и exit code.
**Что кормить** (файл ≥200 символов): черновик этого ретро (Keep/Drop/Try + выводы «сегодня мы
поняли») + дифф или суть собранного кода, если он был. Вопрос панели: «где выводы ретро неверны,
что сломано, что я назвал готовым без улики». Секреты и личные данные отбивает сам прибор до
сети: увидел отказ `refused-secret/private` → вычисти и повтори, а не пропускай панель.
**Отчёт одной строкой:** `🔨 панель: N из 6 ответили · $X · принято K находок (какие) · отклонено M (почему)`.
Каждая принятая находка = правка в ТОМ ЖЕ заходе или строка в Step 3⛳; несогласие называю
вслух с доводом (§1.2-бис: панель не обязывает соглашаться, обязывает ответить).
Ответили <6 из 6 → в отчёт `⚠️ панель неполная` с именами и причинами по каждому
неготовому месту. Независимая работа продолжается, а починка/добор остаются открытыми;
полную приёмку панели и «6/6» объявляй только по шести финальным ответам.
Траты пишутся в полосу `retro` (`~/.claude/_metrics/openrouter-spend.jsonl`).
🌾 **Урожай 06.11.2026:** свести траты полосы `retro` за месяц и показать оператору: оставить, урезать, выключить.
Исторические прогоны: 06.10 6 из 6 за 215 с, $0.47; 07.10 6 из 6 за 181 с, $0.31.
Свежий контроль 19.10: старый runner напечатал 6/6 при пяти финальных ответах и одном
DeepSeek reasoning-only с лимитом 4000. Это ложный зелёный результат прибора, не
поломка всего OpenRouter. Финальный исправленный прогон подтверждается своей квитанцией.

## Step 3📋 — Journal sync (реестр задач; dev's decree 2026-07-04)
Retro is the SAFETY NET of the task journal ([[task-journal-done-undone-linking]]): the in-session reflex («сформулировал → сразу в реестр») catches tasks at birth; retro catches what slipped. Two moves, both against the ONE journal ([[task-backlog-registry]] — **v2 markdown-first, SHIPPED 2026-07-07**):
- **Источник истины = markdown-заметки** `$OBSIDIAN_VAULT/10-Tasks/task-*.md` (шаблон `_Task-Template.md`, MOC `_Tasks-MOC.md`). Синкаются флоту, поэтому работают с ЛЮБОЙ машины без шины и без движка. Завести задачу = новый файл `task-ГГГГ-ММ-ДД-слаг.md`; закрыть = правка frontmatter (`state`/`status` + evidence). Схема строгая: неизвестный `state`/`prio` → `schema_errors` в аудите, а не тихий дефолт.
- **Витрину и аудит строит индексатор** `tasks_index.py` (markdown → `_Dashboards/Task-Backlog.html` + `10-Tasks/_audit/audit-latest.json`). Он крутится ночью на Маяке как ЕДИНСТВЕННЫЙ писатель — руками на хабе/ноуте его НЕ запускать (два писателя одного синкаемого дерива = sync-conflict).
- ⛔ Старый SQLite-движок task-registry (жил на ноуте NODE-0X) = **аварийный fallback, снят с вооружения**; на хабе его нет и не должно быть. Не зови его и не «восстанавливай» — v2 его заменил. (Имя намеренно без code-формата: backtick = «это надо запускать».)

Две операции ретро:
- **Сессия рождена из сида Task-Now?** (первое сообщение начинается «Продолжи задачу task-…» или «Реши СУДЬБУ задачи task-…») → обнови frontmatter ЭТОЙ задачи прямо сейчас: state/touched_at, при done — evidence+outcome; сид без обновлённого frontmatter = петля Task-Now разорвана (v4, dev 2026-08-20).
- **Closed this session** → mark `done` **with evidence** (the /tt proof, commit, counter) + link what it unblocked. Claimed-done without proof → flag, don't close.
- **Still open** (every «📌 Open item», seed prompt, deferred tail, «потом») → ensure it EXISTS in the registry with a link to where it was born + prio/type. Nothing from the open-items list may live only in the chat transcript.
- ⏱ **РАЗРЕЗ ОЖИДАНИЯ (добавлено 07.09 после того, как этот шаг сам породил долг):** у каждого открытого пункта вида «ждём замера / ещё копим / не проверено» спроси — **какая его часть НЕ требует времени?** Почти всегда внутри склеены два вопроса: УСТРОЙСТВО («работает ли конструкция») проверяется детерминированным прибором за минуты, СПРОС («пользуемся ли мы этим») действительно требует недель. Часть про устройство закрывается **в этом же заходе**, а не переносится в реестр. Замер, из-за которого пункт появился: ретро 06.09 записало «гипотеза ДР не проверена, урожай 08.09» — на деле 5 ног гипотезы закрылись прибором за пару минут 07.09, а ждать надо было только спроса. Обязательные подпорки при таком закрытии: **красный контроль** (зелёная нога пустая, пока не показано, что прибор видит поломку) и **независимая линза чужим кодом**, если вывод тебе выгоден. Канон: память [[architecture-proves-in-minutes-demand-needs-weeks]], CLAUDE.md §5.4.
Announce the delta in one line: «📋 журнал: +N новых · ✅M закрыто · без изменений K». Don't duplicate neighbor registries (DR-реестр, improvements-backlog, declined) — link, не копируй.

## Step 3🗺 — Roadmap checkpoint (dev's decree 2026-07-16: «в каждом ретро — как мы продвинулись по roadmap»)
Канон = `$OBSIDIAN_VAULT/04-Projects/ROADMAP.md` (живой публичный роадмап для фолловеров). Три движения, все против ЭТОГО файла:
- **Продвинулись** → отметить чекбоксы/статусы, веху уровня «фолловеру интересно» → строка в Ship log с датой.
- **Появилось новое направление в сессии** → добавить в NOW/NEXT/LATER (не дублируя детальные планы — ссылкой).
- **Ничего не двинулось** → честно сказать это в отчёте (тоже сигнал).
Announce одной строкой: «🗺 roadmap: ✅N продвинуто · ➕M добавлено · ⏸ без движения». Публичная проекция файла наружу — только через контент-гейт (Нора), ретро наружу не постит.

## Step 3🔗 — Connect check (построено → передано → ИСПОЛЬЗУЕТСЯ?) — dev 2026-07-04
Правило Connect ([[connect-rule-pipeline-ownership]]) на подведении итогов: для КАЖДОГО артефакта этой сессии довести цепочку до конца — **«собрали» это ещё НЕ финиш**. Финиш = построено → передано потребителю → **реально используется**. Три исхода на артефакт:
- ✅ **используется** — есть потребитель и он потребляет (скилл вызывают, рутина читает выход, поле CRM читают, дашборд открывают, данные доехали и применены). **Назвать потребителя** — иначе это не ✅.
- 🔗 **передано, потребления пока нет** — доехало, но никто ещё не читает/не применяет → на доску висячих, назначить потребителя/срок.
- ⚠️ **построено «в воздух»** — собрали и бросили, потребителя нет вовсе (dead-letter без consumer — как релинк-очередь: 29k сирот, 0 применено) → **ПОДСВЕТИТЬ оператору явно**: «построили X, но это никем не используется» → решить: подключить потребителя ИЛИ признать выброшенным.

Молчание ≠ используется. «Построили» без названного потребителя = недоделанный Connect, НЕ «done». Строкой: «🔗 Connect: ✅N используется · 🔗M передано-ждёт · ⚠️K в воздух».
⭐ **🌍 МИРОВОЙ ПОТРЕБИТЕЛЬ (dev 24.08, голосом):** у каждой закрытой за сессию починки КЛАССА — четвёртый исход Connect: раздали ли миру? Сеть-ловушка: строки Breakage-Journal этой сессии «класс закрыт» без вердикта 🌍 = долг → прогнать скилл **`/share-fix`** (порог переносимости, реверс-поиск по симптому, 3-5 лучших живых тредов, gist, вахта — вся механика там). Вердикт в отчёте обязателен: 🟢 раздал (ссылки) · ⚪ искал-пусто · ⛔ непереносимо/приватно+причина. Канон: `reglament-pochinil-u-sebya-srazu-razday-miru` + память `fixed-it-share-it-with-the-world`.
⭐ **ПРАВИЛО — ТОЖЕ АРТЕФАКТ (dev 06.08: «это же связывается с правилом коннект???» — да, связывается).** Правило, принятое за эту сессию, проходит тот же Connect-тест, только его «потребитель» — не человек и не следующая стадия, а **механизм, который правило вызовет**. Записали в канон — это «передали», не «используется». Прогон обязателен, по одной строке на правило:
`python ~/.claude/scripts/rule_home_guard.py <слаг>` → **✅ ДВЕРЬ ЕСТЬ и она ИСПОЛНИМАЯ** (потребитель назван) · **⚠️ ПОХОЖА НА ФИКТИВНУЮ** (слаг пересказан прозой, путь исполнения его не тронет — считается 🔗 «передано, потребления нет») · **⛔ БЕЗ ДВЕРИ** (= ⚠️ «в воздух», подсветить оператору явно).
Квота [[rule-needs-a-door-quota]]: дверь строится в ТОМ ЖЕ заходе (строка в существующем скилле дешевле нового робота) ЛИБО правило уходит в `~/.claude/rules-without-door.md` с датой и причиной. Замер, из-за которого пункт появился: 19 из 25 свежих правил (76%) не звал ни один скилл и ни один хук; «5 почему» пролежал в каноне 42 дня и не применился ни разу. Разбор класса: `razbor-serii-2026-08-06-pravilo-prinyato-dveri-net` (волт).
⭐⭐ **ПОЛЬЗУ НАШЛИ — ДАЛИ ФЛОТУ (dev 06.08, капсом «ВСЕГДА!! даже не спрашивай меня»).** У ОБЩЕЙ детали потребитель — не один человек, а **каждый узел флота**, поэтому Connect на ней закрывается только раскаткой. Прогон, по строке на сессию: `python ~/.claude/scripts/fleet_fix_audit.py --by-fix <id>` → кто применил, кто отстал. Исходы: ✅ **применено на всех потребителях** (доказано чтением факта на узле) · 🔗 **зарегистрировано, узел офлайн** — единственное законное ожидание · ⚠️ **осталось на одной машине** = «в воздух», подсветить. ⛔ Запрещено закрывать ретро строками «раскатать?», «жду ОК», «добью завтра» — раскатка не Tier-2 и не руки оператора, значит по §4.1 её решаю я, в ТОМ ЖЕ заходе. Раскатывается не только патч, а любая НАЙДЕННАЯ ПОЛЬЗА (приём, ожившая рельса, обнаружение что подписка идёт не в тот бак, грабли со стоимостью); тест — «пригодится другому узлу или оператору?». ⛔ `apply`, который не ДОСТАВЛЯЕТ файл, регистрировать нельзя — это корень висящих посылок (замер 06.08: 128 штук, apply был `doctor`, на Маяке лежал новый тест поверх старого движка). Живой узел по `tailscale status` → еду сам (ssh + `deploy_apply` НА УЗЛЕ), офлайн → готовые команды в шину. Канон: [[found-value-goes-to-fleet-always]], Библия `reglament-lyubaya-pochinka-raskatyvaetsya-na-ves-flot` §Поправка 06.08.
⚠️ **Грабля 10.09 (NODE-0X):** `fleet_fix_audit.py` стоит за `maintenance_gate` (§10.0, один прогон в сутки на узел) — второй заход за день отбивается. Уже гоняли сегодня → бери вывод ночной карты / `deploy_check.py`, `--force` только с названной оператору причиной. Отбитый гейтом аудит НЕ повод молчать: проверь `PENDING-<узел>` и скажи честно, что доказана РЕГИСТРАЦИЯ, а не применение.
**Исключение — R&D-пробник (грань 5 реглумента, DR26-07-04-HUB-13):** явно помеченный эксперимент с живым time-box + learning-метрикой НЕ считается ⚠️ «в воздух» — он 🧪; но пробник с ИСТЁКШИМ time-box без потребления/вывода = ⚠️ → авто-kill (архив), без sunk-cost-переговоров. «Используется» = смена состояния (применено/закрыто/записано), не «открыл» (Goodhart). Не дублирует журнал (Step 3📋) — журнал ловит «открыто/закрыто», Connect ловит «есть ли у построенного потребитель и потребляет ли он».

## Step 3🚂 — РЕЛЬСЫ: честный процент по чужим LLM + причины недобора (dev 21.09.2026, голосом)
Дословно: «я использовал такие-то LLM на какое-то количество процентов, а не использовал по каким-то причинам. То есть ты ещё называешь честные причины, почему ты не использовал. Забыл ты или какие-то другие причины. И сразу пытаешься поправить этот скилл».

Почему шаг живёт тут, а не в §6.3: правило «выгребай лимиты» стоит с 04.08, дверь `llm_ask.py` построена 06.08 — и всё равно замер 21.09 дал grok 0 вызовов на узле за 7 дней при $300/мес. Корень назвал оператор сам: **забыл**. Забывание невидимо, пока обещание не машиночитаемо.

Один прогон, 0 токенов:
`python ~/.claude/scripts/rail_plan.py verdict --session <id>` → таблица «обещано / вызовов факт / вердикт».

⛔ **`<id>` — ЭТО CLI-SID, А НЕ ТОТ, ЧТО ОТДАЁТ `get_session self`** (замер 06.10.2026, хаб, ретро сессии SMB; класс `session-has-two-ids-instrument-asked-wrong-one`, семья из 7 случаев — порог §5.10 пройден). У сессии ДВА идентификатора в разных пространствах имён:
- **CCD-шный** `local_e9daa1ed-40f5-...` — его печатает `mcp__ccd_session_mgmt__get_session`, он нужен шагам 6a-тер / 6a-кватер;
- **CLI-шный** `262f2548-373f-...` — это `CLAUDE_CODE_SESSION_ID`, то же, что **имя папки перед `scratchpad`** в системном промпте. Именно с ним `declare` связывает план.
`_plan_of()` сличает строки СТРОГО (`rec['session'] != session → continue`), поэтому вердикт по CCD-шному id печатает **«ПЛАНА НЕТ: сессия не объявила рельсы на старте — это и есть нарушение приказа 21.09»** на сессии, которая план объявила и получила «OK план записан». ⚠️ Это ложное обвинение себя, а не замер: прибор не врёт, врёт выбор id. Возьми id так (та же дверь, что у 6a-бис):
```bash
python -c "import sys,os; sys.path.insert(0,os.path.expanduser('~/.claude/scripts')); import rail_plan; print(rail_plan._env_sid())"
```
Пусто → план действительно записан без привязки (`declare` печатает про это ⚠️ своей строкой) → суди `--all-sessions` и скажи это в отчёте. ⛔ «ПЛАНА НЕТ» на первом же прогоне не объявляй нарушением, пока не пересдал вердикт с CLI-sid.

⚠️ **`--session <id>` ОБЯЗАТЕЛЕН У ОБОИХ ВЫЗОВОВ, И У `declare` ТОЖЕ** (замер 06.10.2026, ретро пресс-пасса — 6-й датированный случай, семья `rail-plan-verdict-judges-wrong-session-key`, 8 случаев с 26.09). `declare` без флага пишет план под `CLAUDE_CODE_SESSION_ID`, который в десктоп-сессии бывает чужим или протухшим, а `verdict --session <id>` читает ДРУГОЙ ключ — и второй прогон снова печатает «ПЛАНА НЕТ». Коварство в том, что `declare` отвечает **«OK план записан»**: зелёный ответ на промах по ключу. Правильно так, id берётся из `get_session self`:
```
python ~/.claude/scripts/rail_plan.py declare --session <id> --self "..." --outsource=
python ~/.claude/scripts/rail_plan.py verdict --session <id>
```
⛔ «ПЛАНА НЕТ» после успешного `declare` читать как «правило не исполнено» нельзя — сперва проверь, что в обоих вызовах стоял ОДИН id.
- **exit 0** — у каждой обещанной рельсы есть либо вызовы, либо названная причина.
- ⛔⭐ **«СВЕРКА ЗАКРЫТА» МОЖЕТ БЫТЬ ЗЕЛЁНОЙ ПРИ НУЛЕ ВЫЗОВОВ У ТВОЕЙ СЕССИИ** (замер 06.10.2026, хаб, ретро про бокс для вещей). Колонка «вызовов факт» и строка `ФАКТ за окно` считают УЗЕЛ за окно, то есть вызовы СОСЕДНИХ сессий: я обещал `web>gemini`, сам не сделал ни одного вызова (весь веб-ресёрч прошёл моими `WebSearch`/`WebFetch`), а прибор напечатал «gemini жгли, 14 вызовов» и `СВЕРКА ЗАКРЫТА`. Зелёный тут ВЫГОДЕН тебе и ложен для сессии, поэтому §5.4 («выгодный вывод требует усиленной проверки») обязывает: прежде чем принять зелёный, спроси себя, делала ли вызов ИМЕННО эта сессия — и если нет, признай недобор с кодом причины ВСЛУХ, а не прячься за узловым счётчиком. Прибор не врёт, он отвечает на другой вопрос.
- **Прибора на узле НЕТ** (`rail_plan.py: No such file`) — это НЕ повод пропустить шаг молча.
  Проверь очередь посылок (`deploy_check.py`): не применённая `rail-plan-*` применяется тут же
  (§7.5). Применить нельзя (чужая живая табличка ON AIR на зоне `fleet-code`, замер 21.09) →
  ⛔ НЕ форсить, а написать в отчёт строкой: «🚂 прибора нет, посылка <id> заблокирована
  ON AIR <узел>/<id>, применю после закрытия». Сессия СТАРШЕ самого правила (работа шла до
  21.09) → так и сказать: плана не было, потому что правила ещё не существовало, выдумывать
  задним числом проценты запрещено (§5.4 правда в цифрах).
- ⚠️ **Сессия честно всё делала сама → пустой список пиши `--outsource=` (со знаком равно).** В PowerShell 5.1 форма `--outsource ""` теряет пустой аргумент, и argparse отвечает «expected one argument»; замер 06.10 (NODE-0X), родственный корень 31.08 и 23.09 (PS 5.1 переписывает аргументы нативных команд, семья заведена в очередь на починку). Выдумывать рельсу ради принятия плана нельзя.
- **exit 1 «ПЛАНА НЕТ»** — сессия не объявила рельсы на старте. Это и есть нарушение; объявить сейчас (`rail_plan.py declare`) и сказать в отчёте честно, что план родился на ретро, а не на старте.
- **exit 1 «НЕДОБОР без причины»** — добери причины: `--reason <рельса>=<код>:<текст>`, коды `forgot · rail-dead · class-mismatch · too-small · tier2 · no-work · **own-subagent**`.
- ⭐ **`rail-dead` РУКАМИ БОЛЬШЕ НЕ ПИШЕМ, если рельсу реально звали** (правка 30.09.2026): прибор сам ставит «rail-dead (авто): N попыт., рельса упала», когда в леджере есть ПОПЫТКА. Колонка «попыток мимо» в таблице — это и есть улика. Строка «авто» = долг ПОЧИНКИ РЕЛЬСЫ (логин, квота), а не долг дисциплины: заводи задачу на рельсу, а не причину в вердикт. ГРАНИЦА: прибор доказывает попытку, а не диагноз — 401 и 429 для него одинаковы, текст ошибки вендора ищи в stderr прогона («рельса <имя> мимо: …»).
- ⭐ **Грунт сделал СУБАГЕНТ (Agent model=sonnet/opus) — это код `own-subagent`, а НЕ `forgot` и НЕ `class-mismatch`** (правка 30.09.2026). Субагент жжёт НАШ бак Anthropic, внешней рельсой не является и прибором не считается СОЗНАТЕЛЬНО; объявить его в `declare --outsource` теперь нельзя (exit 2). Замер 28–29.09: два прогона подряд весь грунт отдали субагентам, прибор напечатал ноль и заставил выдумать причину — `own-subagent` существует, чтобы подмена чужой оплаченной подписки своим баком **считалась по леджеру**, а не пряталась под «too-small».
- **Узловой срез** (что вообще этот компьютер обещал и сжёг за окно, все сессии сразу): `rail_plan.py verdict --all-sessions --days <N>`. По умолчанию сверка ПОСЕССИОННАЯ — иначе возвращается класс «вердикт судит чужой план» (8 датированных случаев 21–28.09).
- **`No such file` — прибора на узле НЕТ** (замер 21.09, NODE-0X: посылка `rail-plan-20260921` лежала непринятой, и шаг судить было нечем). Это НЕ повод пропустить шаг молча: (1) посмотреть очередь посылок `python ~/.claude/scripts/deploy_check.py` и применить её тем же заходом; (2) применение отбито правами/классификатором → строка в отчёт «🚂 сверка невозможна: прибора нет, посылка <id> не применена» + пункт в TODO. Отсутствие прибора называется вслух, а не превращается в «рельсы не жгли».

⭐ **«forgot» обязывает ПРАВИТЬ ДВЕРЬ в том же заходе**, а не объяснять. Это прямой приказ оператора («сразу пытаешься поправить этот скилл, чтобы в будущем так не ошибаться») и он смыкается с 🛠 «вердиктом о скилле» ниже: причина `forgot` = скилл/рутина пропустили рельсу, значит правится вызывающий, а не только этот файл.

Перед выводом «двери/хука нет» проверь ОБА каталога `~/.claude/scripts/` и `~/.claude/hooks/`, затем регистрацию в `~/.claude/settings.json` и фактический путь из неё. Для плана рельс на Windows проверяй `~/.claude/hooks/rail_plan_hook.cmd`. Файл есть, запись в настройках есть и хук действительно сработал в новой сессии являются тремя разными проверками. Не найдено в одном каталоге = «пока не нашёл», а не доказанное отсутствие (ошибка из ретро Multica 30.09.2026).

⚠️ **СЕССИЯ, РАСТЯНУТАЯ НА ДНИ И РЕЗЮМЫ: ПЛАН ОБЪЯВЛЯЕТСЯ ЗАНОВО ПОСЛЕ КАЖДОГО РЕЗЮМА** (замер 12.10.2026: сессия жила 4 суток 12 часов и три раза возобновлялась; вердикт на ретро ответил «ВНИМАНИЕ: плану 108 ч — он от ПРОШЛОЙ сессии» и `СВЕРКА НЕ ЗАКРЫТА: судил ЧУЖОЕ обещание», хотя план был объявлен этой же сессией, просто четыре дня назад). Прибор привязывает план к моменту, а не к `sessionId`, поэтому долгая сессия сверяет своё же старое обещание как чужое. ⛔⛔ **ПОПРАВКА 19.10.2026: СОВЕТ «ПЕРЕОБЪЯВИ И СУДИ ЗАНОВО» БЫЛ НЕВЫПОЛНИМ, НЕ ИСПОЛНЯЙ ЕГО.** Замер (сессия A56226, возраст 18 суток): `declare --session <CLI-sid>` ответил «OK план записан», записи легли в леджер с верным ключом и свежими метками — и `verdict` снова напечатал «плану 432 ч». `_plan_of` берёт ПЕРВЫЙ declare сессии **СОЗНАТЕЛЬНО**: его docstring говорит «обещание нельзя отозвать задним числом, только объяснить причиной» (правка после панели, дыру нашли Codex и Grok независимо). Переобъявление игнорируется ЗАМЫСЛОМ, значит опираться на него нельзя. **Правильный порядок на долгой сессии:** (1) `verdict --session <CLI-sid>` по ПЕРВОМУ плану, он и есть обещание; (2) недобор закрыть ПРИЧИНОЙ `--reason <рельса>=<код>:<текст>`; (3) в отчёте назвать возраст плана числом и сказать, что обещание давалось на старте, а не пересобрано. Сам прибор с 19.10 печатает это сам (посылка `railplan-stale-advice-20261019`), но если на узле старая версия — порядок всё равно этот. ⛔ Повторный `declare` объявления на старте не заменяет и недобор не отменяет.
⚠️⚠️ **НО ПОСЛЕ ПОВТОРНОГО `declare` ВЕРДИКТ СЧИТАЕТ ВЫЗОВЫ ТОЛЬКО С МОМЕНТА НОВОГО ОБЪЯВЛЕНИЯ** (замер 14.10.2026, NODE-0X, сессия ddc71972): переобъявил на ретро — и колонка «вызовов факт» показала codex 0 · grok 0 · glm 0, хотя ночью было codex 203 · grok 211 · glm 222 ок-вызовов этой же сессии. Совет выше сам рождает ложное «НЕ ЖГЛИ». Истинный счёт сессии бери из журнала использования, ключ = CLI-sid:
`python -c "import json,collections,os;c=collections.Counter();[c.update([json.loads(l)['skill']]) for l in open(os.path.expanduser('~/.claude/_metrics/part-usage/<УЗЕЛ>.jsonl'),encoding='utf-8') if '<CLI-sid>' in l and 'llm_ask:' in l and '\"ok\"' in l];print(c)"`
и пиши в отчёт ЭТИ числа с пометкой «вердикт прибора обнулён переобъявлением». Формат `--outsource` = `класс:рельса` (двоеточие); подсказка `класс>рельса` в выводе `declare` — это формат ПЕЧАТИ, не ввода.

⛔ Запрещено закрывать шаг словами «мало пользовались другими LLM» без цифр: доля считается прибором, а не на глаз (§5.4 «правда в цифрах»). ⛔ Не смешивать два числа: `rail_plan.py` считает **ВЫЗОВЫ наших рельс**, а процент выборки бака вендора живёт в `subscription_utilization.py report` — это разные величины разного происхождения.
⚠️ **ФОРМА CLI У ДВЕРИ РЕЛЬСЫ -- СПРОСИ `--help`, А НЕ УГАДЫВАЙ** (замер 08.10.2026, NODE-0X,
два потерянных прогона в одном заходе). `llm_ask.py` знает **`--prompt-file`**, а НЕ `--file`:
на `--file` он отвечает `unrecognized arguments` и exit 2, то есть ревью не уехало вовсе, а
выглядело как отправленное. Тем же заходом отбилось `orouter_review.py panel --preset retro`
(см. каветат в Step 3🔨). Правило одно на обе двери: **СПЕРВА `<дверь> --help`**, он печатает
список за секунду. Это дешевле любого перебора форм, и именно его я дважды не исполнил.

Строкой в отчёт: «🚂 рельсы: жгли <рельса=N…> · недобор <рельса:код> · правка двери: да/нет».
Канон: [[rail-plan-declared-then-verified]], [[burn-the-limits-utilization]], [[other-llm-rails-were-review-only]].

## Step 3🧺 — ЗАГРУЖЕНО ТОЛЬКО НУЖНОЕ (dev 18.10.2026, голосом: «подгружены только те скиллы, которые нам нужны, ненужное отключать»)
Плагины, коннекторы и описания скиллов полки едут в КАЖДУЮ сессию и жгут токены (замер 18.10: Sales ~3.3k tok always-on; data 868 tok и 8 мёртвых коннекторов). Шаг:
1. `mcp__ccd_connectors__session_connectors_status` → ответ в файл скретчпада `conn.json`; `ListPlugins` → имена включённых плагинов аккаунта.
2. `python3 ~/.claude/scripts/skill_load_audit.py --connectors-json <conn.json> --account-enabled <имена>` (exit 1 = есть лишнее, 2 = слепой).
3. Лишнее ≤9 объектов и обратимо → выключаю сам: `claude plugin disable <id>` / `set_session_connector_enabled false` / `disable-model-invocation: true` в SKILL.md. ≥10 или класс целиком → одна строка оператору «понял так… затронет N… откат…» (§0.7). Плагин аккаунта claude.ai → одна строка, где кликнуть (claude.ai → Customize → Plugins). Ничего не удаляю.
4. Строкой в отчёт: «🧺 загрузка: always-on ≈N tok · лишнее M (≈K tok) · выключил … · ждёт оператора …».

## Step 3🔄 — Outcome-аудит ПРОШЛЫХ правил (взято у netresearch/retro-skill «outcome mode», adopted 2026-08-26; наш обмен — issue #78 их репо)
Door-audit (Step 3🔗) судит правило при РОЖДЕНИИ; этот шаг судит СУДЬБУ уже записанных — родился с дверью ≠ живёт (замеры: 19/25 без двери, «5 почему» 42 дня без применения, Firefox-first умер тихо за 13 дней). Дёшево, ЧИТАЕМ ночные выходы, сканы руками НЕ гоняем (§10.0):
1. Возьми правила, ТЕМАТИЧЕСКИ близкие этой сессии + до 5 самых старых нетронутых из ночной карты `rule_liveness` (HTML/JSON выход ночного прогона; руками `--scan` не запускать).
2. По каждому три вопроса: применялось ли с прошлого ретро (счётчик §5.8 / упоминание в транскриптах)? нарушалось ли (Breakage-Journal)? актуально ли ещё (не superseded)?
3. Вердикт-строка в отчёт: «🔄 outcome: N проверено · M живут · K мертвы» — каждому мёртвому РЕШЕНИЕ в том же заходе: утиль (в архив с причиной) / дверь построить / отдать сессии-починке. Молча пропустить шаг нельзя; сессия без тематических правил → «🔄 outcome: чужих правил не трогал» одной строкой.

## Step 3🎙 — ON AIR check (v1.1, 2026-07-11 «+++»)
One cheap deterministic move: `python ~/.claude/scripts/onair.py list` (memory `onair-board`).
- This session's own declaration still active → `onair close <id>` — never leave a stale табличка behind.
  ⚠️ **`<id>` — это НЕ то, что печатает `list`** (замер 06.10.2026: четыре попытки закрыть свою же
  живую табличку отбились словами «no active claim», и она осталась висеть). В выводе `list` стоит
  ДРУЖЕЛЮБНАЯ метка вида `HUB/65c81288` (машина/короткий sid) — по ней `close` не ищет. `_find()`
  сличает ровно два написания: поле `id` внутри файла заявки (длинное, вида
  `2026-10-06T143143Z-HUB-01-65c81288-vault-imports-jobs-watch`) ЛИБО имя файла
  ЦЕЛИКОМ, вместе с `.json`. Возьми точное значение так:
  `python -c "import json,glob,os,sys; sys.path.insert(0,os.path.expanduser('~/.claude/scripts')); import onair; [print(json.load(open(f,encoding='utf-8')).get('id')) for f in glob.glob(os.path.join(onair.ACTIVE_DIR,'*<свой-sid>*'))]"`
  ⛔ «no active claim» на СВОЮ живую табличку читать как «её нет» нельзя: это промах по ключу.
- Session DID large structural work (canon / sync / consensus / factory redo) **without** a declaration → flag in the report: «⚠️ крупная работа шла без ON AIR-таблички» (anti-pencil-whipping; the 2026-07-08 consensus.py case).
- No claim + no large structural work → skip silently.

## Step 3⛳ — Drift-audit → сессии-детишки (dev's decree 2026-07-11: retro spawns them ITSELF, no nudges)
The retro-time CLOSURE of the drift rule ([[goal-drift-offload-to-seed-sessions]] / CLAUDE.md § «Дрифт от главной цели»): mid-flight that rule offloads weeds AS they appear; retro is the **safety net** for what slipped — the topics the session got blown into that are NOT the main goal and NOT finished.

Procedure (cheap — reuse material already in hand: Step 0 spine, Step 1 inventory, Step 3📋 journal):
1. **Name the session's MAIN goal** (turnstate spine / the first ask). One line: «⛳ цель сессии: <X>».
2. **List the drift**: topics we discussed / dug / half-built that are neither the main goal nor done. Cross-check chips already issued mid-flight — those are NOT re-spawned, only their Connect status is reported.
3. **For each REAL drifted topic retro ЗАПУСКАЕТ СЕССИЮ САМО — no asking, no waiting** (dev 2026-07-11: «команда РЕТРО активирует соседние сессии-детишки без моих пинков»; усилено 29.07: **«запрещено запускать любые сессии в чёрную»**). Запуск ТОЛЬКО видимой рельсой — `mcp__scheduled-tasks__create_scheduled_task` (`fireAt` — ТОЛЬКО из двери `python ~/.claude/scripts/_shared/fireat_now.py --in 15`, и ЕСЛИ создание отбило метку как «в прошлом» — УВЕЛИЧЬ ЗАПАС ТОЙ ЖЕ ДВЕРЬЮ (`--in 60`), руками время всё равно не пишем. Замер 01.10.2026: часы оболочки и часы приложения расходятся ~на 20 минут, а дверь берёт время из ОБОЛОЧКИ (`source local`) с маржой ровно 15 мин — то есть при перекосе больше маржи она падает по построению, руками время не писать: класс из 6 случаев 11.08-09.09, часы шелла врали до 11 ч; разносить по времени; `notifyOnCompletion: true`), чтобы сессия попала в список приложения и оператор мог её открыть, дотолкать после лимита и ответить на её вопрос. Принцип оператора дословно (29.07): **«плоди чип и САМ ЕГО НАЖИМАЙ»** — решил, что нужна сессия, значит создаёшь её УЖЕ ЗАПУЩЕННОЙ. Чип, который ждёт чужого клика, созданной сессией НЕ считается (замер: 107 из 346 чипов не нажаты никогда), а невидимый `claude -p` не считается тоже (29 сессий — в списке ноль); гейты `chip_guard.py` / `blackbox_session_guard.py` разворачивают оба случая на видимый запуск. Чип уместен только там, где нужны физические руки оператора или другая машина, с маркером `ТРЕБУЕТ РУК оператора:` / `ДРУГАЯ МАШИНА:` и немедленным пингом. Prompt = self-contained seed (Outcome · Контекст из recall · Scope · Deliverable · DoD — формат из [[decompose-into-parallel-sessions]]), сессия стартует с нуля без контекста этой. Register each launch in the task journal (Step 3📋) too — сессия AND registry entry, never either-or.
4. **Threshold & cap:** only a real weed (discussed seriously / carries value / would otherwise be lost) — not every stray thought; **≤5 запусков per retro**, the rest goes journal-only.
5. **Report line:** «⛳ дрифт-аудит: цель <X> · унесло в N тем → 🚀M сессий запущено (видимых) · ♻️K выданы по ходу · 📋J только в журнал». No drift → one word («⛳ дрифта нет»), skip the ceremony. Канон: Библия `reglament-zapreshcheno-zapuskat-sessii-v-chernuyu`.

Distinct from Step 4★ (repeats → skill) and Step 3📋 (open/closed bookkeeping): this step catches **abandoned directions** and hands each one a clean child session. Fires (data loss / security / sync down) are never «drift to defer» — they were handled in-session or escalate now.

## Step 4 — Route durable items to their home (per `operating-agreement` → "Where durable rules go")
- Reusable **tool/script** → record in **memory** (path + when to re-run) so it's findable next time.
- Behavioral **rule about how I work** → global `CLAUDE.md` (short pointer) / a skill / memory / hook.
- Team/agent **rule** (acting for dev) → the **Bible** (`reglament-*`, via skill `bible`).
- A genuinely-recurring **ritual** → its own skill.
- **Don't duplicate** — each level points down, never copies (AK-47).
- **🏠 Home-matrix audit (gate; canon `reglament-vyuchennoe-zapisyvaetsya-vo-vse-doma-matritsa`):** for EVERY rule/lesson captured this session, list all 6 homes (Bible · CLAUDE.md · memory+MEMORY.md · skill · hook/task · MOC) with an explicit ✅ written / ⛔ not-needed+reason — no silent skips — then prove by counter: `python ~/.claude/scripts/rule_home_guard.py <slug/keywords>` (exit 1 = no always-loaded trace → fix before closing the retro). ⚠️ Грабля 10.09 (NODE-0X): этот прибор ТОЖЕ стоит за `maintenance_gate` (§10.0, один прогон в сутки на узел) — на 5-м заходе за сутки он отбивается, и «доказать счётчиком» становится нечем. Тот же класс, что каветат про `fleet_fix_audit.py` в Step 3🔗. Отбило → либо `--force` с названной оператору причиной, либо честная строка в отчёте «дверь проверена глазами, счётчик отбит суточным гейтом» — молча пропускать проверку нельзя.

## Step 4🌍 — КОНТРИБЬЮТ-ТЕСТ (dev 11.08.2026: «как поймём, что это РЕШЕНИЕ тоже контрибьютим?»)
For EVERY artifact classified **Keep-&-reuse** this session, run the 3-question contribution test (canon lives in `~/.claude/skills/rep-reply/SKILL.md` § «Пополнение карты» — do not duplicate the wording, read it): (а) боль универсальная? (б) чужие живые треды есть (30-сек gh search)? (в) отдать можно без утечки? **Two «да» out of three** → write the row into the rep-reply theme→artifact map + mark the artifact as a `/release-slice` candidate; otherwise record the explicit ⛔ with which question failed. No silent skips — the verdict per artifact goes into the retro report. This is the door that turns "we built know-how" into "the world heard about it" without anyone having to remember.
**⭐ Усиление dev 01.09 (голосом ×2, канон `reglament-retro-smotrit-naruzhu-tizer-i-skill-v-mir`):** ретро = СУДЬЯ (~1 мин на артефакт), не раздатчик — замер 01.09: полный качественный проход = ~20 мин на 3 кандидата, в ретро это убивает оба. «2 да из 3» → **строка в очередь** `$OBSIDIAN_VAULT/_outreach/share_fix_queue.jsonl` (JSON-строка: added·from·artifact·queries[дословные симптом-запросы!]·numbers·status:pending) — симптом-запросы и цифры пишутся СЕЙЧАС, пока контекст горячий, именно они теряются к утру. Раздаёт рутина `share-fix-daily` (дом = NODE-0X, каждую ночь 00:20 PDT с 15.10, ≤3 кандидата за прогон, полный ритуал `/share-fix`). Раздать прямо в ретро — только если целевой тред уже известен из сессии (тогда это 2 минуты, не 20). **Совет считается**: код отдавать не обязательно — опыт словами в чужом треде тоже польза. Что можно/нельзя наружу — чек-лист в том же регламенте.
**⭐ HN-кандидат (dev «+++» 10.09):** тот же проход задаёт ВТОРОЙ вопрос ровно один раз на артефакт — «это годится в Hacker News?». Годится ТОЛЬКО жанр «мы померили и показываем цифры» (post-mortem · замер · разбор поломки) и ТОЛЬКО как самостоятельная публичная страница с данными, не пост из ежедневного девлога. Да → строка в `$OBSIDIAN_VAULT/_outreach/hn_candidates.jsonl` (added·from·artifact·title·url·numbers·genre·status:ready|needs-page·blocked_by). Нет → молча, вердикт не нужен. ⛔ Потолок лейна: **своя ссылка на HN не чаще 1 раза в 2 недели** (ежедневный поток туда = профиль спамера, теневой бан накрывает аккаунт И домен); регулярное присутствие = комментарии в ЧУЖИХ тредах 1-3/нед. ⛔ Подача идёт ТОЛЬКО с хаба, ТОЛЬКО после «+» оператора (гейт Норы снят 06.08, ОК не ждём), ноль организованного голосования. Пока нет входа в HN на хабе — очередь копится, наружу не уходит ничего.

## Step 4📓 — Growth-log Макса (persona versioning; dev «+++» 2026-07-02)
If the session was MEANINGFUL for the cofounder line (built/decided/learned something real about the business or about working with dev — not a trivial lookup): **append ONE entry** to memory `cofounder-growth-log.md` — `дата · shell · урок про работу с оператором · один апгрейд себя`; записи о споре/сбое роли несут маркер `SPAR: с-уликой | без-улики | scope-нарушение | подмена-воли` — and **review recent entries**: что оставить в характере, что докрутить. **⚔️ Weekly SPAR count** (воскресный ретро или ≥7 дней с прошлого счёта): grep маркеров за неделю → строка «⚔️ SPAR: N споров (M с-уликой) · K scope/воля-нарушений»; цель = доля улик 100%, нарушения 0; считаем качество и нарушения, НЕ число споров (анти-театр). Канон: memory `objection-sparring-to-consensus` v3 (базлайн июля-2026: 23 спора:25 поддакиваний, scope 3, воля 2). Durable character changes fold DOWN into `cofounder-identity` (memory) and/or `~/.claude/skills/cofounder/references/system-prompt.md` — the log is the journal, those are the canon. Twin of [[persona-pulse-measurement]] (that logs friction/wins about ME helping HIM; this logs MY growth). Skip silently for trivial sessions.

## Step 4🎭 — БИТЫ ДНЯ В КАНОН (закон «канон раньше контента», 2026-07-10)
Ретро = главный системный «писатель битов» (контекст горячий, факты сверены). Для каждого сюжетно-значимого события сессии (веха/провал/поворот/решение/деньги/ответ внешнего мира — словарь `beat_kind` в `_SHOW-CANON.md`): создать бит в `$OBSIDIAN_VAULT/04-Projects\show-canon\beats\` по `_TEMPLATE-beat.md` (3 оси + beat_kind обязательны; `reveal` ставить честно — незакрытое = live_hold). Затем обновить затронутые арки/петли/сезон → `python $IMPORTS_ROOT/content-factory\canon_render.py` (линт + свежие публичные реестры; push — по своим правилам, не отсюда). Рядовая сессия без сюжетных событий → пропустить молча. Идёт ПЕРЕД Step 4🎬: сначала факт в канон, потом суждение о контенте (вердикт ссылается на созданные биты как опору).

## Step 4🎬 — Content-check (dev «все наши сессии = контент», 2026-07-02)
Judge at retro-time, while context is hot: **does THIS session deserve content?** Verdict = **human-post** (route → content-factory / `/episode` / `/intention`; draft-first; dev's authorial voice = best model) · **dev-log** (machine-readable «проблема → как чинили → поправка следующего дня» for robots/future model generations → `/episode` dev-log tier, GitHub EN) · **both** · **no** (skip silently). The nightly robots (facebook-diary-auto, content-factory, intention-lane) stay as the safety net — this step is the hot-context first pass, and dev can override any moment («это заслуживает поста»). Attribution + CTA per [[cofounder-identity]] («придумано Майкрофтом и Тони, Palo Alto AI Research Lab» / "Invented by Mycroft and Tony, Palo Alto AI Research Lab") and [[cofounder-cta-public-contact]].
**⭐ Мини-тизер обязателен (dev 01.09):** every retro with a substantive arc births ≥1 mini-teaser (200-250 chars, «грабли → правило» so the READER gets use, not a status report) → `python D:\Vault\_imports\content-factory\content_miner.py capture --title "<хук>" --note "<тизер>" --tier teaser`. Verdict «no teaser» is legal ONLY with a named reason (empty routine session). Canon: `reglament-retro-smotrit-naruzhu-tizer-i-skill-v-mir`.
⚠️ **Этот тизер и X-пост шага 4🐦 — РАЗНЫЕ вещи, не дубль.** Тизер = инженерная полоса «грабли → правило», уезжает В ВОРОНКУ контент-фабрики черновиком. X-пост = внешняя полоса «что построили → кому польза», публикуется В ТОТ ЖЕ ЗАХОД. Угол «грабли → правило» для X-поста ЗАПРЕЩЁН приказом 05.10 (см. 4🐦).

## Step 4🐦 — X-ПОСТ СЕССИИ, ОБЯЗАТЕЛЬНО И С ПУБЛИКАЦИЕЙ (⭐ dev 05.10.2026, голосом, рельса 001)
Дословно: «После каждой сессии/ретро нужно генерировать короткий Twitter/X-пост. Пост должен быть не про технические проблемы, а про то, что было сделано и какую пользу это даёт внешнему читателю… чтобы обычный бизнесовый человек, не погружённый в технические детали агентов, понял ценность и захотел прочитать… Пост нужно публиковать прямо в Twitter/X после проверки.»

**Кто читатель.** Бизнесовый человек, который знает, что агенты существуют, и НЕ знает, как они устроены. Он должен (а) понять, какую штуку мы сделали, (б) увидеть, для кого и зачем она полезна, (в) почувствовать, что сам станет сильнее, если разберётся. ⛔ Это НЕ «объясни бабушке» и НЕ упрощение до детского: просто, но не примитивно. ⛔ Это НЕ для внутреннего игрока: слова «волт», «рельса», «ретро», имена наших узлов и скиллов снаружи ничего не значат.

**Угол (поправка 06.10, свежее).** Честная история с эмоцией: что пробовали, что получилось ИЛИ не получилось. Провал и слабость законны («весь наш блог про боль»). Технический жаргон по-прежнему не идёт наружу. Ниже старый текст 05.10 действует только в части «не жаргон, а польза читателю». Было 05.10: от РЕЗУЛЬТАТА, не от аварии; первая строка говорит, что теперь ВОЗМОЖНО. ⚠️ Это прямо отменяет для X-полосы привычный нам угол «грабли → правило» и часть профиля `voice-x.md` про post-mortem как высокостатусный контент: приказ оператора 05.10 свежее (§8.5 «свежее бьёт старое», оба `origin: dev`). Остальной `voice-x.md` в силе целиком: BLUF в первой строке, ноль хэштегов, ссылка в первом реплае, peer-тон, ноль AI-слопа.

⛔⭐ **CTA НЕТ. МЫ НИЧЕГО НЕ ПРОДАЁМ** (dev 06.10, голосом; отменяет «CTA можно» от 05.10): ни флот-оффера, ни GitHub-призыва, ни «звезда+фолловнуть». Блог = боль, сложности, слабости, что получилось и что нет, плюс эмоция. Черновик пишет Grok (`llm_ask.py --rails grok`), судит Claude; детали `/x-post` §1 и память `blog-never-sells`.

**Процедура, четыре хода.** Ход 0 стоит ПЕРВЫМ не случайно: 06.10 сессия написала пост, прогнала оба гейта и только потом узнала, что публиковать нечем — это 20 минут работы в пустоту и ровно та «обратная сторона горлышка», которую §4.1 велит ставить в НАЧАЛО, а не в конец.

0. **Проверь рот ДО пера — ДВУМЯ пробами, не одной.** ⚠️ Правка 08.10.2026 (наступил сам, H27595): `list_connected_browsers` вернул живой `Browser 1` — и дверь всё равно оказалась закрыта. Сам `x.com` не грузится: форма отдаёт «Something went wrong» и «Some privacy related extensions may cause issues on x.com. Please disable them and try again.» Дважды, в двух разных вкладках, плюс один раз завис рендерер (`captureScreenshot` таймаут 30 с). То есть **живое расширение ≠ живая дверь**, и 61 из 68 парковок полосы просили у оператора НЕ ТО (включить расширение), когда узкое место уже сместилось на блокирующее приватное расширение в его Chrome. Проба теперь такая: (а) `list_connected_browsers` — пусто значит «расширение отключено»; (б) `navigate` на `https://x.com/compose/post` + `find` композера — страница в состоянии ошибки значит «расширение живо, но X блокирует». Проси у оператора ровно то, что показала ВТОРАЯ проба. Исходный текст правила: пустой массив означает «расширение отключено, публиковать нечем». Тогда порядок обратный: ОДНОЙ строкой скажи оператору «включи расширение Claude in Chrome, пост готовлю», и пиши пост дальше — он уйдёт, как только расширение появится. ⛔ Не трать два гейта, не зная, откроется ли дверь. ⚠️ Проверенные 06.10 и закрытые альтернативы, заново их не перебирай: встроенный браузер (в X не залогинен, логин в X запрещён из-за checkpoint-риска) · n8n (98 воркфлоу, X-постера нет) · Publora MCP (нужен OAuth, в неинтерактивной сессии невозможен) · Publora REST (`publora_smoke.py`: ключа нет, и вендор ПРЯМО запрещает агенту проходить шаги его получения). Пятая дверь, проверенная соседней сессией: **X API отдал 403 client-not-enrolled** -- аккаунт не заведён в их программу, это тоже руки. Единственная живая дверь = расширение Chrome.
   Дверь мертва, а пост готов → **не выбрасывай его**: `retro_x_post.py park --file <черновик> --reason "<живая улика отказа, не догадка>"`. Текст ляжет в журнал и будет ВИДЕН в `status` строкой «ждут отправки»; когда дверь откроется, закрой парковку: `record --url <твит> --closes <slug>`. Механизм добавлен соседней сессией 06.10.
1. Напиши пост сам на Opus/Fable (голос оператора, EN для @Tony_Stef_), ≤280 знаков. Факты берёшь ИЗ ЭТОЙ сессии; цифра без улики в сессии не пишется (§5.4).
2. Два гейта подряд, оба обязательны:
   ```
   python -B "$HOME/.claude/scripts/retro_x_post.py" lint --file "<черновик.txt>"
   python -B "D:\Vault\_imports\content-factory\slop_gate.py" --file "<черновик.md>" --tier teaser --channel x
   ```
   `retro_x_post.py` валит только ОДНОЗНАЧНО формальное: пусто · длина по взвешенному счёту X (ссылка 23, emoji и CJK по 2, NFC) · ссылка в теле, включая голый домен · длинные тире · хэштеги. Остальное печатает ПОДСКАЗКАМИ (возможный технический уклон, наш внутренний идентификатор, какие ноги CTA видны) — подсказка вердикт не меняет и объяснений не требует. `slop_gate.py` держит AI-слоп, один источник на флот. FAIL любого = переписать СЕЙЧАС, в этом же заходе, не «отложить».
   ⚠️ **Гейт НЕ судит смысл приказа, и это записано в его слепой зоне.** Ревью Codex 06.10 выдало первой версии BLOCK с восемью воспроизведёнными уликами: словарь слов валил разрешённые посты («находит ошибки до оплаты» → FAIL на «ошибк», «fixed-price quotes» → FAIL на «fixed», «тизер» в анонсе товара → FAIL как «внутренний жаргон») и пропускал технический отчёт про deadlock и mutex, потому что этих слов в списке не было. Расширение словарей проверкой пользы не становится.
2-бис. **Поэтому вердикт о смысле даёшь ТЫ, и он идёт в отчёт двумя строками** (их не заменяет PASS гейта):
   - `адресат: <кто именно получает пользу>` — роль человека, не «все». Не можешь назвать — пост не готов.
   - `польза: <что он сможет делать иначе>` — проверяемое следствие, не «станет эффективнее».
   - `продажа: нет` — ни оффера, ни призыва, ни просьбы звезды/фолловинга (dev 06.10). Нашёл хоть один — переписать СЕЙЧАС.
   Третья строка обязательна, если подсказка про технический уклон сработала: `уклон: по делу, потому что <…>` ЛИБО перепиши. Это и есть то место, где приказ оператора исполняется; гейт лишь не даёт испортить форму.
3. ⭐ **С 23.10.2026 пост кладётся НА СКЛАД, а не публикуется сессией** (dev, «LLM не бэкенд»): `python3 ~/.claude/scripts/x_outbox.py enqueue --file <черновик.txt> --session <номер>`; публикует робот на NODE-0X, URL твита вернётся квитанцией (`x_outbox.py status`). В отчёт ретро строка «🏭 на складе id=<id>». Абзац ниже = прежний путь, только как исключение вслух.
   Прежний путь: публикуй через **`/x-post`** (живой Chrome, @Tony_Stef_, `social_guard` ≤6/день). ⛔ IP-гейт §7.2: постинг в X с хаба `HUB-01` либо с ноутов оператора NODE-0X/NODE-0X (карв-аут dev 19.10.2026); на любом другом узле пост не публикуется, а уезжает текстом на хаб, и ретро говорит это строкой. Как именно уезжает (проверено 09.10.2026, NODE-0X): `python ~/.claude/scripts/bus_send.py "TASK: <что и текст поста>" < /dev/null` -- слово `TASK` с ДВОЕТОЧИЕМ сразу после, иначе `REFUSING TO SEND: near-miss robot-invisible body`, exit 2; плюс `retro_x_post.py park` у себя, чтобы пост был виден в `status`. ⚠️ Хаб на 09.10 держал 73 парковки и ОДНУ квитанцию за всю жизнь полосы (самая старая 3.6 дня), на ноуте 8 и 0: «уехал на хаб» -- это НЕ «опубликован», а текст ложится в ту же очередь. Называй оператору три числа (сколько ждёт, старейшая, главная причина), не одну строку про свой пост. Ссылка (GitHub/лонгрид) уходит ПЕРВЫМ РЕПЛАЕМ, не в тело.
4. Зафиксируй факт, иначе полоса непроверяема:
   ```
   python -B "$HOME/.claude/scripts/retro_x_post.py" record --url "<ссылка на твит>" --retro "<путь к заметке ретро>" --closes "<slug парковки, если пост стоял в очереди>"
   # ⭐ 22.10.2026: без --closes квитанция очередь НЕ закрывает. Замер: 5 публикаций
   # 19-20.10, closes лишь у одной -> 54 открытых парковки при живой публикации.
   # Прибор теперь сам закроет парковку по --session или когда открыта ровно одна,
   # а при нескольких ответит rc=3 со списком slug -- это долг, а не сбой.
   ```
   Жива ли полоса вообще: `retro_x_post.py status --days 14`.

⚠️ **ПОТОЛОК ДЛИНЫ НА ДЕЛЕ 250, А НЕ 280** (замер 06.10, наступил сам). Два гейта спорят, и скилл раньше не говорил, кто главный: `retro_x_post` разрешает 280 по взвешенному счёту X, а `slop_gate --tier teaser` рубит FAIL на 250 (его граница настроена под RU-каналы, медиана ~800). В окне 251–280 пост проходит первый гейт и валится вторым. Пиши под **250**, и не садись на саму границу: прибор сам пишет, что у лимита длина неточна в обе стороны (память «порог судим разбросом, не точкой»).
⚠️ **Два WARN `slop_gate` на этой полосе ОЖИДАЕМЫ и дефектом не являются** — назови их вслух и иди дальше: `W7-teaser-no-way-out` требует ссылку в тизере, тогда как `retro_x_post` ссылку в теле ВАЛИТ (разрешается первым реплаем, которого slop_gate не видит); `W4-first-person` ищет русские «я/мне/мой» в англоязычном посте для @Tony_Stef_ и потому срабатывает ложно. Блокирует только FAIL.

**⭐ ДВЕРЬ В X ПРОВЕРЯЕТСЯ ЖИВОЙ ПРОБОЙ, И ОНА БЫВАЕТ МЕРТВА ЦЕЛИКОМ** (замер 06.10). Полоса показывала «опубликовано 0 при 11 прогонах гейта», и я счёл это недостатком дисциплины. Причина оказалась транспортной: в тот день отказали ВСЕ ТРИ двери подряд, каждая живой пробой, а не догадкой — (1) `list_connected_browsers` вернул `[]` при пяти живых `chrome.exe` (расширение Claude-in-Chrome к сессии не подключено); (2) `python x_post.py check` → `403 client-not-enrolled`, приложение не привязано к Project в портале разработчика; (3) `python publora_smoke.py` → ключа нет, и Publora программно запрещает агенту его завести. Порядок пробы — этот же, он от дешёвого к дорогому. ⛔ «Опубликовано 0» само по себе НЕ улика против дисциплины: сначала проба двери, потом вердикт о причине (§5.4 «причина = такой же claim»).

**Пропуск законен в ЧЕТЫРЁХ случаях, и каждый называется вслух:** (1) сессия пустая, рассказывать снаружи нечего; (2) узел не хаб и не ноут оператора (NODE-0X/NODE-0X), пост уехал на хаб задачей; (3) `social_guard` вернул лимит 6/день; (4) ⭐ **все двери в X мертвы по живой пробе** — тогда пост НЕ выбрасывается, а парkуется, иначе он умирает в скратчпаде (класс «тихая потеря задач»):
   ```
   python -B "$HOME/.claude/scripts/retro_x_post.py" park --file "<черновик.txt>" --reason "<какая дверь и как отказала>" --session "<ключ>"
   ```
   Припаркованные `status` печатает ВСЕГДА, вне окна `--days`. Открылась дверь — отправляешь и закрываешь парковку ИМЕННО её ключом: `record --url <твит> --closes <slug>`. ⛔ Квитанция без `--closes` чужую парковку не закрывает, и это прибито тестом: именно так рельса 001 уже теряла задачи, когда квитанция закрывала чужую единицу.
   ⭐ **ПАРКУЕШЬ — НАЗОВИ оператору РАЗМЕР ОЧЕРЕДИ, а не только свой пост** (замер 07.10.2026, хаб): в `~/.claude/retro_x_lane.jsonl` лежало **62 парковки и НОЛЬ квитанций `record`** — полоса не отправила ещё ни одного поста за всю свою жизнь, старейшая парковка от 06.10 02:23, и **59 из 62 держит ОДНА причина** (расширение Claude-in-Chrome не подключено). Каждая сессия честно исполняла шаг, честно парковала свой пост и честно писала оператору одну строку про расширение — и ровно поэтому он видел 62 раза «мелкую просьбу» вместо одной накопленной. Поэтому вместе с парковкой печатай ТРИ числа: сколько парковок не закрыто, какая старейшая и сколько из них держит твоя причина. Строка «один клик открывает 62 поста» — это другой разговор, чем «включи расширение». Числа берутся из полосы, а не на глаз:
   `python - <<'PY'` → читаешь `retro_x_lane.jsonl`, считаешь `op=="park"` минус закрытые через `record.closes`, группируешь по причине. ⛔ Своё «я исполнил шаг» успехом полосы НЕ является: полоса меряется квитанциями `record`, и ноль квитанций при 62 парковках — это мёртвая труба, а не дисциплинированные сессии ([[pipe-born-with-a-mouth]]). Тело замера и перепроверка причины — память [[x-lane-62-parked-zero-sent]].
⛔ «Не придумал текст» пропуском не является. ⛔ Вердикт в отчёте обязателен: 🐦 опубликовал (ссылка) · 📮 ушло на хаб · ⚪ пропуск + причина.
Выход полосы: `~/.claude/retro_x_lane.jsonl`. Канон: Библия `reglament-posle-retro-rozhdaetsya-x-post-dlya-vneshnego-chitatelya`, CLAUDE.md §9.4, память `retro-births-an-x-post-for-outsiders`.

## 🛠 ВЕРДИКТ О СКИЛЛЕ, КОТОРЫМ ПОЛЬЗОВАЛИСЬ (dev 07.09, голосом — обязателен, молчание = нарушение)
Применил в этой работе скилл — вынеси вердикт об ЕГО обновлении. Одной строкой, с причиной в обе стороны:
`🔧 обновляю /X — <что споткнулось>` (чинить В ТОМ ЖЕ заходе) · `📝 обновлю не сейчас — <причина>, строка легла в <адрес>` · `✅ /X обновлять не надо — <почему именно: прошло без заминки / заминка разовая и внешняя / правка дороже боли>`.

⭐ **ВЕРДИКТОВ ДВА, НЕ ОДИН** (dev 13.09, голосом). Второй вердикт: **собственная инструкция того, кто сейчас работал** (рутина `scheduled-tasks/<имя>/SKILL.md`, сид, хук): «не стоит ли переписать мою инструкцию на будущее, чтобы она была качественнее?». Та же тройка `🔧 обновляю` · `📝 не сейчас` · `✅ не надо`, всегда с причиной. ⚠️ Замер 13.09: рутина `devto-publish-rhythm` починила СВОЙ файл и смолчала про скилл `/comments`, где висел ПРОТИВОПОЛОЖНЫЙ гейт, правило исполнилось наполовину, и спрашивать пришлось оператору. Канон живёт в СКИЛЛЕ, рутина держит только специфику прогона: разошлись, значит правду в скилл, а из рутины указатель. Канон: [[routine-judges-its-own-instruction-too]], CLAUDE.md §9.3-бис.
Пустое «не надо» вердиктом не является. ⛔ Не путать с `/skill-gap` (тот про скилл, которого НЕТ) и не право раздувать: АК-47 в силе — правка снимает ПЕРЕЖИТУЮ боль, не гипотетическую.
Канон: Библия `reglament-polzuemsya-skillom-srazu-sudim-nado-li-ego-obnovit` · CLAUDE.md §9.3-бис · [[skill-used-judge-if-it-needs-update]].

## Step 4★ — The «repeats → make a skill» reflex (milestone closeout)
This is the step dev asked for (2026-06-18): at a finished milestone, don't just *note* a repeating action — **offer to turn it into a skill**. It's the retro-time expression of the standing rule `evaluate-recurring-into-routine` (повторяющаяся задача → оцени «на рутину?»). Mirror of [[capture-rules-into-bible]] (that catches *rules*; this catches *tasks-to-automate*).

**Trigger (catch it, don't wait to be asked):** any action that **repeated ≥2–3×** this session/milestone, OR that we'll **clearly return to** later (a manual sequence I re-typed, a multi-step procedure, a recurring check).

**Procedure — 4 cheap moves:**
1. **RECALL first — don't duplicate.** Skim the available skills + memory `automation-inventory` for an existing skill/routine/hook that already covers it. If one exists, point dev to it instead of building a twin. **⛳ И тут же второй вопрос (dev hub:5090, 2026-08-04): скилл ЕСТЬ — не проапгрейдить ли его?** «Есть» ≠ «закрыто»: назови, чего ему не хватило ИМЕННО в этой сессии (шаг, который я делал руками поверх скилла / грабли, которых в нём нет / устаревшая строка) → правка в тот же заход, и это тоже строка в 🔁→🛠 (`built/proposed/declined`). Нечего добавить — скажи это словом, молчание = проверка не сработала. Дословный текст вопроса и формат ответа — единственный источник в `/skill-gap` §⛳ (там же — вход-конец рефлекса).
2. **⚠️ AK-47 guard — a skill is just a `SKILL.md`.** One markdown file with a procedure, NOT a server / DB / webhook / external service. (This is the exact trap the Codex milestone-retro report fell into — over-engineered for a SWE team; rejected 2026-06-18.) If the thing genuinely needs more than a markdown procedure, flag it **⚠️ УСЛОЖНЕНИЕ** and let dev decide.
3. **OFFER as ДО→ПОСЛЕ** (per `show-before-after`) — one compact block:
   > **ЧТО:** собрать `/<имя-скилла>` · **ДО:** как делаю руками сейчас (на реальном примере этой сессии) · **ПОСЛЕ:** одна команда `/<имя>` · **что сломается:** ничего (надстройка) · **делаем? да/нет**
4. **On dev's «+» → build it via `skill-creator`.** Pick the right home by SHAPE (per `operating-agreement` → «Where durable rules go»):
   - on-demand ritual I run when asked → **skill** (`skill-creator`).
   - «каждый раз автоматически когда X» → **hook** (skill `update-config`), not a skill.
   - time-based «каждый понедельник / каждое утро» → **scheduled task / routine** (skill `schedule`).
   - «рутина» ≠ обязательно 24/7-робот — часто правильное = простой полуавто + напоминание.
   - ⭐ **СПИСОЧНАЯ работа на N кусков (N велико) → КОНЕЧНАЯ рутина, «слон»** (dev 23.08, §4.5-бис).
     Признак: в сессии я перебирал однотипные элементы (видео / заметки / карточки / островá графа /
     ссылки), список не кончился, и он не кончится и в следующий раз; либо задача уже месяцами
     спотыкается об участие оператора, лимиты вендора или баны. Это НЕ задача и НЕ героическая сессия —
     это слон: `python ~/.claude/scripts/elephant.py new <slug> --title T --quota N --os-task <ЗадачаWindows>`,
     дальше рабочий скрипт на каждом прогоне делает `next` → работа → `mark` → `tick`.
     `tick` сам ловит конец (выключает OS-задачу + доклад в TG-03) и затык (5 пустых прогонов → `blocked`).
     ⛔ Журнал слона НИКОГДА не кладём в синкаемую папку — затрётся, и слон не кончится никогда.
     Живой пример: [[yt-watch-history-drip]]. Канон: [[finite-routines-eat-the-elephant]].
   Then route/link it normally (Step 4) and mention it in the final report (post-hoc, not for permission).
5. **⭐ Скилл уходит в мир (dev 01.09, канон `reglament-retro-smotrit-naruzhu-tizer-i-skill-v-mir`):** любой собранный/существенно обновлённый скилл в том же заходе получает (а) тизер-пост в наши соцсети (через content-factory / каскад) и (б) публикацию самого скилла на нашем публичном GitHub (дефолт `tonydzi/clawrush` `artifacts/`) ПОСЛЕ leak-scan, с пометкой в шапке «built for dev's fleet — adapt paths/names to your setup». Заточен под оператора / сырой / «на тормозке» — публикуем всё равно, честно пометив. Скип — только с названной причиной (leak-scan red / чистая кухня CRM).

## Step 4🔥 — КАТАКЛИЗМЫ СОСЕДЕЙ (dev 01.10.2026, голосом: «сирены в 03 я не читаю, ретро читаю хорошо»)
Ретро — его единственная читаемая лента тревог. Перед Output собери пожары ВНЕ этой сессии
(детерминированно, ~0 токенов):
1. Источники: (а) `Breakage-Journal.md` / `selfheal.py` — строки за последние 3 дня не из этой
   сессии; (б) RED/stale state-файлы известных сторожей (`~/.claude/_screenpipe_watch/state.json`
   и родня: verdict=RED или ts старше 2× такта); (в) `ALERT`/`SOS`/`RED` в шине 03 и
   `_machine-bus/inbox-*` за 48ч; (г) `/arch broken`, если ночная карта свежая.
2. Отбери **топ-3-5 самых сильных** (деньги · потерянные данные · мёртвая рельса записи ·
   недоставленное исходящее · сломанный узел флота). Мелочь и уже починенное — не включать:
   засорённый блок = непрочитанный блок.
3. В Output добавь блок **«🔥 Катаклизмы»** — каждый ОДНОЙ строкой и языком ELI5 (🧒-стиль:
   бытовые слова, что сломалось → что теряем → куда бежать), ⛔ без жаргона и внутренних
   кодовых имён без расшифровки. Пример: «🔥 Голосовые с 12:11 не заливаются в чат — твои
   надиктовки копятся на диске и не доходят до роботов. Дверь: /voice-memos».
4. Пожаров нет → одна строка «🔥 катаклизмов не вижу (проверил журнал+сторожа+шину)» —
   молчание без проверки запрещено (§5.4 пусто из одного места ≠ нет).

## Step 5 — Output (tight + scannable; a review artifact, not a novel)
1. **🎬 «Сегодня мы поняли»** — the arc (Step 2).
2. **🎙 Вердикт Майка** — 💰/🔪/🤺/❓ four-liner (Step 2🎙).
3. **♻️ Reuse table** — artifact · 🟢/🟡/⬆️ · **tested? ✅/❌** · why · routed-to.
3. **🔁→🛠 Repeats → skills** — any action that repeated this milestone, offered as ДО→ПОСЛЕ (Step 4★); mark each built / proposed / declined.
4. **🔗 Connect** — «✅N используется · 🔗M передано-ждёт · ⚠️K в воздух» (Step 3🔗); каждый ⚠️ подсвечен явно + решение (подключить потребителя / выбросить).
4б. **🔄 Outcome** — «N проверено · M живут · K мертвы + решения» (Step 3🔄).
5. **⛳ Drift map** — «цель <X> · унесло в N тем → 🧷M чипов создано · ♻️K по ходу · 📋J в журнал» (Step 3⛳); chips are already created by now, listed post-hoc.
6. **📌 Open items** — anything flagged for dev's decision; each one REGISTERED in the task journal (Step 3📋), shown as «#id · задача · линк».
7. **🗺 Roadmap** — the one-line delta from Step 3🗺 («✅N продвинуто · ➕M добавлено · ⏸ без движения»).
7. **🗜 Compact handoff** — the saved-note path + the FULL enriched `/compact` block printed inline (Step 6b; указатель на файл запрещён).
7б. **🔥 Катаклизмы** — топ-3-5 чужих пожаров ELI5-строками, или «катаклизмов не вижу (проверил…)» (Step 4🔥).
7в. **🐦 X-пост** — опубликованный текст целиком + ссылка на твит, ЛИБО «📮 ушло на хаб», ЛИБО «⚪ пропуск: <причина из трёх законных>» (Step 4🐦), плюс ОБЯЗАТЕЛЬНЫЕ строки `адресат:` и `польза:` из шага 2-бис. Текст поста печатается в отчёт, указатель на файл вместо текста запрещён.
8. **🧒 Простыми словами** recap.

## Step 6 — Compact handoff (retro ⇄ compact glue; STAY in the chat, never /clear)
The retro's distilled output IS the bridge file — so close the loop without losing context. Two moves:

**6a. Auto-save the retro to the vault IN COMPACT FORMAT** (standing authorization from dev, 2026-06-12 — no per-run ask):
Reserve the final Latin filename first, acquire exact leases for that note and `01-Conversations/Claude/_Claude-Sessions-MOC.md`, and add the MOC wikilink **before the note's first write**. The no-orphan guard rejects a new note that has no incoming link; if the MOC lease is busy, wait for its owner instead of creating an orphan or overriding the lease. Then write the clean note to `$OBSIDIAN_VAULT/01-Conversations/Claude/Retros/retro-<YYYY-MM-DD>-<latin-topic-slug>.md` — filename **ALWAYS Latin** per [[vault-conventions]] (Cyrillic topic → translit slug; keep the Russian title in frontmatter `aliases:`).
- Content = frontmatter (`title`, `date`, `type: retro`, `source: claude-session`, `session_id: <cliSessionId — тот же uuid, что в 6a-бис из пути скретчпада>`, `tags`) + the arc (Step 2) + the reuse table (Step 3/4) + **the compact 7-header distillation** (РЕШЕНИЯ / TODO / СЕЙЧАС / ПУТИ И ЗНАЧЕНИЯ / СЧЁТЧИКИ / ОТКРЫТО / ИНСТРУМЕНТЫ И КОНТРАКТЫ — per `$USERPROFILE/.claude/compact-prompt.md`). **This note IS the archive** — it doubles as the compact summary, so retro and compact are never written twice.
- **NO 🧒 block in the note** — vault notes keep their own voice (the ELI5 recap is for the reply TO dev only).
- **Wikilinks: vault ≠ memory (two namespaces).** In the retro NOTE, `[[...]]` may target ONLY existing vault notes (`reglament-*`, `protocol-*`, `concept-*`, `decision-*`, another retro — verify each exists before writing); CC-memory slugs (`machine-migration`, `ak47-simplicity`…) go as plain inline code. Caught 2026-07-04 (Fable re-check): a retro shipped 7/7 broken links — all memory slugs. Canon: `deterministic-script-gotchas` → «Vault wikilinks ≠ CC-memory slugs».
- **Formal review status is a scoped receipt, not prose.** Every independent-review claim in the note MUST be one exact line: `REVIEW[<artifact-id>]: verdict=<VERIFY|ACCEPT|BLOCK|REQUEST_CHANGES>; scope=<what exact bytes/state the verdict covers>; source=<thread:<uuid>|file:<absolute-path>>; reviewer=<name>`. A partial GREEN/RED run never upgrades the formal verdict; a rollback-only VERIFY stays rollback-only and cannot verify the proposal.
  ⚠️ Три грабли формата, каждая стоила прогона линта (замер 26.09.2026): (1) `scope` — максимум **200 символов**, два sha256 туда уже не влезают, оставляй один и слово «только»; (2) **точка с запятой внутри `scope` рвёт разбор** (поле читается как `[^;]+`) — внутри только запятые; (3) `source=file:<path>` обязан лежать в корнях, которые линт обходит (`~/.claude`, волт, `_imports`, папка дока, cwd) — вывод из `Temp\claude\…\tasks\` не засчитывается, копируй улику к остальным квитанциям. Плюс проза: слова «независимый ревьюер» рядом с «accept/pass/verify» в обычном абзаце тоже требуют receipt, поэтому в тексте пиши «Codex смотрит дифф», а вердикты держи только в receipt-строках. (4) **путь в `source=file:` пиши через ПРЯМЫЕ слэши** (`D:/Vault/...`): обратный слэш съедается любым генератором строки (в Python `\R`/`\0` стали управляющими символами и линт дважды отбил receipt с «битым» путём — замер 27.09.2026).
- **Door before archive/mark-done:** immediately after drafting the note, run `python -B "$HOME/.claude/scripts/status_claim_lint.py" "<absolute-retro-note>"`. `rc=0` is required before MOC/log/`mark-done`; `rc=2` means correct the claims and rerun. Do not archive or claim verification while this door is red.
- ⚠️ **Хук `orphan_check_hook` отобьёт запись: новое ретро рождается сиротой.** Дом входящей ссылки один и он известен: `01-Conversations/Claude/_Claude-Sessions-MOC.md`, секция «Свежие ретро» (плюс на ретро ссылаются `DayLedgers/day-ledger-*.md` и `00-System/Breakage-Journal.md`). Впиши строку `- [[retro-...]] · <в чём суть>` ТУДА первой записью батча, до создания note; после появления note проверь, что ссылка ровно одна.
  ⚠️ Грабля замера 14.09.2026: искать дом грепом по всему волту НЕ надо, `grep -rl` по `D:\Vault\Vault-Knowledge` уходит в таймаут 120с. На таймауте я объявил «ретро не линкует никто» и вписал этот вывод сюда как факт; фоновый прогон досчитался и вывод ОПРОВЕРГ. Ровно [[prichina-kak-claim]]: незавершённый поиск даёт «я не нашёл», а не «этого нет».
  Вторая ссылка из содержательного дома (реглумент/концепт/решение, к которому ретро относится) полезна и закрывает заодно Step 4, но обязательной является ссылка из MOC.
- **New-file append only** — never overwrite an existing retro. It's a scoped folder (sits next to the `claude-chats-to-vault` notes), not a live concept/person note, so this is a safe write.
- Nightly Brain Reindex does NOT make this note `/ask`-searchable. `01-Conversations` is evidence, and `brain_embed_update.py` skips it. Copy the recallable facts into an essence note (`02-Decisions` or `10-Tasks`) in the same retro. The chat catalog indexes the retro file only on its own rebuild, not on the 15-minute brain tick. Proof 2026-09-25: a phrase that lives only in the retro = 0 chunks, the same facts in the decision memo = 1 chunk in `_brain_lex_e5.db`.

**6a-бис. Взять и снять сессию с очереди `/retro-lost` — ОБЯЗАТЕЛЬНО, сразу после 6a** (добавлено 2026-08-19; 4-й датированный случай класса «ночная догонялка судит сессию, у которой ретро ЕСТЬ»: партия 01 — 1 случай, партия 02 — 2, партия 03 — 8 из 10).
Сканер `retro_lost_scan.py` знает ровно один признак «закрыто» — маркер в `~/.claude/logs/retro_lost_done/`; волт он не читает и про заметку в `Retros/` не догадается. Без этой строки своя же ночная рутина через 5 суток снова читает транскрипт, снова тратит Opus и снова пишет «ретро уже есть».
- **sessionId брать из пути скретчпада** этой сессии (`…\Temp\claude\<project>\<sessionId>\scratchpad` — имя папки перед `scratchpad`), он есть в системном промпте; гадать по имени файла не нужно.
- ⛔ **НЕ брать id из `get_session self` — это ДРУГОЕ пространство имён, и `take` его отбивает** (замер 07.10.2026, хаб, сессия 737a8bed): `get_session self` отдаёт CCD-шный `local_d2c0b238-…`, и `take local_…` ответил `{"ok": false, "reason": "invalid-session-id"}`, а тот же вызов с CLI-sid `737a8bed-…` сразу выдал epoch. Та же развилка уже описана в Шаге 3🚂 («у сессии ДВА идентификатора»), но ТАМ она про `rail_plan.py`, и шаг 6a-бис её не наследует — поэтому строка стоит здесь отдельно. Соседний шаг 6a-тер работает РОВНО НАОБОРОТ: `set_session_title` понимает только `"self"`/CCD-id. Правило простое: всё, что читает транскрипт (`retro_lost_scan`, `rail_plan`, `session_continues`, `qqq_auto`), хочет CLI-sid; всё, что рисует окно приложения, хочет CCD-id. ⛔ `invalid-session-id` читать как «сессии нет» нельзя — это промах по ключу, а не отсутствие.
- До работы выбери абсолютный путь `<absolute-receipt.json>` вне репозитория и захвати сессию: `python -B "$HOME/.claude/scripts/retro_lost_scan.py" take <sessionId> --holder "<taskId>" --json --receipt-out "<absolute-receipt.json>"`.
- ⚠️ **`--receipt-out` на Windows пиши путём `C:/...`, а НЕ `/c/...` из Git Bash** (замер 12.10.2026, NODE-0X): Windows-Python понимает `/c/Users/...` как `C:\c\Users\...`, квитанция ложится не туда, и `mark-done` получает пустой `--epoch`. Спасло только то, что `take` печатает JSON в stdout: значения бери ОТТУДА дословно.
- `rc=0` доверяй только когда durable receipt exists и JSON содержит непустые `question_id`, `session_id`, `logical_file_id`, `holder` и `epoch` как positive integer. Receipt сохрани до подтверждённого DONE: он нужен для replay после crash. При отсутствующем/битом receipt остановись; DONE не ставь.
- После записи ретро передай значения **дословно из receipt**: `python -B "$HOME/.claude/scripts/retro_lost_scan.py" mark-done "<receipt.session_id>" --question-id "<receipt.question_id>" --logical-file-id "<receipt.logical_file_id>" --holder "<receipt.holder>" --epoch "<receipt.epoch>" --note "<retro-note>"`. Do not recompute identity по пути или sessionId. Wrong/missing identity обязана завершиться fail-closed без DONE/release; точный replay идемпотентен.
  ⚠️ `"$HOME/..."` буквально работает и в Windows PowerShell 5.1, и в Git Bash. `~` после `python` в PowerShell 5.1 остаётся буквальным путём, а `%USERPROFILE%` раскрывает только CMD.
- Не смог достоверно определить sessionId — так и скажи строкой в отчёте, НЕ помечай наугад чужую сессию.
- ⚠️ **`take` ответил `session-not-found` при ВЕРНОМ sessionId — это норма, а не сбой** (замер 06.10.2026, ретро живой сессии 97c50ca4). Сканер `retro_lost_scan.py` держит в очереди только БРОШЕННЫЕ сессии (молчат дольше суток); сессия, в которой ретро идёт прямо сейчас, в очередь ещё не попала, и помечать нечего. Правильное поведение: ОДНА строка в отчёт «в очереди retro-lost сессии нет, помечать нечего», `mark-done` НЕ зовём и `--force` не ищем. ⛔ Не читать это как «дверь сломана»: ночная догонялка возьмёт сессию, только если она затихнет, а к тому моменту заметка ретро уже лежит в волте и робот сам увидит её по `session_id` во frontmatter.
- ⚠️ **А вот `take` с `rc=0` -- ОБРАТНЫЙ случай, и он ОБЯЗЫВАЕТ закрыть квитанцию** (замер 06.10.2026, сессия CRM+мессенджеров: разрыв 62ч24м, сессия затихла на двое суток и в очередь попасть УСПЕЛА, `take` отдал `epoch 223` и живую квитанцию). Абзац выше описывает только ПУСТУЮ очередь, и сессия, впервые увидевшая `rc=0`, порядок выводит сама -- отсюда риск бросить захват незакрытым: держатель висит, а ночная догонялка через 5 суток снова читает транскрипт и снова тратит Opus. Порядок при `rc=0`: дочитать `question_id`, `logical_file_id`, `holder`, `epoch` из квитанции ДОСЛОВНО -> записать заметку ретро -> `mark-done` ровно этими значениями -> убедиться, что в ответе есть строка `done: <...>/logs/retro_lost_done/<sessionId>`. ⛔ Значения не пересчитывать по пути и не брать «на глаз»: неверная личность обязана падать fail-closed, и тогда DONE не ставится вовсе. ⛔ Пути в правках этого файла пиши ПРЯМЫМИ слэшами: обратный слэш перед l/r/t/0 становится управляющим символом и МОЛЧА обрезает строку (семья escape-avariya-v-patche, наступил сам 06.10 ровно в этом абзаце).

**6a-тер. Маркер каждого отдельного завершённого ретро (уточнение оператора 16.10.2026).**

Каждое НОВОЕ завершённое ретро добавляет одну русскую `Р` непосредственно перед
человеческим описанием. Два отдельных ретро = `Р Р`, три = `Р Р Р`.
Форма: `⚙️ · 🏷️🔧 Р Р Переименовать сессии по скиллу · H79507`.
В старом служебном слоте после иконки группы латинские P/R учитываются как прежние маркеры. Свободный человеческий текст вроде R vs Python не переписывается. Новые маркеры только русская Р.
Это отменяет прежний запрет второго маркера в этой инструкции.

Одна дверь: `python -X utf8 ~/.claude/scripts/session_titles.py retro --sid <UUID> --event <путь-новой-заметки-ретро>`.
`--event` = стабильная личность ЭТОГО завершённого ретро: путь к новой заметке либо ID
исходного запроса. Повторная доставка того же события использует тот же event и НЕ
добавляет новую Р. Следующее отдельное ретро получает новый event. Новый timestamp
на каждом техническом retry запрещён. Маркер добавляется после записи дистиллята.
Codex команда сама пишет полное имя через metadata RPC, сверяет его и обновляет реестр.
Claude: `session_titles.py retro-plan --sid <CLI-sid> --event <тот-же-stable-event> --text <текущее-имя> --code <код>`
учитывает маркеры в том же журнале. Применить выданный title доступным set_session_title,
перечитать и синхронизировать реестр через session_code.py title. Ни номер перед текстом,
ни сокращение имени не допускаются.
Перед записью читать текущее имя вплотную. Чужая правка = conflict и один выход, без цикла.
Сбой транспорта = один видимый error/pending; не запускать новую сессию или модель.

**6a-кватер. Проверь ИКОНКУ группы в заголовке — сразу после маркера Р** (⭐ dev 07.09.2026 «кладёшь её в нужную группу»; ⭐ dev 10.09.2026, голосом: «мало пикселей на экране, нужна иконка», и «переименовывать НА СТАРТЕ»).
- Иконка ставится НЕ здесь, а на СТАРТЕ сессии (скилл `/session-groups`). Ретро только ПЕРЕПРОВЕРЯЕТ: тема сессии за день могла уехать в другую группу.
- `get_session self` уже вызван в 6a-тер. Заголовок начинается с иконки из алфавита? 💰 $$$ (деньги/оффер/витрины/статьи наружу) · 🧠 2мозг (волт/RAG/память/клон) · ✍️ content (посты/соцсети/Майкрофт) · 🎯 Лиды-CRM · ⚙️ Инфра (скрипты/флот/синк/канон/браузеры) · 🔬 ДРы · 🏠 личное · 📥 SINK (инбокс/шина/посылки) · ❓ не понял.
- Иконки нет ЛИБО она уже не про эту сессию → `set_session_title self` через общий session_titles.py в форму `<группа> · <два значка темы> <Р за каждое ретро> <имя> · <номер>`. Веха ретро `Р ` живёт ПОСЛЕ иконки (legacy `Р+` в старых именах не переписываем). Гадать запрещено: тема не читается — ставь ❓, оператор разнесёт сам.
- Строка в отчёт: «иконка: <какая>, флаг ccd_sidebar OFF». Молчать нельзя.
- ⛔ ГРУППЫ САЙДБАРА ВЫКЛЮЧЕНЫ (dev 02.10, голосом: «класть сессию в какую-то группу не надо… не имеет смысла»): `ccd_sidebar.move_sessions` НЕ вызываем, сессию в группу не кладём. Остаётся только ИКОНКА в заголовке.
- ⛔ Правка `claude_desktop_config.json` руками НЕ рельса: приложение файл живьём не перечитывает и перепишет из памяти (замер 07.09).
- Канон: память `session-group-at-retro`; движок и алфавит — скилл `/session-groups`; публичная копия github.com/tonydzi/claude-session-icons.

**6b. PRINT the READY enriched paste-line INLINE — обязательный выход КАЖДОГО ретро (⭐ dev 26.08, голосом: «каждый раз давай готовый текст компакта; иди-в-файлик — неудобно»).**
- ⚠️ Fact base (2026-07-22): bare `/compact` does NOT read our format — 354/354 past compacts fell back to the DEFAULT English template; PreCompact hooks cannot inject (issue #14160). The 7-header format applies ONLY pasted inline: `/compact <text>`.
- **Procedure = same enrichment as `/cc` Steps 2-3** (single source of mechanics — don't duplicate, read `~/.claude/skills/cc/SKILL.md`): take the skeleton from `$USERPROFILE/.claude/compact-prompt.md` § «Готовая строка», FILL all 7 headers with THIS session's real facts — reuse the distillation already written into the 6a vault note, don't re-derive — and PRINT one fenced ```code``` block starting with `/compact `, со строкой над ним: «➤ Скопируй блок целиком и вставь следующим сообщением». Then the fork:
> **«Готово, всё в волте. Остаёшься в сессии — вставь блок ниже целиком (без него сжатие пойдёт по дефолтному английскому шаблону). Новый чат — просто уходи, всё уже заархивировано.»**
- ⛔ **Указатель вместо блока ЗАПРЕЩЁН.** «Вставь блок из `~/.claude/compact-prompt.md`» / «возьми текст в файле» = нарушение правила (ровно эта формулировка — жалоба оператора 26.08). Пустой скелет с `<...>` — тоже нарушение: блок обязан быть обогащён сессией. Канон: память `compact-dev-prefers-zero-touch` §Поправка 26.08 + `compact-format-delivery-gotcha`.
- **retro = «не уверен, пора ли»** (archives so both doors stay open, risk-free); **compact = «точно остаюсь»** → paste the block.
- I (the agent) **cannot press `/compact` myself** — it's a harness command. The archive is automatic; printing the ready line is my half, the paste is dev's.

## 🌳 Дерево решений маркера ретро

```mermaid
flowchart TD
 START[Ретро] --> A{Дистиллят записан?}
 A -->|Нет| SAVE[Сначала сохранить факты и ограничения]
 A -->|Да| B{Этот event уже учтён?}
 B -->|Да| SAME[Прежнее число Р, повтор без увеличения]
 B -->|Нет| C{Имя не изменилось параллельно?}
 C -->|Да| ADD[Одна новая Р перед описанием и readback]
 C -->|Нет| STOP{{⛔ СТОП: conflict, без цикла}}
```

## Scope / don't-duplicate
- Internal build-retro only. NOT the public Facebook diary (`facebook-diary-daily`) and NOT the preference scanner (`preference-sweep-daily`).
- If a session built nothing durable, say so plainly — skip the ceremony (but still offer the `/compact` block if the chat got long).

## ⭐ Полнота списка потребителей (dev 10.09.2026)

Первый найденный потребитель почти никогда не единственный — он просто лежал на поверхности. Поиск закончен не когда кто-то найден, а когда **две оси подряд дали ноль новых имён**; внутренний потребитель (узел флота, робот, наш же скилл с костылём) ищется ПЕРВЫМ. Девять осей перебора и обязательный вердикт с числом («осей N/9 · адресов M · насыщение да/нет») — `/consumer-hunt` §Шаг 1-бис. ⚠️ Исчерпывающим обязан быть ПОИСК, адресация идёт по правилам двери: найденный адрес не выбрасывается, а получает статус и дату (🟢 постучались · ⏸ глухая очередь по замеру · 🪦 непереносимо). Канон: `reglament-vypustil-funkcional-naydi-potrebiteley-i-pridi-k-nim` §Поправка 10.09 + [[consumers-are-a-set-not-the-first-one]].

---

**Claude:**

🕐 24.10.2026, 06:5x. Ретро сессии H79620. Сначала приборы, потом суждения.

---

> `ToolSearch` -- {"query": "select:mcp__ccd_session_mgmt__get_session", "max_results": 2}

---

> `Bash` -- {"command": "python -c \"import datetime; print('СЕЙЧАС', datetime.datetime.now().isoformat(timespec='seconds'))\"; echo \"=== CLI-sid из пути скретчпада ===\"; echo \"s_a5230cc4\"; echo \"=== turnstate ===\"; timeout 120 python -X utf8 \"D:/Vault/_imports/turnstate/turn

---

> `mcp__ccd_session_mgmt__get_session` -- {"session_id": "self"}

---

> `Bash` -- {"command": "cd \"C:/Users/dev/.claude/scripts\" && echo \"=== CLI-sid по мнению прибора ===\"; python -c \"import sys,os; sys.path.insert(0,os.path.expanduser('~/.claude/scripts')); import rail_plan; print(repr(rail_plan._env_sid()))\"; echo \"=== вердикт рельс ===\"; timeout 150 python -X utf8 r

---

**Claude:**

Разрыв сессии: создана 27.09 07:30, последняя активность 24.10 05:26 = **26 дней 21 час 56 минут**. Сверка рельс закрылась зелёной на узловых числах, но моя сессия чужих вызовов не делала, поэтому закрываю недобор причинами честно.

---

> `Bash` -- {"command": "cd \"C:/Users/dev/.claude/scripts\" && timeout 150 python -X utf8 rail_plan.py verdict --session s_a5230cc4 --reason \"code_read=too-small:читал прицельными кусками по 20-40 строк через sed, файлов целиком >500 строк не открывал\" --reason \"second_opinion=no

---

> `Bash` -- {"command": "cd \"C:/Users/dev/.claude/scripts\" && echo \"=== retro-lost take ===\"; timeout 120 python -X utf8 retro_lost_scan.py take s_a5230cc4 --holder \"retro-h79620\" --json --receipt-out \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/41a23

---

**Claude:**

Прибор говорит `already-done`: ночная догонялка уже разбирала эту сессию, пока она молчала 26 дней. Значит моё ретро обязано быть ДЕЛЬТОЙ поверх её заметки, а не вторым полным разбором. Ищу её.

---

> `Bash` -- {"command": "ls -la ~/.claude/logs/retro_lost_done/ 2>/dev/null | grep -i \"41a23c08\" | head -3; echo \"=== заметка робота в волте ===\"; grep -rl \"s_a5230cc4\" \"D:/Vault/Vault-Knowledge/01-Conversations/Claude/Retros/\" 2>/dev/null | head -5", "description": "Find ro

---

> `Bash` -- {"command": "cat ~/.claude/logs/retro_lost_done/s_a5230cc4 2>&1", "description": "Read the done marker content"}

---

> `Bash` -- {"command": "set -o pipefail; grep -n -A 12 \"41a23c08\\|Трудоустройство в ИИ-лаборатории\" \"D:/Vault/Vault-Knowledge/01-Conversations/Claude/Retros/retro-lost-2026-10-19-hub-desyatka-40-sessiy.md\" 2>&1 | head -30", "description": "Read robot retro section about this session"}

---

> `Bash` -- {"command": "ls -la \"D:/Vault/Vault-Knowledge/01-Conversations/Claude/Retros/retro-lost-2026-10-19-hub-desyatka-40-sessiy.md\" 2>&1; head -40 \"D:/Vault/Vault-Knowledge/01-Conversations/Claude/Retros/retro-lost-2026-10-19-hub-desyatka-40-sessiy.md\" 2>&1 | tail -28", "description": "Inspect r

---

**Claude:**

Важнее: в заметке робота от 19.10 моей сессии **нет вообще** (ни id, ни темы, grep пуст), а маркер «разобрано» стоит. Значит содержание 27.09 никто не дистиллировал, и это первое настоящее ретро сессии. Завожу поломки через прибор семей.

---

> `Bash` -- {"command": "cd \"C:/Users/dev/.claude/scripts\" && for d in \"маркер ночного ретро закрыл сессию заметкой, которая эту сессию не упоминает\" \"правило записано в канон с объявленной дверью, которой в коде нет\" \"замер до-после сравнил себя с собой: автоснапшот уже закоммитил мою правку в HEAD~1\

---

**Claude:**

Прибор даёт ноль семейных по всем трём, но это «не нашёл», а не «семьи нет». Смотрю список семей, чтобы не выдумать новое имя для уже известного класса.

---

> `Bash` -- {"command": "cd \"C:/Users/dev/.claude/scripts\" && grep -n \"FAMILIES\" prior_art.py | head -3; python -c \"\nimport sys,os; sys.path.insert(0,os.path.expanduser('~/.claude/scripts'))\nimport prior_art as P\nF=getattr(P,'FAMILIES',{})\nprint('семей всего:',len(F))\nimport re\nfor k in F:\n    if 

---

> `Bash` -- {"command": "set -o pipefail; grep -ocE \"pravilo-prinyato-dveri-net|instrument-vrjot-zelyonym|izmerenie-do-sravnilo-sebya\" \"D:/Vault/Vault-Knowledge/00-System/Breakage-Journal.md\" 2>/dev/null; echo \"--- точный счёт по классам ---\"; for c in pravilo-prinyato-dveri-net instrument-vrjot-zelyon

---

> `Bash` -- {"command": "cd \"C:/Users/dev/.claude/scripts\" && for c in pravilo-prinyato-dveri-net instrument-vrjot-zelyonym pribor-ne-nazval-slepuyu-zonu; do printf \"%-34s \" \"$c\"; timeout 120 python -X utf8 breakage.py count --class $c 2>&1 | tail -1; done", "description": "Count classes through the pro

---

> `Bash` -- {"command": "cd \"C:/Users/dev/.claude/scripts\" && timeout 150 python -X utf8 selfheal.py journal --class pravilo-prinyato-dveri-net --what \"Библия 27.09 утверждала, что модуль ручной полосы lab_hand.py дёргается каждым ночным прогоном pipe-a-discover; вызова в коде не было вовсе, модуль числилс

---

> `Bash` -- {"command": "cd \"C:/Users/dev/.claude/scripts\" && timeout 150 python -X utf8 selfheal.py journal --class instrument-vrjot-zelyonym --what \"Маркер ночного retro-lost закрыл сессию 41a23c08 заметкой retro-lost-2026-10-19-hub-desyatka-40-sessiy.md, в которой этой сессии нет ни по id, ни по теме (g

---

> `Bash` -- {"command": "cd \"C:/Users/dev/.claude/scripts\" && timeout 150 python -X utf8 selfheal.py journal --amend --class instrument-vrjot-zelyonym --what \"Маркер ночного retro-lost закрыл сессию 41a23c08 заметкой от 19.10, в которой этой сессии нет ни по id, ни по теме (grep пуст): 'разобрано' при нуле

---

**Claude:**

Поломки заведены: ложная дверь 2/3, слепой сторож 3/3 (карточка ремонта уже есть у флота), врущий зелёным прибор 30/3. Теперь панель шести ломателей — кормлю её черновиком ретро.

---

> `Write` -- {"file_path": "C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_a5230cc4\\scratchpad\\panel_context_h79620.md", "content": "# Draft retro of session H79620 (hub HUB-01, 2026-09-27 -> 2026-10-24)\n\nFind where my conclusions are wrong, w

---

> `Bash` -- {"command": "cd \"C:/Users/dev/.claude/scripts/cc-review\" && timeout 100 python -X utf8 orouter_review.py panel --help 2>&1 | head -25", "description": "Read panel CLI before running"}

---

> `Bash` -- {"command": "cd \"C:/Users/dev/.claude/scripts/cc-review\" && timeout 600 python -X utf8 orouter_review.py panel --preset retro --role break --effort medium --task retro-h79620 --context-file \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/41a23c08-1841-433f-9de5-da0144d595

---

**Claude:**

Панель пошла в фоне. Пока она думает, делаю остальные приборы ретро.

---

> `mcp__ccd_connectors__session_connectors_status` -- {}

---

> `Bash` -- {"command": "cd \"C:/Users/dev/.claude/scripts\" && echo \"=== задача по классу instrument-vrjot-zelyonym есть? ===\"; ls \"D:/Vault/Vault-Knowledge/10-Tasks/\" 2>/dev/null | grep -i \"instrument-vrjot\\|zelyonym\" | head -3; echo \"(пусто = карточки нет)\"; echo \"=== outcome-аудит правил: ноч

---

> `Bash` -- {"command": "cd \"C:/Users/dev/.claude/scripts\" && timeout 150 python -X utf8 skill_load_audit.py 2>&1 | tail -18", "description": "Run skill load audit"}

---

**Claude:**

🧺 Загрузка: лишнее 14 объектов ≈1166 токенов, из них 11 неиспользуемых `local-*` скиллов — это класс целиком, по §0.7 выключать сам не буду, спрошу строкой ниже. Теперь заметка ретро, сначала ссылка в MOC, чтобы не родить сироту.

---

> `Bash` -- {"command": "set -o pipefail; grep -n \"Свежие ретро\" -A 6 \"D:/Vault/Vault-Knowledge/01-Conversations/Claude/_Claude-Sessions-MOC.md\" 2>&1 | head -10", "description": "Find MOC fresh retros section"}

---

> `Bash` -- {"command": "set -o pipefail; tail -40 \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_a5230cc4/tasks/b8hgi7n6i.output\" 2>&1", "description": "Read panel verdict"}

---

**Claude:**

Панель: **6 из 6 за 71 с, $0.074**. Находки сильные, и три из них бьют ровно по моим слабым местам. Принимаю и чиню сейчас.

Первая: мой вывод «это не мой долг» опирался на `HEAD`, а `HEAD` мог содержать автоснапшот моих же правок — ту самую граблю, которую я сам и описал.

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports\" && echo \"=== последний коммит lab_hand.py ДО этой сессии (до 27.09 07:30) ===\"; git log --format=\"%h %ad %s\" --date=iso -- jobs-watch/lab_hand.py 2>/dev/null | tail -3; echo \"=== самый ранний коммит файла (он родился в этой сессии) ===\"; git log --forma

---

**Claude:**

`lab_hand.py` вообще родился в этой сессии, до неё его не существовало. Значит правильная база для вопроса «мой ли это долг» — состояние репозитория **до сегодняшнего дня**. Проверяю в отдельном worktree, как и советовал gpt-6-sol.

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports\" && BASE=$(git log --format=%h --before=\"2026-10-24 00:00\" -1) && echo \"база (последний коммит до сегодня): $BASE  $(git log -1 --format='%ad %s' --date=iso $BASE)\"; WT=\"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/41a23c08-1841-4

---

> `Bash` -- {"command": "WT=\"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_a5230cc4/scratchpad/wt_base/jobs-watch\" && cd \"$WT\" && cp \"D:/Vault/_imports/jobs-watch/jobs.db\" ./jobs.db 2>/dev/null; echo \"=== _test_jobs_comp на коде ВЧЕРАШНЕГО дня (23.10

---

**Claude:**

Доказано на чистом worktree вчерашнего коммита: те же три FAIL. Возражение панели закрыто уликой, долг не мой.

Теперь самая сильная находка (GLM): у полосы `hand` **нет сторожа** — удали строку, и всё останется зелёным, то есть дыра, стоившая 27 дней, может вернуться молча. Ставлю сторож.

---

> `Write` -- {"file_path": "C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_a5230cc4\\scratchpad\\patch7_h79620.py", "content": "#!/usr/bin/env python3\n\"\"\"Patch H79620 #7 (2026-10-24): storozh na polosu 'hand' v manual_lane.WHY_MANUAL.\n\nNahodka pane

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/jobs-watch\" && tail -6 selenium_apply/_test_manual_lane.py; echo \"=== имя функции проверки ===\"; grep -nE \"^def (chk|check)\" selenium_apply/_test_manual_lane.py | head -3", "description": "Inspect manual lane test tail"}

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/jobs-watch\" && sed -n '25,45p' selenium_apply/_test_manual_lane.py; echo \"=== где конец main ===\"; grep -n \"return 1 if FAILED\" selenium_apply/_test_manual_lane.py", "description": "Read check signature and main structure"}

---

> `Bash` -- {"command": "cd \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_a5230cc4/scratchpad\" && python - <<'PY'\n# heredoc-escape-ok: правит текст патч-скрипта\nimport io\np='patch7_h79620.py'; s=io.open(p,encoding='utf-8').read()\ns=s.replace('chk(\"M1',

---

> `Bash` -- {"command": "cd \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_a5230cc4/scratchpad\" && python - <<'PY'\n# heredoc-escape-ok: правит текст патч-скрипта\nimport io\np='patch7_h79620.py'; s=io.open(p,encoding='utf-8').read()\nold = 'io.open(T, \"w\"

---

**Claude:**

Сломал файл отступом. Откатываю из бэкапа и ставлю блок правильно.

---

> `Write` -- {"file_path": "C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_a5230cc4\\scratchpad\\patch7b_h79620.py", "content": "#!/usr/bin/env python3\n\"\"\"Patch H79620 #7b: vosstanovit _test_manual_lane.py iz bekapa i vstavit storozha s otstupom.\n\n

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/jobs-watch\" && python \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_a5230cc4/scratchpad/patch7b_h79620.py\" && timeout 200 python -X utf8 selenium_apply/_test_manual_lane.py 2>&1 | tail -7", "description": 

---

**Claude:**

Сторожа зелёные, но они печатаются ПОСЛЕ итоговой строки — значит при их падении итог соврёт «ВСЁ ЗЕЛЁНОЕ». Это ровно тот класс, который я сегодня журналирую. Переставляю выше итога.

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/jobs-watch\" && python - <<'PY'\n# heredoc-escape-ok: перестановка готового блока, escape не несёт\nimport io, ast\np='selenium_apply/_test_manual_lane.py'; s=io.open(p,encoding='utf-8').read()\nstart=s.index(\"    # --- Полосы «почему руками»\")\nend=s.index(\

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/jobs-watch\" && grep -n \"итог:\" selenium_apply/_test_manual_lane.py | head -3", "description": "Find exact summary line"}

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/jobs-watch\" && python - <<'PY'\n# heredoc-escape-ok: перестановка блока по номерам строк\nimport io, ast\np='selenium_apply/_test_manual_lane.py'\nlines=io.open(p,encoding='utf-8').read().split('\\n')\nstart=next(i for i,l in enumerate(lines) if l.startswith('

---

**Claude:**

Порядок правильный: сторожа печатаются до итога. Теперь красная проба на них и на L13, которую я до панели не делал.

---

> `Write` -- {"file_path": "C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_a5230cc4\\scratchpad\\redproof3_h79620.py", "content": "#!/usr/bin/env python3\n\"\"\"Red proof H79620 #3: storozha M1/M2/M3 (polosa hand) i L13 (zamok bazy).\n\nL13 do paneli kra

---

> `Bash` -- {"command": "set -o pipefail; cd \"D:/Vault/_imports/jobs-watch\" && timeout 580 python -X utf8 \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_a5230cc4/scratchpad/redproof3_h79620.py\" 2>&1 | tail -8", "description": "Red proof for hand-rail gu

---

**Claude:**

Все три краснеют правильно. Теперь две оставшиеся принятые находки. Пять моделей из шести сказали одно: замок базы я объявил починенным без проверки ПОСЛЕ починки. Делаю настоящую пробу под конкурирующей записью.

---

> `Write` -- {"file_path": "C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_a5230cc4\\scratchpad\\lock_proof_h79620.py", "content": "#!/usr/bin/env python3\n\"\"\"Proba zamka POSLE pochinki (H79620, 24.10.2026) -- otvet paneli shesti lomateley.\n\nPyat mo

---

> `Bash` -- {"command": "set -o pipefail; cd \"D:/Vault/_imports/jobs-watch\" && timeout 580 python -X utf8 \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_a5230cc4/scratchpad/lock_proof_h79620.py\" 2>&1 | grep -vE \"^Google|^ручных\" | tail -12", "descript

---

**Claude:**

Проба после починки: при 25-секундной конкурирующей транзакции прогон **прошёл за 24.7 с** (сеть отработала на занятой базе, запись дождалась), тогда как до правки та же ситуация убивала его дважды.

Последняя находка панели: мой замер Meta был на срезе 25 ролей. Считаю без потолка.

---

> `Bash` -- {"command": "set -o pipefail; cd \"D:/Vault/_imports/jobs-watch\" && timeout 580 python -X utf8 selenium_apply/manual_lane.py --n 400 --per-company 50 --out \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_a5230cc4/scratchpad/ml_uncapped.md\" 2>&

---

**Claude:**

Без потолка: Meta 50 + MSL 23 + DeepMind 50 строк в ручном списке. До правки было ноль строк полосы `hand` при любом потолке — то есть починка не «2 роли», а весь рельс.

Теперь пишу заметку ретро. Сначала ссылка в MOC, чтобы не родить сироту.

---

> `Bash` -- {"command": "cd \"D:/Vault/Vault-Knowledge/01-Conversations/Claude\" && python - <<'PY'\n# heredoc-escape-ok: вставка одной строки в MOC\nimport io\np='_Claude-Sessions-MOC.md'; s=io.open(p,encoding='utf-8').read()\nline=(\"- [[retro-2026-10-24-labdoor-meta-hand-lane]] · H79620: полоса lab-door ч

---

> `Write` -- {"file_path": "D:\\Vault\\Vault-Knowledge\\01-Conversations\\Claude\\Retros\\retro-2026-10-24-labdoor-meta-hand-lane.md", "content": "---\ntitle: \"Ретро H79620: полоса lab-door через 26 дней, Meta в ручном списке, ложная дверь в Библии\"\naliases: [\"Трудоустройство в ИИ-лаборатории: ретро 24.10

---

> `Bash` -- {"command": "set -o pipefail; cd \"C:/Users/dev/.claude/scripts\" && timeout 200 python -B -X utf8 status_claim_lint.py \"D:/Vault/Vault-Knowledge/01-Conversations/Claude/Retros/retro-2026-10-24-labdoor-meta-hand-lane.md\" 2>&1 | tail -8", "description": "Lint the retro note claims"}

---

> `Bash` -- {"command": "set -o pipefail; cd \"C:/Users/dev/.claude/scripts\" && timeout 200 python -X utf8 session_titles.py retro --sid s_a5230cc4 --event \"D:/Vault/Vault-Knowledge/01-Conversations/Claude/Retros/retro-2026-10-24-labdoor-meta-hand-lane.md\" 2>&1 | tail -6", "des

---

> `Bash` -- {"command": "set -o pipefail; cd \"C:/Users/dev/.claude/scripts\" && timeout 200 python -X utf8 session_titles.py retro-plan --sid s_a5230cc4 --event \"D:/Vault/Vault-Knowledge/01-Conversations/Claude/Retros/retro-2026-10-24-labdoor-meta-hand-lane.md\" --text \"++Трудо

---

> `ToolSearch` -- {"query": "select:mcp__ccd_session_mgmt__set_session_title", "max_results": 2}

---

> `mcp__ccd_session_mgmt__set_session_title` -- {"session_id": "self", "title": "💰 · 🚪🧪 Р ++Трудоустройство в ИИ-лаборатории · H79620"}

---

**Claude:**

Заголовок получил веху Р и иконки. Теперь X-пост сессии.

---

> `Write` -- {"file_path": "C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_a5230cc4\\scratchpad\\x_post_h79620.txt", "content": "A month ago I wrote in my own notes that a job module ran every night. It never ran once. The feed sat frozen for 26 days. An

---

> `Bash` -- {"command": "set -o pipefail; SP=\"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_a5230cc4/scratchpad\"; cd \"C:/Users/dev/.claude/scripts\" && timeout 150 python -B -X utf8 retro_x_post.py lint --file \"$SP/x_post_h79620.txt\" 2>&1 | tail -8; ech

---

**Claude:**

Оба гейта пропустили (231 знак, только ожидаемые WARN). Подтягиваю ритм по замечанию гейта и кладу на склад.

---

> `Bash` -- {"command": "set -o pipefail; SP=\"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_a5230cc4/scratchpad\"; printf '%s\\n' \"A month ago I wrote in my own notes that a job module ran every night. It never ran. Not once. The feed sat frozen for 26 days.

---

> `Bash` -- {"command": "set -o pipefail; SP=\"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_a5230cc4/scratchpad\"; cd \"C:/Users/dev/.claude/scripts\" && timeout 150 python -X utf8 x_outbox.py enqueue --file \"$SP/x_post_h79620.txt\" --session H79620 2>&1 |

---

> `Bash` -- {"command": "set -o pipefail; cd \"D:/Vault/_imports/content-factory\" && timeout 200 python -X utf8 content_miner.py capture --title \"Я сам написал в своих правилах, что модуль работает каждую ночь. Он не работал ни разу\" --note \"Правило без двери выглядит как правило. 27.09 я записал в канон
