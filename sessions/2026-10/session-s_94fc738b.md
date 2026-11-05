---
session: s_94fc738b
date: 2026-10-07
words: 1063
turns: 2
tools: "Bash, Read, ToolSearch, WebFetch, WebSearch"
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-10-07 · Использовать нам нужно для дешевых моделей. Исследовать возможность эту

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_94fc738b` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

Использовать нам нужно для дешевых моделей. Исследовать возможность эту

E:\!CLAUDE-HUBPC-June26\downloads\photo_2026-10-07_21-33-33.jpg

---

> `Read` -- {"file_path": "E:\\!CLAUDE-HUBPC-June26\\downloads\\photo_2026-10-07_21-33-33.jpg"}

---

> `Bash` -- {"command": "cd ~/.claude/scripts 2>/dev/null && python rail_plan.py declare --self \"оркестрация, живая проба дверей opencode.ai, суждение о пригодности, доклад оператору\" --outsource \"web:gemini\" 2>&1 | tail -5", "description": "Declare rail plan"}

---

> `ToolSearch` -- {"query": "select:WebFetch,WebSearch", "max_results": 2}

---

> `WebFetch` -- {"url": "https://opencode.ai/docs/zen/", "prompt": "What is opencode zen? List all models offered, exact prices per million input/output tokens, how to get an API key, whether it is OpenAI-compatible, base URL, and any limits."}

---

> `WebFetch` -- {"url": "https://opencode.ai/", "prompt": "What is the \"Go\" plan? Price, limits, which open-source models included, what \"use with any agent\" means. List all plans and prices."}

---

> `WebFetch` -- {"url": "https://opencode.ai/go", "prompt": "Full details of the Go plan: price per month, usage limits, which models included, can it be used with other agents/CLIs (API key? OpenAI-compatible endpoint?), rate limits, fair use."}

---

> `WebSearch` -- {"query": "opencode zen api key use with any agent ANTHROPIC_BASE_URL claude code"}

---

> `Bash` -- {"command": "ls ~/.claude/secrets/ 2>/dev/null | head -40; echo ---; grep -ril \"opencode\" ~/.claude/secrets/ ~/.claude/*.json 2>/dev/null | head; echo ---; ls \"C:/Users/dev/.config/opencode\" \"C:/Users/dev/.local/share/opencode\" 2>/dev/null | head -20; echo ---; which opencode 2>/dev/null; 

---

> `Bash` -- {"command": "cd ~; python -c \"\nimport json,os\np=os.path.expanduser('~/.local/share/opencode/auth.json')\nd=json.load(open(p))\nfor k,v in d.items():\n    t=v if isinstance(v,str) else json.dumps(v)\n    print(k, '->', (t[:40]+'...') if len(t)>40 else t)\n\" 2>&1; echo '--- jsonc ---'; cat \"C:/Us

---

> `Bash` -- {"command": "cd ~/.claude/scripts && grep -rn \"jev\" --include=*.py -i . 2>/dev/null | grep -iv \"test\" | head -20", "description": "Find jev rail wiring"}

---

> `Bash` -- {"command": "curl -s -m 20 https://opencode.ai/zen/v1/models | head -c 1500; echo; echo \"=== HTTP ===\"; curl -s -o /dev/null -w \"%{http_code}\\n\" -m 20 https://opencode.ai/zen/v1/models; echo \"=== messages probe (no key) ===\"; curl -s -m 20 -X POST https://opencode.ai/zen/v1/messages -H \"cont

---

> `Bash` -- {"command": "curl -s -m 20 https://opencode.ai/zen/v1/models | python -c \"\nimport sys,json\nd=json.load(sys.stdin)['data']\nids=[m['id'] for m in d]\nprint('всего моделей:',len(ids))\nimport textwrap\nprint(textwrap.fill(', '.join(ids),110))\n\"", "description": "List all zen models"}

---

> `WebFetch` -- {"url": "https://opencode.ai/docs/zen/", "prompt": "Does the page say anything about data retention, privacy, zero data retention, or whether prompts are logged or used for training? Especially for the free models. Quote exactly."}

---

> `Bash` -- {"command": "cd ~/.claude; wc -l jev_usage.jsonl 2>/dev/null; python - <<'EOF'\nimport json,os,collections,datetime\np=os.path.expanduser('~/.claude/jev_usage.jsonl')\nif os.path.exists(p):\n    rows=[json.loads(l) for l in open(p,encoding='utf-8') if l.strip()]\n    print('jev вызовов всего:',len(r

---

> `Bash` -- {"command": "python - <<'EOF'\nimport json,os,collections\nrows=[json.loads(l) for l in open(os.path.expanduser('~/.claude/jev_usage.jsonl'),encoding='utf-8') if l.strip()]\ntot=sum(float(r.get('cost_usd') or 0) for r in rows)\nok=sum(1 for r in rows if r.get('outcome')=='ok')\nprint(f'всего вызовов

---

> `Bash` -- {"command": "ls ~/.claude/ | grep -i -E \"orouter|openrouter|llm_ask|ledger\" | head -20; echo ---; ls ~/.claude/*.jsonl 2>/dev/null | head -30", "description": "Find llm usage ledgers"}

---

> `Bash` -- {"command": "cd ~/.claude/scripts 2>/dev/null; python - <<'EOF'\nimport os,glob,json,collections\n# find llm_ask ledger\ncands=glob.glob(os.path.expanduser('~/.claude/**/*ledger*'),recursive=True)+glob.glob(os.path.expanduser('~/.claude/llm*'))\nprint([c for c in cands][:20])\nEOF\ngrep -n \"LEDGER\

---

> `Bash` -- {"command": "cat > \"C:/Users/dev/.claude/projects/P---WORKDIR-HUB/memory/opencode-zen-cheap-rail.md\" <<'EOF'\n---\nname: opencode-zen-cheap-rail\ndescription: opencode.ai Zen/Go — одна дверь к 87 моделям, Anthropic- и OpenAI-совместимая; кандидат в дешёвую грунт-рельсу, решение за А

---

**Claude:**

**21:50 (Лиссабон) · сессия H26684**

🚂 Рельсы: сам как Claude — живая проба дверей, суждение, доклад. Наружу — `web>gemini` (поиск по интеграциям).

## Что на скриншоте

**opencode.ai** — гейтвей «одна дверь ко всем моделям» от команды opencode (TUI-агент). Две части: **Zen** (поштучно) и **Go** (подписка $10/мес).

## Живая проба (не из доков, прямо сейчас с хаба)

```bash
curl -s https://opencode.ai/zen/v1/models
```
→ **200 без ключа, 87 моделей**: claude-opus-5-5, claude-fable-5, gpt-6-astra, gemini-3.8-flash, grok-4.7, deepseek-v4.1-flash, glm-5.3, kimi-k3, minimax-m3, qwen3.8-max, mistral-large-4, jev-1.13 + 13 бесплатных.
`POST /zen/v1/messages` без ключа → ошибка. Ключ обязателен.

## Почему это интересно именно нам

**Две двери одним ключом**: `/zen/v1/messages` — формат Anthropic. Значит `ANTHROPIC_BASE_URL=https://opencode.ai/zen` + `ANTHROPIC_AUTH_TOKEN=<ключ>` — и **Claude Code ходит в чужую дешёвую модель без единой правки кода**. Это и есть «use with any agent». Наши грунт-рутины (чтение роботом, триаж, слоп-гейт, дайджесты, счётчики) перестают жевать бак Claude Max — а именно бак упирается в «usage limit reached», а не деньги.

**Цена**: Go $10/мес ≈ 30 дешёвых моделей, ~26 000 запросов / 5 часов на deepseek-v4.1-flash (их собственная оценка «$60–120/мес по токенам»). Go Plus $40.

## Два факта против, которые я обязан назвать

⚠️ **Моя первая красивая мысль оказалась враньём.** Я решил «у них jev бесплатный, а мы за него платим OpenRouter'у». Замер `jev_usage.jsonl`: **903 вызова за 30 дней = $0.0465**. Четыре с половиной цента. Экономить там нечего, и ставить это в обоснование было бы подгонкой.

⚠️ **Бесплатные модели учатся на наших промптах** — их же страница приватности: Big Pickle, Exo, Fledge, MiMo, Ling, Nemotron, Muse Spark Contributor. Платные — zero-retention (но OpenAI/Anthropic держат 30 дней). Вывод: бесплатный тир — только публичный вход, волт/CRM/секреты туда ⛔.

## Мой вердикт как кофаундера

**Брать Go за $10 — да, но как ТЕНЬ, а не как замену.** $10 против $736/мес наших текущих подписок — это цена замера, а не инвестиция. Что проверяем за месяц: уехала ли реально грунт-работа с бака Max, и не просел ли `/tt` на дешёвой модели. Не уехала за 30 дней — отменяем, потеряли десятку.

**Что НЕ отдаём туда ни при каком раскладе** (§6.2): оркестрацию, голос оператора, суждение, Alpha/Decision Memo. Только грунт.

🎙 Майк: тут соблазн — «87 моделей одной дверью!» — а по факту мы покупаем не модели, а **обход бутылочного горлышка Max**. Единственный вопрос, на который стоит отвечать цифрой: сколько процентов наших прогонов сегодня тормозят об «usage limit», а не об качество? Если меньше 5% — десятку тоже жалко.

## Руки оператора (10 минут, я не могу сам — создание аккаунта и платёжка)

1. https://opencode.ai/auth → войти (почта или GitHub)
2. https://opencode.ai/go → Go, $10/мес
3. Скопировать ключ → прислать мне сюда или положить в `~/.claude/secrets/opencode_zen.env`

Дальше я сам: заведу рельсу в `llm_routing.json`, поставлю тень с датой урожая и прогоню замер «ушёл ли грунт с бака».

🧒 **Простыми словами:** нашли магазин, где за 10 долларов в месяц дают очень много дешёвых «мозгов» через одну розетку — и наша программа втыкается в неё без переделки. Полезно, потому что наш дорогой мозг (Claude) часто упирается в «на сегодня хватит», а скучную работу можно отдать дешёвому. Но: бесплатные мозги там подсматривают, что мы им пишем — им даём только то, что и так публично. И я проверил свою же красивую идею «сэкономим на Jev» — вранье, мы там тратим 4 цента в месяц. Чтобы купить, нужны твои руки: заплатить и дать мне ключ.

Sources: [opencode Zen docs](https://opencode.ai/docs/zen/), [opencode Go](https://opencode.ai/go), [Claude Code через Zen](https://www.shravanbhati.com/blog/run-opencode-zen-and-go-models-with-claude-code-cli)
