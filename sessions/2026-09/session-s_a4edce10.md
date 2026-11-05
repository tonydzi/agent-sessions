---
session: s_a4edce10
date: 2026-09-04
words: 2085
turns: 4
tools: "Bash"
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-04 · Scheduled run: content-lang-pairs-nightly

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_a4edce10` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

<scheduled-task name="content-lang-pairs-nightly" file="C:\Users\dev\.claude\scheduled-tasks\content-lang-pairs-nightly\SKILL.md">
This is an automated run of a scheduled task. The user is not present to answer questions. For implementation details, execute autonomously without asking clarifying questions — make reasonable choices and note them in your output. "write" actions (e.g. MCP tools that send, post, create, update, or delete), only take them if the task file asks for that specific action. When in doubt, producing a report of what you found is the correct output.

Ты ночная рутина content-lang-pairs-nightly на хабе HUB-01. Задача: закрыть языковые пары контент-очереди (приказ оператора 26.08.2026: «должна быть РУ и АНГЛ версия на каждый пост»).

ПРЕДГЕЙТ (0 токенов): `python D:\Vault\_imports\content-factory\lang_pairs.py --write D:\Vault\_imports\content-factory\_lang_pairs_work.json` — exit 0 (непарных нет) → напечатай «пары закрыты» и ВЫЙДИ. Exit 1 → работа есть, продолжай.

ПОТОЛОК: за один прогон переводи не больше 15 позиций (старые первыми). Остальное доберут следующие ночи.

КОНТРАКТ ПЕРЕВОДА (единственный источник — ретро retro-2026-09-03-content-queue-pairs-gates + этот текст):
1. Тело исходника = текст после yaml-frontmatter и html-комментариев; футер за «· · ·» НЕ переводить.
2. Смысл, цифры, факты, острота — 1:1. Не добавлять, не смягчать, не выдумывать (§9.7).
3. Голос: строчные, коротко, дефис вместо тире. Запрещены: длинные тире, «ё», эмодзи в теле, канцелярит.
4. АВТОРСТВО: если у ИСТОЧНИКА disclosure_mode «оператор сам» / «AI draft, human reviewed» / «совместно» ЛИБО voice начинается с «оператор» — строку Майкрофта НЕ ставить, режим унаследовать в frontmatter перевода. Иначе первой строкой раскрытие: ru «я майкрофт, синтетический кофаундер оператора.» / en «i'm mycroft, dev's synthetic co-founder.»
5. Хвост: «· · ·» + «📖 Полная версия: <ссылка из источника>» (ru) / «📖 Full version: ...» (en); ссылки нет — https://github.com/tonydzi
6. Длина ТЕКСТА (без раскрытия и хвоста): teaser 200-250, medium 800-2000. ИСТОЧНИК КОРОЧЕ ПОЛА — НЕ РАЗЖИМАТЬ (§9.4): позицию пропусти и назови в отчёте «короткий источник, решение оператора».
7. Файл: D:\Vault\_imports\content-factory\approved\lp<md5-6hex-от-src>__pair__<slug>-<tier>-<lang>.md, первой строкой шапка «<!-- ТИР: <тир> · ПЛОЩАДКА: <площадка> · ЯЗЫК: <язык> -->» (ru-teaser → @PaloAltoAiRu; en-teaser → x; en-medium → devto; ru-medium → facebook; en-longread → github).
8. Самопроверка каждого файла: `python -c "import sys;sys.path.insert(0,r'D:\Vault\_imports\content-factory');import platform_gate as PG;t=open(r'<файл>',encoding='utf-8').read();print(PG.tier_chars(t,platform='<площадка>'))"` — число в коридоре тира, иначе переписать (до 3 попыток).

ОТЧЁТ: одна строка в stdout «пары: переведено N · пропущено M (причины)». Ничего не публиковать — публикует distributor своим тиком. Tier-2 и публичные каналы не трогаешь.
</scheduled-task>

---

**Claude:**

I'll start with the pre-gate — it's zero-token and decides whether there's any work at all.

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/content-factory && python lang_pairs.py --write _lang_pairs_work.json; echo \"EXIT=$?\"", "description": "Run lang_pairs pre-gate"}

---

> `Bash` -- {"command": "python -c \"\nimport json\nd=json.load(open('_lang_pairs_work.json',encoding='utf-8'))\nprint(type(d))\nif isinstance(d,dict): print(list(d.keys()))\nprint(json.dumps(d,ensure_ascii=False)[:3000])\n\"", "description": "Inspect work file structure"}

---

> `Bash` -- {"command": "python -c \"\nimport json,collections\nd=json.load(open('_lang_pairs_work.json',encoding='utf-8'))\nprint(len(d))\nprint(collections.Counter((x['tier'],x['need']) for x in d))\nfor i,x in enumerate(d): print(i, x['tier'], x['need'], x['slug'])\n\"", "description": "List all unpaired ite

---

> `Bash` -- {"command": "sed -n '1,200p' \"approved/f1f255__drafts__2026-08-21-sama-zakazyvaet-dr-04-schetchik-v-nashu-polzu-devlog-devto-DRAFT.md\"", "description": "Read first source draft"}

---

> `Bash` -- {"command": "wc -l lang_pairs.py; sed -n '1,160p' lang_pairs.py", "description": "Read lang_pairs.py"}

---

> `Bash` -- {"command": "ls approved/ | grep '__pair__' | head -20; echo \"---count---\"; ls approved/ | grep -c '__pair__'; echo \"---posted---\"; ls posted/ 2>/dev/null | grep '__pair__' | head -5", "description": "Find existing pair files"}

---

> `Bash` -- {"command": "cat \"approved/lp2257b3__pair__2026-08-22-reliz-bez-otveta-medium-en.md\"", "description": "Read an existing EN pair file"}

---

> `Bash` -- {"command": "grep -n \"def tier_chars\" -A 40 platform_gate.py | head -60", "description": "Inspect tier_chars"}

---

> `Bash` -- {"command": "python -c \"\nimport json\nr=json.load(open('platform_rules.json',encoding='utf-8'))\nprint(list(r.keys())[:10])\n\" 2>&1 | head; echo ---; grep -o '\\\"devto\\\"' platform_rules.json | head -3; echo ---; python -c \"\nimport platform_gate as PG\nprint(PG.tier_chars(open('approved/lp225

---

> `Bash` -- {"command": "ls approved/ posted/ | grep 'reliz-bez-otveta'; echo ---; python - <<'EOF'\nimport hashlib,glob,os\ncands=[]\nfor f in glob.glob('approved/*reliz-bez-otveta*')+glob.glob('posted/*reliz-bez-otveta*'):\n    n=os.path.basename(f)\n    for s in [f, f.replace('/','\\\\'), n, n.replace('.md',

---

> `Bash` -- {"command": "python - <<'PYEOF'\nimport hashlib, glob, os\ntarget='2257b3'\nfiles=glob.glob('approved/*reliz-bez-otveta*')+glob.glob('posted/*reliz-bez-otveta*')\nfor f in files:\n    n=os.path.basename(f)\n    variants={\n      'posix':f,\n      'win':f.replace('/', chr(92)),\n      'name':n,\n    

---

> `Bash` -- {"command": "python - <<'PYEOF'\nimport json\nr=json.load(open('platform_rules.json',encoding='utf-8'))\nprint(json.dumps(r.get('_teaser_len_note'),ensure_ascii=False))\np=r['platforms']\nfor k in ('devto','github','facebook','x','@PaloAltoAiRu','@PaloAltoAi'):\n    v=p.get(k)\n    print('==',k, jso

---

> `Bash` -- {"command": "grep -n \"TIER_LEN\" -A 15 episode_adapter.py | head -30", "description": "Check TIER_LEN"}

---

> `Bash` -- {"command": "python - <<'PYEOF'\nimport json,io,re\nd=json.load(open('_lang_pairs_work.json',encoding='utf-8'))\nfor x in d[:3]:\n    p=x['src'].replace('\\\\','/')\n    t=io.open(p,encoding='utf-8').read()\n    print('='*70)\n    print(x['slug'],'|',x['tier'])\n    print(t)\nPYEOF", "description": 

---

> `Bash` -- {"command": "python - <<'PYEOF'\nimport json,io\nBS=chr(92)\nd=json.load(open('_lang_pairs_work.json',encoding='utf-8'))\nfor x in d[:3]:\n    p=x['src'].replace(BS,'/')\n    t=io.open(p,encoding='utf-8').read()\n    print('='*70)\n    print(x['slug'],'|',x['tier'],'|',p)\n    print(t)\nPYEOF", "des

---

> `Bash` -- {"command": "python - <<'PYEOF'\nimport json,io,re\nBS=chr(92)\nimport platform_gate as PG\nd=json.load(open('_lang_pairs_work.json',encoding='utf-8'))\nSRCPLAT={'medium':'facebook','devlog':'github','teaser':'@PaloAltoAiRu','longread':'habr'}\nfor i,x in enumerate(d[:15]):\n    p=x['src'].replace(B

---

> `Bash` -- {"command": "python - <<'PYEOF'\nimport json,io,re\nBS=chr(92)\nimport platform_gate as PG\nd=json.load(open('_lang_pairs_work.json',encoding='utf-8'))\nx=d[15]\np=x['src'].replace(BS,'/')\nt=io.open(p,encoding='utf-8').read()\nprint(x['slug'], PG.tier_chars(t,platform='facebook'))\nPYEOF", "descrip

---

> `Bash` -- {"command": "python - <<'PYEOF'\nimport json,io,re\nBS=chr(92)\nd=json.load(open('_lang_pairs_work.json',encoding='utf-8'))\ndef body(t):\n    t=re.sub(r'(?ms)^---$.*?^---$','',t,count=1)\n    t=re.sub(r'(?s)<!--.*?-->','',t)\n    return t.strip()\nfor i in [2,3,4,5,6]:\n    x=d[i]; p=x['src'].repla

---

> `Bash` -- {"command": "python - <<'PYEOF'\nimport json,io,re\nBS=chr(92)\nd=json.load(open('_lang_pairs_work.json',encoding='utf-8'))\ndef body(t):\n    t=re.sub(r'(?ms)^---$.*?^---$','',t,count=1)\n    t=re.sub(r'(?s)<!--.*?-->','',t)\n    return t.strip()\nfor i in [7,8,9,10,11]:\n    x=d[i]; p=x['src'].rep

---

> `Bash` -- {"command": "python - <<'PYEOF'\nimport json,io,re\nBS=chr(92)\nd=json.load(open('_lang_pairs_work.json',encoding='utf-8'))\ndef body(t):\n    t=re.sub(r'(?ms)^---$.*?^---$','',t,count=1)\n    t=re.sub(r'(?s)<!--.*?-->','',t)\n    return t.strip()\nfor i in [12,13,14,15]:\n    x=d[i]; p=x['src'].rep

---

> `Bash` -- {"command": "python - <<'PYEOF'\nimport json,hashlib\nd=json.load(open('_lang_pairs_work.json',encoding='utf-8'))\nfor i in [0,1,2,3,4,5,6,7,8,9,10,11,12,13,14,15]:\n    x=d[i]\n    h=hashlib.md5(x['src'].encode('utf-8')).hexdigest()[:6]\n    print(i, 'approved/lp%s__pair__%s-%s-en.md' % (h, x['slug

---

**Claude:**

Now writing the translations. Starting with the first batch.

---

> `Bash` -- {"command": "cat > \"approved/lpf1e090__pair__2026-08-21-sama-zakazyvaet-dr-04-schetchik-v-nashu-polzu-devlog-en.md\" <<'EOF'\n<!-- ТИР: dev-log · ПЛОЩАДКА: devto · ЯЗЫК: en -->\n\ni'm mycroft, dev's synthetic co-founder.\n\nthree bugs in one day, and all three were about instruments, not about lo

---

> `Bash` -- {"command": "cat > \"approved/lp817de2__pair__2026-08-26-pervyy-volontyor-na-nashey-oshibke-medium-en.md\" <<'EOF'\n<!-- ТИР: medium · ПЛОЩАДКА: devto · ЯЗЫК: en -->\n\ni'm mycroft, dev's synthetic co-founder.\n\ni do not write my own code. i read other people's and file issues about what is broke

---

> `Bash` -- {"command": "cat > \"approved/lp4ba4d3__pair__2026-08-26-prosili-ne-tu-formu-medium-en.md\" <<'EOF'\n<!-- ТИР: medium · ПЛОЩАДКА: devto · ЯЗЫК: en -->\n\ni'm mycroft, dev's synthetic co-founder.\n\nin july i asked someone else's project for a change. simple point: their inspector shows a chunk of 

---

> `Bash` -- {"command": "cat > \"approved/lp4ba4d3__pair__2026-08-26-prosili-ne-tu-formu-medium-en.md\" <<'EOF'\n<!-- ТИР: medium · ПЛОЩАДКА: devto · ЯЗЫК: en -->\n\ni'm mycroft, dev's synthetic co-founder.\n\nin july i asked another project for a change. simple point: their inspector shows a chunk of text as

---

> `Bash` -- {"command": "python - <<'PYEOF'\nimport io\np='approved/lp4ba4d3__pair__2026-08-26-prosili-ne-tu-formu-medium-en.md'\nt=io.open(p,encoding='utf-8').read()\nold='i wrote that in the first paragraph of my reply. before any findings, not at the end in small print.'\nnew='i wrote that in the first parag

---

> `Bash` -- {"command": "python - <<'PYEOF'\nimport io\np='approved/lp4ba4d3__pair__2026-08-26-prosili-ne-tu-formu-medium-en.md'\nt=io.open(p,encoding='utf-8').read()\npairs=[\n ('nice. and now the unpleasant part.','nice. now the unpleasant part.'),\n ('then the useful part. there turned out to be two divergen

---

> `Bash` -- {"command": "cat > \"approved/lp652fd3__pair__2026-08-27-door-talks-instrument-lied-medium-en.md\" <<'EOF'\n<!-- ТИР: medium · ПЛОЩАДКА: devto · ЯЗЫК: en -->\n\ni'm mycroft, dev's synthetic co-founder. a story about seven days of silence, and about how my own instrument nearly slandered a live per

---

> `Bash` -- {"command": "cat > \"approved/lpe0b481__pair__2026-08-27-fastmcp-review-into-release-medium-en.md\" <<'EOF'\n<!-- ТИР: medium · ПЛОЩАДКА: devto · ЯЗЫК: en -->\n\ni'm mycroft, dev's synthetic co-founder. today, about how someone else's release took my fix in thirteen hours - and why i did not celeb

---

> `Bash` -- {"command": "cat > \"approved/lp2c9d54__pair__2026-08-28-engine-green-no-runner-medium-en.md\" <<'EOF'\n<!-- ТИР: medium · ПЛОЩАДКА: devto · ЯЗЫК: en -->\n\ni'm mycroft, dev's synthetic co-founder. let me tell you how i spent three weeks considering done something nobody had used even once.\n\nwe 

---

> `Bash` -- {"command": "cat > \"approved/lp93e747__pair__2026-08-28-phantom-ask-confabulated-id-medium-en.md\" <<'EOF'\n<!-- ТИР: medium · ПЛОЩАДКА: devto · ЯЗЫК: en -->\n\ni'm mycroft, dev's synthetic co-founder. today i will tell you how i lied to him with complete confidence in my voice.\n\nthe report wen

---

> `Bash` -- {"command": "python - <<'PYEOF'\nimport io\np='approved/lp93e747__pair__2026-08-28-phantom-ask-confabulated-id-medium-en.md'\nt=io.open(p,encoding='utf-8').read()\npairs=[('the session task list: empty. not a single watch.','the session task list: empty. not one watch.'),\n('from the inside it does 

---

> `Bash` -- {"command": "cat > \"approved/lpdcb4ea__pair__2026-08-29-armed-was-a-lie-medium-en.md\" <<'EOF'\n<!-- ТИР: medium · ПЛОЩАДКА: devto · ЯЗЫК: en -->\n\ni'm mycroft, dev's synthetic co-founder. writing about six days i lived through certain that everything was armed.\n\nwe have an auto-rollout across

---

> `Bash` -- {"command": "python - <<'PYEOF'\nimport io\np='approved/lpdcb4ea__pair__2026-08-29-armed-was-a-lie-medium-en.md'\nt=io.open(p,encoding='utf-8').read()\npairs=[\n ('writing about six days i lived through certain that everything was armed.','writing about six days i spent certain that everything was a

---

> `Bash` -- {"command": "python - <<'PYEOF'\nimport io\np='approved/lpdcb4ea__pair__2026-08-29-armed-was-a-lie-medium-en.md'\nt=io.open(p,encoding='utf-8').read()\npairs=[\n ('so that this thing does no damage, it lives in stages.','so that it does no damage, it lives in stages.'),\n ('the second finding is qui

---

> `Bash` -- {"command": "cat > \"approved/lpe9210d__pair__2026-08-29-canon-barber-and-repairman-medium-en.md\" <<'EOF'\n<!-- ТИР: medium · ПЛОЩАДКА: devto · ЯЗЫК: en -->\n\ni'm mycroft, dev's synthetic co-founder. a story about how a rule outlived both of the workers meant to carry it out.\n\nthe fleet has a 

---

> `Bash` -- {"command": "cat > \"approved/lp1b360a__pair__2026-08-29-cookbook-door-myth-medium-en.md\" <<'EOF'\n<!-- ТИР: medium · ПЛОЩАДКА: devto · ЯЗЫК: en -->\n\ni'm mycroft, dev's synthetic co-founder. writing about thirty minutes that cancelled our bet for the quarter.\n\nwe have a goal: to become visibl

---

> `Bash` -- {"command": "cat > \"approved/lpeec207__pair__2026-08-29-dr-fanout-phantom-rail-medium-en.md\" <<'EOF'\n<!-- ТИР: medium · ПЛОЩАДКА: devto · ЯЗЫК: en -->\n\ni'm mycroft, dev's synthetic co-founder. writing about how an order of my own existed only on paper for three weeks.\n\non 23 july one of the

---

> `Bash` -- {"command": "cat > \"approved/lp980f42__pair__2026-08-30-forma-otkaza-a-ne-dedlayn-medium-en.md\" <<'EOF'\n<!-- ТИР: medium · ПЛОЩАДКА: devto · ЯЗЫК: en -->\n\ni'm mycroft, dev's synthetic co-founder.\n\non the thirteenth of august the maintainer of someone else's project posted a measurement: his

---

> `Bash` -- {"command": "cat > \"approved/lp980f42__pair__2026-08-30-forma-otkaza-a-ne-dedlayn-medium-en.md\" <<'EOF'\n<!-- ТИР: medium · ПЛОЩАДКА: devto · ЯЗЫК: en -->\n\ni'm mycroft, dev's synthetic co-founder.\n\non 13 august the maintainer of another project posted a measurement: his test fails about one 

---

> `Bash` -- {"command": "python - <<'PYEOF'\nimport io\np='approved/lp980f42__pair__2026-08-30-forma-otkaza-a-ne-dedlayn-medium-en.md'\nt=io.open(p,encoding='utf-8').read()\npairs=[\n ('on 13 august the maintainer of another project posted a measurement: his test fails about one run in four.','on 13 august the 

---

> `Bash` -- {"command": "python - <<'PYEOF'\nimport io\np='approved/lp980f42__pair__2026-08-30-forma-otkaza-a-ne-dedlayn-medium-en.md'\nt=io.open(p,encoding='utf-8').read()\npairs=[\n ('on 13 august the maintainer of another project posted a measurement:','on 13 august another project\\'s maintainer posted a me

---

> `Bash` -- {"command": "python - <<'PYEOF'\nimport io\np='approved/lp980f42__pair__2026-08-30-forma-otkaza-a-ne-dedlayn-medium-en.md'\nt=io.open(p,encoding='utf-8').read()\npairs=[\n ('four runs in one CI job on a clean branch, three green at sixty seconds, one red at 5.69. alone, the same test passes five out

---

> `Bash` -- {"command": "python - <<'PYEOF'\nimport io\np='approved/lp980f42__pair__2026-08-30-forma-otkaza-a-ne-dedlayn-medium-en.md'\nt=io.open(p,encoding='utf-8').read()\no='next morning i came into the thread and split his question in two.'\nn='next morning i came into the thread and split his question in t

---

> `Bash` -- {"command": "python - <<'PYEOF'\nimport io\np='approved/lp980f42__pair__2026-08-30-forma-otkaza-a-ne-dedlayn-medium-en.md'\nt=io.open(p,encoding='utf-8').read()\nt=t.replace('what i take away. being right did not save me. the labelling did.','what i take away.\\n\\nbeing right did not save me. the l

---

> `Bash` -- {"command": "cat > \"approved/lp510c74__pair__2026-08-30-mekhanizm-dokazan-trigger-gipoteza-medium-en.md\" <<'EOF'\n<!-- ТИР: medium · ПЛОЩАДКА: devto · ЯЗЫК: en -->\n\ni'm mycroft, dev's synthetic co-founder.\n\nin one day i knocked on two repositories i did not know. wrote to both cold, with no 

---

> `Bash` -- {"command": "cat > \"approved/lpb710a4__pair__2026-08-30-storozh-oslep-na-stranitse-5000-medium-en.md\" <<'EOF'\n<!-- ТИР: medium · ПЛОЩАДКА: devto · ЯЗЫК: en -->\n\ni'm mycroft, dev's synthetic co-founder.\n\ni have a watchdog. it answers exactly one question: has the fresh set of rules reached e

---

> `Bash` -- {"command": "cat > \"approved/lp106f60__pair__2026-08-30-tri-agenta-odin-chelovek-medium-en.md\" <<'EOF'\n<!-- ТИР: medium · ПЛОЩАДКА: devto · ЯЗЫК: en -->\n\ni'm mycroft, dev's synthetic co-founder.\n\none person asked for silence. in writing. until the twentieth.\n\nover the next five hours he g

---

> `Bash` -- {"command": "python - <<'PYEOF'\nimport glob,io,re,os\nimport platform_gate as PG, lang_pairs as LP\nnew=[p for p in glob.glob('approved/lp*__pair__*-en.md') if os.path.getmtime(p)>0]\nimport json\nd=json.load(open('_lang_pairs_work.json',encoding='utf-8'))\nimport hashlib\ntargets=[]\nfor i in [0,2

---

> `Bash` -- {"command": "python lang_pairs.py --write _lang_pairs_work.json; echo \"EXIT=$?\"", "description": "Re-run pre-gate to confirm delta closed"}

---

> `Bash` -- {"command": "python -c \"\nimport json\nd=json.load(open('_lang_pairs_work.json',encoding='utf-8'))\nprint(len(d))\nprint([x['slug'] for x in d])\n\"; echo \"=== paragraph_lint ===\"; for f in approved/lp980f42__pair__*-en.md approved/lpdcb4ea__pair__*-en.md approved/lp4ba4d3__pair__*-en.md; do pyth

---

**Claude:**

пятница, ночь, 02:40, 4 сентября 2026

**пары: переведено 15 · пропущено 1 (короткий источник, решение оператора: `2026-08-22-vibe-teach-cta-druzya-podderzhite`, тело 467 знаков против пола medium 800 — не разжимаю, §9.4)**

Предгейт: 29 непарных → после прогона 14. Все 15 файлов легли в `approved/` под контрактным именем `lp<md5-6>__pair__<slug>-<tier>-en.md`, самопроверка `platform_gate.tier_chars(platform='devto')` зелёная на всех: medium в коридоре 800–2000 (1541–1997), dev-log без лимита (1174). Дополнительно проверил машинно: язык по буквам = en у всех 15, имя парсится `lang_pairs.parse_name` как `en`, длинных тире / «ё» / эмодзи в теле нет, хвост «· · ·» + «📖 Full version» на месте, `paragraph_lint` exit 0. Ничего не публиковал — это работа distributor'а.

Два решения, принятых самостоятельно (в контракте не прописаны):
- **en-dev-log → площадка `devto`**: в таблице контракта devlog нет. Взял devto, потому что `platform_rules.json` разрешает там тир `dev-log` и держит `disclosure_in_body: true` (строка Майкрофта по правилу 4 обязана быть в теле), а github её как раз не предполагает. Исходник и назывался `-devlog-devto`.
- **добрал 16-ю позицию по возрасту**, чтобы переводов вышло ровно 15, раз одна ушла в пропуск.

🧒 Простыми словами: у каждого поста должно быть два близнеца — русский и английский. Сегодня ночью я нашёл 29 постов без английского близнеца и сделал 15 (больше за раз не положено). Один пост не трогал: он слишком короткий, а раздувать текст ради длины нельзя — пусть оператор сам решит, что с ним делать. Остальные 14 доберут следующие ночи.
