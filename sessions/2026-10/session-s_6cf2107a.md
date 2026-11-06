---
session: s_6cf2107a
date: 2026-10-29
words: 7132
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-10-29 · You are distilling a DEEP-RESEARCH report into a compact, searchable knowledge note

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_6cf2107a` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

You are distilling a DEEP-RESEARCH report into a compact, searchable knowledge note.
One report, possibly assembled from several AI vendors researching the SAME question.

DR-ID: DR26-10-28-HUB-04
REGISTRY TOPIC: TAP Air Portugal: глубокий разбор отбора пилота OP23SET26

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


===== VENDOR: report (DR26-10-28-HUB-04-tap-air-portugal-глубокий-разбор-отбора-пилот.md) =====
# TAP Air Portugal: глубокий разбор отбора пилота OP23SET26

**Исследовательский срез:** 28 октября 2026 года, Portugal/Lisbon.  
**Рабочий идентификатор:** DR26-10-28-HUB-08-1650.  
**Исходный профиль:** инструктор Sevenair в Португалии; заявлено около 2 500 total time; известен опыт IFR и piston; **неизвестны** turbine/jet hours, наличие type rating, точный EASA licensing state, сроки IR/ME, статус MCC/Advanced UPRT и конкретное основание права на работу в Португалии. Эти неизвестные нельзя заполнять догадками.

Главный вывод исследования: текущий TAP OP23SET26 — реальный конкурс с формально опубликованной трёхфазной схемой. В минимальных требованиях публично фигурируют ≥500 h, EASA CPL(A), действующие Class 1 и ME-IR, завершённая/действительная ATPL theory, MCC, Advanced UPRT либо любой type rating вместо отдельного Advanced UPRT certificate, ICAO English ≥4 и владение португальским и английским. A320/type rating **ценится, но A320 rating не является опубликованным minimum requirement**. citeturn25view1turn36search0turn36search2

Отдельно: я **не нашёл публичного правила TAP или общего правила EASA/EU, по которому один лишь российский паспорт исключает кандидата из работы пилотом у несакционированного перевозчика ЕС**. Более того, EASA прямо разъясняет, что российский гражданин может получать/использовать Part-FCL licensing и medical для эксплуатации нероссийского воздушного судна, например как сотрудник авиакомпании ЕС. Но из этого не следует автоматическая пригодность конкретного кандидата: отдельно существуют право на работу/проживание, individual sanctions screening, aviation-security background check, EASA licensing и собственная кадровая проверка TAP. citeturn17search6turn17search0turn37view3

И ещё одно важное несоответствие: **5 ноября 2026 года — четверг, а не пятница. Пятница — 6 ноября.** В официальном графике TAP блок *Avaliação Aeronáutica* действительно занимает 2–6 ноября. Поэтому «5 November, Friday» — внутренне противоречивая формулировка: нельзя самостоятельно решать, что правильна дата либо день недели; нужно ориентироваться на окончательный timestamp/дату в официальном приглашении или candidate portal. citeturn25view0

## Что установлено официально и что пока неизвестно

Основным источником здесь должен считаться **официальный TAP Regulamento do Concurso PNT, REF. OP23set2026**, а не сайты подготовки к interview. Он устанавливает три фазы и прямо говорит, что все они eliminatory. citeturn25view1turn25view2turn26view1

| Вопрос | Что установлено | Практическое значение |
|---|---|---|
| Минимальный налёт | ≥500 h в опубликованном OP23SET26 | ~2 500 h, если они документированы и принимаются TAP, заметно выше минимума. citeturn36search0turn36search2 |
| Лицензия | Действующая EASA CPL(A) | Если лицензия не Part-FCL/EASA, это фундаментальная проблема; приглашение её не «исправляет». citeturn25view1turn36search2 |
| IR/ME | Действующая multi-engine instrument qualification | TAP требует поддерживать IR/ME validity; если EASA licence выпущена не ANAC, предусмотрен transfer to ANAC к OPC, причём IR должен оставаться действующим для transfer. citeturn25view1 |
| Medical | EASA Class 1 действующий | Помимо существующего Class 1, во второй фазе есть отдельная medical evaluation TAP/UCS с результатом APTO/NÃO APTO. citeturn25view2turn23search1 |
| ATPL theory | Требуется завершённая/действительная theoretical ATPL | Проверить фактический статус в документах, а не полагаться на «frozen ATPL» как разговорный ярлык. citeturn36search0turn36search2 |
| MCC | Требуется | Наличие инструкторского опыта MCC не заменяет certificate, если именно certificate требуется вакансией. citeturn36search0turn36search2 |
| Advanced UPRT | Требуется, **но waived при наличии любого Type Rating** | Если type rating отсутствует, нужен отдельный Advanced UPRT; если имеется TR, сохранить доказательство этого в document pack. citeturn36search0turn20search8 |
| Type rating | A320 не указан как minimum | A320 существенно влияет на ranking; любой TR влияет на UPRT requirement. citeturn26view0turn36search0 |
| Языки | Portuguese + English, written/spoken; ICAO English ≥4 | В объявлении **нет опубликованного CEFR B2/C1 для Portuguese**, поэтому не стоит придумывать такой порог. citeturn36search0turn36search2 |
| Право на работу | В доступном публичном тексте OP23SET26 отдельной строки «EU citizenship/unrestricted EU work rights» я не обнаружил | Но гражданин третьей страны всё равно должен иметь законное основание для employment в Португалии. Это другой юридический вопрос. citeturn14search4turn14search3 |
| Российское гражданство | Публичного blanket TAP ban не найдено | Нельзя превращать отсутствие запрета в гарантию найма; нужны work authorization, sanctions/security/licence checks. citeturn17search6turn37view3 |

### Как TAP ранжирует опыт

На первой фазе TAP использует опубликованную балльную систему. За действующую квалификацию A319/A320/A321 и соответствующий опыт можно получить 5, 10 или 12 points в зависимости от объёма/recency. Отдельно flight hours дают до 5 points: hours на «high performance and complexity» aircraft, для которых TAP приводит B737/A320/B767 как примеры, умножаются на 0,003; hours на других aircraft — на 0,001. Degree с математикой/физикой — 4 points, другая признанная licenciatura — 2; ICAO English Level 5 — 1, Level 6 — 2. citeturn26view0

Поэтому при **строго условном** сценарии, что все заявленные 2 500 h TAP относит к категории «other types», математическая компонента flight-hours ranking была бы:

\[
2500 \times 0.001 = 2.5\ \text{points}.
\]

Это **не оценка фактического балла кандидата**. Turbine/jet/A320 hours неизвестны, и я бы особенно не стал автоматически трактовать piston «complex» в бытовом/EASA смысле как категорию TAP с коэффициентом 0,003: формулировка TAP и приведённые примеры указывают на значительно иной класс оборудования. Фактическую разбивку нужно делать из logbook против формулировки пункта 6.2. citeturn26view0

Если кандидат уже получил реальную summons/invitation на следующую фазу, это сильный признак того, что его application прошла текущий административный фильтр. **Но invitation не является юридическим заключением о будущем work authorization, security vetting, medical fitness или окончательном соответствии всем условиям employment.**

### Фактическая последовательность OP23SET26

Официальный документ даёт следующую структуру:

**Первая фаза — curricular ranking.** Это не экзамен: TAP ранжирует кандидатов по опубликованным баллам. После provisional list предусмотрен короткий appeal process. citeturn26view0turn25view2

**Вторая фаза — три последовательных eliminatory assessments:**
- письменная *Avaliação Aeronáutica*;
- psychological assessment;
- medical assessment.

Для письменной aeronautical assessment минимальный проходной результат — **75%**. Psychological и medical оцениваются APTO/NÃO APTO. Неудачный psychological assessment создаёт 12-месячный срок до новой кандидатуры. Результаты аналогичных внешних тестов вместо тестов TAP не принимаются; исключение предусмотрено лишь для возможного повторного medical по решению TAP при обоснованном сомнении. citeturn25view2turn26view1

**Третья фаза — simulator technical test и final jury interview.** В самом регламенте simulator описан как technical test, включающий theoretical evaluation; результат simulator и interview — APTO/NÃO APTO. citeturn25view1turn26view1

После успешного selection предусмотрены company integration и затем A320 type/refresher/conversion training согласно TAP ATO/OM(D); сами training courses также eliminatory. После release to line регламент предусматривает трёхлетний minimum-stay mechanism и пропорциональный training repayment, не менее €20 500 как исходная сумма при добровольном уходе без just cause до истечения этого периода. citeturn26view1turn26view2

Официальный календарь на момент исследования показывает definitive first-phase list примерно 29 октября, начало selective process 30 октября и первый блок aeronautical assessment 2–6 ноября. CIE I указан со стартом 2 декабря 2026. citeturn25view0

## Эпизод: отбор, eligibility и аудит документов

**Расчётный хронометраж подкаста: 35–40 минут.**

### Открытие: главное за несколько минут

Начать стоит не с interview techniques, а с elimination risk. Для этого профиля главная ошибка — считать «2 500 часов + приглашение» достаточным доказательством eligibility.

Фактические потенциальные blockers находятся в шести отдельных корзинах:

**licence → ratings → medical → training certificates → work authorization → security/background.**

Это независимые вещи. Наиболее опасные UNKNOWN сейчас: кто выдал EASA licence; даты CPL/ME-IR/Class 1; ATPL-theory status; MCC; наличие type rating либо Advanced UPRT; основание работы в Португалии.

### Document audit, который нужно сделать первым

Собрать одну таблицу, где **каждый факт подтверждается документом и expiry date**, а не памятью:

| Поле | Что вписать дословно |
|---|---|
| Licence | issuing authority, licence number, CPL(A), issue/expiry/status |
| IR | ME-IR wording и validity |
| ME class/type | точное endorsement и validity |
| Medical | Class 1, issuing AeMC/authority, expiry |
| ATPL theory | certificate/result + status/date |
| MCC | ATO, certificate, completion date |
| Advanced UPRT | certificate либо «not needed because TR: ___» |
| Type rating | exact type, current/expired, last check |
| Total time | exact logbook total, не «about 2,500» |
| PIC | exact |
| FI | exact |
| IFR/instrument | exact |
| multi-engine | exact |
| turbine | exact |
| jet | exact |
| multi-pilot | exact |
| A320 family | exact |
| last 12/24 months | exact totals by relevant category |
| ICAO English | level + expiry |
| Portuguese | честное operational/interview capability |
| Residence/work status | exact Portuguese document, legal basis, expiry |

Current TAP rules are unusually explicit that CPL(A), IR, ME and Class 1 должны быть действительными на application deadline и оставаться действительными вплоть до employment-contract stage; licence от другого EASA authority должна быть transferred to ANAC к OPC. citeturn25view1

Актуальная EASA Easy Access Rules for Aircrew была обновлена 16 октября 2026 года; для CPL/MPL/ATPL Part-MED требует действующий Class 1 medical. Поэтому здесь имеет смысл сверять licence/medical не со старой распечаткой правил, а с текущей Part-FCL/Part-MED и реальными документами. citeturn21view0turn23search1

Архивированные копии текста OP23SET26 дополнительно перечисляли среди application material CV, licence, medical, evidence of ATPL theory, MCC, Advanced UPRT unless TR, complete logbook/totals и academic documentation. Поскольку официальный TAP vacancy URL сейчас уже закрыт сообщением *“esta vaga já foi preenchida”*, эти зеркала полезны для восстановления original posting, но имеют меньший evidentiary weight, чем TAP regulation и уже загруженные документы candidate portal. citeturn35view0turn2view0

### Что означает профиль с ~2 500 h piston/IFR

Сильная сторона — не «большой TT сам по себе», а **повторяемый evidence of command judgement, IFR discipline, instruction, error detection and intervention**.

Слабая сторона при неизвестных turbine/jet hours — возможный большой разрыв между хорошо развитой instructional competence и тем, что assessors захотят увидеть как airline multi-crew readiness:

- отказ от «я преподаватель, поэтому я главный» в пользу PF/PM cooperation;
- быстрый переход от teaching commentary к concise operational communication;
- energy management на более быстром самолёте;
- anticipation вместо reactive aircraft handling;
- дисциплина SOP и automation monitoring;
- способность быть эффективно обучаемым, а не демонстрировать знания несуществующего type experience.

Это не опубликованные TAP scoring criteria для interview, а целевая подготовка, вытекающая из самого профиля TAP: компания в объявлении выделяет leadership, communication, teamwork, assertiveness, decision-making, problem solving, CRM/safety culture и technical/operational performance. citeturn36search2

### Российский паспорт: что на самом деле отделять друг от друга

Здесь критично не смешивать пять разных вопросов.

**Nationality.** Российское гражданство само по себе не равно EASA prohibition. EASA в санкционном FAQ прямо допускает training/testing/licensing российских граждан для работы вне России на нероссийских aircraft и приводит работу в EU airline как пример допустимой ситуации. Другой EASA FAQ подчёркивает различие между российским licence holder, работающим на несакционированного carrier, и деятельностью в интересах российского/санкционного субъекта. citeturn17search6turn17search0

**EU sanctions.** Действующие санкции действительно серьёзно ограничивают российскую aviation sector: российским carriers запрещён доступ к EU airspace/airports, имеются ограничения на aircraft, parts, technology и services. Одновременно individual sanctions являются списочными: travel bans и asset freezes применяются к перечисленным лицам. Совет ЕС описывает почти 4 600 listed individuals/entities, а не всех обладателей российского паспорта. citeturn37view3

Из этого следует важное различие:

> **Russian citizen employed by TAP on TAP/EU-operated aircraft ≠ Russian air carrier ≠ Russian-registered aircraft ≠ individually sanctioned person.**

Именно смешение этих категорий обычно порождает ложное утверждение «EU airlines cannot employ Russians».

**Residence/right to work.** Для third-country national легальная работа в Португалии требует соответствующего immigration/residence basis. AIMA описывает residence authorization for subordinate professional activity; EU Immigration Portal также отделяет residence visa/permit для employed third-country nationals от freedom of movement EU nationals. citeturn14search4turn14search3turn14search33

То, что человек уже работает flight instructor в Португалии, **не позволяет мне из внешних данных определить точный immigration status или автоматически доказать право перейти к TAP**. Нужно смотреть фактический Portuguese residence/work document.

**Licensing.** Российский паспорт не означает российскую licence. Для TAP существенна EASA CPL(A) и её issuing authority. EASA отдельно предупреждает, что conversion лицензии, первоначально основанной на Russian CAA records, может создавать проблемы с verification; это отличается от ситуации, когда человек уже имеет полноценную EASA Part-FCL licence. citeturn17search6

**Security/background.** EU aviation-security framework требует enhanced background check для соответствующих crew/airport identification privileges. Это security-vetting вопрос, а не опубликованный nationality ban. Я не нашёл в текущем generic EU rule положения вида «Russian nationals fail automatically». citeturn20search2

Практический inference: иностранная история проживания может означать больше документов и verification work. Но из этого **нельзя** выводить ни отказ, ни вероятность отказа.

**TAP company policy.** В публичных условиях именно OP23SET26, которые удалось проверить, я не обнаружил запрета российского гражданства. Публичное отсутствие такого запрета, однако, **не доказывает отсутствие любых внутренних sanctions/compliance/security checks**. Поэтому корректная формулировка — *«публичного blanket nationality exclusion не найдено»*, а не *«TAP гарантированно принимает Russian nationals»*. citeturn25view1turn36search0turn36search2

### Как отвечать, если nationality/work-rights поднимают на interview

**EN**

> “My nationality is Russian. My current legal status in Portugal is **[exact status]**, valid until **[date]**, and my authorization to work is based on **[document/legal status]**. My EASA licence is issued by **[authority]**. I can document each of those points separately.”

Это лучше, чем: *“I already work in Portugal, so there is no problem.”* Последняя фраза делает юридический вывод, которого кандидат не должен делать без документов.

**PT**

> “A minha nacionalidade é russa. O meu estatuto legal atual em Portugal é **[estatuto exato]**, válido até **[data]**, e a minha autorização para trabalhar resulta de **[documento/estatuto]**. A minha licença EASA foi emitida por **[autoridade]**. Posso apresentar a documentação correspondente a cada ponto.”

Не надо добровольно превращать interview в политическую дискуссию. Отвечать точно на compliance question, без defensive monologue.

## Эпизод: competency interview, CRM/TEM и языковая подготовка

**Расчётный хронометраж: 30–40 минут.**

### Что официально ожидается

Текущий TAP profile прямо называет leadership, communication, teamwork, assertiveness, decision-making, problem solving, CRM, safety culture и solid aeronautical knowledge. citeturn36search2

Это хорошо совпадает с EASA CRM framework: CRM рассматривается как существенный safety factor в CAT operations, а training интегрирует communication, workload/team cooperation, situational awareness, problem-solving/decision-making и management of error/threats. citeturn20search12turn20search5

Поэтому инструктору не нужно придумывать «airline captain stories». Наоборот, честный FI material может быть сильным, если каждая история показывает:

**threat recognition → information gathering → communication → decision → intervention → monitoring → debrief/learning.**

### Правильный STAR для инструктора

Не готовить 20 историй. Подготовить **шесть реальных episodes**, каждый примерно на 90–120 секунд:

1. безопасность против schedule/pressure;
2. собственная ошибка или неверное предположение;
3. trainee/student error, который пришлось остановить;
4. сложное решение при weather/technical/operational uncertainty;
5. конфликт или disagreement с коллегой;
6. случай, когда initial plan пришлось изменить после новой информации.

Для каждой карточки:

**S — Situation:** максимум 2–3 предложения.  
**T — Task:** что было вашей ответственностью.  
**A — Action:** именно ваши observable actions, без «we did everything».  
**R — Result:** конкретный результат + чему научились.  
**Reflection:** что сегодня сделали бы лучше.

Самая полезная финальная строка для airline interview часто не «everything went well», а:

> “The main lesson for me was ___, and since then I have changed ___.”

Она показывает trainability.

### Пример структуры без выдумывания личной истории

**EN prompt**

> “Tell us about a time you had to intervene for safety during instruction.”

**Не готовый ответ, а skeleton:**

> “During **[real lesson/flight]**, I noticed **[specific threat/deviation]**. My responsibility was **[task]**. I first **[communication/action]**, then **[decision/intervention]**, while monitoring **[key risk]**. The result was **[verifiable outcome]**. During the debrief I identified **[lesson]**. Looking back, I would improve **[specific point]**.”

**PT prompt**

> “Fale-nos de uma situação em que teve de intervir por razões de segurança durante a instrução.”

**Skeleton:**

> “Durante **[voo/aula real]**, identifiquei **[ameaça/desvio específico]**. A minha responsabilidade era **[tarefa]**. Primeiro **[comunicação/ação]** e depois **[decisão/intervenção]**, mantendo a atenção em **[risco]**. O resultado foi **[resultado verificável]**. No debriefing identifiquei **[aprendizagem]**. Hoje melhoraria **[ponto específico]**.”

### Вопросы, которые стоит прогнать вслух на английском

**“Why do you want to move from flight instruction to airline operations?”**

Хорошая логика: не обесценивать instruction. Показать progression:

> “Instruction has developed my judgement, communication and monitoring skills. I now want to apply those skills in a structured multi-crew airline environment, while accepting that airline operations require a different level of SOP discipline, task sharing and standardisation.”

Не говорить, что FI job «boring» или нужен TAP только ради jet hours.

**“What will be your biggest transition challenge?”**

При неизвестном jet experience честный ответ сильнее bluff:

> “The main transition is from the aircraft and operating environment I know well to a faster, highly standardised multi-crew jet environment. I would manage that through disciplined preparation, strict use of SOPs, active monitoring and being very receptive to instructor feedback.”

**“Tell us about a mistake you made.”**

Запрещённый mental model: выбрать тривиальную ошибку, а затем доказать, что фактически вы были идеальны.

Нужны: genuine mistake → containment → ownership → learning → changed behaviour.

**“What does good CRM mean to you?”**

Не читать определение из учебника:

> “For me, good CRM means using the crew and all available information to maintain a shared and accurate picture of the operation, speaking up early when something does not look right, making decisions explicitly, and continuously checking whether the plan is still safe.”

### Те же drills по-португальски

**“Porque pretende passar da instrução para uma operação de linha aérea?”**

> “A instrução permitiu-me desenvolver julgamento, comunicação, monitorização e gestão de carga de trabalho. Quero agora aplicar essas competências num ambiente de operação multi-crew mais padronizado, sabendo que terei de me adaptar rigorosamente aos SOP, à divisão de tarefas e à cultura operacional da companhia.”

**“Qual considera ser o maior desafio na transição para um avião a jato?”**

> “O principal desafio será adaptar-me a um ambiente mais rápido, mais automatizado e altamente padronizado. A minha abordagem será preparar-me de forma disciplinada, cumprir os SOP, manter uma monitorização ativa e utilizar o feedback dos instrutores.”

**“Fale-nos de um erro seu.”**

Estrutura:

> “O erro foi **[erro real]**. Apercebi-me através de **[indício]**. A minha primeira ação foi **[contenção]**. Depois **[correção/comunicação]**. No debriefing concluí **[aprendizagem]** e alterei **[comportamento/processo]**.”

**“O que significa um bom CRM para si?”**

> “É garantir uma perceção partilhada da situação, comunicar cedo e de forma clara, utilizar todos os recursos disponíveis, gerir ameaças e erros e confirmar continuamente se o plano continua seguro.”

### TEM drill: не превращать его в акронимный экзамен

Хороший practical flow:

**Threat:** что увеличило operational complexity и не было создано вашей ошибкой.  
**Countermeasure:** briefing, plan, cross-check, margin.  
**Error:** действие/бездействие crew, отклонившееся от intention/expectation.  
**Trap:** error remains unnoticed or poorly managed.  
**Undesired state:** aircraft/operation arrives at a state that reduces safety margin.  
**Recovery:** recognise, communicate, prioritise, stabilise, reassess.

Для FI кандидатуры пример должен быть **реальным**, например weather, runway change, student overload, ATC change или time pressure — но конкретную историю кандидат должен взять из собственного logbook/опыта, а не из этого отчёта.

### Особая ловушка для инструктора

На interview не быть «examiner mode».

Плохой сигнал:

> “I told the student what to do and took control.”

Лучше показать sequence:

> “I identified the developing threat, made the required intervention at the appropriate point, restored a safe state, and then used the debrief to make sure the student understood both the cue and the decision process.”

То есть decisiveness без ego.

### Language traps

TAP публично требует Portuguese и English written/spoken, а авиационный English не ниже ICAO 4. Level 5/6 дополнительно приносит ranking points. citeturn36search0turn26view0

Поэтому тренировать следует не красивый accent, а:

- короткую структуру ответа;
- numbers/dates/licensing terminology;
- объяснение safety decision;
- disagreement without confrontation;
- признание неизвестного;
- переход от technical vocabulary к plain language.

Очень хороший drill — дать 90-секундный STAR по-английски, затем **тот же смысл**, но не буквальный перевод, за 90 секунд по-португальски.

### Фразы, которые лучше уметь произнести автоматически

**EN**

> “I don’t want to speculate. Based on the information available to me, I would…”

> “I would first stabilise the situation, confirm the relevant information and then make the decision.”

> “I would follow the applicable SOP and the approved aircraft documentation.”

> “I have not operated that aircraft type, so I would not claim type-specific knowledge I do not have.”

> “I disagreed with the initial plan, so I stated the concern clearly and proposed an alternative.”

**PT**

> “Prefiro não especular. Com base na informação disponível, eu…”

> “Primeiro estabilizaria a situação, confirmaria a informação relevante e depois tomaria a decisão.”

> “Seguiria o SOP aplicável e a documentação aprovada da aeronave.”

> “Não operei esse tipo de aeronave, por isso não vou afirmar conhecimentos específicos que não possuo.”

> “Não concordei com o plano inicial, por isso expus a preocupação de forma clara e propus uma alternativa.”

Последняя пара особенно важна: признавать границу knowledge — airline behaviour, а не слабость.

## Эпизод: technical, IFR, performance, weather и jet transition

**Расчётный хронометраж: 35–40 минут.**

### Что точно известно про technical assessment

Официально известно немного, но это важное «немного»:

- Phase 2 содержит **written aeronautical assessment**;
- проходной результат — **≥75%**;
- Phase 3 содержит **simulator technical test including theoretical evaluation**;
- simulator оценивается APTO/NÃO APTO. citeturn25view2turn25view1turn26view1

**Публичного syllabus OP23SET26, точного question bank, типа simulator aircraft, sequence exercises или scoring matrix я не обнаружил.**

Это нужно воспринимать буквально. Не следует выдавать A320 sim, engine failure, raw-data ILS, group exercise или psychometric battery за подтверждённый current TAP format.

### Что говорят неофициальные источники

Коммерческий assessment-prep сайт SET STANDARD в обновлении October 2026 описывает current OP23SET26 как процесс с aeronautical/theory, psych и simulator/interview preparation, но сам прямо позиционирует материал как independent compilation из public sources/candidate reports, а не TAP publication. citeturn34search5

Другой commercial assessment site перечисляет ATPL questions, reasoning/psychometrics, group work, interview и simulator. Однако **group exercise, например, отсутствует в официальной схеме OP23SET26**. Поэтому это максимум hypothesis для резервной подготовки, не факт текущего конкурса. citeturn6search21turn25view1

Исторический PPRuNe report примерно 2007 года описывал English/psych/group/interview/simulator и для некоторых non-FBW candidates — IFR-oriented sim. Это полезно только как двадцатилетний anecdotal precedent: переносить оттуда упражнения в 2026 было бы методологически неправильно. citeturn0search8

Именно поэтому подготовка должна быть **airline-foundation heavy, aircraft-memory-item light**.

### Приоритет technical revision

#### IFR

Прогнать до состояния, когда объяснение идёт без зубрёжки:

- IFR planning logic;
- departure/arrival/approach structure;
- ILS versus RNAV/RNP concepts;
- minima, DA/H/MDA/H concepts;
- alternate logic;
- holding entries и wind correction как concepts;
- missed-approach decision discipline;
- PBN terminology;
- RVR/visibility distinctions;
- NOTAM/SIGMET/METAR/TAF integration;
- fuel-planning architecture.

Где нормы зависят от regulation/operator — отвечать с оговоркой **“according to the applicable regulation and operator OM”**, а не вытягивать из памяти старое числовое правило.

#### Performance

Уметь **объяснить причинность**, а не только формулы:

- почему mass увеличивает take-off distance;
- temperature/pressure/density-altitude effects;
- headwind/tailwind;
- slope;
- wet/contaminated runway;
- obstacle-limited versus runway-limited take-off;
- accelerate-stop versus accelerate-go intuition;
- climb-gradient versus rate-of-climb;
- landing-distance factors;
- CG effects;
- tyre/brake/runway limits как concepts.

Вопрос «What changes if the runway becomes wet?» должен вызвать системный ответ: **performance calculation → available stopping/acceleration margins → operational limitations → revised decision**, а не одну memorised percentage.

#### Weather

Высокая отдача:

- frontal systems;
- CB life cycle;
- embedded CB;
- windshear/microburst;
- icing mechanisms;
- freezing rain;
- turbulence;
- mountain wave;
- jet stream/CAT;
- pressure systems;
- temperature/dew point;
- METAR/TAF/SIGMET interpretation.

Для windshear/upset **не давать на interview самодельные aircraft-specific memory items**. Правильная позиция:

> “I would recognise the condition, prioritise aircraft control and apply the approved procedure/SOP for the aircraft.”

Для UPRT EASA поддерживает formal advanced training framework; type-specific recovery всегда должна опираться на approved training/manuals. citeturn20search8

#### Aerodynamics и high-speed transition

Особенно для piston-background кандидата:

- swept-wing behaviour;
- Mach effects;
- critical Mach concept;
- shock-induced drag/separation;
- high-altitude buffet margins;
- load factor versus stall;
- energy state;
- thrust response/spool characteristics;
- inertia;
- pitch/power/flight-path relationships;
- pressurisation basics;
- jet-engine conceptual architecture.

Не пытаться за неделю сделать вид, что есть A320 type knowledge. Гораздо лучше точно понимать generic transport-jet physics.

#### Jet operational mindset

Это может дать больше в simulator, чем недели «chair-flying» чужих flows:

**Energy management.** На высокой скорости ошибка, оставленная на 30 секунд, дорого стоит.

**Ahead of aircraft.** Configuration, path, altitude and speed changes anticipatory, not reactive.

**Mode awareness.** Если используется automation, знать, что commanded now, что armed next и совпадает ли actual flight path с intention.

**PF/PM discipline.** Даже без опубликованного TAP scenario демонстрировать brief, cross-check, call-out philosophy и willingness to accept correction.

**Stabilise before diagnose.** Сначала safe flight path/workload, потом secondary problem-solving.

EASA CRM material именно поэтому рассматривает CRM не как soft-skills decoration, а как safety component commercial operations. citeturn20search12

### Simulator: к чему готовиться при неизвестном формате

Официально TAP гарантирует только наличие simulator test; platform/scenario публично не указан. citeturn26view1

Поэтому simulator-prep hierarchy я бы строил так:

**Первый уровень — scan and flight path.** Heading, altitude, speed, vertical path, trend.

**Второй — brief.** Короткий departure/approach brief, threats, division of attention.

**Третий — workload.** Не chasing instruments; prioritisation.

**Четвёртый — crew behaviour.** Verbalise meaningful information, accept monitoring, correct deviations.

**Пятый — generic jet energy.**

**Шестой — A320 familiarisation только на concept level**, если нет TR: displays, flight-mode awareness, broad automation philosophy. Не учить нелегальные/непроверенные flows и memory items из интернет-файлов.

Если у кандидата на самом деле есть A320/current TR, подготовка меняется радикально: тогда использовать **его действующие approved manuals, SOP/FCTM/FCOM material, доступный на законном основании**, а не generic internet notes.

### Technical mock interview

Ниже — вопросы, которые проверяют именно transferable understanding.

**EN: “What factors can make an aircraft take-off-performance limited?”**

Нужна структура:

> aircraft mass → atmosphere → runway length/state/slope → wind → obstacle environment → aircraft/configuration/technical limitations → required regulatory margins.

**EN: “Why is energy management more demanding in a transport jet than in the piston aircraft you currently fly?”**

Хороший ответ касается speed, inertia, altitude, thrust response, configuration timing, descent planning — без притворного type knowledge.

**EN: “You are high and fast on an approach. What is your thought process?”**

> recognise deviation → compare with stabilised-approach criteria/SOP → assess whether safe recovery remains available → communicate → if criteria cannot be met, discontinue/go around according to SOP.

Не геройствовать.

**EN: “What is the difference between a threat and an error?”**

Дать operational example, а не только definition.

**EN: “What concerns you about a rapidly falling temperature close to freezing in visible moisture?”**

Icing potential, changing surface/airframe/engine exposure, runway state, weather trend, operational limitations; затем manuals/SOP.

**EN: “Explain why high density altitude degrades take-off performance.”**

Lower air density → reduced aerodynamic/propulsive performance depending on powerplant → greater true speed/distance for required aerodynamic conditions → degraded climb capability.

**EN: “What does RNP add conceptually compared with basic RNAV?”**

Сказать про required navigation performance и onboard performance monitoring/alerting, не уходя в непроверенные procedure-specific minima.

**PT: “Quais são os principais fatores que limitam a performance à descolagem?”**

> “Começaria pela massa da aeronave, condições atmosféricas, vento, comprimento, inclinação e estado da pista, obstáculos e limitações específicas da configuração ou da aeronave. Depois confirmaria os cálculos e margens de acordo com os procedimentos aprovados.”

**PT: “Está alto e rápido na aproximação. Como decide se continua?”**

> “Reconheço primeiro o desvio, comparo a situação com os critérios de aproximação estabilizada e os SOP aplicáveis, comunico claramente e avalio se ainda existe uma recuperação segura. Se os critérios não puderem ser cumpridos, não tentaria salvar a aproximação.”

### Mini mock panel

Прогнать подряд, без notes:

1. **EN — “Walk us through your flying background.”**  
   Цель: 90 секунд, точные цифры, никаких округлений, которые расходятся с logbook.

2. **PT — “Porque quer trabalhar na TAP?”**  
   Цель: Portugal + long-term airline/multi-crew progression + learning/standardisation. Не «because TAP is prestigious».

3. **EN — “What airline competencies do you bring from instructing?”**  
   Цель: monitoring, communication, intervention, planning, debriefing, decision-making.

4. **PT — “Fale-nos de uma decisão difícil relacionada com segurança.”**  
   Реальная STAR.

5. **EN — “Tell us about a mistake.”**  
   Ownership.

6. **EN — “What is the biggest gap in your experience?”**  
   Если jet/turbine gap реален — назвать его, а не маскировать.

7. **PT — “Como reage quando outro piloto não concorda consigo?”**

8. **EN — “What would you do if the captain chose a course of action you considered unsafe?”**  
   Assertive escalation, shared facts, challenge, SOP; не submissiveness и не instant confrontation.

9. **Technical — performance/weather/IFR random question.**

10. **EN — “Do you have unrestricted permission to work in Portugal?”**  
    Только exact documented answer. Если статус имеет ограничения, их не скрывать.

## План подготовки на семь дней

Исхожу из reported assessment date **Thursday, 5 November 2026**. Официальный TAP calendar подтверждает, что 2–6 November является первым published aeronautical-assessment window; однако reported word “Friday” противоречит календарю, поэтому first action — удостовериться в точной дате из исходного invitation. citeturn25view0

### Четверг, двадцать девятое октября

**Приоритет: eliminate administrative surprises.**

Потратить первый час не на ATPL bank, а на audit: licence authority, CPL, ME-IR, medical, ATPL theory, MCC, UPRT/TR, ICAO English, work/residence status.

Затем построить logbook summary:

`TT / PIC / IFR / ME / FI / turbine / jet / multi-pilot / A320 / last 12m / last 24m`.

После этого — один 60–90-minute diagnostic technical test без подготовки. Отмечать темы, где ответ неуверенный, а не процент ради ego.

### Пятница, тридцатое октября

**Приоритет: IFR foundation.**

Около 3 часов чистой работы:
- IFR/PBN;
- instrument approaches;
- alternates/fuel concepts;
- METAR/TAF/SIGMET;
- 30 минут mental arithmetic/performance.

Финал дня: 20 technical questions вслух на английском.

### Суббота, тридцать первое октября

**Приоритет: performance + aerodynamics + jet transition.**

Performance reasoning, density altitude, runway condition, mass/CG, takeoff/landing constraints.

Затем high-speed aerodynamics и jet energy.

Последний блок: generic jet simulator/desktop session, если доступен, **только для instrument scan, energy and workload**, не для запоминания случайных A320 procedures.

### Воскресенье, первое ноября

**Приоритет: weather + integrated IFR scenarios.**

Взять 8–10 fictional route scenarios:

> destination weather deteriorating;  
> alternate becomes marginal;  
> runway changes;  
> CB on arrival;  
> icing environment;  
> high/fast arrival;  
> strong crosswind;  
> unexpected ATC restriction.

На каждый: **threats → information → options → decision → monitoring.**

### Понедельник, второе ноября

**Приоритет: behavioural + Portuguese/English.**

Подготовить шесть реальных STAR cards.

Каждую:
- EN ≤2 min;
- PT ≤2 min;
- один follow-up *“what did you learn?”*;
- один hostile follow-up *“why did you not act earlier?”*.

Отдельно 20 минут на nationality/work-rights answer без импровизации.

### Вторник, третье ноября

**Приоритет: full mock assessment.**

Утром — 60–90 min timed aeronautical test; current TAP pass mark составляет 75%, поэтому на тренировке цель разумно держать заметно выше cutoff, а не 75% ровно. citeturn25view2

После перерыва — 30 min interview EN/PT.

Позже — simulator session: scan, precision, brief, workload, energy, CRM. Никаких новых aircraft procedures.

### Среда, четвёртое ноября

**Приоритет: taper, accuracy, sleep.**

Не устраивать 8-hour ATPL binge.

Коротко:
- incorrect-question log;
- 20 core technical concepts;
- six STAR openings;
- licence/documents;
- logistics;
- нормальный сон.

Если в invitation всё же выяснится **Friday, 6 November**, четверг 5-го использовать как лёгкий review day, а не дополнительный marathon.

## Матрица неопределённостей и решение перед assessment

| Неопределённость | Уровень риска | Что известно | Что сделать |
|---|---:|---|---|
| 5 Nov vs Friday | **Высокий** | 5 Nov 2026 = Thursday; 6 Nov = Friday; TAP assessment window 2–6 Nov. citeturn25view0 | Проверить исходный invitation/portal, не интерпретировать самостоятельно |
| Какая именно assessment 5 Nov | Средний | Aeronautical assessment официально запланирована в блоке 2–6 Nov. citeturn25view0 | Считать wording invitation source of truth |
| EASA issuing authority | **Высокий** | Non-ANAC EASA licence должна быть transferred to ANAC by OPC. citeturn25view1 | Записать authority и transfer status |
| CPL/ME-IR validity | **Высокий** | Должны оставаться valid до contract; IR нужен для licence transfer. citeturn25view1 | Проверить dates сегодня |
| Class 1 | **Высокий** | Mandatory + отдельная TAP medical assessment. citeturn25view2turn23search1 | Проверить certificate/limitations |
| ATPL theory | **Высокий** | Required in job announcement. citeturn36search0 | Проверить документ и validity |
| MCC | **Высокий** | Required. citeturn36search2 | Найти certificate |
| Advanced UPRT | **Высокий** при отсутствии TR | Mandatory unless any type rating. citeturn36search0 | Подтвердить UPRT или TR |
| Type rating | Средний | Не minimum A320 requirement; A320 влияет на ranking. citeturn26view0turn36search0 | Указать exact TR/current status |
| Turbine/jet hours | Средний | Не опубликованы как minimum; влияют на фактический профиль/возможный ranking category | Вытащить exact totals из logbook |
| ~2 500 hours | Средний | ≥500 minimum; flight-hour scoring зависит от категории aircraft. citeturn26view0turn36search0 | Не говорить «about» на formal interview |
| Portuguese | Средний | Written/spoken Portuguese required; CEFR threshold публично не указан. citeturn36search2 | 60–90 min/day spoken drills |
| ICAO English | **Высокий** | ≥4 minimum; 5/6 дают ranking points. citeturn26view0turn36search0 | Проверить endorsement/expiry |
| Right to work | **Высокий** | Third-country status регулируется отдельно от pilot licence. citeturn14search4turn14search3 | Иметь exact residence/work basis |
| Russian passport | Сам по себе **не установленный blocker** | EASA допускает Russian nationals для non-Russian/EU airline operations при соблюдении sanctions framework. citeturn17search6turn17search0 | Не смешивать nationality с work permit/security/licensing |
| Individual sanctions | Потенциально высокий, но **неизвестен и не исследовался для частного лица** | EU individual sanctions относятся к listed persons/entities. citeturn37view3 | Candidate/compliance process проверяет собственный статус; этот report не исследует частное лицо |
| Aviation security clearance | Средний | Applicable crew access связан с enhanced background check. citeturn20search2 | Иметь coherent residence/employment history и запрошенные официальные документы |
| Simulator aircraft | Неизвестно | Current TAP regulation говорит только «simulator technical test». citeturn26view1 | Generic IFR/jet/CRM first; type-specific only from approved material |
| Simulator scenarios | Неизвестно | Не опубликованы | Не учить слухи как syllabus |
| Psychometric format | Неизвестно | Psychological assessment официально есть, но format не опубликован. citeturn25view2 | Sleep, consistency, honest answers; не «game the personality test» |
| Final jury questions | Неизвестно | Final jury interview входит в phase 3. citeturn26view1 | STAR + EN/PT + documents + technical reasoning |

Итоговая стратегия здесь довольно жёсткая: **не пытаться за семь дней превратить piston/IFR instructor в воображаемого A320 pilot.** TAP уже знает из CV/logbook, какой у кандидата background. Более сильный сигнал — безупречная документальная точность, крепкая ATPL/IFR база, disciplined instrument flying, понятное jet-energy reasoning, CRM без instructor ego, честная граница type-specific knowledge и способность быстро принимать feedback.

## Источники и уровень доказательности

Ниже — более 15 URL, использованных для проверки. **P = primary/official**, **S = secondary current reporting/archive**, **A = anecdotal/commercial — только для контекста, не для установления требований.**

**P — TAP, текущий OP23SET26.** Официальный конкурсный регламент и календарь; главный источник по phases, ranking, 75% cutoff, medical, simulator, licence transfer и subsequent training. citeturn25view0turn25view1turn25view2turn26view0turn26view1turn26view2  
`https://publish-p133109-e1368204.adobeaemcloud.com/content/dam/tap-institucional/media/pdfs/23-sep26/Regulamento_Concurso_PNT_2026_2027.pdf`

**P — TAP Careers, original OP23SET26 job URL.** На 28 October страница уже закрыта с сообщением, что vacancy filled/closed. citeturn35view0  
`https://recrutamento.tap.pt/job/TAP-OFICIAIS-PILOTO-DE-AVIA%C3%87%C3%83O-COMERCIAL-REF%C2%AA-OP23SET26/id_de0be2a9/`

**P — TAP pilot careers category.** Текущая careers infrastructure для pilot vacancies. citeturn1search9  
`https://recrutamento.tap.pt/go/Pilotos/742502/`

**S — Kiosque da Aviação, 26 September 2026.** Современная публикация OP23SET26: 500 h, CPL, Class 1, ATPL theory, ME-IR, MCC, Advanced UPRT/TR waiver, languages. citeturn36search0  
`https://kiosquedaaviacao.pt/tap-air-portugal-abre-recrutamento-para-oficiais-piloto-de-aviacao-comercial/`

**S — EmpregoEstagios, 24 September 2026.** Независимое воспроизведение текущего candidate profile и requirements. citeturn36search2  
`https://www.empregoestagios.com/tap-portugal-esta-a-recrutar-pilotos-de-aviacao-comercial/`

**S — BeBee archived mirror.** Полезен для восстановления списка application documents; не заменяет TAP regulation. citeturn2view0  
`https://bebee.com/pt/jobs/tap-air-portugal-oficiais-piloto-de-aviacao-comercial-tap-air-portugal-lisbon--t7xk-854191065`

**P — EASA, Easy Access Rules for Aircrew, revision October 2026.** Текущая consolidated Part-FCL/Part-MED framework. citeturn21view0turn22view0  
`https://www.easa.europa.eu/en/document-library/easy-access-rules/easy-access-rules-aircrew`

**P — EASA, Part-MED.** CPL/MPL/ATPL требуют действующий Class 1 medical. citeturn23search1  
`https://www.easa.europa.eu/en/document-library/easy-access-rules/online-publications/easy-access-rules-aircrew-regulation-eu-no?page=1&regulatory-subject=Part-MED`

**P — EASA, UPRT FAQ.** Regulatory context Advanced UPRT. citeturn20search8  
`https://www.easa.europa.eu/en/the-agency/faqs/upset-prevention-and-recovery-training`

**P — EASA, Easy Access Rules for Air Operations, revision March 2026.** Current Part-ORO/CRM regulatory context. citeturn20search1turn20search5  
`https://www.easa.europa.eu/en/document-library/easy-access-rules/easy-access-rules-air-operations`

**P — EASA, CRM Training Implementation.** CRM как significant CAT safety factor и training framework. citeturn20search12  
`https://www.easa.europa.eu/en/document-library/general-publications/crm-training-implementation`

**P — EASA, restrictive measures Russia: aircrew training/licensing.** Ключевой источник по допустимости обучения, licensing и medical российских граждан для non-Russian aircraft/EU-airline operations. citeturn17search6  
`https://www.easa.europa.eu/en/the-agency/faqs/aircrew-training-and-licensing-restrictive-measures-russia`

**P — EASA FAQ on Russian citizens holding personnel licences.** Разделяет работу в пользу non-sanctioned carrier и запрещённые Russian-related operations. citeturn17search0  
`https://www.easa.europa.eu/en/faq/136154`

**P — Council of the EU, sanctions Q&A, reviewed 12 October 2026.** Individual sanctions, aviation-sector sanctions и список категорий ограничений. citeturn37view3  
`https://www.consilium.europa.eu/en/policies/sanctions-against-russia-explained/`

**P — European Commission, visa measures concerning Russia.** Визовые ограничения следует отличать от blanket employment prohibition. citeturn15search11  
`https://commission.europa.eu/topics/eu-solidarity-ukraine/eu-sanctions-against-russia-following-invasion-ukraine/visa-measures_en`

**P — AIMA Portugal, residence authorization for subordinate employment.** Основание для разграничения citizenship и legal work authorization. citeturn14search4  
`https://aima.gov.pt/pt/trabalhar/autorizacao-de-residencia-para-exercicio-de-atividade-profissional-subordinada-com-visto-de-residencia-art-88-o-n-o-1`

**P — EU Immigration Portal, employed worker in Portugal.** Immigration framework для third-country workers. citeturn14search3  
`https://home-affairs.ec.europa.eu/policies/migration-and-asylum/eu-immigration-portal/employed-worker-portugal_en`

**P — European Commission, working in another EU country: non-EU nationals.** Отличает EU free-movement rights от положения third-country nationals. citeturn14search33  
`https://employment-social-affairs.ec.europa.eu/policies-and-activities/moving-working-europe/working-another-eu-country/non-eu-nationals_en`

**P — AIMA, employment contracts with foreign citizens, 23 February 2026.** Актуальный Portuguese administrative context для foreign workers. citeturn14search17  
`https://aima.gov.pt/pt/noticias/contratos-de-trabalho-com-cidadaos-estrangeiros`

**P — EUR-Lex, Commission Implementing Regulation (EU) 2015/1998 consolidated 1 October 2026.** Aviation-security requirement for enhanced background checks linked to crew/airport identification. citeturn20search2  
`https://eur-lex.europa.eu/legal-content/EN/TXT/HTML/?uri=CELEX%3A02015R1998-20261001`

**P — EUR-Lex, ECRIS-TCN framework.** Дополнительный официальный контекст для criminal-record information concerning third-country nationals; не является TAP-specific selection rule. citeturn31search12  
`https://eur-lex.europa.eu/EN/legal-content/summary/european-criminal-records-information-system-conviction-information-on-third-country-nationals-ecris-tcn.html`

**A — SET STANDARD, updated October 2026.** Полезная contemporary independent reconstruction, но не источник официального syllabus. citeturn34search5  
`https://setstandard.es/en/tap-air-portugal-pilot-assessment/`

**A — PilotAssessments.** Commercial assessment-preparation source; его дополнительные claims вроде group exercise не подтверждаются текущим official regulation и потому не приняты как факт. citeturn6search21  
`https://pilotassessments.com/tap-air-portugal-pilot-assessment/pilot/atc/`

**A — V1prep.** Interview-prep material, сам ограничивающий применимость историческими campaign details; не источник current requirements. citeturn6search9  
`https://v1prep.com/tap-air-portugal-pilot-interview-prep.html`

**A — PPRuNe historical TAP recruitment thread.** Старый candidate anecdote, полезный только для понимания того, какие формы assessment TAP применяла исторически; не evidence current format. citeturn0search8  
`https://www.pprune.org/interviews-jobs-sponsorship/293052-pilot-recruitment-tap.html`

Самые надёжные факты для ближайшей недели, таким образом, сводятся к четырём вещам: **официальный TAP regulation и calendar; фактический invitation; собственные licence/logbook/immigration documents; действующие EASA/EU rules.** Всё, что касается конкретного simulator scenario, question bank, psychometric package или скрытой nationality policy, остаётся неподтверждённым и не должно превращаться в «факт» только потому, что его повторяет assessment-prep сайт.

---

**Claude:**

{"lang":"ru","topic":"TAP Air Portugal: разбор отбора пилота OP23SET26 для инструктора с ~2500 ч","one_line":"Что реально требует и как устроен конкурс TAP OP23SET26 и как подготовить к нему инструктора Sevenair с ~2500 ч piston/IFR и российским паспортом за неделю до оценки.","key_findings":["OP23SET26 официально трёхфазный и все фазы элиминирующие: (1) ранжирование по баллам, (2) письменная аэронавигационная оценка (проходной порог 75%), психологическая и медицинская (APTO/NÃO APTO), (3) технический тест на симуляторе и финальное интервью жюри. Психологический провал даёт 12 месяцев до новой кандидатуры.","Публичные минимумы: ≥500 ч, действующие EASA CPL(A), Class 1 и ME-IR, завершённая ATPL theory, MCC, Advanced UPRT (снимается при наличии любого type rating), ICAO English ≥4, португальский и английский. Рейтинг на A320 ценится при ранжировании, но минимумом не является. Порога CEFR для португальского не опубликовано.","Лицензия EASA другого государства должна быть переведена в ANAC к OPC, для перевода IR должна оставаться действительной. CPL, IR, ME и Class 1 должны быть действительны на дедлайн подачи и до контракта. Помимо Class 1 есть отдельная медицинская оценка TAP/UCS.","Баллы за налёт: часы на «high performance and complexity» самолётах (примеры TAP: B737/A320/B767) ×0,003, остальные ×0,001. Если все ~2500 ч попадут в «прочие», это лишь 2,5 балла (условный расчёт, не оценка кандидата). Рейтинг A319/A320/A321 даёт 5/10/12 баллов, диплом по математике/физике 4, другая licenciatura 2, ICAO English 5/6 — 1/2 балла. Piston «complex» не стоит автоматически считать категорией ×0,003.","Публичного запрета TAP, EASA или ЕС на найм пилота только по российскому паспорту не найдено; EASA FAQ допускает обучение, лицензирование и медицину российских граждан для работы на нероссийских ВС (в т.ч. в авиакомпании ЕС). Но это не гарантия: отдельно проверяются право на работу и проживание в Португалии (AIMA), индивидуальные санкции (списочные, ~4600 лиц/организаций), enhanced background check по Reg. 2015/1998 и внутренние проверки TAP. Утверждение «авиакомпании ЕС не могут нанимать россиян» ложно из-за смешения гражданства, российских перевозчиков и персональных санкций.","Дата-противоречие: 5 ноября 2026 — четверг, пятница — 6 ноября. Официальный график TAP ставит Avaliação Aeronáutica в окно 2–6 ноября, определяющей считать дату в приглашении или портале кандидата. Также: окончательный первый список ~29 окт, старт процесса 30 окт, CIE I от 2 дек 2026.","Формат симулятора, тип, сценарии, банк вопросов и психометрика публично не раскрыты. Сторонние сайты (SET STANDARD, PilotAssessments, V1prep, PPRuNe 2007) — анекдотичны, групповое упражнение в официальной схеме отсутствует, переносить его как факт нельзя. Подготовка должна быть на базе IFR, производительности, погоды, аэродинамики высоких скоростей, энергии на jet, CRM, а не на заучивании процедур A320.","После отбора: интеграция и обучение A320 (тоже элиминирующее), трёхлетний минимальный срок службы с пропорциональным возмещением обучения, не менее €20 500 при добровольном уходе без just cause.","Сильные стороны профиля инструктора: суждение, мониторинг, IFR-дисциплина, вмешательство при ошибках. Риски: неизвестный turbine/jet опыт, режим «экзаменатора» вместо PF/PM, управление энергией на быстром самолёте. Для интервью рекомендуется 6 реальных STAR-историй на EN и PT (по ≤2 мин) с цепочкой threat→decision→debrief→lesson, честное признание границ знаний по типу.","Неизвестные в профиле кандидата (орган выдачи EASA лицензии, сроки CPL/ME-IR/Class 1, ATPL theory, MCC, UPRT/TR, jet/turbine часы, основание права на работу) нельзя заполнять догадками; первым шагом нужен документальный аудит с датами истечения."],"recommendations":["Сразу сверить дату оценки (чт 5 ноября или пт 6 ноября) по исходному приглашению или порталу кандидата, а не решать самостоятельно.","Сделать документальный аудит: орган выдачи лицензии, номера и сроки CPL/ME-IR/Class 1, ATPL theory, MCC, Advanced UPRT или type rating, ICAO English, статус проживания и права на работу; убедиться в готовности к переводу лицензии в ANAC.","Составить точную сводку лог-бука (TT/PIC/IFR/ME/FI/turbine/jet/multi-pilot/A320/12 и 24 мес.) вместо «около 2500 ч».","Подготовить дословный ответ о гражданстве и праве на работу на EN и PT с точным статусом, сроком и документом; не заявлять «я уже работаю в Португалии, проблем нет».","Строить 7-дневный план: 29.10 аудит и диагностический тест; 30.10 IFR/PBN/METAR; 31.10 производительность, аэродинамика, energy на jet; 1.11 погода и интегрированные сценарии; 2.11 шесть STAR-карточек EN/PT; 3.11 полный пробный тест (цель заметно выше 75%), интервью, симулятор; 4.11 облегчённый день и сон.","Не учить A320 по слухам и интернет-файлам; на симуляторе упор на scan, flight path, brief, нагрузку, энергию, CRM. Если есть действующий TR, готовиться по легальным утверждённым материалам (FCOM/FCTM/SOP).","Отрабатывать формулировки «не буду спекулировать», «следую SOP», «не эксплуатировал этот тип», вместо самодельных aircraft-specific memory items по windshear и upset.","На интервью не уходить в политику и защитные монологи; отвечать точно по документам и без попытки «обыграть» психологический тест."],"entities":{"people":[],"companies":["TAP Air Portugal","Sevenair","EASA","ANAC","AIMA","Совет ЕС","Европейская комиссия","SET STANDARD","PilotAssessments","V1prep","PPRuNe","Kiosque da Aviação","EmpregoEstagios","BeBee"],"products_tools":["TAP Regulamento do Concurso PNT OP23SET26","TAP Careers (recrutamento.tap.pt)","EASA Easy Access Rules for Aircrew","EASA Part-FCL / Part-MED","Commission Implementing Regulation (EU) 2015/1998","ECRIS-TCN","A320","STAR-метод","TEM (Threat and Error Management)","CRM","Advanced UPRT","MCC"]},"open_questions":["Какой орган выдал EASA лицензию кандидата и потребуется ли её перевод в ANAC; даты CPL/ME-IR/Class 1.","Есть ли у кандидата ATPL theory, MCC, Advanced UPRT или любой type rating.","Реальные turbine/jet/multi-pilot/A320 часы и в какую категорию (×0,003 или ×0,001) их отнесёт TAP.","Какое точное правовое основание права на работу и проживания в Португалии и срок его действия.","Реально ли оценка пройдёт 5 ноября (четверг) или 6 ноября (пятница) — нужно сверить с официальным приглашением.","Тип симулятора, сценарии, банк вопросов и формат психометрики — публично не раскрыты.","Как внутренняя комплаенс- и security-проверка TAP применяется к кандидатам с российским гражданством; индивидуальный санкционный статус кандидата не исследовался.","Не определено, какая именно оценка проходит 5 ноября в окне 2–6 ноября."],"related_concepts":["Отбор пилотов авиакомпаний","CRM и TEM","STAR-интервью","EASA Part-FCL и Part-MED","Санкции ЕС и трудоустройство граждан России","Право на работу граждан третьих стран в Португалии","Переход с piston на jet и энергоменеджмент","Advanced UPRT и MCC","Подготовка к симуляторной оценке","Верификация источников: официальные против коммерческих"]}
