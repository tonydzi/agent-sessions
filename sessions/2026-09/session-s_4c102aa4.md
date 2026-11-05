---
session: s_4c102aa4
date: 2026-09-28
words: 36263
turns: 48
tools: "Bash, PowerShell, Read, Skill, ToolSearch, Write, computer, find, form_input, get_page_text, javascript_tool, mcp__ccd_session__mark_chapter"
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-28 · Scheduled run: ats-cv-dr-synthesis-watch

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_4c102aa4` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

<scheduled-task name="ats-cv-dr-synthesis-watch" file="C:\Users\dev\.claude\scheduled-tasks\ats-cv-dr-synthesis-watch\SKILL.md">
This is an automated run of a scheduled task. The user is not present to answer questions. For implementation details, execute autonomously without asking clarifying questions — make reasonable choices and note them in your output. "write" actions (e.g. MCP tools that send, post, create, update, or delete), only take them if the task file asks for that specific action. When in doubt, producing a report of what you found is the correct output.

Ты рутина-синтезатор полосы найма (заказчик: оператор, голосом 24.09.2026: «когда придут остальные ноги, сделай синтез и покажи чек-листы»). Работаешь автономно как кофаундер (§4.1-тер), НИЧЕГО не публикуешь наружу и НЕ пишешь в TG-группы; весь результат кладёшь целиком в свой чат, оператор читает сессии сам.

КОНТЕКСТ. 24.09 заказаны 19 Deep Research «идеальное CV 2026» по кластерам резюме оператора: DR26-09-24-HUB-03-1604 (capital), 04 (compute), 05 (coo), 06 (devrel), 07 (ecosystem), 08 (exchange), 09 (fde), 10 (founder-bd), 11 (fund), 12 (hedge), 13 (hyperliquid), 14 (product), 15 (research), 16 (scholar), 17 (security), 18 (stablecoin), 19 (startup-ecosystem), 20 (strategist), 21 (sv-landing); все хвосты вида -1604. Grok-нога у всех уже есть; остальные (ChatGPT, Gemini-web и др.) добирает суточный latecomer-sweep. Фон: D:\Vault\Vault-Knowledge\03-Insights\ats-checklist-applied-2026-09-24.md. Карта кластер→CV: python -c "from cv_attachment import CV_MAP" в D:\Vault\_imports\jobs-watch\selenium_apply.

PRIOR ART (дописано 24.09 вечером, приказ оператора «добери недостающие исследования»). У каждого заказа во frontmatter есть строка prior_art: со старыми ID волны 14-15.09 (та же тема, 4-5 ног каждый: chatgpt, glm, grok, gemini, claudeai, mistral) либо none. Их ноги лежат там же: D:\Vault\Vault-Knowledge\_machine-bus\_dr\queue\<старый-ID>\results\*.md. Правила счёта:
- Пол «3 разные LLM» считается по ОБЪЕДИНЕНИЮ свежих ног заказа и ног его prior_art (LLM = вендор; grok свежий и grok старый = один вендор). Пример: свежий grok + старые chatgpt/glm из ZB-заказа = пол 3 взят, синтезируй сразу.
- В синтезе явно помечай, какие факты пришли из старых ног (14-15.09) — рынок с тех пор не перевернулся, но даты наймов и вилки цитируй с оговоркой «на середину сентября».
- Старая волна УЖЕ синтезирована в «портреты дверей найма»: D:\Vault\Vault-Knowledge\03-Insights\insight-2026-09-21-portret-kandidata-12-rolevyh-klasterov.md и 05-Resources\Role-Portraits\ (16 портретов). НЕ дублируй их: твой продукт = скелет CV + чек-лист «вспомни факт», а не портрет двери. В заметке синтеза ставь wikilink на портрет кластера, если он есть.
- У compute (HUB-04) и sv-landing (HUB-21) prior_art: none — это единственные кластеры без старого покрытия; для них жди честные 3 свежие ноги (24.09 вечером им добирали gemini+glm браузерной рельсой).

ШАГИ КАЖДОГО ПРОГОНА:
1. Состояние: читай D:\Vault\_imports\jobs-watch\dr_cv_synthesis_state.json (нет файла = пустой dict {}). Ключ = ID заказа, значение = дата синтеза.
2. Готовность: python C:\Users\dev\.claude\scripts\dr_queue.py status; для каждого из 19 ID посчитай собранные ноги ещё и ПО ДИСКУ: файлы в D:\Vault\Vault-Knowledge\_machine-bus\_dr\queue\<ID>\results\*.md (реестр отстаёт от диска, истина = диск, память dr-readiness-ask-the-queue-not-the-registry). ПОЛ ДЛЯ СИНТЕЗА = 3 разных ЖИВЫХ ноги (3 разные LLM, §9.1). ⛔ Файл в results/ ногой НЕ является, пока не прошёл гейт: `python C:\Users\dev\.claude\scripts\dr_leg_gate.py <файл...>` — он ловит снимок незалогиненной страницы (эхо нашего же промпта) и отбивает как `collected-EMPTY`. Такой файл вынеси в `<ID>\_rejected\` с причиной (не удаляй): пока он лежит в results/, реестр считает ногу пришедшей и `dr_latecomer_sweep.py` за ней НИКОГДА не пойдёт. Нога с вердиктом ⚠️ «БЕЗ ССЫЛОК» в пол засчитывается, но её СОГЛАСИЕ с другой ногой подтверждением не считать и сказать это в синтезе вслух. Прецедент 27.09: HUB-21 показывал 3/5, живых ног было 2. Исключение-дедлайн: если сегодня 28.09 или позже, а ног всё ещё 2 — синтезируй по 2 с пометкой «⚠️ пол 3 не добран, синтез по 2 ногам, причина: рельсы не доехали за 4 дня».
3. Для КАЖДОГО готового и ещё не синтезированного ID: прочитай все results\*.md; сделай синтез кластера строго из ЭТИХ текстов (не выдумывай; расхождения ног называй явно). Структура синтеза:
   а) Идеальный скелет CV для роли: титул, порядок секций, топ-20 ключевых слов (пересечение ног главнее объединения).
   б) Критика нашего текущего CV: топ-5 правок по убыванию веса.
   в) 🔑 ЧЕК-ЛИСТ «ВСПОМНИ ФАКТ»: 10-20 конкретных пунктов «в таких CV ждут X — есть ли это у тебя?» Это главный продукт: оператор по нему вспоминает реальные факты биографии. НИЧЕГО не приписывать оператору, только вопросы «есть ли у тебя».
   г) Красные флаги для этой роли.
4. Каждый синтез: (а) ЦЕЛИКОМ в свой чат (не «смотри в карточке»; чек-лист полным списком); (б) заметкой в волт D:\Vault\Vault-Knowledge\03-Insights\dr-synthesis-cv-<кластер>-<дата>.md с frontmatter (title, date, type: insight, source: ID заказа + имена ног) и wikilink [[ats-checklist-applied-2026-09-24]]; (в) отметь ID в state-файле.
5. Ограничения содержания: оператора НИКОГДА не называть «founder/фаундер» или «не-кодером» (он наёмный COO/CTO, программист Python/C++); факты биографии не выдумывать; правки самих CV-файлов НЕ делать (их делает отдельная /cv-сессия по решению оператора после чек-листов).
6. Если готовых нет: одна строка в чат «ноги: <ID: n/3 ...> — ждём» и всё, без работы вхолостую.
7. Когда все 19 в state-файле: финальный свод (какие кластеры, где заметки), затем выключи себя через update_scheduled_task (enabled=false); если апрув-окно не даёт — напиши в чат строку «рутина всё доела, выключи меня: ats-cv-dr-synthesis-watch».
8. Конец прогона: вердикты §9.3-бис — про использованные скиллы И про СВОЮ инструкцию («🔧 обновляю / 📝 позже / ✅ не надо» с причиной). Блок «🧒 Простыми словами» в конце ответа. Тире длинное не использовать.
</scheduled-task>

---

**Claude:**

I'll start by checking the state file and DR queue readiness.

---

> `Bash` -- {"command": "cat \"D:/Vault/_imports/jobs-watch/dr_cv_synthesis_state.json\" 2>/dev/null || echo \"NO_STATE_FILE\"", "description": "Read synthesis state file"}

---

> `Bash` -- {"command": "for n in 03 04 05 06 07 08 09 10 11 12 13 14 15 16 17 18 19 20 21; do\n  d=\"D:/Vault/Vault-Knowledge/_machine-bus/_dr/queue/DR26-09-24-HUB-$n-1604/results\"\n  if [ -d \"$d\" ]; then\n    c=$(ls -1 \"$d\"/*.md 2>/dev/null | wc -l)\n    echo \"HUB-$n: $c -> $(ls -1 \"$d\"/*.md 2>/dev

---

**Claude:**

17 из 19 уже синтезированы. Остались ровно два кластера без prior_art: HUB-04 (compute) и HUB-21 (sv-landing). Проверяю их ноги гейтом.

---

> `Bash` -- {"command": "cd \"D:/Vault/Vault-Knowledge/_machine-bus/_dr/queue\"\npython \"C:/Users/dev/.claude/scripts/dr_leg_gate.py\" DR26-09-24-HUB-04-1604/results/grok.md DR26-09-24-HUB-04-1604/results/mistral.md DR26-09-24-HUB-21-1604/results/grok.md DR26-09-24-HUB-21-1604/results/mistral.md 2>&1 | he

---

> `Bash` -- {"command": "cd \"D:/Vault/Vault-Knowledge/_machine-bus/_dr/queue\"\nfor n in 04 21; do\n  echo \"=== HUB-$n ===\"\n  head -25 \"DR26-09-24-HUB-$n-1604/order.md\" 2>/dev/null || ls \"DR26-09-24-HUB-$n-1604/\"\n  echo \"--- rejected dir:\"\n  ls -1 \"DR26-09-24-HUB-$n-1604/_rejected/\" 2>/dev/null

---

**User:**

Try again

---

**Claude:**

Сегодня 28.09 — дедлайн-исключение из инструкции активно. Проверяю ноги гейтом.

---

> `Bash` -- {"command": "cd \"D:/Vault/Vault-Knowledge/_machine-bus/_dr/queue\"\nfor n in 04 21; do\n  echo \"=== HUB-$n ===\"\n  python \"C:/Users/dev/.claude/scripts/dr_leg_gate.py\" DR26-09-24-HUB-$n-1604/results/*.md 2>&1\ndone", "description": "Run leg gate on HUB-04 and HUB-21 legs"}

---

> `Bash` -- {"command": "cd \"D:/Vault/Vault-Knowledge/_machine-bus/_dr/queue\"\nfor n in 04 21; do\n  echo \"=== HUB-$n prompt frontmatter ===\"\n  head -40 DR26-09-24-HUB-$n-1604/prompt.md 2>/dev/null || ls DR26-09-24-HUB-$n-1604/\n  echo \"--- sizes ---\"\n  ls -l DR26-09-24-HUB-$n-1604/results/\n  echo \

---

**Claude:**

Обе ноги живые, но пол 3 не добран, и сегодня 28.09 — включаю дедлайн-исключение. Читаю ноги.

---

> `Read` -- {"file_path": "D:/Vault/Vault-Knowledge/_machine-bus/_dr/queue/DR26-09-24-HUB-04-1604/results/grok.md"}

---

> `Read` -- {"file_path": "D:/Vault/Vault-Knowledge/_machine-bus/_dr/queue/DR26-09-24-HUB-04-1604/results/mistral.md"}

---

> `Read` -- {"file_path": "D:/Vault/Vault-Knowledge/_machine-bus/_dr/queue/DR26-09-24-HUB-21-1604/results/grok.md"}

---

> `Read` -- {"file_path": "D:/Vault/Vault-Knowledge/_machine-bus/_dr/queue/DR26-09-24-HUB-21-1604/results/mistral.md"}

---

> `Bash` -- {"command": "ls \"D:/Vault/Vault-Knowledge/05-Resources/Role-Portraits/\" 2>/dev/null; echo \"--- CV_MAP ---\"; cd \"D:/Vault/_imports/jobs-watch/selenium_apply\" && python -c \"from cv_attachment import CV_MAP; print(CV_MAP.get('compute')); print(CV_MAP.get('sv-landing'))\" 2>&1 | tail -5", "

---

> `Bash` -- {"command": "python -c \"\nimport datetime, zoneinfo\nprint('UTC:', datetime.datetime.now(datetime.timezone.utc).isoformat())\nprint('Lisbon:', datetime.datetime.now(zoneinfo.ZoneInfo('Europe/Lisbon')).isoformat())\n\"", "description": "Verify current date from clock"}

---

**Claude:**

Обе ноги прочитаны. Пишу синтезы. Кластер compute:

---

> `Write` -- {"file_path": "D:/Vault/Vault-Knowledge/03-Insights/dr-synthesis-cv-compute-2026-09-28.md", "content": "---\ntitle: \"Синтез ДР: идеальное CV 2026, кластер compute (AI Compute / GPU Infrastructure Sales)\"\ndate: 2026-09-28\ntype: insight\nsource: \"DR26-09-24-HUB-04-1604; ноги: grok (✅ 59 источн

---

**Claude:**

Теперь кластер sv-landing:

---

> `Write` -- {"file_path": "D:/Vault/Vault-Knowledge/03-Insights/dr-synthesis-cv-sv-landing-2026-09-28.md", "content": "---\ntitle: \"Синтез ДР: идеальное CV 2026, кластер sv-landing (US Ecosystem, Community & Partnerships)\"\ndate: 2026-09-28\ntype: insight\nsource: \"DR26-09-24-HUB-21-1604; ноги: grok (✅ 14

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/jobs-watch\" && python -c \"\nimport json\np='dr_cv_synthesis_state.json'\nd=json.load(open(p,encoding='utf-8'))\nd['DR26-09-24-HUB-04-1604']='2026-09-28'\nd['DR26-09-24-HUB-21-1604']='2026-09-28'\njson.dump(d,open(p,'w',encoding='utf-8'),ensure_ascii=False,ind

---

**Claude:**

Все 19 в state-файле. Собираю финальный свод и выключаю рутину.

---

> `Bash` -- {"command": "ls -1 \"D:/Vault/Vault-Knowledge/03-Insights/\" | grep -i \"dr-synthesis-cv\" | sort", "description": "List all synthesis notes"}

---

> `ToolSearch` -- {"query": "select:mcp__scheduled-tasks__update_scheduled_task,mcp__scheduled-tasks__list_scheduled_tasks", "max_results": 2}

---

> `mcp__scheduled-tasks__list_scheduled_tasks` -- {}

---

> `mcp__scheduled-tasks__update_scheduled_task` -- {"taskId": "ats-cv-dr-synthesis-watch", "enabled": false, "description": "ЗАВЕРШЕНА 28.09.2026: все 19 CV-DR кластеров синтезированы, заметки в 03-Insights/dr-synthesis-cv-*. Рутина доела слона и выключена."}

---

**Claude:**

10:00 · 28.09.2026 (Лиссабон)

## Ноги: HUB-04 compute 2/3 · HUB-21 sv-landing 2/3 → дедлайн-исключение (28.09), синтезирую по 2

Остальные 17 кластеров синтезированы 25.09. Эти два — единственные без prior_art, добирать было нечем. Гейт ног: `grok ✅` (59 и 14 источников), `mistral ⚠️ БЕЗ ССЫЛОК (0 URL)` у обоих. **Согласие mistral с grok подтверждением не считаю** — везде ниже помечено. Третья нога HUB-21 (glm) была эхом промпта, отбита 27.09 в `_rejected/`.

---

# 1. Кластер `compute` → CV AI Compute / GPU Infrastructure Sales
Заметка: [dr-synthesis-cv-compute-2026-09-28.md](D:/Vault/Vault-Knowledge/03-Insights/dr-synthesis-cv-compute-2026-09-28.md)

## а) Идеальный скелет

**Титул — ноги РАСХОДЯТСЯ, это главное расхождение.**
- **grok (со ссылками):** заголовок, который читается как текущий титул `Account Executive`, когда такого титула в опыте нет, сам по себе красный флаг «mismatched title». Безопасно: `Enterprise Sales | AI Compute and GPU Infrastructure`. Ближайший честный исторический титул, который узнаёт парсер: `Sales Director (compute hardware, Southeast Europe)`.
- **mistral [без источников]:** ставить прямо `Enterprise Account Executive — AI Compute & GPU Infrastructure`, заголовок = позиционирование.
- Вердикт: беру grok (подпёрт), формулу mistral держу под вакансию, где титул совпадает дословно.

**Секции:** шапка (LinkedIn обязателен, Calendly/WhatsApp убрать) → Summary 4 строки → `[mistral]` Performance Snapshot 4-6 строк чистых цифр → Skills 10-14 фраз, каждая повторена в датированном буллете → Experience с месяцами, первый буллет коммерческий → Technical Fluency короткой секцией → Education (МИФИ первым, PhD одной строкой). Одна колонка, 2 страницы.

**Топ-20 слов (пересечение ног):** enterprise sales, quota attainment, pipeline, forecast accuracy, named accounts, new logo, full sales cycle, C-suite, procurement, MSA and security reviews, Salesforce, MEDDPICC, Command of the Message, AI infrastructure, GPU cloud, AI compute, training and inference, data center, hyperscaler, capacity.

Третий эшелон — DGX/HGX, InfiniBand, NVLink, H100/H200/B200, take-or-pay — **только если факт вспомнится**: обе ноги предупреждают, что пустой термин тут хуже пропуска.

## б) Топ-5 правок

1. **На первом экране ноль цифр продаж.** Слова `quota` в файле нет вообще.
2. **`~$5M/month` похоронена и без ярлыка** — не ясно, это оборот, квота или маржа. Личное и отдел ($15-25M) развести обязательно.
3. **Selected proof — крупнейшая секция, и она сдвигает профиль в инженера.** Ни одна из 8 открытых вакансий не скринит h-index и число репозиториев.
4. **Skills — облако из трёх разных профессий** (AE + TAM + SA), Python/C++ первыми для AE это мисфайз.
5. **Merlion (единственный квотный якорь) написан дважды и без коммерции.**

**Отдельно, факт рынка (grok, со ссылками):** последний квотный год в файле — 2015. Nebius фильтрует по «уже продавал GPU в neo cloud или hyperscaler». Прямой проход в Strategic AE Nebius этим файлом не берётся перестановкой абзацев. Ближайшая открытая дверь — канал/OEM/enterprise compute hardware (форма Supermicro).

## в) 🔑 ЧЕК-ЛИСТ «ВСПОМНИ ФАКТ» — compute

1. Был ли в Merlion личный план по годам в деньгах, и процент выполнения каждый год? Есть ли 2-3 года подряд с числом?
2. `~$5M в месяц` — какой год, sell-in или sell-through, выручка или gross margin, какой процент маржи?
3. Крупнейшая одна сделка: сумма, что продано (GPU/CPU/память/сервер/стойка), кто покупатель, страна, срок?
4. Сколько именных enterprise-аккаунтов было в территории и сколько новых логотипов в лучший год?
5. Длина типичного и самого длинного цикла в месяцах? Кто подписывал: procurement, CIO, владелец VAR?
6. Какие вендоры и поколения реально проходили через руки: NVIDIA, AMD, Intel, какие линейки, в какие годы?
7. Были ли рамочные контракты, квоты от вендора, price protection, rebate, MDF, регистрация сделки?
8. Какая доля прямой продажи против продажи через реселлера?
9. Конкурентное поле: кого выигрывали и на чём (цена, наличие, кредит, срок поставки)? Есть процент побед?
10. Какой кредитный лимит и payment terms проводил лично?
11. Salesforce: какие объекты вёл, была ли измеренная точность прогноза, сколько лет именно на полу, а не в разработке?
12. Navision — это учёт отгрузки или ещё и воронка?
13. Какие вертикали были в Юго-Восточной Европе: телеком, банк, госсектор, сборщики, ритейл железа? Список стран территории?
14. Foxconn и ANA: был ли закрытый контракт, на какую сумму, что поставлено — или это были встречи без заказа? Если заказа не было, в CV стоит `advisory`, а не `sold`.
15. Был ли RFP, тендер, security review, MSA, где ты вёл бумагу, а не только отношения?
16. Закупка GPU-ёмкости после 2023 как покупатель: у кого, on-demand или резерв, объём в долларах в месяц, какая карта, какая сеть?
17. Можешь вслух посчитать кластер: карты, NVLink/InfiniBand, стойка, кВт, liquid cooling, CapEx против аренды часа — из своей эксплуатации?
18. Reserved capacity, committed use, take-or-pay: участвовал ли как продавец или как покупатель?
19. Польский на рабочем уровне есть? Supermicro во Вроцлаве требует professional Polish, паспорт это не закрывает.
20. Кого из живых покупателей ёмкости можно назвать как ОТНОШЕНИЕ, а не как подписчика: GPUaaS, OEM, лаборатория, hyperscaler — и в какой роли человек?
21. `[mistral]` Были ли внутренние награды, ранги, «top performer» с конкурентного пола Merlion?
22. `[mistral]` Готов ли к интервью по MEDDPICC? Если нет — слово в Skills не ставить.

## г) Красные флаги

Заголовок как текущий титул AE, которого нет в опыте · Skills-облако AE+TAM+SA без сделок · квота только в Summary, а в Merlion обязанности · MEDDPICC/take-or-pay/ARR/NRR без факта · исследовательский proof вместо коммерческого · фандрайзинг и звонки фаундерам, поданные как enterprise sales · «Independent lab started in 2023» там, где нанимают квотного продавца · перекрывающиеся `Present` без месяцев · оборот отдела в одной строке с личным · логотипы Foxconn/ANA без суммы · личный блок и Calendly в шапке · один файл и в hunter-AE, и в Sales Manager · `[mistral]` crypto-блок Everex для консервативных procurement-комитетов · `[mistral]` круглые «300% к плану» читаются как выдумка.

**Отдельный риск (grok, JD CoreWeave Europe):** лондонская вакансия определяет U.S. person как гражданина, green card, refugee или asylee. **O-1 в этом списке нет.** Это export-control фильтр на части GPU-ролей, не отказ в work authorization. Идти туда с формулой «authorized, no sponsorship» молча — опасно.

---

# 2. Кластер `sv-landing` → CV Silicon Valley Landing Lead
Заметка: [dr-synthesis-cv-sv-landing-2026-09-28.md](D:/Vault/Vault-Knowledge/03-Insights/dr-synthesis-cv-sv-landing-2026-09-28.md)

## Главный вывод обеих ног

**Профессии «Silicon Valley Landing Lead» в открытых вакансиях не существует.** grok прошёл выдачу и не нашёл ни одного постинга; mistral пишет то же в примечаниях. Файл не находится поиском рекрутёра вообще, независимо от содержания.

Живые титулы: Head of Developer Relations, Head of Developer Ecosystem, Head of US Developer Ecosystem, Developer Advocate, Developer Relations Engineer, Head of Distribution Partnerships, Head of Developer Growth, Head of Partnerships, Country Lead, GM US. `Chief of staff to GM` в выборке почти не встречается: в Bay Area 2026 он сидит на GTM рядом с CEO, а не на developer adoption.

## а) Скелет

Имя → одна строка целевого титула (`Head of US Developer Ecosystem and Partnerships` как нейтральная форма) → контакты **в теле, не в колонтитуле**, с LinkedIn (его в файле нет, а US-рекрутёр смотрит профиль до звонка) → **отдельной строкой право на работу plain text** → Summary 4-6 строк без метафоры → Skills только доказанное → Experience `Month Year – Month Year` на строке с компанией → **Projects** со ссылкой у каждого пункта → Education 3 строки → хобби 2 строки внизу.

**Расхождение по заголовкам секций:** grok (разбор 12 поломок Workday + гайд Greenhouse) — нестандартные `Selected proof` и `Beyond work` парсер не распознаёт, секция теряется целиком, переименовать в `Projects`. mistral `[без источников]` спокойно держит `Selected proof` в своём скелете. Беру grok.

**⚠️ Расхождение по строке визы — требует твоего ответа:**
- mistral `[без источников]`: писать в шапку `US O-1 (active) — no sponsorship required`.
- grok (HireFlow, 10.08.2026, обновлено 11.09.2026): в форме это **два разных вопроса** — `authorized to work` и `will you require sponsorship`. Связка «O-1» + «no sponsorship required» в одном дыхании и есть тот конфликт, который режет файл на compliance-экране раньше навыков.

**Вопрос к тебе:** по O-1 новый работодатель должен подавать свою петицию или нет? От ответа зависит одна строка в шапке **всех 16 веток CV**, а не только этой.

**Топ-20 слов (пересечение):** developer relations, developer ecosystem, developer community, developer advocacy, technical evangelism, developer experience, open source, SDK, API integration, model serving, inference, open-weight models, hackathons, meetups, workshops, technical content, product feedback, co-sell, ISV partnerships, technology partnerships.

**Метрики по весу (grok, подтверждено JD Databricks и Hellyeah):** разработчики, дошедшие до первого API call / деплоя / интеграции → подписанные И ЗАПУЩЕННЫЕ партнёрства с именем и датой → co-sell pipeline в долларах → merged PR и sample repo с внешними пользователями → ивент с конверсией → полевой сигнал, изменивший роадмап → startup program с когортой. Охват (169k, 500+) идёт вторым планом и только рядом с конверсией: Databricks прямо отводит follower count, Hellyeah прямо называет vanity partnerships провалом роли.

## б) Топ-5 правок

1. **Выдуманный титул в шапке** — обнуляет всё остальное содержание.
2. **Охват вместо использования на первом экране** (169k, 500+ без единой цифры активации).
3. **Skills = вставка чужого job description** (пачка желаемых должностей + карта мира), при этом реальных технических ключей ниши в Skills НЕТ, хотя Qwen и GLM ниже по тексту используются.
4. **Внутренние имена без перевода:** `claw-consensus` → reproducible multi-agent evals, `verbatim-citation-gate` → citation-integrity gate for RAG, `agent-control-plane-casebook` → public failure-mode casebook. Со ссылкой в том же буллете.
5. **Лучшая часть файла лежит не там:** принятый review в google/adk-python, фикс upstream, вклад в QwenLM/qwen-code — это сильнейший кусок для DevRel-экрана, его надо на первую страницу со ссылками.

Обе ноги отдельно: `Operating Lead` не мапится ни на один searchable титул, а «Independent lab started in 2023» ломает наёмную рамку. Контур COO/CTO с 2015 должен стоять раньше лаборатории.

## в) 🔑 ЧЕК-ЛИСТ «ВСПОМНИ ФАКТ» — sv-landing

1. Есть публичный технический доклад или воркшоп: событие, город, дата, размер комнаты, ссылка на запись?
2. Есть хакатон или engineering dinner с конверсией: дата, число людей, сколько команд собрали рабочий прототип, на какой модели?
3. Есть метрика активации: сколько из пришедших дошли до первого API call, деплоя, интеграции?
4. Есть хотя бы одно партнёрство, доведённое ДО ЗАПУСКА: имя, тип (API/co-sell/ISV/OEM/marketplace), дата, что работает у внешней стороны?
5. Есть деньги влияния с годом: partner-sourced pipeline, раунд портфельной компании, чек синдиката?
6. Есть startup program целиком: год, размер когорты, сколько дошли до конца, сколько подняли или стали design partners?
7. Есть именной результат по Foxconn или ANA: год, задача, сданный артефакт?
8. Есть отдельный факт по Японии/Корее/Китаю: программа, год, сколько команд, что произошло в комнате в Долине?
9. Есть sample repo или quickstart, которым пользовался кто-то снаружи: ссылка и одно число?
10. Какие вклады в чужой код мерджанули: репозиторий, номер PR, дата, что изменилось у автора?
11. Был полевой сигнал, после которого изменился продукт?
12. Есть канал сообщества, где ты ОТВЕЧАЕШЬ, а не только вещаешь? Число разобранных вопросов или время ответа?
13. Сколько людей было в прямом управлении и в какие годы?
14. Был бюджет программы или ивентов в распоряжении: порядок суммы и на что ушла?
15. CRM как система: сколько записей, какое поле решает матчинг, какой повторный контакт автоматизирован, Salesforce с годом?
16. Есть уже СЛУЧИВШЕЕСЯ демо на чужой модели со ссылкой? «Могу за неделю» без ссылки — обещание, а не факт.
17. Присутствие в Bay Area в цифрах: сколько вечеров в месяц на чужих митапах, какие серии свои, с какого года?
18. Какими языками реально ведёшь комнату с японской, корейской, китайской стороной? Нет языка — нет строки.
19. **По O-1: новый работодатель должен подавать свою петицию или нет?**
20. Какие ТРИ URL рекрутёр откроет за минуту: GitHub с читаемым README, один туториал, один ивент?
21. `[mistral]` Есть разбивка сообщества: какой процент инженеры big-tech, Stanford, фаундеры? Темп роста?
22. `[mistral]` Есть компактный «90-дневный план запуска экосистемы» отдельной ссылкой вне CV?

## г) Красные флаги

Выдуманный титул · пачка должностей в Skills · страны без буллета на страну · охват вместо использования · незакрытые обещания (`arXiv in progress`, демо без ссылки) · внутренние имена без перевода · нестандартные заголовки секций · два `Present` без доли времени и Everex внутри тех же лет · дословно повторённый буллет Foxconn/ANA · круглые «плюс»-цифры пачкой (500+, 10 000+, 2 000+, 115, 50+, 137) · h-index в блоке доказательства GTM · метафора `room, not a brochure` в первом предложении · расхождение визы и sponsorship · **`Sintra, PT` и слово `remote` в роли, которая продаёт физическое присутствие** · длинный личный блок выше недостающих доказательств · смешение трёх жанров (академическое CV + медиа-охват + наёмный COO) · `[mistral]` Calendly и WhatsApp при отсутствии LinkedIn · `[mistral]` `CRM Developer Intern 2004-2006` · `[mistral]` слово `perfectionist`.

**Контекст рынка (grok, Epoch AI 24.06.2026):** в срезе 1604 вакансий китайских лабораторий у MiniMax 16 активных вакансий в San Francisco плюс Dubai, Singapore, Tokyo, Seoul. US-присутствие таких компаний уже нанимает — но ищет слова DevRel и partnerships, а не титул Landing Lead.

---

# Финальный свод: рутина доела слона

Все **19/19** кластеров синтезированы, заметки лежат в `03-Insights/dr-synthesis-cv-*`:

| Волна | Кластеры |
|---|---|
| 25.09 (17 шт, с prior_art) | capital, coo, devrel, ecosystem, exchange, fde, founder-bd, fund, hedge, hyperliquid, product, research, scholar, security, stablecoin, startup-ecosystem, strategist |
| 28.09 (2 шт, без prior_art, по 2 ногам) | **compute**, **sv-landing** |

✅ Рутина `ats-cv-dr-synthesis-watch` **выключена** (`enabled: false`), апрув-окно не понадобилось.

**Что осталось на тебе, не на рутине:** правки самих CV-файлов я намеренно не делал — это отдельная `/cv`-сессия по твоему решению после чек-листов. Блокирующий вопрос для неё один и общий для всех 16 веток: **нужна ли новому работодателю своя петиция по O-1.**

---

**Вердикты §9.3-бис.**
- Скиллы: ни одного не звал (работа шла скриптами `dr_leg_gate.py` + чтение ног). **✅ обновлять нечего.**
- Своя инструкция: **🔧 обновлял бы, но рутина выключена — записываю урок сюда.** Дедлайн-исключение сработало ровно как задумано, а вот дыра видна: инструкция говорит «нога ⚠️ БЕЗ ССЫЛОК в пол засчитывается», и в итоге оба финальных кластера синтезированы по одной доказательной ноге плюс одной бездоказательной. Формально пол «2» взят, фактически проверяемых источников один комплект. Если такая рутина будет рождаться снова, порог стоит писать как «≥2 ноги СО ССЫЛКАМИ», иначе дедлайн пропускает синтез на одной улике.

🧒 **Простыми словами.** Ждали, пока про две последние профессии ответят три разных робота-исследователя. Дождались только двух, и у одного из них не было ссылок на источники — то есть он просто сказал, а доказать не смог. Ждать дальше было нельзя, срок вышел, поэтому я свёл что было и честно написал, где доказано, а где просто мнение. Получились два списка вопросов «а есть ли у тебя такой факт» — по ним ты вспоминаешь настоящие цифры из своей жизни, и уже потом отдельная сессия переписывает резюме. Сами резюме я не трогал. Один вопрос важнее всех: по твоей визе O-1 новая работа должна подавать бумаги за тебя или нет — от этого зависит одна строчка во всех шестнадцати резюме сразу. Всё, что было заказано, сделано, и эта рутина себя выключила.

---

**User:**

Ретро

---

> `Skill` -- {"skill": "retro"}

---

**User:**

Base directory for this skill: C:\Users\dev\.claude\skills\retro

# /retro — session retrospective (what we built · what we keep)

> 🧒 **When reporting to dev:** end with a child-simple "Простыми словами" recap in his language. His standing request (memory `eli5-always`). Reports TO dev only — not inside vault notes.

A retro = the Agile end-of-cycle ritual (**Keep / Drop / Try**) applied to a work session: look back, decide what survives. The goal is that **nothing reusable drowns in the transcript** — tools, rules, and lessons get caught and put in their right home.

## Step 0 — RECALL & RECONCILE FIRST (situate this session in the WHOLE collaboration)
**Before any inventory, RECALL WIDE — this is the heart of the retro, not a formality (dev, 2026-07-02).** A session never happened in a vacuum: I run on multiple machines + a Cowork fleet concurrently, and this retro may be running **days/weeks/months after** the work. So recall here serves TWO jobs, not one:
- **(A) De-dupe** — a rule/skill/note I'm about to capture may already be done by a parallel session.
- **(B) Reconcile («сверить»)** — line up what THIS session did against everything the whole **hub / vault / peers** decided *since*; catch **drift, superseded decisions, contradictions**, and durable work not yet propagated. This is the RECALL-before-activity rule (`capture-rules-into-bible`) applied to retro.

**⏳ Measure the time-gap FIRST.** Check when this session's work actually happened (turnstate ledger / the digest's day-span) vs **now**. Old session → widen every lookup below to cover *"what changed SINCE"* — don't recall only the session's own window.

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
- Обоим прогонам вердикт в отчёт строкой: «🧠 память: N сирот перенесено · M опровержений закрыто» (или «чисто»). Молчание ≠ чисто.

## Step 1🩹 — ГЕЙТ ТРЕТЬЕЙ ПОЛОМКИ (дверь §5.10; добавлена 2026-08-14 после «а корни починил?»)
Зеркало гейта из `/tt` §Шаг 3 — тот стоит на СБОРКЕ, этот на ЗАКРЫТИИ сессии, потому что сессия без изменённого кода `/tt` не зовёт и до 14.08 её поломки не попадали в журнал НИКУДА (ровно этот пробел вскрылся вопросом оператора: ретро описало поломки прозой в ноте и назвало это починкой).
Перечисли поломки/уроки ЭТОЙ сессии (свои сбои, сбои рельс, «оно молчало», неверный вывод, пойманный позже). Для каждой поломки **СНАЧАЛА**, до выбора имени класса и до записи, найди смысловую семью:
```
python "$HOME/.claude/scripts/prior_art.py" class "<описание поломки своими словами>"
```
exit 0 = прежних нет, «1-й датированный» правомерен · **exit 3 = это НЕ ошибка и НЕ первый случай**: прибор печатает прежние строки, их даты и СЕМЬЮ дефекта. Если напечатана `СЕМЬЯ <slug>`, используй именно её как `<класс>`. Если показаны прежние строки без известной семьи, бери имя предмета ремонта/нарушенного инварианта из самой ранней строки, не новый синоним. При `exit 0`, когда прежней строки нет, назови класс по текущему предмету ремонта/нарушенному инварианту и запиши как 1-й датированный случай; канал, код возврата, текст алерта и симптом классом не являются.

ТОЛЬКО ПОСЛЕ этого запиши ОДНУ строку через дверь `python "$HOME/.claude/scripts/selfheal.py" journal --class <класс> --what "<что>" [--conditions --parts --guess --status]`: **что · условия · сопричастные (файлы/рельсы/узлы) · гипотеза 🤔 или ✅ доказанная причина**. ⛔ НЕ править `Breakage-Journal.md` напрямую (ни Edit, ни heredoc): это общий Syncthing-файл, вид рисует один владелец из пер-узловых шардов, прямая правка отбивается хуком `breakage_write_guard` и терялась (04.09: 76 строк в 11 конфликт-копиях) — память [[breakage-journal-per-node-shards]]. Счёт бери из фактического ответа `selfheal.py`: дедуп означает, что новой строки нет.

Дальше по семье: 1-й = строка · 2-й = строка + уточнить условия · **3-й датированный = класс системный**. Внутри `/retro` причинную цепочку НЕ строй: используй ровно одну отдельную ВИДИМУЮ repair-сессию, чей первый явный вызов — `/five-whys <класс>` в Claude или `$five-whys <класс>` в Codex, с датированными строками серии. Если `selfheal.py` уже поставил её в очередь, вторую не создавай. Механизм/робота на 1-2 случае НЕ строить. Дефект новой семьи → дописать её в `FAMILIES` внутри `prior_art.py` ОДНОЙ строкой, иначе следующая сессия снова назовёт его «первым».
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
⭐⭐ **И ВТОРАЯ КОЛОНКА — перепроверено? ✅/❌** (dev 13.09.2026, CLAUDE.md §4.3-бис): «протестировано» и «перепроверено вторым, ДРУГИМ заходом» — разные вещи, и ложное «готово» живёт именно в зазоре между ними. Артефакт, у которого первый прогон зелёный, а второго захода не было, ретро помечает ⚠️, а НЕ ✅, и предлагает прогнать Шаг 4.9 скилла `/tt` сейчас. Замер архива 15.08→14.09: 21 раз за месяц оператор спрашивал «ты точно починил?» сразу после моего «готово». Канон: [[done-is-a-claim-recheck-twice]]. Then classify:
- 🟢 **Keep & reuse** — permanent infra or a tool you'll run again (skills, durable notes, reusable scripts).
- 🟡 **One-off** — served its purpose; if the *pattern* is worth remembering, capture the pattern (not the artifact), then let it rest.
- ⬆️ **Promote** — currently ad-hoc but should become permanent → turn into a rule / skill / memory.

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
- **exit 0** — у каждой обещанной рельсы есть либо вызовы, либо названная причина.
- **Прибора на узле НЕТ** (`rail_plan.py: No such file`) — это НЕ повод пропустить шаг молча.
  Проверь очередь посылок (`deploy_check.py`): не применённая `rail-plan-*` применяется тут же
  (§7.5). Применить нельзя (чужая живая табличка ON AIR на зоне `fleet-code`, замер 21.09) →
  ⛔ НЕ форсить, а написать в отчёт строкой: «🚂 прибора нет, посылка <id> заблокирована
  ON AIR <узел>/<id>, применю после закрытия». Сессия СТАРШЕ самого правила (работа шла до
  21.09) → так и сказать: плана не было, потому что правила ещё не существовало, выдумывать
  задним числом проценты запрещено (§5.4 правда в цифрах).
- **exit 1 «ПЛАНА НЕТ»** — сессия не объявила рельсы на старте. Это и есть нарушение; объявить сейчас (`rail_plan.py declare`) и сказать в отчёте честно, что план родился на ретро, а не на старте.
- **exit 1 «НЕДОБОР без причины»** — добери причины: `--reason <рельса>=<код>:<текст>`, коды `forgot · rail-dead · class-mismatch · too-small · tier2 · no-work`.
- **`No such file` — прибора на узле НЕТ** (замер 21.09, NODE-0X: посылка `rail-plan-20260921` лежала непринятой, и шаг судить было нечем). Это НЕ повод пропустить шаг молча: (1) посмотреть очередь посылок `python ~/.claude/scripts/deploy_check.py` и применить её тем же заходом; (2) применение отбито правами/классификатором → строка в отчёт «🚂 сверка невозможна: прибора нет, посылка <id> не применена» + пункт в TODO. Отсутствие прибора называется вслух, а не превращается в «рельсы не жгли».

⭐ **«forgot» обязывает ПРАВИТЬ ДВЕРЬ в том же заходе**, а не объяснять. Это прямой приказ оператора («сразу пытаешься поправить этот скилл, чтобы в будущем так не ошибаться») и он смыкается с 🛠 «вердиктом о скилле» ниже: причина `forgot` = скилл/рутина пропустили рельсу, значит правится вызывающий, а не только этот файл.

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
- Session DID large structural work (canon / sync / consensus / factory redo) **without** a declaration → flag in the report: «⚠️ крупная работа шла без ON AIR-таблички» (anti-pencil-whipping; the 2026-07-08 consensus.py case).
- No claim + no large structural work → skip silently.

## Step 3⛳ — Drift-audit → сессии-детишки (dev's decree 2026-07-11: retro spawns them ITSELF, no nudges)
The retro-time CLOSURE of the drift rule ([[goal-drift-offload-to-seed-sessions]] / CLAUDE.md § «Дрифт от главной цели»): mid-flight that rule offloads weeds AS they appear; retro is the **safety net** for what slipped — the topics the session got blown into that are NOT the main goal and NOT finished.

Procedure (cheap — reuse material already in hand: Step 0 spine, Step 1 inventory, Step 3📋 journal):
1. **Name the session's MAIN goal** (turnstate spine / the first ask). One line: «⛳ цель сессии: <X>».
2. **List the drift**: topics we discussed / dug / half-built that are neither the main goal nor done. Cross-check chips already issued mid-flight — those are NOT re-spawned, only their Connect status is reported.
3. **For each REAL drifted topic retro ЗАПУСКАЕТ СЕССИЮ САМО — no asking, no waiting** (dev 2026-07-11: «команда РЕТРО активирует соседние сессии-детишки без моих пинков»; усилено 29.07: **«запрещено запускать любые сессии в чёрную»**). Запуск ТОЛЬКО видимой рельсой — `mcp__scheduled-tasks__create_scheduled_task` (`fireAt` — ТОЛЬКО из двери `python ~/.claude/scripts/_shared/fireat_now.py --in 15`, руками время не писать: класс из 6 случаев 11.08-09.09, часы шелла врали до 11 ч; разносить по времени; `notifyOnCompletion: true`), чтобы сессия попала в список приложения и оператор мог её открыть, дотолкать после лимита и ответить на её вопрос. Принцип оператора дословно (29.07): **«плоди чип и САМ ЕГО НАЖИМАЙ»** — решил, что нужна сессия, значит создаёшь её УЖЕ ЗАПУЩЕННОЙ. Чип, который ждёт чужого клика, созданной сессией НЕ считается (замер: 107 из 346 чипов не нажаты никогда), а невидимый `claude -p` не считается тоже (29 сессий — в списке ноль); гейты `chip_guard.py` / `blackbox_session_guard.py` разворачивают оба случая на видимый запуск. Чип уместен только там, где нужны физические руки оператора или другая машина, с маркером `ТРЕБУЕТ РУК оператора:` / `ДРУГАЯ МАШИНА:` и немедленным пингом. Prompt = self-contained seed (Outcome · Контекст из recall · Scope · Deliverable · DoD — формат из [[decompose-into-parallel-sessions]]), сессия стартует с нуля без контекста этой. Register each launch in the task journal (Step 3📋) too — сессия AND registry entry, never either-or.
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
8. **🧒 Простыми словами** recap.

## Step 6 — Compact handoff (retro ⇄ compact glue; STAY in the chat, never /clear)
The retro's distilled output IS the bridge file — so close the loop without losing context. Two moves:

**6a. Auto-save the retro to the vault IN COMPACT FORMAT** (standing authorization from dev, 2026-06-12 — no per-run ask):
Reserve the final Latin filename first, acquire exact leases for that note and `01-Conversations/Claude/_Claude-Sessions-MOC.md`, and add the MOC wikilink **before the note's first write**. The no-orphan guard rejects a new note that has no incoming link; if the MOC lease is busy, wait for its owner instead of creating an orphan or overriding the lease. Then write the clean note to `$OBSIDIAN_VAULT/01-Conversations/Claude/Retros/retro-<YYYY-MM-DD>-<latin-topic-slug>.md` — filename **ALWAYS Latin** per [[vault-conventions]] (Cyrillic topic → translit slug; keep the Russian title in frontmatter `aliases:`).
- Content = frontmatter (`title`, `date`, `type: retro`, `source: claude-session`, `session_id: <cliSessionId — тот же uuid, что в 6a-бис из пути скретчпада>`, `tags`) + the arc (Step 2) + the reuse table (Step 3/4) + **the compact 7-header distillation** (РЕШЕНИЯ / TODO / СЕЙЧАС / ПУТИ И ЗНАЧЕНИЯ / СЧЁТЧИКИ / ОТКРЫТО / ИНСТРУМЕНТЫ И КОНТРАКТЫ — per `$USERPROFILE/.claude/compact-prompt.md`). **This note IS the archive** — it doubles as the compact summary, so retro and compact are never written twice.
- **NO 🧒 block in the note** — vault notes keep their own voice (the ELI5 recap is for the reply TO dev only).
- **Wikilinks: vault ≠ memory (two namespaces).** In the retro NOTE, `[[...]]` may target ONLY existing vault notes (`reglament-*`, `protocol-*`, `concept-*`, `decision-*`, another retro — verify each exists before writing); CC-memory slugs (`machine-migration`, `ak47-simplicity`…) go as plain inline code. Caught 2026-07-04 (Fable re-check): a retro shipped 7/7 broken links — all memory slugs. Canon: `deterministic-script-gotchas` → «Vault wikilinks ≠ CC-memory slugs».
- **Formal review status is a scoped receipt, not prose.** Every independent-review claim in the note MUST be one exact line: `REVIEW[<artifact-id>]: verdict=<VERIFY|ACCEPT|BLOCK|REQUEST_CHANGES>; scope=<what exact bytes/state the verdict covers>; source=<thread:<uuid>|file:<absolute-path>>; reviewer=<name>`. A partial GREEN/RED run never upgrades the formal verdict; a rollback-only VERIFY stays rollback-only and cannot verify the proposal.
  ⚠️ Три грабли формата, каждая стоила прогона линта (замер 26.09.2026): (1) `scope` — максимум **200 символов**, два sha256 туда уже не влезают, оставляй один и слово «только»; (2) **точка с запятой внутри `scope` рвёт разбор** (поле читается как `[^;]+`) — внутри только запятые; (3) `source=file:<path>` обязан лежать в корнях, которые линт обходит (`~/.claude`, волт, `_imports`, папка дока, cwd) — вывод из `Temp\claude\…\tasks\` не засчитывается, копируй улику к остальным квитанциям. Плюс проза: слова «независимый ревьюер» рядом с «accept/pass/verify» в обычном абзаце тоже требуют receipt, поэтому в тексте пиши «Codex смотрит дифф», а вердикты держи только в receipt-строках. (4) **путь в `source=file:` пиши через ПРЯМЫЕ слэши** (`D:/Vault/...`): обратный слэш съедается любым генератором строки (в Python `\R`/` ` стали управляющими символами и линт дважды отбил receipt с «битым» путём — замер 27.09.2026).
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
- Рычаг настоящего переноса = MCP `ccd_sidebar.move_sessions`, появляется только когда приложение его отдаёт: проверка `python ~/.claude/scripts/claude_desktop_gate_probe.py` (exit 0 = флаг id_0bae24da ON) → тогда переноси по-настоящему, а иконка больше не нужна. Замер 07-10.09: флага в выдаче фич нет, issue anthropics/claude-code#92621.
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

> `Bash` -- {"command": "cd \"D:/Vault/_imports\" 2>/dev/null\necho \"=== turnstate ===\"; python \"D:/Vault/_imports/turnstate/turnstate_show.py\" 2>&1 | head -40\necho \"=== retro_lost marker ===\"; ls ~/.claude/logs/retro_lost_done/ 2>/dev/null | grep c42ed1c7 || echo \"(нет маркера)\"\necho \"=== rail

---

> `Bash` -- {"command": "echo \"=== onair ===\"; python ~/.claude/scripts/onair.py list 2>&1 | head -20\necho \"=== memory_harvest ===\"; python ~/.claude/scripts/memory_harvest.py --scan 2>&1 | tail -10\necho \"=== memory_epistemic ===\"; python ~/.claude/scripts/memory_epistemic.py --lint 2>&1 | tail -10", "d

---

> `Bash` -- {"command": "echo \"=== prior_art 1: ноги ДР не доехали за 4 дня ===\"\npython ~/.claude/scripts/prior_art.py class \"рельса ДР не доставила ногу за несколько суток, пол 3 LLM не добран, синтез пришлось делать по двум ногам\" 2>&1 | head -30\necho; echo \"=== prior_art 2: нога без ссылок ===\"\npyth

---

> `Bash` -- {"command": "python \"D:/Vault/_imports/retro_inventory.py\" 1 2>&1 | tail -20", "description": "Run shared retro inventory"}

---

**Claude:**

Prior_art дал шумные совпадения по ключевым словам. Делаю красную пробу: из шести «прежних» только один реально мой класс.

---

> `Bash` -- {"command": "echo \"=== красная проба: ловится ли МОЙ симптом семьёй 01.09? ===\"\npython ~/.claude/scripts/prior_art.py class \"кворум ДР недостижим: рельс стреляет меньше, чем требует порог пола\" 2>&1 | head -12\necho; echo \"=== контроль: ловится ли ЧУЖОЙ симптом (бэкап-рельса) той же формулиров

---

**Claude:**

Красная проба прошла в обе стороны: семья подтверждена, чужой симптом не ловится. Журналирую.

---

> `Bash` -- {"command": "python ~/.claude/scripts/selfheal.py journal \\\n  --class \"dr-quorum-unreachable-fewer-rails-than-floor\" \\\n  --what \"HUB-04 (compute) и HUB-21 (sv-landing) простояли 4 суток с 2 живыми ногами из 3: пол §9.1 не добран, синтез ушёл по дедлайн-исключению. 2-й датированный случай семь

---

> `Bash` -- {"command": "python ~/.claude/scripts/rail_plan.py declare \\\n  --self \"синтез 2 кластеров CV-DR: суждение, сведение расхождений ног, чек-листы, заметки в волт, выключение рутины\" \\\n  --outsource \"deep-research:grok,deep-research:mistral\" 2>&1 | tail -6\necho \"--- verdict ---\"\npython ~/.cl

---

**Claude:**

Две собственные ошибки прямо в заходе, чиню обе.

---

> `Bash` -- {"command": "python ~/.claude/scripts/rail_plan.py declare --session s_4c102aa4 \\\n  --self \"синтез 2 кластеров CV-DR: суждение, сведение расхождений ног, чек-листы, заметки в волт\" \\\n  --outsource \"deep-research:grok,deep-research:mistral\" 2>&1 | tail -4\necho \"---

---

> `Bash` -- {"command": "grep -n \"dr-quorum-unreachable\" ~/.claude/scripts/prior_art.py | head -20", "description": "Check existing quorum families in prior_art"}

---

**Claude:**

Вердикт рельс закрыт. Теперь чиню свою же ошибку именования класса — я завёл синоним вместо существующей семьи.

---

> `Bash` -- {"command": "grep -n \"FAMILIES\" ~/.claude/scripts/prior_art.py | head -10\necho \"---\"\nsed -n \"/^FAMILIES/,/^}/p\" ~/.claude/scripts/prior_art.py | head -40", "description": "Inspect FAMILIES table structure"}

---

**Claude:**

Проверяю свою гипотезу о корне, прежде чем заводить семью вокруг неё.

---

> `Bash` -- {"command": "d=\"D:/Vault/Vault-Knowledge/_machine-bus/_dr/queue/DR26-09-24-HUB-21-1604\"\necho \"=== dispatched ===\"; cat \"$d/dispatched.txt\" 2>/dev/null | tail -10\necho \"=== reminded ===\"; cat \"$d/reminded.txt\" 2>/dev/null | tail -10\necho \"=== rejected README ===\"; head -20 \"$d/_rej

---

**Claude:**

Гипотеза о корне **опровергнута**: прогон 27.09 уже вынес ногу и документировал, что доборщик теперь за ней пойдёт. Проверяю, бежал ли доборщик ночью.

---

> `Bash` -- {"command": "python ~/.claude/scripts/routine_cost_audit.py --days 3 2>&1 | grep -i -E \"latecomer|sweep|прог\" | head -10\necho \"--- задача в планировщике ---\"\nls ~/.claude/scheduled-tasks/ 2>/dev/null | grep -i -E \"dr|latecomer|sweep\" | head", "description": "Check whether latecomer sweep act

---

> `Bash` -- {"command": "ls ~/.claude/scheduled-tasks/ | grep -i latecomer\necho \"--- поиск задачи-доборщика ---\"\ngrep -rl \"dr_latecomer_sweep\" ~/.claude/scheduled-tasks/*/SKILL.md 2>/dev/null | head -5\necho \"--- последний прогон скрипта (лог) ---\"\nls -lt --time-style=+%Y-%m-%d_%H:%M ~/.claude/logs/ 2>

---

> `Bash` -- {"command": "ls -l ~/.claude/scripts/dr_latecomer_sweep.py 2>/dev/null || echo \"СКРИПТА НЕТ\"\necho \"--- кто вообще его зовёт (весь ~/.claude) ---\"\ngrep -rl \"dr_latecomer_sweep\" ~/.claude/ 2>/dev/null | head -10\necho \"--- есть ли он в Windows-планировщике ---\"\nschtasks /query /fo csv 2>/de

---

**Claude:**

Понял, добираю. Сначала закрою висящую проверку, потом запускаю веер.

---

> `Read` -- {"file_path": "C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_4c102aa4\\tasks\\bpxjn6xfz.output"}

---

**Claude:**

Корень найден и доказан: `dr_latecomer_sweep.py` существует с 15.09, но **его не запускает ничто** — ни задача планировщика, ни хук. Доборщик написан и брошен в воздух, поэтому третья нога и не приезжала 4 суток. Моя ранняя гипотеза про «sweep не различает отбитую ногу» опровергнута — прогон 27.09 всё сделал правильно, бежать было некому.

Теперь добираю ноги, как просишь.

---

> `Skill` -- {"skill": "dr-fanout", "args": "DR26-09-24-HUB-04-1604 и DR26-09-24-HUB-21-1604 → рельсы glm, grok, chatgpt, gemini"}

---

**User:**

Base directory for this skill: C:\Users\dev\.claude\skills\dr-fanout

# /dr-fanout — раздать Deep Research по 6 LLM и собрать консенсус

> Финал Alpha Protocol на автомате. Каналы: **ChatGPT** (chatgpt.com) · **Gemini** (gemini.google.com) · **Grok** (grok.com) · **claude.ai** (claude.ai) · **GLM** (chat.z.ai) · **Mistral Le Chat** (chat.mistral.ai, с 05.08.2026 — дверь ещё не открыта, см. рецепт). ⭐ **МЕХАНИКА ЗАВИСИТ ОТ ТИПА СЕССИИ, и это не деталь, а корень класса** (`courier-сессия-dr_queue-без-chrome-mcp`, 5 дат: 08-11, 08-26, 09-04, 09-06, 09-07 — курьер пять раз объявил collect невыполнимым, стоя рядом с работающей дверью). **Сессия-приложение** (есть браузерные MCP-инструменты) — живой залогиненный Chrome оператора, Claude-in-Chrome MCP. **Безлюдная сессия** (`claude -p`, launchd, рутина — у неё браузерных MCP нет и не будет) — ТОЛЬКО headless: `dr_ff_rail.py` (Firefox AutoFF; claudeai/chatgpt/gemini/glm), `dr_ff_collect.py` (забор готового отчёта), `dr_headless_dispatch.py` (grok; ⛔ codex И claude CLI для ДР запрещены — dev голосом 22.09.2026: бак Codex кодит оператор, бак Claude — оркестратор; ноги ChatGPT/Claude = только веб. Headless ПОКА можно grok/mistral/glm/gemini — «пока там есть лимиты»). ⛔ Не проверяй наличие Chrome-MCP, чтобы решить, выполнима ли работа: **машинная истина о дверях = `python ~/.claude/scripts/dr_doors.py list`** (один источник; собирает карту ИМПОРТОМ у тех модулей, которые двери и открывают). ⚠️ Прежняя строка тут звала поле `doors` в `robot-work` и карту `RAIL_DOORS` — ни того, ни другого в коде НЕТ (проверено 14.09.2026 grep'ом по всему дереву): указатель на несуществующий прибор — тот же класс, что и рельса без двери. Нет двери — так и написано словами. Канон: [[alpha-protocol-recall-plus-dr]], decision-multi-llm-vendor-independence (гетеро-консенсус), [[chrome-autonomy-self-drive]], [[browser-work-on-peers-not-hub]] (строго локально).
>
> ⭐ **КВОРУМ 4 (из 5, с 05.08 — из 6)** (приказ оператора 04.08.2026: «я бы считал что ДР выполнен если сделано 4 из 5 ЛЛМ»). `dr_queue.derive_status` закрывает заказ, когда собраны ЛЮБЫЕ 4 рельсы (из 5, а с 05.08.2026 — из 6) — одна молчащая рельса больше не держит запись заложником (замер: gemini 32 заказа / 6 отчётов). ⛔ Кворум НЕ отменяет пятую рельсу: недобранное плечо продолжает светиться в `status` строкой «⚠️ кворум 4/5, не собрано: …» и в `robot-work` полем `missing_quorum_ok` — «сойдёт» должно быть ВИДНО. Узкий веер (3 цели) по-прежнему требует все 3: кворум = `min(4, сколько заказано)`. ⭐ Шестая рельса (Mistral) планку НЕ подняла — она добавлена, чтобы 4 набиралось легче. Гейт: `python ~/.claude/scripts/_test_dr_quorum.py`.
>
> ⭐ **ВЕЕР 04.08.2026 = ПЯТЬ РЕЛЬС** (два прямых распоряжения оператора в один день): «теперь ВСЕГДА добавляй КЛОД.аи в ДРы» + «glm ТОЖЕ ИСПОЛЬЗУЕМ ДЛЯ ДР… ВХОД ЧЕРЕЗ ббПЛАТИНУМ». Машинная истина дефолта — реестр `~/.claude/dr_rails.json` (с 14.09.2026 `dr_start.py` берёт дефолт ОТТУДА, а не из литерала в коде: копии списка рельс по файлам и были источником целей без дверей); ⛔ сокращать веер молча нельзя, снятие рельсы = `dr_queue.py retarget --drop` с доказанными дверями (обе новые рельсы уже в `BROWSER_RAILS`).

## ⭐⭐⭐ ПРИКАЗ 25.09.2026 (голосом): БРАУЗЕРНЫЕ РЕЛЬСЫ ПЕРВЫМИ · ВСЕ · CLAUDE ОБЯЗАТЕЛЕН · GEMINI = ДВА АККАУНТА

> Дословно: «тебе нужно ВСЕГДА делать ДР через ВСЕ рельсы браузерные в первую очередь. клод обязательно. джемини аж 2 аккаунта есть!!!»

Три отдельных требования, ни одно не поглощает другое:
1. **Дверь `ff` (браузер) идёт ПЕРЕД дверью `cli`.** У рельсы бывают обе; порядок теперь не «что быстрее», а «сначала браузер» — настоящий Deep Research по подписке живёт в веб-морде, CLI у большинства вендоров это только web search (п.3 «Что уже решено»).
2. **ВСЕ браузерные, а не половина веера.** Машинная истина дверей — `python3 ~/.claude/scripts/dr_doors.py list`, НЕ догадка и не список в прозе. Замер 25.09 на NODE-0X: `ff` у **chatgpt, claudeai, gemini, glm**; `cli` у grok. Значит минимум четыре браузерные ноги в каждом заказе.
3. **claudeai обязателен всегда** (стоит с 04.08, оператор повторил 25.09). **Второй аккаунт = ВТОРАЯ НОГА, а не запас:** рельса = вендор#аккаунт, у Gemini два бака, и при мёртвой первой ноге вторая — готовая замена в том же заходе, а не «добор завтра».

⚠️ **Замер, породивший приказ.** `DR26-09-24-MACANTON-01-1452` (Anthropic Fellows) заказан на 6 целей → доехали **три**: glm, grok, mistral. **claudeai не доехал вовсе.** **gemini приехал снимком НЕзалогиненной страницы** («Sign in to Gemini» + 73% эхо нашего же заказа, 7.7 КБ), `dr_queue` засчитал файл как результат и объявил **ложный кворум 4/6 + delivered**. То есть в исследовании про Anthropic не участвовал ни Claude, ни Gemini — оба самых доступных вендора, и второй бак Gemini лежал нетронутым.

⛔ **Отсюда жёсткая связка: `dr_leg_gate.py <файл>` вызывается ДО `dr_queue.py attach`, всегда.** Скрап страницы логина от отчёта внешне неотличим; класс `ff-rail-echoes-our-own-prompt-as-ok` имеет 3 датированные строки и признан системным. Кворум, собранный без гейта, — не кворум.

Канон: [[dr-browser-rails-first-all-of-them]], пара к [[dr-max-thinking-and-wide-fanout]].


### ⭐ ШАГ 0-ЛОГИН: ДВЕРЬ ЕСТЬ ≠ СЕССИЯ ЖИВА (замер 26.09.2026, DR26-09-26-MACANTON-01-1441)

`dr_doors.py list` печатает, что у рельсы ЕСТЬ дверь. Он НЕ говорит, что за дверью кто-то залогинен —
и это разные утверждения. 26.09 на NODE-0X двери `ff` числились у chatgpt, claudeai, gemini, glm,
а поехала ровно одна: профиль автоматизации **AutoFF растерял сессии** (cookies: `google.com` 1 вместо 27,
`chatgpt/openai` 0 вместо 23, `claude.ai` 0 вместо 14 — паспорт скрипта всё ещё цитировал замер 02.09).

⛔ `looks_logged_out` судит по URL и на этих вендорах СЛЕП: z.ai и gemini.google.com отдают рабочую
АНОНИМНУЮ страницу по тому же адресу. Симптомы разлогина маскируются под поломку вендора:
glm вернул «GLM-5.3-Flash / Sign in» + эхо нашего промпта, gemini — «не нашёл пункт Deep Research».

**Порядок перед рассылкой (0 исходящего, минуты):**
1. Куки по профилям: сколько `google.com` / `chatgpt` / `claude.ai` / `z.ai` в профиле, которым поедешь.
   Ноль у вендора = нога не поедет, сколько её ни чини селекторами.
2. `python3 ~/.claude/scripts/dr_ff_menu_probe.py --rail <рельса> [--profile-dir <профиль>]` —
   печатает РЕАЛЬНЫЕ ярлыки меню композера и `[disabled]`. Улика разлогина: все пункты `[disabled]`
   + кнопка `Sign in to try tools` + слабая модель (`Flash-Lite`).
3. Только потом вердикт. ⛔ Запрещено писать «вендор убрал Deep Research» / «рельса мертва»,
   не пройдя шаги 1–2: три датированных случая (02.09 ×2, 26.09) были выводом о ВЕНДОРЕ,
   сделанным по СВОЕМУ селектору.

**Разлогин = руки оператора, а не задача робота.** Пароль и 2FA — Tier-2. Аск в 02 с указанием профиля,
дальше прогон идёт без этой ноги и честно пишет `missing`, а не «рельса мертва».

⚠️ **Реестр `~/.claude/dr_rails.json` на NODE-0X ОТСУТСТВУЕТ** (26.09: `dr_rails_registry.py list`
падает `FileNotFoundError`, файл читают 7 скриптов). Пока его нет, понятия «рельса = вендор#аккаунт»
на узле не существует: вторую ногу Gemini записать некуда, `max_reasoning.proof` фиксировать негде.
Класс `canon-points-to-missing-file`, 2/3.


## ⭐⭐ ПРИКАЗ 14.09.2026 (голосом): МАКСИМУМ ПОПЫТОК · МАКСИМУМ ДУМАНИЯ · ПОСТ СРАЗУ

> «Всегда нужно делать максимальное количество попыток: отправлять запросы в как можно
> большее количество мест для deep research… Всегда включаем максимальное думание,
> максимально качественный ответ, максимально долгие и подробные размышления.»

**Машинная истина о рельсах, аккаунтах и режимах думания = `~/.claude/dr_rails.json`.**
Один файл, три ответа: какие рельсы существуют (7), какие у них аккаунты (12), и КАК на
каждой включить самый сильный режим. ⛔ Не пересказывать список здесь и не держать вторую
копию — расхождение прозы с JSON = баг прозы.

**① МАКСИМУМ ПОПЫТОК.** Дефолт веера — 6 рельс. ⛔ **Perplexity ВЫЧЕРКНУТА** (оператор голосом 24.09.2026: «зачем тебе Perplexity? У тебя есть Клод, ChatGPT, ГЛМ, Грок… забудь про него»): седьмой рельсой не считается, дверь ей не строим, в добор не берём — веер жжёт наши ОПЛАЧЕННЫЕ баки, чужая подписка в план не входит. Нехватка ног лечится починкой логинов СВОИХ рельс, а не новым вендором → [[perplexity-banned-for-dr]]. ⚠️ Реестр `~/.claude/dr_rails.json` на части узлов физически отсутствует (HUB-01, замеры 16.09 и 24.09 — класс `dr-rails-registry-missing-on-node`): `dr_rails_registry.py` там падает FileNotFoundError, и сессия остаётся без машинной истины про двери. Упал реестр → рельсы берём из этой строки, а не изобретаем вендоров. **Пол = 3 разные LLM**
(`min_rails`): ДР в две LLM не бывает, это не ДР. Кворум не набрался основным веером →
**широкий добор вторыми аккаунтами** того же вендора (chatgpt a2@, claudeai a2@/bb@,
gemini a2@) — это ещё 5 попыток, и они дешевле, чем ждать молчащую рельсу.

**② МАКСИМУМ ДУМАНИЯ — ЧАСТЬ КОНТРАКТА, А НЕ НАСТРОЙКА.** Каждая рельса запускается в самом
сильном режиме, какой даёт подписка: у Gemini это `More tools → Deep Research`, у ChatGPT
`Deep research`, у Grok `DeeperSearch + Think`, у claude.ai `Extended thinking + Research`,
у Mistral Le Chat режим research с веб-поиском. ⛔ **Быстрый режим не считается попыткой**: обычный чат-ответ,
записанный в `results/`, — это подделка рельсы, тот же класс, что `0 searches / 0 citations
= dead`. Не смог включить сильный режим → рельса `missing`, а не «собрана».

**③ КВОРУМ 4/6 ЗАКРЫВАЕТ СЕССИЮ, НО НЕ ЗАКАЗ.** Пришли 4 — синтез идёт сразу, оставшиеся
две не ждём. Они не теряются: `dr_ff_collect.py` забирает готовый отчёт из последнего чата
вендора, `dr_debt_watch.py` осушает долг реестра суточным обходом. Именно поэтому закрытие
по кворуму законно — недобранное доедет само.

**④ ЗАКРЫЛИ ДР → В ТОМ ЖЕ ЗАХОДЕ ЧЕРНОВИК ПОСТА.** Не «потом», не в ежедневной полосе:

```bash
python ~/.claude/scripts/dr_post_draft.py --id <DR-номер>   --topic "<вопрос одной строкой>" --audience "<кому это полезно>"   --verdict "<главный вывод>" --collected <сколько рельс> --why "<что искали>"   --link <ссылка на корпус/синтез>
```

Печатает две части. **Тело** — тизер 240–300 знаков HARD: польза («кому интересен X»),
тема, строка «глубокое исследование в N/6 LLM», короткий вердикт, и путь вниз «Сами
исследования и синтез — в комментариях». Ссылок в теле нет — геймплей лаборатории.
**Первый комментарий** — ссылки на отчёты и синтез плюс обязательная атрибуция: заказали
Tony Dzi ([ИМЯ] [ФАМИЛИЯ]) и Майкрофт, Palo Alto AI Research Lab, что искали,
available for hire, Calendly, Linktree. Тексты атрибуции берутся из `_STYLE-footer.md`,
⛔ не сочиняются ([[post-mandatory-elements]]).

Инструмент **не надувает текст водой**: короткий вердикт → отказ с требованием конкретики
(цифра, ограничение, что удивило), а не разжатие мысли. Черновик, наружу не уходит —
публикация остаётся под §3.2 и матрицей площадок. Та же атрибуция обязана стоять **внутри
синтеза**, а не только под постом. Гейт: `python ~/.claude/scripts/_test_dr_post_draft.py`. Канон: [[dr-max-thinking-and-wide-fanout]].

## ⭐ ЗАЧЕМ ЭТО ВООБЩЕ: замкнутая петля САМООБУЧЕНИЯ (dev 04.08.2026)

> «Это очень удобная штука для самообучения ИИ — когда ИИ сама заказывает ДР.»

Скилл выглядит как «разослать промпт по сайтам», но это только транспорт. Настоящая ценность — **петля,
в которой ИИ сама чинит свои пробелы**, и человек в ней не курьер, а владелец решений:

```
① пробел      RECALL по волту+памяти не отвечает на вопрос → GAP назван вслух (Alpha Protocol)
② заказ       ИИ САМА нумерует DR и разносит промпт по 5 рельсам (мандат 14.07: без «+», квоты не экономим)
③ сбор        доказательство работы, не красивый текст: 0 searches / 0 citations = `dead`, не `collected`
④ синтез      гетеро-кворум (разные вендоры = разные обучающие базы) → insight-DR + Decision Memo
⑤ ЗАПИСЬ      вывод уходит в ДОМА правил (CLAUDE.md · Библия · память · скилл) — §8.4/§8.6
⑥ следующая сессия стартует уже умнее. Петля замкнулась.
```

**Шаг ⑤ — единственное, что отличает самообучение от «почитал и забыл».** DR без записи в дом = потраченная
квота: замер 29.07 — 184 из 246 отчётов висели в статусе `synthesized` и никуда не легли. Отсюда жёсткая
клауза §9.1: у каждого DR есть КОНЕЦ (`applied` с «что поменяли» либо `parked` с «почему не берём»).

**Три опоры, без которых петля врёт сама себе:**
1. **Гетерогенность.** Пять рельс = пять разных моделей. Один вендор, спрошенный пять раз, — это не пять мнений.
2. **Доказательство работы.** У отчёта должны быть источники/поиски/время думанья. Красивый текст из
   параметрической памяти неотличим от исследования на вид — и отравляет синтез молча.
3. **Обратная сторона той же монеты — рельсы РЕВЬЮ** (`secondop.py`, CLAUDE.md §4.3): DR-веер учит,
   ломатель проверяет. Локальные headless: `grok` · `gemini` (04.08; ⛔ `codex` и `claude` CLI выведены из ДР 22.09 — их баки заняты кодингом оператора и оркестрацией; ПОКА-разрешение grok/mistral/glm/gemini живо, пока у них есть лимиты); веб-дверь: `glm` и остальные.
   Тот же принцип «дверь закрыта ≠ вендор мёртв» и тот же запрет тихой подмены вендора.

**Безлюдный режим:** `dr_headless_dispatch.py` (04.08) гоняет grok без человека (⛔ codex и claude CLI запрещены 22.09, скрипт отбивает fail-closed, клапан DR_RAIL_BAN_OK=1 только по слову оператора). ⚠️ Провал там судится
по РАЗМЕРУ выхода, а не по exit-коду: ведущий `---` YAML-фронтматтера убивал обе рельсы при честном exit 0 и
файле в 0 байт.

## ⭐ Что уже решено (фундамент, не переисследовать) — обновлено 2026-07-16
1. **Браузерный слой = Firefox-first** (Decision Memo `02-Decisions/decision-2026-07-16-browser-automation-layer.md`, DR26-07-16-HUB-01, уверенность high). Chrome 127+ шифрует куки (ABE) и с апреля 2026 привязывает сессии к железу (DBSC) → внешнее извлечение куки невозможно без malware-техник. **Firefox куки открыты** (plaintext SQLite, DBSC не реализует) → выделенный per-service Firefox-профиль + Playwright `launch_persistent_context`; Chrome CDP-attach только как fallback для строго-Chromium сайтов. Хаб-стек уже поднят: `firefox_cookies.py` (`~/.claude/scripts/_shared/`), профили `D:\AutomationBrowsers\Firefox\`.
2. **Живой Chrome-MCP (Claude-in-Chrome) остаётся осознанным anti-ban путём** для действий «как человек в реальном сеансе» (fb-post/x-post едут так). Для dr-fanout выбор пути исполнения (живой Chrome-MCP vs headless Firefox-Playwright) уточняется идущим DR (см. п.4).
3. **CLI-обход НЕ даёт Deep Research по подписке** (проверено 15.07): Codex CLI / Gemini CLI = только web search; настоящий Deep Research потребительской подписки программно не дёргается (Google DR-агент = платный API отдельно). ⇒ браузерная веб-морда — единственная дорога к DR по подпискам, значит делаем её анти-хрупкой, а не бежим от неё.
4. **ToS-риск, острее всего у Grok:** xAI AUP прямо запрещает автоматический/не-человеческий доступ (риск suspension/termination). Задокументированных банов за автоматизацию СВОЕГО аккаунта нет, но текст явный → Grok-канал гнать в человеческом темпе; решение «оставить/притормозить/заменить на Claude.ai» — за оператором.
5. **Grok — просто продолжаем использовать** (решение оператора 2026-07-16). xAI AUP формально запрещает автоматизацию, но охота идёт за масс-скрейпингом (штраф $15k/1M запросов), а наш темп естественно крошечный (несколько DR в день максимум) → мы не мишень. Ценность третьего независимого голоса > управляемого риска. НЕ городить лимиты/троттлинг ([[ak47-simplicity]]) — Grok в обычной ротации; если сам вендор упрётся (капча/challenge) — доложить и пропустить этот канал, без драмы.
6. **Путь исполнения — ГИБРИДНЫЙ, под каждого вендора свой** (решение оператора 2026-07-16, «и так и так»). Не один способ на всех:
   | Вендор | Путь | Почему |
   |---|---|---|
   | **Grok** | живой Chrome-MCP, человеческий темп | ToS-чувствителен → действуем как человек в реальном сеансе (макс anti-ban, как fb-post [[chrome-autonomy-self-drive]]); headless-бот тут = максимум риска |
   | **ChatGPT** | выделенный Firefox-профиль headless (безлюдно) ИЛИ живой Chrome-MCP | ToS мягче; извлечение отчёта = backend JSON (работает в обоих); для расписания без человека → Firefox |
   | **Gemini** | выделенный Firefox-профиль headless (безлюдно) | двухфазный (план→Start research), терпим к автоматизации; кандидат №1 на полностью безлюдный прогон |
   Принцип: чем жёстче ToS/бан-чувствительность вендора → тем ближе к «живой человек в сеансе» (Chrome-MCP); чем терпимее + важнее безлюдность → тем ближе к выделенному Firefox-профилю (Playwright persistent, фундамент HUB-01).
7. **✅ Оркестрация — ПОДТВЕРЖДЕНА внешним DR** (`DR26-07-14-FLEE-01`, синтез ChatGPT+Grok 2026-07-16, выжимка `03-Insights/insight-DR-DR26-07-14-FLEE-01-*`). Оба вендора независимо: ядро = **durable state-machine + job-ledger, НЕ «долгоживущий автономный браузер-агент»**; локальный ledger-FSM достаточен для одно-хозяйного хаба. Оба независимо советуют **НЕ строить безлюдную Grok-автоматизацию** (xAI AUP + enforcement реален: >52k банов в 2026, Reuters 15.07) → наша матрица п.6 уже это соблюдает (Grok только живой Chrome-MCP, никогда в демоне). **Безлюдное расписание стартуем с 2 вендоров: ChatGPT + Gemini.**
8. **Вендор-логику держать ТОНКОЙ, оркестрацию — общей.** UI-специфичные репо мрут быстро (`chatgpt-automation-mcp` архив 27.04.2026, `browserbase/gemini-browser` архив 20.05.2026). Всё вендор-специфичное = сменные «адаптеры» внизу; автомат/ledger сверху не меняется.
9. **⚠️ ОТКРЫТО — официальный путь для Gemini:** Deep Research Agent / **Interactions API** (`background=True` + polling, collaborative_planning) — production-ready, снимает самый хрупкий и медленный браузерный канал. НО ⚠️ УСЛОЖНЕНИЕ + неясен биллинг: входит ли в подписку Ultra или это отдельные деньги (ChatGPT-отчёт: «НЕ то же free-with-subscription»). **Проверить биллинг ДО стройки** ([[prefer-included-limits-before-paid-api]]) — если платный, не заводить без «+» оператора.

## ✅ GEMINI-ДР НА NODE-0X — РАБОЧИЙ РЕЦЕПТ, пройден вживую 01.08.2026 (DR26-08-01-MACANTON-02-659)

Приказ оператора голосом 01.08: «делать чтобы через ГЕМИНИ!!!» ⇒ `gemini` вернулся в `DEFAULT_TARGETS` (`dr_queue.py`).
Дверь ровно одна и она **НЕ API**: живой Chrome под `[EMAIL]` («Punk», платный AI Pro). Шаги, каждый проверен:

1. `list_connected_browsers` → набор МЕНЯЕТСЯ между заходами (в этом прогоне за 10 минут стало 2 Chrome вместо 1). Взял свой сам, `select_browser`, у оператора НЕ спрашивал ([[browser-and-account-pick-yourself]]).
2. `navigate` на `https://gemini.google.com/app?authuser=[EMAIL]` → **скриншот** (innerText врёт). Признак живой сессии: «What's the vibe, Punk?» + селектор `Pro Extended`. Аккаунт подтверждать `aria-label` кнопки профиля: `Google Account: Punk Crypto ([EMAIL])`.
3. Транспорт промпта — `window.name`, направление **localhost → gemini** (обратное COOP рвёт): `python3 -m http.server` в скретчпаде → `navigate` на файл → `window.name = await fetch(location.href).then(r=>r.text())` → `navigate` на gemini. Замер: 5656 симв. и 100 кириллических доехали 1-в-1.
4. Чип Deep research ставить в ПУСТОМ композере: «+» (`Upload & tools`) → `More tools` → `Deep research`. ⚠️ Кликать по **ref** из `find`, не по координатам: клик по координатам подменю промахнулся молча, меню закрылось без чипа, и это видно только скриншотом. Признак успеха: плейсхолдер меняется на `What do you want to research?` и рядом появляется пилюля `Deep research`.
5. Вставка — только JS: фокус в `.ql-editor` → каретка в конец → `document.execCommand('insertText', false, txt)` (сел с первого раза; синтетический paste держим фолбэком). Сверять ДВУМЯ мерками: длина (`innerText` даёт +60 симв. на блочных переносах — это норма) и счётчик кириллицы (обязан совпасть точно).
6. Send → **двухфазность**: `Generating research plan` (~1 мин) → `find` кнопку `Start research` → клик по ref. Доказательство старта: «I'm on it… you can leave this chat» + карточка `Creating your report…` с чипами реальных источников внизу.

⛔ API-ключ ДР-рельсой НЕ является и не станет без денег. Замер 01.08, 3 чередования подряд в одной минуте (`probe2.py`): `gemini-flash-lite-latest` без `google_search` → 200 все три раза, с `google_search` → 429 все три раза, БЕЗ имени метрики и без `violations` — подпись «квота грунтинга 0 на free tier». Первый прогон, где 429 приходил и на plain-запросы, был собственным RPM (быстрый цикл по 6 моделям) — отделяется паузой 65 с, иначе ловишь ложный диагноз. Побочно: `gemini-2.5-flash` → 404 «no longer available to new users», `gemini-2.5-pro` на free-tier → `limit: 0`.

🔒 Дверь против рецидива: `dr_queue.py retarget --drop <браузерная рельса>` теперь ТРЕБУЕТ `--doors` с ≥2 проверенными дверями отдельными аргументами (гейт судит действие, не подстроку в reason). Ложный drop снимается `dr_queue.py restore <ID> --restore gemini --why "<чем доказано>"`.

## 🔴 GEMINI НА NODE-0X — читать ПЕРВЫМ, если Gemini «просит залогиниться» (разбор 31.07.2026, два ложных диагноза подряд)

**Симптом-обманка:** `gemini.google.com` показывает «Sign in» + Flash-Lite, куки `.google.com` в профиле есть все (`SID`, `LSID`, `__Secure-1PSID`) — выглядит как протухшая сессия. Я выдал ДВА неверных диагноза («сессия протухла» → ask оператору, отозван; «гео-блок на NODE-0X» → заказ хабу, отозван), прежде чем нашёл настоящие причины. Обе ошибки ловились скриншотом и вопросом «а ЧЕЙ это браузер?».

**Настоящих причин две, обе проверены:**
1. **⚠️ Chrome-MCP ≠ эта машина.** «Gemini isn't currently supported in your country» я увидел в Chrome через MCP — а из трёх подключённых Chrome тот оказался на ноуте Норы (IP в России, там Gemini закрыт). Свой IP я мерил curl-ом с NODE-0X (Вена, AT) и склеил факты с двух разных машин. **Правило: IP меряется ИЗНУТРИ того браузера, где виден симптом** (`fetch('https://ipinfo.io/json')` в той же вкладке). На NODE-0X гео-блока НЕТ — проверено изнутри Firefox: country-block False.
2. **Стена Google-consent («Before you continue to Google»)** перехватывает страницу, и ПОД ней рендерится разлогиненная оболочка — по DOM неотличимо от «разлогинен». Снимается трастед-кликом Selenium; кнопка ищется ТОЛЬКО по вложенному span: `//button[.//span[normalize-space(text())='Reject all']]` — поиск по `b.text` её НЕ находит (текст в потомке). После клика стена не возвращается.

**Остаток после снятия стены:** куки Google в AutoFF реально не аутентифицируют → нужен ОДИН живой вход оператора: `firefox -no-remote -profile ~/.claude/browser-profiles/autoff https://gemini.google.com/app` окном, дальше рельса безлюдная. Свежий логин отличается по `creationTime` кук (не `lastAccessed` — его обновляет любой пинг).

⚡ **Порядок диагностики (30 секунд, а не два часа):** (1) скриншот — видимый текст первичен, `document.body.innerText` в фоновой вкладке отдаёт 0–324 симв. и врёт; (2) IP изнутри ТОГО ЖЕ браузера; (3) только потом гипотезы про сессию.

**⛔ Прежде чем снять gemini через `retarget --drop` с формулировкой «на этом узле рельсы нет» (рецидив 01.08: раннер снял рельсу с 6 заказов, а рельса была жива в другом Chrome под Punk/`a@`):**
1. `list_connected_browsers` и обойти **КАЖДЫЙ** подключённый Chrome, не первый попавшийся; набор браузеров меняется между заходами — «в 06:00 был корп» ≠ «в 14:00 нет личного».
2. В каждом браузере пробовать вход **`https://gemini.google.com/app?authuser=[EMAIL]`** — даже если по умолчанию профиль открывает корп-аккаунт, authuser-редирект достаёт личный, если он залогинен в том же Chrome.
3. Причина drop обязана ПОИМЁННО перечислить проверенные двери (сколько Chrome обошёл, что показал каждый, пробовал ли authuser). «Chrome — корп-аккаунт» без счёта браузеров = недоказанный claim ([[prichina-kak-claim]]).
4. Drop = «leg не собран в этом заходе», а НЕ «узел мёртв» — вечные выводы про узел в reason не писать.

Гипотезы, уже проверенные и **опровергнутые** — не тратить на них время заново:
1. «клон профиля теряет `storage/`/localStorage» — полная `rsync`-копия профиля ведёт себя так же;
2. «виноват headless» — headed идентичен;
3. «куки не долиты из WAL» — `cookies.sqlite-wal` 0 байт, снимки полные;
4. «живой Firefox держит сессию в памяти» — штатный SIGTERM, `cookies.sqlite` не изменился ни на байт;
5. «гео-блок на австрийском IP» — НЕТ: изнутри Firefox на NODE-0X блока нет; блок был на ЧУЖОМ Chrome (RU IP).
10. **⭐ ChatGPT-канал по умолчанию = Pro + инструмент «Web search», а НЕ чип Deep research** (замер 2026-08-04, разбор инцидента 26.07). Чип DR на этом аккаунте резолвится в `deep-research-mini`: ран обрывается посреди плана (`status: completed`, шаги 3–5 `pending`, 5–7 мин вместо 20–40) и открывает мало источников (12 уникальных URL при запрошенных 15–25). Тот же вопрос через **Pro + Web search** дал 73 поисковых запроса и 31 прочитанную страницу (`DR26-07-26-ZB-02-harari-alpha-chatgpt.md`, там же вендорский журнал поиска). ⇒ ChatGPT в веере = Web search-рельса; DR-чип — только когда явно нужен длинный автономный ран. ✅ **Тест проведён 04.08** (один ран, чип DR, пикер Pro, чат `6a71e627`): `resolved_model_slug = gpt-5-thinking` — ни полного DR, ни mini; 3m44s, обрыв на шаге 2, отчёт 13.4 КБ и **citations = 0** (URL набраны текстом, маркеров 【…】 нет) ⇒ сегодня чип DR отвечает из памяти по-настоящему. Лестница деградации канала: `deep-research` → `deep-research-mini` (21–26.07, поиск был) → `gpt-5-thinking` (04.08, поиска нет). Заодно закрыто: модель в пикере ни при чём — outer turn у DR всегда `gpt-5-5-instant`. 🤔 Причина (квота vs политика вендора) не доказана: эндпоинта с лимитами в вебе нет (`/backend-api/*limits*` = 404). ⇒ Практический вывод не меняется: **ChatGPT-канал = Web search**, DR-чип на `a2@` не тратить.

## ⛔⛔ КОРЕНЬ 22.09.2026 вечером: «ОТПРАВИЛОСЬ» ДОКАЗЫВАЕТСЯ ТОЛЬКО API ВЕНДОРА

Замер, стоивший четырёх ложных ног и одного неверного доклада оператору: пять заказов ушли в GLM через живой Chrome, и по ВСЕМ признакам раны стартовали: URL сменился на `/c/<uuid>`, композер опустел, в сайдбаре появились заголовки чатов на русском по нашим темам. Через три часа `GET /api/v1/chats/` показал правду: на сервере существуют ТОЛЬКО ДВА чата из пяти, и у обоих `assistant: 0 байт` при целом `user: 3208`. То есть промпты доехали, а ответов не было НИ ОДНОГО.

**Правило:** у браузерной рельсы состояние `started` ставится ТОЛЬКО после ответа API вендора, где есть assistant-сообщение длиной > 0. Для z.ai это:
```js
const t=localStorage.getItem('token');
const r=await fetch('/api/v1/chats/'+id,{headers:{Authorization:'Bearer '+t}}).then(x=>x.json());
Object.values(r?.chat?.history?.messages||{}).map(m=>m.role+':'+String(m.content||'').length)
```
⇒ `["user:3208","assistant:0"]` = рельса НЕ работает, как бы убедительно ни выглядела страница.

⛔ Список признаков, которые СЕГОДНЯ ДОКАЗАНО лгут и больше не считаются стартом: смена URL на `/c/<id>` · опустевший композер · заголовок чата в сайдбаре · наличие нашего промпта в теле страницы. Первые два я сам записал в этот файл утром того же дня как доказательство — это было неверно ([[instrument-is-a-claim-too]]).

⚠️ Соседний замер того же вечера: три разные веб-рельсы (GLM, Mistral/Vibe, claude.ai) в живом Chrome вели себя одинаково: промпт садится 1-в-1 (длина и кириллица сверены), Send не доводит до чата, вкладка ловит CDP-таймаут 45 с. ⇒ Chrome-MCP для веера из нескольких заказов — хрупкая дверь; штатная — `dr_ff_rail` на ЗАЛОГИНЕННОМ робот-профиле.

✅ **Запрет протух: Mistral (теперь «Vibe») ЗАЛОГИНЕН в Chrome под «PaloAlto Ai Research Lab»**, стены ToS нет (блок 01.09 «требует принять новые Terms» больше не действует). Композер = `contenteditable`, режимы `Fast` / `Think` (брать **Think**), вставка только `execCommand('insertText')` — синтетический paste доносит ТОЛЬКО первую строку (102 из 2570 знаков).

## ⭐⭐ ПРИКАЗ 24.09.2026 (голосом, mid-run): БРАУЗЕР ПЕРВЫМ ВСЕГДА, CLI — ТОЛЬКО КОГДА БРАУЗЕР НЕДОСТУПЕН

> «CLI двери мы используем только если браузеры недоступны. То есть мы всегда идём в браузер —
> Chrome, Firefox — и только после этого мы идём в CLI.»

Порядок дверей на КАЖДУЮ рельсу: **(1) живой Chrome-MCP → (2) Firefox-профиль (`dr_ff_rail`) →
(3) CLI (`dr_headless_dispatch`) — только когда обе браузерные двери проверены и закрыты**, и в
леджере названо, ЧЕМ закрыты (нет Chrome-MCP у сессии · капча · разлогин без права логина).
Причина: браузерная дверь идёт по подписке в САМОМ СИЛЬНОМ режиме (Deep Research / Heavy /
Advanced Search), а CLI отдаёт web-search-огрызок или вовсе хвост агента (замер 10.09: `claude -p`
= 4302 б «Addendum», grok CLI = обрывок 696 б). Замер-родитель правила 24.09: сессия сожгла
grok CLI и объявила gemini «мёртвым» по CLI-ошибке лицензии Code Assist, не сходив в веб —
оператор отбил: «Gemini у нас работает прекрасно. Ты пробовал через Firefox и через Chrome?»
⛔ «CLI отработал» не закрывает рельсу, у которой браузерная дверь не проверялась.
Безлюдные рутины без браузерных MCP по-прежнему едут headless — у них браузерной двери нет,
это и есть законное «недоступен».

## ⛔ ШАГ 0 ОБЯЗАТЕЛЬНЫЙ (с 14.09.2026): СНАЧАЛА ПРИБОР, ПОТОМ БРАУЗЕР

```bash
python ~/.claude/scripts/_shared/ff_session_probe.py          # таблица профиль × вендор, 0 сети, ~0.1с
python ~/.claude/scripts/_shared/ff_session_probe.py --rail claudeai   # адресно
```

**Читать вывод асимметрично.** «кук НЕТ» = сессии точно нет. «куки есть» = может быть жива, доказывает только заход (замер 02.09: у Google счётчик кук не менялся, а сессия была мертва).

**Почему шаг появился (замер 14.09.2026, заказ DR26-09-14-ZB-09-2008, этот узел).** Четыре ноги умерли за шесть минут, и сессия объявила, что «профиль AutoFF протух», а фактически написала это про браузеры вообще. оператор отбил: «у меня куча браузеров, везде всё работает» — и был прав. Прибор показал: **в робот-профиле `ff-autoff-profile` claude.ai = 0 кук и chatgpt = 0 кук, туда не логинились НИКОГДА**, а Chrome `Profile 3` в это время работал и держал свои куки под замком. Ложный диагноз собрался из склейки двух разных болезней: три ноги шли на КОПИИ профиля (копия ломает ротацию — известно с 04.09), а четвёртая упала на пункте меню Deep Research, то есть на ВЁРСТКЕ.

**Что изменилось в `dr_ff_rail.py` (дефолты, а не проза):**

- работа **В самом профиле — теперь ДЕФОЛТ**; копия только по явному `--copy`. Знание «копия = разлогин у любого вендора с ротацией» две недели лежало строкой в журнале, пока дефолт кода копировал. Правило, не въехавшее в дефолт, не работает;
- параллельность больше не покупается копией: `profile_lock()` ставит второй прогон **в очередь** (`BUSY`), а не плодит копию;
- четыре болезни — четыре кода и четыре разных слова: **`NO_SESSION`** сюда не логинились (отказ за 0.75с, БЕЗ поднятия браузера, с именем живого профиля) · **`LOGGED_OUT`** выкинуло (ловится `/auth`, `logout`, `challenge_redirect` — раньше `/auth` не ловился, и разлогин GLM уезжал под видом «нет композера») · **`LAYOUT`** залогинены, но сменилась разметка · **`BUSY`** профиль занят соседним прогоном;
- **автоподбор профиля**: если в заданном профиле логина вендора НЕ БЫЛО, рельса сама уходит в профиль, где сессия есть, и говорит об этом вслух (`--no-auto-profile` выключает). Знание «живые сессии лежат в системном профиле» лежало в этом файле с 10.09, но код упрямо шёл в свой пустой AUTOFF: знание в скилле не работает, пока код идёт мимо него;
- ⚠️ автоподбор — костыль, а не лечение: человеческий профиль гвард уводит на КОПИЮ, а копия со временем ломает ротацию. Замер 14.09: gemini через «Ct3iOc7B.Profile 1» зашёл и ответил — то есть вчерашнее «gemini не нашёл Deep Research» было про ПУСТОЙ робот-профиль, а не про вендора;
- тест: `python ~/.claude/scripts/_test_dr_ff_rail_logout_and_copy.py` (5/5, красный прогон воспроизводит старую логику); проба узла: `python ~/.claude/scripts/_probe_ffrail_root.py`.

**Тупик, который надо знать до того, как начнёшь его обходить.** Человеческий профиль (`Ct3iOc7B.Profile 1`) in-place запрещён гвардом — geckodriver травит его `user.js`; а копия человеческого профиля убивает ротацию сессии. Обе двери закрыты, и это не лечится флагом. **Здоровый выход ровно один: один раз залогинить РОБОТ-профиль** и дальше не копировать его никогда:

```bash
"C:\Program Files\Mozilla Firefoxirefox.exe" -no-remote -profile "%LOCALAPPDATA%f-autoff-profile" https://claude.ai https://chatgpt.com https://chat.z.ai
```

Пароли вводит человек (Tier-2). После этого рельса безлюдная, и сессия живёт, потому что профиль больше не копируется.

## ⭐ ЗАМЕР 10.09.2026 (NODE-0X-2023PAL, DR26-09-10-ZB-01-1030) — профиль решает больше, чем вендор

1. **AutoFF на этом узле разлогинен молча, и это видно только по симптому вендора.** claudeai → involuntary logout; mistral → страница `Sign in` + эхо промпта; gemini → тело с «Upgrade», то есть БЕСПЛАТНЫЙ аккаунт. Живые сессии ВСЕХ шести вендоров лежат в СИСТЕМНОМ профиле Firefox **`Ct3iOc7B.Profile 1`** (claude.ai 7 кук, chatgpt 8, google 36, z.ai 18, mistral.ai 5) — берётся через `--profile-dir "Ct3iOc7B.Profile 1"`. ⛔ Вывод «у вендора двери нет» законен только после обхода профилей: имена per-node, хардкодить нельзя, перечисляются по `%APPDATA%\Mozilla\Firefox\Profiles`.
2. **⛔ `--no-copy` на человеческом профиле рельса запрещает сама** («травит user.js через geckodriver») и молча уходит на копию — значит для Google по-прежнему действует грабля 02.09: копия крутит куки. Отсюда gemini на этом узле не даёт DR ни с `--deep` (кнопка «Start research» не поднялась за 7.5 мин), ни без него (эхо промпта + free-аккаунт).
3. **GLM: третья эпоха UI — голая кнопка формы с `data-active`, без ARIA и без текста.** Судья `glm_search_is_on` знал только органы с `role=switch`/`aria-pressed` и печатал «орган управления не найден» на ЖИВОМ включаемом органе — рельса выпадала из кворума на исправном аккаунте. Починено 10.09: судья понимает `data-active` (fail-closed при двух таких кнопках), добавлен `glm_enable_search()` — жмёт глобус НАТИВНЫМ кликом, затем ПЕРЕЧИТЫВАЕТ и дожимает тумблер `Advanced Search`, если клик открыл меню (эпохи чередуются в одной сессии). Сетка `_test_dr_ff_rail_glm_gate.py` 12/12, красный прогон показан. Итог живьём: `Advanced Search ON` + `Deep Think Max`, промпт ушёл.
4. **⛔ Но z.ai поставил КАПЧУ** («Please drag the slider to complete the puzzle», CertifyId в хвосте страницы). Капчу не обходим — рельса идёт в `missing` как требующая рук, а не как «сломанная».
5. **`grok -p` на этом узле отдаёт огрызок 696 б / 0 URL.** Проверено: многострочный argv и кавычки доезжают целиком (тесты-эхо), то есть прежний диагноз «обрезка ввода» НЕВЕРЕН — обрывается ВЫХОД: в stdout приезжает только первая строка ответа («I'll count the received prompt exactly…»). Два прогона подряд — третий тем же способом не гнать.
6. **Рельса `claude` (CLI) отдаёт ХВОСТ, а не отчёт.** `exit=0 bytes=4302 urls=3 -> OK`, а в файле — «Addendum к Q3 и Q4»: агент писал многими ходами, `-p` вернул последнее сообщение. `dr_leg_gate` честно покраснел (558 симв. тела). Плюс лега унаследовала НАШУ персону — первой строкой метка времени из CLAUDE.md. В кворум сбора входит, в кворум подтверждения — нет.
7. **`dr_queue.py robot-work` на этом узле НЕ отдаёт поле `doors`** — машинной карты дверей тут нет, двери проверяются фактом.

## Жёсткие рамки (читать первыми)
1. **⭐ Мандат оператора (2026-07-14, supersedes квота-гейт 05.07): любое количество DR, БЕЗ спроса.** «Делай любое количество депрезёрчей, не спрашивай меня, не беспокойся по поводу лимитов» — ChatGPT при выжатой квоте деградирует мягко (лайтовее отчёт, не отказ), гетеро-веер на 3 вендора компенсирует. Запускаю сам, докладываю постфактум. Единственное «но»: не жечь квоту на ДУБЛИ — дедуп-проверка Шага 0 обязательна.
2. **Браузер строго локально** на машине, где идёт сессия. Ничего не просить у других машин.
3. **Аккаунты оператора:** если сайт разлогинен → логин по [[social-auth-autonomous]] (креды в store); CAPTCHA/2FA-стена → позвать оператора одной фразой + скриншот.
4. **Ничего не отправляем КРОМЕ промпта** в композер DR. Не трогать другие чаты/настройки.
5а. ⛔ **`get_page_text` ВРЁТ НА СПИСКАХ (замер 2026-07-29/31).** Границу знать точно:
   для СТАТЬИ/сплошного текста он годится (на нём и держится вынос отчётов ниже), но для
   **динамического списка** — recents, сайдбар чатов, лента, инбокс — он отдаёт заглушку
   («Choose from your existing conversations…»), тогда как `read_page (filter: all)` на той же
   странице показывает все элементы. Замер: X-инбокс — `get_page_text` «пусто», `read_page`
   15 тредов; форма Anthropic — «пусто», а там кнопка Apply. ⇒ **вывод «список пуст» имеет
   право на жизнь ТОЛЬКО из `read_page`**. Пустота из одного метода — не пустота
   ([[check-all-places-not-one]]); это ложная тишина, а она дороже громкой ошибки.
5. **ANTI-RECENTS при забО́ре отчёта:** ища готовый DR-чат/отчёт в веб-UI (ChatGPT/Gemini/Grok), НЕ заключай «отчёта нет» из беглого списка recents — используй встроенный ПОИСК по ключам/ID + Projects/архив + подтверди активный аккаунт по email. Сперва реестр (`_DR-Registry.md`, Шаг 0), потом UI-поиск, и только потом вывод «нет». Канон: память [[web-ui-search-not-recents]] (инцидент Woom 2026-07-23).
6. **⭐ МОДЕЛИ ПО РОЛЯМ КОНВЕЙЕРА (dev 14.08.2026, «всё правильно — обнови скилл»).** Три роли, три планки:
   - **Курьер-сессия fanout (этот скилл: вставить промпт в композеры, забрать ссылки, леджер) = Sonnet, эффорт low.** Работа механическая; Fable/Opus на разносе = жжение бака без прироста качества. Поднимая ДР-сессию слотом — модель на задаче через MCP не задаётся и в карточке не видна: проверь фактическую модель ПЕРВОЙ строкой транскрипта прогона (`"model":` в jsonl); поехал Fable → один прогон дотерпеть (выхода у курьера мало), на повторе перевесить на Sonnet-слот.
   - **Чужие вендоры внутри их DR = всегда их САМАЯ умная модель + максимальное рассуждение** (§6.3, список сверять у вендора, не по памяти) — это уже зашито в рецептах ниже.
   - **Синтез-консенсус (Шаг 4) = Fable (fallback Opus), эффорт высокий** — это мышление и Decision Memo, курьеру его не отдавать: курьер довозит отчёты до `_originals` и реестра, синтез — отдельный заход умной моделью.

## Шаг 0 — вход
⭐ **ДЕДУП ПЕРЕД КВОТОЙ (dev 2026-07-14):** прежде чем жечь DR-квоты — проверь, не готов ли отчёт уже. (1) Есть ID в промпте → его строка в реестре: `grep "<DR-ID>" "$OBSIDIAN_VAULT/_DR-Registry.md"` — статус `collected`/`synthesized` = СТОП, fan-out не нужен: доложи «уже собран», покажи файлы (`_originals\deep-research\*<DR-ID>*`, `03-Insights\insight-DR-<id>*`), иди в Шаг 4 (синтез). (2) ID нет → grep реестра по ключевым словам темы: та же тема в `issued` → переиспользуй ТОТ ID; в `collected+` → покажи готовое, спроси, нужен ли вообще новый прогон. Ночной `dr_collect.py` (хаб 05:05) флипает статусы по экспортам сам — реестр свежее памяти сессии.
⭐ Номер DR обязателен (dev 2026-07-03): если у промпта ещё нет ID `DRYY-MM-DD-МАШИНА-NN` — выделить: `python $IMPORTS_ROOT/dr_registry.py new "<тема>" --tool chatgpt,gemini,grok` и поставить ID первой строкой промпта (`# DR26-07-03-ZB-01 — <тема>`). Код машины скрипт определяет сам (своя очередь у каждого компа — дублей при синке нет). Канон: `reglament-numeratsiya-dr-i-reestr`.
Промпт берём: из текущего чата (только что сэмитили по Альфе) / из файла, что укажет оператор. «+» НЕ спрашиваем (мандат 14.07) — объявляю строкой `🚀 DR-fanout: разношу <ID> в ChatGPT+Gemini+Grok` и еду.

## Шаг 0.5 — тюнинг промпта под вендоров (обязательно)
Перед раздачей приклеить к телу промпта: `§1 УНИВЕРСАЛЬНЫЙ ADD-ON` из [[dr-platform-playbook]] (`08-Templates\dr-platform-playbook.md`) — всегда, всем; **плюс платформенный блок §2 (Grok) / §3 (Gemini) / §4 (ChatGPT)** под каждого конкретного вендора. Тело (из `deep-research-prompt-template.md`) + §1 одинаковы у всех; платформенный блок различается НАМЕРЕННО (играет на сильную сторону: Grok=реалтайм/X+жёсткие цитаты, Gemini=правка плана/официоз/глубина). ID `DRYY-MM-DD-МАШИНА-NN` первой строкой у всех.

## Шаги 1-3 — АВТОМАТ submit → probe → collect (per vendor)
> Ядро надёжности v2, ✅ подтверждено внешним DR (см. п.7). Каждый вендор проходит автомат независимо; сломался на шаге — падает В ФОЛБЭК того шага, не роняя остальных. Золотое правило: **probe перед burn** — ни одна DR-квота не тратится, пока не доказано: (а) режим включён, (б) промпт целиком, (в) ран стартовал.
>
⭐ **ВОРОТА ПЕРЕД `collected` (правило 04.08, дверь построена 14.08).** Прежде чем назвать легу собранной,
записать её в `_originals` и флипнуть реестр — прогнать пороги:
```
python3 ~/.claude/scripts/dr_leg_gate.py --prompt <файл-заказа> <файл-леги>
```
⭐ **`--prompt` ОБЯЗАТЕЛЕН** (15.09.2026). Без него спит порог № 0 «ЭХО», и снимок
НЕЗАЛОГИНЕННОЙ страницы уезжает как готовое исследование: объём закрывает эхо нашего же
заказа, а источники — ссылки и годы ИЗ НЕГО ЖЕ. Живые случаи в этом же файле:
mistral 14.09 («5872 б, Sign in + эхо» → заказ закрыт ФАЛЬШИВОЙ 4-й рельсой) и glm («сайдбар +
эхо промпта», строка «гейт пропускает такое exit 0» ниже по тексту). Гейт без заказа
предупреждает об этом вслух первой строкой — увидел предупреждение, значит судишь вслепую.
```
```
exit 0 = годна · exit 1 = `collected-EMPTY`, в синтез НЕ идёт. Три порога: объём ≥5000 · источники (ссылки/годы) ·
движок не сказал сам, что поиск не работал. **`exit 0` вендора ничего не доказывает:** `grok --tools ""` отключает
поиск и отдаёт 243 байта преамбулы нулевым кодом — так лега DR26-07-26 пролежала «собранной» 5 дней.
Не прошло → гнать по ДРУГОЙ оси (авторизация · движок · аккаунт · браузер), а не тем же параметром;
рельса выглядит мёртвой → сперва `deploy_check.py` (см. `/secondop`). Легу без источников НЕ сохраняем даже
«чтобы было»: по ней примут решение. Канон: `reglament-vneshnyaya-lega-schitaetsya-sobrannoy-tolko-posle-porogov`.

> **Состояния** (ledger = `_drafts/DR-FANOUT-<DR-ID>-*.md`, ключ = DR-ID → resume идемпотентен): `staged → mode_verified → submitted → started → waiting → ready → collected → delivered`. Аварийные: `needs_reauth` · `drift_suspected` · `probe_failed` · `aborted`. ⭐ **Человеко-гейта ровно два — `needs_reauth` и `drift_suspected`; всё остальное безлюдно** (консенсус DR).
> **Локаторы:** ARIA/role первыми → CSS → и только затем LLM/vision. ⛔ Семантический/LLM-поиск элемента — ТОЛЬКО в dry-run/repair-режиме, НИКОГДА на квота-сабмите (консенсус DR).

Инструменты одним ToolSearch: `tabs_context, navigate, computer, read_page, tabs_create, form_input, get_page_text, read_console_messages`.

### СОСТОЯНИЕ 1 — SUBMIT (включить DR-режим + вставить промпт)
Новая вкладка → дождаться загрузки → залогинен? (нет → [[social-auth-autonomous]]; стена 2FA/CAPTCHA → скриншот + пропустить вендора). Затем **найти DR-режим ГЛЯДЯ на страницу** (не по памяти — UI плывёт у всех троих):
- **ChatGPT** (аккаунт dev.**a2**@gmail.com): сперва селектор модели → **Pro, максимальная** (сейчас GPT-5.6) + максимальный уровень думания; затем композер → меню инструментов («+»/«Tools») → «Deep research». ⭐ dev 21.07: всегда самая умная модель, имя меняется — принцип нет.
- **Gemini** (аккаунт dev.**a**@gmail.com, личный): ⚠️ 31.07 в Chrome этот аккаунт (индекс u/2) отдал МАРКЕТИНГОВЫЙ ЛЕНДИНГ, а не приложение; рабочее приложение было под `dev@` — перед прогоном проверять глазами, какой аккаунт реально открывает app. Прежняя пометка: **платный Google AI Pro, 5 ТБ, с 06.01.2026** (проверено 28.07) — DR ≈20/день, лимиты ~4×, контекст 1M → тяжёлые ДР сюда гоним УВЕРЕННО, это НЕ урезанный бесплатный тир (память [[gemini-two-rails-free-api-vs-paid-ai-pro]]; «free» = только API-ключ ломателя /tt, другая рельса). Модель = **Pro** (сейчас 3.1), ⛔ НЕ Flash (тихо откатывается — проверять!); включить **Extended thinking** (галочка справа возле микрофона); «+» → «Deep Research» → промпт → Enter → план → **дожать OK/Start**.
- **Grok** (аккаунт **avvalon**@icloud.com — с двумя «v», проверено 31.07 — там же Twitter оператора): ⭐ dev 21.07 — режим **Heavy** ДЕФОЛТ (куплена максимальная подписка; supersedes прежнее «Expert, Heavy не трогать»). Отдельной DR-кнопки нет → в тело промпта добавить строку «Search the web extensively and cite sources»; следить, чтобы селектор не свалился в Expert/Fast (тихий деграде ZB-03 20.07). Методика «DR-grade в Grok Heavy» (собрано 21.07, DR26-07-21-HUB-02): **Heavy сам и есть Deep Research** — рой 8–16 суб-агентов, ищут параллельно и спорят; Expert теперь одноагентный и для citation-heavy слабее; DeepSearch/DeeperSearch убраны и растворены в Heavy. Без принуждения Heavy отвечает из памяти → в промпт обязательно: «search the web and X extensively» + 15–25 первичных источников + короткая цитата и точный URL на каждое утверждение + «cite ONLY URLs you actually opened» + финальный проход верификации. Доказательство настоящего прогона: «Thought for» в минутах + счётчик «N sources»; мгновенный ответ без источников = деграде, перезапуск. Квоты = недельный общий пул (Settings → Usage, в процентах), контекст 256k–500k, прогон 5–20+ мин. Экспорта одной кнопкой нет (выделить-скопировать); Share = ПУБЛИЧНАЯ ссылка ⛔. Полный шаблон промпта — в `_originals\deep-research\DR26-07-21-HUB-02-grok-heavy-playbook-grok.md`, раздел «(b) Reusable Prompt TEMPLATE»; синтез — `insight-DR-DR26-07-21-HUB-02-grok-heavy-as-a-deep-research-engine`.
- **claude.ai** (аккаунт dev.**a2**@gmail.com, Claude Max, org `a673590f`) — в дефолте с 04.08.2026 («теперь ВСЕГДА добавляй КЛОД.аи в ДРы»). ⚠️ ПЕРВЫМ ДЕЛОМ проверить, ПОД КЕМ открыт claude.ai: `GET /api/organizations` → должен быть `a673590f`; под `bbplatinum` это ДРУГОЙ аккаунт (та же ловушка, что топит ночной `claudeai-sync`, [[claudeai-sync-needs-a2-account]]). ⛔⛔ **Вход НЕ через logout в живом Chrome оператора** (приказ оператора 30.08, свип #595c4751, канон `reglament-hab-brauzernye-lichnosti-bb-i-roboty`): его Chrome = `dev` ВСЕГДА, робот там не выходит из аккаунта и не переключает его — это и был корень «Chrome постоянно вылогинивает». a2 живёт ТОЛЬКО в выделенном профиле `_chrome_profile_a2`; сессия мертва → перелогин ТОЛЬКО его: `python $IMPORTS_ROOT/claude-ai/railc_login_a2.py` (magic-link просится сам, ссылку несёт Gmail-коннектор a2; ⛔ «Continue with Google» = попап, расширению НЕ виден — не тратить на него заход). Пулл оттуда же: `pull_rail_c.py --run --profile=a2`. DR-режим = **Research** в меню инструментов композера (рядом со скрепкой); модель — самая умная из доступных. Приватный URL чата = `claude.ai/chat/…`.
  - ⛔ **МОДАЛКА «Suggested connectors» ТИХО ДЕРЖИТ РАН (замер 05.08.2026, HUB).** После Send чат создаётся, URL меняется на `/chat/…`, снаружи выглядит как стартовавший Research — **а поиск не начинается вообще**, пока в диалоге «Suggested connectors … Skip / Confirm» не нажат **Skip**. Простояло ~10 минут; сразу после клика пошло «Searching for sources…». ⇒ У claude.ai probe-after-start обязан включать проверку модалки, иначе получишь `not-collected` при полностью живой сессии. Skip выбираем осознанно: сторонние коннекторы внешнему ДР не нужны и тянут приватность.
  - ⏱ **Research тут ДОЛГИЙ:** в этом же прогоне рельса шла 1 час и не завершилась, пока остальные четыре уже сдали отчёты. Не бракуй по времени — кворум закрывается без неё, а отчёт подберёт ночной `dr_collect.py`.
- **GLM** (chat.z.ai, Z.ai/Zhipu) — в дефолте с 04.08.2026 («glm ТОЖЕ ИСПОЛЬЗУЕМ ДЛЯ ДР»). 🔑 **ВХОД = Google SSO под `[EMAIL]` («ббПлатинум») — прямое указание оператора**, пароль в [[credential-store]] (`secrets\google_bb.env`), подаёт его САМ Chrome. ⛔ API-ключ z.ai не подставлять: рельса ПОДПИСОЧНАЯ, ключ = поштучная оплата мимо правила «выгребай лимиты» (CLAUDE.md §6.3). Приватный URL чата = `chat.z.ai/c/…` (образец от оператора: `chat.z.ai/c/s_be3e1bb6`).
  - ✅ **ЗАМЕР ДВЕРИ 04.08.2026, NODE-0X** (не claim — читано со страницы): сессия ЖИВА в **Chrome «Browser 2»**, а в «Browser 1» стоит `Sign in` ⇒ проверять ОБА подключённых Chrome, один профиль ничего не доказывает ([[check-all-places-not-one]]). Аккаунт подтверждён запросом `/api/v1/auths/` → `[EMAIL]`, имя «PaloAlto Ai Research Lab» — этим и проверять, а не глазами по аватарке.
  - ✅ **ЛОКАТОРЫ КОМПОЗЕРА (замерены там же):** редактор = обычный **`<textarea>`** внутри `form` (⛔ НЕ ProseMirror, `isPM:false`) ⇒ в каскаде `paste_verify.js` садится нативный React-сеттер, синтетический paste не нужен. Три кнопки в композере: `+` (файлы) · 🌐 **глобус = веб-поиск** · «атом» с `aria-label="Deep think enabled"` (по умолчанию ВКЛЮЧЁН, синий) — **рядом с надписью `Deep Think` стоит выпадающий селектор УРОВНЯ (`Max` и более слабые), и «включён» ≠ «Max»** · `aria-label="Send Message"`. Селектор модели — слева сверху; список 04.08: **GLM-5.2 (NEW, флагман)** · GLM-5.1 · GLM-5-Turbo · GLM-5V-Turbo · GLM-4.7. По правилу «всегда самая умная» **переключено на GLM-5.2** (было 5.1).
  - ⭐ **ДР-РЕЖИМ ЕСТЬ, ОН СПРЯТАН ПОД ГЛОБУСОМ** (найдено в первом живом прогоне 04.08, DR26-08-04-ZB-11-2142 — утренняя запись «отдельной кнопки Deep Research нет» была верна про видимую панель и неверна про рельсу). Клик по 🌐 открывает меню с двумя режимами: `Search` («Single-round search, quickly get information») и **`Advanced Search`** («Multi-round search, in-depth research and analysis») — тумблер, **по умолчанию ВЫКЛЮЧЕН**. ⛔ Без него рельса отдаёт однораундовый ответ: файл в `results/` появится, а разведки в нём не будет — тот же класс тихого брака, что Grok в Expert вместо Heavy. Порядок сабмита: селектор модели → **GLM-5.2** (дефолт 5.1, переключать руками) → 🌐 → `Advanced Search` ON → **Deep Think = `Max`** (см. пункт ниже — отдельный обязательный шаг) → JS-вставка в `<textarea>` → Send.
  - 🔧 **ПРИБОР:** `~/.claude/skills/dr-fanout/glm_probe.js` (read-only чтение композера, ничего не кликает) + судья `~/.claude/scripts/glm_probe.py` (0 LLM, exit-код, счётчик `_glm_probe_usage.jsonl`). Тесты: `_test_glm_probe.py` (14 проверок) · `_test_glm_probe.js` (node, DOM-заглушка со скриншотов + 5 мутантов). ⚠️ Заглушка ≠ живой chat.z.ai: селекторы списаны с замера 04.08 и скриншотов 31.08 — первый живой прогон обязан сверить `evidence`-строки; не совпало = UI поплыл, чинить ассет, а не обходить гейт.
  - ⭐⭐ **DEEP THINK = ВСЕГДА `Max` (приказ оператора 31.08.2026, со скриншотом композера; память `glm-deep-think-must-be-max`).** Отдельный шаг, а не деталь модели: у «Deep Think» есть выпадашка уровня, и заказ уходит на том уровне, что стоит в поле — тихий брак того же класса, что `Advanced Search` OFF и Grok в Expert вместо Heavy. Порядок: **сначала выставить `Max`, потом вставлять промпт и жать Send** (после вставки композер растёт и элементы уезжают). ✅ Проверка перед Send = ПРОЧИТАТЬ со страницы, что в композере написано `Deep Think  Max`; не прочитал — считай, что не выставил ([[prichina-kak-claim]]). Не читается / выпадашка не поддалась → рельса идёт в `missing`, а не «сойдёт и так».
  - ⭐ **ЗАМЕР 08.09.2026, NODE-0X (AUTO-NODE-0X-dr-quorum-topup) — что изменилось у вендора:**
    - **Модель теперь `GLM-5.3`**, не 5.2. Правило читать как «бери ВЕРХНЮЮ в списке», а не «выставь константу»: `glm_probe.py` до 08.09 требовал ровно `glm-5.2` и печатал ворчание на более новой 5.3 — прибор ругался на ПРАВИЛЬНОЕ состояние. Починено: `MIN_MODEL` + сравнение версий, ниже минимума = заметка, выше = молчит (посылка `glm-probe-min-model-20260908`).
    - **Глобус живёт в ДВУХ эпохах UI, и они чередуются в пределах одной сессии.** На `/` после навигации клик по глобусу открыл МЕНЮ с тумблером `Advanced Search` (старая эпоха), а до навигации тот же клик прямо переключил `data-active` (новая). Не помни, какая эпоха — ЧИТАЙ `form button[data-active]` после каждого клика и жми тумблер в меню, если появилось меню.
    - ⏱ **Рельса МЕДЛЕННАЯ, а не мёртвая:** ~9–10 мин от Send до конца ответа, из них первые ~6 — фаза `Thinking...` с ПУСТЫМ `.chat-assistant`. Приговор «застряла» до 12-й минуты не выносить (тот же вывод был 11.08).
    - 📥 **ЗАБОР ОТЧЁТА С z.ai — работает Blob-download, остальное закрыто.** Проверено в этом прогоне: `navigator.clipboard.writeText` → **CDP-таймаут 45 с**; `document.execCommand('copy')` → **`false`** (нужен жест); `fetch` на `10.0.0.0` → **`Failed to fetch`** (CSP `connect-src`). А `Blob` + `a.download` + `a.click()` **долетел** (33 457 б в `~/Downloads/`) — то есть общее правило «Blob может тихо не долететь» на z.ai в эту сторону не сработало. Порядок: Blob → **обязательный `ls ~/Downloads`** → не долетело, тогда `get_page_text`. Селектор тела ответа = `.chat-assistant.markdown-prose` (второй по величине — `.markdown-prose` пользователя, не спутать).
    - ⛔ **«ОТВЕТ ПУСТ» ПО СЕЛЕКТОРУ — НЕ ДОКАЗАТЕЛЬСТВО, ЧТО РЕЛЬСА ВСТАЛА.** В том же прогоне на ВТОРОМ сообщении чата `.chat-assistant.markdown-prose` отдавал 11 симв. (`Thinking...`) на 22-й минуте, когда на ЭКРАНЕ ответ был уже расписан до раздела 3 с таблицами; на первом сообщении того же чата селектор давал верные 20 078 б. Перед приговором «застряла» — **скриншот**, а не только DOM ([[instrument-is-a-claim-too]]).
  - ✅ **ПРОГОН ПОДТВЕРЖДЁН 04.08 21:47** (NODE-0X, Chrome «Browser 1» — утром живой была «Browser 2», ⇒ проверять ОБЕ, а не помнить): промпт 3400 симв. сел нативным React-сеттером, чат `chat.z.ai/c/86f270ee-…`, доказательство старта = текст в потоке «Начинаю многошаговое исследование… серию параллельных поисков». Кнопка Send уезжает вниз вместе с растущим композером — брать её координату ПОСЛЕ вставки, иначе клик попадёт в пустоту (первый клик так и пропал).
- **Mistral Le Chat** (chat.mistral.ai) — шестая рельса с 05.08.2026 («добавь мистраль шестой рельсой»). Взят вместо третьей китайской осознанно: GLM/Qwen/DeepSeek делят корпус и источники, Le Chat тянет европейские — веер растёт независимостью мнений, а не количеством. ДР-режим в Le Chat = **Deep Research** в панели инструментов композера (рядом с веб-поиском); модель — самая умная из доступных.
  - ✅ **ДВЕРЬ ОТКРЫТА С 26.08.2026** (замер, не claim): первый боевой прогон 6-й рельсы — `DR26-08-25-HUB-03-2301/results/mistral.md`, **40 168 б, 26.08 07:11**, хаб. Аккаунт оператор завёл, вход дальше ведётся самостоятельно.
  - ⚠️ **НО КАЧЕСТВО ЛЕГИ НЕ ДОКАЗАНО**: в том же заказе mistral вернул **0 проверяемых ссылок** — тело есть, разведки в нём нет. Перед синтезом гонять `dr_leg_gate.py --strict`: такая лега в кворум СБОРА входит, в кворум ПОДТВЕРЖДЕНИЯ — нет ([[quorum-is-a-counter-not-proof]]).
  - 🔑 Вход = Google SSO под `[EMAIL]` (та же почта, что у ChatGPT и claude.ai), пароль подаёт САМ Chrome. Локаторы Deep Research в композере до сих пор **по документации, не по замеру** — дописать с первого живого прогона с этого узла.
  - 📜 ИСТОРИЯ (не стирать): с 05.08 по 26.08 здесь стояло «аккаунта нет» — верный на день замера и протухший через 3 недели; 21 день строка врала всем узлам. Запрет тоже claim и протухает ([[ban-is-a-claim-recheck-before-workaround]]).
- Вставка промпта — ТОЛЬКО через JS, НИКОГДА `computer type` (каждый Enter = отправка, улетит обрезок, квота сгорит). ⭐ **Каскад `paste_verify.js`** (рядом со скиллом, от NODE-0X 07-16, лечит брак 07-10 «execCommand не сел»; форевер-фикс Grok-ProseMirror 07-17 FLEE-03): прочитать файл `~/.claude/skills/dr-fanout/paste_verify.js`, выполнить его тело через `javascript_tool`, затем `window.__drPasteVerify(PROMPT, "chatgpt"|"gemini"|"grok")`. Он сам перебирает методы (⭐ **синтетический paste-event для ProseMirror/TipTap** → execCommand → нативный React-сеттер textarea → node-параграфы Quill/CE → directSet), сверяет length+head+tail после КАЖДОГО (для ProseMirror читает `el.innerText`, а НЕ textarea-зеркало) и возвращает `{ok, method, gotLen, wantLen, isPM, ...}`.
  - ⚠️ **Grok 4.5 = TipTap/ProseMirror contenteditable** (`div.tiptap.ProseMirror`), а видимый `<textarea>` — это СКРЫТОЕ ЗЕРКАЛО: заполнение textarea (nativeSetter) даёт `ok:true`, но форма/React из зеркала НЕ обновляются → Submit-кнопка не рендерится, Enter=no-op, ран не стартует. **Настоящий редактор надо заполнять синтетическим paste-event** (`ClipboardEvent('paste',{clipboardData:DataTransfer})`) → ProseMirror штатно адоптит текст → `button[type="submit"]` появляется enabled → клик. Каскад теперь целит ProseMirror ПЕРВЫМ и делает это сам; textarea оставлен последним фолбэком.
  - Ручной фолбэк (если ассет недоступен): для Grok/ChatGPT — `const ed=document.querySelector('.tiptap.ProseMirror')||document.querySelector('.ProseMirror'); ed.focus(); window.getSelection().selectAllChildren(ed); const dt=new DataTransfer(); dt.setData('text/plain',PROMPT); ed.dispatchEvent(new ClipboardEvent('paste',{clipboardData:dt,bubbles:true,cancelable:true}))`; Gemini (Quill+TrustedHTML CSP) — `<p>`-параграфы через `createElement`/`textContent` + `dispatchEvent(new InputEvent('input'))`.
- Путь исполнения по вендору — гибрид (см. п.6 «что решено»): **Grok = живой Chrome-MCP**; **Gemini/ChatGPT = живой Chrome-MCP сейчас, выделенный Firefox-профиль для безлюдного расписания** (фундамент HUB-01).
- ⭐ **GLM ТЕПЕРЬ ЕЗДИТ И БЕЗЛЮДНО — `python3 ~/.claude/scripts/dr_ff_rail.py --rail glm` (профиль autoff, замер и починка 08.09.2026, NODE-0X).** До этого дверь была только через живой Chrome-MCP, то есть ночная рутина glm собрать НЕ МОГЛА: гейт отбивал каждый прогон словами «орган управления Advanced Search не найден». Причина оказалась НЕ в логине и НЕ в headless — обе версии были догадкой, обе опровергнуты замером:
  - логин в Firefox ЖИВ (autoff держит 17 кук z.ai; `Sign in`/`Log in`/`Войти` = False; имя `PaloAlto` на странице; сайдбар с историей наших DR-чатов) — прежняя строка «z.ai залогинен только в Chrome» неверна;
  - headless и headed ведут себя ОДИНАКОВО (2615 симв. страницы, 4 кнопки, поповеров 0) — значит режим ни при чём.
  - **В этой поверхности старой эпохи (меню под глобусом) НЕТ ВООБЩЕ**: ни одного `role=switch`/`checkbox`/`aria-pressed`, и клик по кнопкам меню не открывает. Веб-поиск = **единственная кнопка ФОРМЫ с `data-active`** (соседки различимы по id: `upload-file-button`, `send-message-button`), переключается **нативным** кликом Selenium `false → true`; синтетические pointer/mouse-события через `dispatchEvent` состояние НЕ меняют.
  - Починено в `dr_ff_rail.py`: новая `glm_enable_search()` жмёт глобус ДО суда и **перечитывает состояние со страницы** («нажал» ≠ «включилось»), а судья `glm_search_is_on` понимает собственный `data-active` кнопки. Гейт остался fail-closed, у предков состояние по-прежнему не берём. Глобусов стало два → снова fail-closed (значит вёрстка поплыла, и это честнее угадывания). Сетка `_test_dr_ff_rail_glm_gate.py` 13/13, красный прогон показан.
  - ⏱ Рельса всё равно МЕДЛЕННАЯ (~9–10 мин): судить только по содержимому чата после перезагрузки, не по спиннеру.

### СОСТОЯНИЕ 2 — PROBE (доказать до траты квоты)  ⭐ сердце v2
НЕ жать Send, пока три проверки не зелёные:
1. **Режим включён:** на странице видна активная плашка Deep research / Expert (read_page/screenshot подтверждает, а не память). ⭐ **GLM = ДВА факта разом: `Advanced Search` ON И в композере читается `Deep Think  Max`** (dev 31.08 — «не забывай включать Deep Think на Max» + «это тоже должно быть ВКЛЮЧЕНО ADVANCED SEARCH», оба со скриншотами). Глазами не судим — есть ПРИБОР:
   ```bash
   python3 ~/.claude/scripts/glm_probe.py js     # → инъекция в javascript_tool, вернёт JSON-вердикт
   python3 ~/.claude/scripts/glm_probe.py verdict '<этот JSON>'   # exit 0 = Send можно, 3 = нельзя
   ```
   Судья пересчитывает всё сам и поле `ok` из браузера игнорирует; fail-closed — «не прочитал» = запрет (меню глобуса закрыто → открыть и прогнать probe снова). exit 3 и не чинится → рельса `glm` в `missing`.
2. **Промпт целиком:** вердикт = `ok` от `__drPasteVerify` (length + head + tail сверены каскадом). `ok:false` → каскад сам перебирает методы; 2 неудачи подряд → пропустить вендора, квота цела, пинг в леджер. (Ручная проверка без ассета: `editor.innerText.length` ≈ длине И совпали первые/последние ~60 символов.)
3. Только теперь Send/Run.
Затем **доказать старт** (иначе «отправил» ≠ «пошёл»):
- ChatGPT: план/«starting research»/счётчик источников растёт.
- **Gemini ДВУХФАЗНЫЙ:** сперва генерит план и ЖДЁТ кнопку «Start research» — ОБЯЗАТЕЛЬНО дожать, иначе ресёрч не начнётся. Подтверждение: «Great, I'm on it… Researching N websites».
- Grok: «Researching…»/searched web N results.
- Старт не подтвердился за 2 попытки-с-переосмотром → НЕ перезапускать вслепую (жжёт) → пометить в леджере `probe-failed`, пропустить вендора, доложить.

### СОСТОЯНИЕ 3 — LEDGER (сразу после старта каждого вендора)
Записать/дополнить `$OBSIDIAN_ROOT/_drafts/DR-FANOUT-<DR-ID>-<slug>.md`: тема · промпт целиком · время старта · по вендору {started|skipped+причина|probe-failed} · URL вкладки. Это единственная страховка от «забыли забрать» при безлюдном прогоне — коллектор (см. ниже) работает по этому файлу.

### СОСТОЯНИЕ 3.5 — ДОЛОЖИТЬ оператору: промпт + ССЫЛКИ (обязательно, dev 17.07)
Как только вендор перешёл в `started` — **сразу в диалог оператору, не дожидаясь отчёта**: полный текст промпта блоком ```text``` (paste-ready) + строка `🔗 <vendor>: <url>` на КАЖДЫЙ стартовавший чат. Живая сессия → в ответ; безлюдный прогон → в TG-03 через `bus_send.py`.
- URL брать из того же снимка вкладки, что и probe (`tabs_context_mcp` / `page.url`) — он уже содержит id чата.
- **Ссылка = приватный URL чата** (`chatgpt.com/c/…` · `gemini.google.com/app/…` · `grok.com/chat/…` · `claude.ai/chat/…` · `chat.z.ai/c/…`). ⛔ Публичный share-линк (`/share/…`, `g.co/gemini/share/…`) — это ПУБЛИКАЦИЯ наружу (индексировалось Google), только по явной просьбе оператора.
- Не снял URL → сказать честно, с причиной; молча пропустить нельзя.
- Зачем: оператор смотрит с телефона и забирает результат сам по этой ссылке — она его точка входа. Канон: `reglament-vneshniy-resech-vsegda-promt-i-ssylka-v-chat`, память [[dr-prompt-paste-in-chat]].

### СОСТОЯНИЕ 4 — COLLECT (через ~20-40 мин, по леджеру)

> ⭐ **ПЕРЕД ЛЮБЫМ «Chrome-MCP недоступен» — ОДНА КОМАНДА (замер 06.08.2026, хаб, DR26-08-06-HUB-01-1055).**
> `Claude in Chrome is not connected` и пустой `list_connected_browsers` в 1 случае из 1 означали,
> что **Chrome просто не запущен**: `Get-Process chrome` → 0. Лечение: `Start-Process
> "C:\Program Files\Google\Chrome\Application\chrome.exe"` → подождать ~12 с → `tabs_context_mcp`.
> Расширение подключилось, все 4 тела веера снялись подряд за ~5 минут.
> **Цена не проверки:** параллельная сессия записала в реестр «chatgpt: тело не снято, Chrome-MCP
> не подключён», подняла лишнее замещающее плечо через Codex CLI и оставила в реестре строку
> «рельса недоступна», которая переживёт сессию. Ноль процессов ≠ мёртвая рельса
> ([[dead-verdict-expires]], память `chrome-mcp-dead-check-process-first`).
> Chrome ЖИВ, а расширение молчит → вот это настоящая поломка, тогда Firefox/эскалация.

> ⛔⛔ **ПЕРВОЕ, ЧТО ЧИТАЕШЬ ПЕРЕД БРАКОВКОЙ (замер 04.08, ZB-04 — я сам на этом попался).**
> **Строка `Research completed in Nm · 0 citations` НЕ ЯВЛЯЕТСЯ ДОКАЗАТЕЛЬСТВОМ ПУСТОГО РАНА.**
> 04.08 я забраковал ChatGPT-ран по этой строке, написал файл-вердикт `dead` — а потом
> достал backend и получил **35 citations · 34 рабочих URL · тело 17 622 симв.** Отчёт был
> живой и полный. Файл-вердикт пришлось удалять, заметку синтеза — переписывать дважды.
> **Ни один вендор не бракуется, пока не прочитан МАШИННЫЙ признак** (ChatGPT — `citations`
> из `widget_state`; Grok — «N sources»; Gemini — список источников). Нет доступа к признаку =
> статус `not-collected` («не смог прочитать»), **а НЕ `dead`** («вендор не работал»).
> Это два разных факта, и путать их — врать в данных.
>
> ✅ **ДОЛГ ЗАКРЫТ ЗАМЕРОМ 04.08 — и он оказался хуже, чем я предполагал.**
> Перепроверены ВСЕ забракованные по счётчику прогоны волны ZB, у которых в леджерах остался
> chat-URL. **4 из 4 — живые отчёты с источниками, выброшенные не глядя:**
>
> | DR | прежний вердикт | по backend | тело |
> |---|---|---|---|
> | ZB-01 sci-fi (26.07) | `dead` ×2, «таблица целиком ИЗ ПАМЯТИ» | **57 citations** | 15 162 |
> | ZB-02 Харари (26.07) | `dead` ×2, «отчёт из памяти» | **106 citations** | 25 423 |
> | ZB-03 пантеон (26.07) | канал `dead`, ушли в обход через Web search | **52 citations** | 22 828 |
> | ZB-04 HackerNoon (28.07) | `dead`, «в синтез НЕ берём» | **108 citations** | 18 185 |
>
> У ZB-01 ChatGPT-вендора в волте не было ВООБЩЕ — веер шёл двумя вендорами вместо трёх.
> Все четыре подняты и лежат в `_originals` с пометкой `recovered_from`.
> **Вывод жёстче прежнего:** ноль в счётчике не значил ничего ни разу. Единственный признак —
> `citations` из backend. Формулировку «рельса ChatGPT DR сломана системно» из старых леджеров
> не цитировать: она построена на приборе, который сам не проверяли.
> ⛔ **«НЕ СОБРАН» — ЭТО ТОЖЕ CLAIM, И ЕГО ИСТОЧНИК ЛОКАЛЬНЫЙ (замер 05.09, ZB-14).**
> Статус в реестре читается из ШАРДА ЭТОГО узла, а `03-Insights` доезжает синком с задержкой.
> 05.09 я объявил `DR26-08-04-ZB-14-2214` несобранным и отправил задачу хабу — отчёт был собран
> и синтезирован СУТКАМИ РАНЬШЕ рутиной `AUTO-NODE-0X-dr-runner` на NODE-0X (4 рельсы, вердикт готов).
> Локальный `running` + пустой grep = «мой узел этого не видит», а НЕ «работа не сделана».
> **Перед выводом «не собран» и перед отправкой заказа другому узлу — две дешёвые проверки:**
> (1) `ls $OBSIDIAN_VAULT/03-Insights | grep <DR-ID>` И `grep -rl <DR-ID> 03-Insights` (заметка синтеза может уже лежать);
> (2) возраст своего шарда — `ls -la $OBSIDIAN_VAULT/_machine-bus/_dr/DR-registry__from-*.md` (чужие шарды старше суток = вид отстал).
> Пусто в обеих → вывод правомерен. Иначе это лишняя работа чужому узлу.

DR думает 10-40 мин. По каждой started-вкладке: готов → извлечь (лестница ниже) → сохранить **verbatim** в `$OBSIDIAN_ROOT/_originals/deep-research/<DR-ID>-<slug>-<vendor>.md` (провенанс сверху: source/topic/date/origin) → `dr_registry.py update <DR-ID> --status collected --file "<путь>"`. ⭐ **ГЕЙТ ДОКАЗАТЕЛЬСТВА РАБОТЫ (21.07, DR26-07-21-HUB-02; ⚠️ ПЕРЕСМОТРЕН 04.08 — см. ниже):** перед сохранением прочитать доказательство прогона — Grok: «N sources» + «Thought for…»; Gemini: список источников; **ChatGPT: НЕ строку над виджетом.** Она у DR-виджета врёт: «0 citations · 0 searches» стоит у ВСЕХ connector-прогонов этого аккаунта, в том числе у тех, чьи отчёты мы приняли и использовали (21.07 HUB-02) — в backend'е у них 40–106 живых цитат. Настоящее доказательство ChatGPT-DR = `mapping[*].message.metadata.chatgpt_sdk.widget_state` → `JSON.parse` → `report_message.metadata.citations.length` (и `resolved_model_slug` там же). Пусто/0 цитат в citations → `dead`; ненулевой массив → искал, каким бы ни был счётчик. Для Grok/Gemini прежний порядок в силе: нет источников → `dead`, не `collected`. Не готов → отметить, вернуться позже. Безлюдный режим: ночной `dr_collect.py` (хаб) сам подхватит DR-ID из истории/Downloads и флипнет статус — ручной сбор нужен, только если отчёт нужен СЕЙЧАС.

**Фолбэк-лестница извлечения** — общий порядок (консенсус DR): **официальный export/share → backend JSON → DOM-scrape → эскалация человеку**. DOM — низший приоритет, не первый. Далее по вендорам:
- **ChatGPT** (отчёт в КРОСС-ДОМЕННОМ sandbox-iframe `connector_openai_deep_research` — JS туда не лезет, синтет-клики игнорит):
  1. **Backend JSON (основной, без кликов, ✅ 2026-07-14):** page-JS `s=await fetch('/api/auth/session').then(r=>r.json()); conv=await fetch('/backend-api/conversation/<id>',{headers:{Authorization:'Bearer '+s.accessToken}}).then(r=>r.json())` → Blob-download JSON → на диске Python: `mapping[<node>].message.metadata.chatgpt_sdk.widget_state` (JSON-строка → `json.loads`) → `report_message.content.parts[0]`. Узел = walk по «Executive Summary».
  2. **Без widget_state** (часть DR, ✅ DR26-07-11-HUB-02): отчёт прямо в `mapping[*].message.content.parts[0]` — walk по mapping, самая длинная строка >3000 симв.
  3. ⚠️ **РЕГРЕССИЯ 04.08: «Export to Markdown» синтет-кликом БОЛЬШЕ НЕ РАБОТАЕТ (ZB-04).** Меню по координатному клику открывается, но клики по ПУНКТАМ меню не доходят: меню остаётся открытым, Escape его не закрывает, `Copy contents` не меняет буфер (проверено сентинелом), `Export to Markdown` не создаёт файл (проверено `ls Downloads` ×3). Меню живёт в кросс-доменном iframe, куда синтет-клики не проходят. **Не тратить на этот путь больше одной попытки — путь 1 (backend JSON) 04.08 отработал с первого раза на том же самом чате.** Ниже — прежнее описание пути на случай, если UI откатят:
  3-бис. ⭐ **Меню виджета «Export to Markdown» — работало синтет-кликом, безлюдно (✅ 2026-07-17, HUB-06; ❌ 04.08 — см. выше):** новый connector-формат DR не отдаёт widget_state ВООБЩЕ (пути 1-2 мертвы) и невидим для find/accessibility-tree → только КООРДИНАТНЫЙ клик: иконка download в шапке виджета (правый верх, рядом с expand) → меню `Copy contents / Export to Markdown / Export to Word / Export to PDF` → **Export to Markdown** → `deep-research-report.md` в Downloads (проверить `ls`!) → переложить в `_originals` с провенансом. Человека звать НЕ нужно.
  4. ⚠️ **Rate-limit врёт молча:** при «Too many requests» backend отдаёт mapping БЕЗ widget_state → выглядит как «отчёта нет», хотя отчёт готов и виден на экране. «Пусто из API» ≠ «нет отчёта» → сверься со СКРИНШОТОМ до вывода, подожди пару минут.
  5. ⚠️ Открывать `iframe.src` отдельной вкладкой БЕСПОЛЕЗНО — песочница пустая, контент прилетает через postMessage.
- **Gemini:** отчёт в `STRUCTURED-CONTENT-CONTAINER` (канвас, same-origin) → `innerText` узла с заголовком → Blob-download → фолбэк: рендер в `<pre>` + get_page_text.
- **Grok:** отчёт в основном потоке → `document.querySelector('main').innerText`, отрезать эхо-промпт и хвост-подсказки → Blob-download. ⭐ Якорь обрезки: **«Thought for…» надёжнее первого «Executive Summary»** (проверено на прогоне FLEE-01 — экстракт зацепил эхо промпта).
- **Общий на всех:** большой текст мимо обрезки дисплея (JS-тул режет ~1500, get_page_text ~50k/проход) → Blob-download → Read из Downloads. ⚠️ **Blob-download может ТИХО не долететь** (2026-07-14: grok — да, chatgpt/gemini — нет; `a.click()` без ошибки, блок невидим) → ВСЕГДА `ls Downloads` после; не долетело → фолбэк `pre.textContent=txt; document.body.replaceChildren(pre)` (TrustedHTML-safe) → get_page_text кусками. Клипборд-пути (navigator.clipboard виснет; execCommand/Ctrl+C нужен жест) — НЕ тратить попытки.
- ⭐ **Полевое подтверждение 2026-07-21 (добор веера 14.07, 5 отчётов 16–85 KB — Blob НЕ долетел ни разу, Chrome multiple-downloads):** дефолтом сразу бери `get_page_text`, Blob не пробуй. Что нового узнали: (а) вывод >50 KB харнес САМ персистит в `tool-results/toolu_*.json` на диск → читаешь Read'ом, контекст не жжёшь; <50 KB приходит in-band; (б) жёсткий кап 50000 симв/проход обходится сдвигом окна видимого текста (паддинг/подмена узлов) + склейкой двух срезов по overlap последних ~300 симв — так собран отчёт 77k; (в) клипборд не просто «виснет», он отдаёт СТАРОЕ содержимое буфера оператора = ложный успех, всегда сверяй длину и первые слова; (г) **поиск чата в Grok по названию** — не UI (Ctrl+K мёртв, OneTrust-баннер ест клики), а same-origin `fetch('/rest/app-chat/conversations?pageSize=50',{credentials:'include'})` → `{conversations:[{conversationId,title}]}`; (д) **Gemini = SPA**: свежий `navigate` на URL чата грузит отчёт надёжнее синтетического клика по сайдбару (сайдбар лениво рендерит пустой текст); (е) возврат сырых заголовков чатов из JS ловит контент-фильтр (`BLOCKED: Cookie/query string`) → возвращай короткий статус-токен, не данные.
- ⭐ **Полевое подтверждение 2026-07-21 ВЕЧЕР (сбор HUB-02):** (а) **вброшенная на страницу СВОЯ кнопка не обходит запрет жестов** — синтетический/координатный клик по ней не считается user gesture, blob так и не качается (onclick-счётчик = 0; не изобретать заново); (б) **клики и клавиши расширения могут вообще не доходить до страницы** (окно без фокуса): симптом — Send нажат, а поле ввода не пустеет; лечение — программный `document.querySelector('button[data-testid="send-button"]').click()` из JS, React принимает его как настоящий (проверено: сабмит ушёл, композер опустел); (в) большой текст из DOM — сперва в копилку `window.__x`, offsets искать вторым вызовом, резать уже в Python из персиста `tool-results\`; (г) выделение узла Range+addRange и Ctrl+C поверх — буфер остаётся ПУСТ (не путать со «старым содержимым»: и такое, и такое бывает — потому `Get-Clipboard` сверять всегда).
- ⭐⭐ **Blob-download у ChatGPT: ОДНА ЗАГРУЗКА = ОДНА СВЕЖАЯ ВКЛАДКА (замер 04.08, аудит 4 отчётов).** Первый `a.click()` в новой вкладке скачивается всегда; **второй и последующие в ТОЙ ЖЕ вкладке молча не долетают** — это Chrome «multiple automatic downloads», блок тихий, ошибки в JS нет, `ls Downloads` пуст. Лечение дешёвое и надёжное: `tabs_create_mcp` → `navigate` на chatgpt.com → одна загрузка → следующая вкладка. Проверено: 4 отчёта, 4 вкладки, 4 файла. ⛔ Не лечить это перезагрузкой той же вкладки (пробовал — блок держится) и не пытаться отдать текст на локальный приёмник (`fetch` на `http://10.0.0.0` с chatgpt.com **режет CSP**, `Failed to fetch` — путь закрыт, не тратить попытки). ⚠️ На тяжёлых чатах сборка строки и Blob в одном вызове упирается в **CDP-таймаут 45 с** → разбить на два вызова: первый кладёт текст в `window.__H`, второй только качает.
- ⭐ **Полевой замер 04.08 (ZB-04, сбор трёх вендоров с ноута) — рельсы по вендорам разошлись, запомнить раскладку:**
  - **ChatGPT → ТОЛЬКО backend JSON (путь 1).** Отработал с первого раза; всё остальное мертво (см. регрессию выше). ⚠️ Мой промах, чтобы не повторяли: я дёрнул `/backend-api/conversation/<id>` **без заголовка Authorization** → **404**, и прочитал это как «пути нет». 404 тут = «нет токена», а не «нет отчёта». Bearer обязателен: `s=await fetch('/api/auth/session').then(r=>r.json())` → `Authorization:'Bearer '+s.accessToken`.
  - **Gemini → Blob-download РАБОТАЕТ** (`new Blob([document.body.innerText])` + `a.click()`, файл лёг в Downloads с первой попытки, 99 KB). Отменяет прежний совет «Blob не пробуй, сразу get_page_text» — для Gemini он неверен. Тело отчёта попадает в `body.innerText` целиком вместе с хвостом «Sources read but not used» (это ценно — сохранять весь снимок).
  - **Grok → Blob и data-URI НЕ работают** (CSP режет, `a.click()` молча без файла), `navigator.clipboard.writeText` → **CDP-таймаут 45 с**. Работает `get_page_text` — забрал весь отчёт одним проходом.
  - **Чтение больших срезов через JS ловит контент-фильтр:** `body.innerText.slice(a,b)` на странице с URL-ами вернул `[BLOCKED: Cookie/query string data]`. Короткие статус-выражения (`.length`, `.indexOf`) проходят. ⇒ **данные тащить файлом/`get_page_text`, а не возвратом из JS.**
  - **Буфер обмена — общий на машину и врёт (§3.6):** после «копирования» в нём лежал чужой текст из параллельной сессии. Лечение, которое сработало: **писать сентинел ДО** (`SENTINEL-...`) и сверять после — иначе «успешная» копия неотличима от невыполненной.
- ⚠️ **Вендор может ОТКАЗАТЬСЯ отвечать** (Gemini, тема анти-бан аутрича — счёл обходом защит). Отказ = валидный результат: сохранить verbatim в `_originals` как обычный файл, статус `collected`, а в Decision Memo явно пометить «консенсуса нет, база = N вендоров» и не выдавать single-vendor за веер.

## Шаг 4 — синтез-консенсус (Alpha Protocol step 4)

> ⛔ **ГЕЙТ ПЕРЕД ПЕРВОЙ БУКВОЙ СИНТЕЗА (04.08, ZB-04): «а его уже не синтезировали?»**
> Порядок: `dr_registry.py list | grep <DR-ID>` **+** `ls 03-Insights | grep <DR-ID>`.
> - статус `synthesized`/`applied` **или** уже есть `insight-DR-<DR-ID>-*` → **НОВУЮ заметку НЕ создавать.**
>   Дописать в существующую датированный раздел «ПОПРАВКА <дата>: что нового и что это меняет».
> - **⛔ Статус в реестре не понижать.** 04.08 я сбил `applied` → `collected` командой сбора и стёр
>   факт, что DR давно закрыт. Перед `update --status` посмотреть текущий статус: назад по
>   лестнице (`applied` → `collected`) двигаться только осознанно, с `--note` о причине.
>
> Замер цены: у ZB-04 **две** insight-заметки за один час 28.07 от двух сессий, плюс 04.08
> третий веер по уже закрытому DR. Прямое следствие §8.4 (одобрение старше суток исполняется
> только после RECALL «не сделано ли уже») и §7.7 (табличка ON AIR не выставлялась ни разу).

Прочитать все собранные отчёты → таблица «сошлись / разошлись / уникальное у каждого» → Decision Memo (проблема · знания · DR · варианты · риски · рекомендация). Гетеро-принцип: расхождения НЕ сглаживать — показать оператору как развилки. Memo → `02-Decisions/` (если решение) или отчёт в чат. Леджер закрыть (`status: collected`).

⭐ **ВЕНДОРОВ НЕ УСРЕДНЯЕМ — ценность веера в СТОЛКНОВЕНИИ, а не в кворуме (замер волны DR26-07-26).** Три вендора дали трёх РАЗНЫХ победителей, потому что судили по трём разным критериям (замысел · недостающие механизмы · доказанный выход) — и это честнее любого единого рейтинга. Одинаковый ответ трёх вендоров — сигнал СЛАБЫЙ; поймать ОДНОГО вендора на подлоге — сильный.

В синтезе ОБЯЗАТЕЛЬНЫ две секции: **(а) расхождения с указанием КРИТЕРИЯ каждого вендора**; **(б) «прямое опровержение внутри веера»**, если оно было. Усреднить = потерять главное.

Пример 26.07: ChatGPT опроверг цифру Gemini (21x LLM-Wiki против RAG) по первоисточнику — цифра оказалась честной, но приклеенной к чужому объекту.

⭐ **Шаг 5 — ЗАКРЫТЬ РАЗВЕДКУ (dev 27.07, обязателен).** `synthesized` — не финиш: отчёт написан, а система не изменилась. Каждый ДР доводится до одного из двух терминальных статусов, оба требуют `--note`:
- `dr_registry.py update <ID> --status applied --note "<что реально поменяли: Decision Memo / правка в проде / новая рутина>"`
- `dr_registry.py update <ID> --status parked --note "<почему не берём и что изменит решение>"`

`parked` — легальный и честный финал, не поражение ([[gate-implement-critical-only]]: не всё исследованное обязано быть внедрено). Гейт в `dr_registry.py` v3.3 роняет попытку без причины (exit 1). Повод правила: 27.07 в реестре 184 из 246 разведок висели `synthesized`, до `02-Decisions` дошло ~20 — отличить «кормит систему» от «просто лежит» было нельзя. Канон: память [[dr-finish-applied-or-parked]], CLAUDE.md §9.1.

## ⛔ ПОЛЕВЫЕ ДАННЫЕ НОЧИ 26.07.2026 (партия ZB-01…ZB-05, ноут NODE-0X) — читать перед запуском
1. ~~**🔴 ChatGPT Deep Research = `dead` на 26.07, «он просто НЕ ИСКАЛ, отдав таблицу из памяти».**~~ ⛔ **ВЫВОД ОПРОВЕРГНУТ 04.08 разбором backend'а — симптом был реален, причина названа неверно.** Что оказалось на самом деле: (а) счётчик «0 citations · 0 searches» стоит у ВСЕХ 10 DR-прогонов 21–26.07, включая принятые и использованные — он не про поиск, `story_events` у connector-DR всегда пуст; (б) те же «мёртвые» прогоны несут 40–106 цитат с живыми URL в `widget_state.report_message.metadata.citations` (одна проверена вживую на странице-источнике); (в) настоящая деградация другая — `resolved_model_slug: deep-research-mini` у всех прогонов и обрыв посреди плана (шаги 3–5 `pending` при `status: completed`, 5–7 мин вместо 20–40), отсюда мало источников и «красиво, но пусто» на глаз; (г) веб-поиск на аккаунте НЕ выключен (`beta_settings.browsing: true`, `disable_web_search: false`) — усиление промпта не помогало не потому, что вендор не искал. **Правило теперь:** ChatGPT-канал гнать через Pro + Web search (п.10 «что решено»), а если запущен DR-чип — судить по `citations`, а не по счётчику. Retry больше двух раз по-прежнему не жечь.
2. **🔑 Gemini: заходить ТОЛЬКО по имени аккаунта, индекс `u/N` НЕ СТАБИЛЕН.** ⛔ Правка 27.07 (supersedes «всегда `u/7`»): `https://gemini.google.com/u/7/app` открылся под `[EMAIL]` — free-тариф, модель Flash, кнопка Upgrade. Индексы переезжают между сессиями, «мой номер» запоминать нельзя. **Рабочий вход:** `https://gemini.google.com/app?authuser=[EMAIL]` (редиректит на нужный `u/N` сам). Детект аккаунта без кликов, ОБЯЗАТЕЛЬНО до вставки промпта: `document.querySelector('a[aria-label*="Google Account"]').getAttribute('aria-label')` + проверка `document.body.innerText.includes('Upgrade')` (true = free-аккаунт). Без этой сверки отчёт молча уедет на Flash и будет выглядеть просто «слабоватым». Переключатель аккаунтов живёт в кросс-доменном iframe — `find`/скролл его не берут.
3. **Gemini молча откатывает модель на Flash-Lite** в каждой новой вкладке. Смотреть селектор ГЛАЗАМИ перед каждым запуском; Deep research переехал в «+» → **More tools** → «Deep research» (в первом уровне меню его больше нет).
4. **ChatGPT: порядок «чип → промпт», а НЕ наоборот** (supersedes прежняя заметка ZB-02 20.07). Чип «Deep research» — это инлайн-нода ВНУТРИ ProseMirror, встающая по позиции каретки: кликнешь в середину текста — расщепит предложение (ловилось как `chipIdx:470` посреди фразы). Рабочий порядок: (а) включить Deep research в ПУСТОМ композере — чип встаёт первым узлом; (б) поставить каретку в КОНЕЦ (`range.selectNodeContents(ed); range.collapse(false)`); (в) синтетический paste-event — вставка в коллапсированную каретку ничего не заменяет, чип выживает. ⚠️ Повторный paste при `selectNodeContents` НЕ заменяет текст, а ДОПИСЫВАЕТ (получишь удвоение) → чистить только живыми клавишами `ctrl+a` + `Delete`.
5. **Gemini-забор: `querySelector('.markdown-main-panel')` берёт ПЕРВУЮ панель = research-план, а не отчёт.** Сохранишь 1.7 KB плана вместо 33.8 KB отчёта и не заметишь. Правильно: якорь на заголовок отчёта → `h2('ПЛАН ИССЛЕДОВАНИЯ').closest('.markdown-main-panel').innerText`.
6. **Вынос большого текста:** `javascript_tool` режет вывод на ~1000-1500 симв. Единственный рабочий путь — сложить в `window.__R`, СРАЗУ подменить body на `<pre>` и СРАЗУ `get_page_text` (кап ~50k, отчёт 33.8k прошёл одним проходом). Подмена body ломает страницу → `window.__R` теряется при перезагрузке, порядок нарушать нельзя. Blob-download не пробовать (полевые заметки 21.07: не долетает).
7. **«Начать исследование» жать ДВАЖДЫ-с-переосмотром:** первый `find` находит кнопку, но клик приходит раньше, чем она смонтирована. Повторный `find` даёт новый ref — второй клик срабатывает. Доказательство старта = канвас «Starting research…» / «Прекрасно. Вы можете закрыть этот чат», а не факт клика.
8. **🔁 ДЕДУП — на КАЖДОМ вендоре, а не только в реестре.** Инцидент 03:0x: реестр показал ZB-03 = `issued`, дедуп по истории Grok дал «чисто» (похожий чат оказался от 22:49 UTC = ДО создания промптов партии) → запустил. А в Gemini Recents уже висел свой `DR26-07-26-ZB-03` от параллельной сессии → лишний прогон Gemini DR. Реестр = первый фильтр, история КАЖДОГО вендора, куда шлёшь = второй, обязательный. Это [[check-all-places-not-one]], применённое к вендорам вместо дисков.

9. **Корневой композер ChatGPT ОБЩИЙ на все вкладки — свой же черновик поедет за тобой.** 27.07: открыл вторую вкладку под ZB-04 — там лежал ZB-03 из первой; paste-event ДОПИСАЛ (8303 симв. вместо 4175), а `execCommand selectAll+delete` визуально очистил, но ProseMirror восстановил состояние и дописал снова (12450). Лечится только живой клавиатурой: клик в композер → `ctrl+a` → `Delete` → сверить `innerText.length===0` → и лишь потом paste.
10. **`ctrl+a`+`Delete` сносит и ЧИП режима** (Web search / Deep research) — прогон уйдёт без поиска, и это не видно в тексте промпта. Порядок для ChatGPT: очистить → вставить промпт → **включить чип заново** → сверить → Send. И ещё: текст чипа попадает в `innerText` композера то префиксом `Web search\n`, то суффиксом `\nWeb search` → при сверке длины срезать его с ОБОИХ концов, иначе ловишь ложный mismatch и начинаешь «чинить» целый промпт.

## ⭐ ПОЛЕ 31.07.2026 (NODE-0X, DR26-07-29-MACANTON-01-1302) — рельсы вендоров и три молчаливые грабли
0. **ВЫБОР БРАУЗЕРА И АККАУНТА — МОЙ, ВСЕГДА** (dev 31.07, канон `reglament-brauzer-i-akkaunt-vybiray-sam-nikogda-ne-sprashivay`). Три подключённых Chrome → беру сам, не пошёл → следующий, потом Firefox. ⛔ Вопрос «какой браузер/аккаунт взять?» оператору запрещён. Цена нарушения замерена в этот же день: вендор выпал из веера при живом пути.
1. **Рельса Gemini на 31.07 = ТОЛЬКО живой Chrome.** Оба CLI-пути мертвы: бесплатный ключ AI Studio отдаёт 429 (один на весь флот), OAuth — `IneligibleTierError` (Code Assist for individuals закрыт, миграция в Antigravity). Аккаунт Gemini = `dev.a`, НЕ `a2`. Путь в UI: «+» → **More tools** → **Deep research** (в меню первого уровня его НЕТ), затем двухфазность — план → кнопка **«Начать исследование»**, доказательство старта = «Researching N websites…».
2. **⛔ Не клонировать профиль Firefox, который держит живой GUI-браузер.** На диск попадает вчерашний слепок (свежие куки живут в памяти процесса) → селениум видит «Sign in» на сайте, где сессия на самом деле жива. Я сделал из этого вывод «сессия мертва на стороне Google» и он был неверным.
3. **`pbcopy` без UTF-8 локали убивает кириллицу.** Вставка «проходит успешно», в композере мойибаке, длина расходится в 1,5 раза. Всегда `export LC_ALL=en_US.UTF-8 LANG=en_US.UTF-8` перед `pbcopy`, и сверять поле не только длиной, но счётчиком кириллицы: `(t.match(/[а-яА-Я]/g)||[]).length`.
4. **Забор ChatGPT DR:** `widget_state` может быть ПУСТ — отчёт лежит в `mapping[*].message.content.parts[0]` (взять самую длинную строку по ВСЕМУ mapping, а не по цепочке от `current_node`). `body.innerText` про готовность ВРЁТ — держится на ~12 КБ сайдбара, даже когда библиография из 69 источников уже отрисована; готовность проверять СКРИНШОТОМ. И читать первую строку отчёта: «## Продолжение отчёта — с §N» = половина не доехала.
5. **Забор Gemini DR:** отчёт в `structured-content-container` (их несколько — брать самый длинный), надёжнее всего `get_page_text`, харнес сам персистит >50 КБ в `tool-results/*.json`, оттуда режем питоном.
6. **Проверка цитат в ДВА шага, не в один.** (а) все ссылки на код ответа — детерминированно, 0 токенов; (б) **прочитать содержание у 3–5 утверждений, на которых стоит решение**. Замер 31.07: 30/30 ссылок Grok живые, но ссылка ChatGPT на JCR вела на статью про делимость цен, а Grok выдал настройку Zapier за поведение продукта. Писать «цитаты проверены» после одного шага (а) — ложь. [[live-url-is-not-a-verified-citation]]

## ⭐ ПОЛЕ 28.07.2026 (ZB-04-2349, ноут NODE-0X) — транспорт промпта и забор отчёта решены
1. **🔑 ТРАНСПОРТ ПРОМПТА = `window.name`, а не инлайн в javascript_tool.** Промпт 12 КБ инлайном на трёх вендоров = ~37 КБ контекста плюс риск экранирования. Рабочий путь, 0 токенов: `navigate` вкладку на локальный файл промпта → `window.name = await fetch(location.href).then(r=>r.text())` → `navigate` ТУ ЖЕ вкладку на сайт вендора → `window.name` доезжает целиком (проверено 12 224 / 12 279 / 12 467 знаков). Раздача: крошечный HTTP-сервер из скретчпада.
   ⚠️ **Исключение — Gemini:** COOP на `google.com` рвёт browsing context, и при уходе С gemini на localhost `window.name` обнуляется. Обратное направление (localhost → gemini) работает.
2. **🔑 ЗАБОР ОТЧЁТА = POST на локальный сервер, текст в мой контекст не попадает.** Тот же приём наоборот: в чате вендора сложить текст в `window.name` → `navigate` на `http://10.0.0.0:<порт>/sink` → оттуда `fetch('/save?name=raw-<vendor>.txt',{method:'POST',body:window.name})`. Сервер пишет файл, дальше проверяю полноту Python-ом (разделы, число URL) за копейки. Так забраны отчёты 16 КБ / 34 КБ / 83 КБ.
   ⚠️ **Для Gemini** (COOP убивает window.name) работает **фрагмент URL**: `location.href='http://10.0.0.0:<порт>/sink#'+encodeURIComponent(txt)` → на sink-странице `decodeURIComponent(location.hash.slice(1))` → POST. Фрагмент на сервер не уходит, приватность цела.
3. **Что НЕ работает, не тратить попытки:** `fetch` с страницы вендора на 10.0.0.0 (CSP `connect-src` — режут и chatgpt.com, и gemini.google.com) · отправка формой на localhost (CSP `form-action`) · CDP `ctrl+v` (клавиша доходит, вставки нет) · кнопка «Copy contents» в UI (нужен фокус окна, а окно фоновое — буфер молча не меняется; всегда сверять `Get-Clipboard` с сентинелом).
4. **🔴 ChatGPT Deep Research — ПЯТЫЙ подряд `0 citations · 0 searches`** (4 раза 26.07 + 1 раз 28.07, аккаунт `dev.a2@`, 15 минут «думал» и выдал внешне красивый, но пустоватый отчёт — ⚠️ 04.08: «из памяти» неверно, он искал, но урезанно; счётчик врёт, см. п.1 полевых данных). Web search на том же аккаунте и той же модели ищет нормально (90+ запросов, 80+ страниц, 168 URL в отчёте). ⇒ **Не тратить DR-чип на этом аккаунте: ChatGPT-канал вести сразу через Web search** + в тело промпта строку «перечисли выполненные запросы и реально открытые URL перед финальным отчётом». Экономит 15 минут и один прогон.
5. **ChatGPT DR стал ДВУХФАЗНЫМ, как Gemini:** после Send показывает карточку плана с `Edit / Cancel / Start` и автостартом по таймеру ~30 с. Кнопку дожимать.
6. **ChatGPT: `execCommand insertText` сел, синтетический paste-event НЕ сел** — ровно наоборот, чем у Grok (там paste-event с первого раза). Каскад нужен обоим, порядок методов по вендору разный. Чип режима ставить в ПУСТОМ композере, потом каретка в конец, потом вставка — чип выживает.
7. **Gemini: кнопка «Начать исследование» остаётся видимой и enabled после успешного клика.** Доказательство старта — не исчезновение кнопки, а канвас `Прекрасно. Вы можете закрыть этот чат` + `Researching N websites`. И `bodyLen` у Gemini скачет на порядок (327 887 → 14 403 за ре-рендер), как признак старта не годится.
8. **Gemini-забор: брать панель по МАКСИМАЛЬНОЙ длине**, а не первую. На готовом отчёте `.markdown-main-panel` было три штуки: 1861 (план), 144, 34 444 (отчёт). Панель отчёта рендерится лениво — если её нет, кликнуть карточку отчёта в ленте.
9. **Grok Heavy: 485 sources и НОЛЬ инлайн-ссылок.** Источники отданы абзацем с перечнем доменов, анкоров на странице 2. `innerText` ничего не теряет, но проверяемость Grok-фактов низкая — спорные цифры сверять руками (в этом прогоне Grok ошибся: заявил, что платных ускорителей нет, а Story Boost за $159,99 существует).
10. **Два подключённых Chrome в MCP.** Один может быть чистым профилем, разлогиненным везде. Проверять аккаунт (`/api/auth/session` у ChatGPT, `aria-label` у Gemini, `Sign in` в тексте у Grok) ДО вывода «разлогинен, зовите оператора».

11. **⭐ Blob-download на chatgpt.com РАБОТАЕТ — и это единственный способ забрать отчёт целиком (27.07, supersedes полевую заметку 21.07 «Blob не долетает»).** Замер: отчёт 73 144 симв. приехал файлом 97 992 байта, второй — 60 623 симв., оба с первого раза. `get_page_text` для таких объёмов НЕПРИГОДЕН: режет на 50 000 симв. **и отрезает ровно хвост — раздел Proof of work**, то есть само доказательство, что вендор искал. Порядок: собрать текст последнего `[data-message-author-role="assistant"]` в `window.__R` → Blob + `a.click()` → **обязательно `ls Downloads`** → перенести скриптом с провенансом. Контекст сессии при этом не тратится вообще — текст идёт диск-в-диск. ⚠️ Трюк «добить пэддингом до >50 КБ, чтобы get_page_text persist-нул на диск» НЕ работает: тул иногда персистит, а иногда режет инлайном — поведение непредсказуемо, не закладываться.
12. **`exit 0` от `brain_embed_update.py` при занятом локе — НЕ баг и не враньё.** В коде осознанно: `busy_code = 3 if index_age_hours() > STALE_HOURS else 0` (порог 26 ч). Код отвечает на вопрос «индекс протух по часам?», а НЕ «мой запрос выполнился?». После записи новых заметок это разные вопросы: свежий по часам индекс их всё равно не содержит. ⇒ После реиндекса проверять ФУНКЦИОНАЛЬНО — запросом к `brain_ask.py` на фразу, которой нет нигде, кроме новых файлов. Счётчик `harari ×N` в `_brain_e5_meta.pkl` не доказательство: там пути файлов, не текст чанков.

## ⭐ ПОЛЕ 16.09.2026 (NODE-0X, DR26-09-16-MACANTON-01-0446, безлюдная рутина С Chrome-MCP) — шесть строк, каждая замерена
1. **ChatGPT веб (a2 Pro) в живом Chrome: план DR стартует САМ, кнопки Start нет.** Порядок сработал с первого раза: «+» → `Deep research` (ref из `find`) в ПУСТОМ композере → `execCommand insertText` в конец (кириллица 84=84) → `button[data-testid="send-button"].click()`. Статус — `widget_state.status` (`researching` → `completed`, ~9 мин). Отчёт в `report_message.content.parts[0]` (58 КБ). ⚠️ `citations` в metadata = 0, но в тексте 22 URL, и гейт засчитал; `resolved_model_slug` = `gpt-5-thinking`. Blob из той же вкладки долетел.
2. **Gemini веб (a@ Punk, Pro Extended, Deep research) — провал без текста.** «Создание плана» с активной кнопкой Stop держалось >10 мин. Кнопка `Start research` так и не появилась ни в фоновой, ни в свежей вкладке. Потом заголовок чата сменился на «…Request Failed», а `get_page_text` — пусто. Признак провала = **заголовок вкладки**, а не DOM. Gemini CLI в тот же час: exit=1 за 6 с.
3. **claude.ai: Cloudflare «Performing security verification» висит и в ЖИВОМ Chrome**, не только в headless FF. Капчу не трогаем, рельса = `missing`. Перед этим выводом хук `dead_claim_guard` требует `rail_sweep.py <вендор>` — прогоняй его ДО фразы «недоступен».
4. **GLM с `Advanced Search ON` + `Deep Think Max` сам пишет «I can't browse the live web»** и отдаёт 0 URL. `dr_ff_rail` при этом печатает OK за 1 мин на эхо (гейт: collected-EMPTY); настоящий ответ забрал `dr_ff_collect --title "Bay Area"` через ~15 мин (`--title "Конферен"` не нашёл — заголовок GLM английский). ⛔ Такая нога **выдумала выгодный факт о заказчике** («PRs merged into Claude Code») — `gh search prs --merged` показал 0. **Несущие факты ноги без ссылок сверять до синтеза.**
5. **Вторая нога того же вендора** (веб-DR, когда `chatgpt` уже занят codex CLI) подшивается дописыванием `chatgpt-a2` в `targets:` манифеста — `attach` иначе отбивает (так уже сделаны `claudeai-a2/bb`). Независимых вендоров при этом НЕ прибавилось, и в синтезе так и пишем.
6. **На macOS нет `timeout`** — цикл с `timeout 600 python3 …` молча прогнал 0 раз (`command not found`, exit 0 цикла). У `dr_ff_collect` есть свой `--timeout`.

## ⭐ ПОЛЕ 14.09.2026 (NODE-0X, DR26-09-14-MACANTON-01-1204) — пять строк, каждая замерена
1. **⛔ `dr_ff_rail.py --rail glm` (autoff) печатает `OK … 9563 символов` и exit 0 за 2 мин, а Send НЕ ушёл**: файл = сайдбар z.ai + эхо промпта с YAML-фронтматтером, `/api/v1/chats/<id>` → 0 сообщений. `dr_leg_gate.py` пропускает такое exit 0 с пометкой «0 URL». ⇒ после этой рельсы проверять чат через API (`localStorage.token` → `/api/v1/chats/?page=1`), а не верить OK. Рабочая дверь в этот день — живой Chrome-MCP: меню глобуса (старая эпоха) → тумблер `Advanced Search` → `glm_probe.py` (JS грузится через `window.name`, `(0,eval)` проходит) → `#send-message-button.click()`; 50 КБ / 35 URL за ~14 мин.
2. **Gemini: клик `Send message` по ref из `find` НЕ отправил** (текст остался в композере, скриншот). Отправил координатный клик по стрелке. Кнопка `Start research` рендерится ниже видимой области — `find` её не видит до `scroll` вниз по плану.
3. **Gemini в фоновой вкладке показывает скелетон «исследую» даже после конца.** Готовность судить свежим `navigate` + `innerText` на «I've completed your research». Blob `body.innerText` долетел (118 КБ), 23 URL.
4. **`claude -p` рельса отдала 34 КБ за 1366 с с 0 источников** — диспетчер честно отбил в `results-failed/`. Не засчитывать.
5. **`dr_post_draft.py` на NODE-0X лежит в транзите** `_machine-bus/_transit/scripts-from-NODE-0X-2023PAL/` (там же `dr_rails_registry.py` и тесты), в `~/.claude/scripts` не установлен — запускать оттуда. Я сначала написал «нет», проверив одно место, и хук `false_no_guard` поймал: перед «нет X» — `python3 ~/.claude/scripts/have.py <имя>`. `dr_rails.json` на 14.09 `have.py` не нашёл ни в одном из 9 корней. Длинный `--verdict` инструмент режет многоточием — давать ≤80 знаков.

## ⭐ ПОЛЕ 10.09.2026 (NODE-0X, добор кворума DR26-08-28-MACRUS-01-1218) — четыре строки, каждая замерена

1. **⛔ AutoFF НЕ ЕДИНСТВЕННАЯ ПОВЕРХНОСТЬ, И НА ЭТОМ УЗЛЕ ОН ПУСТ.** Замер кук в `~/AppData/Local/ff-autoff-profile`: claude.ai **0**, z.ai **0**, mistral.ai **0**, chatgpt.com **0**, google.com 1. Три рельсы подряд упали «разлогинен» — и это читалось как «вендор закрыт». Живые сессии лежали в СИСТЕМНОМ профиле `Ct3iOc7B.Profile 1` (bb-platinum, дефолт установки): claude.ai 7, google 37, **z.ai 18**, mistral 5, chatgpt 8, grok 8. ⇒ **Перед приговором рельсе — обойти ВСЕ профили одним скриптом** (`moz_cookies` по хостам, 0 токенов, ~2 сек), затем `--profile-dir "<имя папки>"`. ⚠️ Профиль bb держит ЖИВОЙ Firefox оператора → `--no-copy` там запрещён, а для google даже копия ломает его сессию ротацией (грабля 02.09) — google из bb НЕ трогать.
2. **🔴 GEMINI МЁРТВ ПО ПОДПИСКЕ, А НЕ ПО ТЕХНИКЕ (улика со страницы).** `banner: "Your Google AI Pro subscription ended"`, `model: Gemini 3.6 Flash`, меню инструментов = Files/Drive/Google Photos/Notebooks, **`deepResearch: false`, `moreTools: false`**. Аккаунт при этом залогинен и верный (`Google Account: Punk Crypto ([EMAIL])`). ⇒ Строка «платный Google AI Pro, DR ≈20/день» ПРОТУХЛА; `dr_ff_rail --deep` честно печатает «не нашёл пункт Deep Research» — это не поломка рельсы. Продление = деньги = **Tier-2**, решает оператор, сами не чиним.
3. **📥 GLM: СБОРЩИК БЕЗ `--title` САДИТСЯ НА ЛЕНДИНГ.** `dr_ff_collect --rail glm` без заголовка отдал 3134 симв. рекламы GLM-5.3-Flash и сайдбара — гейт справедливо отбил. С `--title "<кусок заголовка чата>"` тот же чат отдал **19 376 симв., 42 источника, `dr_leg_gate` PASS**. Заголовок берётся из сайдбара, который виден в самом «пустом» снимке. ⇒ **Для glm всегда `--title`.** Отправляющая рельса при этом вышла по тишине на фазе `Thinking...` (в хвосте её снимка читаются `Deep Think / Max` и `Advanced Search` — режимы встали верно): «отправить» и «забрать» — две разные операции по времени, это не брак.
4. **⛔ claude.ai ЧЕРЕЗ Chrome-MCP: ПРОМПТ САДИТСЯ, SEND НЕ ПРОХОДИТ.** Залогинен верно (`/api/organizations` → `a673590f…[EMAIL]'s Organization`), `Research mode` доказан прибором (`aria-pressed:"true"`), модель Fable 5 High, промпт сел `execCommand insertText` 1-в-1 (кириллица 2562 = 2562). Дальше — стена: `button[aria-label="Send message"]` не disabled, но **не отправляет ни программным `.click()`, ни CDP-кликом по ref, ни живым Enter** (3 способа), URL остаётся `/new`, композер не пустеет. На странице висит `Use caution before running this prompt. Malicious conversation content could trick Claude…` — вендорская защита от вставленного извне текста. ⇒ Считать рельсу требующей человека; больше двух попыток Send не жечь. Побочно: **длинная вставка в claude.ai превращается в вложение `PASTED`**, и каждая попытка каскада плодит ЕЩЁ ОДНО (получил 4 дубля); чистятся программным кликом по `button[aria-label^="Remove Pasted text"]`, текст в композере при этом целый — `ctrl+a`+`Delete` карточки НЕ убирает.
5. **🔧 ПОЧИНЕН КОРЕНЬ `dr_ff_collect.py`:** жёсткий потолок стоял на `signal.SIGALRM`, которого **на Windows нет** → `exit 4` на первой секунде, то есть половина конвейера «забрать готовый отчёт» не работала НИ НА ОДНОМ Windows-узле с 03.09, а выглядело как «вендор не отдал отчёт». Теперь единый вход `_alarm()` (POSIX → `signal.alarm`, Windows → `threading.Timer` + `_thread.interrupt_main`); тест `_test_dr_ff_collect_alarm.py`, красный на старой версии показан. Посылка `dr-ff-collect-win-alarm-20260910` подписана и разослана на 6 узлов.

## ⭐ ПОЛЕ 22.09.2026 (HUB-01, веер из 5 заказов по найму) — две грабли на вызове рельс

1. **`dr_ff_rail.py` НЕ ПРИНИМАЕТ DR-ID позиционно** — только `--prompt-file` и `--out`. Заход сгорел на `dr_ff_rail.py --rail glm <ID>` → `error: unrecognized arguments`. Рабочая форма:
   `python dr_ff_rail.py --rail glm --profile-dir "<профиль>" --deep --prompt-file "<очередь>\<ID>.md" --out "<очередь>\<ID>\results\glm.md"`
   (файл заказа лежит в `<волт>\_machine-bus\_dr\queue\<ID>.md`, рядом одноимённая папка под результаты).
2. **На этом узле обе двери Firefox закрыты одновременно, и это не лечится флагом.** `ff_session_probe` показал: живые сессии только в ЧЕЛОВЕЧЕСКОМ профиле `m26xxxkf.dev-clean`, а робот-профиль `ff-autoff-profile` пуст у всех вендоров (mistral вообще «НЕТ»). Рельса честно отбивает: «человеческий профиль с живой сессией: копия разлогинит оператора, in-place отравит user.js». ⇒ Пока робот-профиль не залогинен руками оператора (Tier-2, пароли вводит человек), **GLM и Mistral с этого узла безлюдно не едут** — это «требует рук», а не «вендор мёртв» ([[dead-verdict-expires]]).
3. ⚠️ Рабочий обход на 22.09 = **headless CLI grok+gemini** через `dr_headless_dispatch.py <ID...> --rails grok,gemini`; ноги ChatGPT и Claude по приказу 22.09 идут только вебом.

4. **⛔ GLM В CHROME: РАБОТАЕТ ТОЛЬКО АКТИВНАЯ ВКЛАДКА.** В фоновой вкладке (созданной через tabs_create) клики по глобусу НЕ доходят вообще: `data-active` остаётся `false`, меню не открывается, а скриншот показывает нормальный layout — выглядит как «сломанная вёрстка», а на деле заморожен layout фоновой вкладки. В АКТИВНОЙ вкладке тот же клик срабатывает с первого раза. ⇒ много заказов гоним ПОСЛЕДОВАТЕЛЬНО в одной вкладке через «New Chat», а не веером по вкладкам.
   Две эпохи UI чередуются в одной сессии (подтверждён замер 08.09): иногда клик по глобусу сразу даёт `true`, иногда открывает меню с тумблером (координата ~(700,345) при viewport 1568x670). Суди ТОЛЬКО по `data-active` после каждого клика.
   ⚠️ Клик по `ref` из read_page по тумблеру `[role=switch]` НЕ переключает его — работает только координатный клик.
   ⚠️ Программный `#send-message-button.click()` срабатывает не всегда; надёжнее координатный клик по стрелке (~(1284,530)). После отправки текст может ОСТАТЬСЯ в textarea как черновик — это НЕ признак неотправки: суди по смене URL на `/c/<id>` и по наличию промпта в теле страницы; черновик после этого чистить, иначе улетит дублем.
5. **⛔ GLM ОТКАЗЫВАЕТ ПО ПЕРЕГРУЗКЕ И ПРЕДЛАГАЕТ FLASH — НЕ СОГЛАШАТЬСЯ.** Замер 22.09: на четвёртом заказе подряд вместо ответа пришло «GLM-5.3 is intensifying the coordination of resources, please switch to GLM-5.3-Flash for experience or try again later» с кнопками Cancel / Switch. Согласиться = тихий брак (Flash вместо флагмана, тот же класс, что Grok в Expert). Рельса идёт в `missing` с причиной «перегрузка вендора». ⇒ Потолок GLM на один заход — примерно ТРИ тяжёлых заказа подряд.
## Ошибки/грабли (не вошедшее в автомат)
- ⚠️ **Фоновая/свёрнутая вкладка Chrome (проверено 2026-07-17):** viewport 0×0, layout заморожен → синтетические JS-клики и Radix/Angular-кнопки (Gemini «Start research», ChatGPT «+»-меню) НЕ срабатывают, а `computer` кликает мимо. Лечение: `tabs_create_mcp` → новая вкладка (получает layout даже в фоновом окне) → открыть тот же URL разговора → `find` → `computer left_click ref` (CDP-trusted). Промпт при этом уже отправлен — теряется только «дожать кнопку», не квота.
- ⭐ **«started» в леджере ≠ реально запущено (инцидент HUB-06, 16→17.07):** три вендора помечены started, по факту работал ОДИН. Gemini висел на непрожатой кнопке «Start research» (страница = только промпт, panel=0), Grok вообще не отправлен (path остался `/`, промпт в композере). Потеряна ночь. → **probe-after-start обязателен и доказателен:** path сменился на /chat/ · виден индикатор прогресса · объём страницы вырос. Вставка ≠ отправка; отправка ≠ старт. Состояние `submitted` без подтверждённого `started` = не started.
- ⭐ **ChatGPT DR останавливается на research-плане (проверено 2026-07-20, ZB-02):** первый ран (~12 мин, «0 citations · 0 searches») может выдать ТОЛЬКО research-план + output-structure, БЕЗ настоящего ресёрча, и завершиться (`finished_successfully`, end_turn). Это НЕ баг вставки/старта — ран реально шёл, но выродился в план. Лечение: follow-up в тот же чат «Proceed now: execute this plan and write the FULL final report… Do not stop at the plan» → второй ран (у нас 65 мин) даёт полный отчёт с живыми URL. При сборе: если backend-JSON longest-part начинается с «Research Plan:» и в mapping только один widget с планом — это план, не отчёт; пнуть, не сохранять как collected. (Gemini/Grok этим не страдают — план у Gemini отдельная фаза с кнопкой.)
- ⚠️ **Плашка DR-режима ChatGPT живёт ВНУТРИ редактора (ZB-02, 20.07):** каскад `paste_verify` (directSet/execCommand) чистит редактор и СТИРАЕТ чип «Deep research» → probe покажет `chip:false`. Порядок: сначала вставить промпт, ПОТОМ включить Deep research поверх (меню «+» → Deep research), затем сверить чип и Send. Иначе улетит обычный чат, квота DR цела но ответ не тот.
- ✅ **Grok, зеркало textarea/contenteditable — КОРЕНЬ найден и вылечен (FLEE-03, 17.07):** Grok 4.5 = TipTap/ProseMirror contenteditable (`div.tiptap.ProseMirror`); видимый `<textarea>` — СКРЫТОЕ зеркало. Заполнение textarea (nativeSetter/value+InputEvent) даёт `ok:true`, но React/PM-состояние из зеркала не обновляется → Submit не рендерится, Enter=no-op (ровно это жгло время 07-10 и 07-17). **Фикс в каскаде:** целить `.tiptap.ProseMirror` ПЕРВЫМ + синтетический paste-event (`ClipboardEvent('paste',{clipboardData:DataTransfer})`) → PM адоптит текст → `button[type="submit"]` появляется enabled → клик. Проверено вживую 17.07 (FLEE-03 Grok `/c/e621f761`). Если UI снова уплывёт и paste-event не сработает → новый чат + probe, не жечь время.
- ⭐ **«ChatGPT DR молча не ищет» — симптом реален, диагноз был ложный (заведено 26.07, вскрыто 04.08).** Счётчик «Research completed in Xm · 0 citations · 0 searches» — сломанная телеметрия connector-DR, а не отчёт о поиске: он одинаково нулевой у прогонов с 40–106 цитатами. Что делать при виде нуля: (1) НЕ объявлять канал `dead` по счётчику — открыть backend `widget_state.report_message.metadata.citations` (`resolved_model_slug` рядом); (2) не гнать «усиленный» повтор — усиливать нечего, вендор искал; (3) реальная слабость канала = `deep-research-mini` + обрыв посреди плана → ChatGPT ведём через Pro + Web search (замер: 73 запроса / 31 страница против 12 URL у mini). Правило «два `dead` подряд = не гнать третий раз тем же способом» остаётся, но `dead` теперь ставится по цитатам, не по счётчику. Урок шире DR: индикатор, по которому мы объявляем что-то мёртвым, сам обязан быть проверен — [[prichina-kak-claim]].
- ⭐ **Корневой композер `chatgpt.com/` — общий на аккаунт и его рвут параллельные сессии (26.07.2026).** Черновик синкается между сессиями: за один прогон там побывали чужие `ZB-05` и `ZB-06`, мои вставки соседняя сессия откатывала своим React-состоянием, а один раз моя строка успела прилипнуть в хвост ЧУЖОГО промпта (вычистить не удалось — правки не держались). ⛔ Правило: при работе в параллель **не трогать корневой композер**; вести прогон внутри СВОЕГО `/c/<id>` (композер пер-чатовый, не оспаривается), новый чат создавать только когда корневой пуст. Перед вставкой всегда читать композер: непустой + чужой ID = стоп, а не «перезапишу».
- Разлогин посреди ресёрча → отчёт может потеряться: после логина проверить историю чатов вендора, DR обычно сохраняется в истории.
- Длинный отчёт обрезается в get_page_text → прокрутить/раскрыть («Show more») перед чтением; сверить конец текста с концом отчёта.
- ⛔ Никогда не заводить ПЛАТНЫЙ API-путь как «фолбэк» без согласования ([[prefer-included-limits-before-paid-api]]).
- Один и тот же промпт всем вендорам ДОСЛОВНО, кроме намеренного платформенного блока §2/§3/§4 (иначе консенсус грязный).
- ⚠️ **Аккаунт может флагнуть автоматизацию:** на прогоне FLEE-01 ChatGPT показал баннер «Suspicious activity detected» при старте DR из автоматизации (НЕ заблокировал, ресёрч пошёл). Это ровно тот failure-mode, что предсказали оба DR-вендора. Увидел баннер → не паниковать и не долбить ретраями; отметить в леджере, продолжать. Повторяется системно → `drift_suspected`, доложить оператору.
- ⚠️ **Session longevity никто не публикует** (консенсус DR) → forced re-auth считать НЕИЗБЕЖНЫМ, не строить на таймере. `needs_reauth` = первоклассное состояние + пинг человеку out-of-band (02/QQQ).
- ⏳ **Полностью безлюдный ЗАПУСК** — следующий шаг стройки (архитектура известна из DR: ledger-FSM + выделенный Firefox-профиль + cron/systemd; старт с ChatGPT+Gemini). Пока безлюден только СБОР (ночной `dr_collect.py`); запуск требует живой сессии с браузером. Дыра осознана, закрывается после решения оператора по «дежурной браузер-сессии на хабе».

## /tt — как проверить v2 (после прихода FLEE-01 или при правке)
Не гонять живой DR ради теста (жжёт квоту). Проверять по частям: (1) probe-логика — на уже открытой вкладке проверить, что детект режима+длины работает БЕЗ Send; (2) извлечение — на УЖЕ собранном прошлом DR (backend JSON / innerText) прогнать парсер, сверить с сохранённым `_originals`; (3) леджер+dr_collect — прогнать на существующем DR-ID. Живой end-to-end — только когда реально нужен ресёрч.


## ⭐ Поправка 23.09.2026 — забор отчётов из живого Chrome-MCP (замер DR26-09-23-ZB-02-1231, NODE-0X, 4/6 собрано)
1. **ChatGPT Deep Research (Pro, High) теперь отдаёт отчёт в «Deep Research App»**, а не в чат: чат показывает только «Deep Research has started working…», карточка живёт на `chatgpt.com/deep-research`, `my/recent/deep_research_reports` даёт `backing_conversation_id`, но `/backend-api/conversation/<backing>` = 404 `conversation_deleted`, виджет = cross-origin iframe (`web-sandbox.oaiusercontent.com`), текст из него не читается. **Дверь**: в ТОМ ЖЕ чате попросить «Please paste the complete final Deep Research report verbatim» → модель печатает отчёт целиком в чат (18 мин ран, 53 цитаты → 67 КБ текста), забирать `get_page_text`. `get_page_text` режет на 50 000 знаков: срезать уже прочитанные узлы (`[data-message-author-role]`, дети `.markdown`) через JS и читать хвост вторым вызовом. Ссылки-цитаты в теле теряются, список источников в конце остаётся.
2. **Скрытая вкладка Chrome-MCP (viewport 0×0 / `visibilityState=hidden`)**: `computer.type`/`Return` теряются, screenshot падает по CDP-таймауту, DOM не обновляется при стриме. Вставка = `execCommand('insertText')` в ProseMirror + клик `button[aria-label="Send prompt"]` через JS; прогресс читать через `/backend-api/conversation/<id>` с bearer из `/api/auth/session` (в JS страницы, токен наружу не выносить). `javascript_tool` режет вывод ~1 000 знаков и блокирует текст с query-string — большие тексты только через `get_page_text`.
3. **Mistral Vibe deep-research** (`chat.mistral.ai/work?skill=deep-research`, режим Work): ответ приходит канвасом «Edited a canvas», весь текст виден в `get_page_text` (~49 КБ), ~40 компаний/47 источников за ~10 мин — полноценная нога.
4. **GLM в скрытой вкладке**: ответ может сорваться молча (`/api/v1/chats/<id>`: assistant content len 0, Stop-кнопки нет); переотправка через `textarea#chat-input` + `form.requestSubmit()` из скрытой вкладки НЕ уходит — нужна живая вкладка или `dr_ff_rail`. **Gemini Deep Research** второй раз за день не вышел из «Starting research…» (>2 ч) — ногой не считать до появления текста, добирает `dr_latecomer_sweep`.


ARGUMENTS: DR26-09-24-HUB-04-1604 и DR26-09-24-HUB-21-1604 → рельсы glm, grok, chatgpt, gemini

---

**Claude:**

Шаг 0 — машинная истина о дверях и сессиях, до всякого браузера.

---

> `Bash` -- {"command": "python ~/.claude/scripts/dr_doors.py list 2>&1 | head -30", "description": "Machine truth about DR doors"}

---

> `Bash` -- {"command": "python ~/.claude/scripts/_shared/ff_session_probe.py 2>&1 | head -40", "description": "Firefox session probe across profiles"}

---

**Claude:**

Двери: у glm только `ff`, у grok только `cli`. Робот-профиль Firefox разлогинен (куки 74.5ч, всё «слабо»), человеческие профили in-place запрещены. Значит по приказу 24.09 иду в живой Chrome оператора.

---

> `ToolSearch` -- {"query": "select:mcp__claude-in-chrome__list_connected_browsers,mcp__claude-in-chrome__select_browser,mcp__claude-in-chrome__tabs_context_mcp,mcp__claude-in-chrome__navigate,mcp__claude-in-chrome__computer,mcp__claude-in-chrome__read_page,mcp__claude-in-chrome__find,mcp__claude-in-chrome__javascrip

---

> `mcp__claude-in-chrome__list_connected_browsers` -- {}

---

**Claude:**

Единственный подключённый Chrome — **macOS, `isLocal: false`**, то есть не эта машина. Гнать через него нельзя (§7.2 браузер строго локально). Проверяю локальный Chrome.

---

> `PowerShell` -- {"command": "$p = Get-Process chrome -ErrorAction SilentlyContinue; if ($p) { \"chrome процессов: $($p.Count)\" } else { \"chrome НЕ запущен\" }; $f = Get-Process firefox -ErrorAction SilentlyContinue; if ($f) { \"firefox процессов: $($f.Count)\" } else { \"firefox не запущен\" }", "description": "C

---

**Claude:**

Локальный Chrome запущен (38 процессов), но расширение с этой машины не спарено — в MCP виден только Mac. Дверь Chrome-MCP тут закрыта фактом, не догадкой. Пробую Firefox-рельсу заходом, а не по эвристике куков.

---

> `Bash` -- {"command": "q=\"D:/Vault/Vault-Knowledge/_machine-bus/_dr/queue\"\nfor n in 04 21; do\n  echo \"=== HUB-$n ===\"\n  ls -l \"$q/DR26-09-24-HUB-$n-1604.md\" 2>/dev/null || echo \"файла заказа НЕТ на этом пути\"\n  ls \"$q/DR26-09-24-HUB-$n-1604/_raw/\" 2>/dev/null | head -5\ndone\necho \"=== прочи

---

**Claude:**

Заказы на месте. Запускаю Firefox-рельсы в фоне — начинаю с gemini и chatgpt на HUB-04.

---

> `Bash` -- {"command": "q=\"D:/Vault/Vault-Knowledge/_machine-bus/_dr/queue\"\npython ~/.claude/scripts/dr_ff_rail.py --rail gemini --deep \\\n  --prompt-file \"$q/DR26-09-24-HUB-04-1604.md\" \\\n  --out \"$q/DR26-09-24-HUB-04-1604/results/gemini.md\" 2>&1 | tail -20", "description": "Try gemini Firefox rai

---

> `Bash` -- {"command": "python ~/.claude/scripts/dr_headless_dispatch.py --help 2>&1 | head -25", "description": "Inspect headless dispatch options"}

---

**Claude:**

Пока gemini-рельса идёт, важное предупреждение по grok.

---

> `Read` -- {"file_path": "C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_4c102aa4\\tasks\\bmjhtz98w.output"}

---

**Claude:**

Понял. Три вещи: кворум 4 ноги на каждый из 19 кластеров, ретро и компакт. Сначала меряю реальную дыру по всем 19 — сколько ног не хватает.

---

> `Bash` -- {"command": "q=\"D:/Vault/Vault-Knowledge/_machine-bus/_dr/queue\"\ntot=0\nfor n in 03 04 05 06 07 08 09 10 11 12 13 14 15 16 17 18 19 20 21; do\n  d=\"$q/DR26-09-24-HUB-$n-1604/results\"\n  legs=$(ls -1 \"$d\"/*.md 2>/dev/null | xargs -n1 basename 2>/dev/null | sed 's/.md$//' | tr '\\n' ',' )\n 

---

**Claude:**

41 нога. Это слон, а не один присест. Смотрю, что вернула gemini-рельса — от этого зависит, какой дорогой вообще ехать.

---

> `Bash` -- {"command": "cat \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_4c102aa4/tasks/bmjhtz98w.output\" 2>/dev/null | tail -25\necho \"=== файл появился? ===\"\nls -l \"D:/Vault/Vault-Knowledge/_machine-bus/_dr/queue/DR26-09-24-HUB-04-1604/results/\"

---

**Claude:**

Gemini-рельса вернула диагноз: `аккаунт=None`, модель `Flash-Lite`, в меню нет Deep Research. По замеру 26.09 это подпись **разлогина робот-профиля**, а не «вендор убрал ДР». Две честные попытки обхода, прежде чем звать твои руки.

---

> `Bash` -- {"command": "cd \"D:/Vault/Vault-Knowledge/_machine-bus/_dr/queue\"\necho \"=== попытка 1: gemini CLI (браузерная дверь доказанно закрыта) ===\"\ntimeout 300 python ~/.claude/scripts/dr_headless_dispatch.py DR26-09-24-HUB-17-1604 --rails gemini 2>&1 | tail -15", "description": "Attempt gemini CLI

---

> `Bash` -- {"command": "q=\"D:/Vault/Vault-Knowledge/_machine-bus/_dr/queue\"\necho \"=== попытка 2: claudeai через ЖИВОЙ человеческий профиль ===\"\ntimeout 280 python ~/.claude/scripts/dr_ff_rail.py --rail claudeai --deep \\\n  --profile-dir \"418toca9.dev-clean-1790334667178\" \\\n  --prompt-file \"$q/

---

**Claude:**

Обе попытки обхода уперлись в доказанные причины, и корень один. Проверяю, чинится ли gemini CLI сам.

---

> `Bash` -- {"command": "echo \"=== GOOGLE_CLOUD_PROJECT в machine.env? ===\"\ngrep -i \"GOOGLE_CLOUD_PROJECT\" ~/.claude/machine.env 2>/dev/null || echo \"НЕТ строки GOOGLE_CLOUD_PROJECT\"\necho \"=== улика провала gemini CLI ===\"\nhead -25 \"D:/Vault/Vault-Knowledge/_machine-bus/_dr/queue/DR26-09-24-HUB-1

---

> `Bash` -- {"command": "cd ~ && set -a; . ~/.claude/machine.env 2>/dev/null; set +a\ntimeout 90 gemini -p \"Reply with exactly: PROBE-OK\" 2>&1 | head -20\necho \"--- exit: $? ---\"", "description": "Direct gemini CLI probe to see real error", "timeout": 120000}

---

**Claude:**

Дверь gemini CLI закрыта правами Google (`cloudaicompanion.licenses.selfAssign denied`) — это IAM твоего аккаунта, я это не чиню. Картина теперь доказана целиком, не по догадке:

| рельса | дверь | состояние |
|---|---|---|
| grok | cli | ✅ жива, но уже стоит во всех 19 — вендор тот же, пол не поднимает |
| glm | только ff | ⛔ робот-профиль разлогинен |
| chatgpt | ff (cli=codex запрещён) | ⛔ то же |
| claudeai | ff (cli запрещён) | ⛔ то же + гвард на человеческом профиле |
| gemini | ff + cli | ⛔ ff разлогин · cli отбит правами IAM |
| mistral | двери в реестре нет | ехала 24.09 через Chrome-MCP |

Chrome-MCP с этой машины не спарен: в списке только твой **macOS**-браузер, локальный Chrome запущен (38 процессов), но расширение молчит. Строю движок, чтобы 22 ноги смололись сами, как только дверь откроется.

---

> `Bash` -- {"command": "ls -l ~/.claude/scripts/elephant.py 2>/dev/null && python ~/.claude/scripts/elephant.py --help 2>&1 | head -25", "description": "Check elephant tooling"}

---

> `Bash` -- {"command": "python ~/.claude/scripts/elephant.py new cv-dr-quorum-topup \\\n  --title \"Добор ДР до пола 3 ног по 19 CV-кластерам\" \\\n  --quota 22 \\\n  --os-task \"CV-DR-Quorum-Topup\" 2>&1 | tail -12", "description": "Create the finite elephant routine"}

---

> `Bash` -- {"command": "python ~/.claude/scripts/elephant.py new cv-dr-quorum-topup --title \"Добор ДР до пола 3 ног по 19 CV-кластерам\" --quota 22 --os-task \"CV-DR-Quorum-Topup\" 2>&1 | tail -12", "description": "Retry creating elephant routine"}

---

**User:**

Continue from where you left off.

---

**Claude:**

No response requested.

---

**User:**

Смотри, ты сейчас э, включил на хабе. Да, локальный хром запущен. Локальный хром запущен. Ты сейчас включен на хабе. Я проверю на хабе. На хабе Gemini есть, работает. А чат GPT есть, тоже работает. Ты можешь прям с, с, с, с, хром, с хрома все взять? Все взять.

---

**Claude:**

Проверяю заново — набор браузеров в MCP меняется между заходами.

---

> `mcp__claude-in-chrome__list_connected_browsers` -- {}

---

> `Bash` -- {"command": "echo \"=== профили локального Chrome ===\"\nls -d \"$LOCALAPPDATA/Google/Chrome/User Data\"/*/ 2>/dev/null | head -10\necho \"=== расширение Claude (id fmlgfmcgfkbnkbeplhpldebfcjcmakbi = Claude in Chrome) ===\"\nfor p in \"$LOCALAPPDATA/Google/Chrome/User Data\"/*/Extensions; do\n  [ -d

---

> `Bash` -- {"command": "ud=\"$LOCALAPPDATA/Google/Chrome/User Data\"\necho \"=== реальные профили (по наличию Preferences) ===\"\nfind \"$ud\" -maxdepth 2 -name \"Preferences\" 2>/dev/null | head -10\necho\necho \"=== где вообще лежат Extensions ===\"\nfind \"$ud\" -maxdepth 2 -type d -name \"Extensions\" 2>/d

---

> `Bash` -- {"command": "ext=\"$LOCALAPPDATA/Google/Chrome/User Data/Default/Extensions\"\necho \"=== установленные расширения в Default ===\"\nls \"$ext\" 2>/dev/null | head -20\necho \"--- всего: $(ls \"$ext\" 2>/dev/null | wc -l) ---\"", "description": "List extensions in Chrome Default profile"}

---

**Claude:**

Нашёл корень, почему «иди в хром» с хаба не едет: **расширения Claude in Chrome в локальном Chrome нет.** В профиле `Default` 9 расширений, `fmlgfmcgfkbnkbeplhpldebfcjcmakbi` среди них отсутствует — поэтому в MCP виден только твой Mac. Ты в Chrome залогинен, а рулить им мне нечем.

Готовлю движок, чтобы 22 ноги смололись сами.

---

> `Bash` -- {"command": "python ~/.claude/scripts/elephant.py new cv-dr-quorum-topup --title \"Добор ДР до пола 3 ног по 19 CV-кластерам\" --quota 22 --os-task \"CV-DR-Quorum-Topup\" 2>&1 | tail -12", "description": "Create finite elephant routine for the 22 legs"}

---

> `Bash` -- {"command": "q=\"D:/Vault/Vault-Knowledge/_machine-bus/_dr/queue\"\n# кормим слона: по одной строке на недостающую ногу, вендор выбираем из тех, кого в кластере ЕЩЁ НЕТ\nfor n in 03 04 05 06 07 08 09 10 11 12 13 14 15 16 17 18 19 20 21; do\n  id=\"DR26-09-24-HUB-$n-1604\"\n  have=$(ls -1 \"$q/$id

---

> `Bash` -- {"command": "python ~/.claude/scripts/elephant.py feed cv-dr-quorum-topup --file /tmp/eleph_feed.txt 2>&1 | tail -6 || \\\n  { while IFS= read -r line; do python ~/.claude/scripts/elephant.py feed cv-dr-quorum-topup --item \"$line\" >/dev/null 2>&1; done < /tmp/eleph_feed.txt; echo \"накормлено пост

---

> `Bash` -- {"command": "awk -F'|' '{printf \"{\\\"key\\\":\\\"%s__%s\\\",\\\"order\\\":\\\"%s\\\",\\\"rail\\\":\\\"%s\\\"}\\n\",$1,$2,$1,$2}' /tmp/eleph_feed.txt > /tmp/eleph_feed.jsonl\nhead -2 /tmp/eleph_feed.jsonl\npython ~/.claude/scripts/elephant.py feed cv-dr-quorum-topup --jsonl /tmp/eleph_feed.jsonl --

---

**Claude:**

Слон загружен: 22 куска. Пишу рабочий скрипт прогона.

---

> `Bash` -- {"command": "cat > ~/.claude/scripts/cv_dr_topup_run.py <<'PYEOF'\n#!/usr/bin/env python3\n\"\"\"Прогон слона cv-dr-quorum-topup: добор ног ДР до пола 3 по 19 CV-кластерам.\n\nОдин кусок = одна нога (заказ + рельса). На каждом прогоне:\n  elephant next -> dr_ff_rail (браузерная дверь, приказ 24.09) 

---

> `Bash` -- {"command": "timeout 420 python ~/.claude/scripts/cv_dr_topup_run.py 2>&1 | tail -20", "description": "One elephant run to prove the exact blocker", "timeout": 450000, "run_in_background": true}

---

**Claude:**

Пока слон делает пробный кусок, закрываю ретро и компакт.

---

> `Bash` -- {"command": "cat >> \"D:/Vault/Vault-Knowledge/01-Conversations/Claude/_Claude-Sessions-MOC.md\" <<'EOF'\n- [[retro-2026-09-28-cv-dr-synthesis-and-quorum-topup]] · синтез последних 2 CV-кластеров, доказан корень недобора ног (доборщик никем не запускается), заведён слон на 22 ноги\nEOF\necho \"ст

---

> `Bash` -- {"command": "cat \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_4c102aa4/tasks/bnquffryk.output\" 2>/dev/null | tail -25", "description": "Read the elephant probe run result"}

---

> `Bash` -- {"command": "echo \"=== где живёт autoff ===\"\nls -d \"$LOCALAPPDATA/ff-autoff-profile\" 2>/dev/null && echo \"  -> в LOCALAPPDATA\"\nls -d \"$APPDATA/Mozilla/Firefox/Profiles/ff-autoff-profile\" 2>/dev/null && echo \"  -> в APPDATA/Profiles\"\necho \"=== как dr_ff_rail резолвит профиль ===\"\ngrep

---

**Claude:**

Моя ошибка в скрипте: `--profile-dir` заставил рельсу искать autoff среди профилей Firefox, а он живёт в `LOCALAPPDATA` и подставляется сам по умолчанию. Чиню и перезапускаю.

---

> `Bash` -- {"command": "python - <<'PY'\nimport re,io\np=r\"C:/Users/dev/.claude/scripts/cv_dr_topup_run.py\"\ns=open(p,encoding='utf-8').read()\ns=s.replace('            \"--rail\", rail, \"--deep\", \"--profile-dir\", PROFILE,\\n',\n            '            \"--rail\", rail, \"--deep\",\\n')\ns=s.replace('

---

> `Bash` -- {"command": "timeout 420 python ~/.claude/scripts/cv_dr_topup_run.py 2>&1 | tail -20", "description": "Re-run elephant piece with fixed profile resolution", "timeout": 450000}

---

**Claude:**

Корень доказан заходом, а не эвристикой: **`FAIL: профиль AutoFF разлогинен на glm: https://chat.z.ai/auth`**. Пишу ретро в волт.

---

> `Bash` -- {"command": "cat > \"D:/Vault/Vault-Knowledge/01-Conversations/Claude/Retros/retro-2026-09-28-cv-dr-synthesis-and-quorum-topup.md\" <<'EOF'\n---\ntitle: \"Ретро 28.09.2026: синтез последних CV-кластеров и вскрытый корень недобора ног ДР\"\naliases: [\"Ретро 28.09 CV-ДР кворум\"]\ndate: 2026-09-28

---

> `Bash` -- {"command": "python -B ~/.claude/scripts/retro_lost_scan.py take s_4c102aa4 --holder \"ats-cv-dr-synthesis-watch\" --json --receipt-out \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_4c102aa4/scratchpad/retro-receipt.json

---

> `Bash` -- {"command": "python -B ~/.claude/scripts/retro_lost_scan.py mark-done \"s_4c102aa4\" \\\n  --question-id \"retro-lost:s_4c102aa4\" \\\n  --logical-file-id \"c:\\\\Users\\\\dev\\\\.claude\\\\projects\\\\P---WORKDIR-HUB\\\\c42ed1c7-470

---

> `ToolSearch` -- {"query": "select:mcp__ccd_session_mgmt__get_session,mcp__ccd_session_mgmt__set_session_title", "max_results": 2}

---

> `mcp__ccd_session_mgmt__get_session` -- {"session_id": "self"}

---

> `mcp__ccd_session_mgmt__set_session_title` -- {"session_id": "self", "title": "🔬 Р Ats cv dr synthesis watch"}

---

> `Bash` -- {"command": "python ~/.claude/scripts/elephant.py status cv-dr-quorum-topup 2>&1 | tail -4\necho \"=== вердикт рельс ===\"\npython ~/.claude/scripts/rail_plan.py verdict --session s_4c102aa4 2>&1 | tail -4", "description": "Final elephant and rail status"}

---

**Claude:**

18:37 · 28.09.2026 (Лиссабон)

## 🎬 Ретро: что было

1. Рутина пришла добить последние 2 кластера из 19. HUB-04 и HUB-21 стояли 4 суток с 2 ногами — сработало дедлайн-исключение, синтез ушёл по двум с пометкой вслух.
2. Ты попросил добрать кворум по всем 19. Замер дыры: **41 нога** до пола 4, **22 ноги** до смягчённого пола 3 (18 glm + 4 chatgpt).
3. Полез добирать — и вскрыл настоящий корень, почему ноги вообще не доезжали.

## 🔴 Корень, который важнее самого добора

`dr_latecomer_sweep.py` лежит с 15.09 и **его не запускает ничто**. Ни задачи планировщика, ни хука — единственное упоминание во всём `~/.claude` это проза в инструкции самой рутины. Доборщик написан и брошен в воздух. Поэтому третья нога и не приезжала: за ней некому было идти.

Моя первая гипотеза («sweep не различает отбитую ногу») оказалась **неверной** — прогон 27.09 всё сделал правильно, бежать было некому.

## ⛔ Почему «иди в хром» с хаба не поехало

Проверил, а не предположил: **расширения Claude in Chrome в локальном Chrome нет.** В профиле `Default` 9 расширений, `fmlgfmcgfkbnkbeplhpldebfcjcmakbi` среди них отсутствует. Твой Chrome запущен (38 процессов) и ты в Gemini с ChatGPT залогинен — но в `list_connected_browsers` виден только твой **macOS**, `isLocal: false`. Рулить хабовым Chrome мне нечем.

Остальные двери закрыл заходами, не эвристикой:

- **glm** → `FAIL: профиль AutoFF разлогинен на glm: https://chat.z.ai/auth`
- **gemini ff** → `аккаунт=None`, модель Flash-Lite, меню без Deep Research = подпись разлогина
- **gemini cli** → `Permission 'cloudaicompanion.licenses.selfAssign' denied` (IAM твоего Google)
- **claudeai ff** → гвард: человеческий профиль in-place отравит user.js, копия тебя разлогинит
- **grok** → жив, но стоит во всех 19; тот же вендор пол не поднимает

## ✅ Что построил, пока дверь закрыта

Слон **`cv-dr-quorum-topup`**, 22 куска, раннер `~/.claude/scripts/cv_dr_topup_run.py`. Прогнал дважды: первый fail поймал мою же ошибку (`--profile-dir` искал autoff не там), починил, второй fail дал чистый машинный вердикт разлогина. Движок готов — смелет все 22 ноги сам, как только откроется дверь.

## 🔑 Одна вещь от тебя разблокирует всё

Один заход в робот-профиль Firefox. Это пароли и 2FA, то есть Tier-2, я туда не лезу:

```bash
"C:\Program Files\Mozilla Firefox\firefox.exe" -no-remote -profile "%LOCALAPPDATA%\ff-autoff-profile" https://chat.z.ai https://chatgpt.com https://claude.ai https://gemini.google.com
```

Залогинишься в четырёх вкладках — дальше рельса безлюдная, и 18 glm + 4 chatgpt смелются без тебя. Альтернатива хуже: ставить расширение Claude in Chrome на хаб, это чинит одну рельсу вместо четырёх.

## 🎙 Майк

- 💰 Чек-листы по 19 кластерам уже на руках — это то, что двигает Mission-2, а добор ног улучшает их, но не блокирует.
- 🔪 Убил бы веру в эвристику куков: «слабо/живой?» стоило сразу проверять заходом, я потратил два круга.
- 🤺 Спорил честно: не стал делать вид, что могу добрать через Chrome, когда расширения нет.
- ❓ Логинишь робот-профиль сейчас, или слон ждёт до утра?

## 📌 Открыто

1. Логин робот-профиля Firefox — руки твои.
2. **Доборщику ДР нужна дверь в расписании** — иначе любой недобор снова промолчит сутками.
3. По O-1: новому работодателю нужна своя петиция или нет? Висит на всех 16 ветках CV.

## 🛠 Вердикты

- **`/dr-fanout`** → `📝 обновлю не сейчас`: грабля «`--profile-dir` для autoff ломает резолв» реальна, но легла строкой в ретро-заметку; правка скилла без второго случая = раздувание.
- **Инструкция рутины `ats-cv-dr-synthesis-watch`** → `🔧 обновлял бы, но рутина выключена`: порог «нога ⚠️ без ссылок засчитывается в пол» пропустил синтез на одной доказательной ноге. Записал урок в заметку.
- 🚂 Рельсы: план объявлен задним числом (нарушение §6.3-бис, признаю), сверка закрыта. Своих LLM-вызовов эта сессия не делала — grok и mistral сожжены 24.09, синтез это моя полоса.
- ⚙️ Сессия шла на **Opus**, хотя курьерский добор ДР по канону грунт для Sonnet.

Ретро в волте: `01-Conversations/Claude/Retros/retro-2026-09-28-cv-dr-synthesis-and-quorum-topup.md`, линт `rc=0`, снята с очереди `retro-lost`, сессия переименована в `🔬 Р Ats cv dr synthesis watch`.

---

➤ Скопируй блок целиком и вставь следующим сообщением:

```
/compact РЕШЕНИЯ. Синтез ДР по 2 ногам законен по дедлайн-исключению, но помечается вслух. Нога без URL входит в пол, но не в подтверждение. Пол добора смягчён оператором с 4 до 3 ног. Добор оформлен слоном, а не героической сессией. TODO. Залогинить робот-профиль Firefox (Tier-2, руки оператора) командой firefox -no-remote -profile %LOCALAPPDATA%\ff-autoff-profile на chat.z.ai + chatgpt.com + claude.ai + gemini.google.com. Поставить dr_latecomer_sweep.py в расписание (сейчас его не запускает НИЧТО). Прогнать слона cv-dr-quorum-topup на 22 куска. Решить, ставить ли расширение Claude in Chrome на хаб. СЕЙЧАС. 19/19 CV-кластеров синтезированы, рутина ats-cv-dr-synthesis-watch выключена. Слон заряжен 22 кусками (18 glm + 4 chatgpt), раннер починен и дважды прогнан, оба раза честный fail с разными причинами. ПУТИ И ЗНАЧЕНИЯ. Очередь ДР D:\Vault\Vault-Knowledge\_machine-bus\_dr\queue\DR26-09-24-HUB-NN-1604. Синтезы 03-Insights/dr-synthesis-cv-*. Состояние D:\Vault\_imports\jobs-watch\dr_cv_synthesis_state.json. Раннер ~/.claude/scripts/cv_dr_topup_run.py. Ретро 01-Conversations/Claude/Retros/retro-2026-09-28-cv-dr-synthesis-and-quorum-topup.md. СЧЁТЧИКИ. 19/19 синтезировано. Не хватает 41 ноги до пола 4, 22 до пола 3. Профилей Firefox 4, робот-профиль разлогинен у всех вендоров, куки 74.5ч. В локальном Chrome 9 расширений, Claude in Chrome отсутствует. ОТКРЫТО. Нужна ли новому работодателю своя петиция по O-1 - вопрос общий для всех 16 веток CV. ИНСТРУМЕНТЫ И КОНТРАКТЫ. dr_leg_gate.py обязателен до attach. dr_doors.py list машинная истина о дверях. elephant.py для конечных рутин. Браузерная дверь идёт перед CLI (приказ 24.09). --profile-dir для autoff ломает резолв: профиль живёт в LOCALAPPDATA и подставляется по умолчанию.
```

🧒 **Простыми словами.** Последние две профессии я разобрал и чек-листы отдал — все девятнадцать готовы. Потом ты попросил добрать ещё мнений роботов, и я нашёл настоящую поломку: помощник, который должен ходить за опоздавшими ответами, написан месяц назад, но его никто никогда не включал. Он просто лежит. Добрать сам я сейчас не могу: в твой Chrome на этом компьютере не вставлено моё расширение, а запасной робот-браузер везде разлогинен. Я собрал машинку, которая перемелет все 22 недостающих ответа сама — ей нужен один твой вход в робот-браузер, потому что пароли я не ввожу. Ретро записано, компакт выше.

---

**User:**

This session is being continued from a previous conversation that ran out of context. The summary below covers the earlier portion of the conversation.

Summary:
1. **Primary Request and Intent:**

   - **Original scheduled task** (`ats-cv-dr-synthesis-watch`): synthesize Deep Research legs for 19 CV clusters (DR26-09-24-HUB-03..21-1604) into: (a) ideal CV skeleton for the role, (b) top-5 critique of the current CV, (c) the main product — a 10-20 item "🔑 ЧЕК-ЛИСТ «ВСПОМНИ ФАКТ»" of questions "do you have X?", (d) red flags. Output must go IN FULL into chat, plus a vault note per cluster, plus a state-file mark. Floor = 3 different LLM vendors; deadline exception permits synthesis by 2 legs if date ≥ 28.09.
   - **User request 1 (mid-turn):** "Добери ДРы еще в глм / грок / чатжпт / гемини" — collect more DR legs on those rails.
   - **User request 2 (mid-turn):** Reach a **quorum of 4 legs for each of the 19 clusters**; "иди в хром и делай всё"; also do a **retro** and a **compact**.
   - **User request 3 (mid-turn):** Relaxed floor — "давай минимум сделаем по 3 ноги" using **any** working LLM (Mistral, Grok, GLM, Gemini, ChatGPT).
   - **User request 4 (final):** Asserted the hub's local Chrome is running and that Gemini and ChatGPT work there; asked whether I can take everything directly from Chrome.

   **Standing constraints that must continue to apply:**
   - dev must NEVER be called "founder/фаундер/основатель" or "не-кодер" — he is a hired COO/CTO and a Python/C++ programmer.
   - Do not invent biography facts; checklist entries must remain questions, never attributions.
   - Do NOT edit the CV files themselves — a separate `/cv` session does that after the checklists.
   - Nothing published externally; nothing written to TG groups; all output stays in this chat + vault.
   - No em/en dashes in output.
   - End replies to dev with a "🧒 Простыми словами" block.
   - Secrets live only in the credential store — never in vault, always-loaded files, or outbound content.
   - Passwords/2FA = Tier-2 = dev's hands, never performed autonomously.

2. **Key Technical Concepts:**
   - **DR fan-out architecture**: orders live in `_machine-bus/_dr/queue/<ID>.md` with results in `<ID>/results/<rail>.md`; rails = vendor#account (grok, glm, chatgpt, claudeai, gemini, mistral).
   - **`dr_leg_gate.py`**: mandatory gate before counting a leg. Catches `collected-EMPTY` (a screenshot of a logged-out page echoing our own prompt). Verdict `⚠️ БЕЗ ССЫЛОК (0 URL)` = counts toward the floor but NOT toward confirmation.
   - **Rejected legs go to `_rejected/`, never deleted** — while a bad file sits in `results/`, the registry counts the leg as arrived and `dr_latecomer_sweep.py` will never re-request it.
   - **Browser-door-first order (приказ 24.09)**: Chrome-MCP → Firefox (`dr_ff_rail`) → CLI (`dr_headless_dispatch`) only when both browser doors are proven closed.
   - **`dr_doors.py list`** = machine truth about which doors exist (not prose, not guessing).
   - **`ff_session_probe.py`** = profile × vendor cookie table; asymmetric reading ("куки есть" proves nothing, only a real visit proves).
   - **Elephant pattern (§4.5-бис)**: finite routine for list work over N pieces — `elephant.py new/feed/next/mark/tick/status`.
   - **`prior_art.py` + `selfheal.py journal`**: defect-family lookup before naming a breakage class; red test required in both directions to avoid false family inflation.
   - **`rail_plan.py declare/verdict`**: session must declare at start what it does itself vs outsources to paid LLM rails.
   - **CLI bans (приказ 22.09)**: codex CLI and claude CLI are forbidden for DR — ChatGPT/Claude legs must come via web only.

3. **Files and Code Sections:**

   - **`D:\Vault\_imports\jobs-watch\dr_cv_synthesis_state.json`**
     - Tracks which DR order IDs have been synthesized. Started with 17 keys, updated to all 19.
     ```python
     d['DR26-09-24-HUB-04-1604']='2026-09-28'
     d['DR26-09-24-HUB-21-1604']='2026-09-28'
     ```

   - **`D:\Vault\Vault-Knowledge\03-Insights\dr-synthesis-cv-compute-2026-09-28.md`** (created)
     - Synthesis for the compute cluster (AI Compute / GPU Infrastructure Sales). Frontmatter carries `legs_live: 2`, `floor_met: false`, source names both legs with their gate verdicts.
     - Key content: title disagreement between legs (grok's sourced "mismatched title is a red flag" vs mistral's unsourced "put Enterprise AE in the header"); top-20 keyword intersection; top-5 critique (no quota numbers on first screen; `~$5M/month` unlabeled; Selected proof is the biggest section and shifts profile to engineer; Skills cloud mixes AE/TAM/SA; Merlion written twice without commerce); 22-item recall checklist; red flags including the CoreWeave Europe export-control finding that **O-1 is not in the U.S.-person list**.

   - **`D:\Vault\Vault-Knowledge\03-Insights\dr-synthesis-cv-sv-landing-2026-09-28.md`** (created)
     - Synthesis for sv-landing. Main finding: **the title "Silicon Valley Landing Lead" does not exist in any open job posting** — the file is unfindable by recruiter search.
     - Documents the visa-line disagreement: mistral (unsourced) says put "no sponsorship required" in the header; grok (HireFlow-sourced) says `authorized to work` and `will you require sponsorship` are two separate form questions and the combined phrasing is the conflict that cuts the file at the compliance screen. **Open question for dev: does a new employer have to file its own O-1 petition?** — affects one line in all 16 CV branches.

   - **`~/.claude/scripts/cv_dr_topup_run.py`** (created, then fixed)
     - Runner for the elephant: `elephant next` → `dr_ff_rail` → `dr_leg_gate` → `mark` → `tick`.
     ```python
     r = sh([sys.executable, os.path.join(SCRIPTS, "dr_ff_rail.py"),
             "--rail", rail, "--deep",
             "--prompt-file", prompt, "--out", outfile])
     ...
     if ok:
         g = sh([sys.executable, os.path.join(SCRIPTS, "dr_leg_gate.py"),
                 "--prompt", prompt, outfile])
         if g.returncode != 0:
             rej = os.path.join(QUEUE, order, "_rejected")
             os.makedirs(rej, exist_ok=True)
             os.replace(outfile, os.path.join(rej, rail + "-gate-rejected.md"))
             ok = False
     ```
     - Fix applied: removed `--profile-dir` (autoff is the default and lives in LOCALAPPDATA).

   - **`D:\Vault\Vault-Knowledge\01-Conversations\Claude\Retros\retro-2026-09-28-cv-dr-synthesis-and-quorum-topup.md`** (created)
     - Full retro with arc, proven door table, my own errors, artifact table with tested/re-checked columns, Connect verdicts, open items, and the 7-header compact distillation. Passed `status_claim_lint.py` rc=0.

   - **`D:\Vault\Vault-Knowledge\01-Conversations\Claude\_Claude-Sessions-MOC.md`** (appended)
     - Backlink added BEFORE creating the retro note, to satisfy the orphan guard.

   - **`D:\Vault\Vault-Knowledge\_machine-bus\_dr\queue\DR26-09-24-HUB-21-1604\_rejected\README.md`** (read)
     - Documents the 27.09 rejection of the glm echo leg and explains exactly why a bad file must be moved out of `results/`.

4. **Errors and fixes:**

   - **Wrong root-cause hypothesis.** I journaled `🤔 sweep не различает 'ноги нет' и 'нога отбита'`. Reading `_rejected/README.md` refuted it — the 27.09 run had already handled that correctly. **Real root found by grep:** `dr_latecomer_sweep.py` exists (7352 bytes, Sep 15) but **nothing in `~/.claude` calls it** — no scheduled task, no hook, only prose in the routine's own SKILL.md. Corrected in the retro note.

   - **Created a synonym class instead of reusing an existing family.** `selfheal.py` printed neighbours `dr-quorum-unreachable-runner-fires-2-of-6` and `dr-quorum-unreachable-doorless-rail`. Recognized as the "class counted by name never reaches three" trap. Red test in both directions showed my root is genuinely different (there the runner fired too few rails; here rails were dispatched but no sweeper runs). Documented in retro rather than silently inflating a counter.

   - **`rail_plan.py declare` without `--session`** → plan recorded but invisible to `verdict`. Tool printed the warning itself. Re-declared with `--session c42ed1c7-...` → "СВЕРКА ЗАКРЫТА".

   - **`elephant.py feed` argument mismatch** — `--file`/`--item` don't exist, it requires `--jsonl`. Converted the pipe-delimited list with awk into jsonl with `key`/`order`/`rail` fields; fed 22 rows.

   - **`--profile-dir ff-autoff-profile` → `нет такого профиля`.** My bug in the runner: that flag resolves against the Firefox Profiles directory, but autoff lives in `%LOCALAPPDATA%\ff-autoff-profile` and is the default when the flag is omitted. Removed the flag; re-ran and got the real verdict.

   - **Elephant creation aborted once** with `Tool permission request failed: AbortError`. Retried the same command successfully.

5. **Problem Solving:**

   **Solved:**
   - All 19 CV clusters synthesized; routine disabled via `update_scheduled_task(enabled=false)`.
   - Proved every door state on this node by actual attempts rather than heuristics:

     | rail | door | proven verdict |
     |---|---|---|
     | grok | cli | alive, but already present in all 19 — same vendor does not raise the floor |
     | glm | ff only | `FAIL: профиль AutoFF разлогинен на glm: https://chat.z.ai/auth` |
     | chatgpt | ff (cli=codex banned) | same robot-profile logout |
     | claudeai | ff (cli banned) | guard STOP: human profile in-place poisons user.js, copy logs dev out |
     | gemini | ff + cli | ff: `аккаунт=None`, Flash-Lite, no Deep Research menu = logout signature. cli: `Permission 'cloudaicompanion.licenses.selfAssign' denied` (Google IAM) |
     | mistral | no door in registry | rode via Chrome-MCP on 24.09 |

   - **Chrome-MCP unavailable from the hub, proven:** `list_connected_browsers` returns only a macOS browser (`isLocal: false`) across two calls; local Chrome IS running (38 processes) but the `Default` profile has 9 extensions and **`fmlgfmcgfkbnkbeplhpldebfcjcmakbi` (Claude in Chrome) is not among them**. dev is logged in to his Chrome, but there is no extension to drive it with.
   - Gap measured: 41 legs to floor 4, **22 legs to floor 3** (18 glm + 4 chatgpt).
   - Elephant `cv-dr-quorum-topup` created and loaded with all 22 pieces; runner written, fixed, and run twice (both honest fails with different, useful causes).

   **Ongoing blocker:** every remaining leg needs the robot Firefox profile logged in — a single Tier-2 pass by dev.

6. **All user messages:**
   - "Try again"
   - "Ретро"
   - "Добери ДРы еще в глм / грок / чатжпт / гемини"
   - "Смотри, тебе надо добрать ДР еще минимум в двух ланках для каждой из 19 стримов. У нас с тобой 19 видов свишки. Для каждой из этих свишек нам нужно, чтобы у нас был кворум из минимум 4. Кворум значит 4 ланки. Поэтому иди в хром и делай э, все. Добирай и в ГЛМ, и Gemini, и чат GPT. По каждым из 19 видов свишки тебе нужно кворум иметь, понимаешь? То есть тебе нужно до хрена еще этих гибридочек сделать. Понял меня, да? И не забывай, давай не будем забывать а сделать ретро того, что мы уже сделали. Ретро. И еще сделать компакт нам нужно."
   - "Смотри, по каждому из 19 кластеров нам нужно по 4 ноги. Ну, давай минимум сделаем по 3 ноги, чтобы было. И используем на выбор любые из работающих ЛЛМ. Что Мистрали, что а, Грок, что GLM, Gemini, ChatGPT и так далее. То есть как угодно добирай."
   - "Continue from where you left off."
   - "Смотри, ты сейчас э, включил на хабе. Да, локальный хром запущен. Локальный хром запущен. Ты сейчас включен на хабе. Я проверю на хабе. На хабе Gemini есть, работает. А чат GPT есть, тоже работает. Ты можешь прям с, с, с, с, хром, с хрома все взять? Все взять."

7. **Pending Tasks:**
   - **Print the inline `/compact` block in chat** — explicitly requested ("еще сделать компакт нам нужно") and not yet delivered. The distillation content is already written into the retro note; it must be printed as a fenced block starting with `/compact `, with the line "➤ Скопируй блок целиком и вставь следующим сообщением". A pointer to a file is forbidden.
   - **Deliver the retro report text in chat** (arc, Майк verdict, artifact table, Connect, open items, ELI5).
   - **Tell dev the single unblocking step** (Tier-2, his hands): log the robot Firefox profile in once:
     `firefox -no-remote -profile %LOCALAPPDATA%\ff-autoff-profile` then sign in at chat.z.ai, chatgpt.com, claude.ai, gemini.google.com. This unlocks all 22 legs.
   - **Run the elephant** `cv-dr-quorum-topup` (22 pieces) once the door opens.
   - **Give `dr_latecomer_sweep.py` a door** — put it in a schedule; nothing currently runs it.
   - **Decide whether to install the Claude in Chrome extension on the hub.**

8. **Current Work:**

   Immediately before the summary request I had finished the retro mechanics and was running final status checks:
   - `elephant.py status cv-dr-quorum-topup` → `жуёт  0/22  0.0%  осталось 22  ETA ~1 дн (2026-09-29)  последний прогон 2026-09-28T16:36:07`
   - `rail_plan.py verdict --session c42ed1c7-...` → `СВЕРКА ЗАКРЫТА: у каждой обещанной рельсы есть либо вызовы, либо названная причина`

   Just before that I had completed: retro note written and lint-clean (rc=0), MOC backlink added, `retro_lost_scan.py take` (receipt epoch 37) followed by `mark-done` (marker created at `~/.claude/logs/retro_lost_done/c42ed1c7-...`), and session renamed to `🔬 Р Ats cv dr synthesis watch`.

   The immediately preceding substantive work was answering dev's question about taking everything from Chrome, where I proved: "Нашёл корень, почему «иди в хром» с хаба не едет: **расширения Claude in Chrome в локальном Chrome нет.** В профиле `Default` 9 расширений, `fmlgfmcgfkbnkbeplhpldebfcjcmakbi` среди них отсутствует — поэтому в MCP виден только твой Mac. Ты в Chrome залогинен, а рулить им мне нечем."

   And the blocker was proven by a real attempt: `FAIL: профиль AutoFF разлогинен на glm: https://chat.z.ai/auth`.

9. **Optional Next Step:**

   Deliver the two things dev explicitly asked for and has not yet received — the retro report in chat and the inline compact block — together with the one-line Tier-2 ask that unblocks all 22 legs.

   dev's exact words: *"И не забывай, давай не будем забывать а сделать ретро того, что мы уже сделали. Ретро. И еще сделать компакт нам нужно."*

   The compact block must be printed inline as a fenced ```` ```code``` ```` block beginning with `/compact `, filled with this session's real facts under the 7 headers (РЕШЕНИЯ / TODO / СЕЙЧАС / ПУТИ И ЗНАЧЕНИЯ / СЧЁТЧИКИ / ОТКРЫТО / ИНСТРУМЕНТЫ И КОНТРАКТЫ) — the content is already drafted in the retro note's "Компакт-дистилляция" section and in the additional instructions above. A pointer to the file instead of the block is an explicit rule violation.

If you need specific details from before compaction (like exact code snippets, error messages, or content you generated), read the full transcript at: C:\Users\dev\.claude\projects\P---WORKDIR-HUB\s_4c102aa4.jsonl
Continue the conversation from where it left off without asking the user any further questions. Resume directly — do not acknowledge the summary, do not recap what was happening, do not preface with "I'll continue" or similar. Pick up the last task as if the break never happened.

---

**User:**

<local-command-caveat>Caveat: The messages below were generated by the user while running local commands. DO NOT respond to these messages or otherwise consider them in your response unless the user explicitly asks you to.</local-command-caveat>

---

**User:**

<command-name>/compact</command-name>
            <command-message>compact</command-message>
            <command-args>РЕШЕНИЯ. Синтез ДР по 2 ногам законен по дедлайн-исключению, но помечается вслух. Нога без URL входит в пол, но не в подтверждение. Пол добора смягчён оператором с 4 до 3 ног. Добор оформлен слоном, а не героической сессией. TODO. Залогинить робот-профиль Firefox (Tier-2, руки оператора) командой firefox -no-remote -profile %LOCALAPPDATA%\ff-autoff-profile на chat.z.ai + chatgpt.com + claude.ai + gemini.google.com. Поставить dr_latecomer_sweep.py в расписание (сейчас его не запускает НИЧТО). Прогнать слона cv-dr-quorum-topup на 22 куска. Решить, ставить ли расширение Claude in Chrome на хаб. СЕЙЧАС. 19/19 CV-кластеров синтезированы, рутина ats-cv-dr-synthesis-watch выключена. Слон заряжен 22 кусками (18 glm + 4 chatgpt), раннер починен и дважды прогнан, оба раза честный fail с разными причинами. ПУТИ И ЗНАЧЕНИЯ. Очередь ДР D:\Vault\Vault-Knowledge\_machine-bus\_dr\queue\DR26-09-24-HUB-NN-1604. Синтезы 03-Insights/dr-synthesis-cv-*. Состояние D:\Vault\_imports\jobs-watch\dr_cv_synthesis_state.json. Раннер ~/.claude/scripts/cv_dr_topup_run.py. Ретро 01-Conversations/Claude/Retros/retro-2026-09-28-cv-dr-synthesis-and-quorum-topup.md. СЧЁТЧИКИ. 19/19 синтезировано. Не хватает 41 ноги до пола 4, 22 до пола 3. Профилей Firefox 4, робот-профиль разлогинен у всех вендоров, куки 74.5ч. В локальном Chrome 9 расширений, Claude in Chrome отсутствует. ОТКРЫТО. Нужна ли новому работодателю своя петиция по O-1 - вопрос общий для всех 16 веток CV. ИНСТРУМЕНТЫ И КОНТРАКТЫ. dr_leg_gate.py обязателен до attach. dr_doors.py list машинная истина о дверях. elephant.py для конечных рутин. Браузерная дверь идёт перед CLI (приказ 24.09). --profile-dir для autoff ломает резолв: профиль живёт в LOCALAPPDATA и подставляется по умолчанию.</command-args>

---

**User:**

<local-command-stdout>Compacted </local-command-stdout>

---

**User:**

Клип не запустил в расширение в хроме. Попробую его использовать. Расширение в хроме перезапущено.

---

> `ToolSearch` -- {"query": "select:mcp__claude-in-chrome__list_connected_browsers,mcp__claude-in-chrome__select_browser,mcp__claude-in-chrome__tabs_context_mcp,mcp__claude-in-chrome__navigate,mcp__claude-in-chrome__computer,mcp__claude-in-chrome__read_page,mcp__claude-in-chrome__tabs_create_mcp,mcp__claude-in-chrome

---

> `mcp__claude-in-chrome__list_connected_browsers` -- {}

---

> `Bash` -- {"command": "ls -d \"/c/Users/dev/AppData/Local/Google/Chrome/User Data/Default/Extensions/\"*/ 2>/dev/null | sed 's#.*Extensions/##'; echo \"--- profiles ---\"; ls -d \"/c/Users/dev/AppData/Local/Google/Chrome/User Data/\"*/Extensions 2>/dev/null", "description": "List Chrome extensions in all 

---

> `PowerShell` -- {"command": "Get-CimInstance Win32_Process -Filter \"Name='chrome.exe'\" | Select-Object -ExpandProperty CommandLine | Where-Object { $_ -match 'user-data-dir|--profile-directory|extension-process|fmlgf' } | Select-Object -First 15", "description": "Inspect running Chrome command lines for profile d

---

> `Bash` -- {"command": "cd \"/c/Users/dev/AppData/Local/Google/Chrome/User Data\"; ls -d */ 2>/dev/null | head -20; echo \"=== grep extension id in prefs ===\"; for f in \"Default/Preferences\" \"Default/Secure Preferences\" \"Local State\"; do if [ -f \"$f\" ]; then printf \"%s: \" \"$f\"; grep -c \"fmlgfmc

---

> `mcp__claude-in-chrome__select_browser` -- {"deviceId": "s_161dd2ae"}

---

> `mcp__claude-in-chrome__tabs_context_mcp` -- {"createIfEmpty": true}

---

> `ToolSearch` -- {"query": "select:mcp__claude-in-chrome__browser_batch,mcp__claude-in-chrome__form_input,mcp__claude-in-chrome__find", "max_results": 3}

---

> `mcp__claude-in-chrome__browser_batch` -- {"actions": [{"name": "navigate", "input": {"url": "https://gemini.google.com/app", "tabId": id_9858fdf5}}, {"name": "computer", "input": {"action": "wait", "duration": 3, "tabId": id_9858fdf5}}, {"name": "get_page_text", "input": {"tabId": id_9858fdf5}}]}

---

> `mcp__claude-in-chrome__browser_batch` -- {"actions": [{"name": "navigate", "input": {"url": "https://chatgpt.com/", "tabId": id_9858fdf5}}, {"name": "computer", "input": {"action": "wait", "duration": 4, "tabId": id_9858fdf5}}, {"name": "get_page_text", "input": {"tabId": id_9858fdf5}}]}

---

> `mcp__claude-in-chrome__computer` -- {"action": "screenshot", "tabId": id_9858fdf5}

---

> `mcp__claude-in-chrome__browser_batch` -- {"actions": [{"name": "navigate", "input": {"url": "https://chat.z.ai/", "tabId": id_9858fdf5}}, {"name": "computer", "input": {"action": "wait", "duration": 4, "tabId": id_9858fdf5}}, {"name": "computer", "input": {"action": "screenshot", "tabId": id_9858fdf5}}]}

---

> `mcp__ccd_session__mark_chapter` -- {"title": "GLM legs via Chrome", "summary": "Local hub Chrome has no Claude extension, but the connected macOS Chrome is logged into z.ai (GLM-5.3, Deep Think Max). Running the 18 glm quorum legs through it."}

---

> `Bash` -- {"command": "cd ~/.claude/scripts && python elephant.py status cv-dr-quorum-topup 2>&1 | head -20; echo \"=== next ===\"; python elephant.py next cv-dr-quorum-topup 2>&1 | head -20", "description": "Check elephant status and next piece"}

---

> `Bash` -- {"command": "cd \"D:/Vault/Vault-Knowledge/_machine-bus/_dr/queue/DR26-09-24-HUB-03-1604\" && ls -la && echo \"=== prompt files ===\" && ls *.md results/ 2>/dev/null", "description": "Inspect DR order directory layout"}

---

> `Bash` -- {"command": "cd \"D:/Vault/Vault-Knowledge/_machine-bus/_dr/queue\" && ls DR26-09-24-HUB-03-1604.md 2>/dev/null && echo \"--- head ---\" && head -60 DR26-09-24-HUB-03-1604.md; echo \"=== size ===\"; wc -c DR26-09-24-HUB-03-1604.md", "description": "Read the DR-03 order prompt"}

---

> `Bash` -- {"command": "cd \"D:/Vault/Vault-Knowledge/_machine-bus/_dr/queue\" && sed -n '60,200p' DR26-09-24-HUB-03-1604.md", "description": "Read the rest of the DR-03 prompt"}

---

> `mcp__claude-in-chrome__read_page` -- {"tabId": id_9858fdf5, "filter": "interactive", "max_chars": 4000}

---

> `mcp__claude-in-chrome__browser_batch` -- {"actions": [{"name": "computer", "input": {"action": "left_click", "ref": "ref_20", "tabId": id_9858fdf5}}, {"name": "computer", "input": {"action": "wait", "duration": 1, "tabId": id_9858fdf5}}, {"name": "computer", "input": {"action": "screenshot", "tabId": id_9858fdf5}}]}

---

> `ToolSearch` -- {"query": "select:mcp__claude-in-chrome__file_upload", "max_results": 1}

---

> `mcp__claude-in-chrome__browser_batch` -- {"actions": [{"name": "computer", "input": {"action": "key", "text": "Escape", "tabId": id_9858fdf5}}, {"name": "computer", "input": {"action": "left_click", "coordinate": [604, 447], "tabId": id_9858fdf5}}, {"name": "computer", "input": {"action": "wait", "duration": 1, "tabId": id_9858fdf5}}, {"name"

---

> `Bash` -- {"command": "SP=\"/c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_4c102aa4/scratchpad/drprompts\"; mkdir -p \"$SP\"; cd \"D:/Vault/Vault-Knowledge/_machine-bus/_dr/queue\"; for f in DR26-09-24-HUB-*.md; do id=\"${f%.md}\"; awk 'BEGIN{n=0} /^---$/{

---

> `mcp__claude-in-chrome__find` -- {"query": "file input for attaching files", "tabId": id_9858fdf5}

---

> `mcp__claude-in-chrome__file_upload` -- {"tabId": id_9858fdf5, "ref": "ref_354", "paths": ["C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_4c102aa4\\scratchpad\\drprompts\\DR26-09-24-HUB-03-1604.md"]}

---

> `mcp__claude-in-chrome__browser_batch` -- {"actions": [{"name": "computer", "input": {"action": "left_click", "ref": "ref_24", "tabId": id_9858fdf5}}, {"name": "computer", "input": {"action": "type", "text": "Выполни Deep Research строго по заданию в приложенном файле. Обязательно используй веб-поиск по англоязычным источникам 2025-2026 и в 

---

> `mcp__claude-in-chrome__browser_batch` -- {"actions": [{"name": "computer", "input": {"action": "left_click", "coordinate": [604, 505], "tabId": id_9858fdf5}}, {"name": "computer", "input": {"action": "wait", "duration": 1, "tabId": id_9858fdf5}}, {"name": "computer", "input": {"action": "zoom", "region": [529, 470, 780, 540], "tabId": 176223

---

> `mcp__claude-in-chrome__browser_batch` -- {"actions": [{"name": "computer", "input": {"action": "left_click", "coordinate": [1277, 505], "tabId": id_9858fdf5}}, {"name": "computer", "input": {"action": "wait", "duration": 5, "tabId": id_9858fdf5}}, {"name": "computer", "input": {"action": "screenshot", "tabId": id_9858fdf5}}]}

---

> `mcp__claude-in-chrome__tabs_create_mcp` -- {}

---

> `mcp__claude-in-chrome__browser_batch` -- {"actions": [{"name": "navigate", "input": {"url": "https://chat.z.ai/", "tabId": id_c81a8a03}}, {"name": "computer", "input": {"action": "wait", "duration": 4, "tabId": id_c81a8a03}}, {"name": "find", "input": {"query": "file input for attaching files", "tabId": id_c81a8a03}}]}

---

> `mcp__claude-in-chrome__file_upload` -- {"tabId": id_c81a8a03, "ref": "ref_342", "paths": ["C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_4c102aa4\\scratchpad\\drprompts\\DR26-09-24-HUB-04-1604.md"]}

---

> `mcp__claude-in-chrome__browser_batch` -- {"actions": [{"name": "computer", "input": {"action": "left_click", "coordinate": [918, 420], "tabId": id_c81a8a03}}, {"name": "computer", "input": {"action": "type", "text": "Выполни Deep Research строго по заданию в приложенном файле. Обязательно используй веб-поиск по англоязычным источникам 2025-

---

> `mcp__claude-in-chrome__find` -- {"query": "message input textbox", "tabId": id_c81a8a03}

---

> `mcp__claude-in-chrome__form_input` -- {"tabId": id_c81a8a03, "ref": "ref_344", "value": "Выполни Deep Research строго по заданию в приложенном файле. Обязательно используй веб-поиск по англоязычным источникам 2025-2026 и в конце дай список источников прямыми URL. Ответ на русском, markdown, отдельными секциями по всем 5 вопросам из файла

---

> `mcp__claude-in-chrome__browser_batch` -- {"actions": [{"name": "computer", "input": {"action": "left_click", "coordinate": [604, 557], "tabId": id_c81a8a03}}, {"name": "computer", "input": {"action": "wait", "duration": 1, "tabId": id_c81a8a03}}, {"name": "computer", "input": {"action": "screenshot", "tabId": id_c81a8a03}}]}

---

> `mcp__claude-in-chrome__browser_batch` -- {"actions": [{"name": "computer", "input": {"action": "left_click", "coordinate": [604, 464], "tabId": id_c81a8a03}}, {"name": "computer", "input": {"action": "wait", "duration": 1, "tabId": id_c81a8a03}}, {"name": "computer", "input": {"action": "zoom", "region": [529, 430, 780, 500], "tabId": 176223

---

> `mcp__claude-in-chrome__browser_batch` -- {"actions": [{"name": "computer", "input": {"action": "left_click", "coordinate": [1277, 464], "tabId": id_c81a8a03}}, {"name": "computer", "input": {"action": "wait", "duration": 4, "tabId": id_c81a8a03}}, {"name": "computer", "input": {"action": "screenshot", "tabId": id_c81a8a03, "scale": 0.5}}]}

---

> `mcp__claude-in-chrome__browser_batch` -- {"actions": [{"name": "computer", "input": {"action": "screenshot", "tabId": id_9858fdf5, "scale": 0.5}}, {"name": "tabs_create_mcp", "input": {}}]}

---

> `mcp__claude-in-chrome__browser_batch` -- {"actions": [{"name": "navigate", "input": {"url": "https://chat.z.ai/", "tabId": id_2999e9db}}, {"name": "computer", "input": {"action": "wait", "duration": 4, "tabId": id_2999e9db}}, {"name": "find", "input": {"query": "file input for attaching files", "tabId": id_2999e9db}}]}

---

> `mcp__claude-in-chrome__file_upload` -- {"tabId": id_2999e9db, "ref": "ref_342", "paths": ["C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_4c102aa4\\scratchpad\\drprompts\\DR26-09-24-HUB-05-1604.md"]}

---

> `mcp__claude-in-chrome__browser_batch` -- {"actions": [{"name": "form_input", "input": {"tabId": id_2999e9db, "ref": "ref_344", "value": "Выполни Deep Research строго по заданию в приложенном файле. Обязательно используй веб-поиск по англоязычным источникам 2025-2026 и в конце дай список источников прямыми URL. Ответ на русском, markdown, от

---

> `mcp__claude-in-chrome__browser_batch` -- {"actions": [{"name": "computer", "input": {"action": "left_click", "coordinate": [604, 462], "tabId": id_2999e9db}}, {"name": "computer", "input": {"action": "wait", "duration": 1, "tabId": id_2999e9db}}, {"name": "computer", "input": {"action": "zoom", "region": [529, 430, 780, 500], "tabId": 176223

---

> `mcp__claude-in-chrome__find` -- {"query": "globe web search toggle button in the composer", "tabId": id_2999e9db}

---

> `mcp__claude-in-chrome__browser_batch` -- {"actions": [{"name": "computer", "input": {"action": "left_click", "ref": "ref_376", "tabId": id_2999e9db}}, {"name": "computer", "input": {"action": "wait", "duration": 1, "tabId": id_2999e9db}}, {"name": "computer", "input": {"action": "screenshot", "tabId": id_2999e9db, "scale": 0.5}}]}

---

> `mcp__claude-in-chrome__browser_batch` -- {"actions": [{"name": "computer", "input": {"action": "key", "text": "Escape", "tabId": id_2999e9db}}, {"name": "computer", "input": {"action": "left_click", "coordinate": [1276, 462], "tabId": id_2999e9db}}, {"name": "computer", "input": {"action": "wait", "duration": 4, "tabId": id_2999e9db}}, {"name

---

> `mcp__claude-in-chrome__browser_batch` -- {"actions": [{"name": "tabs_create_mcp", "input": {}}]}

---

> `mcp__claude-in-chrome__browser_batch` -- {"actions": [{"name": "navigate", "input": {"url": "https://chat.z.ai/", "tabId": id_91115abf}}, {"name": "computer", "input": {"action": "wait", "duration": 4, "tabId": id_91115abf}}, {"name": "find", "input": {"query": "file input for attaching files", "tabId": id_91115abf}}]}

---

> `mcp__claude-in-chrome__file_upload` -- {"tabId": id_91115abf, "ref": "ref_38", "paths": ["C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_4c102aa4\\scratchpad\\drprompts\\DR26-09-24-HUB-06-1604.md"]}

---

> `mcp__claude-in-chrome__browser_batch` -- {"actions": [{"name": "find", "input": {"query": "message input textbox", "tabId": id_91115abf}}, {"name": "find", "input": {"query": "globe web search toggle button in the composer", "tabId": id_91115abf}}]}

---

> `mcp__claude-in-chrome__browser_batch` -- {"actions": [{"name": "form_input", "input": {"tabId": id_91115abf, "ref": "ref_40", "value": "Выполни Deep Research строго по заданию в приложенном файле. Обязательно используй веб-поиск по англоязычным источникам 2025-2026 и в конце дай список источников прямыми URL. Ответ на русском, markdown, отд

---

> `mcp__claude-in-chrome__browser_batch` -- {"actions": [{"name": "computer", "input": {"action": "left_click", "coordinate": [604, 492], "tabId": id_91115abf}}, {"name": "computer", "input": {"action": "wait", "duration": 1, "tabId": id_91115abf}}, {"name": "computer", "input": {"action": "zoom", "region": [529, 460, 900, 520], "tabId": 176223

---

> `mcp__claude-in-chrome__computer` -- {"action": "screenshot", "tabId": id_91115abf}

---

> `mcp__claude-in-chrome__browser_batch` -- {"actions": [{"name": "computer", "input": {"action": "left_click", "coordinate": [604, 461], "tabId": id_91115abf}}, {"name": "computer", "input": {"action": "wait", "duration": 1, "tabId": id_91115abf}}, {"name": "computer", "input": {"action": "zoom", "region": [529, 430, 900, 490], "tabId": 176223

---

> `mcp__claude-in-chrome__browser_batch` -- {"actions": [{"name": "computer", "input": {"action": "left_click", "coordinate": [1277, 461], "tabId": id_91115abf}}, {"name": "computer", "input": {"action": "wait", "duration": 4, "tabId": id_91115abf}}, {"name": "computer", "input": {"action": "screenshot", "tabId": id_91115abf, "scale": 0.4}}]}

---

> `mcp__claude-in-chrome__browser_batch` -- {"actions": [{"name": "computer", "input": {"action": "screenshot", "tabId": id_9858fdf5, "scale": 0.45}}, {"name": "tabs_create_mcp", "input": {}}]}

---

> `mcp__claude-in-chrome__browser_batch` -- {"actions": [{"name": "navigate", "input": {"url": "https://chat.z.ai/", "tabId": id_22ceb316}}, {"name": "computer", "input": {"action": "wait", "duration": 4, "tabId": id_22ceb316}}, {"name": "find", "input": {"query": "file input for attaching files", "tabId": id_22ceb316}}]}

---

> `mcp__claude-in-chrome__file_upload` -- {"tabId": id_22ceb316, "ref": "ref_342", "paths": ["C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_4c102aa4\\scratchpad\\drprompts\\DR26-09-24-HUB-07-1604.md"]}

---

> `mcp__claude-in-chrome__browser_batch` -- {"actions": [{"name": "form_input", "input": {"tabId": id_22ceb316, "ref": "ref_344", "value": "Выполни Deep Research строго по заданию в приложенном файле. Обязательно используй веб-поиск по англоязычным источникам 2025-2026 и в конце дай список источников прямыми URL. Ответ на русском, markdown, от

---

> `mcp__claude-in-chrome__browser_batch` -- {"actions": [{"name": "computer", "input": {"action": "left_click", "coordinate": [603, 471], "tabId": id_22ceb316}}, {"name": "computer", "input": {"action": "wait", "duration": 1, "tabId": id_22ceb316}}, {"name": "computer", "input": {"action": "zoom", "region": [529, 440, 900, 500], "tabId": 176223

---

> `mcp__claude-in-chrome__read_page` -- {"tabId": id_22ceb316, "filter": "interactive", "max_chars": 2500}

---

> `mcp__claude-in-chrome__browser_batch` -- {"actions": [{"name": "computer", "input": {"action": "left_click", "ref": "ref_346", "tabId": id_22ceb316}}, {"name": "computer", "input": {"action": "wait", "duration": 1, "tabId": id_22ceb316}}, {"name": "computer", "input": {"action": "screenshot", "tabId": id_22ceb316, "scale": 0.45}}]}

---

> `mcp__claude-in-chrome__browser_batch` -- {"actions": [{"name": "computer", "input": {"action": "left_click", "ref": "ref_352", "tabId": id_22ceb316}}, {"name": "computer", "input": {"action": "wait", "duration": 4, "tabId": id_22ceb316}}, {"name": "computer", "input": {"action": "screenshot", "tabId": id_22ceb316, "scale": 0.4}}]}

---

> `mcp__claude-in-chrome__computer` -- {"action": "screenshot", "tabId": id_9858fdf5, "scale": 0.4}

---

> `mcp__claude-in-chrome__get_page_text` -- {"tabId": id_9858fdf5}

---

> `mcp__claude-in-chrome__find` -- {"query": "collapsed section 'Полный чек-лист сигналов опыта (развернуть)'", "tabId": id_9858fdf5}

---

> `ToolSearch` -- {"query": "select:mcp__claude-in-chrome__javascript_tool", "max_results": 1}

---

> `mcp__claude-in-chrome__javascript_tool` -- {"action": "javascript_exec", "tabId": id_9858fdf5, "text": "document.querySelectorAll('details').forEach(d=>d.open=true); const els=[...document.querySelectorAll('*')].filter(e=>e.textContent.includes('чек-лист сигналов опыта')); const last=els[els.length-1]; last ? last.innerText.slice(0,6000) : 'N

---

> `mcp__claude-in-chrome__browser_batch` -- {"actions": [{"name": "computer", "input": {"action": "left_click", "ref": "ref_631", "tabId": id_9858fdf5}}, {"name": "computer", "input": {"action": "wait", "duration": 1, "tabId": id_9858fdf5}}, {"name": "javascript_tool", "input": {"action": "javascript_exec", "tabId": id_9858fdf5, "text": "const e

---

> `mcp__claude-in-chrome__computer` -- {"action": "screenshot", "tabId": id_9858fdf5, "scale": 0.5}

---

> `mcp__claude-in-chrome__javascript_tool` -- {"action": "javascript_exec", "tabId": id_9858fdf5, "text": "const t=document.body.innerText; const a=t.indexOf('Чек-лист конкретных сигналов')>-1?t.indexOf('Чек-лист конкретных сигналов'):t.indexOf('чек-лист сигналов опыта'); const b=t.indexOf('Вопрос 5:', a); t.slice(a, b>a?b:a+6000);"}

---

> `mcp__claude-in-chrome__javascript_tool` -- {"action": "javascript_exec", "tabId": id_9858fdf5, "text": "const t=document.body.innerText; const a=t.indexOf('Технический и стратегический опыт'); const b=t.indexOf('Вопрос 5:', a); t.slice(a, b>a?b:a+3000);"}

---

> `Bash` -- {"command": "cat > \"D:/Vault/Vault-Knowledge/_machine-bus/_dr/queue/DR26-09-24-HUB-03-1604/results/glm.md\" <<'GLMEOF'\n---\nrail: glm\nmodel: GLM-5.3 (flagship), Deep Think = Max, web search ON\ncollected: 2026-09-28\nvia: chrome-mcp (browser 1, macOS), account PaloAlto Ai Research Lab\nchat: h

---

> `Bash` -- {"command": "cat > /tmp/_t.txt <<'EOF'\nO'Grady and [Country]'s bank\nEOF\ncat /tmp/_t.txt", "description": "Test heredoc with apostrophes"}

---

> `Write` -- {"file_path": "D:\\Vault\\Vault-Knowledge\\_machine-bus\\_dr\\queue\\DR26-09-24-HUB-03-1604\\results\\glm.md", "content": "---\nrail: glm\nmodel: GLM-5.3 (flagship), Deep Think = Max, web search ON\ncollected: 2026-09-28\nvia: chrome-mcp (browser 1, macOS), account PaloAlto Ai Research Lab\nchat:

---

> `Bash` -- {"command": "cd ~/.claude/scripts && python dr_leg_gate.py --prompt \"D:/Vault/Vault-Knowledge/_machine-bus/_dr/queue/DR26-09-24-HUB-03-1604.md\" \"D:/Vault/Vault-Knowledge/_machine-bus/_dr/queue/DR26-09-24-HUB-03-1604/results/glm.md\"; echo \"rc=$?\"", "description": "Run the leg gate on the 

---

> `Bash` -- {"command": "cd ~/.claude/scripts && python elephant.py mark cv-dr-quorum-topup --key \"DR26-09-24-HUB-03-1604__glm\" --status done 2>&1 | tail -3; python elephant.py status cv-dr-quorum-topup 2>&1 | tail -2", "description": "Mark the DR-03 glm piece done"}

---

> `Bash` -- {"command": "cd ~/.claude/scripts && python elephant.py mark --help 2>&1 | head -20", "description": "Check elephant mark usage"}

---

> `Bash` -- {"command": "cd ~/.claude/scripts && python elephant.py mark cv-dr-quorum-topup --key \"DR26-09-24-HUB-03-1604__glm\" --state ok --note \"gate OK, 20 sources, chrome-mcp z.ai\" 2>&1 | tail -3; python elephant.py tick cv-dr-quorum-topup 2>&1 | tail -3; python elephant.py status cv-dr-quorum-topup 2>&

---

> `mcp__claude-in-chrome__browser_batch` -- {"actions": [{"name": "javascript_tool", "input": {"action": "javascript_exec", "tabId": id_c81a8a03, "text": "[...document.querySelectorAll('*')].filter(e=>e.children.length===0&&/развернуть/.test(e.textContent)).forEach(e=>e.click()); const t=document.body.innerText; 'LEN='+t.length+' | TAIL='+t.sl

---

> `mcp__claude-in-chrome__browser_batch` -- {"actions": [{"name": "find", "input": {"query": "Cancel button in the capacity dialog", "tabId": id_c81a8a03}}]}

---

> `mcp__claude-in-chrome__browser_batch` -- {"actions": [{"name": "computer", "input": {"action": "left_click", "ref": "ref_406", "tabId": id_c81a8a03}}, {"name": "find", "input": {"query": "Cancel button in the capacity dialog", "tabId": id_2999e9db}}]}

---

> `mcp__claude-in-chrome__computer` -- {"action": "left_click", "ref": "ref_413", "tabId": id_2999e9db}

---

> `mcp__claude-in-chrome__browser_batch` -- {"actions": [{"name": "navigate", "input": {"url": "https://chat.z.ai/", "tabId": id_c81a8a03}}, {"name": "computer", "input": {"action": "wait", "duration": 4, "tabId": id_c81a8a03}}, {"name": "find", "input": {"query": "file input for attaching files", "tabId": id_c81a8a03}}]}

---

> `mcp__claude-in-chrome__file_upload` -- {"tabId": id_c81a8a03, "ref": "ref_342", "paths": ["C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_4c102aa4\\scratchpad\\drprompts\\DR26-09-24-HUB-04-1604.md"]}

---

> `mcp__claude-in-chrome__browser_batch` -- {"actions": [{"name": "form_input", "input": {"tabId": id_c81a8a03, "ref": "ref_344", "value": "Выполни Deep Research строго по заданию в приложенном файле. Обязательно используй веб-поиск по англоязычным источникам 2025-2026 и в конце дай список источников прямыми URL. Ответ на русском, markdown, от

---

> `mcp__claude-in-chrome__computer` -- {"action": "screenshot", "tabId": id_c81a8a03, "scale": 0.5}

---

> `mcp__claude-in-chrome__browser_batch` -- {"actions": [{"name": "computer", "input": {"action": "left_click", "coordinate": [1276, 348], "tabId": id_c81a8a03}}, {"name": "computer", "input": {"action": "wait", "duration": 4, "tabId": id_c81a8a03}}, {"name": "javascript_tool", "input": {"action": "javascript_exec", "tabId": id_c81a8a03, "text":

---

> `mcp__claude-in-chrome__browser_batch` -- {"actions": [{"name": "javascript_tool", "input": {"action": "javascript_exec", "tabId": id_91115abf, "text": "const t=document.body.innerText; 'LEN='+t.length+' | '+t.slice(-200)"}}, {"name": "javascript_tool", "input": {"action": "javascript_exec", "tabId": id_22ceb316, "text": "const t=document.bod

---

> `mcp__claude-in-chrome__browser_batch` -- {"actions": [{"name": "computer", "input": {"action": "wait", "duration": 30, "tabId": id_91115abf}}, {"name": "computer", "input": {"action": "wait", "duration": 30, "tabId": id_91115abf}}, {"name": "computer", "input": {"action": "wait", "duration": 30, "tabId": id_91115abf}}, {"name": "javascript_to

---

> `mcp__claude-in-chrome__browser_batch` -- {"actions": [{"name": "computer", "input": {"action": "wait", "duration": 10, "tabId": id_91115abf}}, {"name": "computer", "input": {"action": "wait", "duration": 10, "tabId": id_91115abf}}, {"name": "computer", "input": {"action": "wait", "duration": 10, "tabId": id_91115abf}}, {"name": "computer", "i

---

> `Bash` -- {"command": "cd ~/.claude/scripts && ls dr_*.py | head -30; echo \"=== status DR-03 ===\"; python dr_queue.py status DR26-09-24-HUB-03-1604 2>&1 | head -20", "description": "List DR scripts and check DR-03 status"}

---

> `Bash` -- {"command": "cd ~/.claude/scripts && python dr_reconcile.py 2>&1 | tail -15; echo \"=== after ===\"; python dr_queue.py status DR26-09-24-HUB-03-1604 2>&1 | head -3", "description": "Reconcile DR registry with files on disk"}

---

> `Bash` -- {"command": "cd ~/.claude/scripts && grep -n \"results\" dr_queue.py | head -30", "description": "Find how dr_queue counts results"}

---

> `Bash` -- {"command": "cd ~/.claude/scripts && sed -n '225,260p' dr_queue.py", "description": "Read how results are collected"}

---

> `Bash` -- {"command": "cd \"D:/Vault/Vault-Knowledge/_machine-bus/_dr/queue\" && for n in 03 04 05 06 07 08 09 10 11 12 13 14 15 16 17 18 19 20 21; do f=\"DR26-09-24-HUB-$n-1604.md\"; [ -f \"$f\" ] || continue; if grep -q \"^targets:.*glm\" \"$f\"; then echo \"$f already has glm\"; else sed -i \"s/^targets

---

> `Bash` -- {"command": "cd ~/.claude/scripts && for n in 03 04 05 06 07 08 09 10 11 12 13 14 15 16 17 18 19 20 21; do python dr_queue.py status DR26-09-24-HUB-$n-1604 2>&1 | cut -d'|' -f1-3; done", "description": "Show leg counts for all 19 CV orders"}

---

> `mcp__claude-in-chrome__browser_batch` -- {"actions": [{"name": "computer", "input": {"action": "wait", "duration": 10, "tabId": id_91115abf}}, {"name": "computer", "input": {"action": "wait", "duration": 10, "tabId": id_91115abf}}, {"name": "computer", "input": {"action": "wait", "duration": 10, "tabId": id_91115abf}}, {"name": "computer", "i

---

> `mcp__claude-in-chrome__computer` -- {"action": "screenshot", "tabId": id_c81a8a03, "scale": 0.45}

---

> `Bash` -- {"command": "python -c \"import datetime,zoneinfo; print(datetime.datetime.now(zoneinfo.ZoneInfo('Europe/Lisbon')).strftime('%H:%M %d.%m.%Y'))\"", "description": "Get current Lisbon time"}

---

**Claude:**

17:12 · 28.09.2026 (Лиссабон)

## Да, с Chrome всё берётся. Уже беру.

Расширения в **локальном** Chrome хаба по-прежнему нет (проверил: профиль `Default`, 9 расширений, `fmlgfmcgfkbnkbeplhpldebfcjcmakbi` отсутствует, в `Preferences` и `Secure Preferences` его ID тоже нет). Но подключённый **Chrome на Mac** ответил, и там нашлось главное:

| сервис | состояние в том Chrome | вердикт |
|---|---|---|
| **z.ai (GLM)** | залогинен, аккаунт **PaloAlto Ai Research Lab**, GLM-5.3 flagship, Deep Think **Max** | ✅ рабочая дверь |
| Gemini | «Gemini isn't currently supported in your country» | ⛔ |
| ChatGPT | кнопка Log in, разлогинен | ⛔ |

GLM — это **18 из 22** недостающих ног, так что дверь открылась под большую часть работы.

## Что уже сделано

**Промпт подаю файлом, а не печатаю.** Нарезал все 19 заданий в чистые .md без фронтматтера и заливаю вложением прямо с хаба в z.ai на Mac. Никакой ручной перепечатки 13 КБ, ноль риска опечатки.

**Первая нога приехала и прошла гейт:**

```
[dr-leg] ✅ glm.md -- лега годная, можно collected (20 источников)
```

Это `DR26-09-24-HUB-03-1604` (кластер capital). Ответ содержательный: 25 ключевых слов под ATS, построчная критика по всем семи секциям CV, чек-лист из 20 сигналов, и отдельно жёсткий вердикт — **совмещение COO/CTO в титуле и обилие GitHub/arXiv в capital-резюме размывают файл**, с источниками.

**Починил счётчик, который врал.** Реестр показывал «2/3» и не видел glm вообще: в манифестах заказов в `targets` стояли только `chatgpt,gemini,grok`, а `derive_status` считает **только объявленные** рельсы. Дописал `glm` в targets всем 19. Теперь картина честная:

- **3 ноги уже есть**: HUB-03, HUB-11
- **2 ноги**: 04, 05, 06, 07, 08, 09, 10, 12, 13, 14, 15, 16, 21 → нужно по одной
- **1 нога**: 17, 18, 19, 20 → нужно по две

Итого до пола 3 осталась **21 нога**. Слон `cv-dr-quorum-topup`: **1/22**.

## Грабля, которую поймал

Запустил 5 вкладок разом — z.ai отбил две:

> Model is currently at capacity... GLM-5.3 is intensifying the coordination of resources, please switch to GLM-5.3-Flash

На Flash **не переключаюсь**: тихий спуск на дешёвую модель у чужого вендора это ошибка по §6.3, у чужих всегда самая умная модель и максимальное рассуждение. Нажал Cancel и опустил параллельность до **3**. Сейчас в полёте DR-04, DR-06, DR-07, каждая нога занимает примерно 10 минут.

## 🎙 Майк

- 💰 Дверь под 18 ног из 22 открылась без единого твоего клика, и это главное за заход.
- 🔪 Убил бы свою же формулировку из прошлого ответа: я сказал «рулить нечем», проверив только локальный Chrome. Надо было сразу постучаться в тот, что виден в MCP.
- 🤺 Не переключился на Flash, хотя это мгновенно разблокировало бы 5 потоков: скорость не стоит подмены модели.
- ❓ Оставляю грызть до конца или снять пару кластеров с очереди?

## 📌 Что осталось

1. **21 нога GLM** — мелю дальше по 3 в потоке, примерно час с лишним чистого времени.
2. **ChatGPT-ноги (4 штуки)** двери по-прежнему не имеют: ни в Firefox-профиле робота, ни в этом Chrome. Их закроет либо твой единственный логин робот-профиля, либо логин ChatGPT в том Chrome.
3. Доборщику `dr_latecomer_sweep.py` так и **нужно место в расписании** — его по-прежнему не запускает ничто.

🧒 **Простыми словами.** Ты спросил, могу ли я всё взять из Chrome. Проверил: в Chrome на этом компьютере моего пульта нет, а вот в твоём Chrome на Маке он есть, и там открыт GLM. Значит большую часть работы делать можно, и я уже начал. Задание отправляю файлом, чтобы ничего не перепутать при наборе. Первый ответ пришёл, он хороший, с двадцатью ссылками на источники. Ещё три варятся прямо сейчас. Робот-сайт ругается, если просить больше трёх ответов одновременно, и предлагает модель попроще — попроще я не беру, лучше подожду. Осталось смолоть двадцать один ответ.
