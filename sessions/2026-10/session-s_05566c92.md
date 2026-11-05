---
session: s_05566c92
date: 2026-10-19
words: 1475
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-10-19 · You are distilling a DEEP-RESEARCH report into a compact, searchable knowledge note

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_05566c92` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

You are distilling a DEEP-RESEARCH report into a compact, searchable knowledge note.
One report, possibly assembled from several AI vendors researching the SAME question.

DR-ID: DR26-10-18-HUB-11-1034
REGISTRY TOPIC: AI safety fellowships Constellation Redwood: шанс отбора и найм (через dr_start; ПОТРЕБИТЕЛЬ: Адресные заявки оператора после исследования; дедуп прежних подач) (dr_reconcile 2026-10-19: на диске 1/6 ног, в реестре стояло 'running' — статус выправлен по факту. Тело ног: D:\Vault\Vault-Knowledge\_machine-bus\_dr\queue\DR26-10-18-HUB-11-1034\results)

Return ONLY a JSON object (no prose, no code fence) with EXACTLY these keys:
{
 "lang": "ru|en|mixed",
 "topic": "<clean human topic of the research, <=90 chars>",
 "one_line": "<one sentence: what question this deep-research answered>",
 "key_findings": ["<substantive conclusion grounded in the report>", "..."],
 "recommendations": ["<concrete recommendation / decision the report implies>", "..."],
 "entities": {"people": ["..."], "companies": ["..."], "products_tools": ["..."]},
 "open_questions": ["<what stayed unresolved / needs verification>", "..."],
 "related_concepts": ["<short concept name this connects to, for cross-linking>", "..."]
}
Rules: extract ONLY from the report text; never invent people, numbers or claims not present.
Merge across the vendor sections (they research the SAME question) -- deduplicate findings,
prefer the better-supported statement. 4-10 key_findings, be specific (numbers, names, tradeoffs).
If a list is empty use []. Write findings in the report's own language (ru stays ru).

REPORT (vendor sections tagged; may be Russian, English or mixed):


===== VENDOR: report (DR26-10-18-HUB-11-1034.md) =====
---
id: DR26-10-18-HUB-11-1034
date: 2026-10-18 10:34:35
theme: AI safety fellowships Constellation Redwood: шанс отбора и найм
session_id: s_9dfaa538
machine: HUB-01
targets: chatgpt,claudeai,gemini,grok,glm,mistral
---

# DR26-10-18-HUB-11-1034 — AI safety fellowships Constellation Redwood: шанс отбора и найм

# Fellowship applications and AI safety hiring: maximize selection chances

Machine: HUB-01 (Хаб) · Agent: Codex · Operator: dev · 2026-10-18

Research date: 18 October 2026. Consumer: dev's applications, after research, to AI safety fellowships and jobs. Research only: do not submit forms or contact anyone.

Find current opportunities and a concrete evidence-based strategy to maximize selection chances. Use official primary sources, citations and exact application links. Separate dated history, current verified facts, inference and unknown. No invented acceptance probabilities.

Candidate: experienced Python/C++ engineer and hired COO/CTO, with public OSS contributions and work on coding-agent oversight, evaluation/scoring correctness and agent operations. Do not call him a founder. Do not infer ML-training experience, degrees, security tenure, nationality, work authorization, personal motivations, achievements or counts; these need verification in his own dossier. Identify which evidence must be gathered before claiming fit.

Cover Constellation Astra (empirical and strategy/governance), Visiting Fellowship, Generator Winter 2027, MATS regular fellowship and Bridge/Anchor/Incubation Residency, SPAR, PIBBSS/Principles of Intelligence, Pivotal, LASR, ERA, Iliad, AI Safety Camp, AI Security Bootcamp London, Anthropic Fellows, OpenAI Safety Fellowship. Discover comparable programs beyond this list. Cover London, Berkeley and other relevant locations.

Previous local records: on 30 September 2026, full applications to AI Safety Camp Project Lead and AISB London, plus expressions of interest to Astra, Visiting, Generator, SPAR, PIBBSS, MATS, LASR, Pivotal and future AISB cohorts. Anthropic Fellows canonical application submitted 1 October. These are historical records to deduplicate, not current admissions or proof that future applications are covered. Iliad was filled but blocked before submission. MATS Residency had a separate draft, not proof of submission. AISB invited a technical assessment on 4 October; its seven-day window expired, and a 14 October request for a new link was found as a DRAFT in the available mailbox.

Official pages checked this morning: Generator Winter 2027 open until 1 November AoE, international applicants encouraged by 26 October, program 18 January–9 April 2027, $8,500/month. It expressly prohibits AI writing, rewriting, polishing and translation of free responses; high-level feedback allowed. Respect the policy: give evidence/preparation advice, do not write candidate answers. MATS Residency open until 31 October AoE; permits disclosed AI assistance; CV maximum 2 pages, two references, substantial representative work sample and research plan. Reverify all claims.

For each program report: intake, actual open/closed/rolling/EOI status, exact deadline and timezone, stipend versus expenses/compute budget versus fees, full-time/in-person requirements, location, eligibility, application materials, AI-use policy, selection stages, work tests and likely evaluation criteria. Track-specific eligibility matters. Do not confuse an incubator, unpaid mentorship, a notification signup and a salaried job.

For hiring inspect official boards of Constellation, Redwood, METR, ARC, FAR.AI, Apollo, GovAI and adjacent employers. Give live role titles, individual ATS URLs, salary basis/currency, location, eligibility, required evidence and fit. Prior local notes mention Redwood MTS $350–850K, but today's careers page labels its open role Empirical Researcher: use the current title. Do not assume old vacancies remain open. Research/engineering, security/evals, program management, operations and talent roles all matter; avoid crowdwork and outsourced badges.

Deliver: (1) current opportunity matrix, (2) ranked deadlines and next actions, (3) distinct positioning and evidence gaps by track, (4) adversarial critique of likely rejection reasons, (5) concrete improvements before submission, (6) compliant handling of no-AI answers and tests, (7) shortlist of genuine work samples and referee qualities to seek, without inventing candidate facts, (8) sequential application plan that checks receipt, replies and next-stage deadlines. Include source dates and conflicting/stale pages. State what cannot be judged.

---

**Claude:**

{"lang":"mixed","topic":"Стипендии по безопасности ИИ и найм: шансы отбора (Constellation, Redwood, MATS и др.)","one_line":"Какие программы и вакансии по безопасности ИИ открыты на 18.10.2026 и какая стратегия повышает шансы отбора для оператора (Python/C++ инженер, нанятый COO/CTO).","key_findings":["В присланном тексте нет самих результатов исследования: это только постановка задачи (бриф) с датой 2026-10-18, без таблиц программ, ссылок, выводов и источников. Все findings ниже взяты только из этого брифа и не являются проверенными результатами.","Generator Winter 2027 (по данным брифа, проверено утром 18.10): приём открыт до 1 ноября AoE, международным кандидатам рекомендуют податься к 26 октября, программа 18 января – 9 апреля 2027, $8 500 в месяц. Использование ИИ для написания, переписывания, полировки и перевода свободных ответов запрещено, допустима только общая обратная связь.","MATS Residency (по брифу): приём открыт до 31 октября AoE; раскрытое использование ИИ допускается; резюме не более 2 страниц, две рекомендации, существенный образец работы и исследовательский план.","Прошлые подачи по локальным записям, которые нужно дедуплицировать, а не считать покрытием будущих заявок: 30.09.2026 полные заявки в AI Safety Camp (Project Lead) и AISB London, плюс expressions of interest в Astra, Visiting, Generator, SPAR, PIBBSS, MATS, LASR, Pivotal и будущие когорты AISB; Anthropic Fellows подана 1.10.","Незакрытые хвосты по прошлым подачам: Iliad заполнен, но заблокирован до отправки; у MATS Residency был отдельный черновик (отправка не доказана); AISB пригласил на техническое задание 4.10, семидневное окно истекло, запрос новой ссылки от 14.10 лежит в ящике как DRAFT.","Старые локальные заметки называют вакансию Redwood «MTS $350–850K», но текущая страница вакансий называет открытую роль «Empirical Researcher»: использовать нужно актуальное название, а старым вакансиям открытость не приписывать.","Профиль кандидата ограничен: опыт ML-обучения, степени, срок в безопасности, гражданство, разрешение на работу, мотивы и достижения нельзя выводить, их нужно подтверждать досье самого оператора; основа для позиционирования: Python/C++, роль нанятого COO/CTO, публичные OSS-вклады, работа над надзором за кодовыми агентами, корректностью оценки/скоринга и эксплуатацией агентов.","Вероятности принятия выдумывать нельзя; нужно разделять датированную историю, проверенные текущие факты, выводы и неизвестное, а также различать инкубатор, неоплачиваемое наставничество, подписку на уведомления и оплачиваемую должность."],"recommendations":["Приоритет по срокам: Generator (международным до 26 октября, общий дедлайн 1 ноября AoE) и MATS Residency (31 октября AoE); перед подачей перепроверить все даты и условия на официальных страницах.","Для Generator не писать ответы за кандидата и не использовать ИИ для текста свободных ответов: давать только советы по доказательствам и подготовке, а общую обратную связь получать от людей или ИИ строго в разрешённом объёме.","Для MATS подготовить резюме до 2 страниц, двух рекомендателей, реальный репрезентативный образец работы и исследовательский план, раскрыв использование ИИ.","До подачи собрать в досье оператора подтверждаемые доказательства соответствия по каждому треку, не заявляя недоказанного.","Перед новыми подачами сверить локальные записи, чтобы не дублировать уже отправленные заявки (AI Safety Camp, AISB, Anthropic Fellows).","Разобрать хвосты: выяснить статус Iliad, отправлен ли черновик MATS Residency, запросить у AISB новую ссылку на техническое задание (черновик письма от 14.10 не отправлен).","Мониторить официальные карьерные страницы Constellation, Redwood, METR, ARC, FAR.AI, Apollo, GovAI и смежных работодателей, брать названия ролей, ссылки ATS и валюту оклада только из живых страниц; рассматривать не только исследовательские, но и роли по безопасности/оценкам, программному менеджменту, операциям и талантам, избегая краудворка и аутсорс-бейджей.","Подавать заявки последовательно с проверкой подтверждения получения, ответов и дедлайнов следующих этапов, и честно фиксировать, что нельзя оценить."],"entities":{"people":["dev"],"companies":["Constellation","Redwood Research","METR","ARC","FAR.AI","Apollo Research","GovAI","Anthropic","OpenAI","MATS","SPAR","PIBBSS","Pivotal","LASR","ERA","Iliad","AI Safety Camp","AISB"],"products_tools":["Constellation Astra","Constellation Visiting Fellowship","Generator Winter 2027","MATS Residency","AI Security Bootcamp London","Anthropic Fellows","OpenAI Safety Fellowship","Codex"]},"open_questions":["Результаты исследования отсутствуют в предоставленном тексте: матрица программ, дедлайны, часовые пояса, стипендии, требования, этапы отбора и критерии оценки не получены и требуют проверки по первоисточникам.","Какие живые вакансии сейчас открыты у Constellation, Redwood, METR, ARC, FAR.AI, Apollo, GovAI, их ссылки ATS, валюта и основа зарплаты?","Отправлена ли заявка на MATS Residency и каков статус Iliad?","Какие доказательства из досье оператора (опыт ML, степени, срок в безопасности, гражданство и разрешение на работу, достижения) можно подтвердить?","Какие сопоставимые программы за пределами перечня существуют, помимо Лондона и Беркли?","Какие страницы устарели или конфликтуют (например, старый «Redwood MTS $350–850K» против «Empirical Researcher»)?"],"related_concepts":["стипендии и программы по безопасности ИИ","позиционирование кандидата и пробелы в доказательствах","политика использования ИИ в заявках","дедупликация прошлых подач","приоритизация дедлайнов","найм в организациях по безопасности ИИ","надзор за кодовыми агентами и корректность оценки"]}
