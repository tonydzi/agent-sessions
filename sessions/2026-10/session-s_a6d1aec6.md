---
session: s_a6d1aec6
date: 2026-10-21
words: 1195
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-10-21 · You are distilling a DEEP-RESEARCH report into a compact, searchable knowledge note

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_a6d1aec6` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

You are distilling a DEEP-RESEARCH report into a compact, searchable knowledge note.
One report, possibly assembled from several AI vendors researching the SAME question.

DR-ID: DR26-10-19-HUB-05-2154
REGISTRY TOPIC: Как LLM-сервис обслуживает тысячи пользователей параллельно, держит вредные запросы и хранит историю/контекст (подкаст как LLM думает, эпизод 2) (через dr_start; ПОТРЕБИТЕЛЬ: Фактчек пакета подкаста teach-2026-10-19-llm-serving-memory (эпизод 2 серии how-llm-thinks): исправленная v2 эпизода, если ДР опровергнет факты пакета) (dr_reconcile 2026-10-21: на диске 1/6 ног, в реестре стояло 'running' — статус выправлен по факту. Тело ног: D:\Vault\Vault-Knowledge\_machine-bus\_dr\queue\DR26-10-19-HUB-05-2154\results)

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


===== VENDOR: report (DR26-10-19-HUB-05-2154.md) =====
---
id: DR26-10-19-HUB-05-2154
date: 2026-10-19 21:54:34
theme: Как LLM-сервис обслуживает тысячи пользователей параллельно, держит вредные запросы и хранит историю/контекст (подкаст как LLM думает, эпизод 2)
session_id: H54856
machine: HUB-01
targets: chatgpt,gemini,grok,claudeai,glm,mistral
---

# DR26-10-19-HUB-05-2154 — Как LLM-сервис обслуживает тысячи пользователей параллельно, держит вредные запросы и хранит историю/контекст (подкаст как LLM думает, эпизод 2)

Deep research, answer in Russian, cite primary sources (papers, official docs, engineering blogs) with URLs for every factual claim; mark estimates as estimates; say explicitly where sources disagree.

Topic: How a production LLM service (ChatGPT, Claude, Gemini, open-source stacks like vLLM/SGLang/TensorRT-LLM) serves thousands of users in parallel from one set of weights, how it resists harmful requests, and how conversation memory/context actually works. Audience: a software engineer (Python/C++, PhD) new to LLM infrastructure.

Questions:
1. One copy of weights, many users: are weights shared read-only across requests? How do continuous batching (Orca, OSDI 2022), PagedAttention / vLLM (SOSP 2023), prefill vs decode, chunked prefill, disaggregated prefill/decode, tensor/pipeline/expert parallelism, speculative decoding work? Concrete numbers: GPU memory per token of KV cache for a known open model, typical batch sizes, throughput gains reported in the papers.
2. Isolation: can one user's request "break" or contaminate the model for others? Weights are frozen at inference; per-request state is KV cache. Known real incidents of cross-user leakage (e.g. ChatGPT March 2023 Redis bug), prompt-cache timing side channels (papers 2024-2025), batch non-determinism (Thinking Machines "Defeating Nondeterminism in LLM Inference", 2025).
3. Harmful requests: layers of defence: pretraining data filtering, RLHF/Constitutional AI, refusal direction (Arditi et al. 2024), input/output classifiers (Anthropic Constitutional Classifiers 2025, Llama Guard, OpenAI moderation), rate limits and abuse monitoring, ASL-3 deployment measures. What is known about jailbreak success rates before/after classifiers.
4. Memory: are chat APIs stateless (client resends entire message list each turn)? Compare: OpenAI Chat Completions vs Responses API (previous_response_id, store), Anthropic Messages API, Gemini. How do ChatGPT/Claude apps store history server-side; "memory" features (ChatGPT Memory, Claude memory/projects) as retrieval/injection into context, not weight updates.
5. Context: context window limits (current sizes of frontier models, Oct 2026), cost of attention (quadratic) vs KV-cache linear memory, prompt caching (Anthropic, OpenAI, Gemini): prices/discounts and TTLs, "lost in the middle" (Liu et al. 2023) and context rot research, compaction/summarization of long chats, RAG.
6. Correct common misconceptions: "the model learns from my chat in real time", "each user gets their own model", "the model remembers yesterday's conversation by itself".
Deliver: structured report, numbers table with sources, list of 20+ live primary URLs.

---

**Claude:**

{"lang":"ru","topic":"Как LLM-сервис обслуживает много пользователей, фильтрует вредные запросы и хранит контекст","one_line":"Исследование должно было ответить, как продакшн-LLM-сервис обслуживает тысячи пользователей на одних весах, защищается от вредных запросов и устроен ли контекст и память чата. В файле лежит только постановка задачи, ответов вендоров в нём нет.","key_findings":["Файл отчёта содержит только бриф: 6 вопросов, аудиторию (инженер Python/C++ с PhD, новичок в LLM-инфраструктуре) и формат поставки (структурированный отчёт, таблица чисел с источниками, 20+ живых первичных URL). Ответов вендоров, чисел и выводов в тексте нет.","Бриф намечает вопрос 1: общие веса только для чтения у всех запросов; continuous batching (Orca, OSDI 2022); PagedAttention/vLLM (SOSP 2023); prefill против decode; chunked prefill; disaggregated prefill/decode; tensor, pipeline и expert parallelism; speculative decoding; память KV-кэша на токен для известной открытой модели. Это вопросы, а не результаты.","Вопрос 2 про изоляцию (в брифе это рабочая рамка, не вывод): веса при инференсе заморожены, состояние запроса живёт в KV-кэше. Предлагается проверить инцидент ChatGPT в марте 2023 (баг Redis), тайминговые побочные каналы prompt-кэша (работы 2024-2025) и недетерминизм батчей (Thinking Machines, 2025).","Вопрос 3 про защиту: предложены слои претрейн-фильтрация, RLHF/Constitutional AI, refusal direction (Arditi et al. 2024), классификаторы входа и выхода (Anthropic Constitutional Classifiers 2025, Llama Guard, OpenAI moderation), rate limits, мониторинг злоупотреблений, меры ASL-3. Успех джейлбрейков до и после классификаторов в тексте не приведён.","Вопросы 4-5 про память и контекст: сравнить stateless-API (OpenAI Chat Completions, Responses API с previous_response_id и store, Anthropic Messages, Gemini); память ChatGPT и Claude как поиск и вставка в контекст, а не обновление весов; размеры окон на октябрь 2026; квадратичная стоимость внимания против линейного KV-кэша; цены и TTL prompt-кэширования; lost in the middle (Liu et al. 2023); context rot; compaction и RAG. Ответов нет.","Вопрос 6 про заблуждения, которые надо опровергнуть или подтвердить: «модель учится на моём чате в реальном времени», «у каждого пользователя своя модель», «модель сама помнит вчерашний разговор». Вердиктов в тексте нет.","По метаданным реестра на диске лежит 1 из 6 ног ДР (targets: chatgpt, gemini, grok, claudeai, glm, mistral), статус выправлен с 'running' по факту. Кворум 4/6 не набран, поэтому фактчек пакета подкаста этим отчётом не закрыт."],"recommendations":["Не использовать этот файл как источник фактов для фактчека пакета teach-2026-10-19-llm-serving-memory: в нём нет утверждений, которыми можно опровергать или подтверждать пакет.","Взять тела недостающих ног из D:\\Vault\\Vault-Knowledge\\_machine-bus\\_dr\\queue\\DR26-10-19-HUB-05-2154\\results, а при пустоте перезапустить упавшие рельсы и добрать кворум 4/6 по протоколу ДР.","После получения ответов сверить обязательные пункты брифа: числовая таблица с источниками, 20+ живых первичных URL, пометка оценок, явное указание расхождений между источниками.","До завершения ДР оставить эпизод 2 в текущей редакции и не выпускать исправленную v2."],"entities":{"people":["Arditi","Liu"],"companies":["OpenAI","Anthropic","Google","Thinking Machines"],"products_tools":["ChatGPT","Claude","Gemini","vLLM","SGLang","TensorRT-LLM","Orca","PagedAttention","Llama Guard","OpenAI moderation","Constitutional Classifiers","Responses API","Chat Completions API","Anthropic Messages API","Redis","ChatGPT Memory","Claude projects"]},"open_questions":["Какие реальные данные дали вендоры? В файле только бриф, а тела ног лежат отдельно и на диске есть 1 из 6.","Сколько памяти KV-кэша на токен у конкретной открытой модели и какие приросты пропускной способности заявлены в статьях Orca и vLLM? Не проверено.","Какова доля успешных джейлбрейков до и после классификаторов (Constitutional Classifiers 2025)? Не проверено.","Каковы размеры контекстных окон и цены и TTL prompt-кэширования у Anthropic, OpenAI и Gemini на октябрь 2026? Не проверено.","Как именно устроены серверное хранение истории и функции памяти в приложениях ChatGPT и Claude? Не проверено.","Опровергает ли ДР факты пакета подкаста и нужна ли исправленная v2? Ответ ждёт получения содержательных ног."],"related_concepts":["continuous batching","PagedAttention / KV-кэш","prefill и decode","speculative decoding","prompt caching","изоляция запросов и побочные каналы","недетерминизм батчей","Constitutional Classifiers / refusal direction","stateless chat API","память чата как RAG-инъекция","context rot / lost in the middle","подкаст how-llm-thinks","кворум ДР 4/6"]}
