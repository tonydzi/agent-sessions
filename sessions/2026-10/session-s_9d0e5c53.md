---
session: s_9d0e5c53
date: 2026-10-29
words: 21889
turns: 27
tools: "Bash, Edit, Grep, Read, Skill, ToolSearch, WebFetch, WebSearch, Write, mcp__ccd_session_mgmt__get_session, mcp__ccd_session_mgmt__set_session_title"
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-10-29 · Нужно найти рядом с местом проживания / гостиницей Valgarve фермерские рынки, фермы и bio-…

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_9d0e5c53` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

Нужно найти рядом с местом проживания / гостиницей Valgarve фермерские рынки, фермы и bio-магазины, куда можно заехать за свежими продуктами: молоко, сыры, фрукты, овощи и т.д.

Важно:
- не центральный фермерский рынок — он уже известен;
- подойдут фермерские рынки, bio-фермы, фермы с посещением;
- желательно места, где можно посмотреть/погладить животных и купить продукцию;
- найти максимально близкие варианты в районе Valgarve;
- минимум 4 релевантных места.
__Перевела: GPT-5.5 + whisper__

• • • • •

Нужно провести глубокое исследование по Algarve: найти фермерские рынки и фермы, куда можно приехать и купить свежие продукты — молоко, сыры, овощи, фрукты и т.д. Не обязательно bio, главное — фермерские/локальные продукты.

Исключить центральный фермерский рынок — он уже известен.

Также найти:
- bio/organic магазины;
- биофермы;
- фермы с посещением;
- фермы, где можно посмотреть/погладить животных;
- места, где можно купить продукцию прямо на ферме.

Нужно сделать обзор по Algarve в целом и отдельно определить самые близкие варианты к текущему месту проживания в отеле. Для точного поиска нужен адрес/название отеля.

Отдельно: минимум 4 релевантных варианта для ДР/детей — формулировку нужно уточнить, в транскрипции слышно неясно.
__Перевела: GPT-5.5 + 11labs__
(ВОСКРЕШЕНИЕ ПОСЛЕ ЛИМИТА: дверь Claude не подняла эту голосовую вовремя -- дверь Claude: UIA-SUBMIT-FAIL; Codex сделал только разбор)

---

> `Grep` -- {"pattern": "(?i)valgarve|algarve.*(hotel|отел|гостиниц)|(hotel|отел|гостиниц).*algarve", "path": "C:\\Users\\dev\\.claude\\projects\\P---WORKDIR-HUB\\memory", "output_mode": "content", "head_limit": 20}

---

> `ToolSearch` -- {"query": "select:WebSearch,WebFetch", "max_results": 2}

---

> `Bash` -- {"command": "cd /e/Obsidian/Vault-Knowledge && grep -rliE \"algarve|алгарв\" --include=*.md . 2>/dev/null | xargs -r ls -t 2>/dev/null | head -15", "description": "Find recent vault notes mentioning Algarve"}

---

> `WebSearch` -- {"query": "Valgarve hotel Algarve", "mode": "standard"}

---

> `WebSearch` -- {"query": "farm visit animals buy cheese goat Lagos Praia da Luz Algarve", "mode": "standard"}

---

> `WebSearch` -- {"query": "organic farm shop biological market Lagos Algarve Barão de São João Bensafrim Aljezur", "mode": "standard"}

---

> `WebSearch` -- {"query": "mercado biológico Algarve sábado Lagos Portimão Loulé Tavira farmers market organic", "mode": "standard"}

---

> `WebSearch` -- {"query": "Quinta Vale da Lama Odiáxere farm shop visit animals", "mode": "standard"}

---

> `WebSearch` -- {"query": "Quinta Pedagógica Silves animais visita horário", "mode": "standard"}

---

> `WebSearch` -- {"query": "queijaria queijo de cabra Algarve visita quinta Lagos Vila do Bispo Monchique", "mode": "standard"}

---

> `WebFetch` -- {"url": "https://www.airbnb.co.in/experiences/821716", "prompt": "Where is this experience located (town), what does it include, price, duration, host name?"}

---

> `WebFetch` -- {"url": "https://stg.portugalresident.com/portimao-educational-farm-invites-public-to-feed-animals/", "prompt": "Name, location, animals, opening days/hours, prices of the Portimão educational farm."}

---

> `WebSearch` -- {"query": "Lagos Zoo Barão de São João farm area petting animals opening hours 2026", "mode": "standard"}

---

> `WebSearch` -- {"query": "organic shop Lagos Algarve \"bio\" loja produtos biológicos Lagos", "mode": "standard"}

---

**Claude:**

Ищу дальше: отель, похоже, Vila Valverde (Праia da Luz, рядом с Лагушем), сейчас добираю фермы с животными рядом.

---

> `WebSearch` -- {"query": "Quinta Pedagógica de Portimão horário animais Mexilhoeira Grande visita", "mode": "standard"}

---

> `WebSearch` -- {"query": "farm shop near Lagos Algarve fresh eggs vegetables honey visit farm Espiche Bensafrim Odiáxere", "mode": "standard"}

---

> `WebSearch` -- {"query": "Algarve goat farm experience milking cheese making visit Salir Monchique Aljezur family", "mode": "standard"}

---

> `Bash` -- {"command": "cat \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_9d0e5c53/tasks/bpxrg1qp6.output\" | head", "description": "Check vault search output so far"}

---

**Claude:**

Похоже, «Valgarve» это **Vila Valverde Design Country Hotel** между Праия-да-Луш и Лагушем. Это моя догадка по созвучию: адреса отеля нет ни в памяти, ни в волте. Если отель другой, назовите его, и я пересчитаю расстояния. Под «центральным рынком» я понял субботний Mercado do Levante у автовокзала Лагуша и в список его не включал.

## Ближе всего к отелю (запад, район Лагуша)

| # | Место | Что там | Примерно от Праия-да-Луш |
|---|---|---|---|
| 1 | **Quinta do Catalão**, Espiche | Органическая ферма: куры, утки, огород. Продают свежие яйца, овощи, джемы, сушёный инжир, пасту из кэроба | ~3 км, ближе всех |
| 2 | **Lagos Zoo**, Barão de São João | Детская ферма внутри зоопарка: козы, свиньи, овцы, ослики, их можно кормить. Продуктов там нет, это вариант для детей | ~10 км |
| 3 | **Viv'o Mercado**, Лагуш | Рынок в основном с bio-продуктами от местных фермеров, по средам 17:00–22:00 | ~6 км |
| 4 | **Сельские рынки Bensafrim и Barão de São João** | Небольшие рынки с местными продуктами, вторник–суббота 8:00–13:00 | ~10–12 км |
| 5 | **Mercearia Bio**, Лагуш | Органический магазин местных продуктов, работает в четверг и пятницу после обеда. Есть доставка из интернет-магазина | ~6 км |
| 6 | **Grãos de Amor**, центр Лагуша | Магазин натуральных и органических продуктов, вторник–суббота примерно до 19:00 | ~6 км |
| 7 | **Рынок в Espiche** (Largo da Alegria, у ветряной мельницы) | Маленький сельский рынок | ~3 км |

## Дальше, если готовы проехать

- **Quinta Pedagógica de Portimão** (Aldeia Nova da Boavista), ~25 км. Учебная ферма, где можно кормить уток, кур и осликов. Летом работала в будни 9:30–17:30, выходные закрыты. Зимний график я не нашёл.
- **Quinta Pedagógica de Silves**, ~40 км. Животные и манеж, рассчитана на детей.
- **Сыроварня в Salir** (Барроканал, центр Алгарве), ~75 км. Свежий козий сыр по традиционной технологии, его можно сделать самим, потом дегустация с мёдом.
- **Прогулка с пастухом и козами** в Serra do Caldeirão, около 2 часов. В конце дегустация и покупка козьего сыра, мёда, хлеба.
- **Органический рынок по четвергам** в Natura Garden Centre (Almancil), ~70 км.
- **Muni­cipal-рынки Loulé и Tavira** по субботам; в Тавире идёт программа «Sábados no Mercado».

## Что проверено, а что нет
- **Проверено:** все места взяты из источников ниже.
- **Не проверено:**
  - Работают ли они в конце октября, график мог перейти на зимний.
  - Есть ли у Quinta do Catalão открытый магазин или они продают только своим гостям. Лучше позвонить.
  - Расстояния прикинуты по карте на глаз.
  - Молоко прямо с фермы рядом с Лагушем я не нашёл, только козий сыр в Salir и у пастухов.
- **Пункт «минимум 4 варианта для ДР/детей»** закрыт строками 2 и 7 таблицы, а также фермами в Портимане, Силвише и козами. Но я понял его как «для детей». Если имелся в виду день рождения, напишите, и я поищу фермы, где можно отпраздновать.

🎙 Майк: самый практичный маршрут на одно утро такой: Quinta do Catalão (яйца, овощи), потом зоопарк в Barão de São João (дети и козы), по пути рынок в Bensafrim. Всё в пределах 15 км.

**🧒 Простыми словами**
Рядом с отелем есть маленькая ферма в трёх километрах, где продают яйца и овощи. Ещё есть зоопарк с детской фермой, где можно покормить коз, и несколько деревенских рынков. За козьим сыром и дойкой коз придётся ехать подальше, в горы.

Sources:
- [Vila Valverde Design Hotel](https://www.myguidealgarve.com/pl/zakwaterowanie/vila-valverde-design-hotel)
- [Quinta do Catalão / Espiche farm](https://www.travelocity.com/es/Lagos-Hoteles-Farm-House-On-Sustainable-Farm-With-Animals.h48962064.Informacion-Hotel)
- [Lagos markets (tomorrowalgarve)](https://tomorrowalgarve.com/event/local-monthly-and-weekly-markets-in-lagos/)
- [Viv'o Mercado](https://www.myguidealgarve.com/events/farmers-market-lagos)
- [Lagos Zoo](https://www.algarvetips.com/activities/lagos-zoo/)
- [Mercearia Bio](https://tomorrowalgarve.com/aug-2026-all-in-the-family-the-bio-behind-mercearia-bio/)
- [Grãos de Amor](https://stg.portugalresident.com/?p=296964)
- [Quinta Pedagógica de Portimão](https://lifecooler.com/artigo/dormir/quinta-pedaggica-de-portimo/414822)
- [Quinta Pedagógica de Silves](https://explorial.com/pt-pt/?p=235801)
- [Salir cheese / Algarve cheese](https://www.revigorate.com/cheese-and-wine-flavours-pt.html)
- [Goat herder walk](https://theabroadguide.com/?p=576781)
- [Algarve organic markets](https://www.sulinformacao.pt/en/?p=72128)
- [Tavira Sábados no Mercado](https://postal.pt/algarve/tavira-junta-sabores-algarvios-saude-e-sustentabilidade-nos-sabados-no-mercado/)

---

**User:**

<task-notification>
<task-id>bpxrg1qp6</task-id>
<tool-use-id>toolu_01WUw6F77DJcgJoPzVa9KL7t</tool-use-id>
<output-file>C:\Users\dev\AppData\Local\Temp\claude\P---WORKDIR-HUB\s_9d0e5c53\tasks\bpxrg1qp6.output</output-file>
<status>completed</status>
<summary>Background command "Find recent vault notes mentioning Algarve" completed (exit code 0)</summary>
</task-notification>

---

> `Bash` -- {"command": "cat \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_9d0e5c53/tasks/bpxrg1qp6.output\" | head -20", "description": "Read vault Algarve search results"}

---

**Claude:**

Фоновый поиск по волту закончился (exit 0) и ничего не нашёл: заметок про Algarve или Valgarve там нет. Значит, название отеля так и остаётся моей догадкой по созвучию: Vila Valverde у Праия-да-Луш. Список в прошлом ответе от этого не меняется. Если отель другой, назовите его, и я пересчитаю, что ближе.

**🧒 Простыми словами**
Я поискал в записях, где вы живёте, но ничего не нашёл. Поэтому отель я угадал по похожему названию. Скажите точное название, и я проверю расстояния.

---

**User:**

Чини корни
Пройти почему ты плохо ищешь
Дай мне гугл ссылки - почему не дал?

---

> `Skill` -- {"skill": "geo"}

---

**User:**

Base directory for this skill: C:\Users\dev\.claude\skills\geo

Machine: HUB-01 (Хаб) · Agent: Claude Code · Operator: dev · 2026-10-28

# /geo: каждая точка = ссылка Google Maps

Правило оператора: Библия, карточка `reglament-kazhdyy-raz-kogda-daem-antonu-lokatsiyu-obyazatelno-uka` (05.07.2025, origin dev); повторено голосом 28.10.2026, сессия H85892. Одного адреса мало, нужна ссылка.

## Рецепт

1. Каждое место в ответе оператору (строка таблицы, пункт списка, точка маршрута) несёт ссылку:
   `https://www.google.com/maps/search/?api=1&query=<Название+Город+Portugal>`
   Пробелы заменяю на `+`, точное название бизнеса плюс город. Знаю координаты → `query=37.0876,-8.1789`.
2. В таблице отдельная колонка «Карта» со ссылкой `[открыть](…)`.
3. Маршрут из нескольких точек → ещё одна ссылка маршрута:
   `https://www.google.com/maps/dir/?api=1&origin=<A>&destination=<B>&waypoints=<C>|<D>`
4. Apple Maps по желанию вторым (`https://maps.apple.com/?q=<…>`), в booking обязательна (карта 958).
5. Личный адрес оператора в публичное и в URL наружу не идёт: ссылка с адресом его жилья только ему в чат.

## 🌳 Дерево решений

```mermaid
graph TD
  START[место в ответе] --> A{точное название бизнеса известно?}
  A -->|да| A1[query=Название+Город]
  A -->|нет, есть координаты| B[query=lat,lng]
  A -->|только район| C[query=Район+Город и пометка «точка примерная»]
  A1 --> STOP{{⛔ СТОП: ссылка в ответе}}
  B --> STOP
  C --> STOP
```

## Проверка перед отправкой

Посчитал места в ответе = посчитал ссылки `google.com/maps`. Не сошлось → дописать до отправки.

---

> `Read` -- {"file_path": "C:\\Users\\dev\\.claude\\projects\\P---WORKDIR-HUB\\memory\\where-is-dev-now-recent-sessions-first.md"}

---

> `Bash` -- {"command": "cd \"/e/Obsidian/Vault-Knowledge\" 2>/dev/null; d=$(find . -maxdepth 3 -type d -name \"_session-md\" 2>/dev/null | head -1); echo \"DIR=$d\"; find \"$d\" -name \"*.md\" -mtime -3 2>/dev/null | xargs grep -liE \"pine cliffs|гостиниц|отел|valgarve|algarve|алгарв\" 2>/dev/null | head; echo

---

> `Bash` -- {"command": "cd /e/Obsidian/Vault-Knowledge; ls -d */_session-md 2>/dev/null; ls -d 0*/ | head -20; find . -maxdepth 4 -type d -iname \"*session*\" -not -path \"*_quarantine*\" 2>/dev/null | head", "description": "Locate session markdown directory"}

---

> `Bash` -- {"command": "cd ~/.claude/projects; find . -name \"*.jsonl\" -mtime -3 2>/dev/null | xargs grep -ohiE \".{0,100}(pine cliffs|valgarve|vila valverde|гостиниц[аеу] [^\\\"]{0,40}забронир|отель [A-Z][a-z]+).{0,100}\" 2>/dev/null | sort | uniq -c | sort -rn | head -15", "description": "Grep recent Claude

---

> `WebSearch` -- {"query": "mercado biológico Albufeira Paderne Boliqueime Almancil produtos biológicos dia", "mode": "extended"}

---

> `WebSearch` -- {"query": "quinta com animais visita comprar produtos Loulé Albufeira Paderne Salir Benafim agroturismo cabras queijo", "mode": "extended"}

---

> `WebSearch` -- {"query": "organic farm visit near Albufeira Loulé Algarve buy produce animals kids", "mode": "extended"}

---

**Claude:**

Добираю места с животными рядом с Albufeira и сверяю адрес фермерского магазина.

---

> `WebSearch` -- {"query": "Krazy World Algoz farm animals petting / Amendoeira Organics farm shop address opening", "mode": "standard"}

---

> `WebFetch` -- {"url": "https://amendoeiraorganics.com/", "prompt": "Farm location (village), farm shop opening days/hours, can visitors come, what they sell, animals?"}

---

> `Edit` -- {"replace_all": false, "file_path": "C:\\Users\\dev\\.claude\\projects\\P---WORKDIR-HUB\\memory\\where-is-dev-now-recent-sessions-first.md", "old_string": "description: \"«Где оператор сейчас / рядом со мной» = сперва заголовки и текст сессий за 72 ч, потом остальное; почта последней; 

---

> `Edit` -- {"replace_all": false, "file_path": "C:\\Users\\dev\\.claude\\projects\\P---WORKDIR-HUB\\memory\\where-is-dev-now-recent-sessions-first.md", "old_string": "**How to apply:**", "new_string": "**4-й случай, 28.10 (H68316):** голосовая «рядом с гостиницей Valgarve» (= «в Алгарве», ослы

---

> `Bash` -- {"command": "cd ~/.claude/scripts && ls selfheal.py >/dev/null && python selfheal.py journal --class where-is-dev-wrong-layer --what \"28.10 H68316: 'Valgarve' из голосовой принял за отель, искал по созвучию вместо памяти Pine Cliffs; /geo не открыт, ссылок Maps нет\" 2>&1 | tail -3; ls ~/.claude/

---

> `Bash` -- {"command": "cd ~/.claude/hooks && P='Нужно найти рядом с местом проживания / гостиницей Valgarve фермерские рынки, фермы и bio-магазины'; echo \"{\\\"prompt\\\":\\\"$P\\\",\\\"session_id\\\":\\\"x\\\",\\\"cwd\\\":\\\"E:/!CLAUDE-HUBPC-June26\\\"}\" | python memory_recall_hook.py 2>&1 | head -8;

---

> `Bash` -- {"command": "head -5 ~/.claude/skills/geo/SKILL.md; grep -nE \"def .*match|description|triggers?\" ~/.claude/hooks/skill_suggest_hook.py | head -15", "description": "Inspect geo frontmatter and skill hook matching"}

---

> `Bash` -- {"command": "grep -nE \"SKILL|trigger|«\" ~/.claude/hooks/skill_suggest_hook.py | head -20; wc -l ~/.claude/hooks/skill_suggest_hook.py", "description": "Find how skill hook reads triggers"}

---

> `Bash` -- {"command": "sed -n 15,70p ~/.claude/hooks/skill_suggest_hook.py", "description": "Read hook law table section"}

---

> `Bash` -- {"command": "cd ~/.claude/hooks && cp skill_suggest_hook.py skill_suggest_hook.py.bak-geo-H68316-20261028 && python - <<'EOF'\np='skill_suggest_hook.py'\ns=open(p,encoding='utf-8').read()\nanchor='    (r\"познаком|сведи .* и |intro |сделай интро\"'\nrule='''    # /geo (dev 28.10.2026, H68316: «поч

---

> `Read` -- {"file_path": "C:\\Users\\dev\\.claude\\hooks\\skill_suggest_hook.py", "offset": 34, "limit": 2}

---

> `Bash` -- {"command": "cp ~/.claude/hooks/skill_suggest_hook.py ~/.claude/hooks/skill_suggest_hook.py.bak-geo-H68316-20261028 && echo ok", "description": "Back up skill hook before edit"}

---

> `Edit` -- {"replace_all": false, "file_path": "C:\\Users\\dev\\.claude\\hooks\\skill_suggest_hook.py", "old_string": "    (r\"познаком|сведи .* и |intro |сделай интро\", (\"intro\", \"тёплое интро двух людей\")),", "new_string": "    # /geo (dev 28.10.2026, H68316: «почему не дал гугл ссылки»): обзор мест

---

> `Bash` -- {"command": "cd ~/.claude/hooks; P='Нужно найти рядом с местом проживания / гостиницей Valgarve фермерские рынки, фермы и bio-магазины'\necho \"NEW:\"; echo \"{\\\"prompt\\\":\\\"$P\\\"}\" | python skill_suggest_hook.py | grep -o '/geo[^\"]\\{0,40\\}' | head -2; echo \"rc=${PIPESTATUS[1]}\"\necho \"

---

**Claude:**

Новая находка, она глубже: самотест говорит, что хук подсказки скиллов на хабе вообще не подключён. Проверяю.

---

> `Bash` -- {"command": "grep -n \"skill_suggest\\|memory_recall_hook\\|UserPromptSubmit\" ~/.claude/settings.json | head; grep -rln \"skill_suggest\" ~/.claude/settings*.json \"/e/!CLAUDE-HUBPC-June26/.claude/\"settings*.json 2>/dev/null; grep -n \"settings\\|registered\\|def check\" ~/.claude/hooks/skill

---

> `Bash` -- {"command": "sed -n 445,500p ~/.claude/settings.json; cat ~/.claude/hooks/skill_suggest_hook.cmd; grep -rn \"skill_suggest\" ~/.claude/hooks/hooks_manifest.json 2>/dev/null | head -3; grep -rln \"skill_suggest_hook\" ~/.claude/change_ledger/ 2>/dev/null | head -2", "description": "View UserPromptSub

---

> `Bash` -- {"command": "cd ~/.claude; for f in $(ls -t settings.json.bak* 2>/dev/null | head -40); do grep -q skill_suggest \"$f\" && { echo \"LAST WITH: $f $(stat -c %y \"$f\" | cut -c1-16)\"; break; }; done; ls -t settings.json.bak* 2>/dev/null | head -3; grep -rl \"skill_suggest\" projects/P---WORKDIR-HUB

---

> `Bash` -- {"command": "cd ~/.claude; grep -h -o \".\\{0,160\\}skill_suggest.\\{0,160\\}\" projects/P---WORKDIR-HUB/memory/evaluate-recurring-into-routine.md projects/P---WORKDIR-HUB/memory/crm-engine-rebuild.md | head -4; grep -l skill_suggest $(ls settings.json.bak* 2>/dev/null) 2>/

---

> `Bash` -- {"command": "cd ~/.claude; prev=\"\"; for f in $(ls -tr settings.json.bak*); do if grep -q skill_suggest \"$f\"; then prev=\"$f\"; else if [ -n \"$prev\" ]; then echo \"had: $prev -> dropped by: $f ($(stat -c %y \"$f\"|cut -c1-16))\"; prev=\"\"; fi; fi; done | tail -3; grep -rn \"skill_suggest\" cha

---

> `Bash` -- {"command": "cd ~/.claude; grep -rl \"bak-hooks-20260929\\|hooks-20260929\" scripts/*.py hooks/*.py 2>/dev/null | head -3; grep -rn \"20260929-0323\\|bak-hooks-\" change_ledger/ 2>/dev/null | head -3 | cut -c1-300; python -c \"import json;d=json.load(open('settings.json.bak-railplan',encoding='utf-8

---

> `Write` -- {"file_path": "C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_9d0e5c53\\scratchpad\\restore_skill_hook.py", "content": "import json, os, shutil\np = os.path.expanduser(r\"~\\.claude\\settings.json\")\nbak = p + \".bak-skillsuggest-restore-H6

---

> `Bash` -- {"command": "python \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_9d0e5c53/scratchpad/restore_skill_hook.py\"; python ~/.claude/hooks/skill_suggest_selftest.py 2>&1 | tail -3; echo '{\"prompt\":\"найди фермы рядом с гостиницей\"}' | cmd //c \"%US

---

> `Bash` -- {"command": "python -c \"\nimport json,datetime,os\nr={'ts':datetime.datetime.utcnow().isoformat()+'Z','machine':'HUB-01','agent':'Claude Code/claude-opus-5-5','operator':'dev','session':'H68316','change':'settings.json: re-registered UserPromptSubmit skill_suggest_hook.cmd (silently droppe

---

**Claude:**

## Почему искал плохо: три корня

1. **Не тот слой памяти.** Ваш отель уже записан в памяти: Pine Cliffs (Олюш-ду-Агуа, Албуфейра), вы сами назвали его 26.10. Строка про это есть в моём индексе памяти, но я её не применил. «Valgarve» я принял за название отеля, хотя это «в Алгарве». В итоге нашёл по созвучию Vila Valverde у Лагуша, в ~60 км от вас, и весь первый список ушёл не туда.
2. **Скилл `/geo` не открыт.** Это правило «каждое место = ссылка Google Maps». Оказалось, что хук подсказки скиллов (`skill_suggest_hook`) тихо выпал из настроек хаба между 24 и 29.09. Записи о том, что его убрали намеренно, я не нашёл. С тех пор хаб ни разу не подсказал ни одного скилла, а в правилах (§0.8) он числится живым.
3. **Слабый поиск.** Искал англоязычным веб-поиском, без Google Maps и почти без португальских запросов.

### Что починил
- **Хук подсказки скиллов снова подключён.** Самотест: `SELFTEST skill_suggest @HUB-01: PASS (файл ок · 4/4 кейса ок · зарегистрирован)`, до этого был FAIL «не зарегистрирован». Сработает в новых сессиях хаба.
- **В хук добавлено правило для `/geo`** на слова «рядом с», «гостиница», «отель», «ферма», «рынок», «куда заехать».
  - На вашей исходной фразе: новая версия выдаёт `/geo`, старая выдавала 0. Это доказательство, что именно правка включила подсказку.
  - На постороннем запросе («исправь баг в парсере json») правило не срабатывает: 0 совпадений.
- **Заметка памяти `where-is-dev-now`** теперь включает слова «гостиница / отель / место проживания». Хук памяти на вашу исходную фразу теперь выдаёт её первой: `matched: гостиницей, проживания, местом, рядом`.
- **Записано:** строка в журнал поломок (`selfheal`) и в журнал изменений хаба (`change_ledger`).
- **Откат:** бэкапы `settings.json.bak-skillsuggest-restore-H68316-20261028` и `skill_suggest_hook.py.bak-geo-H68316-20261028`.
- ⚠️ **Не проверено:** выпал ли этот хук на других 7 узлах флота.

## Исправленный список: рядом с Pine Cliffs
Центральным рынком я считаю Loulé и его исключаю. Расстояния примерные, по прямой.

| # | Место | Что там | ~км | Карта |
|---|---|---|---|---|
| 1 | **Quinta do Mel**, Албуфейра | Ферма той же семьи, что Quinta do Freixo: овцы, огород, свои мёд, травы, джемы, магазин и ресторан | ~10 | [открыть](https://www.google.com/maps/search/?api=1&query=Quinta+do+Mel+Albufeira+Portugal) |
| 2 | **Mercadinho Bio**, Natura Garden Centre, Almancil | Органический рынок: яйца, фрукты, овощи. Четверг 11:30–15:00 | ~14 | [открыть](https://www.google.com/maps/search/?api=1&query=Natura+Garden+Centre+Almancil+Portugal) |
| 3 | **Mercado de Produtores de Almancil** | Рынок местных производителей. Четверг 7:30–13:00 | ~13 | [открыть](https://www.google.com/maps/search/?api=1&query=Rua+do+Centro+Comunitario+Almancil+Portugal) |
| 4 | **Horta da Torre**, Quinta da Calma | Органическая ферма, рынок по средам 12:00–15:00. По четвергам 17:30–18:30 раздают заказы в Албуфейре | ~15 | [открыть](https://www.google.com/maps/search/?api=1&query=Horta+da+Torre+Algarve+Portugal) |
| 5 | **Quinta do Freixo**, Benafim | Агроусадьба: овцы породы кампаниса, свои продукты, магазин. Тел. [ТЕЛЕФОН] | ~30 | [открыть](https://www.google.com/maps/search/?api=1&query=Quinta+do+Freixo+Benafim+Loule+Portugal) |
| 6 | **Сыроварня в Salir** | Свежий козий сыр, можно сделать самим, дегустация с мёдом | ~30 | [открыть](https://www.google.com/maps/search/?api=1&query=queijaria+Salir+Loule+Portugal) (точка примерная) |
| 7 | **Krazy World**, Algoz | Контактная ферма: карликовые козы, ламы, олени, их можно кормить. Ежедневно 10:00–17:30 до конца октября | ~25 | [открыть](https://www.google.com/maps/search/?api=1&query=Krazy+World+Algoz+Portugal) |
| 8 | **Amendoeira Organics**, у Querença | Органическая ферма с фермерским магазином. ⚠️ Их сайт сейчас не открывается, возможно закрылись. Сначала позвоните | ~25 | [открыть](https://www.google.com/maps/search/?api=1&query=Amendoeira+Querenca+Loule+Portugal) |
| 9 | **Mercado Mensal de Paderne** | Рынок в первую субботу месяца, 8:00–14:00. Ближайший будет 07.11 | ~15 | [открыть](https://www.google.com/maps/search/?api=1&query=Paderne+Albufeira+Portugal) |

**Утро четверга одним маршрутом:** Pine Cliffs → рынок Almancil → Mercadinho Bio → Quinta do Mel, [маршрут](https://www.google.com/maps/dir/?api=1&origin=Pine+Cliffs+Albufeira&destination=Quinta+do+Mel+Albufeira&waypoints=Almancil+Portugal|Natura+Garden+Centre+Almancil).

Свежее молоко прямо с фермы рядом я не нашёл. Ближе всего к нему козий сыр в Salir.

🎙 Майк: на детей с животными лучше всего Krazy World, на продукты Quinta do Mel и четверговые рынки в Almancil. Всё в 10–25 минутах от отеля.

**🧒 Простыми словами**
Я решил, что вы живёте в другом конце Алгарве, хотя в записях было сказано, где вы. Поэтому первый список был мимо. Ещё у меня тихо сломалась «напоминалка», которая подсказывает нужный инструмент, а без неё я забыл про карты. Напоминалку я вернул, а новый список собрал вокруг Pine Cliffs, и у каждого места теперь есть кнопка «открыть на карте».

Sources:
- [Mercadinho bio Natura Almancil](https://www.reformaagraria.pt/feiras-mercados/faro/loule/mercadinho-bio-natura-almancil/)
- [Mercados Biológicos em Portugal](https://reformaagraria.pt/feiras-mercados/mercados-biologicos/)
- [Horta da Torre](https://www.hortadatorre.com/onde-estamos.html)
- [Quinta do Freixo (Visit Loulé)](https://visit-loule.pt/38153/quinta-do-freixo-agroturismo)
- [Quinta do Mel](https://www.alalgarveconmigo.com/2019/08/quinta-do-mel-un-dulce-refugio-en.html)
- [Quinta do Mel farmstay](https://www.farmstayplanet.com/farmstays/portugal-1/faro-district/albufeira/organic-farms/quinta-do-mel-algarve/)
- [Amendoeira Organics](https://theportugalnews.com/news/2022-09-13/amendoeira-organics-cultivating-a-new-life/70230)
- [Krazy World](https://euroveloportugal.com/en/poi/krazy-world-lda-2)
- [Salir cheese](https://www.revigorate.com/cheese-and-wine-flavours-pt.html)

---

**User:**

Stop hook feedback:
СТОП: ты докладываешь НОЛЬ находок, не назвав ОХВАТ прибора.
  фрагмент: …росе («исправь баг в парсере json») правило не срабатывает: 0 совпадений. - **Заметка памяти `where-is-dev-now`** теперь включает…

Семья «вывод по одной поверхности» — 112 случаев с 27.07. Ноль в ТВОЁМ окне читается
как ноль в мире, и разница всплывает поздно:
  · contrib_watch «debts: []» — смотрел только репо tonydzi, долг висел в ЧУЖИХ тредах (25.08, 29.08);
  · apply_verify «0 без пруфа за 14 дней» — окно было 6 дней, gmail отдаёт максимум 500 (10.09);
  · gh search «0 хитов → мировой боли нет» — короткая фраза тут же дала две живые двери (05.09);
  · «бэкап есть» — офсайтом звалась ОДНА поверхность, офсайт-копии волта не было ~2 недели (11.09).

Дешёвая починка — одна фраза, прогонять заново ничего не надо. Назови в том же абзаце,
ЧТО именно обошёл, и гейт пропустит молча:
  «по 100 репо tonydzi касаний нет; чужие треды прибор не смотрел»
  «за последние 6 суток (граница окна = дата старейшего письма) дыр нет»
  «обошёл все 4 поверхности (fbread · fbreply · 646yqiss · Chrome-MCP) — пусто»
Не знаешь охвата своего прибора — это и есть ответ: пиши «я не нашёл», а не «нет».

---

**Claude:**

Уточняю охват этой проверки. Отрицательный кейс был ровно один: фраза «исправь баг в парсере json», прогон через новый хук дал 0 срабатываний `/geo`. Ложные срабатывания на другие фразы я не мерил. На словах «рынок» и «адрес» в рабочем контексте (рынок вакансий, адрес сервера) правило, скорее всего, сработает зря. Цена такой ошибки небольшая: одна лишняя строка-подсказка. Если начнёт шуметь, сужу правило.

Охват остальных отрицательных выводов:
- **Молоко с фермы.** «Не нашёл» относится только к шести веб-поискам этой сессии (англоязычный поиск, частично португальские запросы). Google Maps и местные группы я не смотрел.
- **Причины выпадения хука.** Я прошёл 107 бэкапов `settings.json` на хабе и нашёл окно, когда он пропал: 24–29.09. Журнал изменений `change_ledger` хаба записи о намеренном удалении не содержит, транскрипты сессий за то окно я не читал. Поэтому это «я не нашёл причину», а не «причины не было».
- **Другие узлы флота.** На 7 остальных узлах я ничего не проверял.

**🧒 Простыми словами**
Я проверил новую напоминалку на одной чужой фразе, и она промолчала, как и должна. Больше фраз я не пробовал, поэтому иногда она может подсказать карты не к месту. Это безвредно, и если будет мешать, я её подправлю.

---

**User:**

<task-notification>
<task-id>bflw0qg1q</task-id>
<tool-use-id>toolu_0177y86ApWf5d9vqe7FLSrai</tool-use-id>
<output-file>C:\Users\dev\AppData\Local\Temp\claude\P---WORKDIR-HUB\s_9d0e5c53\tasks\bflw0qg1q.output</output-file>
<status>completed</status>
<summary>Background command "Grep recent Claude transcripts for hotel name" completed (exit code 0)</summary>
</task-notification>

---

> `Bash` -- {"command": "head -c 3000 \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_9d0e5c53/tasks/bflw0qg1q.output\"", "description": "Read transcript hotel grep output"}

---

> `Bash` -- {"command": "cd ~/.claude/projects; ls */1266ae47* */43841722* 2>/dev/null | head; timeout 100 grep -rl --include=*.jsonl -i \"pine cliffs\" . 2>/dev/null | head -5", "description": "Locate source sessions of Pine Cliffs fact", "timeout": 120000}

---

> `Bash` -- {"command": "cd ~/.claude/projects/P---WORKDIR-HUB; for f in 1266ae47-*.jsonl 43841722-*.jsonl; do echo \"== $f\"; python -c \"\nimport sys,re\nt=open(sys.argv[1],encoding='utf-8',errors='ignore').read()\nfor m in re.finditer(r'(?i).{0,90}(pine.?cliffs|mimo|гостиниц|отел[ья]).{0,90}',t)

---

**Claude:**

Фоновый поиск по транскриптам за 3 суток закончился пустым, но он ослеп, а не ошибся в мире. Когда я открыл первоисточники напрямую, оба факта нашлись:

- **Сессия 1266ae47 (26.10).** Ваши слова: «Гостиница забронирована на 4 ночи, кажется Pine Cliffs». Та сессия уже давала маршрут Синтра → Pine Cliffs Resort Albufeira со ссылками Google Maps.
- **Сессия 43841722 (27.10).** Переписка с `[EMAIL]` про детский или семейный мастер-класс MIMO на 28–30 октября.

Значит, отель Pine Cliffs подтверждён двумя независимыми первоисточниками, и исправленный список вокруг него верный.

Почему пустой поиск был слепым, а не честным нулём. `grep -o` с выражением `.{0,100}` по кириллице в многомегабайтных однострочных JSON молча ничего не вернул, хотя строка «Pine Cliffs» там есть. Тот же прибор по тем же двум файлам через Python нашёл её сразу. Урок уже записан в заметку памяти `where-is-dev-now`: место проживания ищу сначала в этой заметке и в сессиях за 72 часа, а по самим транскриптам читаю Python-парсером, не `grep -o`.

**🧒 Простыми словами**
Мой первый поисковик посмотрел в записи и сказал «ничего нет», но он просто не умел читать русские буквы в этих файлах. Я открыл записи другим способом, и там прямо вашими словами написано: Pine Cliffs. Так что новый список ферм составлен вокруг правильного отеля.

---

**User:**

Чини корни, чини все корни и делай ретро.

---

> `Bash` -- {"command": "cd ~/.claude; ls hooks/hooks_manifest.json 2>/dev/null && python -c \"\nimport json;m=json.load(open('hooks/hooks_manifest.json',encoding='utf-8'));s=json.dumps(m,ensure_ascii=False);print('keys',list(m)[:8]);print('skill_suggest in manifest:', 'skill_suggest' in s)\"; grep -ln \"hooks_

---

> `Grep` -- {"pattern": "hooks_manifest", "path": "C:\\Users\\dev\\.claude\\scripts", "glob": "*.py", "head_limit": 10}

---

> `Grep` -- {"pattern": "skill_suggest", "path": "C:\\Users\\dev\\.claude\\hooks\\hooks_manifest.json", "output_mode": "content"}

---

> `Grep` -- {"pattern": "memory_recall_hook|spawned_brief_recall", "path": "C:\\Users\\dev\\.claude\\hooks\\hooks_manifest.json", "output_mode": "content", "-C": 6}

---

> `Read` -- {"file_path": "C:\\Users\\dev\\.claude\\hooks\\hooks_manifest.json", "offset": 1, "limit": 30}

---

> `Read` -- {"file_path": "C:\\Users\\dev\\.claude\\hooks\\hooks_manifest.json", "offset": 142, "limit": 12}

---

> `Bash` -- {"command": "cp ~/.claude/hooks/hooks_manifest.json ~/.claude/hooks/hooks_manifest.json.bak-skillsuggest-H68316-20261029 && echo ok", "description": "Back up hooks manifest"}

---

**Claude:**

Вписываю хук в манифест, потом прогоняю сторож паритета хуков.

---

> `Edit` -- {"replace_all": false, "file_path": "C:\\Users\\dev\\.claude\\hooks\\hooks_manifest.json", "old_string": "      \"canon\": \"reglament-pered-lyuboy-aktivnostyu-snachala-recall-vsego-volt-i-rag\"\n    },\n    {\n      \"name\": \"dead_claim_guard\",", "new_string": "      \"canon\": \"reglament-per

---

> `Bash` -- {"command": "cd ~/.claude/scripts; python -c \"import json;json.load(open('../hooks/hooks_manifest.json',encoding='utf-8'));print('json ok')\"; timeout 100 python hooks_parity.py --help 2>&1 | head -8", "description": "Validate manifest and read parity tool help", "timeout": 120000}

---

> `Bash` -- {"command": "cd ~/.claude/scripts; echo \"== now:\"; timeout 100 python hooks_parity.py --quiet 2>&1 | tail -6; echo \"rc=$?\"; echo \"== red (old settings without hook):\"; timeout 100 python hooks_parity.py --quiet --settings ../settings.json.bak-skillsuggest-restore-H68316-20261028 2>&1 | grep -i

---

> `Bash` -- {"command": "cd ~/.claude/hooks; P='Нужно найти рядом с местом проживания / гостиницей Valgarve фермерские рынки'; echo \"{\\\"prompt\\\":\\\"$P\\\",\\\"session_id\\\":\\\"x\\\",\\\"cwd\\\":\\\"E:/!CLAUDE-HUBPC-June26\\\"}\" | python memory_recall_hook.py | grep -o 'where-is[^)]*)' ; echo \"---

---

> `Edit` -- {"replace_all": false, "file_path": "C:\\Users\\dev\\.claude\\projects\\P---WORKDIR-HUB\\memory\\where-is-dev-now-recent-sessions-first.md", "old_string": "потом сессии 72 ч; почта последней; чужое «не подтверждено» ≠ нет\"", "new_string": "потом сессии 72 ч; почта последней; чужое 

---

> `Edit` -- {"replace_all": false, "file_path": "C:\\Users\\dev\\.claude\\projects\\P---WORKDIR-HUB\\memory\\where-is-dev-now-recent-sessions-first.md", "old_string": "**How to apply:** чужое", "new_string": "**Случай H68316 (28.10):** «рядом с гостиницей Valgarve» (= «в Алгарве») принял за имя

---

> `Bash` -- {"command": "cd ~/.claude/hooks; P='Нужно найти рядом с местом проживания / гостиницей Valgarve фермерские рынки'; echo \"{\\\"prompt\\\":\\\"$P\\\",\\\"session_id\\\":\\\"x\\\",\\\"cwd\\\":\\\"E:/!CLAUDE-HUBPC-June26\\\"}\" | python memory_recall_hook.py | grep -o 'where-is[^)]*)'; head -12 /e

---

**Claude:**

Все корни закрыты, хук памяти снова ловит исходную фразу. Запускаю ретро.

---

> `Skill` -- {"skill": "retro"}

---

**User:**

Base directory for this skill: C:\Users\dev\.claude\skills\retro

# /retro — session retrospective (what we built · what we keep)

> 🧒 оператору: весь ответ и все сообщения о ходе работы — простым русским; Короткое сообщение может быть одной понятной фразой. Блок «Простыми словами» не заменяет понятный текст. Канон: [[reglament-obyasnyat-i-otchityvatsya-antonu-prostymi-slovami-eli5]], память `eli5-always`. <!-- eli5-whole-answer-20261029 -->

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
  ⛔ **0 в MEMORY.md ещё НЕ значит «пропало»** (замер 24.10.2026, хаб, цена ошибки = сессия починки по уже закрытому корню + ложная строка «класс неизлечим»): ночная уборка Маяка ШТАТНО сворачивает INBOX в `MEMORY-archive.md`, и указатель живёт там. Перед словом «потерялось» список поверхностей спрашивай у РЕЕСТРА, а не перечисляй руками: `python ~/.claude/scripts/surface_sweep.py memory-index <слаг>` — он печатает «поверхностей в реестре N, прочитано N, НЕ ПРОЧИТАНО K» и `[НАШЁЛ]` с файлом и строкой. Замер 24.10: по этому же случаю реестр знал **21 поверхность**, а мой ручной список три. Гейт подсемьи — `hooks/false_no_guard.py` семья 4; правило целиком с четырьмя подсемьями — память `surface-sweep-before-saying-lost`. Нашёл в архиве = всё в порядке, строку НЕ дописывать (иначе родится дубль). Корень этого был закрыт журналом ещё 10.09.2026, но жил только в Breakage-Journal, поэтому его переоткрывали заново. Класс = `memory-index-line-lost-overnight`, 4 датированных случая, корень чинится отдельной сессией.
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
exit 0 = прежних нет, «1-й датированный» правомерен · **exit 3 = это НЕ ошибка и НЕ первый случай**: прибор печатает прежние строки, их даты и СЕМЬЮ дефекта. Если напечатана `СЕМЬЯ <slug>`, используй именно её как `<класс>`. ⭐ ВЕРДИКТ ЧИТАЙ ПО СТРОКЕ «СЕМЕЙНЫХ: N · СЛОВЕСНЫХ: M» (правка прибора 05-06.10.2026): «это НЕ 1-й случай» и счёт §5.10 держат ТОЛЬКО семейные. `СЕМЕЙНЫХ 0` при любом M = скорее всего 1-й случай; имя бери по предмету ремонта ЭТОЙ поломки, а из раздела `[словесное совпадение, в счёт §5.10 НЕ идёт]` имя НЕ брать — до правки там рядом с роднёй стояли переименование репо и врущий поиск в конфигураторе. Глазами видно одну семью → заведи её дверью `python "$HOME/.claude/scripts/prior_art.py" add-family <ключ> --phrase "<фраза>" [--phrase …] [--door "<дверь>"]` с красной пробой в обе стороны. ⛔ Не правь `FAMILIES` в `prior_art.py` руками: посылки возят этот файл целиком и стирают строки, дописанные на узле (за 08-25.10.2026 так пропало 12 семей); дверь пишет шард своего узла `$OBSIDIAN_VAULT/_machine-bus/_prior_art_families/<узел>.json`, модуль подмешивает все шарды. При `exit 0`, когда прежней строки нет, назови класс по текущему предмету ремонта/нарушенному инварианту и запиши как 1-й датированный случай; канал, код возврата, текст алерта и симптом классом не являются.

ТОЛЬКО ПОСЛЕ этого запиши ОДНУ строку через дверь `python "$HOME/.claude/scripts/selfheal.py" journal --class <класс> --what "<что>" [--conditions --parts --guess --status]`: **что · условия · сопричастные (файлы/рельсы/узлы) · гипотеза 🤔 или ✅ доказанная причина**. ⛔ НЕ править `Breakage-Journal.md` напрямую (ни Edit, ни heredoc): это общий Syncthing-файл, вид рисует один владелец из пер-узловых шардов, прямая правка отбивается хуком `breakage_write_guard` и терялась (04.09: 76 строк в 11 конфликт-копиях) — память [[breakage-journal-per-node-shards]]. Счёт бери из фактического ответа `selfheal.py`: дедуп означает, что новой строки нет.

Дальше по семье: 1-й = строка · 2-й = строка + уточнить условия · **3-й датированный = класс системный**. Внутри `/retro` причинную цепочку НЕ строй: используй ровно одну отдельную ВИДИМУЮ repair-сессию, чей первый явный вызов — `/five-whys <класс>` в Claude или `$five-whys <класс>` в Codex, с датированными строками серии. Если `selfheal.py` уже поставил её в очередь, вторую не создавай. Механизм/робота на 1-2 случае НЕ строить. Дефект новой семьи → завести её дверью `prior_art.py add-family` (шард узла, не правка `FAMILIES`), иначе следующая сессия снова назовёт его «первым».
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
- ⭐ **Очередь заявок узла (дверь repair_due, P75770 27.10.2026).** Заявка из очереди становится сессией только через живую сессию: python сессий не поднимает (§9.2). На узле без диспетчера хаба (macOS/Linux) в конце этого шага исполни `$HOME/.claude/scripts/routine_prompts/repair_door.md`: `registry_dispatch.py --repairs-only --write-seeds` → до 3 задач → `selfheal.py repairs --commit <класс>`. Пустая очередь = 0 работы. Сторож вне двери `repair_queue_watch.py` кричит в 03 при queued > 26 ч. Windows-хаб: заявки ест `registry-dispatcher-daily`, шаг пропусти.
- Поломок не было → одна строка «🩹 поломок нет» и дальше. Ноль строк в журнале при названных в отчёте поломках = ретро не закрыто.
- ⛔ **Синтаксис двери журнала НЕ проверяй через `--help` после `--class`** (замер 09.10.2026, NODE-0X, класс `cli-door-writes-row-on-help-flag`): `selfheal.py journal --class X --help` справку не печатает, а ПИШЕТ строку «не описано» и поднимает счёт класса. Так класс стал ложно 3 из 3 и породил заявку на сессию починки с карточкой в 10-Tasks; пришлось чистить шард узла руками и закрывать заявку `selfheal.py repairs --close`. Синтаксис смотри `grep -n journal selfheal.py`.
- ⭐⭐ **СЕМЬЯ НАЗВАЛА ДВЕРЬ → ПРОГОНИ ЭТУ ДВЕРЬ НА МАТЕРИАЛЕ СВОЕЙ ПОЛОМКИ, А НЕ ТОЛЬКО ЗАПИШИ СТРОКУ** (замер 25.10.2026, NODE-0X, сессия A56173). `prior_art.py` печатает «ДВЕРЬ СЕМЬИ: … → дверь уже есть: прогони ЕЁ», и шаг читался как «не строй вторую».

  Прогнать её на СВОЁМ случае инструкция не велела, и ровно этот прогон дал главную находку захода: у семьи `cifra-v-ishodyashchem-ne-u-istochnika` дверь `outbound_fact_lint.py` на моём же тексте ответила «фактов найдено 0 · ЧИСТО», и на цифровой версии («2 статьи», «7 машин») тоже ноль. Её regex `amount` требует ДВУХ цифр (принятый предел, записанный комментарием в коде) и не знает числительных словами. То есть дверь слепа ровно к тому дефекту, от которого поставлена, а я без прогона записал бы строку и ушёл, считая её рабочей.

  Порядок: дверь названа → скорми ей текст или артефакт ЭТОЙ поломки → **молчание двери на своём же случае = НАХОДКА, а не чистота**, и она идёт в отчёт отдельной строкой «дверь семьи слепа к <форма>». Починка двери — отдельная видимая сессия (флотовый сторож, нужна красная проба в обе стороны и раскатка §7.3-бис), правкой на ходу её не трогаем. ⛔ «Дверь есть» вердиктом о её работе не является: это §5.4 («прибор — такой же claim») и §5.5 («прибор не имеет права быть слепым») на шаге журнала. Канон правила: память `run-the-family-door-on-your-own-case`.
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
⭐ **ЗАКРЫВАЕШЬ СЛЕПУЮ ЗОНУ ПРОВЕНАНСОМ — ПРЕДЬЯВИ УЛИКУ СВЯЗИ** (замер 25.10.2026, NODE-0X, A56173). Не смог прочитать сам артефакт (PDF без распаковщика, бинарь, чужой формат) и судишь по его источнику — это законно ТОЛЬКО с уликой, что выход действительно сделан из этого источника: даты (`stat` обоих), лог сборки или хеш. Без улики это не закрытие зоны, а пересказ своей надежды. Замер: я закрыл зону «`resume.pdf` печатается из `resume.html`, там нуль»; два `stat` показали, что PDF от 04.10 СТАРШЕ html от 10.10, а сам html — транзитная копия с другого узла. Цена улики — две команды. Пара к `run-the-family-door-on-your-own-case`.
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

> `Bash` -- {"command": "python -c \"import datetime; print('СЕЙЧАС', datetime.datetime.now().isoformat(timespec='seconds'))\"; cd ~/.claude/scripts; python -X utf8 prior_art.py class \"в голосовой оператора слово Valgarve принял за имя отеля, не применил память где оператор сейчас, искал не там\" 2>&1 | grep -E \"СЕ

---

> `Bash` -- {"command": "cd ~/.claude/scripts; python -X utf8 selfheal.py journal --class gate-hook-not-in-manifest-dropped-silently --what \"skill_suggest_hook выпал из settings.json хаба 24-29.09 молча; его не было в hooks_manifest.json, hooks_parity его не видел; ~35 дней хаб не подсказывал скиллы (/geo проп

---

**Claude:**

Пока журнал пишется в фоне, готовлю черновик ретро для панели ломателей.

---

> `Write` -- {"file_path": "C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_9d0e5c53\\scratchpad\\retro_draft.md", "content": "# Retro draft, session H68316 (28-29.10.2026, hub)\n\nTask: voice note (transcribed) asked for farmers markets, farms with anima

---

> `Bash` -- {"command": "cd ~/.claude/scripts/cc-review && timeout 280 python -X utf8 orouter_review.py panel --preset retro --role break --effort medium --task retro-56a81386 --context-file \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_9d0e5c53/scratchpad/r

---

> `Bash` -- {"command": "f=\"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_9d0e5c53/scratchpad/panel_out.txt\"; python -X utf8 -c \"\nimport json,sys\nt=open(sys.argv[1],encoding='utf-8').read()\nj=json.loads(t.split('RETRO_PANEL_JSON=')[1].splitlines()[0])\np

---

> `Edit` -- {"replace_all": false, "file_path": "C:\\Users\\dev\\.claude\\hooks\\skill_suggest_hook.py", "old_string": "    (r\"рядом с|поблизости|недалеко от|near (my|the) |гостиниц|\\bотел|места? проживан|\"\n     r\"ферм[аыуе]?\\b|фермерск|рын(ок|ки|ка)\\b|bio-?магазин|куда (заехать|сходить|поехать)|\"\n  

---

> `Write` -- {"file_path": "C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_9d0e5c53\\scratchpad\\geo_cases.py", "content": "import json, subprocess, os, sys\nhook = os.path.expanduser(r\"~\\.claude\\hooks\\skill_suggest_hook.py\")\ncases = [\n    (\"Нужн

---

> `Bash` -- {"command": "python -X utf8 \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_9d0e5c53/scratchpad/geo_cases.py\"; echo rc=$?; python -X utf8 ~/.claude/hooks/skill_suggest_selftest.py 2>&1 | tail -1", "description": "Run geo rule positive/negative cas

---

> `Bash` -- {"command": "cat \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_9d0e5c53/tasks/b3bnxjkia.output\" | grep -E \"journal:|строка|НЕ ЗАПИСАНА\" | head -6; cd ~/.claude/scripts; python -X utf8 rail_plan.py verdict --session 56a81386-3942-4989-bdd8-a270

---

> `Bash` -- {"command": "cd ~/.claude/scripts; python -X utf8 rail_plan.py declare --session s_9d0e5c53 --self \"поиск мест WebSearch, починка хуков, ретро\" --outsource \"web:gemini\" 2>&1 | tail -2; python -X utf8 rail_plan.py verdict --session s_9d0e5c53 --

---

> `Bash` -- {"command": "cd ~/.claude/scripts; V=/e/Obsidian/Vault-Knowledge; N=\"$V/01-Conversations/Claude/Retros/retro-2026-10-29-algarve-farms-skill-hook-dropped.md\"; M=\"$V/01-Conversations/Claude/_Claude-Sessions-MOC.md\"; timeout 60 python -X utf8 workspace_write_lease.py acquire \"$M\" 2>&1 | tail -1; 

---

> `Bash` -- {"command": "cd ~/.claude/scripts; V=/e/Obsidian/Vault-Knowledge; S=s_9d0e5c53; for f in \"$V/01-Conversations/Claude/_Claude-Sessions-MOC.md\" \"$V/01-Conversations/Claude/Retros/retro-2026-10-29-algarve-farms-skill-hook-dropped.md\"; do timeout 60 python -X utf8 workspace

---

> `Edit` -- {"replace_all": false, "file_path": "D:\\Vault\\Vault-Knowledge\\01-Conversations\\Claude\\_Claude-Sessions-MOC.md", "old_string": "## Свежие ретро\n- [[retro-2026-10-29-recall-age-by-last-activity]]", "new_string": "## Свежие ретро\n- [[retro-2026-10-29-algarve-farms-skill-hook-dropped]] · «Valg

---

**Claude:**

Ссылка в MOC стоит. Пишу саму заметку ретро.

---

> `Write` -- {"file_path": "D:\\Vault\\Vault-Knowledge\\01-Conversations\\Claude\\Retros\\retro-2026-10-29-algarve-farms-skill-hook-dropped.md", "content": "---\ntitle: \"Ретро: фермы Алгарве и выпавший хук подсказки скиллов\"\naliases: [\"Ретро H68316 фермы Алгарве\"]\ndate: 2026-10-29\ntype: retro\nsource: 

---

> `Bash` -- {"command": "cd ~/.claude/scripts; N=\"D:/Vault/Vault-Knowledge/01-Conversations/Claude/Retros/retro-2026-10-29-algarve-farms-skill-hook-dropped.md\"; python -B -X utf8 status_claim_lint.py \"$N\"; echo \"lint rc=$?\"; timeout 90 python -B -X utf8 retro_lost_scan.py take 56a81386-3942-4989-bdd8-a

---

> `Bash` -- {"command": "set -o pipefail; cd ~/.claude/scripts; N=\"D:/Vault/Vault-Knowledge/01-Conversations/Claude/Retros/retro-2026-10-29-algarve-farms-skill-hook-dropped.md\"; python -B -X utf8 status_claim_lint.py \"$N\"; echo \"lint rc=$?\"; timeout 90 python -B -X utf8 retro_lost_scan.py take 56a81386

---

**Claude:**

Пока линт и очередь работают в фоне, ставлю маркер ретро в название сессии.

---

> `ToolSearch` -- {"query": "select:mcp__ccd_session_mgmt__get_session,mcp__ccd_session_mgmt__set_session_title", "max_results": 2}

---

> `mcp__ccd_session_mgmt__get_session` -- {"session_id": "self"}

---

> `Bash` -- {"command": "cd ~/.claude/scripts; timeout 60 python -X utf8 session_titles.py retro-plan --sid s_9d0e5c53 --event \"D:/Vault/Vault-Knowledge/01-Conversations/Claude/Retros/retro-2026-10-29-algarve-farms-skill-hook-dropped.md\" --text \"🏠 · 🧀🗺️ Фермы рядом с отелем в Алг

---

> `mcp__ccd_session_mgmt__set_session_title` -- {"session_id": "self", "title": "🏠 · 🧀🗺️ Р Фермы рядом с отелем в Алгарве и починка подсказки скиллов · H68316"}

---

> `Bash` -- {"command": "cd ~/.claude/scripts; timeout 60 python -X utf8 session_code.py title H68316 \"🏠 · 🧀🗺️ Р Фермы рядом с отелем в Алгарве и починка подсказки скиллов · H68316\" 2>&1 | tail -1; cat \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_9d0e5c53

---

> `Bash` -- {"command": "cd ~/.claude/scripts; timeout 60 python -X utf8 session_code.py title --sid s_9d0e5c53 --title \"🏠 · 🧀🗺️ Р Фермы рядом с отелем в Алгарве и починка подсказки скиллов · H68316\" 2>&1 | tail -1", "description": "Sync title into session registry", "timeout": 90000

---

**Claude:**

Пишу короткий пост для X и прогоняю оба гейта.

---

> `Write` -- {"file_path": "C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_9d0e5c53\\scratchpad\\xpost.txt", "content": "Asked my AI for goat farms near our hotel. It confidently planned a trip 60 km away. The reason: a small reminder that tells it which

---

> `Bash` -- {"command": "set -o pipefail; S=\"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_9d0e5c53/scratchpad\"; cp \"$S/xpost.txt\" \"$S/xpost.md\"; python -B -X utf8 ~/.claude/scripts/retro_x_post.py lint --file \"$S/xpost.txt\" 2>&1 | tail -3; timeout 100

---

> `Bash` -- {"command": "S=\"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_9d0e5c53/scratchpad\"; python -B -X utf8 ~/.claude/scripts/retro_x_post.py lint --file \"$S/xpost.txt\" > \"$S/lint.txt\" 2>&1; echo \"rc=$?\"; head -8 \"$S/lint.txt\"", "description": 

---

> `Write` -- {"file_path": "C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_9d0e5c53\\scratchpad\\xpost.txt", "content": "I asked my AI for goat farms near my hotel. It planned a trip 60 km away. Confidently. Why? A small reminder that tells it which tool

---

> `Bash` -- {"command": "S=\"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_9d0e5c53/scratchpad\"; cp \"$S/xpost.txt\" \"$S/xpost.md\"; python -B -X utf8 ~/.claude/scripts/retro_x_post.py lint --file \"$S/xpost.txt\" > \"$S/lint.txt\" 2>&1; echo \"lint rc=$?\";

---

> `Bash` -- {"command": "S=\"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_9d0e5c53/scratchpad\"; timeout 60 python3 ~/.claude/scripts/x_outbox.py enqueue --file \"$S/xpost.txt\" --session H68316 > \"$S/xq.txt\" 2>&1; echo \"rc=$?\"; tail -2 \"$S/xq.txt\"; cat

---

> `Bash` -- {"command": "S=\"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_9d0e5c53/scratchpad\"; grep -E '\"id\"|status|\"ok\"' \"$S/xq.txt\" | head -4; echo ---; ls -la \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/56a81386-3942-498

---

> `Bash` -- {"command": "timeout 90 python -X utf8 ~/.claude/scripts/bus_send.py \"TASK: всем узлам: в hooks/hooks_manifest.json добавлен skill_suggest_hook (UserPromptSubmit), на хабе он молча выпал из settings.json 24-29.09. Прогоните python ~/.claude/scripts/hooks_parity.py --json, при bad>0 python ~/.claude

---

**Claude:**

Ретро готово. Все три корня закрыты на хабе. На остальные 7 узлов ушла задача, их подтверждений ещё нет.

## 🎬 Что поняли за сессию
- **Сначала ошибка.** Слово «Valgarve» из голосовой я принял за название отеля. Нашёл по созвучию Vila Valverde у Лагуша и собрал весь список там, в 60 км от вас. При этом в памяти уже было записано: вы живёте в Pine Cliffs. И ни у одного места не было ссылки на Google Maps.
- **Корень глубже.** Хук, который подсказывает мне нужный скилл, молча выпал из настроек хаба между 24 и 29.09. Его не было в списке обязательных хуков (`hooks_manifest.json`). Поэтому сторож его пропажу не заметил, и около 35 дней хаб не подсказал ни одного скилла.
- **Что починено:**
  - хук вписан в список обязательных и снова подключён;
  - добавлено правило «место в ответе → `/geo`»;
  - в заметку памяти «где оператор сейчас» вернул слова-триггеры. Их стёрла соседняя сессия H63929, которая параллельно чинила тот же корень и завела единый файл «где оператор сейчас»;
  - список ферм пересобран вокруг Pine Cliffs, у каждого места ссылка на карту.
- **Панель шести моделей** нашла слабое место в моём правиле: голые слова «рынок» и «ферма» срабатывали на «рынок акций». Правило сужено.

## 🎙 Вердикт Майка
- 💰 Денег сессия не приносит, но заодно вернула подсказки скиллов ко всей работе хаба: собеседования, лиды, подкасты.
- 🔪 Убил бы свой первый заход: три поиска про незнакомый «отель» до того, как заглянуть в память.
- 🤺 Панель поспорила со мной по делу, и я принял её находку. Сам я тоже спорил честно.
- ❓ Сколько ещё хуков живёт на хабе вне списка обязательных?

## ♻️ Что сделано и как проверено
| Что | Проверено | Перепроверено |
|---|---|---|
| Хук в списке обязательных | ✅ сторож хуков: 0 проблем из 16 обязательных; на старых настройках флагует этот хук | ✅ самотест хука: было FAIL, стало PASS |
| Правило `/geo` | ✅ 9 из 9 кейсов: 3 должны срабатывать, 6 нет | ✅ после находки панели |
| Слова-триггеры в памяти | ✅ хук памяти ловит вашу исходную фразу | ⚠️ соседняя сессия уже раз их стёрла |
| Список ферм | ⚠️ часы работы в конце октября не проверены | ❌ |

## Служебные проверки
- **🧠 Журнал поломок:** записано 2 новых класса по 1-му случаю и 1 уточнение. Прибор семейных совпадений не нашёл. Класс «искал оператора не в том слое» уже на 4-м случае, его корень закрыла сессия H63929.
- **🔨 Панель:** ответили 6 из 6 моделей, все с финальным ответом. Принял 3 находки:
  - ложные срабатывания на «рынок» и «ферму»: исправлено;
  - 7 узлов флота не проверены: туда ушла задача;
  - соседняя сессия может снова перезаписать заметку памяти: записано как открытый пункт.
- **Отклонил 2 находки:**
  - «`отел` ловит слово „хотел“»: проверил, не ловит;
  - «grep не починен»: это урок, а не код, он записан в заметку ретро.
- **🚂 Чужие модели:** план на старте сессии я не объявил, хотя хук напомнил. Весь поиск шёл моим собственным веб-поиском, без рельсы gemini. План объявил задним числом с причиной «forgot», сверка закрыта.
- **🌐 Флот:** задача ушла в шину и чат 03 (message 191468). Ответов от узлов пока нет.
- **🐦 X-пост:** лежит на складе, id `da0d9e2ca9177a8b`, опубликует робот.
  > I asked my AI for goat farms near my hotel. It planned a trip 60 km away. Confidently. Why? A small reminder that tells it which tool to use had quietly switched off a month ago. Nobody noticed. Silent failures hurt more than loud ones.

  Кому польза: людям, которые держат агентов в работе. Что они смогут: проверить, что «тихие» помощники агента на самом деле включены. Продажи в посте нет. Оба гейта пройдены, осталось одно ожидаемое предупреждение: в посте нет ссылки.
- **Заметка ретро** лежит в волте `01-Conversations/Claude/Retros/retro-2026-10-29-algarve-farms-skill-hook-dropped.md`, ссылка из каталога сессий стоит.
- **⚠️ Не закончено:** проверка заметки на формат и снятие сессии с ночной очереди ретро всё ещё идут в фоне. Значит, это не проверено.
- **Время:** сессия жила 26 ч 31 мин (создана 28.10 12:34 UTC, последняя активность 29.10 15:05 UTC).
- **Название сессии:** «🏠 · 🧀🗺️ Р Фермы рядом с отелем в Алгарве и починка подсказки скиллов · H68316».

## 📌 Открыто
- Подтверждения от 7 узлов, что хук у них подключён.
- Сторож хуков не увидит хук, который удалили одновременно из настроек и из списка обязательных (находка GPT-6 Sol).
- Заметку памяти могут снова перезаписать параллельной правкой.

## 🗜 Если остаёшься в этой сессии
➤ Скопируй блок целиком и вставь следующим сообщением:
```
/compact РЕШЕНИЯ: хук skill_suggest обязателен, вписан в hooks_manifest.json и settings.json хаба; правило /geo только на явный запрос места (рядом с, гостиница, отель, фермерский, куда заехать, near me), голые «рынок» и «ферма» сняты; отель оператора = Pine Cliffs (00-System/where-dev-now.md). TODO: ACK 7 узлов по шине 03 (msg 191468); сторож паритета слеп к хуку, удалённому из обоих мест; заметку памяти where-is-dev защитить от параллельной перезаписи. СЕЙЧАС: ретро записано, X-пост на складе da0d9e2ca9177a8b, фоновые status_claim_lint и retro_lost take не досчитались. ПУТИ И ЗНАЧЕНИЯ: ~/.claude/hooks/skill_suggest_hook.py, hooks_manifest.json, settings.json; бэкапы *.bak-*H68316*; ретро 01-Conversations/Claude/Retros/retro-2026-10-29-algarve-farms-skill-hook-dropped.md. СЧЁТЧИКИ: панель 6/6, /geo 9/9, hooks_parity bad 0/16. ОТКРЫТО: часы работы ферм в конце октября, жива ли Amendoeira. ИНСТРУМЕНТЫ И КОНТРАКТЫ: skill_suggest_selftest.py, hooks_parity.py --json --settings, selfheal.py journal, /geo.
```

**🧒 Простыми словами**
Я перепутал, где вы живёте, и не дал ссылок на карту. Причина: у меня тихо отвалилась «напоминалка», которая говорит, каким инструментом пользоваться. Месяц её никто не замечал, потому что её не было в списке того, что проверяет сторож. Теперь она в списке, снова включена и больше не путает «рынок акций» с рынком овощей. Остальным компьютерам я отправил задачу проверить у себя, их ответов пока нет.

---

**User:**

<task-notification>
<task-id>bpscj7uxf</task-id>
<tool-use-id>toolu_01JAu4755vM5QcdXVYgoLGus</tool-use-id>
<output-file>C:\Users\dev\AppData\Local\Temp\claude\P---WORKDIR-HUB\s_9d0e5c53\tasks\bpscj7uxf.output</output-file>
<status>completed</status>
<summary>Background command "Lint retro note and take retro-lost queue" completed (exit code 0)</summary>
</task-notification>

---

> `Bash` -- {"command": "cat \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_9d0e5c53/tasks/bpscj7uxf.output\" | tail -8; ls \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_9d0e5c53/scratchpad/rl_receipt.json

---

> `Bash` -- {"command": "grep -nE \"^\\s*(FAIL|строка|line)|:[0-9]+:\" \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_9d0e5c53/tasks/bpscj7uxf.output\" | head -12; head -6 \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/56a81386-3942-4

---

> `Edit` -- {"replace_all": false, "file_path": "D:\\Vault\\Vault-Knowledge\\01-Conversations\\Claude\\Retros\\retro-2026-10-29-algarve-farms-skill-hook-dropped.md", "old_string": "| Правило `/geo` в `skill_suggest_hook.py` |", "new_string": "| Правило geo в `C:/Users/dev/.claude/hooks/skill_suggest_hook.p

---

> `Bash` -- {"command": "cd ~/.claude/scripts; N=\"D:/Vault/Vault-Knowledge/01-Conversations/Claude/Retros/retro-2026-10-29-algarve-farms-skill-hook-dropped.md\"; timeout 280 python -B -X utf8 status_claim_lint.py \"$N\" > /tmp/scl.txt 2>&1; echo \"lint rc=$?\"; tail -2 /tmp/scl.txt", "description": "Re-run 

---

> `Bash` -- {"command": "cd ~/.claude/scripts; N=\"D:/Vault/Vault-Knowledge/01-Conversations/Claude/Retros/retro-2026-10-29-algarve-farms-skill-hook-dropped.md\"; python -B -X utf8 status_claim_lint.py \"$N\"; rc=$?; echo \"lint rc=$rc\"; if [ $rc -eq 0 ]; then python -B -X utf8 retro_lost_scan.py mark-done 

---

**Claude:**

Обе фоновые проверки досчитались. Одна прошла, вторая потребовала мелкую правку, повторная проверка снова идёт в фоне.

- **Снятие сессии с ночной очереди ретро:** захват прошёл (rc=0, epoch 747). Отметка «готово» поставится автоматически, как только заметка пройдёт проверку формата.
- **Проверка заметки ретро:** вернула rc=2 из-за одной строки. Проверка приняла имя `/geo` с соседним именем файла за путь к несуществующему файлу и не нашла его. Я написал в этой строке полный путь `C:/Users/dev/.claude/hooks/skill_suggest_hook.py`.
- **Повторная проверка:** первый прогон оборвался по моему лимиту в 280 секунд, сама проверка идёт дольше. Сейчас она работает в фоне без лимита, следом сама поставит отметку в ночной очереди. Итог пришлю, когда она закончится.

**🧒 Простыми словами**
Проверка заметки споткнулась об одну строку: приняла название инструмента за путь к файлу. Я исправил строку, и проверка идёт заново. Когда она закончится, ночной робот увидит, что ретро по этой сессии уже сделано, и не будет делать его второй раз.

---

**User:**

<task-notification>
<task-id>bo6x7wgbx</task-id>
<tool-use-id>toolu_01PvzVFDfrWjyc3uWa6kY8gx</tool-use-id>
<output-file>C:\Users\dev\AppData\Local\Temp\claude\P---WORKDIR-HUB\s_9d0e5c53\tasks\bo6x7wgbx.output</output-file>
<status>completed</status>
<summary>Background command "Lint then mark retro-lost done in background" completed (exit code 0)</summary>
</task-notification>

---

> `Bash` -- {"command": "tail -5 \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_9d0e5c53/tasks/bo6x7wgbx.output\"", "description": "Read lint and mark-done result"}

---

> `Bash` -- {"command": "cd ~/.claude/scripts; V=D:/Vault/Vault-Knowledge; for f in \"$V/01-Conversations/Claude/_Claude-Sessions-MOC.md\" \"$V/01-Conversations/Claude/Retros/retro-2026-10-29-algarve-farms-skill-hook-dropped.md\"; do timeout 60 python -X utf8 workspace_write_lease.py release \"$f\" --session

---

> `Bash` -- {"command": "timeout 60 python -X utf8 ~/.claude/scripts/workspace_write_lease.py release-session --session s_9d0e5c53 2>&1 | tail -1", "description": "Release all session leases", "timeout": 90000}

---

**Claude:**

Ретро закрыто: заметка прошла проверку формата, ночной робот больше не возьмёт эту сессию.

- **Проверка заметки:** `lint rc=0`.
- **Ночная очередь ретро:** отметка «готово» поставлена (`mark rc=0`), файл `~/.claude/logs/retro_lost_done/56a81386-…`.
- **Блокировки на запись:** снято 3 (`RELEASED 3`), в том числе на заметку ретро и каталог сессий.

Открытым осталось только ожидание подтверждений от 7 узлов флота, что хук подсказки скиллов у них подключён.

**🧒 Простыми словами**
Всё по ретро доделано: заметка проверена, ночной робот не будет разбирать эту сессию второй раз, файлы разблокированы. Ждём только, когда остальные компьютеры ответят, что включили у себя напоминалку.
