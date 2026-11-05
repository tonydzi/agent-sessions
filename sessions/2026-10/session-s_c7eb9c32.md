---
session: s_c7eb9c32
date: 2026-10-19
words: 5509
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-10-19 · You are distilling a DEEP-RESEARCH report into a compact, searchable knowledge note

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_c7eb9c32` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

You are distilling a DEEP-RESEARCH report into a compact, searchable knowledge note.
One report, possibly assembled from several AI vendors researching the SAME question.

DR-ID: DR26-10-18-HUB-10-1034
REGISTRY TOPIC: AI vendor fellowships residencies paid research entry programs global update 2026-10-18 (втащен в очередь dr_start --adopt; ПОТРЕБИТЕЛЬ: Two routines: discovery and deduplicated applications) (dr_reconcile 2026-10-19: на диске 1/6 ног, в реестре стояло 'running' — статус выправлен по факту. Тело ног: D:\Vault\Vault-Knowledge\_machine-bus\_dr\queue\DR26-10-18-HUB-10-1034\results)

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


===== VENDOR: grok (DR26-10-18-HUB-10-1034-dr-grok.md) =====
Собираю живые страницы программ и проверяю дедлайны по первичным источникам.A. Сводка на 18 октября 2026

Проверено живыми страницами в этом прогоне. Год и часовой пояс ставлю только там, где они напечатаны на источнике. «October 18» без года и без пояса не превращаю в «23:59 PT».

Срочные живые окна

1. Сегодня, 18 октября, без напечатанного года и без пояса. Anthropic Fellows, AI Safety & Security, январская когорта. Страница, открытая 18.10.2026, всё ещё пишет «Applications are now open» и «apply here by October 18». Заявка по инструкции JD идёт в портал Constellation, не в нативную отправку Greenhouse: https://bit.ly/afpsafety открылся как Airtable https://airtable.com/appceerp9YQRlwDhU/pagW63dilE5oV7cPY/form . Источник: https://job-boards.greenhouse.io/anthropic/jobs/id_2e26dffe и https://alignment.anthropic.com/2025/anthropic-fellows-program-2026/ . Оплата 3850 USD / 2310 GBP / 4300 CAD в неделю, 4 месяца, compute около 15 тыс. USD в месяц. Нужны уже имеющиеся право работы и нахождение в US, UK или Canada. Визу не спонсируют. Python обязателен. Студенческий статус не требуется.

2. Сегодня, 18 октября, день назван Sunday, пояс не назван. AI Safety Camp, 12-й виртуальный набор, заявки лидов проектов. Команда участника откроется 7–29 ноября. Стипендии в целом нет. https://www.aisafety.camp/

3. 19 октября 2026, пояс не напечатан. Iliad Fellowship, когорта 1 декабря 2026 – 5 марта 2027, London или Bay Area. Пособие на дорогу и жильё 6000 USD в месяц, не зарплата. Математический уклон, типично PhD или эквивалент. https://www.iliad.ac/ и https://www.iliad.ac/fellowship

4. 26 октября 2026, это не жёсткий дедлайн, а рекомендация для международных заявителей из-за визы. Generator Residency. Жёсткое закрытие: конец дня 1 ноября 2026, Anywhere on Earth. https://generatorresidency.org/

5. 28 октября 2026, пояс не напечатан. Anthropic STEM Fellow и Conceptual Reasoning Fellow, 12 января – 8 мая 2027. 100–167 тыс. USD за 4 месяца. Только US work authorization, визу не спонсируют. STEM: PhD и несколько лет опыта. Conceptual: PhD или эквивалентный исследовательский опыт. https://job-boards.greenhouse.io/anthropic/jobs/id_b016af84 и https://job-boards.greenhouse.io/anthropic/jobs/id_b8244b3d

6. 30 октября 2026, включая рекомендательные письма, пояс не напечатан. NVIDIA Graduate Fellowship 2027–2028, до 60 000 USD. Только действующий PhD-студент после первого года. Для заявленного нестудента это не очередь. https://research.nvidia.com/graduate-fellowships

7. 31 октября 2026, AoE. MATS Residency, зимнее окно 2027. 155–285 тыс. USD в год gross, 6–24 месяца, London / Berkeley / Washington DC, визовая поддержка. Прямо рассчитана на опытных людей вне PhD-титула. https://www.matsprogram.org/residency и форма https://forms.matsprogram.org/residency-w27

Без календарного дедлайна, но форма на странице живая. Anthropic ML Systems & Reinforcement Learning и Anthropic Institute (Economics & Policy): rolling на когорту с ожидаемым стартом в январе 2027, подача внизу Greenhouse, не через bit.ly. https://job-boards.greenhouse.io/anthropic/jobs/id_8effa947 и https://job-boards.greenhouse.io/anthropic/jobs/id_cfa88352

Уже закрыто и не путать с «ещё можно». OpenAI Residency 2026. OpenAI Safety Fellowship, приём до 3 мая, программа 14 сентября 2026 – 5 февраля 2027 уже идёт. MATS Winter 2027 fellowship, stage 1 закрыт 6 сентября. Astra, Visiting Fellowship Fall 2026, ERA Winter 2027, GovAI UK и DC Winter 2027, IAPS Spring 2027, PIBBSS Winter 2026–2027, LASR текущий набор, SPAR mentee Fall 2026.

Заявки в этом прогоне не подавались и никому не писалось.

B. Матрица покрытия

Дата проверки всех строк: 2026-10-18. «Не открыто» значит отрицательный вердикт не ставлю.

| Вендор | Тип, который искали | Статус | Что открыто |
| --- | --- | --- | --- |
| Anthropic | Fellows safety/security, ML/RL, Institute, STEM, Conceptual | safety: open, cutoff October 18 без года и пояса; ML и Institute: open rolling Jan 2027; STEM и Conceptual: open до 28 Oct 2026 | пять Greenhouse JD ниже |
| OpenAI | Residency; Safety Fellowship | Residency 2026 closed; Safety Fellowship applications closed, когорта in progress | https://openai.com/residency/ https://alignment.openai.com/safety-fellowship/ |
| Google DeepMind / Google Research | Student Researcher; отдельный non-student residency | student-only, цикл 2026–2027 указан; non-student residency на открытой странице нет | https://deepmind.google/student-researcher-program/ |
| Microsoft Research | fellowship / residency vs обычный найм | именованной fellowship-страницы не открыто; открыты вакансии Researcher и Postdoctoral Researcher (контракт «Resident» 2 года) — это найм, не fellows-программа | https://apply.careers.microsoft.com/careers/job/1970393556982899 https://apply.careers.microsoft.com/careers/job/1970393556991730 |
| Meta / FAIR | AI Mentorship; residency | Mentorship: не принимают, следующий набор ожидают в ноябре 2026, только PhD партнёрских вузов. Отдельный residency не найден на этой странице | https://www.metacareers.com/careerprograms/research?tab=AI+Mentorship |
| xAI | fellowship / residency | на careers и open roles именованной программы нет. Есть обычные роли, включая Safety, Interpretability, Model Evaluation, и Software Engineer Tutor | https://x.ai/careers/ https://x.ai/careers/open-roles |
| NVIDIA | Graduate Fellowship | open до 30 Oct 2026, только PhD | https://research.nvidia.com/graduate-fellowships |
| Amazon / AWS | fellowship / residency | официальная страница в этом прогоне не открыта | не проверено |
| Apple | scholars / residency | официальная страница не открыта | не проверено |
| Mistral | fellowship / residency / internship | на https://mistral.ai/careers именованной программы в извлечённом тексте нет, только обычный найм | https://mistral.ai/careers |
| Cohere | Scholars | страница извлечена поиском: Status Closed, открытия ждут осенью 2026. Прямой рендер вернул в основном навигацию, вторым полным рендером статус не перечитан | https://cohere.com/research/scholars-program |
| Hugging Face | residency | в индексе лежит анонс 2022 года с дедлайном 3 апреля 2022. Живой набор 2026 на официальной странице не открыт | https://huggingface.co/buckets/hf-doc-build/blog/tree/ai-residency.md |
| AI21 | fellowship | не открыто | не проверено |
| Aleph Alpha | fellowship | не открыто | не проверено |
| IBM | fellowship | не открыто | не проверено |
| Databricks / Mosaic | fellowship | не открыто | не проверено |
| Snowflake | fellowship | не открыто | не проверено |
| Together | research intern | агрегатор описывает Summer 2027 intern только для MS/PhD. Официальный ATS не открыт | не официальный источник: https://zerogtalent.com/ai-jobs/together-ai/research-intern-frontier-speculative-decoding-summer-2027-5267198007 |
| Fireworks | fellowship | официальная страница не открыта | не проверено |
| Cerebras | fellowship vs job | агрегатор показывает обычную вакансию Applied ML Research Scientist, не fellowship. Официальный ATS не открыт | не проверено как программа |
| Groq | fellowship | официальная страница не открыта | не проверено |
| Perplexity | fellowship | не открыто | не проверено |
| Cursor / Anysphere | fellowship | не открыто | не проверено |
| Cognition | fellowship | не открыто | не проверено |
| Replit | fellowship | не открыто | не проверено |
| Stability | fellowship | не открыто | не проверено |
| Runway | fellowship | не открыто | не проверено |
| Character.AI | fellowship | не открыто | не проверено |
| Inflection | fellowship | не открыто | не проверено |
| Liquid AI | fellowship | не открыто | не проверено |
| Poolside | fellowship | не открыто | не проверено |
| Magic | fellowship | не открыто | не проверено |
| DeepSeek | jobs vs fellowship | главная ведёт Join Us на https://talent.deepseek.com/ . Сам портал вакансий не открыт. Fellowship на главной не назван | https://www.deepseek.com/ |
| Alibaba/Qwen, Z.ai/Zhipu, Moonshot/Kimi, MiniMax, Baidu, Tencent, ByteDance, Huawei, Naver, LG, Samsung | fellowship | официальные страницы в этом прогоне не открыты | не проверено, отрицательный вердикт запрещён |

Не-вендоры, открытые отдельно. Это не трудоустройство вендора.

| Организация | Статус 18.10.2026 | URL |
| --- | --- | --- |
| MATS fellowship Winter 2027 | stage 1 closed 6 Sep; программа с 19 Jan 2027 | https://www.matsprogram.org/apply |
| MATS Residency Winter 2027 | open до 31 Oct 2026 AoE | https://www.matsprogram.org/residency |
| Constellation Astra | приём закрыт, только EOI. Баннер «close on May 3rd» на главной расходится со страницей программы | https://constellation.org/programs/astra https://constellation.org/ |
| Constellation Visiting | Fall 2026 closed, когорты поквартально, EOI | https://constellation.org/programs/visiting-fellowship |
| Generator (Constellation и Kairos) | open до 1 Nov 2026 AoE | https://generatorresidency.org/ |
| SPAR / Kairos | mentee Fall 2026 closed 18 Aug 2026 AoE; Spring 2027 «around December» | https://sparai.org/ |
| FAR.AI | на careers нет открытой заявки fellowship; секции Research, Events, Programs без дат | https://www.far.ai/careers |
| Redwood | своей fellowship нет; отсылают в MATS и Astra. Empirical Researcher — обычная роль | https://www.redwoodresearch.org/careers |
| METR | обычные роли и General EOI, не fellowship | https://metr.org/careers |
| Apollo | «We don’t currently offer internships.» Вакансии есть, визу спонсируют | https://www.apolloresearch.ai/careers |
| ERA | Winter 2027 closed | https://erafellowship.org/fellowship |
| LASR | следующий когортный слот June–September 2027, заявки не открыты, есть express interest | https://www.lasrlabs.org/ |
| AI Safety Camp | лиды: дедлайн 18 Oct; участники: 7–29 Nov | https://www.aisafety.camp/ |
| IAPS | Spring 2027 closed | https://www.iaps.ai/fellowship |
| GovAI | UK и DC Winter 2027 closed | https://www.governance.ai/post/winter-fellowship-2027-applied-track https://www.governance.ai/post/dc-winter-fellowship-2027 |
| CAIS AI and Society | напечатанный дедлайн 24 Mar, 11:59 PM PDT, даты 1 Jun–21 Aug 2026. На дату проверки это прошло. Страница поиска всё ещё показывала Apply. Следующий цикл не указан | https://safe.ai/fellowship |
| PIBBSS / Principles of Intelligence | Winter 2026–2027 closed, дедлайн был 20 Jul 2026 | https://princint.ai/programs/fellowship/ |
| Iliad | Dec 2026 fellowship до 19 Oct 2026; Jan 2027 fellowship и Intensive до 16 Nov 2026 | https://www.iliad.ac/ |
| Impact First Residency | страница говорит, что программа для students в London, apply by October 18. Для заявленного нестудента не очередь | https://www.impactfirst.org.uk/residency |

C. Карточки программ

Общие пометки. application_state для всех: not_started. Prepared, submitted и confirmed здесь не используются. Work authorization кандидата неизвестен, поэтому «eligible» ниже значит «профиль не студенческий и формальный студенческий барьер не сработал», а не «виза точно есть». Оценки fit не являются оценкой шанса.

C1. anthropic|fellows-safety-security|2027-01

Тип: paid research fellowship, партнёрский набор Constellation, не прямой найм Anthropic. Статус: open на живой JD. Проверено: 2026-10-18. Дедлайн: текст «by October 18», год и пояс на JD и на блоге не напечатаны. Rolling: да, «review applications on a rolling basis», и при этом для январской когорты названа дата. Когорта: «January cohort», день старта и конца на этом JD не напечатаны. Не переносить даты STEM. Длительность: 4 месяца, full-time, 40 часов в неделю, возможное продление. Локация: workspace Berkeley или London; remote внутри UK, US, Canada. Оплата: 3850 USD или 2310 GBP или 4300 CAD в неделю плюс benefits «vary by country»; compute около 15 тыс. USD в месяц. Навыки: Python обязателен; CS, math или physics названы как сильный фон; PhD, прошлый ML и статьи не требуются по блогу. Студент: запрета нет. Виза: не спонсируют. Нужно уже иметь full-time work authorization в UK, US или Canada и быть в этой стране. Референсы: initial application и reference check. Оценки: technical assessments, interviews, research discussion. AI в заявке: общая политика https://www.anthropic.com/candidate-ai-guidance , обновлена 10 Jul 2025: первый черновик сам, Claude можно для правки; take-home без Claude, если прямо не разрешили; живое интервью без AI. Cooldown: не напечатан. Fit: сильный по Python, security, evals, agents, open source. Неизвестно: work authorization, пояс дедлайна, точные даты января, примет ли нативная кнопка Greenhouse заявку. JD прямо говорит, что интервью ведёт Constellation и что кнопка ведёт в их портал. На той же странице Greenhouse всё ещё рисует собственную форму. Это два входа одного объявления, не две вакансии. Оффер full-time не гарантирован. JD: 25–50% прошлых fellows получили full-time offer. Блог: over 35% прошлых fellows затем вышли на full-time AI safety в Anthropic. Цифры разные, обе первичные, знаменатель не сверен.

Источник: https://job-boards.greenhouse.io/anthropic/jobs/id_2e26dffe  
Заявка по инструкции: https://bit.ly/afpsafety  
Блог: https://alignment.anthropic.com/2025/anthropic-fellows-program-2026/

C2. anthropic|fellows-ml-systems-rl|2027-01

Тип: тот же Fellows, два потока внутри одного JD: ML Systems & Performance и Reinforcement Learning. Статус: open, rolling, «next cohort expected to start in January 2027». Отдельной даты October 18 на этом JD нет. Если январь не подходит, можно написать об этом. Длительность 4 месяца. Стипендия та же недельная тройка валют. Compute около 15 тыс. USD в месяц. Локация: shared workspace «in SF»; remote в UK, US, Canada. Виза нет. Python обязателен. Референсы «may ask later». Форма внизу Greenhouse, не bit.ly. AI-политика та же ссылка. Fit: сильный для C++/Python и systems. Неизвестно: пояс и момент, когда rolling закроют; точный старт.

https://job-boards.greenhouse.io/anthropic/jobs/id_8effa947

C3. anthropic|fellows-institute-econ-policy|2027-01

Тип: Economics & Policy внутри Fellows. Статус: open, rolling, ожидаемый старт January 2027, подача внизу этой страницы. Стипендия та же. Compute назван «substantial», цифра 15 тыс. на этом JD не повторена. Python обязателен. «Strong track record of empirical research» в блоке good fit. Интерес к экономике или политике желателен, прошлый опыт не обязателен. Просят writing sample, предпочтительно job-market paper. Виза нет, US/UK/Canada. Fit: слабее safety-трека, если нет эмпирических экономических или policy-работ. Не вычёркиваю: JD сам говорит, что опыт не обязателен. Неизвестно: тот же rolling cutoff.

https://job-boards.greenhouse.io/anthropic/jobs/id_cfa88352

C4. anthropic|stem-fellow|2027-01-12

Тип: фиксированный контракт через employer of record, не прямой найм. Статус: open until October 28, 2026. Пояс нет. Офферы планируют к November 20. Даты программы: January 12 – May 8, 2027. Оплата 100000–167000 USD за четыре месяца. Одна неделя ориентации в San Francisco обязательна. Default SF, remote внутри US «in certain circumstances». Виза нет, нужна existing US work authorization. Минимум: PhD в STEM и несколько лет опыта, пример post-doc или faculty, плюс ежедневный Claude и Claude Code. Прошлый ML полезен, не обязателен. Референсы: имя, email, как знакомы. Take-home типичен на поздних стадиях. Fit: формальный PhD-барьер. В профиле кандидата PhD не заявлен. В очередь «точно подходит» не ставлю.

https://job-boards.greenhouse.io/anthropic/jobs/id_b016af84

C5. anthropic|conceptual-reasoning-fellow|2027-01-12

Те же даты, деньги, виза, ориентация и дедлайн 28 Oct 2026, что у STEM. Поля: philosophy, cognitive science, economics, policy, law. Минимум: PhD или equivalent research experience. Fit: equivalent experience формально открыт, но профиль кандидата это не подтверждает. Неизвестность, не отказ.

https://job-boards.greenhouse.io/anthropic/jobs/id_b8244b3d

C6. openai|residency|2026

Тип: шестимесячный найм, full-time employee, не internship. Статус: «Applications for the 2026 Residency are now closed.» Старт, когда программа открыта, rolling в течение года. Локация: San Francisco HQ, минимум 3 дня в офисе, remote и satellite offices запрещены. Relocation есть. Зарплата 18333 USD в месяц плюс benefits. Визу и sponsorship дают по обстоятельствам. Нельзя быть enrolled в школе. Ментор и проект вместе с командой. Часть резидентов получает full-time offer сразу после шести месяцев. Это не гарантия. Куда подавать сейчас: живой кнопки нет, страница отсылает к careers. Fit при будущем открытии: сильный для перехода инженера в research. Сейчас подавать некуда.

https://openai.com/residency/

C7. openai|safety-fellowship|2026-09

Тип: внешняя исследовательская стипендия с менторами OpenAI. Не внутренний доступ и не найм. Партнёр по заявкам: Constellation, почта [EMAIL]. Статус приёма: closed. Английская страница: «will close May 3» без года. Даты программы напечатаны: 14 Sep 2026 – 5 Feb 2027. Китайская страница OpenAI прямо пишет дедлайн 2026年5月3日: https://openai.com/zh-Hans-CN/index/introducing-openai-safety-fellowship/ . Пояс дедлайна нет. Уведомление успешных было обещано к July 25. Workspace в Berkeley у Constellation или remote. Стипендия и benefits описаны как «see the application form». Форму https://bit.ly/c-openai-safety-fellowship в этом прогоне не открывал, сумму не знаю. Референсы обязательны. Темы: safety evaluation, robustness, scalable mitigations, agentic oversight, misuse. Выход: paper, benchmark или dataset. Fit был бы сильный. Сейчас окно закрыто, когорта идёт.

https://alignment.openai.com/safety-fellowship/

C8. mats|fellowship|2027-winter

Тип: 12 недель, in-person Berkeley и London, remote или part-time только если позволят обстоятельства и ментор. Статус: «Winter 2027 applications are closed.» Stage 1 закрыт September 6th. Офферы early to mid-November. Старт January 19, 2027, FAQ: до April 10, 40 часов в неделю. Стипендия 1600 USD в неделю, 19200 USD за 12 недель, плюс 24000 USD compute на карточке apply, жильё, еда, дорога, J-1 если нужно. Два референса, контакт только если прошли дальше. Empirical: assessments и coding 3–5 часов. Повторная подача разрешена и не штрафуется. Это не текущая заявка. Следующее окно на странице не датировано.

https://www.matsprogram.org/apply https://matsprogram.org/faq

C9. mats|residency|2027-winter

Тип: paid residency, 6–24 месяца, три трека Bridge, Anchor, Incubation. Статус: open. Окно 25 August 2026 – 31 October 2026 AoE. Форма: https://forms.matsprogram.org/residency-w27 . До 30 резидентов в год, три окна, старт rolling. Оплата 155000–285000 USD gross в год плюс benefits. Compute без заранее заданного потолка. Офисы London, Berkeley, Washington DC. Hybrid, минимум треть срока очно. Full-time. Part-time только sabbatical, case by case. Виза где нужно, relocation до 25000 USD, включая партнёра и детей. Bridge прямо для опытных профессионалов и людей из cybersecurity. Оценивают качество работы, не титул CV. Fit: самый прямой платный вход под заявленный профиль среди не-вендоров. Неизвестно: сколько референсов и есть ли work-test на форме, страницу формы не раскрывал.

https://www.matsprogram.org/residency https://www.matsprogram.org/residency/tracks

C10. constellation|astra|eoi

Тип: fully funded in-person fellowship, Berkeley, потоки empirical и strategy/governance. Страница программы: 5 месяцев, стипендия 8400 USD в месяц, empirical compute около 15 тыс. USD в месяц, визовая помощь. Статус приёма: «January 2026 cohort are now officially closed», дальше только EOI. Главная всё ещё пишет «Applications close on May 3rd». Это не живой дедлайн октября 2026. Empirical-страница одновременно пишет «September 2026 – February 2027» и «register interest when our next cohort launches». Расхождение не сглаживаю: подача сейчас не открыта. Менторы с пометкой звёздочки участвуют через fellowship своей организации вместе с Constellation. Это не оффер Anthropic или OpenAI.

https://constellation.org/programs/astra  
EOI: https://bit.ly/c-astra-eoi

C11. constellation|visiting|quarterly

3–6 месяцев, Berkeley, не remote. Жильё, дорога, обед и ужин. Стипендии нет. Если деньги барьер, можно написать, могут искать paid residency. Fall 2026 closed. До 6 месяцев внутри любого двухлетнего окна. Нужна уже full-time работа по AI safety. Для человека без такой текущей роли это слабый fit. EOI: https://bit.ly/c-vf-eoi

https://constellation.org/programs/visiting-fellowship

C12. generator|winter|2027

Тип: трёхмесячная residency для generalists, не research track. Организаторы Constellation и Kairos. Статус: open. 18 Jan – 9 Apr 2027, Berkeley, продление избранным до early July. Стипендия 8500 USD в месяц, проектный бюджет, еда в рабочие дни, офис Constellation. Дедлайн: end of day 1 Nov 2026 AoE. Международным настоятельно советуют подать к 26 Oct 2026 из-за визы. Это не напечатано как закрытие окна. Треки Self-Directed и Embedded. Инженерия названа среди подходящих навыков. Заявка: https://forms.kairos-project.org/generator/apply . Fit: сильный как вход в экосистему, слабый как замена исследовательского fellowship. Неизвестно: спонсорство визы да или только «время на обработку».

https://generatorresidency.org/

C13. spar|mentee|2026-fall и 2027-spring

Part-time remote, 5–40 часов в неделю, 3 месяца. Fall 2026: 14 Sep – 14 Dec 2026, заявки закрыты. Дедлайн был Tuesday, August 18, 2026, end of day AoE. Spring 2027 откроется around December. Студенты и профессионалы. Прошлый research не обязателен. Компенсация на главной в раскрытых FAQ не прочиталась, сумму не утверждаю. AI: форма запрещает AI assistance в ответах. Источник запрета: https://sparai.org/apply/advisor . Fit весной: хороший для evals и security, если появятся такие проекты. Сейчас не подавать.

https://sparai.org/

C14. lasr|cohort|2027-summer

13 недель, in-person London, London Initiative for Safe AI. Следующий набор June–September 2027, заявки не открыты. Express interest: https://airtable.com/appNVUD1bMd5wftwd/shrJsQ0FqGUotGQPM . Текущее описание денег: 15000 GBP на жизнь плюс еда, офис, дорога. Три раза в год. Нужны ML engineering и количественные навыки. Опытный инженер назван типичным сильным участником. Fit при открытии: сильный. Дедлайн будущего окна неизвестен.

https://www.lasrlabs.org/

C15. aisc|virtual|2027

3 месяца online, 11 Jan – 18 Apr 2027, открытие 9–10 Jan. Лиды: дедлайн October 18 (Sunday), доработка proposal к November 1. Участники команд: 7–29 Nov. Стипендий нет, кроме отдельных matched donations. Research-лиду нужен предыдущий research experience. Минимум 10 часов в неделю. Fit лида: неизвестен, исследовательский стаж в профиле не заявлен. Fit участника: окно ещё не открыто, неоплачиваемое. Заявка лида: https://airtable.com/app48Boo180yWEifN/shrM1Brxftjk8bNlz

https://www.aisafety.camp/

C16. iliad|fellowship|2026-12 и 2027-01

Три месяца, in-person, London или Bay Area. 6000 USD в месяц на travel and housing. Dec: 1 Dec 2026 – 5 Mar 2027, заявки до 19 Oct 2026, пояс нет. Jan: 4 Jan – 26 Mar 2027, заявки до 16 Nov 2026. Intensive Jan: 4–29 Jan 2027, тот же дедлайн 16 Nov. Аудитория: сильная математика, обычно PhD, postdoc или equivalent. Fit: неизвестен, не выдумываю математический уровень. Заявка: https://www.iliad.ac/apply?direct

https://www.iliad.ac/fellowship

C17. era|winter|2027

10 недель, Cambridge, 18 Jan – 26 Mar 2027. Стипендия 10000 GBP. Приём Winter 2027 closed. Возраст 18+, формального диплома страница не требует. Следующее окно не датировано.

https://erafellowship.org/fellowship

C18. govai|uk-winter|2027 и govai|dc-winter|2027

Оба приёма closed. UK: 18 Jan – 9 Apr 2027, London, зарплата 12000 GBP, обед, стол, full-time, спонсируют 3-month temporary work visa. DC: 18 Jan – 9 Apr 2027, stipend 21000 USD плюс дорога, in-person. Это governance, не evals. Дедлайн DC в старом посте X был 12 Jul 2026, 11:59 PM ET. На дату проверки страницы уже говорят closed.

https://www.governance.ai/post/winter-fellowship-2027-applied-track  
https://www.governance.ai/post/dc-winter-fellowship-2027

C19. iaps|spring|2027

Closed. 22 Feb – 14 May 2027. DC, London или remote, но все обязаны быть в DC 22 Feb – 5 Mar 2027. Senior 24000 USD, Fellow 18000 USD, плюс 3000 USD на DC или London track. Governance, не лабораторный research.

https://www.iaps.ai/fellowship

C20. pibbss|winter|2026-2027

Closed. Дедлайн был 20 Jul 2026. Программа November 2026 – February 2027, около 3 месяцев, около 20 fellows, 3000 USD в месяц. Междисциплинарный вход в AI safety. Сайт pibbss.ai открылся как https://princint.ai/ .

https://princint.ai/programs/fellowship/

C21. nvidia|graduate-fellowship|2027-2028

Open. Заявки с 30 Sep 2026, дедлайн 30 Oct 2026 включая письма, победители 15 Jan 2027. До 60000 USD через университет. Обязателен PhD после первого года, full-time зачисление весь award year, летняя очная стажировка 2027. Локации стажировки: US, Canada, Germany, Sweden, Finland, Switzerland, Israel, Taiwan, Singapore. Для нестудента не eligible.

https://research.nvidia.com/graduate-fellowships

C22. deepmind|student-researcher|2026-2027

Только enrolled Bachelor, Master или PhD. 12–24 недели, 5 дней, очно в офисе Google. Заявки через обычные вакансии Google, не отдельный non-student трек. Для этого кандидата не eligible.

https://deepmind.google/student-researcher-program/

C23. cohere|scholars|next

Извлечение https://cohere.com/research/scholars-program : Status Closed. «Applications are expected to open in Fall 2026.» Сегодня уже 18 Oct 2026, а статус в извлечении всё ещё Closed. Точную дату не выдумываю. Исторически: remote-first, full-time, paid, около 8 месяцев с января, публикации не обязательны. Сумму оплаты страница не дала.

C24. meta|ai-mentorship|next

Не принимают. Следующее открытие ожидают в November 2026, закрытие исторически в January. Только PhD студентов UW, CMU, Berkeley, NYU, Mila. Это не residency для нестудента.

https://www.metacareers.com/careerprograms/research?tab=AI+Mentorship

C25. redwood|jobs и metr|jobs и apollo|jobs и far|careers

Это обычный найм или пустая карьерная витрина, не fellowship. Redwood явно отправляет fellowship-интерес в MATS и Astra. Apollo: интернатур нет, повторная подача на роли через 6 месяцев. METR: work test и work trial, виза на технические роли. FAR: отдельной открытой заявки на странице careers нет.

D. Очередь живых заявок

Только то, что на 18.10.2026 открыто и не отсечено студенческим или PhD-барьером. Work authorization везде неизвестен. Ничего не подано.

| Приоритет | Ключ | Почему сейчас | Куда | Доказательство |
| --- | --- | --- | --- | --- |
| 1, сегодня | anthropic\|fellows-safety-security\|2027-01 | Python, security, evals, agents, OSS. Не студент. Виза неизвестна и может быть жёстким стопом | https://bit.ly/afpsafety | https://job-boards.greenhouse.io/anthropic/jobs/id_2e26dffe |
| 2, сегодня не дедлайн, rolling | anthropic\|fellows-ml-systems-rl\|2027-01 | systems и Python. Тот же визовый стоп | низ Greenhouse-формы | https://job-boards.greenhouse.io/anthropic/jobs/id_8effa947 |
| 3, до 31 Oct 2026 AoE | mats\|residency\|2027-winter | опытный нестудент, Bridge, безопасность и надёжность агентов | https://forms.matsprogram.org/residency-w27 | https://www.matsprogram.org/residency |
| 4, до 26 Oct желательно, жёстко 1 Nov 2026 AoE | generator\|winter\|2027 | оплачиваемая residency, инженерия названа. Это generalist, не research paper track | https://forms.kairos-project.org/generator/apply | https://generatorresidency.org/ |
| 5, rolling | anthropic\|fellows-institute-econ-policy\|2027-01 | Python обязателен, эмпирический track record желателен. Слабее fit | низ формы | https://job-boards.greenhouse.io/anthropic/jobs/id_cfa88352 |
| 6, 19 Oct 2026, fit неизвестен | iliad\|fellowship\|2026-12 | окно живое, математический барьер не измерен | https://www.iliad.ac/apply?direct | https://www.iliad.ac/ |

Рядом, не в оплаченной очереди. AISC project lead до конца 18 Oct, если есть свой research proposal и прошлый research. Участником команд можно будет с 7 Nov, без стипендии. Impact First сегодня закрывается и на странице ограничен students.

Не ставить в очередь. STEM Fellow: PhD не подтверждён. NVIDIA и DeepMind Student Researcher: нужен текущий студент. OpenAI Residency и OpenAI Safety Fellowship: приём закрыт. MATS fellowship Winter 2027: stage 1 закрыт.

E. Закрытые программы и что стеречь

| Ключ | Сигнал следующего окна | Куда смотреть |
| --- | --- | --- |
| openai\|residency | careers и соцсети, старт rolling, когда снова откроют | https://openai.com/residency/ https://openai.com/careers/search/ |
| openai\|safety-fellowship | второй набор не обещан. Письмо [EMAIL] указано для вопросов, не как канал, куда я писал | https://alignment.openai.com/safety-fellowship/ |
| mats\|fellowship | три когорты в год уже заявлены историей Autumn 2026. Следующий stage 1 не датирован. Кнопка notify на apply | https://www.matsprogram.org/apply |
| constellation\|astra | EOI. Игнорировать баннер May 3, пока программа снова не напечатает дату | https://bit.ly/c-astra-eoi |
| constellation\|visiting | следующий квартал после Fall 2026 | https://bit.ly/c-vf-eoi |
| cohere\|scholars | страница уже обещала Fall 2026 и одновременно стоит Closed. Проверять ту же URL, не агрегаторы | https://cohere.com/research/scholars-program |
| meta\|ai-mentorship | November 2026, но только PhD партнёрских вузов | https://www.metacareers.com/careerprograms/research?tab=AI+Mentorship |
| spar\|mentee | around December для Spring 2027. Запрет AI на текстах ответов | https://sparai.org/ |
| lasr | заявки на June–September 2027 | https://www.lasrlabs.org/ |
| era, govai, iaps, pibbss | mailing list или EOI, даты не напечатаны | страницы из раздела C |
| cais\|ai-society | летний 2026 дедлайн прошёл. Ждать новой страницы с новым годом, не нажимать старый Apply как будто он живой | https://safe.ai/fellowship |
| anthropic fellows | safety может закрыться в день проверки. ML и Institute rolling без даты. Следующая когорта после января на этих JD не названа | пять Greenhouse URL |

F. Реестр и запросы для рутин

Ключ: vendor_or_org + program_slug + cohort_id. Два ATS URL одной когорты склеивать. Greenhouse job id и bit.ly одного Anthropic safety-набора — одна запись, поле application_urls массив. Статус программы и статус заявки — разные поля. not_started, prepared, submitted, confirmed не синонимы.

Схема одной записи:

program_key, org, program_name, track, cohort_id, program_type, status, date_checked, source_url, application_urls, deadline_date, deadline_year_explicit, timezone, rolling, cohort_start, cohort_end, duration, location, remote, pay_amount, pay_currency, pay_period, compute, degree_restriction, student_restriction, work_auth, visa_sponsorship, references, assessments, ai_use_rule, reapply_rule, fit, unknowns, application_state, evidence_quote

Еженедельный поиск, официальные домены первыми:

"Fellows Program" OR residency OR fellowship site:anthropic.com OR site:job-boards.greenhouse.io/anthropic  
site:openai.com/residency OR site:alignment.openai.com fellowship OR residency  
site:deepmind.google student researcher OR visiting researcher OR fellowship  
site:metacareers.com "AI Mentorship" OR residency  
site:x.ai/careers fellowship OR residency OR "member of technical staff" safety  
site:research.nvidia.com/graduate-fellowships  
site:cohere.com/research/scholars-program  
site:matsprogram.org/apply OR site:matsprogram.org/residency deadline OR closed OR open  
site:constellation.org/programs Astra OR "Visiting Fellowship"  
site:generatorresidency.org "Apply by"  
site:sparai.org "applications"  
site:lasrlabs.org "applications" OR "express interest"  
site:erafellowship.org "applications"  
site:governance.ai fellowship Winter OR Summer  
site:iaps.ai/fellowship  
site:princint.ai/programs/fellowship  
site:www.iliad.ac Applications close  
site:www.aisafety.camp "Application deadline"  
site:safe.ai/fellowship  
site:mistral.ai/careers fellowship OR residency OR intern  
site:talent.deepseek.com  
fellowship OR residency OR 学者 OR 实习 site:qwenlm.github.io OR site:zhipuai.cn OR site:moonshot.cn OR site:minimaxi.com OR site:research.baidu.com

Ежедневная дедупликация заявок:

Смотреть только status=open и deadline в ближайшие 14 дней или rolling=true. Группировать по program_key. Если application_state уже submitted или confirmed, не создавать вторую задачу на другой URL того же ключа. bit.ly и Greenhouse id id_2e26dffe — один ключ. Не повышать not_started до prepared без сохранённого черновика и не повышать prepared до submitted без письма приёма или номера заявки. Safety Anthropic проверять каждый день, пока на JD есть «now open» или пока дата October 18 не сменится на закрыто. MATS Residency проверять до 31 Oct 2026 12:00 UTC−12. Generator: международный риск с 26 Oct, жёсткая проверка 1 Nov AoE.

Предел этого прогона. Amazon, Apple, AI21, Aleph Alpha, IBM, Databricks, Snowflake, Fireworks, Groq, Perplexity, Cursor, Cognition, Replit, Stability, Runway, Character.AI, Inflection, Liquid, Poolside, Magic и китайские, корейские и японские лаборатории кроме главной DeepSeek не открыты. Для них нет вердикта «программы нет». Together и Cerebras увидены только через агрегаторы. Сумма стипендии OpenAI Safety Fellowship не прочитана, форма не открыта. Пояс дедлайна Anthropic safety, STEM, Conceptual и Iliad December не напечатан. Заявки не отправлялись.

🧒 Простыми словами

Сегодня ещё можно успеть в исследовательскую программу Anthropic по безопасности: платят каждую неделю, но визу сами не делают, и час закрытия на странице не написан. До конца октября открыт длинный оплачиваемый MATS Residency для опытных людей. Две соседние двери Anthropic, про системы и про экономику, без сегодняшней даты, заявка прямо на их странице. Стипендия NVIDIA и студенческая программа Google для этого профиля не подходят: там надо быть студентом. Много других лабораторий я в этом заходе просто не открыл, поэтому не говорю, что у них ничего нет.

---

**Claude:**

{"lang":"ru","topic":"Оплачиваемые fellowship/residency программы AI-лабораторий: живые окна на 18.10.2026","one_line":"Какие оплачиваемые fellowship, residency и входные исследовательские программы AI-вендоров и safety-организаций открыты на 18.10.2026, с дедлайнами, условиями и пригодностью для нестудента.","key_findings":["Anthropic Fellows (AI Safety & Security, январская когорта): дедлайн «by October 18» без года и пояса, заявка через портал Constellation (bit.ly/afpsafety → Airtable), а не нативный Greenhouse. 3850 USD / 2310 GBP / 4300 CAD в неделю, 4 месяца, compute ~15 тыс. USD в месяц. Нужно уже иметь право работы и находиться в US/UK/Canada, визу не спонсируют, Python обязателен, студенческий статус не требуется.","Anthropic ML Systems & RL и Institute (Economics & Policy): rolling на когорту с ожидаемым стартом в январе 2027, форма внизу Greenhouse JD. Те же деньги и визовые условия. Anthropic STEM Fellow и Conceptual Reasoning Fellow: до 28 октября 2026, 12 янв – 8 мая 2027, 100–167 тыс. USD за 4 месяца, только US work authorization, нужен PhD или эквивалент. Для кандидата без заявленного PhD в очередь «точно подходит» не ставятся.","MATS Residency Winter 2027 открыт до 31 октября 2026 AoE: 6–24 месяца, 155–285 тыс. USD в год gross, London/Berkeley/DC, визовая поддержка, relocation до 25 тыс. USD, до 30 резидентов в год. Трек Bridge прямо рассчитан на опытных профессионалов и людей из cybersecurity, оценивают качество работы, а не титул. Самый прямой платный вход для нестудента.","Generator Residency (Constellation + Kairos): 18 янв – 9 апр 2027, Berkeley, 8500 USD в месяц, жёсткий дедлайн 1 ноября 2026 AoE, международным рекомендуют подать к 26 октября из-за визы. Это generalist-программа, не исследовательский трек.","Iliad Fellowship: декабрьская когорта подаётся до 19 октября 2026, январская и Intensive до 16 ноября; 6000 USD в месяц на дорогу и жильё (не зарплата), математический уклон, обычно PhD или эквивалент. AI Safety Camp: лиды до 18 октября, участники 7–29 ноября, стипендий нет.","Закрыты и не ставятся в очередь: OpenAI Residency 2026, OpenAI Safety Fellowship (приём до 3 мая, программа 14 сен 2026 – 5 фев 2027), MATS fellowship Winter 2027 (stage 1 закрыт 6 сен), Astra (только EOI), Visiting Fellowship Fall 2026, ERA, GovAI, IAPS, PIBBSS, LASR (следующий набор июнь–сент 2027), SPAR Fall 2026 (Spring 2027 около декабря), Cohere Scholars (Closed, ожидали осень 2026), Meta AI Mentorship (ноябрь 2026, только PhD партнёрских вузов).","Студенческие/PhD-программы не подходят нестуденту: NVIDIA Graduate Fellowship (до 60 000 USD, дедлайн 30 окт, нужен действующий PhD), Google DeepMind Student Researcher, Impact First Residency (students, London).","Покрытие неполное: у Microsoft Research, xAI, Mistral, DeepSeek, Redwood, METR, Apollo, FAR.AI именованной fellowship не найдено (обычный найм). Amazon, Apple, AI21, Aleph Alpha, IBM, Databricks, Snowflake, Fireworks, Groq, Perplexity, Cursor, Cognition, Replit, Stability, Runway и китайские/корейские лаборатории не открыты, отрицательный вердикт по ним запрещён. Отчёт собран одним вендором (grok), заявки не подавались.","Предложена схема реестра: ключ vendor_org + program_slug + cohort_id, Greenhouse id и bit.ly одной когорты склеиваются в одну запись; статусы программы и заявки (not_started/prepared/submitted/confirmed) разные поля; ежедневная дедупликация смотрит open с дедлайном в 14 дней или rolling."],"recommendations":["Приоритет очереди: 1) Anthropic Fellows Safety/Security сегодня через bit.ly/afpsafety (риск: work authorization в US/UK/CA неизвестен и может быть стопом); 2) Anthropic ML Systems & RL (rolling); 3) MATS Residency до 31 окт AoE; 4) Generator до 26 окт желательно, жёстко 1 ноя AoE; 5) Anthropic Institute Econ/Policy (слабее fit); 6) Iliad Dec до 19 окт при неизвестном математическом барьере.","Не ставить в очередь STEM/Conceptual Fellow без подтверждённого PhD, NVIDIA, DeepMind Student Researcher, закрытые OpenAI и MATS fellowship.","Ключ Anthropic safety проверять ежедневно, пока на JD есть «now open» или дата October 18 не сменится на закрыто; MATS Residency проверять до 31 окт 12:00 UTC−12; Generator с 26 окт и жёстко 1 ноя AoE.","Не превращать «October 18» без года и пояса в «23:59 PT»; год и пояс фиксировать только если они напечатаны на источнике.","Еженедельный поиск вести по официальным доменам первыми (список site:-запросов из отчёта), закрытые программы стеречь по тем же URL, а не по агрегаторам.","Для непроверенных вендоров ставить «не проверено», а не «программы нет»; довыяснить их отдельным прогоном и вторым вендором."],"entities":{"people":[],"companies":["Anthropic","OpenAI","Google DeepMind","Microsoft Research","Meta","xAI","NVIDIA","Mistral","Cohere","DeepSeek","Constellation","Kairos","MATS","Redwood Research","METR","Apollo Research","FAR.AI","GovAI","IAPS","PIBBSS","Iliad","LASR","ERA","SPAR","CAIS","AI Safety Camp","Impact First","Hugging Face","Together","Cerebras"],"products_tools":["Anthropic Fellows Program","MATS Residency","Generator Residency","Astra Fellowship","Visiting Fellowship","OpenAI Residency","OpenAI Safety Fellowship","NVIDIA Graduate Fellowship","Iliad Fellowship","AI Safety Camp","Greenhouse","Airtable","Meta AI Mentorship","Cohere Scholars Program","Google DeepMind Student Researcher Program"]},"open_questions":["Есть ли у кандидата право работы в US/UK/Canada (стоп для Anthropic Fellows) и US work authorization (для STEM/Conceptual)?","Пояс и точное время дедлайна Anthropic safety (год и пояс не напечатаны), точные даты январской когорты, принимает ли нативная кнопка Greenhouse заявку.","Расхождение цифр по конверсии в full-time: JD пишет 25–50% прошлых fellows, блог over 35%; знаменатель не сверен.","Сколько референсов и есть ли work-test в форме MATS Residency; спонсируется ли виза в Generator.","Сумма стипендии OpenAI Safety Fellowship не прочитана, форма не открыта; когда Cohere Scholars реально откроется (статус Closed при обещании осени 2026).","Статус непроверенных вендоров (Amazon, Apple, IBM, китайские лаборатории и др.), а также Together и Cerebras (видны только через агрегаторы).","Отчёт содержит только 1 из 6 ног веера: нужна перекрёстная проверка другими вендорами и живой повторный прогон дедлайнов."],"related_concepts":["AI safety fellowships","Frontier AI lab entry programs","Дедупликация заявок по program_key","Ежедневная и еженедельная рутина discovery программ","Work authorization и визовые барьеры","Anthropic Fellows","MATS","Constellation ecosystem","Реестр заявок application_state","Deep Research кворум вендоров"]}
