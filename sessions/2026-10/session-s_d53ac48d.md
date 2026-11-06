---
session: s_d53ac48d
date: 2026-10-29
words: 1772
turns: 13
tools: "Bash, Read, ToolSearch, WebFetch, WebSearch, Write, mcp__whatsapp2__download_media, mcp__whatsapp2__list_messages, mcp__whatsapp__list_messages"
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-10-29 · Сделай ДР по его компании. Возьми его презентации из ватсапа

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_d53ac48d` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

Сделай ДР по его компании. Возьми его презентации из ватсапа

Скажи сколько у него в компании сотрудник, сколько он зарабатывают

Средняя сумма и время контракта 

Все подробно чтобы я понял стоит ли повторить его бизнес

E:\!CLAUDE-HUBPC-June26\downloads\photo_2026-10-29_13-22-46.jpg

---

> `Read` -- {"file_path": "E:\\!CLAUDE-HUBPC-June26\\downloads\\photo_2026-10-29_13-22-46.jpg"}

---

**Claude:**

Контакт: Mehdi, [ТЕЛЕФОН]. Ищу чат в WhatsApp (оба аккаунта).

---

> `ToolSearch` -- {"query": "select:mcp__whatsapp__search_contacts,mcp__whatsapp2__search_contacts,mcp__whatsapp__list_messages,mcp__whatsapp2__list_messages,mcp__whatsapp__download_media,mcp__whatsapp2__download_media,mcp__whatsapp__get_chat,mcp__whatsapp2__get_chat", "max_results": 10}

---

> `mcp__whatsapp__list_messages` -- {"jid": "id_829af891", "limit": 100}

---

> `mcp__whatsapp2__list_messages` -- {"jid": "id_829af891", "limit": 100}

---

**Claude:**

Нашёл: три документа от Mehdi 16.10. Скачиваю.

---

> `mcp__whatsapp2__download_media` -- {"jid": "id_829af891", "messageId": "4A59D8A8CB32BFAFA402"}

---

> `mcp__whatsapp2__download_media` -- {"jid": "id_829af891", "messageId": "4A99A3AB3D7D9CCD5604"}

---

> `mcp__whatsapp2__download_media` -- {"jid": "id_829af891", "messageId": "4A7986F4C750FFAE8490"}

---

> `Bash` -- {"command": "cd \"C:/Users/dev/.local/share/wa-wa2/whatsapp-mcp/downloads\" && for f in 4A59D8A8CB32BFAFA402 4A99A3AB3D7D9CCD5604 4A7986F4C750FFAE8490; do echo \"===== $f\"; python -c \"\nimport sys\nfrom pypdf import PdfReader\nr=PdfReader('$f.pdf'); print('pages',len(r.pages))\nfor i,p in enumer

---

**Claude:**

Три PDF прочитаны. В деке страницы 5 и 9 картинки, рендерю их, параллельно ищу компанию в открытых источниках.

---

> `Bash` -- {"command": "cd \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_d53ac48d/scratchpad\" && python -c \"\nimport fitz\nd=fitz.open(r'C:/Users/dev/.local/share/wa-wa2/whatsapp-mcp/downloads/4A99A3AB3D7D9CCD5604.pdf')\nfor i in (4,8):\n  d[i].get_pixm

---

> `ToolSearch` -- {"query": "select:WebSearch,WebFetch", "max_results": 2}

---

> `Read` -- {"file_path": "C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_d53ac48d\\scratchpad\\deck_p5.png"}

---

> `Read` -- {"file_path": "C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_d53ac48d\\scratchpad\\deck_p9.png"}

---

> `WebFetch` -- {"url": "https://saenaaigroup.com", "prompt": "Summarize everything: services, pricing, team size, clients, location, partner status, founding date, any revenue or headcount claims."}

---

> `WebSearch` -- {"query": "\"Saena AI\" Mehdi Tabdili", "mode": "standard"}

---

> `WebSearch` -- {"query": "Anthropic Claude Partner Network consulting partners program 2026 requirements referral", "mode": "standard"}

---

**Claude:**

Сайт нашёл. Ищу численность (LinkedIn, регистрации), Konekti, Cypress Consulting и наши заметки о звонке с ним.

---

> `WebSearch` -- {"query": "\"Saena AI Group\" Claude", "mode": "extended"}

---

> `WebSearch` -- {"query": "Cypress Consulting acquired by System One 2026 Amir Tabdili", "mode": "standard"}

---

> `WebSearch` -- {"query": "Claude Partner Network Services Track tiers Registered Select Preferred certified individuals number required", "mode": "standard"}

---

> `Bash` -- {"command": "grep -rli -E \"saena|tabdili|8203416|820-3416\" \"D:/Vault/Vault-Knowledge\" --include=*.md 2>/dev/null | head -20; echo ---; grep -rli -E \"saena|tabdili\" \"E:/!CLAUDE-HUBPC-June26/crm-engine\" 2>/dev/null | head; echo ---; python D:/Vault/_imports/brain_ask.py \"Mehdi Saen

---

> `WebSearch` -- {"query": "site:linkedin.com \"Saena AI Group\"", "mode": "extended"}

---

> `WebSearch` -- {"query": "Konekti Systems network Claude agents", "mode": "standard"}

---

> `WebSearch` -- {"query": "Claude implementation consulting boutique hourly rate engagement size 2026 AI consultancy revenue per consultant", "mode": "extended"}

---

**Claude:**

Konekti может быть их же собственной компанией: проверяю, это важно для оценки «кейса».

---

> `WebFetch` -- {"url": "https://konekti-ai-website.pages.dev/", "prompt": "Who founded/runs Konekti? Any names (Tabdili, Cypress), team, location, relationship to Saena or Cypress Consulting? Customers, pricing."}

---

> `WebFetch` -- {"url": "https://saenaaigroup.com/", "prompt": "List verbatim: all client logos/names and how they are described (client vs partner), team members, any case study numbers, the exact phrase around $10M client value, and all page links (about, team, cases, pricing). Also any footer company legal name/

---

> `WebSearch` -- {"query": "\"Mehdi Tabdili\"", "mode": "extended"}

---

> `WebFetch` -- {"url": "https://reports.adviserinfo.sec.gov/reports/individual/individual_7177275.pdf", "prompt": "Extract: full name, other names, CRD, firms and dates, locations, exams/qualifications, and the full text of any disclosure events (regulatory actions, dates, regulator, allegations, sanctions, fines)

---

> `WebFetch` -- {"url": "https://www.linkedin.com/in/mehdi-tabdili-a968729/", "prompt": "Extract current position, Saena, employers with dates, education, CFA, location, followers."}

---

> `Bash` -- {"command": "python -c \"\nfrom pypdf import PdfReader\nr=PdfReader(r'C:\\Users\\dev\\.claude\\projects\\P---WORKDIR-HUB\\s_d53ac48d\\tool-results\\webfetch-1793288761204-uy8bsl.pdf')\nprint('\\n'.join((p.extract_text() or '') for p in r.pages))\" | head -c 1

---

> `Bash` -- {"command": "python -c \"\nfrom pypdf import PdfReader\nr=PdfReader(r'C:\\Users\\dev\\.claude\\projects\\P---WORKDIR-HUB\\s_d53ac48d\\tool-results\\webfetch-1793288761204-uy8bsl.pdf')\nt='\\n'.join((p.extract_text() or '') for p in r.pages); i=t.find('This re

---

**Claude:**

Это меняет картину. Одна быстрая проверка связи Konekti с братом (Amir, Cypress), потом считаю экономику.

---

> `WebSearch` -- {"query": "Konekti konekti.us Cypress Consulting Tabdili network automation", "mode": "standard"}

---

> `Read` -- {"file_path": "C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_d53ac48d\\tasks\\b3dnlpgvz.output"}

---

> `Bash` -- {"command": "mkdir -p \"E:/!CLAUDE-HUBPC-June26/docs/research/saena-ai-group\" && cp \"C:/Users/dev/.local/share/wa-wa2/whatsapp-mcp/downloads/4A99A3AB3D7D9CCD5604.pdf\" \"E:/!CLAUDE-HUBPC-June26/docs/research/saena-ai-group/saena-pitch-deck.pdf\" && cp \"C:/Users/dev/.local/share/wa-w

---

> `Write` -- {"file_path": "E:\\!CLAUDE-HUBPC-June26\\docs\\research\\saena-ai-group\\README.md", "content": "---\ntitle: Saena AI Group (Mehdi Tabdili) — разбор бизнеса и стоит ли повторять\ndate: 2026-10-29\ntype: research\nmethod: ИДР (инхаус: 3 PDF из WhatsApp + веб + реестр SEC/FINRA); веер внешних LLM

---

> `Bash` -- {"command": "python ~/.claude/scripts/machine_stamp.py sig --model \"Opus 5.5\"", "description": "Get message signature line"}

---

**Claude:**

15:48 (Лиссабон)

Я разобрал компанию Mehdi. Сделал это сам: три PDF из его чата в WhatsApp (второй аккаунт, прислал 16.10), его сайт и государственные реестры США. Опрос нескольких внешних нейросетей (полный ДР) не запускал, это был мой собственный разбор.

## Коротко
**Компания: Saena AI Group, Вашингтон.** Они внедряют Claude в компании из регулируемых отраслей: финансы, медицина, госсектор. Сами себя называют «только Claude». В партнёрской программе Anthropic у них начальный уровень: вступить может любой, членство бесплатное.

**Сотрудники.** В презентации 5 человек:
- сам Mehdi;
- его брат Amir. Его компанию Cypress Consulting купила System One в январе 2026, так что он, скорее всего, ещё занят там;
- руководитель аппарата (chief of staff);
- менеджер по госзаказам;
- AI-продакт.

Начальный уровень партнёрства это подтверждает: на следующий уровень нужно минимум 10 сертифицированных людей и 2 клиента с работающим внедрением.

**Сколько зарабатывают.** Публичных цифр нет. Строка на сайте «$10M+ client value delivered» означает «пользу для клиентов», а не их выручку. По ценам из его образца коммерческого предложения я оцениваю **$200–800 тыс. в год сейчас**. Если все пятеро будут полностью загружены, потолок около $1.5–2 млн. Это моя оценка, не данные.

**Средний контракт и срок.** Это из его же образца предложения:
- ставка **$275 в час**;
- первый блок 60 часов = **$16 500**, полный объём **$16.5–27.5 тыс.**;
- срок **около 4 недель** при 15 часах в неделю;
- оплата 50% при подписании и 50% в конце;
- полудневный тренинг продаётся отдельно за $3 500.

Дальше клиента переводят на ежемесячную абонентскую плату. Её сумму он не называет.

**Как устроена воронка:**
1. 10-дневный аудит за фиксированную цену. Смотрят, кто и как пользуется Claude, сколько уходит на токены, где дыры в безопасности подключений и требованиях регуляторов.
2. Ежемесячная абонентка: «фабрика» рабочих сценариев плюс контроль расходов.
3. Для регулируемых отраслей: независимая проверка готовых AI-сценариев, как в банковском контроле моделей.

## 🚩 Главное, что надо знать
В открытом реестре финансовых советников (SEC/FINRA, номер 7177275) на **Mehdi Tabdiliazar** есть дело штата Вирджиния SEC-2021-00017. Суть:
- он писал «CFA» (престижный сертификат финансового аналитика) в LinkedIn и на сайтах;
- когда попросили подтверждение, **прислал поддельный сертификат**, а потом признал, что CFA у него нет;
- итог: пожизненный запрет работать финансовым советником в Вирджинии и штраф $4 000, который он заплатил. Дело окончательно закрыто 16.01.2024.

В презентации Saena 2026 года снова написано «CFA».

Что это тот же человек, я уверен сильно, но не на 100%. Совпадают имя, работа портфельным менеджером во Всемирном банке с 2014 года, город (Вашингтон/Арлингтон) и его X-аккаунт @mtabdili, подписанный «Mehdi Tabdiliazar». Не проверял реестр самого CFA Institute: теоретически он мог получить сертификат позже.

Ещё два непроверенных места:
- Его главный кейс, компания Konekti (17 агентов для управления сетями), по профилю совпадает с бизнесом его брата. Возможно, это «свой» клиент 🤔.
- Логотипы Kirkland & Ellis, Francisco Partners и других подтверждены только его собственным сайтом.

## Стоит ли повторять
🎙 Майк: **Да, повторять стоит, а партнёрствовать с ним стоит только аккуратно.**

- **Войти легко.** Членство в партнёрской программе бесплатное, нужен экзамен CCA-F. Его преимущество в связях среди финансистов Вашингтона, а не в технологиях.
- **Технологически мы сильнее.** У нас уже есть публичные репозитории ровно под его аудит: `llm-spend-audit` (расходы на токены), `mcp-daemon-diet` (подключения MCP), `agent-approval-gate` (контроль того, что агент записывает в боевые системы). Он продаёт как услугу то, что у нас уже лежит готовым кодом.
- **Против.** Рынок быстро забивается: за 3 месяца в программу подали 40 тыс. заявок и сертифицировали 10 тыс. консультантов. Ставки на рынке $100–350 в час. Продавать регулируемым компаниям долго, решает доверие.
- **С Mehdi.** Рефералка только письменно и только после оплаты клиентом. Твоё имя на его материалы не ставить: история с поддельным сертификатом ударит по любому, кто рядом.

Следующий шаг, если хочешь: запущу полный ДР веером на 3+ внешние нейросети (у кого из партнёров Claude реальная выручка, какие ниши ещё свободны) и сделаю наш одностраничник «аудит Claude» поверх трёх репозиториев.

Отчёт и исходники: [README.md](docs/research/saena-ai-group/README.md). Рядом лежат 3 его PDF и выписка из реестра SEC (`sec-iapd-7177275.pdf`).

Источники:
- [saenaaigroup.com](https://saenaaigroup.com/)
- [SEC IAPD отчёт 7177275](https://reports.adviserinfo.sec.gov/reports/individual/individual_7177275.pdf)
- [Дело Virginia SCC](https://www.scc.virginia.gov/DocketSearch#/caseDetails/142071)
- [System One покупает Cypress Consulting](https://pulse2.com/system-one-acquires-cypress-consulting-to-expand-data-center-network-engineering-automation-and-security-services/amp/)
- [Уровни Claude Partner Network](https://www.anthropic.com/news/services-track-partner-hub)
- [Обзор уровней CPN](https://kanerika.com/blogs/claude-partner-network/)
- [Ставки AI-консалтинга 2026](https://pulseaisolutions.com/ai-consultant-hourly-rate-2026/)
- [Konekti](https://konekti-ai-website.pages.dev/)

🏛H · Opus 5.5 · 30139

---

**User:**

<task-notification>
<task-id>b3dnlpgvz</task-id>
<tool-use-id>toolu_01SNJ2pEPvPPLUCXXDF4wJy8</tool-use-id>
<output-file>C:\Users\dev\AppData\Local\Temp\claude\P---WORKDIR-HUB\s_d53ac48d\tasks\b3dnlpgvz.output</output-file>
<status>completed</status>
<summary>Background command "RECALL: search vault, CRM and RAG for Mehdi/Saena" completed (exit code 0)</summary>
</task-notification>

---

> `Read` -- {"file_path": "C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_d53ac48d\\tasks\\b3dnlpgvz.output"}

---

> `Bash` -- {"command": "cd \"D:/Vault/Vault-Knowledge/07-People\" && wc -c mehdi-tabdili-saena-ai.md; grep -n -i -E \"сотрудн|employee|headcount|revenue|выручк|\\\\\\$|час|hour|retainer|ретейн|CFA|team|команд|контракт|клиент\" mehdi-tabdili-saena-ai.md | head -40; ls | grep -i mehdi", "description": "Check 

---

> `Read` -- {"file_path": "D:\\Vault\\Vault-Knowledge\\07-People\\mehdi-tabdili-saena-ai.md"}

---

**Claude:**

Нашлось важное, что меняет две цифры в отчёте. Обновляю отчёт и карточку Mehdi.

---

> `Bash` -- {"command": "cp \"D:/Vault/Vault-Knowledge/07-People/mehdi-tabdili-saena-ai.md\" \"E:/!CLAUDE-HUBPC-June26/_app-backups/mehdi-tabdili-saena-ai-H30139-20261029.before.md\" && cat >> \"D:/Vault/Vault-Knowledge/07-People/mehdi-tabdili-saena-ai.md\" <<'EOF'\n\n## 🚩 Проверка 29.10.2026: регуля

---

**Claude:**

15:55 (Лиссабон)

Поиск по нашей памяти закончился позже ответа и нашёл запись твоего звонка с Mehdi 14.10. Она меняет ответ про сотрудников и добавляет ещё одно расхождение.

**Сотрудники: три источника говорят разное.**
- На звонке он сказал: «около 20 человек с сертификатами Anthropic».
- В презентации в разделе «Наша команда» 5 человек.
- В публичном каталоге партнёров Anthropic (снимок 07.10) его фирмы нет. Значит, в лучшем случае у него начальный уровень, где обычно меньше 10 сертифицированных людей.

Я верю презентации: **около 5 человек**. Цифру 20 подтвердить нечем.

**Ещё одно расхождение.** На звонке он сказал, что «продал сетевую компанию полтора года назад». Сетевую Cypress Consulting продали всего 9 месяцев назад, в январе 2026, и её CEO был брат Amir.

**Его предложение нам (со звонка):** 20% комиссии с каждого клиента, которого мы приведём, на всё время сотрудничества.

**Где мы сейчас.** 23.10 мы ответили ему письмом и попросили почту на домене @saena.ai и место на экзамене CCA-F: без почты фирмы-партнёра на этот экзамен не записаться. Он пока не ответил.

С учётом истории с поддельным сертификатом я бы брал у него только этот доступ к экзамену и комиссию, письменно и после оплаты клиентом. Нигде не стоять рядом с ним по имени. Выручку и размер контракта я не меняю.

Что обновил:
- Отчёт: [README.md](docs/research/saena-ai-group/README.md).
- Карточка Mehdi в волте `07-People/mehdi-tabdili-saena-ai.md`: дописан раздел про дело в реестре и расхождения. Копия до правки лежит в `_app-backups/mehdi-tabdili-saena-ai-H30139-20261029.before.md`.

Следующий шаг: полный ДР веером на внешние нейросети по нише «внедрение Claude» (какие ниши ещё свободны и кто реально зарабатывает) запущу по твоему «+».

🏛H · Opus 5.5 · 30139

---

**User:**

<task-notification>
<task-id>bblai4fny</task-id>
<tool-use-id>toolu_019CzmJYKnUh5bBVstEynRPw</tool-use-id>
<output-file>C:\Users\dev\AppData\Local\Temp\claude\P---WORKDIR-HUB\s_d53ac48d\tasks\bblai4fny.output</output-file>
<status>completed</status>
<summary>Background command "Check existing Mehdi card for numbers" completed (exit code 0)</summary>
</task-notification>

---

**Claude:**

Ничего нового: фоновая проверка карточки Mehdi закончилась, а эту карточку я уже прочитал напрямую и учёл в прошлом сообщении. Отчёт не меняется.

🏛H · Opus 5.5 · 30139
