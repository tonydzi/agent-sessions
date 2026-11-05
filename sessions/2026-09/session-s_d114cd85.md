---
session: s_d114cd85
date: 2026-09-23
words: 2148
turns: 3
tools: "Bash, Read"
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-23 · You are distilling a DEEP-RESEARCH report into a compact, searchable knowledge note

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_d114cd85` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

You are distilling a DEEP-RESEARCH report into a compact, searchable knowledge note.
One report, possibly assembled from several AI vendors researching the SAME question.

DR-ID: DR26-09-22-HUB-02-1159
REGISTRY TOPIC: Мульти-агентная работа в ОДНОЙ папке: кто в мире уже связал Claude Code и Codex локами/протоколом — что забрать, где мы впереди, куда положить наше (через dr_start; ПОТРЕБИТЕЛЬ: контракт PACT-PARITY-20260922 + публикация нашего протокола координации агентов (цель №2)) (dr_reconcile 2026-09-23: на диске 4/6 ног, в реестре стояло 'running' — статус выправлен по факту. Тело ног: D:\Vault\Vault-Knowledge\_machine-bus\_dr\queue\DR26-09-22-HUB-02-1159\results)

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


===== VENDOR: report (DR26-09-22-HUB-02-1159.md) =====
---
id: DR26-09-22-HUB-02-1159
date: 2026-09-22 11:59:56
theme: Мульти-агентная работа в ОДНОЙ папке: кто в мире уже связал Claude Code и Codex локами/протоколом — что забрать, где мы впереди, куда положить наше
session_id: unknown
machine: HUB-01
targets: chatgpt,gemini,grok,claudeai,glm,mistral
---

# DR26-09-22-HUB-02-1159 — Мульти-агентная работа в ОДНОЙ папке: кто в мире уже связал Claude Code и Codex локами/протоколом — что забрать, где мы впереди, куда положить наше

Тема: два и более автономных кодинг-агента (Claude Code, OpenAI Codex / codex-cli, Cursor Agent,
Aider, Devin, Gemini CLI, Amp, OpenHands, Goose и прочие) работают ОДНОВРЕМЕННО в ОДНОЙ рабочей
папке / одном чекауте репозитория — не в отдельных worktree и не по очереди, а параллельно,
с общим диском и общим состоянием.

Нужен максимально конкретный, проверяемый обзор. Три равные по важности половины — отвечай
на все три, не сваливайся только в первую.

=== ПОЛОВИНА 1. ЧТО В МИРЕ УЖЕ СДЕЛАНО ===

1. GitHub: назови поимённо репозитории, где это реализовано кодом, а не соглашением в промпте.
   Интересуют категории:
   - файловые/адвизорные блокировки между агентами (lock-файлы, lease с TTL, SQLite/Redis-мьютекс,
     flock/fcntl, .lock-протоколы);
   - «один вопрос — один исполнитель» (семантическая, а не файловая блокировка);
   - оркестраторы мульти-агентов с общим диском (agent-to-agent bus, mailbox, message envelope,
     handoff-протокол между РАЗНЫМИ вендорами — именно Claude×Codex, а не N инстансов одного);
   - MCP-серверы, целиком посвящённые координации/локам между агентами;
   - обёртки, которые делают git worktree-изоляцию автоматической (это альтернативный подход —
     назови, чем он на практике хуже/лучше общей папки).
   По каждому репозиторию: ссылка, звёзды, дата последнего коммита, жив ли, ЧТО именно
   реализовано, и какой у него механизм (одной фразой).

2. Форумы и дискуссии, где это обсуждали практики (не маркетинг):
   Hacker News, Reddit (r/ClaudeAI, r/ChatGPTCoding, r/LocalLLaMA, r/ExperiencedDevs),
   GitHub Issues/Discussions самих anthropics/claude-code и openai/codex, Lobsters, dev.to,
   X/Twitter-треды инженеров, личные блоги. Ищи описания РЕАЛЬНЫХ коллизий: два агента
   переписали один файл, потеряли правку, зациклились, испортили git-историю, подрались за
   один порт/БД. Дай ссылки, даты, имена авторов и СУТЬ того, что они выяснили.

3. Официальная позиция вендоров: что Anthropic и OpenAI пишут в документации про параллельный
   запуск нескольких агентов в одном каталоге; есть ли явные предупреждения, есть ли
   встроенные механизмы (например, какие-либо hooks/permissions/locks), и есть ли открытые
   issue с просьбой такое добавить.

4. Ноу-хау, которое стоит забрать: перечисли конкретные приёмы с оценкой «дёшево/дорого внедрить»
   и «что именно чинит». Приоритет — приёмы, которые ловят СЕМАНТИЧЕСКИЙ конфликт (двое взяли
   РАЗНЫЕ файлы одной задачи), а не только физическую запись в один файл. Отдельно: как они
   решают проблему, что агент-победитель должен УЗНАТЬ, что проиграл, и что делать проигравшему.

=== ПОЛОВИНА 2. ГДЕ МЫ ВПЕРЕДИ (честная сверка, не комплимент) ===

Вот что уже построено у нас (Palo Alto AI Research Lab). Скажи по КАЖДОМУ пункту: это
уже существует в мире (тогда где именно, ссылка), это существует в более слабом виде, или
этого действительно нет и мы впереди. Где мы наивны или изобретаем велосипед — скажи прямо.

  A. Роли implementer/reviewer назначаются по АРТЕФАКТУ, а не по вендору: один и тот же агент
     в одном файле автор, в другом ревьюер. Себя никто не ревьюит.
  B. Трёхуровневая иерархия захвата: сначала claim на ВОПРОС (стабильный question_id, одна
     эпоха), затем lease на ТОЧНЫЙ ФАЙЛ вывода, и только сверху advisory-видимость «кто что
     делает». Смысл: физический лок не ловит конфликт, когда двое взяли разные файлы одной
     задачи.
  C. Смена пишущего только после явного release/close и нового конверта; ревьюер не правит
     ветку автора.
  D. Один физический источник инструкций/скиллов для ОБОИХ агентов, смонтированный junction'ом,
     а не скопированный — чтобы копии не разошлись молча.
  E. Авторитет — локальная SQLite на узле с BEGIN IMMEDIATE, кооперативная; межмашинная
     эксклюзия честно объявлена ОТСУТСТВУЮЩЕЙ, а не выдана за существующую.
  F. Отправитель сообщения между агентами обязан fail-closed проверить глагол конверта ДО
     выдачи транспортной квитанции, причём список допустимых глаголов НЕ копируется, а читается
     из исходника приёмника статическим разбором. Причина: класс дефекта «OK при недоставке» —
     транспорт выдал зелёную квитанцию, а потребитель сообщение не принял, и сутки переписки
     шли мимо.
  G. Lease по умолчанию на ТОЧНЫЙ ФАЙЛ; лок на папку — только явным opt-in с причиной, TTL и
     видимым scope. Причина: захват папки блокировал посторонние файлы на десятки минут.

  Отдельно оцени: есть ли в мире аналог пункта F (гейт на ОТПРАВКЕ, читающий контракт
  приёмника) — это, по нашей гипотезе, самое редкое, и хотелось бы знать, кто ещё так делает.

=== ПОЛОВИНА 3. КУДА И КОМУ ЭТО ПОЛОЖИТЬ ===

Если предположить, что перечисленное во второй половине оформлено как открытый артефакт
(спецификация протокола + референсная реализация на Python + тесты), то:

  1. Куда положить, чтобы это НАШЛИ: какие конкретные репозитории/списки/каталоги реально
     читают люди, решающие эту задачу — awesome-списки, реестры MCP-серверов, каталоги
     агентных протоколов, конференции/CFP, arXiv-категории, Zenodo/DOI, Show HN, конкретные
     сабреддиты. Назови ИМЕНА и требования к заявке у каждого.
  2. Кому написать ПОИМЁННО: авторы и мейнтейнеры проектов из половины 1, у которых эта
     проблема открыта — кто ведёт релевантные issue, кто жаловался на коллизию в треде.
     Дай ссылку на конкретный тред/issue, где сообщение будет уместным, а не спамом.
     Отдельно отметь треды, которые ЖИВЫ (комментарии за последние 2-4 недели).
  3. Какие существующие протоколы/стандарты уже застолбили это место (MCP, A2A, ACP,
     agent-protocol и т.п.) — с чем наш подход обязан состыковаться или чему он противоречит,
     чтобы не выпустить заведомо несовместимую вещь.
  4. Формат, который в этой нише реально заходит: спека? MCP-сервер? плагин к claude-code?
     статья с бенчмарком? Приведи примеры того, что за последний год в этой теме получило
     заметный отклик, и что провалилось.

=== ТРЕБОВАНИЯ К ОТВЕТУ ===

Думай максимально глубоко и долго, включи самый сильный доступный в этом аккаунте режим
рассуждения. Ответ нужен максимально качественный, подробный и продуманный: с источниками,
датами, оценкой уверенности и явным указанием, где данных не хватает.

- Каждое утверждение — со ссылкой и датой. Без ссылки помечай «не проверено».
- ⛔ Не выдумывай репозитории и имена. Если нашёл мало — так и скажи: «нашёл N, вот они»,
  а не добирай правдоподобным. Пустой результат по разделу — валидный ответ.
- Отличай РЕАЛИЗОВАННОЕ КОДОМ от НАПИСАННОГО В README и от соглашения в промпте (AGENTS.md,
  CLAUDE.md «договоритесь между собой») — это три разных уровня зрелости, помечай каждый.
- Отдельной строкой в конце: что из найденного ты считаешь САМЫМ ценным для заимствования
  и почему, одной фразой.

---

**Claude:**

05:53, 23 сентября 2026.

---

> `Bash` -- {"command": "cat \"D:\\Vault\\Vault-Knowledge\\_machine-bus\\_dr\\queue\\DR26-09-22-HUB-02-1159\\results\"/*.md 2>/dev/null | head -5; ls \"D:\\Vault\\Vault-Knowledge\\_machine-bus\\_dr\\queue\\DR26-09-22-HUB-02-1159\\results\" 2>/dev/null"}

---

> `Bash` -- {"command": "cd \"D:\\Vault\\Vault-Knowledge\\_machine-bus\\_dr\\queue\\DR26-09-22-HUB-02-1159\\results\" && for f in *.md; do echo \"=== $f ($(wc -c < \"$f\") bytes) ===\"; done"}

---

> `Read` -- {"file_path": "D:\\Vault\\Vault-Knowledge\\_machine-bus\\_dr\\queue\\DR26-09-22-HUB-02-1159\\results\\chatgpt.md"}

---

> `Read` -- {"file_path": "D:\\Vault\\Vault-Knowledge\\_machine-bus\\_dr\\queue\\DR26-09-22-HUB-02-1159\\results\\claudeai.md"}

---

> `Read` -- {"file_path": "D:\\Vault\\Vault-Knowledge\\_machine-bus\\_dr\\queue\\DR26-09-22-HUB-02-1159\\results\\glm.md"}

---

> `Read` -- {"file_path": "D:\\Vault\\Vault-Knowledge\\_machine-bus\\_dr\\queue\\DR26-09-22-HUB-02-1159\\results\\grok.md"}

---

**Claude:**

```json
{
  "lang": "ru",
  "topic": "Мульти-агентная координация в одной папке: Claude×Codex локи/протоколы в мире vs наш протокол",
  "one_line": "Три LLM-вендора (ChatGPT, Claude.ai, Grok; GLM упал на капче) сверили, кто в мире уже связал Claude Code и Codex локами/протоколом в общей рабочей папке, честно оценили 7 пунктов нашего координационного протокола (implementer/reviewer по артефакту, claim→lease→visibility, junction-скиллы, SQLite-authority, fail-closed send-гейт, file-lease-по-умолчанию) против найденного, и наметили, куда и кому выложить это как открытый артефакт.",
  "key_findings": [
    "Найдено ~15-20 GitHub-репо с реальным кодом координации (не промпт-соглашением): mcp_agent_mail лидирует (2153⭐, пуш 21-22.09.2026, автоинсталлер под все CLI-агентов сразу); почти все остальные — 0-11⭐, созданы июль-сентябрь 2026. Только OpenMOSS/claude-codex-handoff и ещё 2-3 репо явно называют пару именно Claude×Codex, а не N копий одного вендора.",
    "Академическое исследование по 33 596 PR от AI-агентов в 2807 репо (arXiv 2607.04697) показало: конфликт между PR разных вендоров — 41.7% против 19.8% у одного вендора, но кросс-вендорная параллельная активность — всего 0.5% случаев (122 из 2807 репо). Межвендорная коллизия редкая, но злее.",
    "AgentRoom (arXiv 2608.23740, 24.08.2026) — ближайший академический аналог: CRDT-слияние конкурентных правок + MCP file-claim с формальным доказательством взаимного исключения; протестирован на реальных Claude Code 2.1.119 и Codex CLI 0.120.0, снижает collision rate с 0.20 почти до нуля.",
    "Ни у Anthropic, ни у OpenAI нет первоклассной кросс-вендорной координации. Anthropic Agent Teams (экспериментальная, выключена по умолчанию) координирует только N копий Claude через файловый лок на claim задачи + mailbox в ~/.claude/teams; сама документация предупреждает «два тиммейта, правящие один файл — перезапись». Прямой запрос lock-файла закрыт как «not planned» (issue #19364).",
    "Живой тред anthropics/claude-code#76727 (wshallwshall, открыт 11.07.2026, комментарии до 20.09.2026): разбор 13 782 Edit/Write за 30 дней на 15-20 параллельных сессиях — 44% ушли в главное дерево (реальный баг), но 29% были корректными абсолютными записями в чужой worktree. Вывод: лок должен смотреть на target path записи, а не на cwd сессии.",
    "Пункт F нашего протокола (отправитель статически парсит исходник приёмника на допустимые глаголы ДО транспортной квитанции) — аналога не найдено ни в одном из ~20 просмотренных проектов; лучший кандидат на реально новый вклад, но текущая AST-реализация хрупкая (динамическая регистрация, decorators, расхождение версий кода).",
    "Пункт B (claim на question_id/epoch → lease на точный файл → advisory-видимость) тоже не имеет точного аналога; ближайшие — Axis (атомарный job claim + file claim) и Colony (task claims), но нигде stable question-объект не вынесен отдельно от файла как первый уровень захвата.",
    "Worktree — вендорский дефолт (`claude --worktree`, автo-worktree у Codex-приложения), но не ловит семантический конфликт: кейс Kiel (Anthropic engineering blog, 05.02.2026) — 16 контейнеров с локами на задачу всё равно затирали фиксы друг друга на неразрезанной задаче сборки GCC; живой Show HN-тред (naw103/foremerge, 492⭐, 22.09.2026) — тот же класс бага с PaymentService.",
    "Формат, реально получающий отклик: MCP-сервер + одноключевой установщик (mcp_agent_mail, 2153⭐) или arXiv-статья с бенчмарком на именованных версиях CLI (AgentRoom); голые спеки/прототипы без install path остаются на 0-2⭐ независимо от возраста (agent-coord, AGNT-LOCK, kigster/agent-lock и др.)."
  ],
  "recommendations": [
    "Паковать протокол как MCP-сервер + Python reference implementation + collision benchmark (сценарии: два пишут один файл, lease истёк и старый writer проснулся, folder-claim блокирует чужой файл, неизвестный verb на transport и т.д.) — это доказанно рабочий формат в нише.",
    "Ослабить хрупкость пункта F: не гонять runtime AST-парсинг чужого исходника, а генерировать canonical capabilities.json на билде приёмника, проверять CI-валидатором, а receipt разделить на ENQUEUED/ACCEPTED/APPLIED.",
    "Написать wshallwshall в claude-code#76727 — самый точный и живой адрес: сослаться на его находку (лок по target path, не cwd) и предложить runnable демо, а не презентацию всего протокола.",
    "Написать naw103 (foremerge, живой HN-тред 22.09.2026) про совместимость question_id/epoch с их symbol-level intent (replace/extend) — прямой interoperability-партнёр.",
    "Подавать в ICSE 2027 AGENT workshop (дедлайн 27.11.2026) или arXiv cs.SE/cs.MA с реальным бенчмарком на Claude Code × Codex, а не голой спекой — по образцу AgentRoom.",
    "Не заявлять приоритет по пунктам A, C, E, G (существуют в мире в похожем/слабом виде) — вести публикационный нарратив вокруг B и F как действительно редких находок.",
    "Явно писать в README границы гарантий (нет межмашинной эксклюзии, папка не лочится по умолчанию, ревьюер не может стать писателем) — это тот же приём честности, что сделал foremerge и agent-sync заметными."
  ],
  "entities": {
    "people": ["wshallwshall", "hipvlady", "tianalei", "naw103", "Brenda [ФАМИЛИЯ]", "Klara [ФАМИЛИЯ]", "Meirtz", "dan-calin", "kigster", "daveyod1", "garylesueur", "Quentin [ФАМИЛИЯ] (Dicklesworthstone)", "kcarriedo", "drexthealpha"],
    "companies": ["Anthropic", "OpenAI", "Google (A2A)", "Zed"],
    "products_tools": ["Claude Code", "Codex / codex-cli", "MCP (Model Context Protocol)", "A2A", "ACP (Zed Agent Client Protocol)", "mcp_agent_mail", "Axis", "Limen", "OpenMOSS/claude-codex-handoff", "AgentRoom", "CoAgent", "MPAC", "Beads", "Gas Town", "foremerge", "worktrunk", "claude-squad", "Claude Code Agent Teams", "agent-locks", "agent-coord", "pact", "shared-agent-memory", "GitGuardex", "Colony", "awesome-mcp-servers", "modelcontextprotocol/registry", "gh-issue-lease", "agent-sync"]
  },
  "open_questions": [
    "Точные даты последних коммитов части репозиториев не подтверждены — GitHub API отдавал не все метаданные в этом прогоне.",
    "Уникальность пункта F (fail-closed sender gate по исходнику приёмника) проверена только на публичном открытом коде — не доказательство отсутствия в закрытых решениях.",
    "openai/codex Discussion #22749 найден только по заголовку, содержимое не прочитано ни одним вендором.",
    "Систематический обход X/Twitter и Lobsters не дал результатов — пробел поиска, а не доказательство пустоты.",
    "Живость части тредов (комментарии за последние 2-4 недели) не подтверждена окончательно — нужна ручная перепроверка через `gh issue view --comments` перед контактом.",
    "Секция GLM не дала содержательного ответа (упёрлась в капчу верификации) — не учтена в синтезе, покрытие фактически 3 вендора из 4."
  ],
  "related_concepts": ["multi-agent-role-discipline", "llm-pact", "one-system-propagate", "machine-bus-telegram-rail", "git-worktree-isolation", "PACT-PARITY-20260922"]
}
```
