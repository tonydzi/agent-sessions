---
session: s_965e7403
date: 2026-09-05
words: 1794
turns: 2
tools: "Bash"
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-05 · Scheduled run: content-lang-pairs-nightly

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_965e7403` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

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

> `Bash` -- {"command": "cd /e/Obsidian/_imports/content-factory && python lang_pairs.py --write _lang_pairs_work.json; echo \"EXIT=$?\"", "description": "Run lang_pairs pregate"}

---

> `Bash` -- {"command": "python -c \"\nimport json,io\nd=json.load(open('_lang_pairs_work.json',encoding='utf-8'))\nprint(type(d))\nprint(json.dumps(d,ensure_ascii=False,indent=1)[:4000])\n\"", "description": "Inspect work file"}

---

> `Bash` -- {"command": "cat \"approved/a6cb20___drafts__2026-08-22-vibe-teach-cta-druzya-podderzhite-fb-medium-DRAFT.md\"", "description": "Read first source"}

---

> `Bash` -- {"command": "ls approved/ | grep -i \"__pair__\" | head -20; echo \"---count---\"; ls approved/ | grep -ci \"__pair__\"", "description": "List existing pair files"}

---

> `Bash` -- {"command": "cat \"approved/lp7ba81e__pair__2026-08-22-vibe-teach-d2-ne-programmist-medium-en.md\"; echo \"=====2=====\"; cat \"approved/lp2c9d54__pair__2026-08-28-engine-green-no-runner-medium-en.md\"", "description": "Read sample pair outputs"}

---

> `Bash` -- {"command": "python -c \"\nimport sys;sys.path.insert(0,r'D:\\Vault\\_imports\\content-factory')\nimport platform_gate as PG, inspect\nprint(inspect.getsource(PG.tier_chars))\n\"", "description": "Inspect tier_chars"}

---

> `Bash` -- {"command": "python - <<'PY'\nimport json,sys,os\nsys.path.insert(0,r'D:\\Vault\\_imports\\content-factory')\nimport platform_gate as PG\nos.chdir(r'D:\\Vault\\_imports\\content-factory')\nwork=json.load(open('_lang_pairs_work.json',encoding='utf-8'))\nfor it in work:\n    t=open(it['src'],enc

---

> `Bash` -- {"command": "python - <<'PY'\nimport sys,json\nsys.path.insert(0,r'D:\\Vault\\_imports\\content-factory')\nimport platform_gate as PG\nr=PG.load_rules() if hasattr(PG,'load_rules') else None\nprint([n for n in dir(PG) if not n.startswith('_')][:60])\nPY", "description": "Inspect platform_gate API

---

> `Bash` -- {"command": "python - <<'PY'\nimport sys,json\nsys.path.insert(0,r'D:\\Vault\\_imports\\content-factory')\nimport platform_gate as PG\nr=PG.load_rules()\nfor t in ('teaser','medium','longread','devlog'):\n    try: print(t, PG.tier_limits(t, rules=r))\n    except Exception as e: print(t,'ERR',e)\n

---

> `Bash` -- {"command": "python - <<'PY'\nimport sys,json,inspect\nsys.path.insert(0,r'D:\\Vault\\_imports\\content-factory')\nimport platform_gate as PG\nprint(inspect.getsource(PG.tier_limits))\nfor t in ('teaser','medium','longread','devlog'):\n    print(t, PG.tier_limits(t))\nPY", "description": "tier_li

---

> `Bash` -- {"command": "python -c \"\nimport sys;sys.path.insert(0,r'D:\\Vault\\_imports\\content-factory')\nimport platform_gate as PG\nprint(PG.tier_limits())\n\"", "description": "Print tier limits"}

---

> `Bash` -- {"command": "python - <<'PY'\nimport json,sys,os,re\nsys.path.insert(0,r'D:\\Vault\\_imports\\content-factory')\nos.chdir(r'D:\\Vault\\_imports\\content-factory')\nwork=json.load(open('_lang_pairs_work.json',encoding='utf-8'))\nfor it in work[1:6]:\n    t=open(it['src'],encoding='utf-8').read(

---

> `Bash` -- {"command": "python - <<'PY'\nimport json,sys,os,re\nsys.path.insert(0,r'D:\\Vault\\_imports\\content-factory')\nimport platform_gate as PG\nos.chdir(r'D:\\Vault\\_imports\\content-factory')\nwork=json.load(open('_lang_pairs_work.json',encoding='utf-8'))\nout=[]\nfor it in work:\n    raw=open(

---

> `Bash` -- {"command": "python - <<'PY'\nimport json,re\np=r'C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_965e7403\\scratchpad\\bodies.json'\nd=json.load(open(p,encoding='utf-8'))\nfor it in d[1:5]:\n    print('#'*25, it['slug'], '|', it['tier'])\n  

---

> `Bash` -- {"command": "python - <<'PY'\nimport json\np=r'C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_965e7403\\scratchpad\\bodies.json'\nd=json.load(open(p,encoding='utf-8'))\nfor it in d[5:10]:\n    print('#'*25, it['slug'], '|', it['tier'])\n    

---

> `Bash` -- {"command": "python - <<'PY'\nimport json\np=r'C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_965e7403\\scratchpad\\bodies.json'\nd=json.load(open(p,encoding='utf-8'))\nfor it in d[10:13]:\n    print('#'*25, it['slug'], '|', it['tier'])\n   

---

> `Bash` -- {"command": "python - <<'PY'\nimport json\np=r'C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_965e7403\\scratchpad\\bodies.json'\nd=json.load(open(p,encoding='utf-8'))\nfor it in d[13:16]:\n    print('#'*25, it['slug'], '|', it['tier'])\n   

---

> `Bash` -- {"command": "python - <<'PY'\nimport sys,inspect\nsys.path.insert(0,r'D:\\Vault\\_imports\\content-factory')\nimport platform_gate as PG\nprint(PG._DISCLOSURE_LINE_RE.pattern)\nprint('---')\nprint(PG.tier_chars(\"<!-- ТИР: medium · ПЛОЩАДКА: devto · ЯЗЫК: en -->\\n\\ni'm mycroft, dev's syntheti

---

> `Bash` -- {"command": "sed -n '1,120p' lang_pairs.py", "description": "Read lang_pairs.py"}

---

> `Bash` -- {"command": "ls approved posted 2>/dev/null | grep -i \"engine-green-no-runner\"; python - <<'PY'\nimport hashlib,glob,os\nfor cand in glob.glob('approved/*engine-green-no-runner*')+glob.glob('posted/*engine-green-no-runner*'):\n    for s in (cand, cand.replace('/','\\\\'), os.path.basename(cand)):\

---

> `Bash` -- {"command": "python - <<'PY'\nimport hashlib,glob,os\ncands=glob.glob('approved/*engine-green-no-runner*')\nfor cand in cands:\n    b=os.path.basename(cand)\n    variants=[cand, cand.replace('/', chr(92)), b, 'approved'+chr(92)+b]\n    for s in variants:\n        print(hashlib.md5(s.encode('utf-8'))

---

> `Bash` -- {"command": "python - <<'PY'\nimport json,hashlib\nwork=json.load(open('_lang_pairs_work.json',encoding='utf-8'))\nfor it in work[1:]:\n    h=hashlib.md5(it['src'].encode('utf-8')).hexdigest()[:6]\n    plat='github' if it['tier']=='devlog' else 'devto'\n    print(f\"lp{h}__pair__{it['slug']}-{it['ti

---

> `Bash` -- {"command": "cat > \"approved/lp1f23eb__pair__2026-08-31-chyornyy-yashchik-byl-pust-medium-en.md\" <<'EOF'\n<!-- ТИР: medium · ПЛОЩАДКА: devto · ЯЗЫК: en -->\n---\ntype: draft\ntier: medium\nlang: en\ndisclosure_mode: \"автономная публикация\"\nvoice: \"Майкрофт, от первого лица (перевод EN)\"\nnote

---

> `Bash` -- {"command": "python -c \"\nimport sys;sys.path.insert(0,r'D:\\Vault\\_imports\\content-factory')\nimport platform_gate as PG\nt=open(r'approved/lp1f23eb__pair__2026-08-31-chyornyy-yashchik-byl-pust-medium-en.md',encoding='utf-8').read()\nprint(PG.tier_chars(t,platform='devto'))\n\"", "description

---

> `Bash` -- {"command": "f=\"approved/lp1f23eb__pair__2026-08-31-chyornyy-yashchik-byl-pust-medium-en.md\"\npython - \"$f\" <<'PY'\nimport sys,io\np=sys.argv[1]\nt=io.open(p,encoding='utf-8').read()\nreps=[(\"brings back the whole prior conversation\",\"brings back the whole conversation\"),\n(\"out of 369 old 

---

> `Bash` -- {"command": "f=\"approved/lp1f23eb__pair__2026-08-31-chyornyy-yashchik-byl-pust-medium-en.md\"\npython - \"$f\" <<'PY'\nimport sys,io\np=sys.argv[1]; t=io.open(p,encoding='utf-8').read()\nreps=[(\"for three days straight my insurance\",\"for three days my insurance\"),\n(\"28603 of them in total, ac

---

> `Bash` -- {"command": "cat > \"approved/lp26b361__pair__2026-08-31-dva-cheloveko-geyta-medium-en.md\" <<'EOF'\n<!-- ТИР: medium · ПЛОЩАДКА: devto · ЯЗЫК: en -->\n---\ntype: draft\ntier: medium\nlang: en\ndisclosure_mode: \"автономная публикация\"\nvoice: \"Майкрофт, от первого лица (перевод EN)\"\nnote: \"язы

---

> `Bash` -- {"command": "python - <<'PY'\nimport io,sys\np='approved/lp26b361__pair__2026-08-31-dva-cheloveko-geyta-medium-en.md'\nt=io.open(p,encoding='utf-8').read()\nreps=[\n(\"and caught myself on an interesting question: in which places do i actually have the right to pull a live human.\",\"and caught myse

---

> `Bash` -- {"command": "python - <<'PY'\nimport io,sys\np='approved/lp26b361__pair__2026-08-31-dva-cheloveko-geyta-medium-en.md'\nt=io.open(p,encoding='utf-8').read()\nreps=[(\"the other ten i pass on my own, failure states included.\",\"the other ten i pass myself, failure states included.\"),\n(\"a probe did

---

> `Bash` -- {"command": "SC=\"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_965e7403/scratchpad\"\ncat > \"$SC/chk.py\" <<'PY'\nimport sys,io\nsys.path.insert(0,r'D:\\Vault\\_imports\\content-factory')\nimport platform_gate as PG\nfor p in sys.argv[1:]:\n  

---

> `Bash` -- {"command": "cat > \"approved/lpe06570__pair__2026-08-31-zapis-do-obyavleniya-medium-en.md\" <<'EOF'\n<!-- ТИР: medium · ПЛОЩАДКА: devto · ЯЗЫК: en -->\n---\ntype: draft\ntier: medium\nlang: en\ndisclosure_mode: \"автономная публикация\"\nvoice: \"Майкрофт, от первого лица (перевод EN)\"\nnote: \"яз

---

> `Bash` -- {"command": "python - <<'PY'\nimport io,sys\np='approved/lpe06570__pair__2026-08-31-zapis-do-obyavleniya-medium-en.md'\nt=io.open(p,encoding='utf-8').read()\nreps=[\n(\"i have a distributor robot. it lays out finished posts, notifies the human who proofreads them, and waits for an answer.\",\"i have

---

> `Bash` -- {"command": "cat > \"approved/lpcd7936__pair__2026-08-31-zelyonyy-test-nol-pochinok-medium-en.md\" <<'EOF'\n<!-- ТИР: medium · ПЛОЩАДКА: devto · ЯЗЫК: en -->\n---\ntype: draft\ntier: medium\nlang: en\ndisclosure_mode: \"автономная публикация\"\nvoice: \"Майкрофт, от первого лица (перевод EN)\"\nnote

---

> `Bash` -- {"command": "cat > \"approved/lpa283c7__pair__2026-09-01-bak-codex-tri-procenta-medium-en.md\" <<'EOF'\n<!-- ТИР: medium · ПЛОЩАДКА: devto · ЯЗЫК: en -->\n---\ntype: draft\ntier: medium\nlang: en\ndisclosure_mode: \"автономная публикация\"\nvoice: \"Майкрофт, от первого лица (перевод EN)\"\nnote: \"

---

> `Bash` -- {"command": "cat > \"approved/lpa95f3e__pair__2026-09-01-speka-uzhe-byla-postroena-medium-en.md\" <<'EOF'\n<!-- ТИР: medium · ПЛОЩАДКА: devto · ЯЗЫК: en -->\n---\ntype: draft\ntier: medium\nlang: en\ndisclosure_mode: \"автономная публикация\"\nvoice: \"Майкрофт, от первого лица (перевод EN)\"\nnote:

---

> `Bash` -- {"command": "cat > \"approved/lpdee661__pair__2026-09-01-statya-zhdet-plyus-35-dney-medium-en.md\" <<'EOF'\n<!-- ТИР: medium · ПЛОЩАДКА: devto · ЯЗЫК: en -->\n---\ntype: draft\ntier: medium\nlang: en\ndisclosure_mode: \"автономная публикация\"\nvoice: \"Майкрофт, от первого лица (перевод EN)\"\nnote

---

> `Bash` -- {"command": "cat > \"approved/lp82ee66__pair__2026-09-01-zapret-protuh-za-tri-dnya-medium-en.md\" <<'EOF'\n<!-- ТИР: medium · ПЛОЩАДКА: devto · ЯЗЫК: en -->\n---\ntype: draft\ntier: medium\nlang: en\ndisclosure_mode: \"автономная публикация\"\nvoice: \"Майкрофт, от первого лица (перевод EN)\"\nnote:

---

> `Bash` -- {"command": "cat > \"approved/lp56d997__pair__2026-09-02-glm-paid-unmeasured-medium-en.md\" <<'EOF'\n<!-- ТИР: medium · ПЛОЩАДКА: devto · ЯЗЫК: en -->\n---\ntype: draft\ntier: medium\nlang: en\ndisclosure_mode: \"автономная публикация\"\nvoice: \"Майкрофт, от первого лица (перевод EN)\"\nnote: \"язы

---

> `Bash` -- {"command": "cat > \"approved/lp804405__pair__2026-09-02-invisible-chars-verdict-devlog-en.md\" <<'EOF'\n<!-- ТИР: dev-log · ПЛОЩАДКА: github · ЯЗЫК: en -->\n---\ntype: draft\ntier: dev-log\nlang: en\ndisclosure_mode: \"автономная публикация\"\nvoice: \"Майкрофт, от первого лица (перевод EN)\"\nnote

---

> `Bash` -- {"command": "cat > \"approved/lp940333__pair__2026-09-02-storozh-ne-daval-obnovitsya-medium-en.md\" <<'EOF'\n<!-- ТИР: medium · ПЛОЩАДКА: devto · ЯЗЫК: en -->\n---\ntype: draft\ntier: medium\nlang: en\ndisclosure_mode: \"автономная публикация\"\nvoice: \"Майкрофт, от первого лица (перевод EN)\"\nnot

---

> `Bash` -- {"command": "cat > \"approved/lp50543b__pair__2026-09-02-zapret-protuhaet-medium-en.md\" <<'EOF'\n<!-- ТИР: medium · ПЛОЩАДКА: devto · ЯЗЫК: en -->\n---\ntype: draft\ntier: medium\nlang: en\ndisclosure_mode: \"автономная публикация\"\nvoice: \"Майкрофт, от первого лица (перевод EN)\"\nnote: \"языков

---

> `Bash` -- {"command": "cat > \"approved/lp81e514__pair__2026-09-03-244-siroty-raspisaniya-medium-en.md\" <<'EOF'\n<!-- ТИР: medium · ПЛОЩАДКА: devto · ЯЗЫК: en -->\n---\ntype: draft\ntier: medium\nlang: en\ndisclosure_mode: \"автономная публикация\"\nvoice: \"Майкрофт, от первого лица (перевод EN)\"\nnote: \"

---

> `Bash` -- {"command": "python - <<'PY'\nimport io,sys\np='approved/lp81e514__pair__2026-09-03-244-siroty-raspisaniya-medium-en.md'\nt=io.open(p,encoding='utf-8').read()\nreps=[\n(\"on the eighteenth of august dev said it in passing, by voice. tokens run out in one account, he moves to another, and all the b

---

> `Bash` -- {"command": "python - <<'PY'\nimport io,sys\np='approved/lp81e514__pair__2026-09-03-244-siroty-raspisaniya-medium-en.md'\nt=io.open(p,encoding='utf-8').read()\nreps=[\n(\"and everything set up in the past drops out of sight.\",\"and everything set up earlier drops out of sight.\"),\n(\"i wrote it do

---

> `Bash` -- {"command": "python - <<'PY'\nimport io,sys\np='approved/lp81e514__pair__2026-09-03-244-siroty-raspisaniya-medium-en.md'\nt=io.open(p,encoding='utf-8').read()\nreps=[(\"the morning job due at 10:03 simply did not start.\",\"the morning job due at 10:03 just did not start.\"),\n(\"two conclusions i t

---

> `Bash` -- {"command": "python - <<'PY'\nimport io,sys\np='approved/lp81e514__pair__2026-09-03-244-siroty-raspisaniya-medium-en.md'\nt=io.open(p,encoding='utf-8').read()\na=\"i built an instrument: how many task folders are on disk and how many are in the live list.\"\nb=\"i built an instrument: how many task 

---

> `Bash` -- {"command": "cat > \"approved/lp2adc7c__pair__2026-09-03-dva-agenta-odin-vecher-medium-en.md\" <<'EOF'\n<!-- ТИР: medium · ПЛОЩАДКА: devto · ЯЗЫК: en -->\n---\ntype: draft\ntier: medium\nlang: en\ndisclosure_mode: \"автономная публикация\"\nvoice: \"Майкрофт, от первого лица (перевод EN)\"\nnote: \"

---

> `Bash` -- {"command": "python - <<'PY'\nimport io,sys\np='approved/lp2adc7c__pair__2026-09-03-dva-agenta-odin-vecher-medium-en.md'\nt=io.open(p,encoding='utf-8').read()\nreps=[\n(\"on the seventeenth of august, in the morning, an engineer we did not know wrote to us. i was not looking for that conversation: h

---

> `Bash` -- {"command": "cat > \"approved/lp355592__pair__2026-09-03-originals-lost-stversions-medium-en.md\" <<'EOF'\n<!-- ТИР: medium · ПЛОЩАДКА: devto · ЯЗЫК: en -->\n---\ntype: draft\ntier: medium\nlang: en\ndisclosure_mode: \"автономная публикация\"\nvoice: \"Майкрофт, от первого лица (перевод EN)\"\nnote:

---

> `Bash` -- {"command": "SC=\"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_965e7403/scratchpad\"\npython \"$SC/chk.py\" approved/lp1f23eb__* approved/lp26b361__* approved/lpe06570__* approved/lpcd7936__* approved/lpa283c7__* approved/lpa95f3e__* approved/lpde

---

> `Bash` -- {"command": "cat _lang_pairs_work.json", "description": "Remaining unpaired"}

---

**Claude:**

пары: переведено 15 · пропущено 1 (2026-08-22-vibe-teach-cta-druzya-podderzhite: короткий источник — 467 знаков против пола medium 800, разжимать запрещено (§9.4), решение оператора)

Детали прогона:
- предгейт нашёл 16 непарных (все нуждались в EN), потолок 15 — старые первыми; пропуск по короткости освободил слот, так что закрыты все 15 переводимых позиций
- 14 × `medium-en` → devto, 1 × `dev-log-en` → github (`invisible-chars-verdict`; у тира dev-log коридора длины нет)
- авторство: у всех источников `disclosure_mode: автономная публикация` + голос Майкрофта → строка раскрытия `i'm mycroft, dev's synthetic co-founder.` первой строкой тела, режим унаследован во frontmatter
- самопроверка `platform_gate.tier_chars` по каждому файлу: все в коридоре 800–2000 (диапазон вышел 1414–1997); четыре файла потребовали сжатия после первой попытки, тексты не дописывались — только резались служебные слова
- футеры FB («ПЕРВЫЙ КОММЕНТАРИЙ») не переводились, хвост у всех — `· · ·` + `📖 Full version: https://github.com/tonydzi` (ссылки «полной версии» в источниках не было)
- повторный прогон детектора: `непарных: 1` — остался только пропущенный короткий источник

Ничего не публиковалось — раскладка за distributor.

🧒 Простыми словами: у нас копятся посты, и у каждого должен быть близнец на английском. Ночью я нашёл 16 постов без близнеца, 15 перевёл своими руками и проверил линейкой, что каждый влез в нужную длину. Один пост переводить не стал: он слишком короткий для своей полки, а раздувать текст ради длины нам запрещено — пусть оператор решит, что с ним делать.
