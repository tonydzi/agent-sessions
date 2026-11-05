---
session: s_33a90300
date: 2026-10-07
words: 38633
turns: 63
tools: "Bash, Edit, Skill, ToolSearch, Write, mcp__ccd_session_mgmt__get_session, mcp__ccd_session_mgmt__set_session_title, mcp__claude-in-chrome__list_connected_browsers"
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-10-07 · Это задача от оператора. Она пришла голосом в Telegram-группу «001 СЕССИЯ НОВАЯ»

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_33a90300` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

Это задача от оператора. Она пришла голосом в Telegram-группу «001 СЕССИЯ НОВАЯ»,
расшифрована ботом. Источник: tg:chat_REDACTED:u240304.

ДОСЛОВНО, ЧТО СКАЗАЛ оператор:
---
Давай попробуем применить как канарейка. 

Попробуем?

Карпатыч поделился очередной легендарочкой. На этот раз он рассказывает, как понимать ответы нейронок. Модели все больше пашут сами, а наша работа съезжает в сторону «проверить и понять, что они там натворили». И вот тут засада. Нейронка за минуту выдает простыню, а ты потом полчаса продираешься через «является», «осуществляет» и «в рамках данного подхода». Узким местом становится уже не модель, а наша с вами белковая размышлялка.

И решение у Андрея интересное. Он просит модели отвечать на ASD-STE100. Это упрощенный технический английский, на котором с 80-х пишут инструкции по ремонту самолетов...

Логика простая. Механик в любой точке мира должен понять инструкцию одинаково, иначе самолет не взлетит (или взлетит, но ненадолго). Поэтому правила там жесткие. Около 900 разрешенных слов, и у каждого только одно значение. В процедурном предложении максимум 20 слов. В одном предложении одна команда, и никакого пассива. Не «utilize», а «use». Не «ensure», а «make sure». Сначала команда, потом риск.

А фишка в том, что нейронки прочитали тонны такой документации и знают стандарт. Стандарт, правда, строгий, поэтому Карпати иногда просит «на 80% как ASD-STE100». По сути это такая ручка громкости для антислопа, кайф. 

Ну и он там еще несколько форматов вывода информации приводит. Например вместо текста просить схему, потому что глаз схватывает быстрее, чем мозг дочитывает. Дописать к запросу «сделай в HTML» и получить вместо простыни интерактивную страничку. 
А самая жирная ставка у него на видео-объяснения в стиле 3Blue1Brown, с озвучкой через ElevenLabs или бесплатную локальную альтернативу. 

И как тут не вспомнить мой пост о том, что Карпати хочет только одного, чтобы мы выжгли все свои лимиты, если главная мысль его поста, что код и интеллект дешевеют, поэтому теперь можно заказывать целое приложение или ролик, просто чтобы один раз понять одну тему. И потом выкинуть, как черновик. Раньше такое было бы безумием, а теперь это обычный вторник.

[РЕЛЬСА 001: это текстовое сообщение от 2026-10-07T01:03 UTC, поднято роботом voice001_watch.
]
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

> `Bash` -- {"command": "TZ=Europe/Lisbon date '+LISBON %Y-%m-%d %H:%M'; TZ=Europe/Moscow date '+MSK %Y-%m-%d %H:%M'; echo \"---HOST---\"; hostname", "description": "Замер времени и хоста"}

---

> `Bash` -- {"command": "cd /c/Users/dev/.claude 2>/dev/null || cd ~/.claude; grep -ril \"ASD-STE\\|STE100\\|simplified technical english\" . 2>/dev/null | head -30; echo \"=== VAULT ===\"; grep -ril \"ASD-STE\\|STE100\\|simplified technical\" /e/Obsidian/Vault-Knowledge 2>/dev/null | head -30; echo \"=== don

---

> `Bash` -- {"command": "ls ~/.claude/scripts/llm_ask.py ~/.claude/scripts/_shared/ 2>/dev/null | head -40; echo \"=== secondop ===\"; ls -la ~/.claude/cc-review/ 2>/dev/null | head -20; echo \"=== output-styles ===\"; ls ~/.claude/output-styles/ 2>/dev/null", "description": "Смотрю рельсу llm_ask и secondop"}

---

> `Bash` -- {"command": "grep -ril \"ASD-STE\\|STE100\\|simplified technical\\|Teague\\|карпат\" ~/.claude/projects/P---WORKDIR-HUB/memory/ ~/.claude/skills/ 2>/dev/null | head -20; echo \"=== END ===\"", "description": "RECALL по памяти и скиллам"}

---

> `Bash` -- {"command": "cat ~/.claude/projects/P---WORKDIR-HUB/memory/Teague-llm-wiki-no-live-door.md 2>/dev/null; echo \"=== PROMPTDESIGN ===\"; cat ~/.claude/projects/P---WORKDIR-HUB/memory/promptdesign-mine.md 2>/dev/null | head -40", "description": "Читаю память про Карпати и пр

---

> `Bash` -- {"command": "find ~/.claude -maxdepth 2 -name \"secondop.py\" -o -maxdepth 2 -name \"orouter_review.py\" 2>/dev/null; echo \"=== llm_ask head ===\"; sed -n '1,60p' ~/.claude/scripts/llm_ask.py", "description": "Ищу движки веера"}

---

> `Bash` -- {"command": "grep -n \"AGENT_FRAME\" ~/.claude/scripts/llm_ask.py | head -20; echo \"=== FRAME BODY ===\"; python - <<'EOF'\nimport re,io\np=r\"C:\\Users\\dev\\.claude\\scripts\\llm_ask.py\"\ns=io.open(p,encoding=\"utf-8\").read()\ni=s.find(\"AGENT_FRAME\")\nprint(s[i-200:i+3000])\nEOF", "descript

---

> `Bash` -- {"command": "cat \"C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_33a90300\\tasks\\bp29rou06.output\" 2>/dev/null | tail -40", "description": "Проверяю фоновый греп по волту"}

---

> `Bash` -- {"command": "sed -n '890,950p' ~/.claude/scripts/llm_ask.py", "description": "Читаю тело AGENT_FRAME"}

---

> `Bash` -- {"command": "f=\"C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_33a90300\\tasks\\bp29rou06.output\"; ls -la \"$f\"; echo \"--- content ---\"; cat \"$f\"; echo \"--- end ---\"", "description": "Статус фонового грепа по волту"}

---

> `Bash` -- {"command": "cd ~/.claude/scripts; ls | grep -iE \"ste_|slop|paragraph|lint\" | head -30; echo \"=== rail_plan ===\"; ls rail_plan.py prior_art.py red_proof.py 2>/dev/null; echo \"=== shadow queue ===\"; ls \"D:\\Vault\\Vault-Knowledge\\00-System\\Shadow-First-Queue.md\" 2>/dev/null && tail -6 \"

---

> `Bash` -- {"command": "cd ~/.claude/scripts && python prior_art.py class \"ответ LLM слишком длинный и его трудно читать, упрощённый технический язык ASD-STE100 как ручка антислопа\" 2>&1 | head -40", "description": "Счёт по семье через prior_art"}

---

> `Bash` -- {"command": "cd ~/.claude/scripts && python rail_plan.py declare --self \"оркестрация канарейки ASD-STE100: решение где ставить, прибор-скорер (детерминизм, 0 токенов), A/B-замер, дверь в llm_ask, запись в shadow-queue, /tt\" --rails \"codex,grok,gemini: живые ответы на ОДИН реальный вопрос в двух р

---

> `Bash` -- {"command": "cd ~/.claude/scripts && sed -n '1,45p' paragraph_lint.py", "description": "Смотрю домашний стиль соседнего прибора"}

---

> `Bash` -- {"command": "cd ~/.claude/scripts && python rail_plan.py declare --help 2>&1 | head -25", "description": "Смотрю интерфейс rail_plan declare"}

---

> `Bash` -- {"command": "f=\"C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_33a90300\\tasks\\bp29rou06.output\"; wc -c \"$f\"; grep -c \"exited with code\" \"$f\" 2>/dev/null || echo \"НЕ ЗАВЕРШИЛСЯ\"", "description": "Статус фонового поиска по волту"}

---

> `Bash` -- {"command": "cd ~/.claude/scripts && python rail_plan.py declare --self \"оркестрация канарейки ASD-STE100: где ставить, прибор-скорер (0 токенов), дверь в llm_ask, запись в shadow-queue, /tt\" --outsource \"second_opinion:codex,second_opinion:grok,second_opinion:gemini\" 2>&1 | tail -12", "descript

---

> `Bash` -- {"command": "cd ~/.claude/scripts/_shared && ls *.py | head -40; echo \"=== blind_zone iface ===\"; sed -n '1,40p' blind_zone.py 2>/dev/null", "description": "Смотрю общие помощники: blind_zone, usage"}

---

> `Bash` -- {"command": "cd ~/.claude/scripts/_shared && grep -n \"^def line\\|^def verdict\" blind_zone.py; sed -n \"$(grep -n '^def line' blind_zone.py | cut -d: -f1),+25p\" blind_zone.py", "description": "Сигнатура blind_zone.line"}

---

> `Bash` -- {"command": "cd ~/.claude/scripts && grep -rln \"part_usage\\|part-usage\" _shared/*.py *.py 2>/dev/null | head -5; echo \"=== iface ===\"; sed -n '1,30p' _shared/part_usage.py 2>/dev/null || grep -n \"def .*usage\" paragraph_lint.py", "description": "Ищу общий счётчик использования"}

---

> `Bash` -- {"command": "cd ~/.claude/scripts/_shared && grep -n \"^def \\|^PART\\|^USAGE\" skill_usage_log.py | head -20; echo \"---\"; sed -n '1,25p' skill_usage_log.py", "description": "Интерфейс счётчика skill_usage_log"}

---

> `Bash` -- {"command": "cd ~/.claude/scripts/_shared && sed -n '72,84p' skill_usage_log.py; echo \"=== log sig ===\"; sed -n '133,145p' skill_usage_log.py", "description": "Виды счётчика и подпись log()"}

---

**Claude:**

Пишу прибор. Сначала скорер — детерминированный, 0 токенов.

---

> `Bash` -- {"command": "cat > /c/Users/dev/.claude/scripts/ste_score.py <<'PYEOF'\n#!/usr/bin/env python3\n# -*- coding: utf-8 -*-\n\"\"\"ste_score.py — РУЧКА ГРОМКОСТИ АНТИСЛОПА числом: насколько текст похож на ASD-STE100.\n\nЗАЧЕМ (оператор 07.10.2026, текстом в рельсу 001, по посту про совет Карпаты:\n«Давай

---

> `Write` -- {"file_path": "C:\\Users\\dev\\.claude\\scripts\\ste_score.py", "content": "#!/usr/bin/env python3\n# -*- coding: utf-8 -*-\n\"\"\"ste_score.py — РУЧКА ГРОМКОСТИ АНТИСЛОПА ЧИСЛОМ: насколько текст похож на ASD-STE100.\n\nЗАЧЕМ (оператор 07.10.2026, текстом в рельсу 001, по посту про совет Карпаты:\n«Д

---

> `Bash` -- {"command": "cd /c/Users/dev/.claude/scripts && python ste_score.py --self-test; echo \"EXIT=$?\"", "description": "Самотест скорера"}

---

> `Write` -- {"file_path": "C:\\Users\\dev\\.claude\\scripts\\ste_directive.md", "content": "[OUTPUT STYLE — {PCT}% ASD-STE100 Simplified Technical English.\n\nWrite your answer in Simplified Technical English (ASD-STE100), at about {PCT}% compliance.\nYou know this standard: it is the controlled English of ai

---

> `Bash` -- {"command": "cd /c/Users/dev/.claude/scripts && python - <<'EOF'\nimport io\np=\"ste_directive.md\"\ns=io.open(p,encoding=\"utf-8\").read()\ns=s.replace(\"no simple替 equivalent\",\"no simple equivalent\")\nio.open(p,\"w\",encoding=\"utf-8\",newline=\"\\n\").write(s)\nprint(\"替 осталось:\", \"替\" i

---

> `Bash` -- {"command": "cd /c/Users/dev/.claude/scripts && grep -n \"add_argument\\|^def main\\|prompt = \\|ap = argparse\\|ArgumentParser\" llm_ask.py | tail -40", "description": "Ищу argparse в llm_ask.py"}

---

> `Bash` -- {"command": "cd /c/Users/dev/.claude/scripts && sed -n '1755,1800p' llm_ask.py", "description": "Читаю участок сборки промпта"}

---

**Claude:**

Теперь дверь — флаг `--ste` в `llm_ask.py`, по умолчанию ВЫКЛЮЧЕН.

---

> `Bash` -- {"command": "cd /c/Users/dev/.claude/scripts && cp llm_ask.py llm_ask.py.bak-pre-ste-20261007 && python - <<'EOF'\nimport io\np = \"llm_ask.py\"\ns = io.open(p, encoding=\"utf-8\").read()\n\nold_arg = '''    ap.add_argument(\"--routing\", action=\"store_true\",\n                    help=\"показать

---

**Claude:**

Канарейка должна быть ЗАМЕРЕНА, а не объявлена. Гоню живой A/B на реальном открытом вопросе флота.

---

> `Bash` -- {"command": "mkdir -p /c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_33a90300/scratchpad/ste && cat > /c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_33a90300/scratchpad/ste/q.txt <<'EOF'\nWe run a f

---

> `Bash` -- {"command": "D=/c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_33a90300/scratchpad/ste; cd /c/Users/dev/.claude/scripts && python llm_ask.py --prompt-file \"$D/q.txt\" --rails codex --mode first --timeout 420 > \"$D/codex-off.md\" 2>\"$D/codex-off.

---

> `Bash` -- {"command": "D=/c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_33a90300/scratchpad/ste; cd /c/Users/dev/.claude/scripts && python llm_ask.py --prompt-file \"$D/q.txt\" --rails grok --mode first --timeout 420 > \"$D/grok-off.md\" 2>\"$D/grok-off.err

---

> `Bash` -- {"command": "D=/c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_33a90300/scratchpad/ste; cd /c/Users/dev/.claude/scripts && python llm_ask.py --prompt-file \"$D/q.txt\" --rails codex --mode first --timeout 420 --ste 80 > \"$D/codex-on.md\" 2>\"$D/co

---

> `Bash` -- {"command": "D=/c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_33a90300/scratchpad/ste; cd /c/Users/dev/.claude/scripts && python llm_ask.py --prompt-file \"$D/q.txt\" --rails grok --mode first --timeout 420 --ste 80 > \"$D/grok-on.md\" 2>\"$D/grok

---

**Claude:**

Пока рельсы думают — тест с красным доказательством.

---

> `Write` -- {"file_path": "C:\\Users\\dev\\.claude\\scripts\\_test_ste_score.py", "content": "#!/usr/bin/env python3\n# -*- coding: utf-8 -*-\n\"\"\"_test_ste_score.py — сторож прибора ste_score.py (канарейка ASD-STE100, 07.10.2026).\n\nПОЧЕМУ ИМЕННО ЭТИ ПРОВЕРКИ. Прибор меряет ЧУЖОЙ текст, поэтому самый доро

---

> `Bash` -- {"command": "cd /c/Users/dev/.claude/scripts && python _test_ste_score.py; echo \"EXIT=$?\"", "description": "Гоняю сторож"}

---

**Claude:**

Прибор соврал о ПРИЧИНЕ: русское предложение он забраковал как «короче 3 слов». Корень — проверки стоят в неверном порядке.

---

> `Bash` -- {"command": "cd /c/Users/dev/.claude/scripts && python - <<'EOF'\nimport io\np=\"ste_score.py\"\ns=io.open(p,encoding=\"utf-8\").read()\nold = '''def _judgeable(sent):\n    \"\"\"Судим только то, что похоже на английскую прозу.\"\"\"\n    words = WORD_RE.findall(sent)\n    if len(words) < 3:\n    

---

> `Bash` -- {"command": "D=/c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_33a90300/scratchpad/ste; for f in codex-off codex-on grok-off grok-on; do printf \"%-12s %8s байт  err: %s\\n\" \"$f\" \"$(wc -c < $D/$f.md 2>/dev/null || echo 0)\" \"$(tail -1 $D/$f.err 

---

> `Bash` -- {"command": "cd /c/Users/dev/.claude/scripts && python red_proof.py --help 2>&1 | head -25", "description": "Интерфейс red_proof"}

---

> `Bash` -- {"command": "cd /c/Users/dev/.claude/scripts && python red_proof.py --file ste_score.py \\\n --old 'if letters and len(latin) / float(len(letters)) < 0.6:\n        return False, \"не латиница (русский или смешанный текст)\"' \\\n --new 'if False:\n        return False, \"не латиница (русский или с

---

**Claude:**

Проверка прошла на сломанном коде — значит убийство №5 в моём списке названо неверно: латиницу подстраховывает счёт слов. Ломается там не ЧИСЛО, а ПРИЧИНА. Переписываю ломатель под то, что поломка реально меняет.

---

> `Write` -- {"file_path": "C:\\Users\\dev\\.claude\\scripts\\_shared\\_probe_ste_latin.py", "content": "#!/usr/bin/env python3\n# -*- coding: utf-8 -*-\n\"\"\"Ломатель-проба для red_proof: ПРИЧИНА отказа судить русский текст.\n\nУбийство №5 из списка _test_ste_score.py изначально было названо неверно: «уберу 

---

> `Bash` -- {"command": "cd /c/Users/dev/.claude/scripts && python red_proof.py --file ste_score.py \\\n --old 'if letters and len(latin) / float(len(letters)) < 0.6:' \\\n --new 'if False and letters and len(latin) / float(len(letters)) < 0.6:' \\\n --also _shared/_probe_ste_latin.py \\\n --expect-fail '{py}

---

> `Bash` -- {"command": "cd /c/Users/dev/.claude/scripts && python red_proof.py --file ste_score.py \\\n --old 'res[\"clean_pct\"] = round(100.0 * res[\"clean\"] / j, 1) if j else 0.0' \\\n --new 'res[\"clean_pct\"] = round(100.0 * res[\"clean\"] / res[\"sentences_total\"], 1) if res[\"sentences_total\"] else

---

> `Bash` -- {"command": "cd /c/Users/dev/.claude/scripts && python red_proof.py --file ste_score.py \\\n --old '    L.append(rules_line())\n    L.append(blind_line(res))\n    return \"\\n\".join(L)' \\\n --new '    L.append(rules_line())\n    return \"\\n\".join(L)' \\\n --expect-fail '{py} -c \"import sys;sy

---

> `Bash` -- {"command": "cd /c/Users/dev/.claude/scripts && python - <<'EOF'\nimport io\np=\"_test_ste_score.py\"\ns=io.open(p,encoding=\"utf-8\").read()\nold=\"  5  убрать проверку латиницы -> русский текст станет «судимым» и получит фальшивый балл\"\nnew=(\"  5  убрать проверку латиницы -> прибор СОВРЁТ О П

---

> `Bash` -- {"command": "ls -d \"D:\\Vault\\_originals\" 2>/dev/null && ls \"D:\\Vault\\_originals\" | head -5; echo \"=== Operations ===\"; ls \"D:\\Vault\\Vault-Knowledge\\03-Insights\\Operations\" 2>/dev/null | grep -iE \"pilot|shadow|experiment\" | head -10; echo \"=== count ===\"; ls \"E:\\Obsidia

---

> `Bash` -- {"command": "D=/c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_33a90300/scratchpad/ste; for f in codex-off codex-on grok-off grok-on; do printf \"%-11s %7s байт | %s\\n\" \"$f\" \"$(wc -c < $D/$f.md 2>/dev/null || echo 0)\" \"$(tail -1 $D/$f.err 2>/d

---

> `Write` -- {"file_path": "D:\\Vault\\_originals\\voice001-20261007-ste100-canary.md", "content": "---\nsource: tg:chat_REDACTED:u240304\nchannel: \"001 СЕССИЯ НОВАЯ\"\nreceived: 2026-10-07T01:03:00Z\nkind: original-verbatim\nnote: Текст оператора дословно, без правок. Копия нужна, потому что в чате 001 сообщения

---

> `Bash` -- {"command": "D=/c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_33a90300/scratchpad/ste; for f in codex-off codex-on grok-off grok-on; do printf \"%-11s %7s байт\\n\" \"$f\" \"$(wc -c < $D/$f.md 2>/dev/null || echo 0)\"; done", "description": "Размеры

---

> `Bash` -- {"command": "for t in b245plxi1 b1f4udzxr b1x5fnpmh; do echo \"=== $t ===\"; cat \"C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_33a90300\\tasks\\$t.output\" 2>/dev/null | tail -8; done", "description": "Читаю вывод фоновых прогонов"}

---

> `Bash` -- {"command": "ls -la \"/c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_33a90300/scratchpad/ste/\" 2>&1", "description": "Листинг папки замера"}

---

> `Bash` -- {"command": "D=/c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_33a90300/scratchpad/ste; echo \"### codex-off.err\"; cat \"$D/codex-off.err\"; echo; echo \"### grok-off.err\"; cat \"$D/grok-off.err\"", "description": "Читаю диагностику рельс"}

---

**Claude:**

Обе рельсы отдали таймаут 420с. Таймаут — это «не смог проверить», а не «рельса мертва» (§5.4). Делаю живую пробу.

---

> `Bash` -- {"command": "D=/c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_33a90300/scratchpad/ste; cd /c/Users/dev/.claude/scripts && time python llm_ask.py --prompt \"Reply with exactly: ALIVE\" --rails codex --mode first --timeout 150 > \"$D/probe-codex.txt

---

> `Bash` -- {"command": "D=/c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_33a90300/scratchpad/ste; cd /c/Users/dev/.claude/scripts && time python llm_ask.py --prompt \"Reply with exactly: ALIVE\" --rails grok --mode first --timeout 150 > \"$D/probe-grok.txt\"

---

**Claude:**

Пока пробы идут — замер на РЕАЛЬНОМ корпусе, который у нас уже лежит: англоязычные ДР-отчёты.

---

> `Bash` -- {"command": "cd \"E:\\!CLAUDE-HUBPC-June26\" && ls -la downloads/*.md 2>/dev/null | head; echo \"=== прогон ===\"; python /c/Users/dev/.claude/scripts/ste_score.py \"downloads/deep-research-report.md\" 2>&1 | head -30", "description": "Замер на реальном ДР-отчёте"}

---

**Claude:**

Живые данные сразу нашли дефект: в смешанном RU/EN тексте русские слова ВЫПАДАЮТ из токенов, и оставшиеся английские склеиваются в фальшивую «цепочку существительных». Это ровно класс [[fixture-green-live-run-red]]. Чиню корень.

---

> `Bash` -- {"command": "cd /c/Users/dev/.claude/scripts && cp ste_score.py ste_score.py.bak-pre-mixed-20261007 && python - <<'PYEOF'\nimport io\np = \"ste_score.py\"\ns = io.open(p, encoding=\"utf-8\").read()\n\n# 1) токенизатор с РАЗРЫВАМИ + счёт русских слов\nold = '''WORD_RE = re.compile(r\"[A-Za-z][A-Za-

---

> `Bash` -- {"command": "D=/c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_33a90300/scratchpad/ste; echo \"### grok проба\"; cat \"$D/probe-grok.txt\" 2>/dev/null | head -8; echo; echo \"### codex проба\"; cat \"$D/probe-codex.txt\" 2>/dev/null | head -8; echo; 

---

**Claude:**

Grok жив (73с на тривиальный промпт при xhigh). Значит 420с — это не мёртвая рельса, а дорогая постановка вопроса. Меняю ВОПРОС на более дешёвый по рассуждению, усилие НЕ понижаю (§6.3), таймаут поднимаю.

---

> `Bash` -- {"command": "D=/c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_33a90300/scratchpad/ste; cat > \"$D/q2.txt\" <<'EOF'\nExplain to an engineer how a canary rollout works when you ship a small fix to a fleet of\n8 machines that are not identical: 5 Windo

---

> `Bash` -- {"command": "D=/c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_33a90300/scratchpad/ste; cat \"$D/probe-codex.txt\" | head -6", "description": "Проба codex"}

---

**Claude:**

Обе рельсы живы: codex 88с, grok 73с. Запускаю A/B заново.

---

> `Bash` -- {"command": "D=/c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_33a90300/scratchpad/ste; cd /c/Users/dev/.claude/scripts && python llm_ask.py --prompt-file \"$D/q2.txt\" --rails codex --mode first --timeout 900 > \"$D/c-off.md\" 2>\"$D/c-off.err\"; 

---

> `Bash` -- {"command": "D=/c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_33a90300/scratchpad/ste; cd /c/Users/dev/.claude/scripts && python llm_ask.py --prompt-file \"$D/q2.txt\" --rails codex --mode first --timeout 900 --ste 80 > \"$D/c-on.md\" 2>\"$D/c-on.

---

> `Bash` -- {"command": "D=/c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_33a90300/scratchpad/ste; cd /c/Users/dev/.claude/scripts && python llm_ask.py --prompt-file \"$D/q2.txt\" --rails grok --mode first --timeout 900 > \"$D/g-off.md\" 2>\"$D/g-off.err\"; e

---

> `Bash` -- {"command": "D=/c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_33a90300/scratchpad/ste; cd /c/Users/dev/.claude/scripts && python llm_ask.py --prompt-file \"$D/q2.txt\" --rails grok --mode first --timeout 900 --ste 80 > \"$D/g-on.md\" 2>\"$D/g-on.e

---

> `Bash` -- {"command": "ls /c/Users/dev/.claude/_metrics/llm_ask_partial/ 2>/dev/null | wc -l; ls -S /c/Users/dev/.claude/_metrics/llm_ask_partial/ 2>/dev/null | head -8", "description": "Корпус живых ответов рельс"}

---

> `Bash` -- {"command": "cd \"E:\\!CLAUDE-HUBPC-June26\" && python /c/Users/dev/.claude/scripts/ste_score.py \"downloads/deep-research-report.md\" 2>&1 | sed -n '1,8p;$p'", "description": "Перезамер ДР после починки"}

---

**Claude:**

258 реальных ответов рельс лежат в `_metrics/llm_ask_partial` — это и есть корпус, который мы читаем. Добавляю сводный режим, чтобы замер был повторяемым на урожае.

---

> `Bash` -- {"command": "cd /c/Users/dev/.claude/scripts && python - <<'PYEOF'\nimport io\np = \"ste_score.py\"\ns = io.open(p, encoding=\"utf-8\").read()\n\nold = '''    ap.add_argument(\"--self-test\", action=\"store_true\")'''\nnew = '''    ap.add_argument(\"--aggregate\", action=\"store_true\",\n         

---

> `Bash` -- {"command": "cd /c/Users/dev/.claude/scripts && sed -n '524,536p' ste_score.py", "description": "Смотрю битый участок"}

---

> `Edit` -- {"replace_all": false, "file_path": "C:\\Users\\dev\\.claude\\scripts\\ste_score.py", "old_string": "        res = score(\"\n\n\".join(t for _, t in texts), a.max_words)", "new_string": "        res = score((\"%s%s\" % (chr(10), chr(10))).join(t for _, t in texts), a.max_words)"}

---

> `Bash` -- {"command": "cd /c/Users/dev/.claude/scripts && python _test_ste_score.py 2>&1 | tail -2; echo \"--- БАЗОВАЯ ЛИНИЯ: живые ответы рельс ---\"; python ste_score.py --aggregate /c/Users/dev/.claude/_metrics/llm_ask_partial/*.md 2>&1 | head -18", "description": "Тесты + базовая линия корпуса"}

---

> `Bash` -- {"command": "D=/c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_33a90300/scratchpad/ste; for f in c-off c-on g-off g-on; do printf \"%-7s %7s байт | %s\\n\" \"$f\" \"$(wc -c < $D/$f.md 2>/dev/null || echo 0)\" \"$(tail -1 $D/$f.err 2>/dev/null | cut -

---

> `Bash` -- {"command": "cd /c/Users/dev/.claude/scripts && python selfheal.py journal --help 2>&1 | head -18", "description": "Интерфейс журнала уроков"}

---

> `Bash` -- {"command": "cd /c/Users/dev/.claude/scripts && python selfheal.py journal --class \"fixture-green-live-run-red\" --what \"ste_score.py: самотест и 38 проверок были ЗЕЛЁНЫЕ, живой прогон по ДР-отчёту дал 34 фальшивые цепочки существительных и завысил FAIL. Корень: судимость считалась по БУКВАМ (ру

---

**Claude:**

Я сам наступил на [[class-counted-by-name-never-reaches-three]] — завёл новый ключ `fixture-green-live-run-red` при живой семье `fixture-green-rail-shape-unknown`. Исправляю счёт.

---

> `Bash` -- {"command": "cd /c/Users/dev/.claude/scripts && python prior_art.py families 2>&1 | grep -iE \"fixture\" ; echo \"=== перелогирую в ПРАВИЛЬНУЮ семью ===\"; python selfheal.py journal --class \"fixture-green-rail-shape-unknown\" --what \"ste_score.py (07.10): 38 проверок и самотест ЗЕЛЁНЫЕ, первый 

---

> `Bash` -- {"command": "D=/c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_33a90300/scratchpad/ste; for f in c-off c-on g-off g-on; do printf \"%-7s %7s байт | %s\\n\" \"$f\" \"$(wc -c < $D/$f.md 2>/dev/null || echo 0)\" \"$(tail -1 $D/$f.err 2>/dev/null | cut -

---

> `Bash` -- {"command": "D=/c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_33a90300/scratchpad/ste; echo \"################ GROK БЕЗ STE (первые 1200 симв)\"; head -c 1200 \"$D/g-off.md\"; echo; echo; echo \"################ CODEX С STE-80 (первые 1200 симв)\"; 

---

> `Bash` -- {"command": "cat \"C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_33a90300\\tasks\\bvsligjih.output\" 2>/dev/null | tail -6", "description": "Результат переноса в семью"}

---

> `Bash` -- {"command": "D=/c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_33a90300/scratchpad/ste; for f in c-off c-on g-off g-on; do printf \"%-7s %7s байт | %s\\n\" \"$f\" \"$(wc -c < $D/$f.md 2>/dev/null || echo 0)\" \"$(tail -1 $D/$f.err 2>/dev/null | cut -

---

> `Bash` -- {"command": "D=/c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_33a90300/scratchpad/ste; cd /c/Users/dev/.claude/scripts && echo \"############ CODEX: до → после\" && python ste_score.py --compare \"$D/c-off.md\" \"$D/c-on.md\" 2>&1", "description":

---

> `Bash` -- {"command": "D=/c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_33a90300/scratchpad/ste; printf \"g-on: %s байт | %s\\n\" \"$(wc -c < $D/g-on.md 2>/dev/null || echo 0)\" \"$(tail -1 $D/g-on.err 2>/dev/null | cut -c1-80)\"", "description": "Жду grok с 

---

**Claude:**

Добавляю счётчик на саму дверь — иначе у канарейки не будет замера использования (§5.8).

---

> `Bash` -- {"command": "cd /c/Users/dev/.claude/scripts && python - <<'PYEOF'\nimport io\np = \"llm_ask.py\"\ns = io.open(p, encoding=\"utf-8\").read()\nold = '''            prompt = ste_score.directive(pct) + prompt\n            _log(\"STE-канарейка: директива %d%% добавлена (+%d симв.)\"\n                 

---

> `Bash` -- {"command": "cd /c/Users/dev/.claude/scripts/_shared && python skill_usage_log.py --kind part --days 1 2>&1 | grep -iE \"llm_ask_ste|ste_score\" | head -5; echo \"--- прямое чтение шарда ---\"; python - <<'EOF'\nimport sys, json\nsys.path.insert(0, \".\")\nimport skill_usage_log as s\nrows = [r fo

---

> `Bash` -- {"command": "D=/c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_33a90300/scratchpad/ste; printf \"g-on: %s байт | %s\\n\" \"$(wc -c < $D/g-on.md 2>/dev/null || echo 0)\" \"$(tail -1 $D/g-on.err 2>/dev/null|cut -c1-80)\"", "description": "grok с директ

---

> `Bash` -- {"command": "cd /c/Users/dev/.claude/scripts && python - <<'PYEOF'\nimport io\np = r\"D:\\Vault\\Vault-Knowledge\\00-System\\Shadow-First-Queue.md\"\nrow = (\"| [[pilot-ste100-canary|Канарейка ASD-STE100]] — упрощённый технический английский как \"\n       \"РУЧКА АНТИСЛОПА на чужих рельсах (`l

---

> `Bash` -- {"command": "D=/c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_33a90300/scratchpad/ste; printf \"g-on: %s байт\\n\" \"$(wc -c < $D/g-on.md 2>/dev/null || echo 0)\"; tail -2 \"$D/g-on.err\" 2>/dev/null", "description": "grok с директивой — финальная п

---

> `Bash` -- {"command": "ls \"D:\\Vault\\Vault-Knowledge\\90_MOCs\" 2>/dev/null | head -30", "description": "Какие MOC есть для дороги из хаба"}

---

> `Bash` -- {"command": "head -25 \"D:\\Vault\\Vault-Knowledge\\90_MOCs\\_Experiments-MOC.md\" 2>/dev/null; echo \"... строк всего:\"; wc -l < \"D:\\Vault\\Vault-Knowledge\\90_MOCs\\_Experiments-MOC.md\"", "description": "Смотрю MOC экспериментов для дороги из хаба"}

---

> `Bash` -- {"command": "D=/c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_33a90300/scratchpad/ste; printf \"g-on: %s байт\\n\" \"$(wc -c < $D/g-on.md 2>/dev/null || echo 0)\"; tail -3 \"$D/g-on.err\" 2>/dev/null; echo \"---\"; cd /c/Users/dev/.claude/scripts 

---

**Claude:**

Пишу заметку в волт, пока grok с директивой ещё считает.

---

> `Write` -- {"file_path": "D:\\Vault\\Vault-Knowledge\\03-Insights\\Operations\\experiment-ste100-canary.md", "content": "---\ntitle: \"Эксперимент — канарейка ASD-STE100: упрощённый технический английский как ручка антислопа\"\ntype: experiment\nlayer: essence\nstatus: active\nstage: shadow\norigin: dev\n

---

> `Bash` -- {"command": "cd /c/Users/dev/.claude/scripts && python - <<'PYEOF'\nimport io\n# 1) поправить ссылку в очереди теней на фактическое имя заметки\np = r\"D:\\Vault\\Vault-Knowledge\\00-System\\Shadow-First-Queue.md\"\ns = io.open(p, encoding=\"utf-8\").read()\ns2 = s.replace(\"[[pilot-ste100-cana

---

> `Bash` -- {"command": "D=/c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_33a90300/scratchpad/ste; printf \"g-on: %s байт\\n\" \"$(wc -c < $D/g-on.md 2>/dev/null || echo 0)\"; tail -3 \"$D/g-on.err\" 2>/dev/null", "description": "grok с директивой — ещё раз"}

---

**Claude:**

Метрика (в) — «не ломает ли директива ФОРМАТ» — это назначенный kill-риск. Проверяю его сейчас, а не на урожае.

---

> `Bash` -- {"command": "D=/c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_33a90300/scratchpad/ste; cat > \"$D/fmt.txt\" <<'EOF'\nReview this one-line change and answer in the required format.\n\nCHANGE: a gate rejected any apply command containing the word \"py

---

> `Bash` -- {"command": "D=/c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_33a90300/scratchpad/ste; echo \"### gemini err\"; cat \"$D/fmt-on.err\"; echo; echo \"### g-on\"; printf \"%s байт\\n\" \"$(wc -c < $D/g-on.md)\"; tail -3 \"$D/g-on.err\"", "description":

---

> `Bash` -- {"command": "D=/c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_33a90300/scratchpad/ste; cd /c/Users/dev/.claude/scripts && echo \"############ GROK: до → после\" && python ste_score.py --compare \"$D/g-off.md\" \"$D/g-on.md\" 2>&1 | sed -n '1,17p'"

---

> `Bash` -- {"command": "D=/c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_33a90300/scratchpad/ste; cd /c/Users/dev/.claude/scripts && python llm_ask.py --prompt-file \"$D/fmt.txt\" --rails codex --mode first --timeout 400 --ste 80 > \"$D/fmt-codex.md\" 2>\"$D

---

> `Bash` -- {"command": "D=/c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_33a90300/scratchpad/ste; cd /c/Users/dev/.claude/scripts/_shared && python blind_zone.py --run python /c/Users/dev/.claude/scripts/ste_score.py --aggregate /c/Users/dev/.claude/_met

---

**Claude:**

Гейт слепой зоны требует назвать, чем судить остаток. Отвечаю в коде — иначе следующий читатель «поднимет покрытие», ослабив языковой фильтр, и вернёт ровно тот баг, что я сегодня починил.

---

> `Bash` -- {"command": "cd /c/Users/dev/.claude/scripts && python - <<'PYEOF'\nimport io\np = \"ste_score.py\"\ns = io.open(p, encoding=\"utf-8\").read()\nold = '''ВХОД:  пути к файлам .md/.txt  ЛИБО  --stdin'''\nnew = '''⚠️ ПОКРЫТИЕ И ЧЕМ СУДИТЬ ОСТАТОК (ответ гейту blind_zone, замер 07.10.2026).\n   На ОДН

---

> `Bash` -- {"command": "D=/c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_33a90300/scratchpad/ste; printf \"fmt-codex: %s байт\\n\" \"$(wc -c < $D/fmt-codex.md 2>/dev/null || echo 0)\"; echo \"--- тег ---\"; grep -nE \"VERDICT: (ACCEPT|BLOCK)\" \"$D/fmt-codex.m

---

> `Write` -- {"file_path": "C:\\Users\\dev\\.claude\\projects\\P---WORKDIR-HUB\\memory\\ste100-is-a-knob-not-a-certificate.md", "content": "---\nname: ste100-is-a-knob-not-a-certificate\ndescription: \"Канарейка ASD-STE100 на чужих рельсах (llm_ask.py --ste, дефолт ВЫКЛ): форму правит сильно (чист

---

> `Bash` -- {"command": "cd /c/Users/dev/.claude/projects/P---WORKDIR-HUB/memory && python - <<'PYEOF'\nimport io\np = \"MEMORY.md\"\ns = io.open(p, encoding=\"utf-8\").read()\nline = (\"- [ASD-STE100 это ручка, не сертификат](ste100-is-a-knob-not-a-certificate.md) — \"\n        \"⭐07.10 канарейк

---

> `Bash` -- {"command": "D=/c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_33a90300/scratchpad/ste; printf \"fmt-codex: %s байт\\n\" \"$(wc -c < $D/fmt-codex.md 2>/dev/null || echo 0)\"; grep -nE \"VERDICT\" \"$D/fmt-codex.md\" 2>/dev/null; tail -2 \"$D/fmt-code

---

> `Bash` -- {"command": "D=/c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_33a90300/scratchpad/ste; n=0; while [ $n -lt 10 ] && [ \"$(wc -c < $D/fmt-codex.md 2>/dev/null || echo 0)\" = \"0\" ]; do n=$((n+1)); python -c \"import time;time.sleep(10)\"; done; print

---

**Claude:**

Формат выжил: `VERDICT: BLOCK` на месте при включённой директиве. Дописываю замеры в заметку.

---

> `Bash` -- {"command": "cd /c/Users/dev/.claude/scripts && python - <<'PYEOF'\nimport io\np = r\"D:\\Vault\\Vault-Knowledge\\03-Insights\\Operations\\experiment-ste100-canary.md\"\ns = io.open(p, encoding=\"utf-8\").read()\nold = \"\"\"**grok без директивы:** чистых 52.0%, средняя длина 16.0, длинных 4, п

---

> `Bash` -- {"command": "cd /c/Users/dev/.claude/scripts && python - <<'PYEOF'\nimport io\np = r\"D:\\Vault\\Vault-Knowledge\\03-Insights\\Operations\\experiment-ste100-canary.md\"\ns = io.open(p, encoding=\"utf-8\").read()\nold = \"\"\"2. **Порог «80% как ASD-STE100» просьбой НЕ берётся.** Получили 56.7%.

---

> `Skill` -- {"skill": "tt", "args": "ste_score.py + ste_directive.md + llm_ask.py --ste (канарейка ASD-STE100)"}

---

**User:**

Base directory for this skill: C:\Users\dev\.claude\skills\tt

# /tt — ворота качества сразу после сборки

> 🧒 **При докладе оператору:** заверши простым «Простыми словами» на его языке (его standing-правило [[eli5-always]]). Только в сообщении ЕМУ — не внутри артефактов.

Это **не ретро**. Ретро = упаковка всей сессии в конце. `/tt` = узкая проверка **одной вещи, которую мы только что собрали**, пока контекст горячий. Боль оператора (2026-06-25): «собрали, сказали „готово", пошли дальше — а оно сделано на 2/3». `/tt` ловит это ДО «готово».

**Когда:** сразу после сборки/правки **скилла · скрипта · рутины · хука · vault-пайплайна · заметки-механики** — всего, что должно ЧТО-ТО делать. Не для разговорных ответов и не для тривиальных правок текста.

**Граница vs соседи:** `/1` = жива ли СИСТЕМА после крэша; `/verify` (встроенный) = работает ли ПРИЛОЖЕНИЕ в браузере; `/tt` = работает ли **именно то, что мы только что собрали**.

---

## Шаг 0 — RECALL области (что вообще изменили)
Не по памяти — по фактам. Перечисли, что эта задача реально создала/тронула:
- свежие/изменённые файлы: `~/.claude/skills`, `~/.claude` (память/CLAUDE.md/хуки/scheduled-tasks), `$IMPORTS_ROOT`, волт-заметки;
- быстрый якорь: `python "$IMPORTS_ROOT/retro_inventory.py" 1` (тот же инвентарь, что у /retro) ИЛИ просто перечисли то, что правил в ЭТОЙ сессии.
- Возьми только то, что относится к ТЕКУЩЕЙ задаче (чужие fleet-правки игнор — это не наше, см. [[session-machine-tagging]]).
- **RECALL знаний по теме** (гейт, грабли 2026-07-04: чинили OAI-путь не глянув память — чуть не продублировали параллельную сессию): перед прогоном/фиксом подними, что УЖЕ известно — grep `memory\` + `/ask` (RAG) + греп волта по теме изменённого. Параллельная сессия могла уже сделать/задокументировать это ([[capture-rules-into-bible]] → RECALL-before-activity).
- ⭐ **А ЭТО УЖЕ НЕ ПОСТРОЕНО? — ПРИБОРОМ, ДО ПЕРВОЙ СТРОКИ КОДА** (замер 03.09.2026): память, RAG и волт свежий чужой скрипт НЕ видят — он лежит в `~/.claude/scripts` и всё. Сессия собрала `tg_voice_translate.py`, хотя рабочий `tg_translate_3chats.py` уже сутки лежал в той же папке, а рядом был и третий, `tg_translate.py`. RECALL был сделан «честно» и промахнулся, потому что не обошёл поверхность с кодом.
```
python ~/.claude/scripts/prior_art.py build <2-4 слова задачи>
```
Обходит scripts · _imports · skills · hooks · memory, печатает СКОЛЬКО поверхностей и файлов обошёл (пусто = замеренное пусто, а не «я посмотрел»). exit 0 = чисто, строй · **exit 3 = есть готовое: прочти найденное в разделах `scripts`/`_imports` ПРЕЖДЕ чем писать своё**. Русский запрос по английским именам ловится — внутри мост RU→EN. Контрфакт-проверка на реальном промахе: готовый движок вышел бы 5-м в топе своей поверхности. Канон: память `class-counted-by-name-never-reaches-three` (там же семьи дефектов и почему счёт по имени не работает).

- **⭐ РЕЕСТР ДВЕРЕЙ: «семья доказана» = есть файл двери с красневшим тестом** (замер 01.10.2026, NODE-0X: утренний разбор назначил 4 двери, ни одного файла, вечером семьи повторились один в один). Если `/tt` закрывает разбор корней: на NODE-0X `python3 ~/lab/bin/door_ledger.py check` (exit 1 = у доказанной семьи нет файла двери, теста или красного лога → дверь строится в этом заходе, строка памяти дверью не считается); на других узлах прибора нет → строка «door_ledger: нет на узле, сверил руками: <семья → файл>».

- **⭐ Карта дверей [[three-tools-three-doors]]** (dev 09.08): АК-47 применяется на ОБОИХ концах — если спека НЕ прошла вопрос «слабейший починит молотком?» ДО стройки, это находка Шага 4, а не только брак приёмки. Чинится 3-й рецидив класса → сперва карта условий (`reglament-pyat-pochemu-koren-po-serii-sessiy`); очевидный фикс создаёт предъявленный вред → карточка противоречия (ТРИЗ), ⛔ до доказанной причины.

## Шаг 0-бис — СОБИРАЕШЬСЯ СКАЗАТЬ «НЕЛЬЗЯ»? СПРОСИ ИНСТРУМЕНТ

Срабатывает, если в вердикте вот-вот появится «невозможно», «нет такой ручки»,
«by design не поддерживается», «архитектурно нельзя» — или если ты готов
предложить оператору ручной шаг вместо автоматизации.

«Невозможно» — такой же claim, как вывод, и улика №1 не лог, а **собственный
интерфейс инструмента**. Пройди дешёвый круг снизу вверх, порядок не нарушать:

1. `<инструмент> --help` (и `-h`, и `help <подкоманда>`) — ПОЛНЫЙ список флагов,
   а не тот, что помнишь.
2. Подкоманды и их собственные `--help`.
3. Конфиг инструмента и переменные окружения.
4. Документация ТОЙ ЖЕ версии.
5. Только теперь логи, реверс бинаря, эксперимент.

Не прошёл круг — формулировка ровно одна: «я не нашёл, как это сделать».
Писать «этого не существует» без названного места поиска = вердикт максимум ⚠️.

⚠️ Ловушка, из-за которой правило родилось (10.09.2026, RC-факап): чем дороже
был путь к выводу, тем убедительнее он кажется. Сорок минут форензики по логам
приложения дали красивое доказанное «нельзя», а `claude --help` содержал
`--remote-control [name]` и закрывал задачу за пять секунд.
Дорогая улика НЕ отменяет обязанность пройти дешёвую.

⛔ **МОЛЧАЩИЙ `--help` — ЭТО ДЕФЕКТ ИНСТРУМЕНТА, А НЕ ОТСУТСТВИЕ ОТВЕТА.** Шаг 1
круга обязан ОТКРЫВАТЬСЯ: `--help` с ненулевым кодом, трейсбеком или «неизвестный
флаг» означает, что дверь канона заперта, и чинить надо её, а не искать обход.
Проверка одной строкой: `<инструмент> --help; echo $?` → не 0 = задача, не факт.

Практика: дверь `--help` не имеет права зависеть от библиотеки, про которую
спрашиваешь — usage печатается ДО тяжёлых импортов, иначе полу-правка соседа
уносит с собой и возможность спросить. Замер 21.09.2026 на NODE-0X: у
`deploy_register.py` `--help` давал exit 2 («неизвестный флаг»), у
`touchbase.py` — `TypeError` при импорте; обе рельсы месяц обходили руками,
потому что круг Шага 0-бис упирался в первую же ступень.

⛔ **ОБРАТНАЯ ЛОВУШКА (30.09.2026, NODE-0X): НАЙДЕННЫЙ ФЛАГ — ТОЖЕ CLAIM.** Круг выше
защищает от ложного «нельзя», но у него есть симметричный отказ: `--help` показал
подходящую ручку, и этого хватило, чтобы объявить «путь есть». `--help` доказывает
СУЩЕСТВОВАНИЕ флага, а не его ПРИМЕНИМОСТЬ к нашим данным. Поэтому флаг, на который
опирается вердикт, план или текст сида, обязан быть проверен ВЫЗОВОМ на наших данных
в том же заходе — иначе пишем «флаг есть, на наших данных не проверен».

Замер, породивший поправку: сид 29.09 объявил claim «codex-рельса лечится только руками
оператора» протухшим, потому что `codex login --help` несёт `--with-access-token`. Флаг
действительно есть — но ждёт «agent identity JWT», и на честном ChatGPT OAuth access
token отвечает `agent identity JWT payload is not valid JSON`. Токен при этом доезжал
целым (1888 байт, 3 части JWT, payload парсится), то есть транспорт был ни при чём, и
без живого вызова ошибку было НЕ отличить от битой передачи. Настоящий headless-путь
оказался другим (файл `auth.json` с пустым `refresh_token`).

Канон: `reglament-sprosi-instrument-pered-tem-kak-obyavit-nevozmozhnost`
+ память [[ask-the-tool-before-declaring-impossible]], [[prichina-kak-claim]].

## Шаг 1 — ПРОГНАТЬ вживую (на реальных данных, не в теории)
Запусти собранное **по-настоящему** на настоящих данных оператора и покажи фактический вывод:
- скилл → выполни его процедуру руками здесь же;
- скрипт → запусти его (read-only/dry-run если есть побочки);
- рутина/хук → дёрни вручную или проверь, что он реально срабатывает (а не «должен бы»);
- заметка-правило → проверь, что ссылки/слаги резолвятся, frontmatter валиден.
«Теоретически работает» ≠ доказано. Нужен живой вывод.
- ⚠️ ТЕМ ЖЕ ИНТЕРПРЕТАТОРОМ/БИНАРЁМ, каким пойдёт у ПОТРЕБИТЕЛЯ (планировщик/рутина/другой узел), не «каким попало из PATH»: класс «PATH резолвит не тот питон/бинарь» кусался 11.08 (258 ложных падений регресса), 12.08 (две установки CC), 13.08 (gdocs_bridge: google-либы только у 3.12 из 5 питонов), 19.08 (brain_ask месяцами красный не тем питоном). Сомнение → напечатай `sys.executable`/`py -0p`/`which` и сверь с вызовом потребителя (Breakage-Journal, task-2026-08-13-python-path-class-repair).

## Шаг 2 — ПОЛОМАТЬ нарочно (negative + edge)
Попробуй сломать — реальные грабли этого дома:
- пустой / кривой ввод, отсутствует зависимость или ключ;
- грабли путей **C:/E:** ([[deterministic-script-gotchas]]) — ищет ли на правильном диске;
- машинно-специфичный хардкод: `grep -n "C:\\\\Users\\\\dev" <файл>` — путь с ЧУЖИМ юзером/машиной в общем движке обязан идти через `_paths.py`/machine.env (грабли 2026-07-04: хаб вшил `C:\Users\dev`, на ноуте путь мёртв → тихий fallback);
- v2.1 / 403 / устаревший конфиг — берётся ли факт из ЖИВОГО источника, не со стале-копии ([[recall-first-on-incident-and-live-source-truth]]);
- деградирует ли мягко (понятная ошибка), а не падает молча/тихо «делает вид»;
- ⭐⭐ **СОБРАЛ МЕТРИКУ/СКОР/ЛИНЕЙКУ → СПРОСИ У НЕЁ ЕЁ МАКСИМУМ** (замер 30.09.2026, T10 второй памяти): выпиши теоретический диапазон величины и добавь кейс на выход за него. `nDCG@12` выдавал **1.6309 при математическом максимуме 1.0**, потому что засчитывал одно и то же золото дважды, когда стем попадал в выдачу повторно (две заметки с одним именем в разных папках, а wikilink адресует ПО ИМЕНИ). 78 зелёных тестов дефект не видели: все проверяли метрику на данных без дубля. Нашли ЧУЖИЕ глаза за минуту, и это уже после мержа модуля — значит прибор идёт на панель Шага 2.5 раньше, чем его числа уходят наружу. ⚠️ Мутант-флаг тут не спасает: он ловит «метрика сломана», а не «метрика сломана в разрешённую сторону». Второй вопрос той же двери: по какому КЛЮЧУ метрика отождествляет объекты (имя файла? путь? id?) — ключ по имени делает коллизию не краем, а вторником. Не проверил диапазон → вердикт максимум ⚠️. Канон: [[metric-can-exceed-its-own-maximum]], [[instrument-is-a-claim-too]].
- ⭐⭐ **ЛЮБАЯ ПОЧИНКА, а не только сторож, закрывается ТЕСТОМ, ПОКАЗАННЫМ КРАСНЫМ** (CLAUDE.md §5.4 [[red-first-or-the-test-is-fake]]; дверь достроена 03.09.2026 — до этого шаг ниже требовал красноты только у СТОРОЖЕЙ/гейтов, а правило в каноне универсально, и обычный код закрывался «на глаз»). Порядок: сперва проверка на НЕчинёном коде и её падение ПОКАЗАНО (номер кейса + exit 1), потом починка, потом зелёный. Ломать — на КОПИИ, живые файлы не портить, и это делается ПРИБОРОМ, а не дисциплиной: `python ~/.claude/scripts/red_proof.py --file <боевой> --old '<строка>' --new '<строка>' --expect-fail '{py} {f} selftest'` (копирует в temp, ломает копию, требует ≠0, печатает md5 боевого файла до/после; `--old-file`/`--new-file` для многострочных шаблонов и обратных слешей, `--also <тест>` если тест импортирует цель по имени модуля). exit 0 красное доказано · 1 проверка ПРОШЛА на сломанном = тест фальшивый · 2 шаблон найден не ровно один раз (тихая осечка ломателя). ⚠️⚠️ **И ЧИТАЙ ЭТОТ КОД БЕЗ ПАЙПА.** `$?` после `| tail`/`| head` принадлежит ПОСЛЕДНЕЙ команде конвейера, а не прибору: `python -c "import sys; sys.exit(3)" | head -1` даёт `$?=0` при фактическом 3. Замер 06.10.2026: три разные сессии за один вечер наступили на это в один вечер — у меня `red_proof` печатал «КРАСНОЕ ДОКАЗАНО», а `echo $?` показывал 0, и дважды наоборот: `echo rc=$?` после пайпа объявлял провал успехом. Правило: код возврата берётся ЛИБО без пайпа, ЛИБО через `${PIPESTATUS[0]}`, ЛИБО вывод сперва в файл, а потом читается. Класс `pipe-eats-the-exit-code`. ⚠️ ЗАМЕР 05.10.2026, почему тут прибор, а не доверие: правило «на копии» стояло в этой строке с 03.09, и за ОДИН вечер три сессии над одним `session_pusher.py` нарушили его 11 раз (8 циклов `cp/sed/mv` у одной + 3 у владельца файла). Цена: `mv` восстановил снимок, снятый ДО чужой починки, и молча откатил уже проверенную правку другой сессии — проверенный результат пришлось доказывать заново. Брейк-кейс остаётся в `_test_*.py`. Контр-кейс обязателен: хотя бы одна проверка, зелёная С САМОГО НАЧАЛА, иначе сетка красит всё подряд и ничего не доказывает. Нет предъявленного красного прогона → вердикт максимум ⚠️, «я посмотрел глазами» красным прогоном не является.
  - ⛔ **СПЕРВА СПРОСИ, СПОСОБЕН ЛИ ВЫБРАННЫЙ ПРИБОР УВИДЕТЬ ЭТОТ КЛАСС.** Прибор, зелёный на заведомо сломанном коде, даёт фальшивую сетку, которую потом предъявляют как доказательство.

    Замер 21.09.2026: под класс «py39 падает на `int | None`» просился `python -m py_compile` — но PEP 604 синтаксически валиден и в 3.9, падение происходит при ИСПОЛНЕНИИ модуля. Сетка была бы зелёной на всех мёртвых рельсах. Дискриминатор пришлось строить по AST + позиции аннотации (`scripts/py39_union_lint.py`).

    Тест самого прибора: прогони его по файлу, про который ТОЧНО знаешь, что он сломан. Молчит — значит мимо класса.
- ⭐⭐ **КРАСНОТУ ДОКАЗЫВАЕТ ПРИБОР, А НЕ ТВОЙ ГЛАЗОМЕР** (замер 04.09.2026, семья `neizvestnyy-flag-molcha-rabotaet` — 13 датированных случаев с 11.08): краснота трёх кейсов «проверялась» цепочкой `python test.py --flagA || python test.py --flagB`. Первый вызов шёл с ЧУЖИМ флагом, тест проглотил его молча (`"--red" in sys.argv` — членство, не разбор), отработал ЗЕЛЁНЫЙ набор, вернул 0, и `||` до правильного вызова не дошёл. Вывод «красный прогон показан» описывал команду, которая не запускалась.
  ```
  python ~/.claude/scripts/red_verify.py <test.py> --red-flag --against-broken-<чей>
  ```
  Три замера, ни один не пропускается: **канарейка строгости** (мусорный флаг обязан дать ≠0 — иначе скрипт глотает аргументы и его красный режим недоказуем в принципе), **зелёный 0**, **красный ≠0**. exit 0 доказано · 3 недоказуемо · 4 сам прибор не сошёлся на контрольном примере. ⛔ **Отказ запуститься (exit 2) краснотой НЕ является** — прибор ловил на этом сам себя на живом прогоне. Лечение недоказуемого теста — `_shared/strict_argv.py` (одна строка `strict(["--red"])` до любой работы; публичным артефактам — 6-строчная inline-копия, чтобы репо оставалось stdlib-only).
  ⭐ **У FAIL-CLOSED ГЕЙТА — МУТАЦИОННЫЙ ЗАМЕР, а не «тесты зелёные»** (замер 10.09.2026, процедура скилла `/red-first-review`): глуши по одной КАЖДУЮ его защиту и гоняй набор. Тест зелёный на мутанте = защиту можно удалить, и никто не заметит; именно она регрессирует молча. Живой результат на нашем leak-гейте касбука: **выжило 5 из 8** — сносились список имён людей, заимствованные паттерны, страховка по имени класса и САМ `control_sample`, все 14 тестов оставались зелёными. По ходу вскрылось, что заимствование паттернов у зрелого сканера было сломано молча (`getattr(rls,"PATTERNS",[])` при списке `FAIL` — тихий дефолт вернул пустоту, «мы берём зрелый сканер» было неправдой шесть дней). После кейсов-убийц: 8 из 8. Образец = `~/.claude/scripts/_mutate_casebook_gate.py`. ⚠️ Мутант обязан РЕАЛЬНО ломать защиту: `X = [] or [...]` возвращает НЕПУСТОЙ список, и два «выживших» оказались артефактом кривой мутации — проверяй саму мутацию, прежде чем верить её вердикту.

  ⚠️ **СЕРИЮ мутантов гоняй с `PYTHONDONTWRITEBYTECODE=1`.** `__pycache__` инвалидируется по (mtime, size), поэтому мутации в пределах одной секунды проходят проверку насквозь, и следующий мутант показывает провалы ПРЕДЫДУЩЕГО.

  Замер 21.09.2026: мутант B отдал профиль мутанта A, а изолированно был зелёным — я чуть не «починил» здоровую проверку.

  Ловец: мутант обязан убивать ровно СВОЮ проверку; валит чужие — либо назван неверно, либо прогон грязный. Контрольный прогон на восстановленном оригинале в конце обязателен [[mutant-runs-need-dontwritebytecode]].
  ⚠️⚠️ **И отдельно проверь, что УТВЕРЖДЕНИЕ проверки про то, что поломка МЕНЯЕТ.** Кейс краснеет, только если его `assert` смотрит на величину, которую ломатель двигает; иначе проверка вакуумна с рождения и красным прогоном это НЕ видно. Замер 06.10.2026, один файл `retro_x_post.py`, один вечер, **5 случаев**: (1) поломка влияла на подсказку, а проверка сторожила ВЕРДИКТ -> GREEN; (2) проверка искала в выводе `bug x` с пробелом, а код печатает `bugsx1` -> вакуум с момента написания; (3) три гарантии (границы слова, склейка emoji, печать слепой зоны) не сторожились вовсе -> 39/39 GREEN на всех трёх поломках; (4) проверка «CLI печатает длину» искала `280`, то есть сам `X_LIMIT`, который в строке есть ВСЕГДА -> подмена длины на 0 оставляла 66/66 GREEN; (5) поломка «выключить склейку emoji» на ОДИНОЧНОМ смайлике недоказуема, потому что со склейкой и без неё ответ одинаков (2) -- доказывают флаг (2 против 4) и семья (2 против 11). Рабочее правило: **ломатель и утверждение обязаны называть РАЗНЫЕ числа**, иначе кейс не исполняет путь. Сверяй внутренний счётчик напрямую (`_word_counts(...) == {"bugs": 1}`), а не подстроку в человекочитаемом тексте: формат меняется, и проверка тихо умирает. Печать проверяй перехватом stdout, а не чтением словаря. ⛔ И не ломай руками там, где достаёт `red_proof.py`: его **exit 2** («шаблон найден не ровно один раз») -- это ровно случай «поломка не применилась, а GREEN выглядит гарантией», и в тот же вечер я прошёл мимо прибора и поймал этот случай руками [[fake-check-is-worse-than-no-check]].
  ⚠️ И проверь, что краснеет КАЖДЫЙ кейс, а не файл целиком: красная ветка обязана ломать ОБЪЕКТ (подменить фильтр, движок, загрузчик), а не стирать провал теста (`if RED: missed = []`). Общий exit 1 от одного честного кейса маскирует соседей, которые не краснеют никогда — так 04.09 в одном файле два кейса из трёх молча проходили красный режим [[kill-list-makes-tests-checkable]].
- ⭐ артефакт = СТОРОЖ/гейт/пробник → ДВОЙНОЕ доказательство обязательно (dev «+++» 05.08, Библия `reglament-storozh-krasneet-na-slomannom-i-zhivyot-v-svoyom-kontekste`): (1) RED на заведомо сломанном показан, и брейк-кейс ОСТАЛСЯ в `--self-test`/`_test_*.py`; (2) прогон В КОНТЕКСТЕ проживания — из планировщика/cron (`schtasks /Run` / вызов crontab-строки) + чтение его ВЫХОДА (лог/артефакт), не из живой сессии. Замер 05.08: session_reaper 15 зелёных прогонов из Task Scheduler при живой аварии (MSIX-редирект). Нет любой половины → вердикт максимум ⚠️;
- ⭐ **чинил ВЫБОР/маршрутизацию (движок, вендор, модель, рельса, путь) → провокация обязана бить и ветку УМОЛЧАНИЯ, не только явную ошибку.** Вызови артефакт БЕЗ параметра выбора и докажи, что дефолт — тот, что заявлен (панель/None/явный отказ), а не тихий первый вендор. Замер 04→06.08: тест рельс secondop на 13 пунктов сторожил только явный `--engine`, ветка «движок не назван → молча codex» жила при зелёном тесте, нашёл оператор («почему только кодекс??»). У поломки выбора ВСЕГДА две двери: «назван неверно» и «не назван вообще» — закрыл одну, проверь вторую (паспорт `scripts/docs/secondop_rails.md`, проверки 8/8b/8c);
- ⭐ **РАЗНЫЕ РИТМЫ ПРОИЗВОДИТЕЛЯ И ПОТРЕБИТЕЛЯ → провоцируй ГЭП, а не «здесь и сейчас»** [[consumer-stamp-not-collector-stamp]]. Если сборщик бегает чаще потребителя (или наоборот), а потребитель читает «самый свежий» файл — подделай штамп/дату на длину пропуска и докажи, что окно РАСТЯНУЛОСЬ, а не осталось дефолтным; отдельно проверь недоставку (окно обязано копиться, а не пропадать) и потолок догона. Замер 30.08: сборщик ежедневный + судья раз в 2 суток = каждая вторая ночь клуба молча не доезжала до оператора, при этом ВСЕ приборы зелёные (каждый мерил свой шаг, а не сквозной путь данных); нашла панель Шага 2.5, живой прогон этот класс не ловит в принципе.
- ⭐ **ДЕТЕКТОР СУДИТ ПОДСТРОКУ, А НЕ СТРУКТУРУ** [[gate-must-judge-action-not-substring]] — прогон ОБЯЗАТЕЛЕН, если правка трогает гейт/сторож/фильтр/precheck/тест:
  `python3 ~/.claude/scripts/substr_lint.py <изменённые файлы>` (0 токенов, stdlib; exit 1 = находки).
  Шесть правил: R0 файл не разобрался → зелёный по нему ничего не значит (fail-closed) · R1 `"<короткое
  слово>" in <текст>` без границы · R2 regex-альтернатива голых слов без `\b` · R3 `grep` по выводу
  структурированного источника (JSON/YAML/py — слово может быть КЛЮЧОМ, а не значением) · R4 флагом
  `--md` — текстовое правило по заметке без отрезания YAML-шапки · **R5 вердикт по СЫРОЙ команде
  харнеса** (`tool_input["command"]` целиком уходит в матчер) → спроси `_shared/cmd_action.executed_text`:
  команда ЗАПУСКАЕТ сторожимое или лишь УПОМИНАЕТ его в данных. Находка = Шаг 4 (корень), либо
  ОСОЗНАННЫЙ глушитель `# substr-ok: <причина>` (голый маркер без причины не глушит).
  ⭐ **ПОПУЛЯЦИЯ, А НЕ АДРЕСАТ ИЗ РУК** (замер 03.09, разбор 22-го случая): у двери был ОДИН вызыватель —
  этот шаг по «изменённым файлам», счётчик показал 12 прогонов за 15 суток и только на хабе, поэтому
  10+ новых случаев родились в гейтах, которых никто в тот заход не правил. Правишь ЛЮБОЙ гейт/хук →
  добавь `python ~/.claude/scripts/substr_lint.py --roster` (живая перепись hook-файлов из settings.json
  + их `_shared`). Без рук это же сторожит ночная сетка: `_test_hook_roster_substr.py` (храповик —
  красный только на РОСТЕ долга, старый долг зафиксирован пер-узловой базовой линией).
  ⛔ **ПЕРЕПИСЬ — ТОЖЕ CLAIM, И ЕЁ ЧИСЛО НАДО ЧИТАТЬ** (замер 04.09, 23-й случай — дефект нашёлся
  В САМОЙ ДВЕРИ): `--roster` печатает «живых hook-файлов: N». Сверь N с `settings.json` глазами
  ОДИН раз. До 04.09 пути тянул regex по ВИДУ пути (требовал начала `C:\`, `$HOME/`, `%USERPROFILE%/`,
  `~/`), голый POSIX-абсолют `/Users/dev` не матчился: на NODE-0X из 39 команд попадали 3, перепись
  говорила «17» вместо 64, и вне неё были ровно рецидивисты класса — `blackbox_session_guard.py`
  (сломался дважды за утро 04.09), `maintenance_gate.py`, `false_no_guard.py`. Ночной храповик при
  этом был зелёным на базовой линии «1 находка» при реальном долге **43 находки в 16 гейтах (25%
  популяции)**. Урок общий: у сторожа с ПОПУЛЯЦИЕЙ доказывают не только вердикт, но и ПЕРЕПИСЬ —
  пустая или куцая популяция даёт зелёный, неотличимый от честного [[instrument-is-a-claim-too]].
  Замер 19.08: класс дал **5 датированных поломок за 8 дней** — 11.08 `"да"` внутри «со**зда**ём» увело
  приватную запись в `visibility: public` · 14.08 «является» внутри «появляется» · 18.08 «не **пост**авка»
  в ЗАГОЛОВКЕ сняла живой пост с публикации (SKIP не красный) · 19.08 `grep -E "dispatch|collect|deliver"`
  по JSON, где это КЛЮЧИ → 7 часовых тиков подряд будили LLM впустую. Шум двери замерен: **5.3% файлов
  на корпусе 1117** — это дверь, а не вечно красный сторож [[always-red-watchdog-teaches-ignoring-red]].
  ⛔ ГРАНИЦА (АК-47, не превращать каждый grep в парсер): структурный разбор обязателен там, где источник
  структурирован **И** вердикт что-то ГАСИТ (skip/block/publish/будить LLM); над плоским человеческим
  текстом, где ложный хит виден и дёшев, grep остаётся правильным решением. Тест: `_test_substr_lint.py`;
- ⭐ **СТАТУС-CLAIM БЕЗ УЛИКИ: ✅ рядом с именем файла** [[prichina-kak-claim]] — прогон ОБЯЗАТЕЛЕН,
  если в области Шага 0 есть НАРУЖНЫЙ док (README / INSTALL / отчёт / паспорт / пост) или черновик, писанный агентом:
  `python ~/.claude/scripts/status_claim_lint.py <файлы>` (0 токенов, stdlib; exit 2 = находки).
  Судит СТРУКТУРУ, не подстроку: ✅ в пределах 80 символов от имени файла → файл ищется на диске
  в НЕСКОЛЬКИХ корнях (§5.4 check-all-places), вердикт = «НЕ ПОДТВЕРЖДЁН + где искал», не «файла нет».
  Починка находки: приложи улику (`ls`/цитата) ЛИБО замени ✅ на 🤔 ЛИБО осознанный `status-claim-ok: <причина>`
  (голый маркер не глушит). Замер 29.08: класс дал **3 датированные поломки** (10.08 панель ревьюит
  непрочитанный файл · 13.08 панель судит вырожденный контекст · 14.08 draft-агент подал несуществующие
  `package_verify.py`/`quarantine_lite.py` как установленные ✅). Шум двери замерен: **3.5% файлов на корпусе 200**
  (было 1334 находки до структурного порога — это был бы вечно-красный сторож).
  Входная половина того же класса стоит сама: `secondop` EVIDENCE RULE + 5-я строка сид-блока 🔍 УЛИКА.
  Тест: `_test_status_claim_lint.py`;
- ⭐ **EXIT-КОД ПОСЛЕ ПАЙПА — НЕ ТВОЙ КОД** (класс `exit-code-eaten-by-pipe-grep`, **4 датированных
  случая**, сессия починки 05.10.2026). Тронул шелл-файл (`.sh`/`.bash`/`.cmd`/`.bat`) — прогони
  `python ~/.claude/hooks/pipe_rc_guard.py --files <изменённые файлы>` (0 токенов, stdlib; **exit 2 = находки**).
  Дефект: `$?` после пайпа — код ПОСЛЕДНЕЙ ступени, а не твоей команды, и врёт он в самую
  опасную сторону — СПОКОЙСТВИЕМ. Замер 05.10: `python -c "sys.exit(3)" 2>&1 | tail -1; echo $?` → **0**,
  прямой запуск того же → **3**; а `if cmd | grep -nE X | head -10; then` истинно ДАЖЕ БЕЗ СОВПАДЕНИЙ.
  Цена класса: 27.07 гейт утечки физически не мог судить → секрет уехал в ПУБЛИЧНЫЙ репо; 31.07 на NODE-0X
  `install.py | tail -5 && deploy_apply.py` записал DONE при exit 127 на голове (установки НЕ БЫЛО, а флот
  покрасился зелёным); 27.09 `ssh ... | grep -v WARNING` дал сторожу exit 0 по ЧУЖОМУ коду.
  **Главная дверь класса — не этот шаг, а PreToolUse-хук** `pipe_rc_guard.py` на каждый Bash-вызов
  (settings.json, matcher `Bash|PowerShell`): три из четырёх случаев родились не в файле, а в живом замере,
  где линтер по файлам не стоит на пути вообще. Отказ хука = exit 2 + причина в stderr.
  Починка находки — одно из трёх: (1) не пайпить ту команду, чей код читаешь; (2) `set -o pipefail`;
  (3) `${PIPESTATUS[0]}` вместо `$?`. Осознанный обход — `# pipe-rc-ok: <причина>` (голый маркер не глушит).
  Судит ПОТРЕБЛЕНИЕ кода, не пайп сам по себе: `cmd | head -30` без `$?` и `| grep -q X` как тест
  пропускаются молча. Шум замерен: **0 находок на корпусе 360 шелл-файлов** `~/.claude` (единственная
  находка оказалась формой `|| true` — явным отказом от кода, и детектор сужен под неё, а не
  заглушён маркером). Честные пробелы названы в docstring: PowerShell не судится · плоский `grep`
  последней ступенью пропускается · пайп внутри `$( )` не судится.
  Почему ДВЕРЬ, а не ещё одна запись: правило стояло дословно с 27.07 в ДВУХ домах памяти,
  с названной ценой — и не остановило НИКОГО, включая того, кто его писал (§8.6: правило без
  вызывающего принято, но НЕ РАБОТАЕТ). Ловит и `|&` (= `2>&1 |`), и `grep -v` по полному пути,
  и `var=$(пайп); echo $?` — все три нашла break-панель (codex+grok) как ЛОЖНОЕ ЗЕЛЁНОЕ уже после
  сборки; `|&` пропускал ровно исторический случай 27.09. Тест: `~/.claude/hooks/_test_pipe_rc_guard.py`
  (26 проверок, краснота доказана ТРЕМЯ поломками → 12 / 2 / 2 провала); память [[deterministic-script-gotchas]];
- ⭐ **метрика-ДОЛЯ/отношение → сверь ЕДИНИЦЫ числителя и знаменателя** [[measurement-units-must-match]].
  Правка строит или трогает долю/процент/сравнение двух рельс записи? Выпиши, что физически
  означает ОДНА строка КАЖДОЙ рельсы. Разные единицы (событие хука vs подъём процесса vs
  сессия) → доля врёт молча. Замер 13.08: доля Firefox 9 дней сравнивала подъёмы драйвера
  с MCP-кликами (1.6% сырая vs 7.6% честная); ТРИ внешних ломателя не поймали — каждый
  смотрел свою рельсу порознь, сравнение единиц не проверял никто;
- ⭐ **фолбэк метрики: рапорт можно, ДЕЙСТВИЕ нельзя** [[fallback-metric-ok-to-report-never-to-act]].
  Найди в правке каждое место «честный измеритель молчит → беру соседний похуже» и посмотри,
  что стоит НИЖЕ по потоку: `print` — ок, `kill`/`send`/`write`/`commit` — дыра.
  Прогон: `grep -nE "or 0\b|except.*:\s*$|is None|not .*_map|fallback" <файл>` и глазами по хитам.
  Замер 04.08: обещание «судим только по дельте» жило в docstring и 54 зелёных тестах, а
  отменяла его ОДНА строка фолбэка на `ps %CPU` — нашёл внешний ломатель, не тесты.

## Шаг 2.5 — ВТОРОЕ МНЕНИЕ: ⭐ПАНЕЛЬ, все рельсы ОДНОВРЕМЕННО (приказ оператора 05.08.2026)

**Дефолт с 05.08 — одна команда, четыре пары глаз разом:**
```
python "%USERPROFILE%\.claude\scripts\cc-review\secondop.py" panel --ritual tt --task <id> --context "<что собрали + что проверили>"

⛔ **СУБАГЕНТЫ CLAUDE ПАНЕЛЬЮ НЕ ЯВЛЯЮТСЯ** (замер 24.09.2026): прогнал 128 агентов через Workflow, получил 40 настоящих находок — и при этом рельсы codex/grok не вызывались ни разу, чужой оплаченный бак не горел, а `rail_plan.py verdict` честно показал ноль. Это отличные ВТОРЫЕ глаза, но того же вендора: одна модель — одни слепые пятна. Панель = ЧУЖИЕ рельсы (`secondop.py panel`); субагенты идут сверх неё, а не вместо. Рельса не отвечает — так и пиши «рельса мертва, причина» (24.09: `codex exec` отдал 401, refresh token отозван), а не «панель прогнана».

⭐⭐ **ПАНЕЛЬ СУДИТ ПОЧИНКУ, А НЕ ИСХОДНУЮ ЗАДАЧУ** (замер 04.09.2026). Чинил корень — в `--context` кладёшь КОД ПОЧИНКИ и список «что я объявил закрытым», а в `--task` пишешь «сломай ЭТИ починки». Зелёная СВОЯ приёмка доказательством не является: 21 корень был зелёным локально и на сервере, после чего панель из 8 движков нашла в тех же починках **8 дефектов**, из них три назвали ≥2 движка независимо (маркер готовности удовлетворялся текстом прошлого отчёта · порог размера добивался сайдбарными ссылками · fail-closed гейт оказался fail-open по состоянию ПРЕДКА элемента). Сходимость ≥2 движков = чинить не думая; одиночное наблюдение = проверять уликой. И сетку, написанную НА находки панели, гони мутантами отдельно: её первая версия пропускала 4 из 8 мутантов, потому что смотрела на возвращаемый текст, а починки меняли время и сообщение ([[red-first-or-the-test-is-fake]], [[panel-broke-my-own-fix]]).

⚠️ ЛИМИТ КОМАНДНОЙ СТРОКИ (замер 17.09, T09): `--context` уезжает АРГУМЕНТОМ, файлового флага у `secondop.py` нет, и на Windows контекст >32 КБ падает с `Argument list too long` ещё ДО вендоров. Класть весь файл нельзя: резать до ГОРЯЧИХ функций (у T09 влезло 13.6 КБ = схема + закрытие + sync + apply_order + врезка) — и это не отмена правила ниже, а его форма.

⭐ РЕЦЕПТ НАРЕЗКИ (T10, 30.09.2026 — врезка про лимит стояла, а КАК резать не говорила, и заход ушёл на угадывание): пиши launcher-файлом, а не строкой в шелле. Функция `hot(path, start_marker, end_marker, limit)` берёт кусок исходника ОТ имени функции ДО имени следующей, куски склеиваются с заголовками «=== файл — что это (LIVE CODE) ===», в конце блок «=== WHAT I ALREADY CHECKED ===» одним абзацем. Перед запуском печатай `len(context.encode("utf-8"))` и держи ≤ 16 КБ: у T10 влезло 10 223 байта = метрики + раннер + сборка gold + вынесенные ступени конвейера, и панель на этом нашла дефект метрики. Маркеры — ИМЕНА ФУНКЦИЙ (`def ndcg_at(`), не номера строк: номера съезжают от любой правки выше.

⭐ В `--context` кладём ПЕРВОИСТОЧНИК — живой код горячих участков (или файлы целиком), не свой пересказ; пересказ допустим лишь как навигация поверх. Замер 20-21.08: панель на пересказе — точность 25% (2 из 3 ложных находок выросли из формулировок пересказа), та же панель на живом коде — 10/10. Находки панели — гипотезы: каждую сверить с первоисточником, в отчёт обе колонки (принято/опровергнуто с уликой). Канон: Библия `reglament-proveryayushchemu-pervoistochnik-ne-pereskaz` + память [[panel-judges-my-spec-not-the-code]].
```
Codex, Grok и Gemini идут ПАРАЛЛЕЛЬНО (каждый своим процессом). ⭐⭐ **С 28.09.2026 БРАУЗЕРНУЮ НОГУ ДВИЖОК ОТКРЫВАЕТ САМ** (`dr_ff_rail`, профиль AutoFF): порядок = CLI-подписки → **браузерные подписки** → OpenRouter (поштучная оплата последней, §6.3). Флаг `--browser-exec auto|always|off`, дефолт `auto` = браузер включается, когда CLI дал <2 независимых семей. ⚠️ Кворум считается по СЕМЬЯМ, и **своя семья (`anthropic`) в независимость не идёт ни одной дверью** — панель нужна ради ЧУЖИХ слепых пятен. Вендор без исполнителя (grok.com, deepseek) остаётся ручным: он и называется РУЧНЫМ, добивается через `log-ext`. Повод правки: класс `foreign-review-rails-all-dead` — 23/25/27.09 три раза подряд «чужих глаз не получить», и все три раза пробовалась ОДНА поверхность (CLI), потому что ручной шаг «открой вкладку» в безлюдном прогоне делать некому. Контрфакт 28.09 на одной и той же заявке: CLI-only → rc 3 (1 семья), с браузерной ногой → rc 0 (2 семьи, у GLM находки поверх grok). Тест `_test_secondop_browser_leg.py`. Код выхода `3` = независимого второго мнения нет (ответил один) → вердикт `/tt` максимум ⚠️. Порядок «сначала Codex, потом остальные» отменён: на практике он означал «только Codex» (замер 05.08: Grok $300/мес выбран на 12%). Паспорт: `scripts/docs/secondop_panel.md`.

Ниже — механика ОДИНОЧНЫХ рельс: она жива и нужна, когда панель избыточна (одна мелкая правка) или когда чинишь конкретного вендора.

### Одиночные рельсы (частный случай)
Своя проверка слепа к своим же слепым зонам — второй вендор ловит то, что мы не видим ([[test-after-build-skill]] + Decision Memo Phase 1.5). Поэтому ломает не только сессия, но и внешние глаза. Их ТРИ пары (dev 21.07; ⭐26.07 Grok переехал в CLI; ⭐27.07 добавлен Gemini): **Codex** (headless CLI, дефолт), **Grok** (⭐26.07 на хабе локальная CLI-рельса на подписке, headless — `secondop.py t3 --engine grok`; браузер grok.com = ФОЛБЭК, см. [[grok-second-reviewer-rail]]) и **Gemini** (headless без браузера, `gemini_review.py break`, см. [[gemini-third-reviewer-rail]]).

**Когда зову (узко, чтобы ритуал не раздуло):** в области Шага 0 есть изменённый **исполняемый** артефакт (скрипт · скилл · хук · рутина · пайплайн). Только заметки/тексты/frontmatter → пропускаю **осознанно**, логирую и пишу это в вердикт.

**Рельса 1 — Codex (дефолт, зову всегда первым):**
```
python "%USERPROFILE%\.claude\scripts\cc-review\secondop.py" t3 --ritual tt --task <id-задачи> --context "<что собрали + что уже проверили в шагах 1-2>"
```
Пир без Codex-логина → тот же вызов через `_shared\secondop_client.py` (брокер ответит по шине).

**Рельса 2 — Grok-ломатель (зову когда):** (а) Codex недоступен/quota-blocked — Grok спасает вердикт от ⚠️; (б) артефакт рискованный/safety-critical или Codex дал спорный COUNTER — гетеро-пара, зову ОБОИХ; (в) оператор сказал «спроси грока».
**Механика-дефолт (⭐26.07, хаб): локальный CLI headless** — `python ...\secondop.py t3 --engine grok --ritual tt --task <id> --context "..."` (лог и зеркало в чат 04 автоматические, ручной log-ext НЕ нужен). CLI мёртв/разлогинен (`secondop.py doctor` — ⚠️ не `grok doctor`: такой подкоманды у grok НЕТ, проверено 04.08, в `grok --help` 13 команд и doctor среди них нет; exit 0 = обе рельсы живы · 3 = вендор установлен и не отвечает ЛИБО рельс нет вовсе · 1 = канон обещает подкоманду, которой в движке нет) → **фолбэк-браузер** (Chrome-MCP, человеческий темп, как /dr-fanout; строго локальный браузер [[browser-work-on-peers-not-hub]]):
1. `python ...\secondop.py grok-prompt --task <id> --context "<что собрали + что проверили>"` → paste-ready промпт;
2. вставить в НОВЫЙ чат grok.com (обычная модель, Expert не трогать), дождаться ответа;
3. первая строка ответа = вердикт `ACCEPT`/`COUNTER`/`BLOCK`;
4. залогировать: `python ...\secondop.py log-ext --reviewer grok --task <id> --ritual tt --verdict "<1-я строка>" --note "<ссылка grok.com/c/… ПЕРВОЙ + суть находок>"`. Ссылка на чат в `--note` **обязательна и идёт первой** (note режется до 200 симв. — длинная преамбула съест ссылку, Grok COUNTER 21.07) — это доказательство, что вердикт реально от Grok, а не вписан рукой (Codex VERIFY 21.07); плюс ответ Grok целиком цитируется в вердикте /tt. Не распознан формат → вердикт НЕ засчитан (переспросить в формате или log-skip).

**Рельса 3 — Gemini-ломатель (⭐27.07, скилл `/gemini`; зову когда):** (а) Codex И Grok недоступны/выжгли квоту — Gemini спасает вердикт от ⚠️; (б) safety-critical артефакт или спорный COUNTER — зову третьим голосом; (в) оператор сказал «спроси джемини».
```
python "%USERPROFILE%\.claude\scripts\cc-review\gemini_review.py" break --task <id> --context "<что собрали + что проверили>"
```
Headless, без браузера (REST-рельса ~7-10 с; `--engine cli` = `@google/gemini-cli`). Вердикт первой строкой `ACCEPT`/`COUNTER`/`BLOCK` и **сам** пишется в `usage.jsonl` (`log-ext --reviewer gemini`) — ручной log-ext НЕ нужен. Рельса не ответила → скрипт сам пишет `log-skip` и выходит с кодом 3 (вердикт /tt тогда максимум ⚠️ PARTIAL). Ключ = бесплатный тир Google AI Studio (`secrets\gemini.env`), биллинга нет → превышение = 429, не счёт; ⚠️ OAuth-вход CLI для физлиц Google отключил — чинить бесполезно, живёт только API-ключ.

**Как читать ответ (всех трёх рельс):** `COUNTER`/`BLOCK`/сценарии поломки = **находка** → это Шаг 4 (корень → починить → перепрогнать), не «мнение к сведению». `ACCEPT` = согласие, находки нет. Достаточно ОДНОГО полученного внешнего вердикта; вторая пара глаз — по правилам рельсы 2.

**Рельса 4 — браузерная дверь ЛЮБОГО вендора (⭐31.07, правило оператора: отменяется дверь, а не вендор).** Кончилась квота / нет CLI / headless разлогинен → это закрылась ОДНА дверь; веб-морда вендора открыта всегда (подписки живые, Chrome залогинен на всех машинах [[one-chrome-account-all-machines]]):
1. `python ...\secondop.py web-prompt --engine <grok|gemini|chatgpt|claude|mistral|deepseek> --context "<что собрали + что проверили>"` → paste-ready промпт с контрактом вердикта;
2. вставить в НОВЫЙ чат на сайте вендора (строго локальный браузер), дождаться ответа;
3. залогировать `log-ext --reviewer <вендор>` со ссылкой на чат ПЕРВОЙ в `--note`.
Состояние дверей узла — факт, не догадка: `python ~/.claude/scripts/llm_rails.py --verify` (❌ = двери нет совсем; ⚠️/✅ = дверь есть). Цена ошибки замерена 31.07: Grok был залогинен в браузере и уже дал вердикт, а сессия записала «нужен login = руки оператора» — смотрели на закрытую дверь рядом с открытой ([[browser-door-when-cli-dead]]).

**Скип — только явный, никогда молчаливый** (COUNTER Codex 17.07): причины **«квота» и «нет CLI» больше НЕ принимаются** — сперва рельса 4; log-skip законен, только когда закрыты ВСЕ двери (включая браузерную — например, узел headless без браузера И шина-брокер молчит) / нет исполняемых артефактов →
```
python ... secondop.py log-skip --ritual tt --task <id> --reason "<все двери закрыты: перечисли какие|нет исполняемых артефактов>"
```
и вердикт Шага 5 **не может быть ✅** по этой причине: максимум **⚠️ PARTIAL «второе мнение не получено»**. Пропущенный звонок ≠ зелёный тест. Исключение: артефакт неисполняемый — тогда скип нейтрален, ✅ возможен.

**Наблюдаемость:** каждый вызов/скип пишется в `bridge-state/usage.jsonl` (attempted · ok · skipped · finding); суточный дайджест — `secondop.py digest --post` → чат 03. Ноль вызовов за сутки = сигнал «ритуал не работает», а не тишина.

## Шаг 3 — СЛОЙ ВИДИМОСТИ (видно ли, что сработало?)
Самый частый тихий баг — не в ядре, а в том, что **результат не видно** ([[verify-existing-before-proposing]]):
- **Готовый гейт первым:** если у проверяемого есть СВОЙ детерминированный гейт/тест (`memory_guard.py`, `/arch`, `sync_check`, `_test_*.py`) — запусти ЕГО и бери ЕГО вердикт; не пере-выводи логику самодельным awk/grep — дубль гейта со временем разъезжается с оригиналом и даёт ложные/расходящиеся тревоги (грабли 2026-06-27/07-04: raw-awk и `memory_guard.py` мерили длину строк по-разному).
- есть ли счётчик/лог/строка-доказательство, что оно отработало?
- «LastResult=N без логов» = неотладимо → это ❌ по видимости, даже если ядро вроде ок. (Так поймали пустой TurnState и ложный RED синка.)
- ⭐ **ПРИЧИНА ОБЯЗАНА БЫТЬ ПРИЧИНОЙ ТОГО, ЧТО ДЕРЖИТ** (замер 14.08.2026, `hold-with-reason-ok-is-a-lying-indicator`). У прибора с НЕСКОЛЬКИМИ условиями возьми красную строку и спроси: «по ней человек знает, что чинить?». Красный флаг с зелёным хвостом (`[HOLD] файл.md — ok`) = прибор ВРЁТ: он считал два условия, а напечатал причину не того. Так 47 из 106 постов копилки стояли молча, 21 из них 8 суток. Держат оба условия — печатать оба. Это ❌ по видимости, даже если ядро право.

## Шаг 3.1 — ⭐ ГЕЙТ МАСШТАБА: цена растёт с ОБЪЁМОМ или с ИЗМЕНЕНИЯМИ? (03.09.2026)
Собрал/правил прибор, который что-то ОБХОДИТ (треды, файлы, репо, чаты, строки БД) — задай ему один вопрос: **с чем растёт цена прогона?**
- Растёт с ЧИСЛОМ ИЗМЕНЕНИЙ — ок, поток изменений примерно постоянен.
- Растёт с ОБЪЁМОМ — **дата смерти уже назначена**, прибор сломается ровно от нашего успеха. Лечение = кэш вердикта по дешёвому признаку изменения, который отдаёт сам источник (`updated_at`, ETag, хэш, mtime): неизменившийся объект обязан стоить НОЛЬ запросов. Поднять потолок ≠ починить (это перенос смерти на месяц).
- Есть потолок/лимит/`--max-*` — три обязательных проверки: (1) прибор ПЕЧАТАЕТ, что посчитал не всё («осмотрено N из M»), а не отдаёт голое число ([[instrument-is-a-claim-too]]); (2) рез идёт ПОСЛЕ сортировки, иначе под нож уходит хвост списка — а там обычно лежит добор-заплатка, закрывающая дыру покрытия; (3) у кэша названа ГРАНИЦА ТОЧНОСТИ (что признак изменения НЕ ловит) и принудительное протухание по возрасту.
- Замер, из которого правило: `github_reply_meter` умер дважды от одного корня — 29.08 по таймауту (громко), 03.09 потолком с молчаливой потерей 14 тредов из 214 (тихо). Кэш по `updated_at`: покрытие 200/214 → 217/217, API 433 → 110. Канон: [[instrument-cost-must-scale-with-change]].
- Пропустил гейт на приборе-обходчике → вердикт максимум ⚠️.

## Шаг 3.2 — ПУБЛИЧНАЯ ВИДИМОСТЬ: смотри с чужой стороны провода (01.08.2026)
Если изменённый артефакт **публичный** (профиль, README, страница, репо, пакет, пост) — зелёный тест на нашей стороне ещё НЕ значит, что снаружи это видно. Проверка обязана быть **анонимной**: свой токен/кука/логин показывают тебе твою же приватную картину, и ты объявишь «готово» ровно там, где сломано.
- Правило: **опубликовано ≠ видно.** Пока анонимный запрос не увидел артефакт — он не зашипен, а лежит.
- Инструмент (GitHub-аккаунт лабы и его Pages): `python3 ~/.claude/scripts/public_surface_audit.py --html` → exit 1 при красном, дашборд `_Dashboards/Public-Surface.html`, паспорт `00-System/Public-Surface-Passport.md`. Ночная рутина сигналит только на СМЕНУ картины.
- Для чего у аудитора нет строки — проверь руками одним `curl` без токенов на конкретную строку из артефакта (не на код 200: 200 с пустым телом — самый частый тихий сбой).
- Цена пропуска замерена: profile README двух сессий (S0 31.07 + S1 01.08) был невидим, потому что GitHub требует отдельного клика «Share to Profile» и молчит, когда он не нажат ([[github-profile-readme-share-to-profile]]).

## Шаг 3.3 — ⭐ ЖИВОЙ ЛИ ОБЪЕКТ, В КОТОРЫЙ МЫ ПИШЕМ? (03.09.2026)
Артефакт пишет в **профиль / аккаунт / базу / ветку / слот / канал**, выбранные по КОНФИГУ (`default=`, `current`, `active`, `[Install*]`, «первый в списке») → один дешёвый замер ДО вердикта: чем доказано, что этим объектом ПОЛЬЗУЮТСЯ? Конфиг называет НАМЕРЕНИЕ установщика, диск показывает ФАКТ — свежесть `prefs.js`/`cookies`/`logins`/mtime/счётчика.
- ⛔ Признак живости НЕ должен включать файл, который пишет сам проверяемый инструмент: после залива мёртвый объект выглядит самым свежим, и прибор врёт ровно там, где его зовут.
- Расхождение конфига и факта печатается ВСЛУХ (`WARN: конфиг указывает на X (активность …), живой — Y (активность …)`), а не глушится.
- Замер, из-за которого шаг появился: `chrome2firefox` залил 19978 адресов, 59646 визитов и 6817 закладок в профиль Firefox из `profiles.ini` и напечатал зелёные счётчики; живой профиль оператора в `profiles.ini` не значился вовсе, а у выбранного последняя активность была за три недели ДО миграции. Поймал не тест, а человек, который пошёл проверять свои пароли.
- Не доказал живость → вердикт максимум ⚠️. Канон: память [[live-object-is-picked-by-use-not-by-config]], [[instrument-is-a-claim-too]].

## Шаг 3.3-полу — ⭐ СКОРИНГ СУДИТ ОБЪЕКТ ИЛИ МЕШОК СЛОВ? (04.09.2026)
Артефакт **фильтрует / скорит / ранжирует / отбирает** из РАЗНОРОДНОГО потока (лента, канал, инбокс, выдача поиска, чужой борд) → два вопроса ДО вердикта, оба с цифрой:
- **Чем доказано, что это объект нужного ТИПА?** У вакансии есть ДОЛЖНОСТЬ; буллет, проза и рекламная простыня должностью не являются. Отвод только по ПОЗИТИВНО опознанному признаку («это фрагмент»), а не по «не нашёл каноническую форму» — иначе выпадают живые разговорные посты и дайджесты списком.
- **Признак взят из ПРЕДМЕТА или из текста вокруг него?** Роль и тема считаются по должности; тело даёт уменьшенный вес, но не ноль (иначе теряется не-AI роль в AI-компании).
- ⛔ **Каждое слово словаря — claim, и его надо посчитать на живых данных**: сколько верных срабатываний против ложных. Голое «Partner» дало 82 срабатывания и НИ ОДНОГО верного.
- Замер, из-за которого шаг появился: фильтр вакансий `jobs_tg.py` принимал за вакансию обрывки разрезанных постов, резюме соискателей (96 в базе), рекламу самого канала и скам с торговлей SSN — последний брал 8-11 баллов, потому что нёс и EU, и US, и remote. Брак: 13 строк из 60, 5 из 12 верхних. Прибор не падал ни разу, счётчики были зелёные.
- Не опознал тип и не посчитал словарь → вердикт максимум ⚠️. Канон: память [[score-the-object-not-the-bag-of-words]], [[instrument-is-a-claim-too]].

## Шаг 3.3-бис — ⭐ КЛЮЧ, ПО КОТОРОМУ СШИВАЮТ: он вообще заполнен? (03.09.2026)
Артефакт опирается на **join key / поле идемпотентности / ключ дедупа / ключ «уже сделано»** (`slug`, `external_id`, `msg_id`, `hash`, `story_id`) → ОДИН дешёвый замер ДО вердикта: какая ДОЛЯ записей этот ключ реально несёт? Считать `count(*) WHERE key = '' OR key IS NULL`, а не проверять, что поле есть в схеме.
- ⛔ Пустой у большинства ключ = гейт, который открыт ВСЕГДА и молчит: проверка честно возвращает False на каждой записи, ни один прибор не краснеет, счётчики печатают числа, и по ним принимают решения.
- Ключ читает один код, а заполняет другой → назови обоих поимённо. Читатель есть, писателя нет — это и есть поломка, а не «фича не сработала».
- Второй провод обязан быть НЕЗАВИСИМ от первого: статус в базе и файл на диске врут по-разному. У детектора расхождения обязан быть исполнитель (`--heal`), иначе долг только печатается ([[detector-without-executor]]).
- Замер, из-за которого шаг появился: в контент-воронке `slug` пуст у 2248 записей из 2276 (98.8%) и у 100% сидов в статусе `new`. Один пустой ключ дал три следствия — идемпотентность выбора не срабатывала ни разу, обратная связь черновик→воронка рвалась молча (2 живых долга), а публикация не пришивалась к сиду: леджер 173 `posted` (137 с 20.08) против `published: 2` в воронке.
- Не посчитал заполненность ключа → вердикт максимум ⚠️. Канон: память [[empty-join-key-is-an-always-open-gate]], [[instrument-is-a-claim-too]].

## Шаг 3.3-тер — ⭐ ПРОМЕЖУТОЧНОЕ СОСТОЯНИЕ: кто вернёт элемент, если держатель умрёт? (04.09.2026)
Артефакт переводит элемент в **промежуточную корзину** (`taking` / `in-progress` / `claimed` / `lease` / `processing` / статус «взято в работу») → три вопроса ДО вердикта, все три дешёвые:
- **(1) Кто возвращает?** Есть ли жатва/reaper, которая по TTL вернёт элемент в очередь, если держатель умер между «взял» и «отметил». Атомарный захват защищает от ДУБЛЯ и ничего не говорит про ПОТЕРЮ — это разные беды, и вторая молчит.
- **(2) От какого события мерится возраст удержания?** `os.replace`/`mv`/`UPDATE` часто сохраняют старую метку, и возраст выходит «сколько лежит в очереди», а не «сколько держат». Сторож на такой метке сожмёт свежий захват старого элемента в первую же секунду.
- **(3) Видит ли счётчик здоровья промежуточную корзину?** Если «сколько ждёт» считает только `pending`, потерянные элементы делают очередь короче, чем она есть, и здоровье выглядит зелёным.
- Замер, из-за которого шаг появился (04.09, `spawn_queue.py`): `take` уносил сид в `taking/` атомарно и правильно, возврата не было — 03.09 два сида восстанавливали руками, 04.09 третий висел 11 часов и не считался никем; возраст при этом мерился от `add`, а не от `take`.
- Исполнителя вешай на УЖЕ СУЩЕСТВУЮЩУЮ дверь ([[detector-without-executor]]): здесь жатву вшили в хук самой очереди (96 срабатываний за двое суток), новой рутины не завели.
- Нет ответа хотя бы на один из трёх вопросов → вердикт максимум ⚠️. Канон: память [[atomic-take-without-reaper-loses-work]].

## Шаг 3.3-кватер — ⭐ СКЛЕЙКА ЛЮДЕЙ: чем доказано, что это ОДИН человек? (04.09.2026)
Артефакт **связывает запись с человеком** (импорт контактов, обогащение CRM, дедуп карточек, «дописать ссылку в существующую карточку») → назови КЛЮЧ каждой связи ДО вердикта.
- **В файл пишется только сильный ключ** — телефон или handle. Совпадение по ИМЕНИ или ПОЧТЕ в файл не идёт никогда: оно уходит в корзину «требует глаз» и ждёт человека. Молча выбросить = потерять подсказку, молча записать = отравить карточку.
- **Сильный ключ на входе не делает сильной всю цепочку.** Замер 03.09: телефон верно находил контакт в мосте `apple-contacts`, а ложной была следующая связь «контакт → заметка волта» со своим tier. Проверяй tier у КАЖДОГО звена, а не только у первого.
- **Ошибка склейки выглядит как успех**: лог рапортует «дописано ссылок 143», карточка выглядит обогащённой. Поэтому нужен красный кейс «слабый tier → ссылки нет», а не глазами по логу.
- Ключ-индекс строй по нормализованной форме рядом с маркером (`+`, `phone:`, `тел`), а не «любое число 9-15 цифр»: 637 коллизий last10 и склеенные даты `2026 09 03` в роли номеров, победитель по порядку `os.walk`. При коллизии не выигрывает НИКТО.
- Замер, из-за которого шаг появился: мост на 75% построен по имени (T4-name 957 из 1275), и слабый tier вписал 4 ЧУЖИЕ переписки в боевые карточки лидов — Azam Shaghaghi в `amir-sultan-malik-awan.md`, Manizha Ash дважды в `alex-ge-pengfei-ge.md`, Нора Лебедева в `apefan-2.md`.
- **Прогон гейта** (эталонная сетка склейки, 0 LLM — красный кейс «слабый tier → ссылки нет» уже внутри):
  ```bash
  python D:\Vault\_imports\whatsapp\_test_wa_ingest.py
  ```
  Свой импортёр людей — скопируй оттуда секцию «ИДЕНТИЧНОСТЬ» под свой мост и покажи её КРАСНОЙ на сломанной копии.
- Не назвал ключ каждой связи → вердикт максимум ⚠️. Канон: память [[identity-merge-only-on-strong-key]], [[crm-lead-full-provenance]].

## Шаг 3.3-квинт — ⭐ КОРПУС В ВОЛТЕ: чем его НАЙДУТ, и доказано ли это запросом? (04.09.2026)
Артефакт кладёт в волт **пачку заметок** (импорт переписки, выгрузка, корпус) → назови ДВЕРЬ поиска и покажи ЖИВОЙ хит.
- Строка в логе про реиндекс — claim про прибор, не про результат ([[instrument-is-a-claim-too]]). Реиндекс мог отработать ДО рождения заметок, не покрыть их по scope или собрать базу, у которой нет потребителя.
- Доказательство = запрос по редкому слову из конкретной новой заметки и её путь в выдаче. Замер 03.09: 454 заметки и 148 696 сообщений лежали в волте, в векторном индексе WhatsApp-чанков **ноль**, FTS знал 35 старых путей. После пересборки каталога запрос «Dearden» вернул `wa-Timothy-Dearden--461055.md`, путей стало 492.
- Есть быстрый SQL/FTS слой поверх корпуса → назови его вслух в `/find` и `/ask`, иначе LLM будет читать markdown вместо бесплатного запроса (§6.1).
- Дверь не названа или названа без живого хита → вердикт максимум ⚠️. Канон: память [[corpus-needs-a-named-search-door]].

## Шаг 3.3-секст — ⭐ СШИВКА С ЧУЖИМ ОБЪЕКТОМ: ключ СТРУКТУРНЫЙ или текстовый? (04.09.2026)
Прибор связывает НАШУ запись с ЧУЖИМ объектом (письмо, страница, карточка, тред) → четыре вопроса, каждый обязателен:
- **Ключ структурный?** Домен адреса, id в URL, отдельное поле — да. «Имя компании встречается в строке письма» — нет: текст несёт ещё и транспорт (`[EMAIL]`), и матч цепляется за него. Замер 04.09: в реестре лежала строка `company='ashby'` (мусор писателя), её алиас совпадал в служебном адресе КАЖДОГО письма Ashby и забрал 16 чужих подтверждений — mem0, dust, Cursor получили вердикт «заявка не ушла», а 61/61 тестов были зелёными.
- **Матч однозначен?** «Первый по порядку словаря» = случайный владелец, то есть тихая кража В ПЛЮС. Побеждает самый длинный/специфичный ключ, ничья → None. Молчание честнее выдуманного хозяина.
- **Приговор по ТЕЛУ или по заголовку?** Заголовок (тема письма, title страницы) — свободный текст чужого вендора, бесконечное множество: латать его регекспами = чинить симптом, дыра откроется на следующем шаблоне (замер: латали 03.09, открылась 04.09). Тело — шаблонный язык, конечное множество идиом; пополнять его законно.
- **Какой канал прибор НЕ смотрит?** Назови вслух. Часть объектов приходит другой дорогой (мы подавались письмом, а не формой) — для них у прибора обязан быть ОТДЕЛЬНЫЙ вердикт, а не молчаливое «не найдено». Смешать со «доказано» = соврать в цифрах; выдать за «пропало» = послать человека делать необратимый дубль.
- Хоть один вопрос без ответа → вердикт максимум ⚠️. Канон: память [[match-entity-by-structural-key]], [[instrument-is-a-claim-too]].

## Шаг 3.4 — ⭐ РАТЧЕТ: escape-авария в коде (03.09.2026)

```
python ~/.claude/scripts/_test_no_control_bytes.py
```

Правил код патчем, внутри которого есть обратный слэш (windows-путь, `\n`, `\b`, `\d` в регулярке)? Прогони это ПЕРЕД вердиктом. `exit 1` = где-то в коде лежит управляющий байт.

**Почему отдельный шаг, а не «и так увижу».** 03.09 класс сработал шесть раз за один день, и один случай был дорогим и невидимым: в `deploy_deadwood.py` литерал `r"\bmd5"` стал `r"<0x08>md5"`, и живая проверка «verify прибит к md5» не срабатывала **никогда**. Голый `grep` печатает такую строку как `r"md5"` — терминал съедает backspace, глазами дефект не виден вообще. Нашёлся только побайтовым сканом.

**Лечение на будущее:** патч с обратными слэшами пишем **файлом** (Write → `python файл.py`), а не python-в-heredoc: escape ломается на границе слоёв. Канон: память [[patch-code-via-file-not-heredoc]].

## Шаг 3.45 — ⭐ ВЛАДЕЛЕЦ ОБЪЕКТА: не заводи второго убийцу (04.09.2026)

```
python ~/.claude/scripts/robot_owner_lint.py
```

Собрал робота, который **трогает объект** — гасит процессы, перезапускает приложение, чистит папку, правит общий файл? Прогони это перед вердиктом. `exit 1` = появился робот, которого нет в `~/.claude/robot_owners.json`.

**Правило:** у объекта один АВТОМАТИЧЕСКИЙ владелец. Владелец есть — расширяй его, а не заводи своего. Свой всё же нужен (ручной инструмент, патруль) — впиши в реестр с ролью и с тем, чем он ограничен, и **уважай рельсы владельца**.

**Почему отдельный шаг.** Класс с тремя датированными случаями: 26.07 два сторожа дрались на восстановлении пакета; 31.08 двенадцать чинилок на одно приложение довели до приказа «выключить всё», и невиновный жнец простоял трое суток (138 зависших процессов); 03.09 патруль закрыл ровно те процессы, что жнец пощадил осознанно. Пять «почему» дали корень не в роботах: **владельца негде было посмотреть, поэтому своего написать дешевле, чем найти чужого.** Замер 04.09: 13 скриптов способны убить процесс Claude.

Канон: память [[one-object-one-owner-robot]], реестр `~/.claude/robot_owners.json`.

## Шаг 3.5 — ТЕСТ + ДОК гейт (§5.8, dev 28.07 «и ВСЕГДА это делать теперь»)
Каждая живая деталь в области Шага 0 обязана выйти из /tt с тестом И доком — иначе вердикт максимум ⚠️:
- **НОВАЯ деталь** (скрипт/скилл/рутина/хук): тест и док-паспорт рождаются **в этом же заходе**, ждать «докажи, что приживётся» ⛔. Паспорт — для слабейшего починщика ([[repairability-first-how-we-build]]): что делает · вход/выход · кто дёргает · что ломается · как понять · как починить.
- ⭐ **РУТИНА → СТРОКА В РЕЕСТРЕ** (dev 02.09, голосом): собрал/изменил повторяющийся процесс (задача планировщика · cron · hook · вахта · ручная повторёнка) → покажи его строку в мега-списке рутин: обнови снимок узла `python %USERPROFILE%\.claude\scripts\fleet_routines_collect.py` и найди рутину в `_machine-bus\_fleet-routines\routines-<NODE>.json` (Маяк ежечасно сводит снимки в Google-книгу «Флот — живой стол»). Повторёнка ВНЕ планировщика сама не доедет — занеси в книгу руками. Нет строки → ⚠️. Канон `reglament-lyubaya-povtoryayushchayasya-rabota-zhivyot-v-reestre-rutin` + [[routine-must-live-in-registry]].
- ⭐ **РУТИНА → НАЗОВИ СВОЙ ВЫХОД** (класс `silent-green-watchdog` / семья `instrument-vrjot-zelyonym`, 46 датированных случаев, починка 04.09): рутина рождается с рапортом «зелено» и БЕЗ единого свидетеля результата — «задача выстрелила» ≠ «работа приземлилась». Прогон: `python %USERPROFILE%\.claude\scripts\_shared\green_gap.py` (0 LLM, свой контрольный пример, exit 0/1/3/4). Новая рутина обязана дать ОДНО из двух: строку в `ARTIFACTS` (`scripts\_shared\output_freshness.py` — ГДЕ приземляется её работа) **либо** строку с ПРИЧИНОЙ в `~/.claude/green_gap_exempt.json` (выхода нет осознанно). Молчание = зелёный, который никто не проверял → вердикт максимум ⚠️. Ратчет: старый долг назван числом и молчит, кричит только НОВОЕ. Замер 04.09 (хаб): 243 наших включённых задачи против 41 строки реестра = выход заявлен у 17%.
- ⭐ **ПРИБОР → НАЗОВИ ПОКРЫТИЕ И СЛЕПУЮ ЗОНУ ЧИСЛОМ** (dev 01.10.2026 голосом, класс `instrument-blind-to-most-of-its-subject`; пара к шагу выше и к правилу Connect: собравший прибор отвечает за его ПОКРЫТИЕ, а не за то, что прибор существует). Собрал или тронул прибор (сторож, счётчик, аудит, «долг X», дашборд-число), и проверь вывод: `python3 ~/.claude/scripts/_shared/blind_zone.py --run <команда прибора>`. exit 0 = зрячий · **1 = СЛЕПОЙ** (покрытие <90% или «не знаю» больше вердиктов) · **3 = прибор МОЛЧИТ про слепую зону**: такой хуже отсутствующего, потому что даёт ложное спокойствие · 4 = упал, вердикта нет. Определение: «судимый» предмет = вердикт по самому предмету (файл/строка/живой отклик), а не по руками выставленному `status:`; «посмотри глазами» вердиктом не считается. Зрячий прибор ловит расхождение в обе стороны («заявлено, а нет» и «сделано, а не отмечено»), и это показывает его тест. Нужна строка `blind_zone.line(судимые, все, причина)` в КАЖДОМ отчёте. Exit 3 → вердикт `/tt` максимум ⚠️. Exit 1 допустим только с названной причиной и задачей на подъём покрытия. Замер 01.10 на первом потребителе `canon_proposal_state.py`: до правки exit 3 (молчал), после него `не могу судить 67 из 70 → покрытие 4% → СЛЕПОЙ`, хотя в его отчёте «NO-TARGET=61» выглядело как ответ. Тест `_shared/_test_blind_zone.py`. Память [[instrument-must-not-be-blind]].
- ⭐⭐ **ПРИБОР → ПУСТОЕ МНОЖЕСТВО НЕ ЗЕЛЁНОЕ** (подсемья `vacuous-green` семьи `instrument-vrjot-zelyonym`, **156 датированных случаев с 10.08**, сессия починки класса 07.10.2026). Собрал/тронул прибор → `python ~/.claude/scripts/vacuous_green.py scan <путь>` (0 LLM, 0 сети). **exit 0** = нового нет · **1 = НОВОЕ место или РОСТ счёта → смотреть глазами в этом же заходе** · **2 = НЕ ПРОВЕРЕН, и это НЕ «чисто»**. Ловит две формы: **SKIP** (`if <коллекция>:` с утверждениями, а `else` не падает → пустота пропускает проверки) и **SHRINK** (множество фильтруется по `.exists()`/`.is_dir()` своей же переменной цикла → исчезновение предмета не краснеет). **ЛЕЧЕНИЕ одно и называется ВНЕШНИЙ ПОЛ**: ожидаемое множество лежит ВНЕ наблюдаемой системы (`sync_floor.json` у `sync_monitor`, `state.json→planted` у `appdata_sweep_canary`), прибор краснеет когда наблюдённое < объявленного, и пол **не опускается** (пересадка после атаки пишет ОБЪЕДИНЕНИЕ, иначе успешная атака понижает планку и прибор зеленеет снова). ⚠️ **Почему подметальщик, а не ещё один сторож**: лечение этой подсемьи изобреталось ЧЕТЫРЕ РАЗА (29.07 делегат консенсуса · 06.10 `sync_floor` · 06.10 канарейка AppData · 06.10 пустой пул слотов) и каждый раз оставалось у ОДНОГО потребителя, потому что все прежние лечилки рантаймовые и ОПТ-ИН. Замер опт-ина 07.10: `blind_zone` из пункта выше зовут **6 приборов из 674** — дверь, которую обязана пригласить та самая голова, у которой слепое пятно, класс закрыть не может. Базовая линия `~/.claude/vacuous_green_baseline.json` держит СЧЁТ мест на (файл, форма), а не множество ключей: первая версия свернула 89 мест в 71 ключ и была бы слепа ко ВТОРОМУ новому месту в уже задолжавшем файле (поймано на себе в тот же день). ⛔ Форму `for x in <выведенное>:` подметальщик НЕ ловит сознательно (дало бы сотни мест = прибор-флудер, то есть снова проигнорированная дверь); её лечит только внешний пол у самого прибора. Реестр всех пяти дверей семьи — `prior_art.py` → `FAMILY_DOORS["instrument-vrjot-zelyonym"]`. Тест `_test_vacuous_green.py` (9 групп проверок, 6 мутаций показаны красными 07.10). Память [[instrument-is-a-claim-too]], [[watchdog-must-verify-the-item]].
- ⭐ **ПРИБОР → ЧЕМ ДОКАЗЫВАЕШЬ ЗЕЛЁНЫЙ** (семья «жив на бумаге» / класс `watchdog-mints-green-from-transport`, **7 датированных случаев**, разбор /five-whys 02.10.2026). Собрал/тронул файл, который МИНТИТ вердикт живости (`alive`/`active`/`healthy`/`green`/🟢) про компонент, делающий работу (демон · MCP · канал · мост · рекордер · сессия · рельса) → `python ~/.claude/scripts/liveness_lint.py --check <путь>`. **exit 0** = чисто, либо дыра заморожена в baseline (старый долг правку НЕ блокирует), либо 🟡 МЯГКИЙ ярус (улика слоя access/output в файле есть, но не в функции вердикта — назвать и свести в одну функцию, когда будешь рядом) · **exit 1 = НОВАЯ жёсткая дыра ЛИБО дыра ВЫРОСЛА внутри замороженного файла → чинить В ЭТОМ ЖЕ заходе**, иначе вердикт максимум ⚠️ · **exit 2 = НЕ ПРОВЕРЕН, и это НЕ «чисто»** (нет файла/корня). Лечение линт печатает сам, и оно одно из трёх: (1) звать контракт `from liveness import judge, E` → `judge([...])`; (2) судить ВОЗРАСТ ВЫХОДА (mtime/age_sec/last_*_timestamp), §5.5; (3) осознанная дыра → `--accept` с причиной в ревью. ⚠️ **Почему гейт ЗДЕСЬ, а не в ночном аудите**: контракт живости `_shared/liveness.py` существует с 01.10, вызывается и краснеет (`--audit` exit 1, три 🔴) — и класс воспроизвёлся в тот же день. Замер 02.10: из 63 приборов живости контракт зовут **2 (3%)**; у **234 из 321** рутины выход не заявлен, и **37 из них НОВЫЕ** с прошлого снимка. Отчёт ничего не держит: тот же механизм уже доказан на соседнем классе (ниже, `help_flag_lint`: 55 новых дыр за 11 суток после baseline). Замер при рождении: предметов 277, вердикт по 49, жёстких дыр 10 (заморожены), мягких 23, **покрытие линта 18% → по шагу выше он честно объявляет себя СЛЕПЫМ сам**. Мороз баселайна накрывает ЧИСЛО мест минта, а не имя файла: дописал в замороженный файл ещё один ложно-зелёный — краснеет. Мёртвый импорт `judge` и мёртвая `_age_sec` уликой не считаются (находки break-панели 02.10, вердикт BLOCK, применены в том же заходе). Тест `_test_liveness_lint.py --mutations` (19 кейсов + 5 мутаций, каждая обязана сломать ИМЕНОВАННЫЙ кейс). Память [[watchdog-must-verify-the-item]].
- ⭐ **ВЫХОД В СИНКАЕМОЙ ПАПКЕ → НАЗОВИ ЕГО КЛАСС** (класс `shared-writers`, починка 14.09): выход рутины/скрипта лёг в синкаемое (волт · `_machine-bus` · `~/.claude` · `_imports`) → он ОБЯЗАН иметь строку в `D:\Vault\_imports\sync\derived_writers.json`, ровно в одном из трёх классов: `per_node` (данные пер-узловые — имя получает суффикс узла, конфликт физически невозможен) · `writers` (данные общие — ОДИН назначенный владелец, и раннер у него ДОКАЗАН, иначе меняем громкую поломку на тихую заморозку) · `idempotent_verified` (тело рендера НЕ зависит от часов — **только с именем теста**, который это доказывает). Прогон: `python D:\Vault\_imports\sync\derived_writers.py --check` и `--audit`. Нет строки → вердикт максимум ⚠️. ⚠️ Класс определяется по ВОПРОСУ «данные тут про ЭТОТ узел или про весь флот?», а не по тому, где лежит файл: ошибка в эту сторону стоила слепоты — один писатель у пер-узлового файла = ослепли на пяти узлах. Замер 14.09: 8 путей кровоточили 10 суток, самый громкий (`ACTIVE_NOW.md`) — 43 копии с 6 узлов, потому что класс `idempotent` был объявлен БЕЗ теста и оказался ложью. Канон: `derived_writers.json` §_refuted + [[watchdog-must-verify-the-item]].
- ⭐ **ПУТЬ В КОНФИГЕ ОБЯЗАН СУЩЕСТВОВАТЬ** (класс `config-path-points-nowhere`, замер 06.09.2026): трогал реестр аккаунтов/профилей (`_imports/chatgpt/accounts.json`, `~/.claude/browser-profiles/accounts.json`) → прогони `python3 ~/.claude/scripts/accounts_paths_lint.py` (0 LLM, 0 сети; exit 0 чисто · 1 красное · 3 нет данных · 4 крэш). Повод: `ff_profile` у `bb`/`au04` указывал на `autoff-bb`/`autoff-au04`, которых не было НИ НА ОДНОМ узле — лестница жатвы токена не могла отработать в принципе и **не сказала ни слова** (рельса печатала честный SKIP «нет bearer», а ПРИЧИНУ не назвал никто). Линт судит и **связку двух реестров**, но ТОЛЬКО у аккаунта, чей `runner` = этот узел: браузерный реестр машинно-локален (`browser-profiles/` в `~/.claude/.gitignore` + под `*` в `.stignore` — ни git, ни Syncthing его не возят), поэтому у чужого аккаунта два поля описывают РАЗНЫЕ машины и сравнивать их нельзя (у a2 верны ОБА: `fbread` на хабе, `autoff` на NODE-0X). Такое не молчит и не желтит — идёт строкой «НЕ СВЕРЯЛОСЬ» + `meta[join_not_compared]`. ⚠️ Имя узла с доменным хвостом (`<узел>.local`, FQDN в Docker/CI) резолвится срезом хвоста: без него СВОЙ сломанный аккаунт выходил ЗЕЛЁНЫМ (замер 07.09: `rc=0`, `GREY` вместо `RED`). Красное = чинится здесь; не прогнал после правки реестра → вердикт максимум ⚠️. Тест: `_test_accounts_paths_lint.py` (5 мутаций, все показаны красными 07.09).
- ⭐ **ДОКА ЖИВЁТ В КОДЕ** (dev 07.08 голосом, СУПЕР ВАЖНО): у Python-детали док = **docstring в самом файле** (назначение · вход/выход · кто дёргает · рельса · `updated: ГГГГ-ММ-ДД`), один источник — отдельный md-пересказ того же самого ⛔; тест назван в docstring, деталь названа в тесте (код·тест·дока = единый узел). Docstring отсутствует или без updated-даты → ⚠️. Канон `reglament-dokumentaciya-po-chastyam-i-vnutri-koda`.
- **ИЗМЕНЁННАЯ/ПОЧИНЕННАЯ деталь**: поведение поменялось → док обновляется **той же сессией** (док, который врёт, дороже отсутствующего); класс пойманного бага получает тест/гейт, чтобы не вернулся ([[fix-root-cause-not-symptoms]] forever-fix).
- **«Тест есть» ≠ «тест гоняют»** ([[test-exists-vs-grid-runs-it]]): тест без расписания/сетки и видимой даты прогона ≤30 дн считается несуществующим (§5.8 правило 2). Подключи в регресс-сетку или назови причину.
- ⭐ **СЧЁТЧИК ИСПОЛЬЗОВАНИЯ** (§5.8 третий атрибут, dev 04.08: «на весь функционал вешаем счётчики — кто и насколько успешно использует»): деталь считает свои вызовы строкой JSONL `ts·node·actor·event·outcome` рядом с собой (эталоны: `usage.jsonl` secondop, `_spawn_slot_guard.log`, `_chip_guard.log` — тот же паттерн, НЕ новая инфраструктура). Гейт считает ALLOW/BLOCK, скилл — старт, рутина — исход тика (не факт запуска). Флотовой механизм → лог читаем с хаба, иначе «кто пользуется» снова слепое пятно (замер 04.08: session-control-pack — применение видно 5/6, использование только локально). Нет счётчика → ⚠️. Канон `reglament-schyotchik-ispolzovaniya-na-ves-funkcional`.
  ⭐ **И ТЕСТ В НЕГО НЕ ПИШЕТ** (замер 04.09.2026): путь счётчика обязан переопределяться флагом `--counter`/env, а регресс-сетка обязана его переопределять — иначе метрика «живое или утиль» врёт. Замер: в `whatsapp_pipeline.jsonl` 67% строк написал тест, использование было завышено **в 7 раз**, и почти не используемая деталь выглядела живой. Кейс приёмки: снять размер боевого JSONL в начале теста и сверить в конце («боевой счётчик тестом НЕ тронут»). Эталон: `D:\Vault\_imports\whatsapp\_test_wa_ingest.py` (подстановка в общей `run()`). Счётчик без флага → ⚠️. Память [[counter-is-production-tests-must-not-write-it]].
- ⭐ **KILL-LIST: тест обязан сказать, что именно он ловит** (замер 11.08, [[kill-list-makes-tests-checkable]]). В докстроке теста — блок `МУТАЦИИ, КОТОРЫЕ ЭТОТ ТЕСТ ОБЯЗАН УБИТЬ`: одна строка = конкретная правка исходника → ИМЯ падающего от неё кейса. Ревьюер применяет каждую строку к **КОПИИ** детали (живую не мутируй: сторож стреляет каждые 5-20 минут) и смотрит, покраснел ли НАЗВАННЫЙ кейс. Строка не сработала = ЛОЖНАЯ заявка, и это хуже отсутствующей: по ней деталь считается защищённой. Добавь сверх списка СВОЮ мутацию — обе фикции 11.08 (кейс из одних отрицательных проверок; снятая защита, которую тест не заметил) всплыли именно на ней. Пустая мутация (добавил переменную) ничего не доказывает — сверь, что подстановка изменила поведение. Пишет тест внешняя подписка (§6.3, `secondop.py implement`), kill-list требуй прямо в спеке + «честный пробел лучше зелёного вранья».
- **Доказательство**: строка детали в карте покрытия — `python ~/.claude/scripts/coverage_map.py` (тест ✅ · док ✅ · ссылки); нет карты на узле → перечисли тест и док явными путями в вердикте. ⚠️ Карта считает покрытым только `_test_<имя детали>.py`: тест, названный по сценарию (`_test_cron_watchdog_absent.py`), в зачёт не идёт → покрытие ЗАНИЖЕНО, проверь глазами перед выводом «тестов нет».
- ⭐ **РЕЛЬСА ХРАНЕНИЯ — НАЗОВИ ОКНО ВОССТАНОВЛЕНИЯ** (dev 21.08 «почини корень»): деталь, которую зовём бэкапом / зеркалом / репликой / синком / снапшотом, выходит из /tt с ✅ только если (1) названо ОКНО — сколько времени есть на откат, и (2) показан ПРОГОН, где удаление на источнике НЕ уничтожило вторую копию. Способы ровно три: датированный карантин · версия/снимок · отказ прохода по порогу из ЗАМЕРА (медиана + наблюдённый максимум по истории прогонов, не из головы). Реплика без окна — вторая мишень, а не страховка. Отчёт обязан нести ЧИСЛО удалённого/отложенного И В ХОРОШИЕ ДНИ ТОЖЕ (цифры, которой нет в отчёте, для наблюдателя не существует), красное едет на живую рельсу, а не в файл рядом со скриптом. Нет окна или нет прогона → максимум ⚠️. Замер 21.08: зеркало E→F каждую ночь переносило в «запасную копию» все удаления суток и рапортовало успех, потому что «удалено N extras» лежит внутри кодов возврата 0-7. Канон `reglament-strahovka-ne-povtoryaet-razrushenie` + [[insurance-must-not-replay-destruction]].
- ⭐ **CLI-ДЕТАЛЬ ОБЯЗАНА ОТВЕЧАТЬ НА `--help` И БИТЬ ПО НЕИЗВЕСТНОМУ ФЛАГУ** (гейт при рождении, замер 03.09.2026): тронул/собрал скрипт, который читает аргументы → `python ~/.claude/scripts/help_flag_lint.py --check <путь>`. ⚠️ Линт ответил «не понял аргумент --check» — это НЕ «фичи нет», это ОТСТАВШАЯ КОПИЯ НА УЗЛЕ: прогони `python ~/.claude/scripts/copy_sweep.py help_flag_lint` и сверь размеры (канон с `--check` = 28 683 б, августовская без него = 23 393 б). Замер 17.09 на хабе: фичу дописали ЗДЕСЬ 03.09 (рядом лежал её `bak-precheck-20260903`), а sync-конфликт 15.09 откатил рабочую копию к августовской и оставил каноническую рядом файлом `*.sync-conflict-*` — узел ослеп на свой же гейт, а скилл для оператора выглядел врущим. Лечение: поставить каноническую копию в `scripts/`, прогнать парный `_test_help_flag_lint.py` (с секцией G должно быть PASS 35). exit 0 = чисто ЛИБО дыра заморожена в baseline (**старый долг правку НЕ блокирует**) · **exit 1 = НОВАЯ дыра класса `unparsed-flag-silently-runs-work` → чинить В ЭТОМ ЖЕ заходе**, иначе вердикт максимум ⚠️ (лечение линт печатает сам, 3 строки в начало `main()`). Почему гейт ЗДЕСЬ, а не только в ночной сетке: ratchet краснеет НОЧЬЮ и только ОТЧЁТОМ, а отчёт ничего не держит — за 11 дней после baseline 23.08 во флот въехало **55 новых дыр, ВСЕ в файлах, тронутых после baseline** (старых 0), и класс дал 8 датированных случаев уже ПОСЛЕ объявления «закрыт» (`pr_watch.py --help` = 7.5 мин живого тика по GitHub; `output_freshness.py --help` отправил пост в живой чат 03 в 01:41). ⚠️ **exit 2 = «НЕ ПРОВЕРЕН», и это НЕ «чисто»**: файл вне корней линта (`scripts/`, `imports/`) он не сканирует — гони гейт на детали, живущей в корнях, либо задай `HELP_FLAG_LINT_ROOT`. Тест: `_test_help_flag_lint.py` секция G (мутации: вырезать ветку → G1/G3/G4/G5; гейт, который не краснеет → G2; убрать проверку корней → G6 ловит ложное зелёное).
- ⭐ **ОТПЕЧАТОК АВТОРА ВНЕ GIT — ЧЕРЕЗ ЕДИНСТВЕННУЮ ДВЕРЬ** (§5.11; дыра вскрыта замером 15.09.2026): тронул деталь → проверь, доедет ли провенанс. `git ls-files --error-unmatch <файл>` отвечает «не знает git» (на NODE-0X `~/.claude/.gitignore` держит `*`, поэтому `scripts/` и `skills/` под git НЕ ходят) → идёт вне-git ветка §5.11: подпись с датой ВНУТРЬ артефакта + строка РОВНО через `python ~/.claude/scripts/change_ledger.py add --actor … --tool … --target … --summary …`. ⛔ Самодельный писатель запрещён: `open(<леджер>,'a')` руками и имя узла из `socket.gethostname()` вместо `COMPUTERNAME` — это класс `ledger-writer-bypasses-the-one-door`, ТРИ датированных случая (04.09 · 10.09 · 15.09), и 10.09 он стоил УНИЧТОЖЕННОГО файла журнала на case-insensitive FS (два написания одного узла = один инод). Доказательство: `python ~/.claude/scripts/change_ledger.py lint` — назови долю канона ЧИСЛОМ (замер NODE-0X 15.09: всего 234, канон 5, вне канона 227 — дверь обходили 97%). Строки нет либо писал мимо двери → вердикт максимум ⚠️. Канон `reglament-otpechatok-avtora-na-kazhdom-izmenenii-koda` + [[edit-authorship-signature]]; корневой гейт — `task-2026-09-15-ledger-writer-bypasses-the-one-door`.
- **УБЕРИ ВЕРСТАК** (§5.8 правило 1): каждый созданный по пути инструмент проштампуй — постоянный (тест+док) / одноразовый (`_scratch\`, авто-снос 30 дн) / в корзину. Не проштамповал = не закрыл.

## Шаг 3.6 — BACKPRESSURE: цикл без внешнего давления не допускается (альфа 17.08.2026)
Если проверяемая деталь **работает без человека в цикле** (рутина, cron, `/loop`, Ralph-луп, `claude -p`
в баш-цикле, самоперезапускающийся агент, автоулучшатель) — она обязана **назвать своё внешнее
давление**. Не назвала → вердикт максимум ⚠️, в прод не идёт.

Откуда правило: Julia [ФАМИЛИЯ], приём **backpressure** — внешнее давление, которое удерживает
зацикленного агента от того, чтобы «слететь с катушек». Агент в цикле **будет** придумывать себе
всё новые улучшения; без давления он уходит в космос и жжёт бак. Источник — доклад Крестникова
(Сбер/GigaChain) 17.08.2026, [[insight-2026-08-17-harness-i-ralph-loop-krestnikov]]. ⚠️ Приём чужой,
у нас на своих задачах ещё не замерен — это 🤔 гипотеза, но цена ошибки односторонняя: без давления
теряем бак и данные, с давлением теряем только пару строк кода.

**Не новая инфраструктура:** у нас давление УЖЕ есть, просто у него не было имени и не было двери,
которая спрашивает. Годные виды давления (нужен хотя бы один, лучше два):
1. **Детерминированный судья** — `_test_*.py` / готовый гейт (`regress_run.py`, `memory_guard.py`,
   `/arch`), который цикл обязан пройти на каждой итерации. Судья не живёт внутри того, что судит (§5.5).
2. **Потолок итераций / времени** — жёсткий кап и авто-kill ([[shadow-first-mvp-pattern]] time-box).
   «Бесконечный» цикл без капа = ❌, а не ⚠️.
3. **Бюджетный тормоз** — лимит токенов/вызовов, при упоре цикл встаёт САМ, а не после счёта оператору.
4. **Kill-switch** — файл-флаг/`paused`, который останавливает цикл без правки кода.
5. **Порог «не хуже»** — метрика упала → откат итерации (это и есть keep/rollback п.6 альфы).

**Проверка на приёмке (не на слово):** взять названное давление и **сломать нарочно** —
одна итерация обязана быть отбита. Не проверил прогоном = давления нет (§5.8 «проверка без
прогона = нет проверки»).

⛔ Давлением НЕ являются: «промпт просит быть аккуратным», «я посмотрю утром», «модель умная»,
ревью человеком постфактум. Давление должно быть машинным и срабатывать БЕЗ человека —
иначе человек снова оказался в середине конвейера (§4.1 [[human-is-the-bottleneck]]).

## Шаг 3.7 — ⭐ РАЗДАЙ НА ФЛОТ: ноу-хау без раздачи = пользы нет (dev 05.08, капсом «ДАВАТЬ ПОЛЬЗУ»)
Собрал полезное — оно обязано доехать до КАЖДОГО узла-потребителя, иначе вердикт максимум ⚠️.
Правило §7.3-бис существовало и молчало: 05.08 два новых скилла и патч движка пролежали три часа
никому не раздаными, потому что ни одна дверь не спрашивала «а флот?». Теперь спрашивает эта.
1. **Назови круг потребителей ДО раздачи.** Кому не нужно — явная строка `NOTFORME` с причиной
   (чужая ОС, нет железа), а не молчание.
2. **Проверь РЕЛЬС, а не надежду.** «Синк довезёт» — claim, требующий улики: у каждой шары свой
   список пиров. Спроси факт у самого Syncthing:
   `python3 -c "..."` → `rest/db/file?folder=<шара>&file=<путь>` (файл в индексе = едет).
   Замер 05.08: `claude-skills` = 6 узлов, `claude-home` (там же `scripts/*.py`) = 5 — **Маяка нет**,
   и скилл приехал бы туда без движка, который зовёт. Дверь без замка хуже отсутствия двери.
3. **Рельс не достаёт → payload-посылка** (`_deploy/payloads/<id>/` + `install.py` + `CHECKSUMS.txt`) —
   единственный канал, провабельно доходящий до всех; затем `deploy_register.py all <id> ... --verdict PASS --tier 1`
   с МАШИННЫМИ apply/verify (verify читает ФАКТ: маркер/хэш/значение, не намерение).
   `--verdict` обязателен (гейт 02.09): в шину едет только PASS этого /tt; WARN/FAIL = отказ,
   осознанный обход `--force-unsafe "причина"` (причина уезжает в запись посылки).
4. **Закрой свой узел сам** (`deploy_apply.py <id>`) и назови поимённо, кто ещё не применил.
   ⛔ Тишина узла ≠ применено: выключенный, отставший и исправный молчат одинаково.
5. ⭐ **КАНАРЕЙКА СНАЧАЛА, ПОТОМ ОСТАЛЬНЫЕ** (dev 06.08, [[canary-before-fleet-rollout]]):
   раздача ОПАСНОГО класса (канон · хук · шина · синк · сторож · авторизация · автозапуск ·
   системная настройка) идёт ступенями — **1 узел-канарейка** → verify читает ФАКТ (+ один живой
   прогон, если тронута рельса) → **узел ДРУГОГО типа/ОС** → остальные потребители. Откат назван
   ДО раскатки; узлам без того же механизма — `NOTFORME`. Безобидное (заметка · док · тест ·
   строка в скилл) едет сразу всем. Сомнение → считаем опасным. Опасный класс, уехавший на всех
   разом без зелёной канарейки, — вердикт максимум ⚠️: повезло ≠ проверено.
Табло: `python ~/.claude/scripts/fleet_fix_audit.py --html`. Канон: CLAUDE.md §7.3-бис,
[[fleet-parity-board]], [[improvement-rollout-all-peers]], [[sync-can-silently-downgrade-a-part]].

## 🛠 ВЕРДИКТ О СКИЛЛЕ, КОТОРЫМ ПОЛЬЗОВАЛИСЬ (dev 07.09, голосом — обязателен, молчание = нарушение)
Применил в этой работе скилл — вынеси вердикт об ЕГО обновлении. Одной строкой, с причиной в обе стороны:
`🔧 обновляю /X — <что споткнулось>` (чинить В ТОМ ЖЕ заходе) · `📝 обновлю не сейчас — <причина>, строка легла в <адрес>` · `✅ /X обновлять не надо — <почему именно: прошло без заминки / заминка разовая и внешняя / правка дороже боли>`.

⭐ **ВЕРДИКТОВ ДВА, НЕ ОДИН** (dev 13.09, голосом). Второй вердикт: **собственная инструкция того, кто сейчас работал** (рутина `scheduled-tasks/<имя>/SKILL.md`, сид, хук): «не стоит ли переписать мою инструкцию на будущее, чтобы она была качественнее?». Та же тройка `🔧 обновляю` · `📝 не сейчас` · `✅ не надо`, всегда с причиной. ⚠️ Замер 13.09: рутина `devto-publish-rhythm` починила СВОЙ файл и смолчала про скилл `/comments`, где висел ПРОТИВОПОЛОЖНЫЙ гейт, правило исполнилось наполовину, и спрашивать пришлось оператору. Канон живёт в СКИЛЛЕ, рутина держит только специфику прогона: разошлись, значит правду в скилл, а из рутины указатель. Канон: [[routine-judges-its-own-instruction-too]], CLAUDE.md §9.3-бис.
Пустое «не надо» вердиктом не является. ⛔ Не путать с `/skill-gap` (тот про скилл, которого НЕТ) и не право раздувать: АК-47 в силе — правка снимает ПЕРЕЖИТУЮ боль, не гипотетическую.
Канон: Библия `reglament-polzuemsya-skillom-srazu-sudim-nado-li-ego-obnovit` · CLAUDE.md §9.3-бис · [[skill-used-judge-if-it-needs-update]].

## Шаг 4 — КОРЕНЬ → починить → перепрогнать
⭐ СНАЧАЛА ГЕЙТ ТРЕТЬЕЙ ПОЛОМКИ (dev 09-10.08, CLAUDE.md §5.10): поломка объекта ВНЕ области этой задачи → НЕ чинить. До выбора имени класса обязательно вызови `python "$HOME/.claude/scripts/prior_art.py" class "<описание поломки своими словами>"`: `exit 3` означает найденный prior art, а не ошибку. Напечатанную `СЕМЬЯ <slug>` используй как `--class`. ⭐ ЧИТАЙ СТРОКУ «СЕМЕЙНЫХ: N · СЛОВЕСНЫХ: M», А НЕ ЧИСЛО ХИТОВ (правка прибора 05-06.10.2026): в счёт §5.10 идут ТОЛЬКО семейные. `СЕМЕЙНЫХ 0` при любом M = скорее всего 1-й случай; имя класса бери по предмету ремонта ЭТОЙ поломки, а из раздела `[словесное совпадение]` имя НЕ брать — там рядом лежат чужие дефекты, совпавшие обрывками слов. Видишь глазами, что словесные строки — одна семья с твоей → допиши семью в `FAMILIES` внутри `prior_art.py` ОДНОЙ строкой (и обязательна красная проба в обе стороны), иначе следующая сессия снова назовёт дефект «первым». При `exit 0`, когда прежней строки нет, назови класс по текущему предмету ремонта/нарушенному инварианту и запиши как 1-й датированный случай; канал, код возврата, текст алерта и симптом классом не являются.

Только после этого запиши случай дверью `python "$HOME/.claude/scripts/selfheal.py" journal --class <класс> --what "..." --conditions "..." --parts "..." --guess "..."` — рукописная строка в Breakage-Journal.md НЕВИДИМА счётчику (journal_rows считает только |-таблицу; замер 21.08: 27 рукописных строк browser-rail-down не подняли ни одной починки). Счёт бери из фактического ответа двери: дедуп означает, что новой строки нет.

На 3-й датированной строке, а также сразу для KEEP-ядра, потери данных, безопасности, денег или совравшего прибора, корень НЕ разбирай внутри `/tt`: используй ровно одну отдельную ВИДИМУЮ repair-сессию, и её первый явный вызов обязан быть `/five-whys <класс>` в Claude или `$five-whys <класс>` в Codex, с датированными строками серии. Если `selfheal.py` уже поставил такую сессию в очередь, вторую не создавай. Первый/второй рядовой случай, доказанная простая причина и единичный внешний сбой в `/five-whys` не идут.

⭐⭐ **СПЕРВА СПРОСИ У НАЗВАННОЙ ДВЕРИ, РАБОТАЛА ЛИ ОНА ХОТЬ РАЗ** (замер 06.10.2026). Вердикт «у нас не было двери/сторожа/автоматики» — такой же CLAIM, как причина. Дверь может СУЩЕСТВОВАТЬ, иметь тест и счётчик — и **фейл-клозиться на каждом вызове**, печатая правдоподобное «занято» (`BUSY`, `held by`, `blocked`, `skip`). Такая строка читается как ЗАКОННАЯ причина подождать, оператор уходит делать руками, и класс закрывается в отчёте как «сделано вручную» — а ручная работа потом протухает бесшумно.

Проверка одной строкой: открой счётчик двери и найди хотя бы одну строку с `ok`/`outcome: ok`. Сплошные `busy`/`skip`/`blocked`/`lease-error` = дверь заперта, **и предмет ремонта — замок, а не отсутствие двери**. ⚠️ Сильнейшая улика запертой двери — фраза «сделали руками» в истории объекта: никто не делает руками то, что работает само.

Замер, породивший шаг: `codex_skills_bridge.py sync` отбивался `held by <directory-requires-opt-in>` при КАЖДОМ прогоне, потому что `workspace_write_lease.acquire_many([КАТАЛОГ])` требует `dir_lease=True` + непустой `dir_reason`, а их не передавали. Из-за этого полки скиллов Cursor и Codex мирили руками, и Cursor **две недели жил вообще без семьи `continue`**. Два аргумента в одной строке: cursor 216→286 из 286, codex 218→286, висячих junction 48→0 за один прогон. Та же форма сидела в приёмке: 4 из 5 провалов `_test_codex_skills_bridge.py` были этим же лизом, и их читали как «среда шалит». Канон: [[automated-door-can-be-locked-shut]], пара к [[instrument-is-a-claim-too]] и [[detector-without-executor]] (там исполнителя нет, тут он есть, но без права исполнять).

⭐ ИМЯ КЛАССА = ПРЕДМЕТ РЕМОНТА, НЕ КАНАЛ (CLAUDE.md §5.10, 02.09): не бери в `--class` симптом сторожа, код возврата или «красную строку» — проверь фразой «починю — класс закроется НАВСЕГДА?». «Нет, завтра приедет другой предмет» = это очередь под видом дефекта, дроби по предмету (`<цель>-<тег>`). Замер: 32 разных робота сидели в одном `dead-scheduled-task`, счёт не опускался ниже порога и две настоящие починки его не закрыли [[breakage-class-is-a-defect-not-a-channel]].
Любой провал шагов 1-3 (= артефакт ЭТОЙ задачи) → копай в КОРЕНЬ ([[fix-root-cause-not-symptoms]]), не лепи заплатку на симптом, почини КЛАСС → вернись на Шаг 1 и перепрогони, пока чисто. Safety-critical (локи/синк/auth/scheduler/идемпотентность) → «прочитай прежде чем чинить» + мини-тест ([[verify-existing-before-proposing]]).

## Шаг 4.5 — РАЗРЫВ СЕССИИ: считаем сигналы (ТЕНЬ с 2026-07-28, оператор «+»)
Нашёл баг на шагах 1-3 и он не чинится с ходу — прежде чем зарываться, посчитай 4 сигнала и **залогируй**:
```
python ~/.claude/scripts/split_rule.py log --what "<что чиним>" --attempts <провалившихся попыток> \
   --files <файлов в корне> --repro-min <минут на воспроизведение> --context-pct <% контекста> \
   [--shared] --decision stay|split --minutes <итого> --note "<комментарий>"
```
Правило (пока ТЕНЬ, решение всё равно твоё): выносить в отдельную сессию, если сработал ЛЮБОЙ сигнал —
**A** ≥2 провалившихся попытки · **B** корень >2 файлов или задета смежная система (шина/канон/планировщик/auth) ·
**C** воспроизведение >10 мин · **D** контекст съеден ≥70%.
Выносишь — сид-промпт обязателен (что делали · чего достигли · что уже отвергнуто и почему · критерий приёмки ·
не-цели), задача в `10-Tasks`, артефакт помечается ⚠️, а не ✅. Тень без записей = правило НЕ проверено;
сводка `split_rule.py summary --days 14`, критерии флипа в `00-System/Split-Rule-Shadow.md`.

## Шаг 4.9 — ⭐⭐ ВТОРОЙ ЗАХОД: «готово» — такой же CLAIM, как причина (dev 13.09.2026, две голосовые подряд)
Дословно: «когда ты сделал тесты, всё проверил и думаешь, что всё работает — сделай тест ещё раз. Часто бывает: ты говоришь, что всё работает, а на самом деле нихера не работает. И когда я спрашиваю „а ты точно всё починил?" — оказывается „ой, нет, что-то не сделал"».

⚠️ ЗАМЕР АРХИВА 15.08→14.09.2026 (3613 транскриптов): **57 реплик-сомнений оператора в 36 сессиях, 21 из них — сразу после моего claim'а готовности**. Самая частая форма — голое «проверь ещё раз» и «ТЫ УВЕРЕН???????????». Класс датирован многократно, механизм по §5.10 законен.

Шаги 1-3 зелёные — это ПЕРВЫЙ заход. Слово «готово» произносится только после ВТОРОГО, и второй обязан отличаться от первого, иначе он повторяет ту же слепоту:

1. **От ТРЕБОВАНИЯ, а не от кода.** Выпиши списком, что просили (по словам оператора/сида, не по своему пересказу), и против КАЖДОГО пункта поставь улику: живой вывод, счётчик, строку файла. Пункт без улики = не сделан, даже если помнишь, что делал его. Именно тут ловится «сделано на 2/3».
2. **ДРУГИМ методом.** Повтор той же команды вторым заходом НЕ является. Смени угол: прочитай изменённое место С ДИСКА вместо памяти о правке · спроси ПОТРЕБИТЕЛЯ вместо производителя · посчитай прибором то, что первый раз смотрел глазами · глянь артефакт с чужой стороны провода.
3. **Ровно те места, что чинил.** Не общее здоровье системы: изменение реально на диске? доехало до потребителя? СТАРОЕ поведение исчезло (а не соседствует с новым)?
4. **Свой ПРИБОР — тоже объект второго захода.** Первый замер этого самого правила дал 475 «случаев»; второй заход по прибору показал, что в выборку попали системные вставки харнеса, и честное число — 57. Зелёный счётчик, посчитавший не то, хуже отсутствия счётчика.
5. **Назови, чего НЕ проверял.** Строка «проверено: … · НЕ проверено: … (почему)» обязательна. Честное «эту половину не трогал» — нормальный результат; умолчание — ложное «готово».
6. **Критичное → ТРЕТИЙ заход, чужими глазами** (деньги · необратимое · раскатка на флот · исходящее третьим лицам · публикация · секреты · правка канона): панель Шага 2.5, другой узел или другой инструмент.

⛔ Пока Шаг 4.9 не пройден, запрещены слова «всё работает» · «готово» · «починил» · «✅». Максимум — «первый прогон зелёный, иду на перепроверку». Вердикт ✅ без предъявленного второго захода = максимум ⚠️.
Канон: CLAUDE.md §4.3-бис · Библия `reglament-gotovo-dokazyvaetsya-vtorym-zahodom` · [[done-is-a-claim-recheck-twice]]; блок для рутин — `~/.claude/scripts/routine-recheck-block.md` (раскатка `routine_discipline_apply.py --block=recheck`).

## Шаг 5 — ВЕРДИКТ с доказательством
Короткая таблица: **что проверено · как (живой вывод) · ✅/⚠️/❌**. Затем одна итоговая строка:
- ✅ **PASS** — прогнал, ломал, видно — работает. ТОЛЬКО это = «готово».
- ⚠️ **PARTIAL** — работает, но есть жёлтый флаг (назови его + что осталось).
- ❌ **FAIL** — не работает / не видно → корень + что чиню.
Доказательство (вывод/счётчик/скрин) обязательно — без него «✅» не считается.
⭐ **Второй заход (Шаг 4.9) предъявлен строкой** «перепроверил так-то, нашёл/не нашёл то-то» — иначе вердикт максимум ⚠️, каким бы зелёным ни был первый прогон.

**🪞 Гейт льстящего вывода (до того, как назвать вердикт).** Вывод, к которому пришёл, — ВЫГОДЕН ли он мне? (закрывает работу · объясняет неудачу не нашей виной · ставит нас впереди · разрешает не делать неприятное · подтверждает то, во что уже верили).

Да → усилить проверку, а не ослабить: ОДНА НЕЗАВИСИМАЯ улика сверх той, что уже есть.
Прибор: `python ~/.claude/scripts/self_serving_gate.py --check "<вывод>"` (`--ru` печатает чек-лист).

**Потолки вердикта (жёлтый максимум, даже если всё остальное зелёное):** явный скип второго мнения
(Шаг 2.5) · нет теста/дока/счётчика (Шаг 3.5) · **автономный цикл без названного и проверенного
backpressure (Шаг 3.6)** · не раздано на флот (Шаг 3.7). Автономный цикл БЕЗ потолка итераций —
не ⚠️, а ❌: это единственный случай, когда отсутствие давления валит вердикт сразу.

**🌍 Мировой потребитель (декрет оператора 24.08.2026):** вердикт ✅ на починке КЛАССА (чужой может воспроизвести симптом без наших внутренностей) → в ТОМ ЖЕ заходе прогнать скилл **`/share-fix`** (реверс-поиск по дословному симптому → 3-5 лучших живых тредов → gist → вахта pr_watch). Вердикт обязателен: 🟢 раздал (ссылки) · ⚪ искал-пусто · ⛔ непереносимо/приватно+причина; молчание запрещено. Механика целиком в `/share-fix` — тут только вызов и вердикт. Канон: `reglament-pochinil-u-sebya-srazu-razday-miru` + память `fixed-it-share-it-with-the-world`.

**📋 Журнал задач (декрет оператора 2026-07-04):** вердикт ✅ = момент закрытия в реестре задач ([[task-journal-done-undone-linking]]): если проверенная вещь числится в реестре — отметь `done` с ЭТИМ доказательством + линк, что она разблокировала; ❌/⚠️ = задача остаётся open (хвост «дочинить X» — в реестр сразу). С машины без движка — `bus_send.py` TASK/DONE. Одна строка в докладе: «📋 журнал: #id → done (доказательство: …)».

---

## Связка с /retro (аудит, не дубль)
`/tt` тестирует на каждой задаче (горячо). `/retro` в конце сессии лишь **АУДИТит** строку «протестировано? ✅/❌» по каждому артефакту и, если ❌ — флагает и предлагает прогнать `/tt` сейчас. Ретро само проверку НЕ делает (поздно/холодно). Не дублируем: каждый уровень ссылается вниз (AK-47).

## Границы / не-дубль
- markdown-only тонкий оркестратор; НЕ сервер/БД/вебхук (если правда нужен > markdown — флаг ⚠️ УСЛОЖНЕНИЕ, решает оператор).
- read-only/dry-run где есть побочки; запись в волт — бэкап-первым ([[vault-backup-rule]]).
- Если сессия ничего не собрала — скажи прямо «тестировать нечего», без церемонии.

<!-- PANEL-DELIVERY-CHECK v1 · 29.09.2026 · GIT-S4 заход 15 -->
⛔ **ПАНЕЛЬ МОЖЕТ ОТРАПОРТОВАТЬ СЕМЬИ, НЕ ПОКАЗАВ ИМ ПРЕДМЕТ.** Прогнал второе мнение —
прежде чем считать заход состоявшимся, прочитай ОТВЕТЫ, а не итоговую строку: если
рецензенты пишут «кода/диффа не прислали», предмет не уехал, и «N независимых семей» —
зелень поверх ревью, которого не было ([[instrument-is-a-claim-too]]).
Известный случай: `secondop.py t3 --task <файл>` отправляет движкам только `--context`;
тело задачи клади в `--context`. Панель без доставленного предмета = скип, максимум ⚠️.


ARGUMENTS: ste_score.py + ste_directive.md + llm_ask.py --ste (канарейка ASD-STE100)

---

> `Bash` -- {"command": "cd /c/Users/dev/.claude/scripts && echo \"=== prior_art build (поздно, но честно) ===\"; python prior_art.py build simplified technical english readability 2>&1 | tail -8; echo; echo \"=== help_flag_lint ===\"; python help_flag_lint.py --check ste_score.py 2>&1 | tail -4; echo \"rc=$?

---

> `Bash` -- {"command": "cd /c/Users/dev/.claude/scripts && echo \"=== substr_lint ===\"; python substr_lint.py ste_score.py llm_ask.py _test_ste_score.py 2>&1 | tail -12; echo \"rc=$?\"; echo; echo \"=== vacuous_green ===\"; python vacuous_green.py scan ste_score.py 2>&1 | tail -8; echo \"rc=$?\"", "descript

---

**Claude:**

Я сам наступил на грабли, о которых предупреждает шаг 2: `$?` после пайпа принадлежит `tail`. Перечитываю коды без пайпа.

---

> `Bash` -- {"command": "cd /c/Users/dev/.claude/scripts && python help_flag_lint.py --check ste_score.py > /tmp/hfl.txt 2>&1; echo \"help_flag_lint rc=$?\"; head -12 /tmp/hfl.txt; echo \"======\"; python substr_lint.py ste_score.py _test_ste_score.py > /tmp/sl.txt 2>&1; echo \"substr_lint (только мои файлы) 

---

**Claude:**

Настоящая находка: `--help` у прибора зависит от импортов, которые идут раньше. Чиню по предписанию линта.

---

> `Bash` -- {"command": "cd /c/Users/dev/.claude/scripts && python - <<'PYEOF'\nimport io\np = \"ste_score.py\"\ns = io.open(p, encoding=\"utf-8\").read()\nold = '''import argparse\nimport json\nimport os\nimport re\nimport sys\n\nHERE = os.path.dirname(os.path.abspath(__file__))'''\nnew = '''import argparse\

---

**Claude:**

Поведение верное, но линт всё равно красный. Его вердикт — тоже claim; читаю, что он на самом деле ищет.

---

> `Bash` -- {"command": "cd /c/Users/dev/.claude/scripts && grep -n \"work-at-import\\|work_at_import\" help_flag_lint.py | head -10", "description": "Что именно ловит work-at-import"}

---

> `Bash` -- {"command": "cd /c/Users/dev/.claude/scripts && sed -n '225,250p' help_flag_lint.py", "description": "Читаю детектор"}

---

> `Bash` -- {"command": "cd /c/Users/dev/.claude/scripts && python - <<'PYEOF'\nimport io\np = \"ste_score.py\"\ns = io.open(p, encoding=\"utf-8\").read()\nold = '''HERE = os.path.dirname(os.path.abspath(__file__))\nfor _c in (os.path.join(HERE, \"_shared\"),\n           os.path.join(os.path.expanduser(\"~\")

---

**Claude:**

Теперь панель — чужие глаза на сам код (Шаг 2.5). Кладу в контекст ЖИВОЙ код, не пересказ.

---

> `Bash` -- {"command": "cd /c/Users/dev/.claude/scripts && python - > /tmp/panel_ctx.txt <<'PYEOF'\nimport io\ndef hot(path, start, end=None, limit=6000):\n    s = io.open(path, encoding=\"utf-8\").read()\n    i = s.find(start)\n    if i < 0:\n        return \"=== %s: маркер %r НЕ НАЙДЕН ===\\n\" % (path, st

---

> `Bash` -- {"command": "cd /c/Users/dev/.claude/scripts && CTX=\"$(cat /tmp/panel_ctx.txt)\" && python cc-review/secondop.py panel --ritual tt --task ste-score-20261007 --context \"$CTX\" > /tmp/panel_out.txt 2>&1; echo \"panel rc=$?\"; tail -40 /tmp/panel_out.txt", "description": "Панель чужих глаз на код п

---

> `Bash` -- {"command": "cd /c/Users/dev/.claude/scripts && git ls-files --error-unmatch ste_score.py > /dev/null 2>&1; echo \"под git: rc=$? (0=да, иное=нет)\"; echo \"=== coverage_map ===\"; python coverage_map.py > /tmp/cm.txt 2>&1; echo \"rc=$?\"; grep -iE \"ste_score\" /tmp/cm.txt | head -5", "descriptio

---

> `Bash` -- {"command": "cd /c/Users/dev/.claude/scripts && python - <<'PYEOF'\nimport io\nfor p, who in ((\"ste_score.py\", None), (\"_test_ste_score.py\", None)):\n    s = io.open(p, encoding=\"utf-8\").read()\n    if \"АВТОР ПРАВКИ:\" in s:\n        print(p, \"подпись уже есть\")\n        continue\n    old

---

> `Bash` -- {"command": "cd /c/Users/dev/.claude/scripts && python change_ledger.py add --actor \"claude@HUB-01\" --operator \"dev\" --session \"voice001-ste100-20261007\" --tool \"claude-code\" --target \"~/.claude/scripts/ste_score.py, ste_directive.md, _test_ste_score.py, _shared/_probe_ste_latin.

---

**Claude:**

Шаг 4.9 — второй заход ДРУГИМ методом: читаю с диска, а не из памяти о правке.

---

> `Bash` -- {"command": "echo \"=== 1. флаг РЕАЛЬНО в боевом llm_ask на диске? ===\"; grep -c '\"--ste\"' /c/Users/dev/.claude/scripts/llm_ask.py; echo \"=== 2. дефолт точно ВЫКЛ (None)? ===\"; grep -n 'add_argument(\"--ste\"' -A1 /c/Users/dev/.claude/scripts/llm_ask.py | head -3; echo \"=== 3. БЕЗ флага пр

---

> `Bash` -- {"command": "cat \"C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_33a90300\\tasks\\brhf99emb.output\" 2>/dev/null | tail -45", "description": "Результат панели"}

---

> `Bash` -- {"command": "cd /c/Users/dev/.claude/scripts && echo \"=== заметка и очередь на диске (перечитываю, а не верю) ===\"; ls -la \"D:\\Vault\\Vault-Knowledge\\03-Insights\\Operations\\experiment-ste100-canary.md\" | awk '{print $5, $9}'; grep -c \"ste100-canary\" \"D:\\Vault\\Vault-Knowledge\\00

---

**Claude:**

Свой же §9.10 нарушил в заметке — 4 полотна. Чиню.

---

> `Bash` -- {"command": "cd /c/Users/dev/.claude/scripts && python paragraph_lint.py \"D:\\Vault\\Vault-Knowledge\\03-Insights\\Operations\\experiment-ste100-canary.md\" 2>/dev/null | head -6", "description": "Все четыре полотна"}

---

> `Bash` -- {"command": "cd /c/Users/dev/.claude/scripts && python - <<'PYEOF'\nimport io\np = r\"D:\\Vault\\Vault-Knowledge\\03-Insights\\Operations\\experiment-ste100-canary.md\"\ns = io.open(p, encoding=\"utf-8\").read()\n\nfixes = [\n(\n\"Суть совета: просить модель отвечать на **ASD-STE100** — упрощён

---

> `Bash` -- {"command": "f=\"C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_33a90300\\tasks\\brhf99emb.output\"; wc -c \"$f\" 2>/dev/null; tail -50 \"$f\" 2>/dev/null", "description": "Панель — проверяю"}

---

> `Bash` -- {"command": "n=0; while [ $n -lt 11 ] && [ ! -s /tmp/panel_out.txt ]; do n=$((n+1)); python -c \"import time;time.sleep(25)\"; done; echo \"ждал ${n}×25с\"; wc -c /tmp/panel_out.txt 2>/dev/null; tail -45 /tmp/panel_out.txt 2>/dev/null", "description": "Дожидаюсь панели"}

---

**Claude:**

Панель нашла настоящий дефект: при нуле судимых предложений прибор печатал `clean_pct = 0.0`. Это «нет данных», выданное за «0% чистых» — ровно класс ложного числа. Чиню.

---

> `Bash` -- {"command": "cd /c/Users/dev/.claude/scripts && cp ste_score.py ste_score.py.bak-pre-nodata-20261007 && python - <<'PYEOF'\nimport io\np = \"ste_score.py\"\ns = io.open(p, encoding=\"utf-8\").read()\n\n# 1) нет судимых -> НЕТ ДАННЫХ, а не ноль процентов\nold = '''    j = res[\"sentences_judged\"]\

---

> `Bash` -- {"command": "cd /c/Users/dev/.claude/scripts && python - <<'PYEOF'\nimport io\np = \"_test_ste_score.py\"\ns = io.open(p, encoding=\"utf-8\").read()\nold = '''ok(\"5c русский: балл не выдуман\", ru[\"clean_pct\"] == 0.0, ru[\"clean_pct\"])'''\nnew = '''# ⛔ НЕ 0.0: находка панели codex 07.10. Ноль 

---

> `Bash` -- {"command": "cd /c/Users/dev/.claude/scripts && python red_proof.py --file ste_score.py \\\n --old 'res[\"clean_pct\"] = round(100.0 * res[\"clean\"] / j, 1) if j else None' \\\n --new 'res[\"clean_pct\"] = round(100.0 * res[\"clean\"] / j, 1) if j else 0.0' \\\n --expect-fail '{py} -c \"import sy

---

> `Bash` -- {"command": "cd /c/Users/dev/.claude/scripts && python - <<'PYEOF'\nimport io\np = \"ste_score.py\"\ns = io.open(p, encoding=\"utf-8\").read()\nold = '''   ⛔ НЕ «поднимай покрытие», ослабляя языковой фильтр: именно так выглядел баг, починенный\n   07.10 (русская фраза с английскими терминами прохо

---

> `Bash` -- {"command": "cd /c/Users/dev/.claude/scripts && python help_flag_lint.py --check ste_score.py > /tmp/g1 2>&1; echo \"help_flag_lint rc=$?\"; python ste_score.py --help > /tmp/g4 2>&1; echo \"--help rc=$?\"; python ste_score.py --self-test > /tmp/g5 2>&1; echo \"самотест rc=$?\"; tail -1 /tmp/g5", 

---

> `Bash` -- {"command": "cd /c/Users/dev/.claude/scripts && timeout 100 python ste_score.py --self-test > /tmp/g5 2>&1; echo \"самотест rc=$?\"; tail -1 /tmp/g5", "description": "Самотест с жёстким лимитом"}

---

> `Bash` -- {"command": "cd /c/Users/dev/.claude/scripts && timeout 110 python help_flag_lint.py --check ste_score.py > /tmp/g1 2>&1; echo \"help_flag_lint rc=$?\"; head -2 /tmp/g1", "description": "help_flag_lint ещё раз"}

---

> `Bash` -- {"command": "cd /c/Users/dev/.claude/scripts && timeout 110 python ste_score.py --help > /tmp/g4 2>&1; echo \"--help rc=$?\"; head -1 /tmp/g4; timeout 110 python vacuous_green.py scan ste_score.py > /tmp/g3 2>&1; echo \"vacuous_green rc=$?\"", "description": "--help и vacuous_green"}

---

> `Bash` -- {"command": "cat /tmp/g1 2>/dev/null | head -3; echo \"---\"; cat \"C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_33a90300\\tasks\\b65ytxic9.output\" 2>/dev/null | tail -3", "description": "Результат help_flag_lint"}

---

> `Bash` -- {"command": "cd /c/Users/dev/.claude/scripts && timeout 500 python help_flag_lint.py --check ste_score.py > /tmp/g1b 2>&1; echo \"help_flag_lint rc=$?\"; head -2 /tmp/g1b", "description": "help_flag_lint с большим окном", "run_in_background": true}

---

> `Bash` -- {"command": "n=0; f=\"C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_33a90300\\tasks\\bo78cj8e9.output\"; while [ $n -lt 10 ] && ! grep -q \"exited with code\" \"$f\" 2>/dev/null; do n=$((n+1)); python -c \"import time;time.sleep(25)\"; done

---

> `Bash` -- {"command": "f=\"C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_33a90300\\tasks\\bo78cj8e9.output\"; cat \"$f\" 2>/dev/null | head -5; echo \"--- завершился: $(grep -c 'exited with code' \"$f\" 2>/dev/null) ---\"", "description": "Проверяю л

---

> `Bash` -- {"command": "tail -12 /tmp/panel_out.txt; echo \"=== ВРЕМЯ ===\"; TZ=Europe/Lisbon date '+LISBON %H:%M'; TZ=Europe/Moscow date '+MSK %H:%M'", "description": "Хвост панели и время"}

---

**Claude:**

Панель догрузилась через OpenRouter и дала ещё три находки. Две — настоящие дефекты того же класса «прибор врёт о причине». Третью (порог 0.75) назвали ДВА независимых движка, значит её решаю замером, а не на глаз.

---

> `Bash` -- {"command": "cd /c/Users/dev/.claude/scripts && python - <<'PYEOF'\nimport io\np = \"ste_score.py\"\ns = io.open(p, encoding=\"utf-8\").read()\nold = '''    letters = LETTER_RE.findall(sent)\n    latin = LATIN_RE.findall(sent)\n    if cyr and len(words) / float(len(words) + len(cyr)) < 0.75:'''\n#

---

> `Bash` -- {"command": "D=/c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_33a90300/scratchpad/ste; cd /c/Users/dev/.claude/scripts && echo \"=== цена строгости на англоязычных ответах рельс (то, ради чего прибор) ===\"; for f in c-off c-on g-off g-on; do prin

---

> `Bash` -- {"command": "cd /c/Users/dev/.claude/scripts && python - <<'PYEOF'\nimport io\np = \"_test_ste_score.py\"\ns = io.open(p, encoding=\"utf-8\").read()\nold = '''mixed = ste_score.score(\"Open the valve now please. Это русское предложение внутри текста.\")'''\nnew = '''# --- находки ПАНЕЛИ 07.10 (cod

---

> `Bash` -- {"command": "cd /c/Users/dev/.claude/scripts && timeout 60 python - <<'EOF'\nimport sys\nsys.path.insert(0, \".\")\nimport ste_score as s\nr = s.score(\"12345 67890 11111. /usr/bin/python3 /opt/x. 3.14 2.71 1.41.\")\nprint(\"причины:\", r[\"unjudged_reasons\"])\nprint(\"всего предложений:\", r[\"s

---

**Claude:**

Моё утверждение было неверным, не код: `/usr/bin/python3` несёт буквы и потому судится. Правлю утверждение по замеру и называю границу.

---

> `Bash` -- {"command": "cd /c/Users/dev/.claude/scripts && python - <<'PYEOF'\nimport io\np = \"_test_ste_score.py\"\ns = io.open(p, encoding=\"utf-8\").read()\nold = '''ok(\"5h ветка «нет букв» ДОСТИЖИМА (панель gemini: была мёртвой)\",\n   num[\"unjudged_reasons\"].get(\"нет букв (формула, путь, число)\", 

---

> `Bash` -- {"command": "f=\"C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_33a90300\\tasks\\bo78cj8e9.output\"; echo \"=== help_flag_lint (большое окно) ===\"; cat \"$f\" | head -4; echo \"=== финальные гейты ===\"; cd /c/Users/dev/.claude/scripts &&

---

> `Bash` -- {"command": "cat \"C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_33a90300\\tasks\\bo78cj8e9.output\" 2>/dev/null | head -5", "description": "Результат линта с большим окном"}

---

> `Bash` -- {"command": "cd /c/Users/dev/.claude/scripts && python - <<'PYEOF'\nimport io\np = r\"D:\\Vault\\Vault-Knowledge\\03-Insights\\Operations\\experiment-ste100-canary.md\"\ns = io.open(p, encoding=\"utf-8\").read()\n\nold = \"\"\"## Два дефекта, найденных по дороге\"\"\"\nnew = \"\"\"## Замер 4 — 

---

> `Bash` -- {"command": "cd /c/Users/dev/.claude/scripts && python - <<'PYEOF'\nimport io\np = r\"D:\\Vault\\Vault-Knowledge\\03-Insights\\Operations\\experiment-ste100-canary.md\"\ns = io.open(p, encoding=\"utf-8\").read()\nold = \"В панель уехал ЖИВОЙ код горячих функций (9287 байт), не пересказ. Ответил

---

> `Bash` -- {"command": "cd /c/Users/dev/.claude/scripts && python - <<'PYEOF'\nimport io\np = r\"C:\\Users\\dev\\.claude\\projects\\P---WORKDIR-HUB\\memory\\ste100-is-a-knob-not-a-certificate.md\"\ns = io.open(p, encoding=\"utf-8\").read()\nreps = [\n(\"Тест `_test_ste_score.py` 38/38, список 

---

> `Bash` -- {"command": "cd /c/Users/dev/.claude/scripts && timeout 110 python rail_plan.py verdict > /tmp/rv.txt 2>&1; echo \"rail_plan rc=$?\"; cat /tmp/rv.txt | head -14; echo \"=== ВРЕМЯ ===\"; TZ=Europe/Lisbon date '+LISBON %Y-%m-%d %H:%M'; TZ=Europe/Moscow date '+MSK %H:%M'", "description": "Вердикт по 

---

**Claude:**

**02:29 Лиссабон / 02:29 МСК** · узел HUB-01

**🚂 План рельс был объявлен на старте:** сам как Claude — оркестрация, прибор, дверь, волт, `/tt`. Наружу — codex, grok, gemini. Факт по `rail_plan.py verdict`: codex 33 вызова, gemini 12, glm 8. Чужие баки горели по делу.

---

## Канарейку поставил. Она работает, но не так, как обещает пост

Канарейка стоит на **чужих рельсах** (`codex`, `grok`, `gemini`, `GLM`, OpenRouter), не в твоих ответах. Причина простая: они и так отвечают по-английски, врезка одна, замер детерминирован, наружу не уходит ничего.

В твои ответы STE не ставлю — ты читаешь по-русски, а ASD-STE100 английский стандарт. Тот же принцип у нас уже закрыт §9.10, ELI5 и `/ai-slop`.

**Дверь:** `llm_ask.py --ste [80]`. **По умолчанию ВЫКЛЮЧЕНА** — без флага промпт не меняется ни на байт. Откат = не давать флаг.

---

## Замер 1 — база на 258 ЖИВЫХ ответах рельс (не фикстура)

```
предложений судимо 917 из 2223 · слов 15638 · средняя длина 17.1 · самое длинное 192
ЧИСТЫХ предложений 44.3%  (порог STE-80) → FAIL
длиннее 20 слов: 233 · пассив: 112 · -ing: 253 · цепочки сущ.: 213
неутверждённых слов: 103 → verify x46, additional x10, requires x7, leverage x4, prior to x3
абзацев длиннее 6 предложений: 82 из 445
покрытие судимости 41% → СЛЕПОЙ (остальное русский текст, формулы, обрывки)
```

## Замер 2 — A/B: один вопрос, одна рельса, разница ТОЛЬКО в директиве

**codex** (усилие xhigh не понижал):

| метрика | без директивы | с `--ste 80` | дельта |
|---|---|---|---|
| ЧИСТЫХ предложений, % | 9.5 | 56.7 | **+47.2 п.п.** |
| средняя длина предложения | 20.4 | 13.4 | **−7.0** |
| длиннее 20 слов | 10 | 1 | −9 |
| пассив | 2 | 0 | −2 |
| слов всего | 428 | 403 | −25 |
| неутверждённых слов | 4 | 6 | **+2 ⚠️** |

**grok:**

| метрика | без директивы | с `--ste 80` | дельта |
|---|---|---|---|
| ЧИСТЫХ предложений, % | 52.0 | 78.9 | **+26.9 п.п.** |
| средняя длина предложения | 16.0 | 12.1 | −3.9 |
| пассив | 2 | 0 | −2 |
| неутверждённых слов | 1 | 0 | −1 |
| слов всего | 401 | 459 | **+58 ⚠️** |

## Замер 3 — ломает ли директива ФОРМАТ (это назначенный kill-риск)

Дал codex задание, которое обязано кончаться строкой `VERDICT: ACCEPT|BLOCK` — тот самый контракт, на котором держится `secondop`. **Тег остался на месте**, последняя строка `VERDICT: BLOCK`, ничего после неё. Это 1 случай из 5, нужных для закрытия метрики.

---

## Пять вещей, которые я узнал, и три из них против восторга

1. **По ФОРМЕ ручка работает сильно и сразу.** Предложения короче, пассив уходит в ноль.
2. **Порог «80% как ASD-STE100» просьбой НЕ берётся.** codex 56.7%, grok 78.9% — ни один не дошёл.
3. **Словарь директива не чинит вовсе.** У codex неутверждённых слов стало БОЛЬШЕ (4→6). Модель знает про короткие фразы, но подменять слова на утверждённые не умеет — словаря у неё нет, как и у нас.
4. **Объёма ручка НЕ экономит.** codex −6%, grok **+14%**. Кто ждёт «ответы станут компактнее» — ждёт не того.
5. **Дельта тем больше, чем хуже база.** Значит флаг имеет смысл ставить адресно, на разливающуюся рельсу, а не на все разом.

**Цена:** директива +1676 байт в промпт. Обе рельсы при xhigh медленные сами (73–88 с на тривиальный промпт, 712 с на заказ «400 слов»). Первая попытка с таймаутом 420 с дала четыре таймаута — и это было «не смог проверить», а не «рельса мертва»: живая проба в тот же час вернула ALIVE.

---

## Шесть дефектов нашли по дороге, все закрыты

**Своими прогонами (3):**

| что | корень | улика |
|---|---|---|
| прибор врал о ПРИЧИНЕ | русское предложение отвергалось как «короче 3 слов», потому что проверка длины шла раньше проверки языка | красное `red_proof.py` |
| фикстуры зелёные, живой прогон красный | судимость считалась по БУКВАМ, а русские слова выпадали из токенов и склеивали английские термины — 34 фальшивые цепочки на одном ДР-отчёте, чистых 31.4% вместо 75.8% | живой прогон |
| `--help` зависел от тяжёлых импортов | цикл на уровне модуля = работа до разбора аргументов | `help_flag_lint` rc=1 → rc=0 |

**Панелью чужих глаз (3) — 5 независимых семей, в контекст уехал ЖИВОЙ код:**

| что | кто нашёл | цена, названная числом |
|---|---|---|
| `clean_pct = 0.0` при нуле судимых — «не мерил» выдавалось за «0% чистых», гейт валил неизмеренный текст | codex | стало `None` + «НЕТ ДАННЫХ», `--fail-under` на None не срабатывает |
| ветка «нет букв» НЕДОСТИЖИМА | gemini/OpenRouter | причина врала в **242 из 288** вердиктов «короче 3 слов» на корпусе |
| смешанное предложение звалось английской прозой | codex **И** OpenRouter/gpt независимо | порог поднят 0.75 → **0.9 ЗАМЕРОМ**: корпус 951→917 судимых, на целевых англоязычных ответах — **ноль изменений** |

Grok в панели отвалился по таймауту 240 с, gemini — по квоте 429.

---

## 🧪 `/tt` — вердикт: ⚠️ **PARTIAL**

| что проверено | как | итог |
|---|---|---|
| прогон на реальных данных | 258 живых ответов рельс + 4 живых прогона рельс | ✅ |
| сторож | `_test_ste_score.py` **50/50**, самотест 11/11 | ✅ |
| красное на сломанном коде | **5 поломок** через `red_proof.py`, 2 дефекта найдены ДО починки | ✅ |
| панель чужих глаз | 5 независимых семей, 3 находки, все закрыты в том же заходе | ✅ |
| счётчики §5.8 | `ste_score` 35 строк, `llm_ask_ste` строка с `args_len=80` — прочитаны из шарда | ✅ |
| гейты | `help_flag_lint` 0 · `substr_lint` 0 · `vacuous_green` 0 · `status_claim_lint` 0 · `paragraph_lint` 0 | ✅ |
| дока в коде + подпись автора + леджер правок | docstring с `updated`, строка в `change_ledger` (деталь вне git) | ✅ |
| второй заход другим методом | перечитал флаг и дефолт С ДИСКА, замерил байты промпта с/без флага | ✅ |
| слепая зона | `blind_zone --run` = **СЛЕПОЙ, покрытие 41%** | ⚠️ |
| раздача на флот | **не раздано — это КАНАРЕЙКА, намеренно только хаб** | ⚠️ |
| формат у ревью-рельс | 1 случай из 5 | ⚠️ |

**Почему не ✅.** Два жёлтых флага сознательные, один открытый.

`СЛЕПОЙ` при покрытии 41% — честный вердикт, и поднимать его я **отказываюсь**: 1018 предложений корпуса русские, их судят `paragraph_lint` и `slop_gate`, а не этот прибор. Повысить покрытие можно только ослабив языковой фильтр — то есть вернув баг, который я сегодня починил. Я вписал это прямо в паспорт прибора, чтобы следующий читатель не «улучшил» его обратно.

Раздачи на флот нет потому, что ты сказал «как канарейка»: один узел, потом замер, потом остальные. Откат назван — не давать флаг.

Открытый флаг один: формат проверен на одном движке из пяти, и твоего вердикта «стало легче читать» ещё нет.

---

## Чего я НЕ взял из твоего поста (не забыл — не взял)

Там три других формата вывода, ни один в эту канарейку не входит:

- **схема вместо текста** — у нас уже есть `/dash` и §2.4 «дашборд по максимуму», отдельной канарейки не требует;
- **«сделай в HTML»** — пересекается с тем же §2.4 и Artifact-рельсой;
- **видео-объяснения в стиле 3Blue1Brown с озвучкой** — это отдельная крупная стройка, пересекается с `/teach-podcast` и `/youtube-publish`. Скажи слово — подниму отдельной сессией.

---

## Урожай 2026-10-21, kill-критерий назван

Строка в `00-System/Shadow-First-Queue.md`, заметка `03-Insights/Operations/experiment-ste100-canary.md`, дорога из `_Experiments-MOC`, оригинал твоего текста дословно в `_originals`, память `ste100-is-a-knob-not-a-certificate`.

Метрики: ≥20 прогонов с `--ste` · дельта ≥+20 п.п. на ≥5 парах · **НОЛЬ** сломанных форматов · твои ≥3 прочитанных ответа. **KILL: дельта <+10 п.п. → флаг выключаем.**

**🛠 Вердикт о скилле:** `✅ /tt обновлять не надо` — прошёл без заминки и поймал три настоящих дефекта (`help_flag_lint`, `paragraph_lint`, панель), которые я бы пропустил. Единственная заминка — я **дважды сам** нарушил его же предупреждение «`$?` после пайпа принадлежит `tail`»; это моя дисциплина, а не дефект инструкции: она об этом написана капсом.

**⚠️ Одной строкой:** `MEMORY.md` 49 КБ при красном пороге — не сжимаю по ходу чужой задачи, это работа ночного оптимизатора (§10.0).

---

🧒 **Простыми словами.** Карпати советует просить робота писать как в инструкции к самолёту: короткие фразы, простые слова. Я сделал ручку, которой это можно включить чужим роботам, и линейку, которая мерит, помогло ли.

Померил на живых ответах. Фразы правда стали короче почти вдвое — читать легче. Но слова робот проще не делает, и текст короче не становится, иногда даже длиннее.

Включается только если я сам попрошу — само ничего не изменилось. Через две недели проверю на деле и скажу, оставляем или выбрасываем.

Пока делал, линейка трижды соврала, и трижды её поймали — один раз мой же тест, один раз живые данные, один раз чужие роботы-проверяльщики. Всё починил.

---

**User:**

<task-notification>
<task-id>by4y67xhv</task-id>
<tool-use-id>toolu_01Sr6G61u57MHBPoM81zdcAL</tool-use-id>
<output-file>C:\Users\dev\AppData\Local\Temp\claude\P---WORKDIR-HUB\s_33a90300\tasks\by4y67xhv.output</output-file>
<status>completed</status>
<summary>Background command "Читаю линт" completed (exit code 0)</summary>
</task-notification>

---

> `Bash` -- {"command": "cat \"C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_33a90300\\tasks\\by4y67xhv.output\" 2>/dev/null | head -6", "description": "Читаю догнавший прогон линта"}

---

**Claude:**

Догнал фоновый прогон, который раньше упирался в таймаут от загрузки машины. Подтверждает уже доложенное, нового нет:

```
help_flag_lint rc=0
OK ste_score.py -- дыры класса unparsed-flag-silently-runs-work нет
```

Вердикт `/tt` не меняется: ⚠️ **PARTIAL** по трём названным флагам (слепая зона 41% — сознательно, флот — канарейка только хаб, формат — 1 случай из 5).

Канарейка стоит и выключена по умолчанию. Урожай 2026-10-21.

🧒 **Простыми словами:** догнала последняя проверка, которая раньше просто не успевала из-за занятой машины. Сказала «всё в порядке» — то же, что я уже говорил. Ничего делать не надо.

**02:33 Лиссабон / 02:33 МСК**

---

**User:**

<task-notification>
<task-id>bp29rou06</task-id>
<tool-use-id>toolu_01XwxGpQ9HGUm9AWaD9LteES</tool-use-id>
<output-file>C:\Users\dev\AppData\Local\Temp\claude\P---WORKDIR-HUB\s_33a90300\tasks\bp29rou06.output</output-file>
<status>completed</status>
<summary>Background command "RECALL: ищу прежние следы ASD-STE100" completed (exit code 0)</summary>
</task-notification>

---

**Claude:**

Досчитал тот самый грep по волту, про который я с самого начала сказал «вывод об отсутствии нельзя делать, пока он жив». Закрываю его честно.

---

> `Bash` -- {"command": "f=\"C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_33a90300\\tasks\\bp29rou06.output\"; wc -c \"$f\"; echo \"--- содержимое ---\"; cat \"$f\"", "description": "Читаю досчитавший RECALL по волту"}

---

**Claude:**

Фоновый RECALL нашёл то, чего не видели ни `prior_art class`, ни `prior_art build`: **решение от 04.10 и ретро от 06.10 ровно про лестницу Карпати**. Это prior art, который я проглядел. Читаю.

---

> `Bash` -- {"command": "sed -n '1,60p' \"D:\\Vault\\Vault-Knowledge\\02-Decisions\\_Inbox\\2026-10-04--lestnica-karpati-4-stupeni-obyasneniy-dlya-sessiy-i-kontenta.md\"", "description": "Читаю решение от 04.10 про лестницу Карпати"}

---

> `Bash` -- {"command": "ls -la \"D:\\Vault\\Vault-Knowledge\\_machine-bus\\_transit\\scripts-from-HUB-01\\ste_score.py\" 2>/dev/null; echo \"--- кто и куда везёт transit ---\"; ls \"D:\\Vault\\Vault-Knowledge\\_machine-bus\\_transit\\\" 2>/dev/null | head -10", "description": "Проверяю, не уехала 

---

**Claude:**

Это серьёзно. Решение от 04.10 уже содержит вывод, который бьёт по моей директиве: автор SimpleEnglish (3717 звёзд) сам опубликовал «почему мой скилл бесполезен — микро-промпт из 8 строк эффективнее». Дочитываю и смотрю ретро от 06.10.

---

> `Bash` -- {"command": "sed -n '60,140p' \"D:\\Vault\\Vault-Knowledge\\02-Decisions\\_Inbox\\2026-10-04--lestnica-karpati-4-stupeni-obyasneniy-dlya-sessiy-i-kontenta.md\"", "description": "Дочитываю решение 04.10"}

---

> `Bash` -- {"command": "sed -n '1,70p' \"D:\\Vault\\Vault-Knowledge\\01-Conversations\\Claude\\Retros\\retro-2026-10-06-Teague-ladder-explain-formats.md\"", "description": "Читаю ретро от 06.10"}

---

**Claude:**

Это крупная находка, и она бьёт по тому, что я построил. Сессия 06.10 уже прошла этот путь и получила ЗАМЕР:

| вариант | слов | предложений | жирного | буллетов |
|---|---|---|---|---|
| без скилла | 249 | 18.9 | 52 | 35 |
| полный скилл, 53 правила | 171 | 13.4 | 24 | 22 |
| **микро-промпт, 8 строк** | **150** | **5.8** | **0** | **0** |

Вывод автора инструмента о собственном продукте: скилл выигрывает только на СВОЁМ линтере. Моя директива — 1676 байт, ~30 правил. Я построил ровно то, что измеренно проигрывает. И мерил своим же линтером — то, от чего предостерегает их durable №1.

Проверяю это, а не верю на слово. Сначала учу прибор считать то, что видит ЧИТАТЕЛЬ.

---

> `Bash` -- {"command": "cd /c/Users/dev/.claude/scripts && python - <<'PYEOF'\nimport io\np = \"ste_score.py\"\ns = io.open(p, encoding=\"utf-8\").read()\n\nold = '''def score(text, max_words=20, max_sent_par=6, cluster_limit=3):\n    res = {'''\nnew = '''def reader_visible(text):\n    \"\"\"Счёт того, что в

---

> `Bash` -- {"command": "cd /c/Users/dev/.claude/scripts && sed -n '336,348p' ste_score.py", "description": "Смотрю битое место"}

---

**Claude:**

Снова наступил на `patch-code-via-file-not-heredoc` — о нём прямо предупреждает `/tt`. Чиню файлом-патчем, как велит канон.

---

> `Write` -- {"file_path": "C:\\Users\\dev\\.claude\\scripts\\_shared\\_patch_ste_reader.py", "content": "#!/usr/bin/env python3\n# -*- coding: utf-8 -*-\n\"\"\"Разовый патч: чинит функцию reader_visible в ste_score.py после мангла heredoc.\n\nПовод: 07.10.2026 escape-последовательности `\\\\n` внутри bash-her

---

> `Bash` -- {"command": "cd /c/Users/dev/.claude/scripts && timeout 110 python _shared/_patch_ste_reader.py; echo \"rc=$?\"; timeout 110 python _test_ste_score.py > /tmp/tr2.txt 2>&1; echo \"тесты rc=$?\"; tail -2 /tmp/tr2.txt", "description": "Применяю патч-файл и перегоняю"}

---

**Claude:**

Теперь микро-промпт как второй стиль директивы и трёхрукавный замер на том же вопросе и той же рельсе.

---

> `Write` -- {"file_path": "C:\\Users\\dev\\.claude\\scripts\\ste_directive_micro.md", "content": "Reply rules. Answer in prose, five sentences maximum, no headers, no bullet lists, no bold, no tables. First sentence answers the question. No em-dashes: write two sentences instead. If you use a technical term, 

---

> `Write` -- {"file_path": "C:\\Users\\dev\\.claude\\scripts\\_shared\\_patch_ste_micro.py", "content": "#!/usr/bin/env python3\n# -*- coding: utf-8 -*-\n\"\"\"Разовый патч: добавляет стиль директивы `micro` в ste_score.py и флаг --ste-style в llm_ask.py.\n\nПовод: ретро 06.10.2026 и решение 04.10.2026 («лестн

---

> `Bash` -- {"command": "cd /c/Users/dev/.claude/scripts && cp ste_score.py ste_score.py.bak-pre-micro-20261007 && cp llm_ask.py llm_ask.py.bak-pre-micro-20261007 && timeout 110 python _shared/_patch_ste_micro.py; echo \"patch rc=$?\"; echo \"=== проверки ===\"; timeout 60 python ste_score.py --directive --st

---

**Claude:**

Микро — 309 байт против 1703. Гоню третий рукав на том же вопросе и тех же рельсах.

---

> `Bash` -- {"command": "D=/c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_33a90300/scratchpad/ste; cd /c/Users/dev/.claude/scripts && python llm_ask.py --prompt-file \"$D/q2.txt\" --rails codex --mode first --timeout 900 --ste 80 --ste-style micro > \"$D/c-mi

---

> `Bash` -- {"command": "D=/c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_33a90300/scratchpad/ste; cd /c/Users/dev/.claude/scripts && python llm_ask.py --prompt-file \"$D/q2.txt\" --rails grok --mode first --timeout 900 --ste 80 --ste-style micro > \"$D/g-mic

---

> `Bash` -- {"command": "D=/c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_33a90300/scratchpad/ste; cd /c/Users/dev/.claude/scripts && echo \"=== ЧИТАТЕЛЬСКИЕ ВЕЛИЧИНЫ на уже собранных рукавах ===\"; for f in c-off c-on g-off g-on; do printf \"%-6s \" \"$f\"; 

---

**Claude:**

Важная деталь: во всех четырёх рукавах жирного и буллетов УЖЕ ноль — потому что мой вопрос прямо просил «400 слов прозы» и тем самым погасил главный эффект, который мерил автор. Нужен вопрос БЕЗ указания формата.

---

> `Bash` -- {"command": "D=/c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_33a90300/scratchpad/ste; cat > \"$D/q3.txt\" <<'EOF'\nOur deploy script copies a file to 8 machines and then reports success. On two of them the\nfile arrived but the service kept running

---

> `Bash` -- {"command": "D=/c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_33a90300/scratchpad/ste; cd /c/Users/dev/.claude/scripts && python llm_ask.py --prompt-file \"$D/q3.txt\" --rails codex --mode first --timeout 900 > \"$D/q3-off.md\" 2>\"$D/q3-off.err\"

---

> `Bash` -- {"command": "D=/c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_33a90300/scratchpad/ste; cd /c/Users/dev/.claude/scripts && python llm_ask.py --prompt-file \"$D/q3.txt\" --rails codex --mode first --timeout 900 --ste 80 --ste-style full > \"$D/q3-fu

---

> `Bash` -- {"command": "D=/c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_33a90300/scratchpad/ste; cd /c/Users/dev/.claude/scripts && python llm_ask.py --prompt-file \"$D/q3.txt\" --rails codex --mode first --timeout 900 --ste 80 --ste-style micro > \"$D/q3-m

---

**Claude:**

Пока рельсы считают — разбираю, почему RECALL промахнулся. Это важнее самой директивы.

---

> `Bash` -- {"command": "cd /c/Users/dev/.claude/scripts && timeout 110 python prior_art.py build Teague ladder explain > /tmp/pa.txt 2>&1; echo \"rc=$?\"; grep -iE \"поверхност|обошёл|файлов\" /tmp/pa.txt | head -6; echo \"--- какие корни зашиты ---\"; grep -nE \"SURFACES|_surfaces|ROOTS\" prior_art.py | h

---

> `Bash` -- {"command": "cd /c/Users/dev/.claude/scripts && sed -n '83,120p' prior_art.py", "description": "Читаю список поверхностей"}

---

**Claude:**

Корень найден: `prior_art.build_surfaces()` обходит scripts, skills, hooks, memory, _imports. **Волт в список НЕ входит.** А решения и ретро — это ровно то место, где живут наши ВЕРДИКТЫ. Меряю цену расширения, прежде чем трогать.

---

> `Bash` -- {"command": "V=\"D:\\Vault\\Vault-Knowledge\"; for d in 02-Decisions 03-Insights 90_MOCs \"01-Conversations/Claude/Retros\"; do printf \"%-32s %s .md\\n\" \"$d\" \"$(find \"$V/$d\" -name '*.md' 2>/dev/null | wc -l)\"; done; echo \"--- для сравнения, что обходит сейчас ---\"; printf \"%-32s %s\\n\

---

> `Bash` -- {"command": "V=\"D:\\Vault\\Vault-Knowledge\"; echo \"02-Decisions/_Inbox: $(find \"$V/02-Decisions/_Inbox\" -maxdepth 1 -name '*.md' 2>/dev/null | wc -l) .md\"; D=/c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_33a90300/scratchpad/ste; echo \"---

---

> `Bash` -- {"command": "D=/c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_33a90300/scratchpad/ste; cd /c/Users/dev/.claude/scripts && echo \"############ GROK q2: full → micro\"; timeout 60 python ste_score.py --compare \"$D/g-on.md\" \"$D/g-micro.md\" 2>&1 |

---

> `Bash` -- {"command": "cd /c/Users/dev/.claude/scripts && start=$(date +%s); timeout 200 python prior_art.py build test cost measure > /tmp/pacost.txt 2>&1; rc=$?; end=$(date +%s); echo \"prior_art rc=$rc, секунд: $((end-start))\"; grep -iE \"обойдено\" /tmp/pacost.txt", "description": "Текущая цена прогона

---

**Claude:**

Микро-промпт дал неожиданный результат, проверяю глазами, не артефакт ли это разбора.

---

> `Bash` -- {"command": "D=/c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_33a90300/scratchpad/ste; head -c 700 \"$D/g-micro.md\"; echo; echo \"...\"; echo \"--- число точек в тексте ---\"; grep -o '\\.' \"$D/g-micro.md\" | wc -l", "description": "Читаю ответ gr

---

**Claude:**

Не артефакт: grok честно выдал 5 предложений по ~91 слову. Запрет «максимум пять предложений» столкнулся с задачей, требующей объёма, и породил монстров — ровно противоположное STE. Это уточняет вывод ретро: два стиля не конкуренты, у них разные задачи.

Теперь чиню корень промаха RECALL. Прогон `prior_art` = 3 секунды на 3745 файлов, значит расширение по карману.

---

> `Write` -- {"file_path": "C:\\Users\\dev\\.claude\\scripts\\_shared\\_patch_prior_art_vault.py", "content": "#!/usr/bin/env python3\n# -*- coding: utf-8 -*-\n\"\"\"Разовый патч: учит prior_art.py видеть ВЕРДИКТЫ волта (ретро и MOC-карты).\n\nПОВОД (замер 07.10.2026, цена названа). `build_surfaces()` обходил 

---

> `Bash` -- {"command": "cd /c/Users/dev/.claude/scripts && cp prior_art.py prior_art.py.bak-pre-vault-20261007 && timeout 110 python _shared/_patch_prior_art_vault.py; echo \"patch rc=$?\"; echo \"=== ЦЕНА ПОСЛЕ ===\"; start=$(date +%s); timeout 200 python prior_art.py build Teague ladder explain formats >

---

> `Bash` -- {"command": "cd /c/Users/dev/.claude/scripts && head -20 /tmp/pa2.txt", "description": "Находит ли prior_art пропущенное ретро"}

---

> `Bash` -- {"command": "cd /c/Users/dev/.claude/scripts && timeout 200 python prior_art.py build Teague ladder explain formats 2>&1 | grep -iE \"retro|moc|vault\" | head -6; echo \"=== контрольная проба: ищет ли ровно нашу тему ===\"; timeout 200 python prior_art.py build ASD-STE100 simplified technical en

---

**Claude:**

Новые поверхности молчат — проверяю, доезжает ли прибор до файла вообще. «Пусто» и «не дошёл» выглядят одинаково (§5.4).

---

> `Bash` -- {"command": "cd /c/Users/dev/.claude/scripts && timeout 110 python - <<'EOF'\nimport sys\nsys.path.insert(0, \".\")\nimport prior_art as pa\nsurf = pa.build_surfaces()\nfor name, path, exts, rec in surf:\n    import os\n    print(\"%-14s рекурсив=%-5s есть=%-5s  %s\" % (name, rec, os.path.isdir(pa

---

> `Bash` -- {"command": "cd /c/Users/dev/.claude/scripts && timeout 110 python - <<'EOF'\nimport sys, os\nsys.path.insert(0, \".\")\nimport prior_art as pa\n# ищем словами, которые ТОЧНО есть в пропущенном ретро\nhits, ns, nf = pa.search([\"карпати\", \"лестница\", \"ste100\"]) if hasattr(pa, \"search\") else

---

> `Bash` -- {"command": "cd /c/Users/dev/.claude/scripts && timeout 110 python - <<'EOF'\nimport sys\nsys.path.insert(0, \".\")\nimport prior_art as pa\nhits, ns, nf = pa.scan_build([\"карпати\", \"лестница\", \"ste100\", \"Teague\"])\nprint(\"поверхностей %d, файлов %d, хитов %d\" % (ns, nf, len(hits)))\nf

---

> `Bash` -- {"command": "cd /c/Users/dev/.claude/scripts && timeout 110 python - <<'EOF'\nimport sys\nsys.path.insert(0, \".\")\nimport prior_art as pa\nhits, ns, nf = pa.scan_build(\"карпати лестница ste100 Teague\")\nprint(\"поверхностей %d, файлов %d, хитов %d\" % (ns, nf, len(hits)))\nfor h in hits[:10]

---

**Claude:**

Починка работает: пропущенное ретро теперь **первый хит** (43 балла, поверхность `vault-retros`). Доказываю красным и проверяю q3.

---

> `Bash` -- {"command": "cd /c/Users/dev/.claude/scripts && timeout 150 python red_proof.py --file prior_art.py \\\n --old '        retros = os.path.join(v, \"01-Conversations\", \"Claude\", \"Retros\")' \\\n --new '        retros = os.path.join(v, \"01-Conversations\", \"Claude\", \"RetrosNOPE\")' \\\n --exp

---

> `Bash` -- {"command": "D=/c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_33a90300/scratchpad/ste; for f in q3-off q3-full q3-micro c-micro; do printf \"%-10s %6s байт\\n\" \"$f\" \"$(wc -c < $D/$f.md 2>/dev/null || echo 0)\"; done", "description": "Статус рука

---

> `Bash` -- {"command": "D=/c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_33a90300/scratchpad/ste; n=0; while [ $n -lt 4 ] && [ ! -s \"$D/q3-off.md\" ]; do n=$((n+1)); python -c \"import time;time.sleep(25)\"; done; printf \"q3-off: %s байт\\n\" \"$(wc -c < $D/

---

**Claude:**

Все три рукава на вопросе БЕЗ указания формата собраны. Это решающий замер.

---

> `Bash` -- {"command": "D=/c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_33a90300/scratchpad/ste; cd /c/Users/dev/.claude/scripts && for f in q3-off q3-full q3-micro; do echo \"######## $f\"; timeout 60 python ste_score.py \"$D/$f.md\" 2>/dev/null | sed -n '

---

**Claude:**

`q3-off` дал «судимо 0 из 26» — прибор отказался судить базовый ответ целиком. Смотрю, почему, прежде чем делать выводы.

---

> `Bash` -- {"command": "D=/c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_33a90300/scratchpad/ste; head -c 600 \"$D/q3-off.md\"; echo; echo \"=== причина отказа ===\"; cd /c/Users/dev/.claude/scripts && timeout 60 python ste_score.py \"$D/q3-off.md\" 2>/dev/n

---

**Claude:**

Прибор был прав, что отказался: базовый ответ пришёл **по-русски** и таблицами. Это и находка, и признание — языковой сдвиг я не контролировал, значит рукав «без директивы» для сравнения STE негоден. Беру читательские величины, они сравнимы.

---

> `Bash` -- {"command": "D=/c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_33a90300/scratchpad/ste; cd /c/Users/dev/.claude/scripts && for f in q3-off q3-full q3-micro; do printf \"%-10s \" \"$f\"; timeout 60 python ste_score.py \"$D/$f.md\" 2>/dev/null | grep

---

**Claude:**

Вот решающая таблица, и она подтверждает вывод ретро на читательской оси:

| рукав | слов | жирного | буллетов | строк таблиц | чистых предложений |
|---|---|---|---|---|---|
| без директивы (ответ пришёл по-русски) | 12 лат. | 9 | 5 | 5 | нет данных |
| **моя `full`** | 316 | **8** | **7** | **7** | **76.0%** |
| **`micro`, 8 строк** | 112 | **0** | **0** | **0** | 20.0% |

Моя директива **вообще не гасит** жирное, буллеты и таблицы — я просто забыл это в неё написать. Микро гасит всё в ноль. Беру недостающие строки из измеренно лучшего.

---

> `Bash` -- {"command": "cd /c/Users/dev/.claude/scripts && cp ste_directive.md ste_directive.md.bak-pre-layout-20261007 && python - <<'PYEOF'\nimport io\np = \"ste_directive.md\"\ns = io.open(p, encoding=\"utf-8\").read()\nold = \"- Write no filler. Delete \\\"it should be noted that\\\" and \\\"it is import

---

> `Bash` -- {"command": "D=/c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_33a90300/scratchpad/ste; cd /c/Users/dev/.claude/scripts && python llm_ask.py --prompt-file \"$D/q3.txt\" --rails codex --mode first --timeout 900 --ste 80 --ste-style full > \"$D/q3-fu

---

> `Bash` -- {"command": "cd /c/Users/dev/.claude/scripts && timeout 110 python selfheal.py journal --class \"recall-promahnulsya-poverhnost-ne-obojdena\" --what \"prior_art.py build_surfaces() обходил scripts/skills/hooks/memory/_imports и обещал в докстроке «ВСЕ места, где живут наши детали», но ВОЛТ в списо

---

> `Bash` -- {"command": "cd /c/Users/dev/.claude/scripts && timeout 150 python prior_art.py class \"RECALL промахнулся, потому что поверхность не обойдена: прибор сказал чисто, а решение лежало в волте\" > /tmp/fam.txt 2>&1; echo \"rc=$?\"; head -12 /tmp/fam.txt", "description": "Какая это семья"}

---

**Claude:**

Семья `vyvod-po-odnoy-poverhnosti` — **168 случаев с 27.07, двери у неё НЕТ**. Я сегодня построил дверь ровно для одного её экземпляра. Регистрирую честно — именно как частичную.

---

> `Bash` -- {"command": "cd /c/Users/dev/.claude/scripts && grep -n \"FAMILY_DOORS\" prior_art.py | head -4; echo \"---\"; sed -n \"$(grep -n 'FAMILY_DOORS = ' prior_art.py | head -1 | cut -d: -f1),+22p\" prior_art.py", "description": "Структура реестра дверей"}

---

> `Write` -- {"file_path": "C:\\Users\\dev\\.claude\\scripts\\_shared\\_patch_family_door_surface.py", "content": "#!/usr/bin/env python3\n# -*- coding: utf-8 -*-\n\"\"\"Разовый патч: регистрирует ЧАСТИЧНУЮ дверь семьи vyvod-po-odnoy-poverhnosti.\n\nПовод (07.10.2026): prior_art сам потребовал — «ДВЕРИ У СЕМЬИ

---

> `Bash` -- {"command": "cd /c/Users/dev/.claude/scripts && timeout 110 python _shared/_patch_family_door_surface.py; echo \"rc=$?\"; echo \"=== проверяю, что дверь теперь называется ===\"; timeout 150 python prior_art.py class \"RECALL промахнулся, потому что поверхность не обойдена: прибор сказал чисто, а р

---

> `Bash` -- {"command": "D=/c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_33a90300/scratchpad/ste; n=0; while [ $n -lt 4 ] && [ ! -s \"$D/q3-full2.md\" ]; do n=$((n+1)); python -c \"import time;time.sleep(25)\"; done; printf \"q3-full2: %s байт\\n\" \"$(wc -c <

---

> `Bash` -- {"command": "D=/c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_33a90300/scratchpad/ste; n=0; while [ $n -lt 4 ] && [ ! -s \"$D/q3-full2.md\" ]; do n=$((n+1)); python -c \"import time;time.sleep(26)\"; done; printf \"q3-full2: %s байт (ждал ещё %d)\\n

---

> `Bash` -- {"command": "D=/c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_33a90300/scratchpad/ste; cd /c/Users/dev/.claude/scripts && echo \"######## директива v2 (с правилами вёрстки)\"; timeout 60 python ste_score.py \"$D/q3-full2.md\" 2>/dev/null | sed -n 

---

**Claude:**

Синтез сработал и **впервые взял порог**:

| рукав | чистых предложений | средняя длина | слов | жирного | буллетов | таблиц |
|---|---|---|---|---|---|---|
| `full` v1 | 76.0% FAIL | 9.8 | 316 | 8 | 7 | 7 |
| `micro` 8 строк | 20.0% FAIL | 22.4 | 112 | 0 | 0 | 0 |
| **`full` v2** | **81.0% PASS** | 10.7 | 225 | **0** | **0** | **0** |

Это отменяет мой же вывод часом раньше. Записываю.

---

> `Write` -- {"file_path": "C:\\Users\\dev\\.claude\\scripts\\_shared\\_patch_ste_note_v2.py", "content": "#!/usr/bin/env python3\n# -*- coding: utf-8 -*-\n\"\"\"Разовый патч: дописывает в заметку волта и в память результат третьего круга канарейки.\n\nПовод: фоновый RECALL по волту досчитал и нашёл prior art,

---

> `Bash` -- {"command": "cd /c/Users/dev/.claude/scripts && timeout 110 python _shared/_patch_ste_note_v2.py; echo \"patch rc=$?\"; echo \"=== гейты текста ===\"; timeout 110 python paragraph_lint.py \"D:\\Vault\\Vault-Knowledge\\03-Insights\\Operations\\experiment-ste100-canary.md\" > /tmp/plf.txt 2>&1; e

---

> `Bash` -- {"command": "cd /c/Users/dev/.claude/scripts && python - <<'PYEOF'\nimport io\np = r\"D:\\Vault\\Vault-Knowledge\\03-Insights\\Operations\\experiment-ste100-canary.md\"\ns = io.open(p, encoding=\"utf-8\").read()\nold = \"Добавлены две дешёвые поверхности: `vault-retros` (1979 файлов) и `vault-m

---

> `Bash` -- {"command": "cd /c/Users/dev/.claude/scripts && timeout 110 python change_ledger.py add --actor \"claude@HUB-01\" --operator \"dev\" --session \"voice001-ste100-20261007\" --tool \"claude-code\" --target \"~/.claude/scripts/prior_art.py (поверхности волта + дверь семьи), ste_score.py (чит

---

**Claude:**

**07:33 Лиссабон / 07:33 МСК** · узел HUB-01

## Фоновый RECALL досчитал и перевернул половину моего вывода

Тот grep по волту, который я с начала сессии отказывался считать завершённым, вернулся и нашёл **два файла, которые приборы не увидели**:

- `02-Decisions/_Inbox/2026-10-04--lestnica-karpati-...` — решение от 04.10
- `01-Conversations/Claude/Retros/retro-2026-10-06-Teague-ladder-explain-formats.md` — ретро от 06.10

Обе сессии разбирали ровно эту тему и несли **замер автора репозитория `AminBlg/SimpleEnglish`** (3717 звёзд), который сам опроверг свой продукт файлом `WHY-USELESS-2026-09-02.md`: скилл из 53 правил выигрывает только на СВОЁМ линтере, микро-промпт из 8 строк выигрывает на всём, что видит читатель.

Я построил директиву из ~30 правил и мерил её своим же линтером. Ровно то, от чего предостерегает их вывод.

---

## Проверил это на своей рельсе, а не поверил на слово

Сначала научил прибор считать то, что видит **читатель**, а не только мои правила. Потом вопрос БЕЗ указания формата, одна рельса codex, три рукава:

| рукав | чистых предложений | средняя длина | слов | жирного | буллетов | строк таблиц |
|---|---|---|---|---|---|---|
| без директивы | нет данных (ответ пришёл **по-русски**) | — | 12 лат. | 9 | 5 | 5 |
| `full` v1 — моя | 76.0% FAIL | 9.8 | 316 | **8** | **7** | **7** |
| `micro` — 8 строк | 20.0% FAIL | 22.4 | 112 | **0** | **0** | **0** |
| **`full` v2 — синтез** | **81.0% PASS** | 10.7 | 225 | **0** | **0** | **0** |

**Моя директива вообще не гасила жирное, буллеты и таблицы.** Я просто не написал этого в неё. Микро-промпт гасит всё в ноль.

Но у микро своя беда: его «максимум пять предложений» на объёмной задаче дал у grok **пять предложений по 91 слову**. Это противоположность STE. Автор и сам удалил это правило в версии 2.1.0.

Значит стили не конкуренты. Добавил в `full` три недостающие строки из измеренно лучшего — и получил 81.0% PASS при нуле жирного, буллетов и таблиц.

---

## ⭐ Отменяю свой же вывод, который дал час назад

Я написал: **«порог 80% просьбой НЕ берётся»**. Это было верно для моей первой директивы и **неверно вообще**.

Порог берётся. Не берётся тем набором правил, который кажется очевидным.

Остальные выводы держатся: словарь директива не чинит, объём не экономит, дельта тем больше, чем хуже база.

---

## Починил корень промаха RECALL — он стоил этой сессии

`prior_art.build_surfaces()` обходил scripts, skills, hooks, memory, _imports и обещал в докстроке «ВСЕ места, где живут наши детали». **Волта там не было** — то есть наши решения и ретро были приборам невидимы.

Добавил две дешёвые поверхности: `vault-retros` (1979 файлов) и `vault-mocs` (79). Цена 3 с → 5 с, файлов 3745 → 5803. Пропущенное ретро стало **первым хитом** (43 балла). Красное доказано.

⛔ `02-Decisions` (19069 файлов) и `03-Insights` (2600) НЕ добавил сознательно: там цена росла бы с ОБЪЁМОМ архива, а не с числом изменений. Их дверь — RAG `brain_ask`. Пробел вписал в докстроку прибора, чтобы «prior_art сказал чисто» никто не прочитал как «в волте этого нет».

Семья класса — `vyvod-po-odnoy-poverhnosti`, **168 случаев с 27.07.2026, двери не было вовсе**. Зарегистрировал **ЧАСТИЧНУЮ**: она закрывает слепоту самого `prior_art`, но не семью — у каждого другого прибора свой список поверхностей. Лечение семьи целиком назвал в реестре: прибор обязан ПЕЧАТАТЬ, какие поверхности обошёл и какие нет.

---

## Что я сделал не так в этой сессии

**Трижды наступил на грабли, о которых прямо предупреждает `/tt`.** Дважды читал `$?` после пайпа — он принадлежит `tail`, не прибору. Дважды писал патч с обратными слэшами через heredoc и дважды ломал исходник; потом перешёл на патч-файлы, как велит канон, и это сработало с первого раза.

**Честный пробел замера:** рукав «без директивы» ответил по-русски, оба рукава с директивой — по-английски. Языковой сдвиг я не контролировал, поэтому базовый рукав для сравнения STE негоден, сравнимы только три английских столбца.

**Шесть дефектов нашли чужие и живые данные, не моё рассуждение.** Панель (5 независимых семей) дала три, живой прогон два, линт один.

---

## 🧪 Вердикт: ⚠️ **PARTIAL**, тот же

`ste_score` 50/50 · самотест 11/11 · `paragraph_lint` 0 · `prior_art` 7 поверхностей · красное доказано **шестью** поломками. Строка в леджер правок записана.

Жёлтые флаги не изменились: слепая зона 41% (сознательно), флот не задет (канарейка), формат проверен на одном движке из пяти, твоего вердикта «легче читать» ещё нет.

**Что лежит на столе отдельно:** семья `vyvod-po-odnoy-poverhnosti` с 168 случаями требует не моей частичной двери, а сессии починки — прибор должен печатать своё покрытие поверхностей. Скажи слово, подниму.

---

🧒 **Простыми словами.** Старый поиск по архиву досчитал только что — и нашёл, что две сессии до меня уже это изучали и даже померили. Мои искалки этого не нашли, потому что они не умели смотреть в архив. Починил: теперь умеют.

Оказалось, у них было важное: длинный список правил работает хуже восьми коротких строк. Я проверил сам, и вышло интереснее — мой список забыл запретить жирный шрифт, списки и таблицы. Дописал три строки, и стало лучше обоих вариантов.

Мой вчерашний вывод «до 80% не дотянуть» был неверным. Дотянули: 81.

Сам при этом три раза наступил на грабли, про которые инструкция предупреждает заглавными буквами. Записал.

---

**User:**

мы будем это использовать?

---

> `Bash` -- {"command": "cd /c/Users/dev/.claude/scripts/_shared && timeout 110 python - <<'EOF'\nimport sys\nsys.path.insert(0, \".\")\nimport skill_usage_log as s\nrows = [r for r in s.read_all(days=2, kind=\"part\") if \"ste\" in (r.get(\"skill\") or \"\")]\nfrom collections import Counter\nc = Counter(r[\

---

**Claude:**

**Да — но в одном узком месте, и не на рельсах по умолчанию.**

## Где

**1. `llm_ask --ste 80`, когда я спрашиваю чужую рельсу то, чей прозаический ответ буду пересказывать тебе.** Замерено: 81% чистых предложений, ноль жирного/буллетов/таблиц, предложения по 10.7 слова. Это дёшево и обратимо.

**2. Четыре строки вёрстки — no bold, no bullets, no tables, no em-dash — в английское ИСХОДЯЩЕЕ.** GitHub-комментарии, заявки, EN-посты. Для русского у нас есть `/ai-slop` и `slop_gate`, для английского двери нет вообще. Это измеренно работающая часть, и она чужая, не моя придумка.

**3. `ste_score --fail-under 80` как гейт на английский текст перед отправкой.** 0 токенов, 0 сети.

## Когда НЕ

- **В мои ответы тебе** — ты читаешь по-русски, стандарт английский.
- **На `secondop` и ревью по умолчанию** — формат с тегом вердикта проверен 1 раз из 5.
- **Где ответ ДОЛЖЕН быть таблицей или кодом** — директива таблицы убивает.
- **Стиль `micro` на объёмных задачах** — даёт предложения по 91 слову.

## Почему — и тут неудобная правда

Главный потребитель ответов чужих рельс — **я, машина**. Что машине легче читать короткие предложения, **не замерено** и скорее неправда.

Настоящая польза там, где текст читает человек. Поэтому адрес №2 важнее №1, а №1 — приятный побочный эффект.

**Счётчик говорит прямо:** 8 вызовов флага, все мои сегодняшние, внутри эксперимента. Органического использования **ноль**. Если к 21.10 будет так же — флаг убиваем, оставляем скорер и четыре строки.

**От тебя нужно одно слово про адрес №2.** Ретро 06.10 уже предлагало положить восемь строк в `/taste-check` и ждёт с тех пор.

Теперь ретро.

---

> `Skill` -- {"skill": "retro", "args": "канарейка ASD-STE100 + починка слепоты prior_art к волту"}

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
- ⚠️ **Прибор даёт ложное «чисто» (замер 10.09.2026, NODE-0X):** `--scan` напечатал «0 missing pointer(s) to repair», а указатель на свежую заметку (`zenodo-publish-rail`, дописан 07.09) из `MEMORY.md` за ночь исчез — сироту он не увидел, потому что сверяет не ту пару папок. Поэтому ПОМИМО прогона сверь руками указатели на заметки, которые ЭТА сессия и пара прошлых записали: `grep -c "<слаг>" <проектная-папка>/memory/MEMORY.md` → 0 = дописать строку тем же заходом. Класс = `memory-index-line-lost-overnight`, 4 датированных случая, корень чинится отдельной сессией.
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
⭐ **И ТРЕТЬЯ КОЛОНКА ДЛЯ ПРИБОРОВ — покрытие N/M** (dev 01.10.2026, класс `instrument-blind-to-most-of-its-subject`): у каждого собранного или тронутого за сессию прибора (сторож, аудит, счётчик долга) ретро выписывает строку `СЛЕПАЯ ЗОНА:` из его вывода (`python3 ~/.claude/scripts/_shared/blind_zone.py --run <прибор>`). Строки нет (exit 3) → ⚠️ и правка прибора тем же заходом. Покрытие <90% → ⚠️ + задача на подъём покрытия. Число без слепой зоны в отчёте ретро не ставится. Then classify:
- 🟢 **Keep & reuse** — permanent infra or a tool you'll run again (skills, durable notes, reusable scripts).
- 🟡 **One-off** — served its purpose; if the *pattern* is worth remembering, capture the pattern (not the artifact), then let it rest.
- ⬆️ **Promote** — currently ad-hoc but should become permanent → turn into a rule / skill / memory.

## Step 3🔨 — ПАНЕЛЬ ШЕСТИ ЛОМАТЕЛЕЙ, В КАЖДОМ РЕТРО (⭐ dev 06.10.2026: «ВСЕГДА … во ВСЕХ РЕТРО»)
Без исключений: и полное ретро, и полоса `push3`, и сессия без кода. Шесть **средних** моделей
через OpenRouter: 3 Китай (GLM-5.3, DeepSeek V4 Pro, Qwen 3.7 Plus) + 1 Европа (Mistral Medium 3.5) +
2 США (GPT-6 Sol, Grok 4.3). Поправка 07.10 (оператор): «Мистраль два раза не надо», второй EU-семьи
на OpenRouter нет. ⛔ Фронтир не берём (Fable, gpt-6-astra, glm-prime, kimi-k3, gemini-pro, grok-4.7),
⛔ примитив тоже (luna, flash-lite, small, haiku). Состав зашит в код, руками не собирать:
`RETRO_FAN` в `orouter_review.py`, сторож `_test_orouter_fan.py` (23 проверки). Ответил фолбэк →
в выводе строка `qwen/… → ответил фолбэк minimax/…`: так и пиши в отчёт, не имя из заказа.
```bash
python ~/.claude/scripts/cc-review/orouter_review.py panel --preset retro --task retro-<sessionId> --context-file <файл>
```
⚠️ **На узле старая версия `orouter_review.py` без `--preset`** (замер 07.10.2026, NODE-0X: `unrecognized arguments: --preset retro`) → тот же состав явно: `panel --role break --lane eyes --task retro-<sid> --models "z-ai/glm-5.3,deepseek/deepseek-v4-pro-0813,qwen/qwen3.7-plus,mistralai/mistral-medium-3-5,openai/gpt-5.6-terra,x-ai/grok-4.3" --context-file <файл>`. Ответило 5 из 6: Qwen отбит 404 настройкой приватности OpenRouter (Zero data retention), это и есть строка «панель неполная», а не сбой прибора.
**Что кормить** (файл ≥200 символов): черновик этого ретро (Keep/Drop/Try + выводы «сегодня мы
поняли») + дифф или суть собранного кода, если он был. Вопрос панели: «где выводы ретро неверны,
что сломано, что я назвал готовым без улики». Секреты и личные данные отбивает сам прибор до
сети: увидел отказ `refused-secret/private` → вычисти и повтори, а не пропускай панель.
**Отчёт одной строкой:** `🔨 панель: N из 6 ответили · $X · принято K находок (какие) · отклонено M (почему)`.
Каждая принятая находка = правка в ТОМ ЖЕ заходе или строка в Step 3⛳; несогласие называю
вслух с доводом (§1.2-бис: панель не обязывает соглашаться, обязывает ответить).
Ответили <4 из 6 → в отчёт `⚠️ панель неполная` с именами молчунов, ретро не блокирует.
Траты пишутся в полосу `retro` (`~/.claude/_metrics/openrouter-spend.jsonl`).
🌾 **Урожай 06.11.2026:** свести траты полосы `retro` за месяц и показать оператору: оставить, урезать, выключить.
Живые прогоны: 06.10 6 из 6 за 215 с, канарейка.47 (старый состав с Gemini и двумя Mistral); 07.10 новый
состав 6 из 6 за 181 с, канарейка.31, из них Mistral канарейка.24. Kimi K2.6 отсеян (дольше 10 мин). Qwen закрыт
настройкой приватности на аккаунте OpenRouter, пока за него отвечает MiniMax M3.

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

⛔ Запрещено закрывать шаг словами «мало пользовались другими LLM» без цифр: доля считается прибором, а не на глаз (§5.4 «правда в цифрах»). ⛔ Не смешивать два числа: `rail_plan.py` считает **ВЫЗОВЫ наших рельс**, а процент выборки бака вендора живёт в `subscription_utilization.py report` — это разные величины разного происхождения.
Строкой в отчёт: «🚂 рельсы: жгли <рельса=N…> · недобор <рельса:код> · правка двери: да/нет».
Канон: [[rail-plan-declared-then-verified]], [[burn-the-limits-utilization]], [[other-llm-rails-were-review-only]].

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
**⭐ Усиление dev 01.09 (голосом ×2, канон `reglament-retro-smotrit-naruzhu-tizer-i-skill-v-mir`):** ретро = СУДЬЯ (~1 мин на артефакт), не раздатчик — замер 01.09: полный качественный проход = ~20 мин на 3 кандидата, в ретро это убивает оба. «2 да из 3» → **строка в очередь** `$OBSIDIAN_VAULT/_outreach/share_fix_queue.jsonl` (JSON-строка: added·from·artifact·queries[дословные симптом-запросы!]·numbers·status:pending) — симптом-запросы и цифры пишутся СЕЙЧАС, пока контекст горячий, именно они теряются к утру. Раздаёт ночная рутина `share-fix-daily` (хаб, ≤3 кандидата/ночь, полный ритуал `/share-fix`). Раздать прямо в ретро — только если целевой тред уже известен из сессии (тогда это 2 минуты, не 20). **Совет считается**: код отдавать не обязательно — опыт словами в чужом треде тоже польза. Что можно/нельзя наружу — чек-лист в том же регламенте.
**⭐ HN-кандидат (dev «+++» 10.09):** тот же проход задаёт ВТОРОЙ вопрос ровно один раз на артефакт — «это годится в Hacker News?». Годится ТОЛЬКО жанр «мы померили и показываем цифры» (post-mortem · замер · разбор поломки) и ТОЛЬКО как самостоятельная публичная страница с данными, не пост из ежедневного девлога. Да → строка в `$OBSIDIAN_VAULT/_outreach/hn_candidates.jsonl` (added·from·artifact·title·url·numbers·genre·status:ready|needs-page·blocked_by). Нет → молча, вердикт не нужен. ⛔ Потолок лейна: **своя ссылка на HN не чаще 1 раза в 2 недели** (ежедневный поток туда = профиль спамера, теневой бан накрывает аккаунт И домен); регулярное присутствие = комментарии в ЧУЖИХ тредах 1-3/нед. ⛔ Подача идёт ТОЛЬКО с хаба, ТОЛЬКО после «+» оператора и ОК Норы, ноль организованного голосования. Пока нет входа в HN на хабе — очередь копится, наружу не уходит ничего.

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

0. **Проверь рот ДО пера.** `mcp__claude-in-chrome__list_connected_browsers` — пустой массив означает «расширение отключено, публиковать нечем». Тогда порядок обратный: ОДНОЙ строкой скажи оператору «включи расширение Claude in Chrome, пост готовлю», и пиши пост дальше — он уйдёт, как только расширение появится. ⛔ Не трать два гейта, не зная, откроется ли дверь. ⚠️ Проверенные 06.10 и закрытые альтернативы, заново их не перебирай: встроенный браузер (в X не залогинен, логин в X запрещён из-за checkpoint-риска) · n8n (98 воркфлоу, X-постера нет) · Publora MCP (нужен OAuth, в неинтерактивной сессии невозможен) · Publora REST (`publora_smoke.py`: ключа нет, и вендор ПРЯМО запрещает агенту проходить шаги его получения). Пятая дверь, проверенная соседней сессией: **X API отдал 403 client-not-enrolled** -- аккаунт не заведён в их программу, это тоже руки. Единственная живая дверь = расширение Chrome.
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
3. Публикуй через **`/x-post`** (живой Chrome, @Tony_Stef_, `social_guard` ≤6/день). ⛔ IP-гейт §7.2: постинг в X только с хаба `HUB-01`; на другом узле пост не публикуется, а уезжает текстом на хаб, и ретро говорит это строкой. Ссылка (GitHub/лонгрид) уходит ПЕРВЫМ РЕПЛАЕМ, не в тело.
4. Зафиксируй факт, иначе полоса непроверяема:
   ```
   python -B "$HOME/.claude/scripts/retro_x_post.py" record --url "<ссылка на твит>" --retro "<путь к заметке ретро>"
   ```
   Жива ли полоса вообще: `retro_x_post.py status --days 14`.

⚠️ **ПОТОЛОК ДЛИНЫ НА ДЕЛЕ 250, А НЕ 280** (замер 06.10, наступил сам). Два гейта спорят, и скилл раньше не говорил, кто главный: `retro_x_post` разрешает 280 по взвешенному счёту X, а `slop_gate --tier teaser` рубит FAIL на 250 (его граница настроена под RU-каналы, медиана ~800). В окне 251–280 пост проходит первый гейт и валится вторым. Пиши под **250**, и не садись на саму границу: прибор сам пишет, что у лимита длина неточна в обе стороны (память «порог судим разбросом, не точкой»).
⚠️ **Два WARN `slop_gate` на этой полосе ОЖИДАЕМЫ и дефектом не являются** — назови их вслух и иди дальше: `W7-teaser-no-way-out` требует ссылку в тизере, тогда как `retro_x_post` ссылку в теле ВАЛИТ (разрешается первым реплаем, которого slop_gate не видит); `W4-first-person` ищет русские «я/мне/мой» в англоязычном посте для @Tony_Stef_ и потому срабатывает ложно. Блокирует только FAIL.

**⭐ ДВЕРЬ В X ПРОВЕРЯЕТСЯ ЖИВОЙ ПРОБОЙ, И ОНА БЫВАЕТ МЕРТВА ЦЕЛИКОМ** (замер 06.10). Полоса показывала «опубликовано 0 при 11 прогонах гейта», и я счёл это недостатком дисциплины. Причина оказалась транспортной: в тот день отказали ВСЕ ТРИ двери подряд, каждая живой пробой, а не догадкой — (1) `list_connected_browsers` вернул `[]` при пяти живых `chrome.exe` (расширение Claude-in-Chrome к сессии не подключено); (2) `python x_post.py check` → `403 client-not-enrolled`, приложение не привязано к Project в портале разработчика; (3) `python publora_smoke.py` → ключа нет, и Publora программно запрещает агенту его завести. Порядок пробы — этот же, он от дешёвого к дорогому. ⛔ «Опубликовано 0» само по себе НЕ улика против дисциплины: сначала проба двери, потом вердикт о причине (§5.4 «причина = такой же claim»).

**Пропуск законен в ЧЕТЫРЁХ случаях, и каждый называется вслух:** (1) сессия пустая, рассказывать снаружи нечего; (2) узел не хаб, пост уехал на хаб задачей; (3) `social_guard` вернул лимит 6/день; (4) ⭐ **все двери в X мертвы по живой пробе** — тогда пост НЕ выбрасывается, а парkуется, иначе он умирает в скратчпаде (класс «тихая потеря задач»):
   ```
   python -B "$HOME/.claude/scripts/retro_x_post.py" park --file "<черновик.txt>" --reason "<какая дверь и как отказала>" --session "<ключ>"
   ```
   Припаркованные `status` печатает ВСЕГДА, вне окна `--days`. Открылась дверь — отправляешь и закрываешь парковку ИМЕННО её ключом: `record --url <твит> --closes <slug>`. ⛔ Квитанция без `--closes` чужую парковку не закрывает, и это прибито тестом: именно так рельса 001 уже теряла задачи, когда квитанция закрывала чужую единицу.
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
- До работы выбери абсолютный путь `<absolute-receipt.json>` вне репозитория и захвати сессию: `python -B "$HOME/.claude/scripts/retro_lost_scan.py" take <sessionId> --holder "<taskId>" --json --receipt-out "<absolute-receipt.json>"`.
- `rc=0` доверяй только когда durable receipt exists и JSON содержит непустые `question_id`, `session_id`, `logical_file_id`, `holder` и `epoch` как positive integer. Receipt сохрани до подтверждённого DONE: он нужен для replay после crash. При отсутствующем/битом receipt остановись; DONE не ставь.
- После записи ретро передай значения **дословно из receipt**: `python -B "$HOME/.claude/scripts/retro_lost_scan.py" mark-done "<receipt.session_id>" --question-id "<receipt.question_id>" --logical-file-id "<receipt.logical_file_id>" --holder "<receipt.holder>" --epoch "<receipt.epoch>" --note "<retro-note>"`. Do not recompute identity по пути или sessionId. Wrong/missing identity обязана завершиться fail-closed без DONE/release; точный replay идемпотентен.
  ⚠️ `"$HOME/..."` буквально работает и в Windows PowerShell 5.1, и в Git Bash. `~` после `python` в PowerShell 5.1 остаётся буквальным путём, а `%USERPROFILE%` раскрывает только CMD.
- Не смог достоверно определить sessionId — так и скажи строкой в отчёте, НЕ помечай наугад чужую сессию.
- ⚠️ **`take` ответил `session-not-found` при ВЕРНОМ sessionId — это норма, а не сбой** (замер 06.10.2026, ретро живой сессии 97c50ca4). Сканер `retro_lost_scan.py` держит в очереди только БРОШЕННЫЕ сессии (молчат дольше суток); сессия, в которой ретро идёт прямо сейчас, в очередь ещё не попала, и помечать нечего. Правильное поведение: ОДНА строка в отчёт «в очереди retro-lost сессии нет, помечать нечего», `mark-done` НЕ зовём и `--force` не ищем. ⛔ Не читать это как «дверь сломана»: ночная догонялка возьмёт сессию, только если она затихнет, а к тому моменту заметка ретро уже лежит в волте и робот сам увидит её по `session_id` во frontmatter.
- ⚠️ **А вот `take` с `rc=0` -- ОБРАТНЫЙ случай, и он ОБЯЗЫВАЕТ закрыть квитанцию** (замер 06.10.2026, сессия CRM+мессенджеров: разрыв 62ч24м, сессия затихла на двое суток и в очередь попасть УСПЕЛА, `take` отдал `epoch 223` и живую квитанцию). Абзац выше описывает только ПУСТУЮ очередь, и сессия, впервые увидевшая `rc=0`, порядок выводит сама -- отсюда риск бросить захват незакрытым: держатель висит, а ночная догонялка через 5 суток снова читает транскрипт и снова тратит Opus. Порядок при `rc=0`: дочитать `question_id`, `logical_file_id`, `holder`, `epoch` из квитанции ДОСЛОВНО -> записать заметку ретро -> `mark-done` ровно этими значениями -> убедиться, что в ответе есть строка `done: <...>/logs/retro_lost_done/<sessionId>`. ⛔ Значения не пересчитывать по пути и не брать «на глаз»: неверная личность обязана падать fail-closed, и тогда DONE не ставится вовсе. ⛔ Пути в правках этого файла пиши ПРЯМЫМИ слэшами: обратный слэш перед l/r/t/0 становится управляющим символом и МОЛЧА обрезает строку (семья escape-avariya-v-patche, наступил сам 06.10 ровно в этом абзаце).

**6a-тер. Переименуй сессию: маркер «Р» в видимом имени — СРАЗУ после 6a-бис** (⭐ dev 02.09.2026, голосом: «когда я вижу этот маркер, я понимаю, что дошёл в этой сессии до крупного milestone»; ⭐ **поправка dev 15.09.2026, голосом: маркер теперь просто `Р`, БЕЗ плюсика** — «дописываем не Р с плюсиком, а просто Р»).
- Вызови `mcp__ccd_session_mgmt__get_session` с `session_id: "self"` → возьми текущий `title`. Если в нём УЖЕ стоит маркер ретро — `Р ` (новый) ЛИБО legacy `Р+`/`р+`/`рр+` — шаг закрыт, второй маркер не лепить и legacy НЕ переписывать (старые имена оставляем как есть, чинить историю нечем и незачем).
- Иначе `mcp__ccd_session_mgmt__set_session_title` с `session_id: "self"` и `title: "<иконка> Р <старое имя без изменений>"` — маркер `Р` + ПРОБЕЛ, после иконки группы (иконка первой, см. 6a-кватер), без иконки — просто `"Р <старое имя>"`. Меняется ТОЛЬКО человекочитаемое имя в приложении (titleSource=tool), системный id не трогается; имя, данное оператором, сохраняется целиком после маркера.
- ⚠️ Пробел после `Р` обязателен: он и есть граница маркера. `Р` без пробела слипается с русским словом («Ретро», «Работа») и читатели (жнец, таблица сессий) такую сессию маркером не считают.
- MCP session_mgmt недоступен (headless `claude -p`, чужой харнес) → одна строка в отчёте «маркер Р не поставлен: нет session_mgmt», не молчи.

**6a-кватер. Проверь ИКОНКУ группы в заголовке — сразу после маркера Р** (⭐ dev 07.09.2026 «кладёшь её в нужную группу»; ⭐ dev 10.09.2026, голосом: «мало пикселей на экране, нужна иконка», и «переименовывать НА СТАРТЕ»).
- Иконка ставится НЕ здесь, а на СТАРТЕ сессии (скилл `/session-groups`). Ретро только ПЕРЕПРОВЕРЯЕТ: тема сессии за день могла уехать в другую группу.
- `get_session self` уже вызван в 6a-тер. Заголовок начинается с иконки из алфавита? 💰 $$$ (деньги/оффер/витрины/статьи наружу) · 🧠 2мозг (волт/RAG/память/клон) · ✍️ content (посты/соцсети/Майкрофт) · 🎯 Лиды-CRM · ⚙️ Инфра (скрипты/флот/синк/канон/браузеры) · 🔬 ДРы · 🏠 личное · 📥 SINK (инбокс/шина/посылки) · ❓ не понял.
- Иконки нет ЛИБО она уже не про эту сессию → `set_session_title self` в форму `<иконка> Р <имя>`. Веха ретро `Р ` живёт ПОСЛЕ иконки (legacy `Р+` в старых именах не переписываем). Гадать запрещено: тема не читается — ставь ❓, оператор разнесёт сам.
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

## Scope / don't-duplicate
- Internal build-retro only. NOT the public Facebook diary (`facebook-diary-daily`) and NOT the preference scanner (`preference-sweep-daily`).
- If a session built nothing durable, say so plainly — skip the ceremony (but still offer the `/compact` block if the chat got long).

## ⭐ Полнота списка потребителей (dev 10.09.2026)

Первый найденный потребитель почти никогда не единственный — он просто лежал на поверхности. Поиск закончен не когда кто-то найден, а когда **две оси подряд дали ноль новых имён**; внутренний потребитель (узел флота, робот, наш же скилл с костылём) ищется ПЕРВЫМ. Девять осей перебора и обязательный вердикт с числом («осей N/9 · адресов M · насыщение да/нет») — `/consumer-hunt` §Шаг 1-бис. ⚠️ Исчерпывающим обязан быть ПОИСК, адресация идёт по правилам двери: найденный адрес не выбрасывается, а получает статус и дату (🟢 постучались · ⏸ глухая очередь по замеру · 🪦 непереносимо). Канон: `reglament-vypustil-funkcional-naydi-potrebiteley-i-pridi-k-nim` §Поправка 10.09 + [[consumers-are-a-set-not-the-first-one]].

---

> `Bash` -- {"command": "cd /c/Users/dev/.claude/scripts && python -c \"import datetime; print('СЕЙЧАС', datetime.datetime.now().isoformat(timespec='seconds'))\"; echo \"--- CLI-sid (из rail_plan) ---\"; timeout 60 python -c \"import sys,os; sys.path.insert(0,os.path.expanduser('~/.claude/scripts')); import r

---

> `ToolSearch` -- {"query": "select:mcp__ccd_session_mgmt__get_session,mcp__ccd_session_mgmt__set_session_title", "max_results": 3}

---

> `mcp__ccd_session_mgmt__get_session` -- {"session_id": "self"}

---

> `Bash` -- {"command": "cd /c/Users/dev/.claude/scripts && timeout 110 python rail_plan.py verdict --session s_33a90300 > /tmp/rv2.txt 2>&1; echo \"rc=$?\"; cat /tmp/rv2.txt | head -16", "description": "Шаг 3🚂 вердикт рельс по CLI-sid"}

---

> `Bash` -- {"command": "cd /c/Users/dev/.claude/scripts && timeout 110 python retro_lost_scan.py take s_33a90300 --holder \"retro-live-20261007\" --json --receipt-out \"C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_33a90300

---

> `Bash` -- {"command": "cd /c/Users/dev/.claude/scripts && python - <<'PYEOF'\nimport io\np = r\"D:\\Vault\\Vault-Knowledge\\01-Conversations\\Claude\\_Claude-Sessions-MOC.md\"\ns = io.open(p, encoding=\"utf-8\").read()\nrow = (\"- [[retro-2026-10-07-ste100-canary-and-prior-art-blindness]] · канарейка ASD

---

> `Write` -- {"file_path": "D:\\Vault\\Vault-Knowledge\\01-Conversations\\Claude\\Retros\\retro-2026-10-07-ste100-canary-and-prior-art-blindness.md", "content": "---\ntitle: \"Ретро 07.10.2026 — канарейка ASD-STE100 и слепота prior_art к волту\"\naliases: [\"Ретро 07.10.2026 — канарейка STE100\", \"retro ste1

---

**Claude:**

Теперь панель шести ломателей на сам черновик ретро — она обязательна в каждом ретро.

---

> `Bash` -- {"command": "cd /c/Users/dev/.claude/scripts && timeout 115 python status_claim_lint.py \"D:\\Vault\\Vault-Knowledge\\01-Conversations\\Claude\\Retros\\retro-2026-10-07-ste100-canary-and-prior-art-blindness.md\" > /tmp/scl2.txt 2>&1; echo \"status_claim_lint rc=$?\"; tail -2 /tmp/scl2.txt; time

---

> `Bash` -- {"command": "cd /c/Users/dev/.claude/scripts && timeout 115 python cc-review/orouter_review.py panel --preset retro --task retro-b0dceaf6 --context-file \"D:\\Vault\\Vault-Knowledge\\01-Conversations\\Claude\\Retros\\retro-2026-10-07-ste100-canary-and-prior-art-blindness.md\" > /tmp/panel6.txt 

---

> `Bash` -- {"command": "cd /c/Users/dev/.claude/scripts && timeout 115 python paragraph_lint.py \"D:\\Vault\\Vault-Knowledge\\01-Conversations\\Claude\\Retros\\retro-2026-10-07-ste100-canary-and-prior-art-blindness.md\" 2>/dev/null | head -3", "description": "Оба полотна"}

---

> `Bash` -- {"command": "cd /c/Users/dev/.claude/scripts && python - <<'PYEOF'\nimport io\np = r\"D:\\Vault\\Vault-Knowledge\\01-Conversations\\Claude\\Retros\\retro-2026-10-07-ste100-canary-and-prior-art-blindness.md\"\ns = io.open(p, encoding=\"utf-8\").read()\nfixes = [\n(\"**1. Прибор соврал о ПРИЧИНЕ*

---

**Claude:**

Панель отбилась на `--preset` — скилл предупреждает об этой версии и даёт явный состав. Использую его.

---

> `Bash` -- {"command": "cd /c/Users/dev/.claude/scripts && timeout 115 python cc-review/orouter_review.py panel --role break --lane eyes --task retro-b0dceaf6 --models \"z-ai/glm-5.3,deepseek/deepseek-v4-pro-0813,qwen/qwen3.7-plus,mistralai/mistral-medium-3-5,openai/gpt-5.6-terra,x-ai/grok-4.3\" --context-fi

---

> `mcp__ccd_session_mgmt__set_session_title` -- {"session_id": "self", "title": "⚙️ H11354 Р ASD-STE100 для ответов нейронок"}

---

> `Bash` -- {"command": "cd /c/Users/dev/.claude/scripts && timeout 110 python retro_lost_scan.py mark-done \"s_33a90300\" --question-id \"retro-lost:s_33a90300\" --logical-file-id \"c:\\Users\\dev\\.claude\\projects\\P---WORKDIR-HUB\\b0dceaf6

---

> `Bash` -- {"command": "cd /c/Users/dev/.claude/scripts && timeout 110 python onair.py list > /tmp/oa.txt 2>&1; echo \"onair rc=$?\"; head -6 /tmp/oa.txt; echo \"=== катаклизмы: свежие поломки не из этой сессии ===\"; timeout 110 python selfheal.py journal --help > /dev/null 2>&1; tail -6 \"D:\\Vault\\Ant

---

> `Bash` -- {"command": "grep -E \"^\\[PANEL|НЕ ОТВЕТИЛА|ИТОГО|^VERIFY|^COUNTER|^ACCEPT|^BLOCK\" /tmp/panel7.txt | head -20; echo \"=== находки ===\"; grep -A3 -E \"^(COUNTER|BLOCK)\" /tmp/panel7.txt | head -40", "description": "Читаю панель шести"}

---

> `Bash` -- {"command": "wc -c /tmp/panel7.txt; echo \"---\"; head -40 /tmp/panel7.txt", "description": "Что отдала панель"}

---

> `Bash` -- {"command": "cd /c/Users/dev/.claude/scripts && timeout 110 python cc-review/orouter_review.py panel --help 2>&1 | head -24", "description": "Какие флаги есть у этой версии panel"}

---

> `Bash` -- {"command": "cd /c/Users/dev/.claude/scripts && timeout 115 python cc-review/orouter_review.py panel --role break --effort medium --task retro-b0dceaf6 --models \"z-ai/glm-5.3,deepseek/deepseek-v4-pro-0813,qwen/qwen3.7-plus,mistralai/mistral-medium-3-5,openai/gpt-5.6-terra,x-ai/grok-4.3\" --contex

---

> `ToolSearch` -- {"query": "select:mcp__claude-in-chrome__list_connected_browsers", "max_results": 2}

---

> `mcp__claude-in-chrome__list_connected_browsers` -- {}

---

**Claude:**

Дверь в X **ожила** (Browser 1, локальный Windows) — вчера она была мертва на всех трёх путях. Готовлю пост и гоняю оба гейта.

---

> `Bash` -- {"command": "D=\"C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_33a90300\\scratchpad\"; printf '%s' \"I wrote 30 rules to make AI answers readable. My own scorer said 76 percent good. Then I counted what a reader actually sees: 8 bold blocks

---

> `Bash` -- {"command": "D=\"C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_33a90300\\scratchpad\"; cp \"$D/xpost.txt\" \"$D/xpost.md\"; timeout 110 python -B \"D:\\Vault\\_imports\\content-factory\\slop_gate.py\" --file \"$D/xpost.md\" --tier teaser

---

> `Bash` -- {"command": "cat \"C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_33a90300\\tasks\\baa7zp0sg.output\" 2>/dev/null | head -4; echo \"--- panel8 ---\"; grep -cE \"PANEL\" /tmp/panel8.txt 2>/dev/null || echo \"пока пусто\"", "description": "Ста

---

> `Bash` -- {"command": "wc -c /tmp/panel8.txt; grep -E \"PANEL|НЕ ОТВЕТИЛА|ИТОГО|ответил фолбэк\" /tmp/panel8.txt | head -14", "description": "Читаю панель шести"}

---

> `Bash` -- {"command": "grep -nE \"^\\[|^(VERIFY|COUNTER|ACCEPT|BLOCK)|^[0-9]\\.|^ *[0-9]\\)\" /tmp/panel8.txt | head -30", "description": "Структура ответов панели"}

---

**Claude:**

Панель шести дала урожай. **Четыре движка независимо** поймали у меня арифметику: «шесть дефектов» при семи пунктах. И две находки по делу — самые важные.

---

> `Write` -- {"file_path": "C:\\Users\\dev\\.claude\\scripts\\_shared\\_patch_panel_findings.py", "content": "#!/usr/bin/env python3\n# -*- coding: utf-8 -*-\n\"\"\"Разовый патч по находкам панели шести (ретро 07.10.2026).\n\nПРИНЯТО ДВЕ НАХОДКИ КОДОМ:\n\n1. glm-5.3 #5 и gpt-5.6 #2 независимо: `prior_art` печа

---

> `Bash` -- {"command": "cd /c/Users/dev/.claude/scripts && cp prior_art.py prior_art.py.bak-pre-surfaces-20261007 && timeout 110 python _shared/_patch_panel_findings.py; echo \"patch rc=$?\"", "description": "Применяю находки панели кодом"}

---

> `Bash` -- {"command": "cd /c/Users/dev/.claude/scripts && timeout 115 python _test_ste_score.py > /tmp/tp.txt 2>&1; echo \"тест ste_score rc=$?  $(tail -1 /tmp/tp.txt)\"; echo \"=== prior_art печатает поверхности ===\"; timeout 150 python prior_art.py build test surfaces > /tmp/pas.txt 2>&1; echo \"rc=$?\";

---

> `Bash` -- {"command": "cd /c/Users/dev/.claude/scripts && python - <<'PYEOF'\nimport io\np = r\"D:\\Vault\\Vault-Knowledge\\01-Conversations\\Claude\\Retros\\retro-2026-10-07-ste100-canary-and-prior-art-blindness.md\"\ns = io.open(p, encoding=\"utf-8\").read()\nreps = [\n# 1) арифметика, которую поймали 

---

> `Bash` -- {"command": "cat \"C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_33a90300\\tasks\\b6g1z9yeq.output\" 2>/dev/null | head -8", "description": "Что упало в проверке правок"}

---

> `Bash` -- {"command": "cd /c/Users/dev/.claude/scripts && timeout 110 python - <<'EOF'\nimport sys\nsys.path.insert(0, \".\")\nimport prior_art as pa\nprint(pa.surfaces_line())\nEOF\necho \"rc=$?\"", "description": "Прямая проверка новых строк prior_art"}

---

> `Bash` -- {"command": "cd /c/Users/dev/.claude/scripts && python - <<'PYEOF'\nimport io\np = r\"D:\\Vault\\Vault-Knowledge\\01-Conversations\\Claude\\Retros\\retro-2026-10-07-ste100-canary-and-prior-art-blindness.md\"\ns = io.open(p, encoding=\"utf-8\").read()\nold = \"Проверил это на своей рельсе, а не 

---

> `Bash` -- {"command": "cd /c/Users/dev/.claude/scripts && python - <<'PYEOF'\nimport io\np = \"prior_art.py\"\ns = io.open(p, encoding=\"utf-8\").read()\nassert s.count(\"brane_ask\") == 1\nio.open(p, \"w\", encoding=\"utf-8\", newline=\"\\n\").write(s.replace(\"brane_ask\", \"brain_ask\"))\nprint(\"опечатк

---

**Claude:**

Хук поймал меня на том же классе в третий раз — и правильно. Через `sed`, без heredoc.

---

> `Bash` -- {"command": "cd /c/Users/dev/.claude/scripts && sed -i 's/brane_ask/brain_ask/g' prior_art.py && timeout 110 python -c \"import sys;sys.path.insert(0,'.');import prior_art as p;print('опечатка осталась:', 'brane_ask' in p.surfaces_line())\"", "description": "Чиню опечатку через sed"}

---

> `Bash` -- {"command": "cd /c/Users/dev/.claude/scripts && timeout 110 python change_ledger.py add --actor \"claude@HUB-01\" --operator \"dev\" --session \"voice001-ste100-20261007\" --tool \"claude-code\" --target \"~/.claude/scripts/prior_art.py, ste_score.py\" --summary \"Ретро: панель шести, 5 и

---

**Claude:**

**16:20 Лиссабон** · сессия **H11354** · разрыв между созданием и сейчас: **15 ч 03 мин** (создана 01:17 UTC, работа шла двумя присестами)

## 🔎 Сверка

Фоновый RECALL по волту досчитал и нашёл prior art, который приборы не видели: решение 04.10 и ретро 06.10 ровно про лестницу Карпати. ⚠️ **Дрифт был, и он мой**: я построил директиву из ~30 правил, тогда как в волте уже лежал замер, по которому такой набор проигрывает восьми строкам. Закрыл третьим кругом.

## 🎬 Сегодня мы поняли

Канарейка встала туда, где измерима и безопасна: чужие рельсы, флаг по умолчанию выключен. База на 258 ЖИВЫХ ответах, не на фикстуре: чистых предложений 44.3%.

A/B дал сильную дельту по форме — у codex 9.5% → 56.7%, у grok 52.0% → 78.9%, пассив в ноль у обоих. Словарь директива не чинит, объём не экономит.

Потом выяснилось, что мой скорер хвалил сам себя: 76% «чисто» при 8 жирных блоках, 7 буллетах и 7 строках таблиц. Научил его считать то, что видит читатель.

Директива v2 — мои правила плюс три строки, взятые у измеренно лучшего — взяла порог впервые: **81.0% PASS на codex при нуле жирного, буллетов и таблиц**.

И починен корень промаха: `prior_art` не обходил волт вовсе, а теперь ещё и **печатает, какие поверхности обошёл и какие не обходит** — это и была настоящая лечилка семьи из 168 случаев.

## 🎙 Вердикт Майка

- 💰 **деньги:** напрямую ноль. Косвенно — четыре строки вёрстки годятся в английское исходящее (GitHub, заявки), где двери у нас нет, а это найм и OSS-заметность.
- 🔪 **что убил бы:** первый A/B на вопросе, который сам просил «400 слов прозы». Он погасил главный эффект и дал ложный вывод. Третий круг пришлось делать заново.
- 🤺 **спарринг:** спорил честно. Три находки панели принял, три отклонил с доводом, с порогом согласился только после замера. Свой же вывод «порог не берётся» опроверг сам.
- ❓ **вопрос:** четыре строки вёрстки — в `/taste-check` для английского исходящего или оставляем только у рельс? Тот же вопрос задало ретро 06.10 и ответа не получило.

## 🔨 Панель шести: **5 из 6 ответили**

qwen отбит HTTP 404 (настройка приватности аккаунта OpenRouter), mistral упёрся в лимит и не дописал.

**Принято кодом, 2 находки:**

| находка | кто | что изменилось |
|---|---|---|
| `prior_art` печатал «обойдено 7 поверхностей», но не КАКИХ и молчал про непокрытые `02-Decisions`/`03-Insights` → «ЧИСТО» по-прежнему читалось как «этого нет», **моя правка семью НЕ закрыла** | glm-5.3 и gpt-5.6 **независимо** | печатает две строки: обойдено + не обходим с причиной |
| `--fail-under` выдавал слово `PASS`, хотя судит 6 правил из 11 | gpt-5.6 | `PASS ПО СУДИМЫМ ПРАВИЛАМ (6 из 11; словарь не проверен)` |

**Принято правкой текста, 3:** арифметика «шесть дефектов» при семи пунктах — её независимо назвали **четыре движка из пяти**; формулировка про занижение доли чистых; 81.0% не было привязано к модели и условиям.

**Отклонено с доводом:** deepseek про перевёрнутое направление провала (31.4% чистых хуже 75.8% — вывод верен), deepseek про отсутствие теста на смесь (есть, кейсы 5f и 5i), mistral про «дефолт ВЫКЛ при живом урожае» (урожай мерит вызовы, не дефолт).

**Самая острая находка — от glm про мой же kill-критерий:** как было написано, он убивал флаг, уже доказавший дельту +47 п.п., просто за низкий счётчик. Переписал на двухсоставный: дельта <+10 → убиваем всё; дельта доказана, а вызовов <20 → убиваем ФЛАГ, оставляем скорер и четыре строки. На сегодня вызовов 8 при дельте +47, значит решение по второму плечу предсказуемо — и это сказано **заранее**, а не подогнано на урожае.

## ♻️ Артефакты

| артефакт | класс | тест | перепроверено | покрытие | потребитель |
|---|---|---|---|---|---|
| `ste_score.py` | 🟢 keep | ✅ 50/50 + 11/11 | ✅ | 41% смесь → СЛЕПОЙ вслух; 100% на англ. ответе | я при чтении рельс, `--fail-under` |
| `ste_directive.md` v2 | 🟢 keep | ✅ 81.0% PASS codex | ✅ | — | `llm_ask --ste` |
| `ste_directive_micro.md` | 🟡 эталон сравнения | ✅ | ✅ | — | короткие ответы |
| `llm_ask --ste/--ste-style` | 🟢 keep | ✅ счётчик живой | ✅ | — | 8 вызовов, все в эксперименте |
| поверхности + печать в `prior_art.py` | 🟢 keep | ✅ красное доказано | ✅ пропущенное ретро = первый хит | 7 обойдено, 3 названы непокрытыми | **каждая сессия флота** |

## 🩹 Поломки: 7 (3 своих · 3 панель · 1 RECALL)

Все записаны дверью `selfheal.py`. Семья `vyvod-po-odnoy-poverhnosti` — **168 случаев с 27.07**, дверь зарегистрирована как **частичная**, честно.

О себе: **три раза** наступил на грабли, о которых `/tt` предупреждает капсом. Дважды читал код возврата после пайпа, трижды пробовал патчить код через heredoc — на третьем разе меня остановил хук `heredoc_escape_guard`. Хук сработал там, где не сработала моя дисциплина.

## 🔗 Connect · 🚂 Рельсы · 🔥 Катаклизмы

**Connect:** ✅2 используется (`prior_art` — все сессии флота; `ste_score` — я) · 🔗3 передано-ждёт (флаг, директивы, частичная дверь) · ⚠️0 в воздух.

**Рельсы:** обещал codex+grok+gemini, факт по узлу codex 58, grok 60, gemini 6. ⚠️ Честная оговорка: прибор считает УЗЕЛ за окно; мои собственные вызовы gemini все упали в 429, те 6 — соседних сессий.

**🔥 Катаклизмы:** в журнале поломок свежих чужих пожаров за 3 дня не вижу. На доске ON AIR **99 активных заявок, большинство `expired`** — доска замусорена, но это не пожар, а гигиена; упоминаю, чтобы не выглядело как тишина.

## 🐦 X-пост — **готов, оба гейта PASS, жду твоего слова**

Дверь в X сегодня **ожила** (Browser 1, локальный Windows) — вчера были мертвы все три.

```
I wrote 30 rules to make AI answers readable. My own scorer said 76 percent good.
Then I counted what a reader actually sees: 8 bold blocks, 7 bullet lists, 7 table
rows. My ruler was grading my own homework. Three borrowed lines fixed it.
```

239 знаков · `retro_x_post` PASS · `slop_gate` WARN (три ожидаемых: ровный ритм, нет «я» в англ. тексте, нет ссылки — её место в первом реплае)

**адресат:** человек, который заказывает у ИИ текст и принимает его по собственному впечатлению
**польза:** поймёт, что оценку качества нельзя брать у того же, кто текст писал
**продажа:** нет

Публикация наружу — твой «+». Канон велит публиковать сразу, но пост в публичный аккаунт я без твоего слова в этом чате не отправляю.

## 📌 Открыто

1. **Четыре строки вёрстки в английское исходящее** — ждёт твоего слова со 06.10.
2. **Формат у ревью-рельс 1/5** — доберу к урожаю.
3. **Семья из 168 случаев** — моя дверь частичная; `02-Decisions` (19069 файлов) по-прежнему слеп, его дверь это RAG, а не grep. Нужна отдельная сессия.

## 🗜 Компакт

➤ Скопируй блок целиком и вставь следующим сообщением

```bash
/compact РЕШЕНИЯ. Канарейка ASD-STE100 на чужих рельсах через llm_ask.py --ste, дефолт ВЫКЛЮЧЕН, откат = не давать флаг. Стилей два: full (~30 правил + 4 строки вёрстки) для объёмных ответов, micro (8 строк) для коротких; micro на объёмной задаче даёт предложения по 91 слову. prior_art обходит волт в части ретро и MOC и ПЕЧАТАЕТ свои поверхности + непокрытые; 02-Decisions (19069) и 03-Insights (2600) не покрыты по гейту масштаба, их дверь brain_ask. TODO. Четыре строки вёрстки в английское исходящее (ждёт слова оператора со 06.10). Формат у ревью-рельс добрать 4 из 5. Сессия починки семьи vyvod-po-odnoy-poverhnosti (168 случаев, моя дверь частичная). X-пост готов, оба гейта PASS, ждёт плюса. СЕЙЧАС. Урожай канарейки 2026-10-21, KILL двухсоставной: дельта менее +10 пп убиваем всё; дельта доказана а вызовов менее 20 убиваем флаг, оставляем скорер и 4 строки. На 07.10 вызовов 8, дельта +47. ПУТИ И ЗНАЧЕНИЯ. ~/.claude/scripts/ste_score.py, ste_directive.md, ste_directive_micro.md, _test_ste_score.py, _shared/_probe_ste_latin.py, ~/.claude/_metrics/llm_ask_partial (258 ответов база), 00-System/Shadow-First-Queue.md, 03-Insights/Operations/experiment-ste100-canary.md, 01-Conversations/Claude/Retros/retro-2026-10-07-ste100-canary-and-prior-art-blindness.md. СЧЁТЧИКИ. part-usage ste_score 175, llm_ask_ste 8 все внутри эксперимента. База корпуса 917 судимых из 2223, чистых 44.3%. A/B codex 9.5 в 56.7, grok 52.0 в 78.9, директива v2 81.0 PASS на codex при нуле жирного и буллетов. prior_art 7 поверхностей 5803 файла, 3с в 5с. Панель 5 из 6, принято 2 находки кодом и 3 текстом. ОТКРЫТО. Слово оператора про адрес 2. Формат 1 из 5. Семья 168 случаев. ИНСТРУМЕНТЫ И КОНТРАКТЫ. ste_score.py --compare ДО ПОСЛЕ, --aggregate, --fail-under N exit 3, --directive --style full|micro; exit 1 СЛЕПОЙ или нет данных, 2 ошибка входа. llm_ask.py --ste PCT --ste-style full|micro. clean_pct None при нуле судимых значит нет данных, НЕ ноль процентов. PASS печатается с оговоркой "по судимым правилам 6 из 11".
```

**🛠 Вердикты о скиллах.** `🔧 обновляю /retro` — он велит `--preset retro`, которого у нашей версии `orouter_review.py` нет, и велит `--lane eyes`, которого тоже нет; обе строки дали по отбитому прогону. Правлю в том же заходе. `✅ /tt обновлять не надо` — поймал три настоящих дефекта, а мои три нарушения его же правил это дисциплина, не инструкция.

---

🧒 **Простыми словами.** Я сделал линейку, которая мерит, насколько понятно пишет ИИ. Линейка сказала «хорошо на 76%». А потом я посчитал то, что реально видит человек — и там оказалось восемь жирных вставок, семь списков и таблица. Линейка хвалила мою же работу по моим же правилам.

Позвал шесть чужих роботов проверить мой отчёт. Пятеро ответили, четверо нашли у меня простую ошибку в счёте: написал «шесть», а пунктов было семь. Двое независимо нашли вещь поважнее: мой поисковик говорил «ничего не нашёл», не сказав, где он вообще искал. Починил — теперь он сам говорит, куда смотрел и куда не смотрел.

Сам три раза наступил на грабли, про которые в моей же инструкции написано капсом. На третий раз меня остановила не дисциплина, а автоматический сторож. Это хорошая новость про сторожа и плохая про меня.

Твист дня: мой вывод «до 80 не дотянуть» оказался неверным. Дотянули 81 — но не тем способом, который казался очевидным.
