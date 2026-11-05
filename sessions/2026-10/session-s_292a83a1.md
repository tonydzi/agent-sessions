---
session: s_292a83a1
date: 2026-10-06
words: 5383
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-10-06 · Ты адверсариальный ревьюер. ЗАДАЧА: ОПРОВЕРГНУТЬ правки ниже, а не похвалить. Это Python-к…

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_292a83a1` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

Ты адверсариальный ревьюер. ЗАДАЧА: ОПРОВЕРГНУТЬ правки ниже, а не похвалить. Это Python-код конвейера подачи заявок на вакансии.

Три утверждения автора, каждое проверь на ложность:
A) LAB_DOOR_OPEN_RX + score 14 поднимает 'открытые двери' лабораторий выше шума, но НЕ вытесняет профильные роли (у тех score до 18).
B) Замена 'intern' на r'\bintern(?:s|ship|ships)?\b' режет стажировки и НЕ режет International/Internal. BAD_LAB = тот же список минус intern.
C) select() в pipe_a_night фильтрует рельсы по excluded_rails() fail-soft и не ломается, если модуль pipe_a_rail отсутствует.

Найди КОНКРЕТНЫЕ контрпримеры и баги: ложные срабатывания/пропуски регулярок, SQL-инъекция через имена компаний в labs_sql, порядок ветвей в door_cluster (деньги раньше двери?), что будет при пустом rails после фильтра, регрессии. Отвечай списком: НОМЕР. [BUG|OK] утверждение -> контрпример.

=== DIFF ===
diff --git a/jobs-watch/batch_daily.py b/jobs-watch/batch_daily.py
index ba88c8e6..dff7ca26 100644
--- a/jobs-watch/batch_daily.py
+++ b/jobs-watch/batch_daily.py
@@ -39,6 +39,10 @@ try:
     import pipe_a_rail                    # cooldown рельс; файл рядом, синкается с лагом
 except ImportError:                       # узел, куда pipe_a_rail.py ещё не доехал -> без cooldown, но не падаем
     pipe_a_rail = None
+try:                                      # полоса «внутрь лаборатории»: там интерншип разрешён (канон 01.10)
+    from jobs_discover import LAB_DOOR_CO
+except Exception:                         # нет файла/сломан -> полоса пуста, интерны режутся как вне лабы (консервативно)
+    LAB_DOOR_CO = frozenset()
 DB = os.path.join(HERE, "jobs.db")
 VAULT = os.environ.get("OBSIDIAN_VAULT", r"D:\Vault\Vault-Knowledge")
 OUTDIR = os.path.join(VAULT, "04-Projects", "Pipe-A-Batches")
@@ -228,6 +232,9 @@ def select(c, n, ats=None, money=False, min_pay=MIN_PAY, excluded=None):
     if not rails:
         return [], [("--", "--", f"все рельсы исключены: cooldown={sorted(excluded)}, фильтр --ats={ats}")]
     rails_sql = ",".join("'%s'" % r for r in rails)
+    # имена лабораторий в SQL: одинарные кавычки внутри имени удваиваются (ни одного такого
+    # имени сегодня нет, но список правит человек -- пусть сломается не тут)
+    labs_sql = ",".join("'%s'" % str(x).replace("'", "''") for x in sorted(LAB_DOOR_CO)) or "''" 
     # ⛔ ats='tg' в пачку НЕ идёт: url ведёт на ПОСТ в чате, а не на форму подачи,
     # и часть постов -- это #кандидат, человек ищет работу сам (замер 01.09: две
     # такие строки стояли в топе mass). Податчик на них встанет. TG остаётся
@@ -266,10 +273,22 @@ def select(c, n, ats=None, money=False, min_pay=MIN_PAY, excluded=None):
         # от его имени на intern-позицию бьёт по позиции силы. Замер: 107 таких
         # строк в базе, 6 доехали до пачек, ТРИ прошлые смены помечали их skip
         # РУКАМИ, подано ноль. То есть фильтр уже существовал -- в голове человека.
-        "AND lower(title) NOT LIKE '%intern%' "
+        # 05.10: «intern» резался ПОДСТРОКОЙ и убивал International/Internal. Замер боевой
+        # базы: под фильтр попали 133 роли status=new, настоящих стажировок 58, ложно
+        # срезано 75 -- среди них 16 строк с базой >= $200K (верх: Anthropic «Warehouse and
+        # Logistics Manager - International» $405K) и 33 строки в лабораториях LAB_DOOR_CO,
+        # то есть ровно полоса «любой ценой внутрь». Режем ПО СЛОВУ через GLOB-границу.
+        # Канон 01.10 (голосом): интерншип/residency/fellowship В ЛАБОРАТОРИИ -- штатный
+        # ход, его НЕ режем; student-only режется везде, включая лабораторию.
+        # Сторож: _test_batch_daily.py блок I (I1--I6), красный показан 05.10.
+        "AND NOT ( (lower(title) LIKE '%internship%' OR lower(title) LIKE '%interns%' "
+        "           OR lower(title) GLOB '*intern' OR lower(title) GLOB '*intern[^a-z]*') "
+        f"         AND company NOT IN ({labs_sql}) ) "
         "AND lower(title) NOT LIKE '%new grad%' "
         "AND lower(title) NOT LIKE '%new-grad%' "
         "AND lower(title) NOT LIKE '%graduate program%' "
+        "AND lower(title) NOT LIKE '%campus %' "
+        "AND lower(title) NOT LIKE '%summer analyst%' "
         "AND lower(title) NOT LIKE '%apprentice%' "
         f"ORDER BY {order}").fetchall()
     picked, skipped = [], []
diff --git a/jobs-watch/jobs_discover.py b/jobs-watch/jobs_discover.py
index 30eeec0b..e834a326 100644
--- a/jobs-watch/jobs_discover.py
+++ b/jobs-watch/jobs_discover.py
@@ -18,7 +18,10 @@ upsert в jobs.db таблицу ats_jobs. 0 токенов LLM, только п
 вакансия координатора или support в Anthropic была для трубы невидима. Ярусы решает door_cluster():
 интерншип в лаборатории проходит (dev 01.10), student-only (new grad/campus) и
 гиг-мельница (LAB_JUNK_RX: AI Tutor, аннотатор, rater) отсечены,
-Fellows Program проходит, деньги старше ноги в двери. Список лабораторий явный (LAB_DOOR_CO, 23 имени),
+Fellows Program проходит, деньги старше ноги в двери. Список в двери явный (LAB_DOOR_CO; число растёт,
+считай len() -- на 06.10.2026 их 88) и состоит из ДВУХ наборов: _FRONTIER_CO (ИИ-лаборатории,
+приказ 27.09) и PEER_DOOR_CO (одноклассники: агентная память / контекст / координация агентов,
+приказ 03.10; у них в двери другая причина -- прямое попадание в наш домен, а не «любая цена»),
 а НЕ весь tier1: замер 27.09 дал по всему tier1 +2159 строк, из них Stripe +374 и фонды +348 — раздувание
 базы; по 23 лабораториям +955 (было видно 1797, стало 2752). Канон: Библия
 reglament-vnutr-ii-laboratorii-lyuboy-cenoy-poziciya-ne-vazhna, зеркало скилл /apply §1.1-бис.
@@ -247,7 +250,7 @@ LAB_JUNK_RX = GIG_RX  # имя оставлено: на него ссылают
 # отношения не имеет (замер 27.09: по всему tier1 полоса дала +2159 строк, из них Stripe +374,
 # Databricks +324, фонды +348 — это раздувание базы, а не вход в лабораторию).
 # Имена сверяются с колонкой company в jobs_spec_data.VERIFIED (точное совпадение).
-LAB_DOOR_CO = frozenset({
+_FRONTIER_CO = frozenset({
     # frontier-лаборатории и модельные компании
     "Anthropic", "OpenAI", "xAI", "Mistral AI", "Thinking Machines", "Inflection AI",
     "Cohere", "Reflection AI", "Nous Research", "Reka", "Black Forest Labs", "Liquid AI",
@@ -283,8 +286,110 @@ LAB_DOOR_CO = frozenset({
     "Periodic Labs", "Lila Sciences", "Xaira Therapeutics",
 })
 
-LAB_DOOR = "lab-door"                       # нога в двери frontier-лабы: tier1-доска, кластера нет
+# ⭐ ПОЛОСА ОДНОКЛАССНИКОВ — компании, которые делают ТО ЖЕ, ЧТО И МЫ: агентная память,
+# слой контекста, координация флота агентов. Приказ оператора 03.10.2026, голосом:
+# «Zep, GrabFleet, Cogni, Interloom, Glean, SuperMemory, MemZero и Lepta... все компании
+# AI, которые занимаются тем, чем мы занимаемся. Даже если это стартапы, потому что у нас
+# опыта много». Последняя фраза и есть механика: в этом классе ценность оператора — не вилка
+# и не уровень роли, а ПРЯМОЕ ПОПАДАНИЕ В ДОМЕН, поэтому имена идут в ту же дверь, что
+# лаборатории (score 4: видно в базе, в автоволну само не лезет), а не судятся по порогу
+# $200K, который отсекает стартапы целиком.
+#
+# ⚠️ ДВА ЗАМЕРА, ПОРОДИВШИЕ ИМЕННО ТАКУЮ ФОРМУ (06.10.2026):
+#  1. Правка 03.10 была СДЕЛАНА (блок с «Letta» и «Mem0» в этом же наборе, см.
+#     _scratch/jobs_discover.py.bak2-20261003) и 05.10 ЗАТЁРТА: добор лабораторий
+#     переписал тот же участок комментария и унёс оба имени. len(LAB_DOOR_CO) при этом
+#     вырос, поэтому ни один тест не покраснел. Отсюда ОТДЕЛЬНЫЙ именованный набор:
+#     затереть его молча, правя соседний блок, уже нельзя.
+#  2. Та правка не сработала бы и без затирания: имена вписали как "Letta"/"Mem0", а в
+#     jobs_spec_data.VERIFIED компании лежат как 'letta'/'mem0'. Сравнение в door_cluster
+#     ТОЧНОЕ (`company in LAB_DOOR_CO`) — дверь была нарисованной. Поэтому написание
+#     здесь обязано совпадать с колонкой company в VERIFIED символ в символ, и это
+#     проверяет _test_peer_door.py (P2), а не глаза.
+#
+# Правило списка (L9c, 30.09): имя без ЖИВОЙ двери сюда не кладём. Живая дверь = либо
+# строка в VERIFIED (доска отдала 200 И >= 1 роль; зонд 06.10), либо запись в
+# lab_hand.json — ручная полоса для компаний без публичного ATS-API (как DeepMind/Meta).
+PEER_DOOR_CO = frozenset({
+    # ядро: память и контекст для агентов
+    "Zep AI",          # «Context Lake for AI agents», YC W24. ATS-доски НЕТ: нанимает через
+                       # YC Work at a Startup. Роли приезжают ТРЕТЬЕЙ рельсой --
+                       # careers_feed.py нога B -> careers_rows.json (ats='yc'), прогон 06.10
+                       # 07:27 дал 2 роли: MTS Research $180-250K и Head of FDE $220-270K.
+                       # ⚠️ ИМЯ «Zep AI», а НЕ «Zep»: так его печатает каталог YC, а сравнение
+                       # в door_cluster точное. С «Zep» дверь была НАРИСОВАННАЯ -- третий
+                       # датированный случай одной болезни (03.10 Letta/Mem0 регистр,
+                       # 05.10 затирание блока, 06.10 это). Сторож = _test_peer_door.py P2,
+                       # и он ЗНАЕТ про рельсу careers_rows.json, иначе краснел бы на живой двери.
+    "Letta",           # ashby/letta: Research Engineer, Scientist Post-Training (доска была
+                       # в PRUNED как мёртвая — вердикт протух, GET 06.10 дал 4 роли)
+    "mem0",            # ashby/mem0 (написание из VERIFIED — строчными!)
+    "Engram",          # ashby/engram: Platform / ML Systems / Research
+    "Hyperspell",      # ashby/hyperspell
+    # (Supermemory, Cognee, Graphlit, Interloom из того же приказа двери не имеют —
+    #  они в PEER_NO_DOOR ниже, с причиной по каждому)
+    # ядро: слой контекста и извлечение под агентов
+    "Glean",           # уже стоял в воротах с 27.09 как прикладная ИИ-компания; здесь он
+                       # по второй, более сильной причине — это ровно наш класс
+    "LlamaIndex", "Reducto", "Unstructured", "Vectara",
+    # ядро: координация и флот агентов
+    "LangChain", "dust", "Mastra", "All Hands AI", "Sema4.ai", "Sim",
+})
+
+# Имена ИЗ ПРИКАЗА, у которых двери на 06.10.2026 НЕТ. Держим их здесь с причиной, а не
+# молча выбрасываем: иначе «не нашёл» через месяц читается как «мы и не искали».
+# Вердикт о недоступности протухает (память ban-is-a-claim-recheck-before-workaround):
+# перезондировать зондом класса, нашлась дверь -> имя переезжает в PEER_DOOR_CO одним
+# заходом вместе со строкой в VERIFIED или lab_hand.json.
+PEER_NO_DOOR = {
+    "Graphlit":    "06.10: /careers -> 404 (сайт уехал на graphlit.dev), 6 вендоров ATS x "
+                   "слаг-кандидаты -> 404, в каталоге YC нет. Двери не нашёл.",
+    "Cognee":      "06.10: дверь ЕСТЬ, но только LinkedIn Jobs — 3 вакансии "
+                   "(/jobs/view/id_9218ac5e, /id_43b24d65, /id_3101f9aa), названия анонимно не "
+                   "читаются. LinkedIn у оператора забанен -> дверь для нас закрыта, пока не "
+                   "снят бан (память linkedin-unban-siege). ATS нет, в каталоге YC нет.",
+    "Interloom":   "06.10: /careers -> HTTP-ошибка, ATS -> 404, в каталоге YC нет. Двери не нашёл.",
+    "Supermemory": "06.10: /careers редиректит на главную и ни одной дверной ссылки в HTML, "
+                   "ATS -> 404, в каталоге YC нет. Двери не нашёл.",
+}
+
+# Ворота door_cluster смотрят в ОДИН набор: лаборатории + одноклассники. Разделение нужно
+# не воротам, а людям и сторожу — чтобы знать, по какой причине имя в двери.
+LAB_DOOR_CO = _FRONTIER_CO | PEER_DOOR_CO
+
+LAB_DOOR = "lab-door"                     # нога в двери frontier-лабы: tier1-доска, кластера нет
 LAB_DOOR_SCORE = 4                          # ниже порога пачки 8: виден в базе, в авто-волну сам не лезет
+# 05.10.2026, ДР «перекачанные деньгами ИИ-компании» (вложение голосовой 001): главная тактика
+# для нестандартного профиля -- не бороться с 5000 откликов на generic SWE, а входить через
+# требование, которое компания публикует САМА под людей вне штатного расписания: «General
+# Application», «Opportunistic», «Open Application for Unconventional Talent», «Register Your
+# Interest». Замер, породивший правку: таких дверей в базе 25, подано по ним 0 -- они рождались
+# со score 4 и в сортировке пачки проигрывали вообще всему. Лаборатория с миллиардом и двумя
+# вакансиями иначе недоступна в принципе, поэтому дверь оценивается ВЫШЕ рядовой роли полосы,
+# но ниже точного совпадения с CV-кластером (там 18): выигрывает у шума, не вытесняет профиль.
+# ⛔ Только внутри LAB_DOOR_CO: вне лабораторий «Talent Pool» -- это воронка продажников (n8n,
+# gusto, sentinellabs), повышать её нельзя. Сторож: _test_jobs_discover.py блок O (O1--O7).
+LAB_DOOR_OPEN_SCORE = 14
+# ДОБОР СЛОВАРЯ 06.10.2026. Прежний словарь знал только КАНЦЕЛЯРСКИЕ формы приглашения
+# («General Application», «Register Your Interest»), а живые доски класса зовут человеческим
+# языком — и такие двери рождались со score 4, то есть НИЖЕ порога пачки 8, и не подавались
+# никогда. Замер (прогон досок класса 06.10, строки реальные, не выдуманные):
+#   LlamaIndex   «Don't See Your Role?»                      -> было 4, надо 14
+#   Reducto      «Don't See a Perfect Role? Apply Anyway!»    -> было 4
+#   Engram       «Expression of Interest»                     -> было 4
+#   Unstructured «Join us - Evergreen Opportunities»          -> было 4
+#   Restate      «Create your own Role»                       -> было 4
+#   Composio     «<insert your dream job here>»               -> было 4
+# Это ровно та дверь, которую ДР 05.10 называет главной тактикой для нестандартного профиля,
+# то есть дефект бил по самому ценному. Апостроф берём как `.?`: доски пишут и ' и ’, и «dont».
+# ⛔ Повышение по-прежнему работает ТОЛЬКО внутри LAB_DOOR_CO (ветка door_cluster): вне двери
+# «Talent Pool» — воронка продажников (n8n, gusto, sentinellabs). Сторож: _test_peer_door.py D1/D2.
+LAB_DOOR_OPEN_RX = re.compile(
+    r"general\s+application|general\s+interest|open\s+application|opportunistic|"
+    r"register\s+your\s+interest|unconventional\s+talent|"
+    r"don.?t\s+see\s+(?:your|a|the|an)\b|apply\s+anyway|expression\s+of\s+interest|"
+    r"evergreen\s+opportunit|create\s+your\s+own\s+role|dream\s+job|"
+    r"talent\s+network|spontaneous\s+application|stay\s+in\s+touch", re.I)
 # 02.10: UNCL (`money-uncl`) -- самый частый кластер второго яруса: его отдаёт
 # money_cluster() для роли с базой >= FLOOR, не совпавшей ни с одним MONEY_RX.
 # Своей CV-ветки у него нет и быть не может (кластер по определению «не распознан»),
@@ -322,6 +427,10 @@ def door_cluster(title, tier, comp, company=None):
          «моя задача попасть любой ценой внутрь компании, не важно, какую позицию».
          До этой ветки роль без кластера и без вилки на доске Anthropic/OpenAI/xAI молча
          выбрасывалась в run() (`continue`) и в jobs.db не попадала вовсе;
+      3-бис. открытая дверь лаборатории (LAB_DOOR_OPEN_RX: General Application / Opportunistic /
+         Open Application / Register Your Interest) -> 'lab-door' со score LAB_DOOR_OPEN_SCORE=14:
+         ДР 05.10 называет это главной тактикой для нестандартного профиля, а замер показал
+         25 таких дверей в базе при НОЛЕ подач -- score 4 проигрывал в сортировке всему;
       4. остальное -> (None, 0), как и было.
     """
     t = title or ""
@@ -339,6 +448,9 @@ def door_cluster(title, tier, comp, company=None):
         # Единственная правда о том, лаборатория это или нет, = LAB_DOOR_CO.
         if LAB_JUNK_RX.search(t):
             return None, 0
+        if LAB_DOOR_OPEN_RX.search(t):
+            # открытая дверь лаборатории: компания сама пригласила профиль вне расписания
+            return LAB_DOOR, LAB_DOOR_OPEN_SCORE
         return LAB_DOOR, LAB_DOOR_SCORE
     return None, 0
 
@@ -531,7 +643,9 @@ def run():
     # 24.09: раз в неделю тянем доски YC-компаний, которые нанимают (yc_feed.py); новые попадут в VERIFIED.
     # 02.10: второй подпитчик — vc_feed.py, портфельные доски 33 фондов на Getro (слайс слона за прогон).
     fed = 0
-    for mod in ("yc_feed", "vc_feed"):
+    # 06.10: третий подпитчик — event_feed.py, компании-ОРГАНИЗАТОРЫ ивентов
+    # (приказ оператора голосом: «если компания проводит ивент, мы добавляем её в лист работодателей»).
+    for mod in ("yc_feed", "vc_feed", "event_feed"):
         try:
             fed += __import__(mod).refresh_if_stale(7) or 0
         except Exception as e:
diff --git a/jobs-watch/pipe_a_night.py b/jobs-watch/pipe_a_night.py
index 31f5b41e..75af131a 100644
--- a/jobs-watch/pipe_a_night.py
+++ b/jobs-watch/pipe_a_night.py
@@ -6,7 +6,13 @@
 перестал запускаться. Подача — детерминированная работа (отбор SQL + run_slice), LLM ей не нужен.
 Что делает (хаб, задача Windows раз в сутки ночью):
   1) jobs_db_guard.gate() — база, «забывшая» поданное, = дубли; красный -> стоп и тревога;
-  2) отбор: сперва frontier-лаборатории на ЛЮБУЮ позицию (кластер lab-door, §9.14 CLAUDE.md, dev 27.09),
+  2) отбор: сперва frontier-лаборатории на ЛЮБУЮ позицию (кластер lab-door, §9.14 CLAUDE.md, dev 27.09;
+     порядок ВНУТРИ полосы -- сила роли и свежесть, НЕ деньги: вилку лаборатории обычно не публикуют,
+     а денежным порядком квоты выедали 752 строки с вилкой из 2 163, см. комментарий у lab_order),
+     затем ОДНОКЛАССНИКИ -- компании нашего класса (агентная память / контекст / координация агентов,
+     jobs_discover.PEER_DOOR_CO, приказ dev 03.10) своей квотой PEER_SHARE и СВОИМ бюджетом рельс:
+     кластер у них тот же 'lab-door', поэтому без квоты 16 имён растворялись в 88 именах ворот,
+     а общий счётчик ashby выжигался лабораториями до единой их строки (66 из 89 стоят на ashby),
      затем роли с базой $200K+ (dev 24.09); рельсы greenhouse (+ lever пробой ≤ LEVER_PROBE);
      ashby — ТОЛЬКО в полосе лабораторий и квотой ≤ ASHBY_PROBE (05.10: запрет 24-25.09 «спам-стена»
      протух — по ashby прошло 477 подач и ИМЕННО там оба интервью базы, по greenhouse 433 и НОЛЬ;
@@ -37,6 +43,22 @@ OUTDIR = os.path.join(VAULT, "04-Projects", "Pipe-A-Batches")
 USAGE = os.path.join(os.path.expanduser("~"), ".claude", "state", "pipe_a_night_usage.jsonl")
 N_DEFAULT = 150        # 02.10 dev «подними ночь до 50 заявок»: конверсия ~35% -> волна ~150
 LAB_SHARE = 100         # мест под лаборатории любой позиции (§9.14)
+# ⭐ 06.10 (приказ dev 03.10, голосом): мест под КОМПАНИИ НАШЕГО КЛАССА -- агентная память,
+# контекст, координация агентов (jobs_discover.PEER_DOOR_CO: Zep, Letta, mem0, Engram,
+# Hyperspell, Glean, LlamaIndex, Mastra, Sim, dust, LangChain...). В базе они лежат тем же
+# кластером 'lab-door', что лаборатории, поэтому отличаются ТОЛЬКО по имени компании.
+# ⚠️ ЗАМЕР, ПОРОДИВШИЙ КВОТУ (06.10, боевая база): в полосе лабораторий 100 мест и сортировка
+# `comp DESC, score DESC`, а новых строк cluster='lab-door' 2163, из них С ВИЛКОЙ 750. То есть
+# первые 100 мест забирают строки с вилкой, и роль одноклассника БЕЗ вилки недостижима
+# в принципе: 62 из 89 его строк вилки не имеют (langchain 53 из 53, dust 7 из 13). Стартап
+# памяти зарплату на доске не печатает -- значит без своей квоты приказ «добавь их в воронку»
+# даёт видимость в базе и НОЛЬ подач, ровно как «25 открытых дверей, 0 подач» 05.10.
+# 20 из 150 = полоса видна в каждой волне и не вытесняет ни профиль, ни лаборатории.
+PEER_SHARE = 20
+try:    # имена одноклассников берём из движка: один список на движок и на волну
+    from jobs_discover import PEER_DOOR_CO
+except Exception:        # движок не доехал на узел -> полоса пустая, но волна не падает
+    PEER_DOOR_CO = frozenset()           # сторож равенства: _test_pipe_a_night.py блок C
 LEVER_PROBE = 3         # lever капчит: квота-проба, не бан
 # 05.10: ashby открыт ПОЛОСЕ ЛАБОРАТОРИЙ. Замер: ashby 477 подач -> 2 интервью + 1 pending,
 # greenhouse 433 подачи -> 0; при этом 1 496 из 2 000 непройденных ролей лабораторий
@@ -51,12 +73,25 @@ PER_COMPANY_LAB = 6
 PER_COMPANY = 4
 MIN_PAY, MAX_PAY = 200000, 900000   # база > $900K почти всегда мусор парсера (деньги компании, не зарплата)
 NOCOMP_MIN_SCORE = 10   # третий ярус: сильная роль без вилки («без вилки не выбрасывать», dev 24.09)
-BAD = re.compile(r"intern|new grad|campus|university grad|recruit|mechanical|electrical|technician|thermal|"
-                 r"clearance|TS/SCI|nurse|paralegal|german|japanese|korean|mandarin|french|spanish|italian|"
-                 r"dutch|portuguese|tutor|annotat|\brater\b|account executive|\bSDR\b|\bBDR\b|sales development",
-                 re.I)
+# 05.10: стоп-слова держим СПИСКОМ, а не одной строкой-простынёй. Было: BAD одной строкой +
+# BAD_LAB = BAD.pattern.replace("intern|", "", 1) -- хирургия по тексту шаблона, которая молча
+# рассыпается, как только сам токен меняется. Теперь один источник токенов, лабораторный
+# вариант = тот же список минус intern.
+# ЗАМЕР 05.10: токен был `intern` БЕЗ границы слова и убивал однокоренные International и
+# Internal. На условии-близнеце в batch_daily замерено: 133 роли status=new под фильтром,
+# НАСТОЯЩИХ стажировок 58, ложно срезано 75 -- в том числе 16 строк с базой >= $200K (верх:
+# Anthropic "Warehouse and Logistics Manager - International" $405K, далее $300K, $295K x2,
+# $247K) и 33 строки в лабораториях. Класс РЕЦИДИВНЫЙ: "детектор судит подстроку, а не
+# структуру", 13-я датированная строка журнала; закрытие 19.08 покрыло регулярки Python со
+# границей слова, но не покрыло ни SQL LIKE, ни вот такой токен без границы.
+# Сторож: _test_pipe_a_night.py блок W (W1--W3), красный показан 05.10.
+_BAD_INTERN = r"\bintern(?:s|ship|ships)?\b"
+_BAD_REST = (r"new grad|campus|university grad|recruit|mechanical|electrical|technician|thermal|"
+             r"clearance|TS/SCI|nurse|paralegal|german|japanese|korean|mandarin|french|spanish|italian|"
+             r"dutch|portuguese|tutor|annotat|\brater\b|account executive|\bSDR\b|\bBDR\b|sales development")
+BAD = re.compile(_BAD_INTERN + "|" + _BAD_REST, re.I)
 # 01.10 (dev): интерншип в лаборатории = ДА; new grad / campus по-прежнему отсечены
-BAD_LAB = re.compile(BAD.pattern.replace("intern|", "", 1), re.I)
+BAD_LAB = re.compile(_BAD_REST, re.I)
 KEYS = ("url", "company", "title", "ats", "cluster", "location", "score", "tier")
 
 
@@ -68,40 +103,115 @@ def select(conn, n=N_DEFAULT, today=None):
         "AND COALESCE(applied,'') >= ?", (since.isoformat(),))}
     cols = {r[1] for r in conn.execute("PRAGMA table_info(ats_jobs)")}
     comp = "comp_min" if "comp_min" in cols else "NULL"
+    # 05.10: cooldown рельсы живёт в pipe_a_rail, и до этой правки его читал ТОЛЬКО
+    # batch_daily -- хотя докстринг pipe_a_rail обещает «оба селектора читают его сами».
+    # Цена промаха: ashby у ночного податчика разрешён ИМЕННО в полосе лабораторий, которая
+    # идёт первой, значит ASHBY_PROBE попыток ушли бы в стену по нашим лучшим целям, а каждая
+    # попытка флагает КОМПАНИЮ на сутки (/apply 2.2). Сторож: блок R (R1/R2), красный показан.
+    try:
+        import pipe_a_rail as _rail
+        _dead = set(_rail.excluded_rails())
+    except Exception:            # модуль не доехал на узел -> идём как раньше, но не падаем
+        _dead = set()
+    if _dead:
+        print("рельсы в cooldown, из волны исключены: %s" % ", ".join(sorted(_dead)))
+
+    def _rails_in(rails):
+        rails = [r for r in rails if r not in _dead] or ["__none__"]
+        return ",".join("'%s'" % r for r in rails)
+
     def _base(rails):
-        rails_sql = ",".join("'%s'" % r for r in rails)
         return (f"SELECT url,company,title,ats,cluster,location,score,tier,{comp} FROM ats_jobs "
-                f"WHERE status='new' AND ats IN ({rails_sql}) AND ")
+                f"WHERE status='new' AND ats IN ({_rails_in(rails)}) AND ")
     base = _base(RAILS_MONEY)
-    out, per, lever, ashby = [], {}, 0, 0
+    out, per, taken = [], {}, set()
+    # 06.10: квоты рельс считаются ПО ПОЛОСЕ, а не на всю волну. Корень: класс (dev 03.10)
+    # почти целиком стоит на ashby, лабораторная полоса идёт первой и выжигала общий ASHBY_PROBE
+    # до единой строки класса -- полоса получала ноль МОЛЧА, ровно как «25 открытых дверей, 0 подач».
+    lever_n, ashby_n = {}, {}
 
-    def take(sql, limit):
-        nonlocal lever, ashby
+    def take(sql, limit, lane="money"):
         for row in conn.execute(sql):
             e = dict(zip(KEYS, row[:8]))
+            if e["url"] in taken:
+                # полосы лабораторий и одноклассников смотрят в ОДИН кластер 'lab-door' и
+                # пересекаются (Glean с вилкой проходит обеими). Без этой строки одна и та же
+                # ссылка уехала бы в волну дважды = два сабмита на одну вакансию.
+                continue
             k = (e["company"] or "").lower()
-            lab = e["cluster"] == "lab-door"
-            cap = PER_COMPANY_LAB if lab else PER_COMPANY
+            door = e["cluster"] == "lab-door"          # полоса двери: свои капы и стоп-слова
+            cap = PER_COMPANY_LAB if door else PER_COMPANY
             if k in recent:
                 cap = max(1, cap // 2)        # подавались за 2 дня -> половина мест, не ноль
-            if (BAD_LAB if lab else BAD).search(e["title"] or "") or per.get(k, 0) >= cap:
+            if (BAD_LAB if door else BAD).search(e["title"] or "") or per.get(k, 0) >= cap:
                 continue
             if e["ats"] == "lever":
-                if lever >= LEVER_PROBE:
+                if lever_n.get(lane, 0) >= LEVER_PROBE:
                     continue
-                lever += 1
+                lever_n[lane] = lever_n.get(lane, 0) + 1
             elif e["ats"] == "ashby":
-                if ashby >= ASHBY_PROBE:
+                if ashby_n.get(lane, 0) >= ASHBY_PROBE:
                     continue
-                ashby += 1
+                ashby_n[lane] = ashby_n.get(lane, 0) + 1
             per[k] = per.get(k, 0) + 1
+            taken.add(e["url"])
             e["location"] = e["location"] or ""
             e.update(extra={}, comp_min=row[8])
             out.append(e)
             if len(out) >= limit:
                 return
 
-    take(_base(RAILS_LAB) + f"cluster='lab-door' ORDER BY COALESCE({comp},0) DESC, score DESC", min(LAB_SHARE, n))
+    # 06.10: ПОРЯДОК полосы лабораторий больше НЕ ранжирует по деньгам. Было
+    # `ORDER BY COALESCE(comp_min,0) DESC, score DESC` -- строка родилась вместе с файлом
+    # 29.09 копией из денежной полосы, отдельного решения за ней не стояло (git log -L 131).
+    # Цена: NULL приравнивался к НУЛЮ долларов, то есть к худшему возможному значению. Замер
+    # живой базы 06.10: lab-door status='new' 2 163 строки, с известной comp_min только 752
+    # (621 ashby + 131 greenhouse); мест LAB_SHARE=100, квота ASHBY_PROBE=40 -- 752 строки с
+    # вилкой выедали обе квоты целиком, а 1 411 строк БЕЗ вилки стояли в хвосте бесконечно.
+    # В волне 06.10 (109 строк, 83 лаборатории, 22 компании) не было ни Prometheus (10 ролей,
+    # вилки нет), ни Ineffable Intelligence (3, нет), ни Periodic Labs (35, вилка у 3).
+    # Это подрывало цель самой полосы: §9.14 CLAUDE.md и [[get-inside-the-lab-at-any-position]]
+    # -- «в frontier ИИ-лаборатории уровень роли и порог денег НЕ фильтр». Формально сортировка
+    # фильтром не является, но при полной квоте работает как фильтр.
+    # Сосед batch_daily.order_sql так НЕ делает: там корзины денег, корзина «вилка неизвестна»
+    # стоит ВЫШЕ корзины «известна и ниже планки», а внутри неё денежный член намеренно погашен;
+    # полоса лабораторий была строго небрежнее соседа. Полоса класса ниже с рождения взяла
+    # score DESC -- тем же порядком.
+    # Теперь порядок = сила роли, потом свежесть. Денежные ярусы ниже НЕ тронуты.
+    # Сторож: _test_pipe_a_night_labsort_1006.py (L1--L4), красное показано 06.10.
+    lab_order = "score DESC" + (", first_seen DESC" if "first_seen" in cols else "")
+    # ...и ПЕРВЫЙ ключ -- круги по компаниям: сперва лучшая роль КАЖДОЙ лаборатории, только
+    # потом вторая у каждой. Без этого круга свежесть повторяет ту же болезнь другим ключом.
+    # ЗАМЕР 06.10: у 1 572 из 1 579 ashby-строк полосы score РАВЕН 4, то есть весь порядок
+    # решает второй ключ; приток новых строк 39-45 в сутки при окне ASHBY_PROBE=40 -- значит
+    # `first_seen DESC` отдаёт окно последним двум дням обнаружения, а бэклог 1 302 строки от
+    # 28.09 и 127 от 01.10 не будет достигнут НИКОГДА. Голодание по деньгам сменилось бы
+    # голоданием по возрасту: три целевые компании (Prometheus 10.05, Ineffable 10.05,
+    # Periodic Labs 09.30--10.06) стоят ровно на границе окна и в двух прогонах подряд дали
+    # 13 строк и 1 -- лотерея, а не отбор. Круг по компаниям делает «внутрь ЛЮБОЙ лаборатории»
+    # (§9.14) проверяемым: 74 компании в пуле, 57 на ashby, окно 40 -> 40 РАЗНЫХ компаний.
+    # Оконная функция есть с SQLite 3.25; на древней сборке тихо откатываемся к плоскому
+    # порядку, а не падаем (сторож L7/L8).
+    rot = f"ROW_NUMBER() OVER (PARTITION BY lower(company) ORDER BY {lab_order})"
+    if not _window_ok(conn):
+        rot = None
+    take(_base(RAILS_LAB) + f"cluster='lab-door' ORDER BY " + (f"{rot}, {lab_order}" if rot else lab_order),
+         min(LAB_SHARE, n), lane="lab")
+    # Полоса ОДНОКЛАССНИКОВ (dev 03.10): отличается от лабораторной только списком имён,
+    # потому что кластер у них один. Порядок -- тот же lab_order, один источник на обе полосы.
+    # Зачем полоса ВООБЩЕ нужна после починки сортировки выше: сортировка решает, кто первый
+    # среди 2 163 строк, а квота решает, что одноклассники в волне ЕСТЬ. Мест LAB_SHARE=100,
+    # лабораторных строк 2 163 -- при равном score (у двери он всегда 4) одноклассник
+    # проигрывает по рождению строки, и 20 имён класса растворяются в 88 именах воротах.
+    # Вторая половина: бюджет ashby. В lab-door 1 547 ashby-строк при ASHBY_PROBE=40, полоса
+    # лабораторий идёт первой -- на общем счётчике одноклассник не получал НИ ОДНОЙ попытки,
+    # а 66 из 89 его строк стоят ровно на ashby. Поэтому бюджет рельс считается по полосе.
+    # limit кумулятивен по out -> считаем от набранного.
+    if PEER_DOOR_CO:
+        peers_sql = ",".join("'%s'" % x.lower().replace("'", "''") for x in sorted(PEER_DOOR_CO))
+        take(_base(RAILS_LAB) + f"cluster='lab-door' AND lower(company) IN ({peers_sql}) "
+                                f"ORDER BY {lab_order}",
+             min(len(out) + PEER_SHARE, n), lane="peer")
     if comp != "NULL":
         take(base + f"cluster NOT IN ('lab-door','money-uncl') AND {comp} BETWEEN {MIN_PAY} AND {MAX_PAY} "
                     f"ORDER BY {comp} DESC, score DESC", n)
@@ -110,6 +220,18 @@ def select(conn, n=N_DEFAULT, today=None):
     return interleave(out)
 
 
+def _window_ok(conn):
+    """есть ли в этой сборке SQLite оконные функции (ROW_NUMBER, с 3.25) -> bool.
+
+    Спрашиваем САМ движок пробой, а не сравниваем строку версии: сборка может быть урезанной.
+    Цена ошибки -- падение ночной подачи целиком, поэтому проба, а не вера в версию."""
+    try:
+        conn.execute("SELECT ROW_NUMBER() OVER (ORDER BY 1)").fetchone()
+        return True
+    except sqlite3.OperationalError:
+        return False
+
+
 def interleave(rows):
     """формы одной компании не подряд: круговой проход по компаниям в порядке первого появления.
     Подряд идущие сабмиты одной компании = спам-флаг и затык кодов Greenhouse (~4 письма/час на компанию)."""
@@ -157,10 +279,26 @@ def main():
     os.makedirs(OUTDIR, exist_ok=True)
     json.dump(wave, open(wp, "w", encoding="utf-8"), ensure_ascii=False, indent=1)
     labs = sum(e["cluster"] == "lab-door" for e in wave)
-    print(f"волна {day}: {len(wave)} строк (лаборатории {labs}, lever {sum(e['ats'] == 'lever' for e in wave)}) -> {wp}")
+    # 06.10: у полосы одноклассников обязан быть РОТ. Её строки лежат тем же кластером
+    # 'lab-door', поэтому в счёте `labs` они неотличимы от лабораторий -- отчёт сказал бы
+    # «лаб 103» и про исполнение приказа 03.10 не сказал бы НИЧЕГО, то есть полоса могла
+    # отдавать ноль месяцами, и это было бы не видно (CLAUDE.md §5.5: прибор не имеет права
+    # быть слепым; §5.8: у каждой живой детали свой счётчик).
+    _peers_lc = {x.lower() for x in PEER_DOOR_CO}
+    peers = sum((e["company"] or "").lower() in _peers_lc for e in wave)
+    peer_co = sorted({(e["company"] or "") for e in wave if (e["company"] or "").lower() in _peers_lc})
+    print(f"волна {day}: {len(wave)} строк (дверь {labs}, из них одноклассники {peers} "
+          f"по {len(peer_co)} компаниям, lever {sum(e['ats'] == 'lever' for e in wave)}) -> {wp}")
+    if peers:
+        print("   одноклассники в волне: " + ", ".join(peer_co))
+    else:
+        # ноль говорится ВСЛУХ: молчащая полоса читается как «полосы нет»
+        print(f"   ⚠️ одноклассников в волне НОЛЬ (имён в наборе {len(PEER_DOOR_CO)}, "
+              f"квота {PEER_SHARE}) -- проверить, есть ли у них строки status='new'")
     if dry or not wave:
         _log({"ts": datetime.datetime.now().isoformat(timespec="seconds"), "node": socket.gethostname(),
-              "actor": "pipe_a_night", "event": "dry" if dry else "empty", "outcome": "ok", "wave": len(wave)})
+              "actor": "pipe_a_night", "event": "dry" if dry else "empty", "outcome": "ok",
+              "wave": len(wave), "door": labs, "peers": peers, "peer_co": peer_co})
         return 0
     out = os.path.join(SEL, f"run_night_{day}.out")
     idx = ",".join(str(i) for i in range(len(wave)))
@@ -169,12 +307,13 @@ def main():
                        cwd=SEL, stdout=f, stderr=subprocess.STDOUT, timeout=int(7.5 * 3600))   # 150 форм x ~2.5 мин, окно 01:30-09:00
     counts = tally(open(out, encoding="utf-8", errors="ignore").read())
     msg = (f"[Труба А][НОЧЬ {day}] {socket.gethostname()} pipe_a_night: волна {len(wave)} "
-           f"(лаб {labs}) · " + ", ".join(f"{k} {v}" for k, v in counts.items()))
+           f"(дверь {labs}, одноклассники {peers}) · " + ", ".join(f"{k} {v}" for k, v in counts.items()))
     bus = os.path.join(os.path.expanduser("~"), ".claude", "scripts", "bus_send.py")
     if os.path.exists(bus):
         subprocess.run([sys.executable, bus, msg], timeout=120)
     _log({"ts": datetime.datetime.now().isoformat(timespec="seconds"), "node": socket.gethostname(),
-          "actor": "pipe_a_night", "event": "run", "outcome": "ok", "wave": len(wave), "counts": counts})
+          "actor": "pipe_a_night", "event": "run", "outcome": "ok", "wave": len(wave), "counts": counts,
+          "door": labs, "peers": peers, "peer_co": peer_co})
     print(msg)
     return 0

---

**Claude:**

## Вердикт по трём утверждениям

**A. [OK, но с недоказанной предпосылкой]** score 14 < «там 18» — поднимает открытую дверь выше шума, не вытесняет профиль.

Из диффа видно, что ветка `LAB_DOOR_OPEN_RX` вложена в уже существующую ветку `company in LAB_DOOR_CO` (шаг «3-бис» в нумерации докстринга, после шагов 1–2, которых в диффе НЕТ). Сама архитектура («роль без кластера и без вилки... молча выбрасывалась» — т.е. это fallback для НЕраспознанных ролей) подсказывает, что CV-match (score 18) считается раньше и отдельно, а door_cluster вызывается только когда профильный матчер вернул пусто. **Но это не доказано самим диффом** — тела шагов 1–2 не показаны, поэтому порядок вызовов (деньги/профиль раньше двери или нет) неверифицируем по приведённому коду.

Побочный риск, не опровергающий A напрямую, но ослабляющий точность: `LAB_DOOR_OPEN_RX` содержит `talent\s+network` и `dream\s+job` — реальный заголовок типа **"Talent Network Lead"** (кадровая роль, не инвайт на подачу) внутри лаборатории ложно получит score 14 вместо 4, хотя это не «открытая дверь», а обычная вакансия.

**B. [BUG]** `\bintern(?:s|ship|ships)?\b` режет стажировки и не режет International/Internal.

Python-регэксп (`pipe_a_night.py`) корректен: `\b` не совпадает между двумя буквами, поэтому "international"/"internal" не ловятся — здесь утверждение верно.

Но **в `batch_daily.py` эквивалентная SQL-реализация слабее регэкспа**:
```sql
lower(title) LIKE '%internship%' OR lower(title) LIKE '%interns%' OR GLOB '*intern' OR GLOB '*intern[^a-z]*'
```
`LIKE '%interns%'` и `LIKE '%internship%'` — это substring-проверки БЕЗ левой границы слова (в отличие от GLOB-веток с `[^a-z]`). Контрпример: гипотетический заголовок **"Winternship Program"** или **"Preinternship Track"** содержит подстроку `internship`/`interns` без word-boundary слева и будет ложно отфильтрован, хотя сам токен "intern" как отдельное слово там не встречается. Риск практически низкий (такие слова редки в реальных тайтлах), но это расхождение между двумя "эквивалентными" реализациями одного правила в разных файлах — ровно тот класс дефекта, который §5.10 CLAUDE.md называет рецидивным («детектор судит подстроку, а не структуру»), и здесь он остался наполовину починенным.

Также **gerund-форма "Interning"** (редкая, но существующая формулировка) — false negative в `\bintern(?:s|ship|ships)?\b`: после "intern" идёт "ing", оптациональная группа не покрывает "ing", `\b` не находится между "n" и "i" (оба буквы) → титул "Interning Program" пройдёт фильтр как НЕ-интернship.

Отдельная, более существенная находка по BAD_LAB: `cluster == "lab-door"` теперь присваивается И фронтир-лабам, И `PEER_DOOR_CO` (Zep, Letta, mem0...), а `BAD_LAB`/`PER_COMPANY_LAB=6` применяются по этому же флагу `door`. Но сам комментарий в диффе настаивает, что у одноклассников «другая причина — прямое попадание в наш домен, а не "любая цена"» (в отличие от канона §9.14 про лаборатории). Итог: политика «интерншип разрешён, капа 6» молча расползлась на компании, для которых канон её не оговаривал — это конфликт между собственным комментарием кода и реализацией.

**C. [OK]** fail-soft по `excluded_rails()` подтверждён.

`import pipe_a_rail as _rail; _dead = set(_rail.excluded_rails())` целиком внутри `try/except Exception` → ImportError/AttributeError/TypeError (если `excluded_rails()` вернёт не-iterable) всё ловится, `_dead` остаётся `set()`. Пустой `rails` после фильтра обработан: `_rails_in` подставляет `["__none__"]`, что превращает `IN (...)` в безопасный пустой результат, а не в синтаксическую ошибку SQL. Контрпримера не нашёл — утверждение верно как есть.

**Но рядом найдена конкретная регрессия, не входящая в заявленные три пункта**: бюджеты `ashby_n`/`lever_n` теперь — словари **по `lane`** ("lab", "peer", "money"), а не единый глобальный счётчик, как было (`out, per, lever, ashby = [], {}, 0, 0`). И lab-лейн, и peer-лейн используют один и тот же `RAILS_LAB` (включающий ashby). Конкретный сценарий: lab-лейн выбирает до `ASHBY_PROBE=40` ashby-строк (`ashby_n['lab']`), затем peer-лейн СВОИМ счётчиком `ashby_n['peer']` может добрать ещё до 40 — итого до 80 ashby-попыток за ночь вместо заявленного единого потолка 40. Собственный докстринг файла называет именно этот рельс чувствительным («05.10: запрет 24-25.09 "спам-стена" протух») — то есть рефакторинг для борьбы с голоданием peer-полосы по деньгам тихо снял защиту от спам-стены на ashby, умножив пробный бюджет на число полос.

---

**Доп. проверки по запросу:**

- **SQL-инъекция через имена компаний** — не найдена: оба места (`labs_sql` в `batch_daily.py`, `peers_sql` в `pipe_a_night.py`) корректно удваивают одинарные кавычки (`.replace("'", "''")`) перед вклеиванием в `'...'`-литерал — стандартный и достаточный эскейпинг для SQLite.
- **Порядок веток `money` vs `door` в `door_cluster`** — неверифицируем по диффу (шаги 1–2 не показаны); флагую как открытый риск, требующий чтения полного тела функции.
- **Пустой `rails` после фильтра** — обработан сентинелом `__none__`, не ломается.
