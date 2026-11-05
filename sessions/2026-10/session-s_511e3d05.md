---
session: s_511e3d05
date: 2026-10-27
words: 2367
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-10-27 · You are distilling a DEEP-RESEARCH report into a compact, searchable knowledge note

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_511e3d05` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

You are distilling a DEEP-RESEARCH report into a compact, searchable knowledge note.
One report, possibly assembled from several AI vendors researching the SAME question.

DR-ID: DR26-10-26-HUB-03-1338
REGISTRY TOPIC: Как LLM думает на разных слоях, особенно глубоких: layerwise computation и causal interpretability (через dr_start; ПОТРЕБИТЕЛЬ: оператор: продолжение 11.10 и исправлений 18.10; карта слоев, четыре направления, четыре этапа и воспроизводимый план) (dr_reconcile 2026-10-27: на диске 1/6 ног, в реестре стояло 'running' — статус выправлен по факту. Тело ног: D:\Vault\Vault-Knowledge\_machine-bus\_dr\queue\DR26-10-26-HUB-03-1338\results)

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


===== VENDOR: report (DR26-10-26-HUB-03-1338.md) =====
---
id: DR26-10-26-HUB-03-1338
date: 2026-10-26 13:38:07
theme: Как LLM думает на разных слоях, особенно глубоких: layerwise computation и causal interpretability
session_id: s_49d19bcf
machine: HUB-01
targets: chatgpt,claudeai,gemini,grok,glm,mistral
---

# DR26-10-26-HUB-03-1338 — Как LLM думает на разных слоях, особенно глубоких: layerwise computation и causal interpretability

---
title: "Как LLM вычисляет ответ по слоям: recall и заказ Deep Research"
type: reference
stage: proposed
date_added: 2026-10-26
related: ["[[teach-2026-10-18-how-llm-thinks]]", "[[teach-2026-10-18-how-llm-thinks-corrections-v2]]", "[[2026-10-11-glubokoe-issledovanie-llm-6acaed4e]]"]
sources: ["https://chatgpt.com/c/s_eb0907a5", "https://notebooklm.google.com/notebook/s_00b1eb72"]
session_id: s_49d19bcf
corr_id: voice001:chat_REDACTED:t1793020565
---

Machine: HUB-01 (Хаб) · Agent: Codex · Operator: dev · 2026-10-26

# Recall: что уже изучали

Это пакет заказа исследования, не новый научный отчёт. Научные утверждения прежних материалов перечислены как предмет повторной проверки внешними исследователями.

| Дата | Прочитанный источник | Что переносим в новый заказ |
|---|---|---|
| 11.10.2026 | `01-Conversations/ChatGPT/conversations/2026-10-11-glubokoe-issledovanie-llm-6acaed4e.md` | Исходные вопросы оператора: что происходит на внутренних слоях, как наблюдать вычисления, связь данных и поведения, alignment и веса. Есть исходный разговор и развёрнутый ответ ChatGPT. |
| 18.10.2026 | `05-Resources/NotebookLM/_packets/teach-2026-10-18-how-llm-thinks.md` | Прежний обзор приборов: logit/tuned lens, probes, steering, SAE, circuit tracing, NLA, J-lens; практические входы TransformerLens, Gemma Scope, Neuronpedia. Исторические данные и токсичность сохраняются как контекст, не замещают тему слоёв. |
| 18.10.2026 | `05-Resources/NotebookLM/_packets/teach-2026-10-18-how-llm-thinks-corrections-v2.md` | Обязательные оговорки: веса/активации/CoT различаются; декодируемость не доказывает использование; SAE и графы неполны; вмешательства требуют контролей. В v1 были чрезмерные выводы о данных и токсичности. |
| 18–19.10.2026 | `05-Resources/NotebookLM/_teach-curriculum.md:490–508` | Зафиксированы RU/EN v2 и один существующий блокнот. Техническая приёмка аудио не равна полной научной проверке или независимому прослушиванию. Повторный заказ 19.10 обнаружил дубликат и переиспользовал материал. |
| 19.10.2026 | `teach-2026-10-19-llm-serving-memory.md`, реестр DR26-10-19-HUB-05-2154 | Соседняя тема: многопользовательский сервис, KV-cache, история и фильтры. В строке реестра указана одна нога Grok; это не кворум исследования внутренних слоёв. |

Проверены память узла, RAG, FTS сессий, пакеты NotebookLM, исходник ChatGPT и реестр. RAG ответил, но релевантные точные источники найдены локальным поиском. Поверхности RAG частично скрыты SECRET-GATE; у свежих jsonl неполное покрытие. FTS показал точные сессии s_9ca616ff, s_5ddb4242 и s_259cdbaa. Полнота всей истории всех устройств не доказана.

Важный пробел прежнего пакета: обзор приборов уже есть, но нужна доказательная карта вычислений по глубине, отдельно ранние, средние, поздние слои и шаги генерации. Нужен новый многовендорный заказ по этому пробелу с проверкой прежних выводов.

# Исследовательское задание для внешних LLM

Conduct a deep research investigation. Research cutoff: actual execution date; state that date. Do not ask clarifying questions. Produce the research in English, with a short Russian executive summary and glossary. Search primary papers, official research pages, model cards, repositories and documented replications. This is a scientific investigation, not a market comparison.

TOPIC: How transformer LLMs compute across layers, especially deep/internal and late layers; what can be observed, causally established and reproduced.

OBJECTIVE: Continue an existing October 11 investigation and October 18 teaching package. Explain the computation clearly for an engineer, distinguish demonstrated mechanisms from metaphors, and specify a small reproducible open-model experiment. Do not treat supplied prior claims as verified evidence.

PRIOR WORK TO RECHECK: An earlier overview covered logit/tuned lens, probes, steering, sparse autoencoders, activation patching/ablation, attribution graphs/circuit tracing, Natural Language Autoencoders and J-space/J-lens. It separated weights, transient activations and generated chain-of-thought. A correction required causal interventions, random-direction and unrelated-position controls, and held-out paraphrases. It warned that intermediate decoding is not a literal inner monologue, feature activation is not intention, reconstruction is incomplete, and ordinary closed chat APIs do not provide arbitrary internal tensors. Preserve these distinctions, update or overturn them with sources.

Previous ancillary questions concerned toxic training data, alignment and historical corpora. Retain them only where they explain layerwise mechanisms. Do not let corpus history or multi-user serving displace the main topic. The prior package's claim that all post-2000 text exceeds all earlier text was explicitly marked not established; do not repeat it as fact. Toxic-data findings were conditional experiments, not a universal safety prescription.

FOUR REQUIRED RESEARCH DIRECTIONS. Each vendor investigates ALL FOUR independently so agreement can be compared:

1. LAYERWISE COMPUTATION. Trace one token through embeddings, residual stream, attention, MLP and unembedding/logits. Compare empirical roles of early, middle and late blocks for lexical, syntactic, semantic, factual, relational and answer-preparation information. Distinguish absolute layer index from normalized depth. Explain what changes across token positions and repeated generation steps. Avoid a universal staircase unless demonstrated across architectures, models and tasks. Distinguish architectural depth, hidden representations, reasoning-token time, recurrence and test-time compute. Ask whether late layers refine, suppress, route, calibrate or compose rather than simply becoming more abstract.

2. OBSERVABILITY AND CAUSALITY. Compare logit/tuned lens, probes, attention maps, SAE/transcoders, circuit tracing, NLA and J-lens. For each: required access, measured object, layer/token granularity, assumptions, trained decoder, reconstruction/coverage errors, artifacts, controls, reproducible code and known failures. Separate decodability, correlation, necessity, sufficiency and causal mediation. Compare patching, ablation and steering; address off-manifold interventions, redundant mechanisms and probe leakage. Explain when causal claims survive held-out tasks and model variants.

3. DEEP REPRESENTATIONS AND BEHAVIOR. Investigate multi-hop inference, planning, numerical reasoning, latent representations, multilingual concepts, uncertainty, truthfulness, refusal and alignment. What evidence places these mechanisms in particular layers or distributed circuits? Can base/instruct/posttraining comparisons locate changes? How does CoT relate to internal computation, and when is it unfaithful? Recheck claims about hidden intentions, situational awareness, introspection, evaluation awareness and toxic persona features with explicit alternative explanations. Neither assume consciousness nor dismiss it by rhetoric; state what the experiments can and cannot establish.

4. REPRODUCIBILITY AND TRANSFER. Compare findings across at least two open model families and base/instruct variants where evidence exists; label unavailable comparisons. Describe access limits for closed models without inferring internals from prose. Propose an experiment on a small supported open model: two prompt conditions, per-layer measurements, logit difference and behavioral metrics, intervention positions, matched-norm random controls, held-out paraphrases, seed handling and uncertainty. Report prerequisites, supported versions and estimated RAM/VRAM separately from measured use. Give a CPU-friendly fallback and a browser demonstration if feasible. No installation, training, paid API or execution is requested in this order.

FOUR REQUIRED STAGED OUTPUTS (stages are distinct from vendor rails):

Release 1: prior-work audit and evidence map. List what the prior package established, overclaimed, left open or needs updating. Create a source-to-question matrix and explicit search-coverage limits.

Release 2: layer-by-layer explanatory atlas, with a worked token example, distinctions between layer depth and reasoning steps, diagrams and a model/task comparison table. Label proposed examples as illustrative.

Release 3: adversarial review of deep-layer claims and measurement tools. Preserve contradictory findings, methodological confounds, null results and strongest counterarguments. Give an evidence-strength table.

Release 4: reproducibility protocol and decision memo. Provide one smallest useful experiment, acceptance/falsification criteria, constraints, open questions and next research steps. This is a proposal, never claim that our experiment was run.

OUTPUT FORMAT: A. Executive summary; B. Four staged outputs; C. Key findings with evidence strength; D. Contradictions and debates; E. Best practices and failure modes; F. Reproducibility protocol; G. Action plan; H. Sources. Include a glossary and a compact matrix: claim | model/version | depth/layer | token/task | method | intervention/control | observed effect | uncertainty | source/date | replication status.

Candidate primary leads to verify, not endorsements: transformer-circuits.pub; anthropic.com research on circuit tracing, natural-language-autoencoders and global-workspace; OpenAI persona-feature research; Google DeepMind Gemma Scope; TransformerLens and circuit-tracer official repositories; original tuned-lens and activation-patching papers. Verify existence, exact publication date, method and claimed result, including any 2026 material. Prefer the original experiment over retellings.

MINIMUM ACCEPTANCE: four substantive directions, four staged outputs, linked primary evidence for every major claim, explicit limitations, and a proposed falsifiable experiment. A plan, an echoed prompt or a list of citations without findings is not a research report.

# Исполнение и приёмка

Заказать один общий веер на шесть браузерных рельс: ChatGPT Deep Research, Claude.ai Research, Gemini Deep Research, Grok, GLM, Mistral. Минимум четыре независимых вендора с полными отчётами; два аккаунта одного вендора считаются одной рельсой. Codex собирает recall и заказ, но не является исследовательской ногой.

К общему телу добавляется универсальный §1 и отдельный платформенный блок из `08-Templates/dr-platform-playbook.md`. UI-режимы выбираются по живому интерфейсу и текущей поправке /dr-fanout от 26.10. Модель из текста промпта не является доказательством настройки режима.

Состояния различаются: prepared → queued → submitted → researching → report retrieved → gate passed → cross-vendor synthesis. Реестр running не доказывает фактического старта браузера. Для каждой ноги нужны URL беседы, наблюдаемый режим, дата, readback отправленного текста и наблюдаемый статус. Полный отчёт проходит `dr_leg_gate.py --strict --prompt <manifest> <report>` до зачёта.

Независимый ревьюер этого пакета: Claude, session s_0ed0fd2d. Адресный PROPOSE отправлен как tonyssd:1992658; в ограниченном окне ответа по точному corr_id не было. До содержательного ответа статус NO_QUORUM / SELF_DECISION, не консенсус. Лизы и независимое ревью сохраняются.

рельса: Codex subscription для recall/подготовки; исследования только в браузерных подписках внешних вендоров. Новое аудио не заказывается этим пакетом.

---

**Claude:**

{"lang":"mixed","topic":"Layerwise computation и causal interpretability LLM: заказ Deep Research и recall","one_line":"Пакет заказа (не научный отчёт) на многовендорное исследование того, как transformer LLM вычисляют ответ по слоям, что наблюдаемо, что доказано причинно и как воспроизвести на малой открытой модели.","key_findings":["Документ является пакетом заказа и recall, а не новым научным отчётом: научных результатов по слоям в нём нет, прежние утверждения перечислены как предмет повторной проверки внешними исследователями.","Прежние материалы (11.10 и 18.10.2026) покрывали приборы: logit/tuned lens, probes, steering, SAE, activation patching/ablation, attribution graphs/circuit tracing, NLA, J-space/J-lens; практические входы TransformerLens, Gemma Scope, Neuronpedia.","Прежние оговорки v2 (18.10): веса, активации и CoT различаются; декодируемость не доказывает использование; SAE и графы неполны; вмешательства требуют контролей (случайные направления, нерелевантные позиции, held-out перефразы); промежуточное декодирование не внутренний монолог; активация признака не намерение; обычные закрытые чат-API не дают произвольных тензоров.","Выявленный пробел: обзор приборов есть, но нет доказательной карты вычислений по глубине (ранние, средние, поздние слои и шаги генерации); отсюда новый заказ по четырём направлениям: layerwise computation, observability и causality, deep representations и поведение, reproducibility и transfer.","Утверждение прежнего пакета, что весь текст после 2000 года превышает весь более ранний, помечено как не установленное и не должно повторяться как факт; выводы о токсичных данных были условными экспериментами, не универсальной рекомендацией.","Задание требует различать абсолютный индекс слоя и нормализованную глубину, архитектурную глубину и время рассуждения (reasoning tokens, recurrence, test-time compute), и не принимать универсальную «лестницу абстракции» без доказательства на разных архитектурах, моделях и задачах; позднюю роль слоёв проверять как refine, suppress, route, calibrate или compose.","Приёмка: четыре этапа (аудит прежней работы и карта доказательств; атлас по слоям с примером токена; адверсариальный обзор с таблицей силы доказательств; протокол воспроизведения и decision memo) и матрица claim | model | layer | task | method | control | effect | uncertainty | source | replication status.","Проверка покрытия слабая: RAG частично скрыт SECRET-GATE, у свежих jsonl неполное покрытие, полнота истории всех устройств не доказана; на диске найдена 1 нога из 6, статус реестра выправлен по факту (dr_reconcile 2026-10-27); независимое ревью Claude не ответило, статус NO_QUORUM / SELF_DECISION."],"recommendations":["Запустить один общий веер на шесть браузерных рельс (ChatGPT DR, Claude.ai Research, Gemini DR, Grok, GLM, Mistral) с минимумом четырёх независимых вендоров; два аккаунта одного вендора считаются одной рельсой; Codex не исследовательская нога.","Для каждой ноги фиксировать URL беседы, наблюдаемый режим UI, дату, readback отправленного текста и статус; полный отчёт пропускать через dr_leg_gate.py --strict --prompt <manifest> до зачёта; реестр running не считать доказательством старта.","Прежние выводы не считать верифицированными: сверять с первоисточниками (transformer-circuits.pub, Anthropic по circuit tracing, NLA и global-workspace, OpenAI persona features, Gemma Scope, репозитории TransformerLens и circuit-tracer, оригинальные работы tuned lens и activation patching), проверять существование, точную дату и метод, включая материалы 2026 года.","Спроектировать минимальный воспроизводимый эксперимент на малой поддерживаемой открытой модели: два условия промпта, измерения по слоям, logit difference и поведенческие метрики, позиции вмешательства, matched-norm случайные контроли, held-out перефразы, обработка seed и неопределённости; отдельно оценка и измеренное потребление RAM/VRAM, CPU-фолбэк и браузерная демонстрация при возможности; запуск и установка в этом заказе не требуются, нельзя заявлять, что эксперимент выполнен.","Сравнивать результаты минимум на двух открытых семействах и base/instruct вариантах, недоступные сравнения помечать, о внутренностях закрытых моделей не судить по их прозе.","Сохранять противоречащие находки, нулевые результаты и методологические confounds; различать декодируемость, корреляцию, необходимость, достаточность и каузальную медиацию.","Соседние темы (токсичные данные, исторические корпуса, multi-user serving и KV-cache из DR26-10-19-HUB-05-2154) удерживать только там, где они объясняют послойные механизмы."],"entities":{"people":["оператор"],"companies":["Anthropic","OpenAI","Google DeepMind","ChatGPT","Claude.ai","Gemini","Grok","GLM","Mistral","Codex","NotebookLM"],"products_tools":["TransformerLens","circuit-tracer","Gemma Scope","Neuronpedia","logit lens","tuned lens","sparse autoencoders","transcoders","activation patching","attribution graphs","Natural Language Autoencoders","J-lens","dr_leg_gate.py","dr_start","dr_reconcile","RAG","SECRET-GATE","brain_ask.py"]},"open_questions":["Есть ли доказанная универсальная картина ролей ранних, средних и поздних слоёв (лексика, синтаксис, семантика, факты, подготовка ответа) для разных архитектур, моделей и задач, в нормализованной глубине?","Поздние слои уточняют, подавляют, маршрутизируют, калибруют или композируют, а не просто становятся «абстрактнее»?","Какие причинные утверждения (patching, ablation, steering) выживают на held-out задачах и вариантах моделей с учётом off-manifold вмешательств, избыточных механизмов и утечки в пробах?","Насколько CoT соответствует внутреннему вычислению и когда он неверен (unfaithful)?","Что экспериментально можно и нельзя установить про скрытые намерения, situational awareness, интроспекцию, evaluation awareness и токсичные persona-признаки при явных альтернативных объяснениях?","Локализуются ли изменения post-training при сравнении base и instruct моделей по слоям?","Подтверждены ли и существуют ли заявленные материалы 2026 года (NLA, global-workspace, J-lens) с точными датами и методами?","Достигнут ли кворум: на диске 1 нога из 6, независимое ревью отсутствует, полнота recall по всем устройствам не доказана."],"related_concepts":["layerwise computation","residual stream","logit lens и tuned lens","activation patching и causal mediation","sparse autoencoders и transcoders","circuit tracing и attribution graphs","steering vectors","chain-of-thought faithfulness","persona features и alignment","мультиязычные концепты","multi-hop reasoning","воспроизводимость интерпретируемости","Deep Research кворум и dr_fanout","KV-cache и serving"]}
