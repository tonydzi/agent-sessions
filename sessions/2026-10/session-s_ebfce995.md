---
session: s_ebfce995
date: 2026-10-22
words: 941
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-10-22 · Read-only independent review of this docs-only diff. Goal: direct a first-time user to EXI…

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_ebfce995` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

Read-only independent review of this docs-only diff. Goal: direct a first-time user to EXISTING brain-lite START, keep full setup optional, label counts accurately. No executable changes. Live sources verified on 2026-10-22: brain-lite v1.1.0, release ZIP114867 sha07d71fc733e8fef95b9f991be7b0b3d8b5e319d1f893c250d88108dabfa9e64a; registry1 own CORE card, external0; all-state pulse title issue search0 incomplete_resultsfalse. Original release installed in isolated USERPROFILE using unmodified UPDATE Windows step1+2 on pwsh7.6.5 exit0;38 libraryfiles unchanged after real memo task by nonauthor Codex; fresh-context recall being checked. Root does not claim external installation, new peer or 100 machines. Find blocking factual/scope/privacy issues in NEW LINES. Existing unchanged code/claims are out of this docfix. End with ===VERDICT=== APPROVE or REQUEST_CHANGES or AMBIGUOUS.

diff --git a/FOR-ROBOTS.md b/FOR-ROBOTS.md
index ad14160..d95e0db 100644
--- a/FOR-ROBOTS.md
+++ b/FOR-ROBOTS.md
@@ -9,6 +9,12 @@ If a step would need more than that, stop and ask your human.
 
 ## Steps
 
+For a first local task, start with https://github.com/tonydzi/brain-lite/blob/main/START.md.
+It contains a single owner-pasted request for a checked release, a separate work folder, and
+one useful task with a receipt. Preserve its approval step and scope. Installing brain-lite
+does not register an agent or grant fleet access. The full skills and updater below require
+an explicit request for that larger setup; they are not prerequisites for the light start.
+
 1. Install the lab's skills: `npx skills add tonydzi/second-brain-starter-kit` (or the Claude
    Code plugin marketplace commands in README.md). Tell your human how many skills landed.
 2. Download `fleet_daily.py` from this repository, run `python fleet_daily.py init`, then
diff --git a/README.md b/README.md
index d155b44..a9df542 100644
--- a/README.md
+++ b/README.md
@@ -2,20 +2,36 @@
 
 *Читать по-русски: [README.ru.md](README.ru.md)*
 
+**First time using an agent? [Start with brain-lite](https://github.com/tonydzi/brain-lite/blob/main/START.md).**
+Open that page and copy its one block into a working Claude Code or Codex with local folder
+access. It guides you through a checked release download, your approval, and one useful task
+with a receipt. The small library stays separate from your work; it does not install the full
+skill collection, sync folders, services, or a scheduler.
+
+After your first task, return here: Door 2 lists your agent by an optional PR; Door 3 lets you
+contribute a fix or review. A local brain-lite install does not register a member or connect a
+machine to the private fleet. The full skills and daily updater in Door 1 are optional.
+
+**Public funnel snapshot, 2026-10-22:** the [registry](https://github.com/tonydzi/claw-consensus/blob/main/fleet/MEMBERS.md)
+lists **1 lab-owned card and 0 external cards**. The public repository has **0 pulse issues**;
+that issue count does not verify active machines. External active machines are **unverified**.
+The goal is 100 active machines, not 100 downloads. Sources: the linked registry and
+[pulse issue search](https://github.com/tonydzi/join-the-fleet/issues?q=is%3Aissue%20pulse%20in%3Atitle).
+
 We run a fleet of machines where AI agents coordinate each other: a Windows hub with two GPUs,
 three Macs, a Windows laptop, two colleagues' PCs and a VPS anchor. Claude Code, Codex, Cursor and Grok agents
 on those machines talk over a message bus, agree on what to do by propose / counter / accept /
 commit, and wake a human only for money or for something irreversible. Everything they run on
 is open source. Today the fleet has 8 machines. We want 100.
 
-**This page is the whole onboarding.** Fifteen minutes, one link, no account with us, no secrets
-shared. Your machine stays yours. You can leave by deleting one folder.
+Use the light start above for your first local task. The three optional doors below cover
+the full skill collection, the public agent registry, and contributions. Your machine stays yours.
 
 There are three doors. Take any one; take all three if you like.
 
 ---
 
-## Door 1: your machine (15 minutes)
+## Door 1: the full skill collection and daily updater (optional)
 
 Install the lab's skills and the daily routine that keeps them current.
 
diff --git a/README.ru.md b/README.ru.md
index 200da8e..8012c4f 100644
--- a/README.ru.md
+++ b/README.ru.md
@@ -2,18 +2,35 @@
 
 *English: [README.md](README.md)*
 
+**Впервые пробуешь помощника? [Начни с brain-lite](https://github.com/tonydzi/brain-lite/blob/main/START.md).**
+Открой страницу и скопируй один блок в работающий Claude Code или Codex с доступом к локальной
+папке. Он проведёт через проверку скачанного релиза, твоё согласие и одну полезную задачу с
+квитанцией. Маленькая библиотека хранится отдельно от твоей работы; полный набор скиллов,
+синхронизация, службы и планировщик для этого не нужны.
+
+После первой задачи вернись сюда: дверь 2 позволяет отдельным PR внести агента в реестр,
+дверь 3 предлагает вклад или ревью. Локальная установка brain-lite сама не регистрирует
+участника и не подключает машину к частному флоту. Полный набор и ежедневное обновление
+из двери 1 необязательны.
+
+**Снимок публичной воронки на 22.10.2026:** в [реестре](https://github.com/tonydzi/claw-consensus/blob/main/fleet/MEMBERS.md)
+**1 наша карточка и 0 внешних карточек**. В публичном репозитории **0 pulse issues**;
+число таких issues не доказывает активность машин. Активные внешние машины **не проверены**.
+Цель: 100 активных машин, а не 100 скачиваний. Источники: реестр по ссылке и
+[поиск pulse issues](https://github.com/tonydzi/join-the-fleet/issues?q=is%3Aissue%20pulse%20in%3Atitle).
+
 У нас флот машин, на которых ИИ-агенты координируют друг друга: Windows-хаб с двумя GPU, три
 Мака, Windows-ноутбук, два компьютера коллег и VPS-якорь. Claude Code, Codex, Cursor и Grok на этих
 машинах общаются через шину, договариваются по схеме предложил / возразил / принял / закоммитил
 и будят человека только ради денег или необратимого. Всё, на чём это крутится, открыто. Сегодня
 во флоте 8 машин. Хотим 100.
 
-**Эта страница и есть весь онбординг.** Пятнадцать минут, одна ссылка, никаких аккаунтов у нас,
-никаких секретов. Машина остаётся твоей. Уйти можно, удалив одну папку.
+Для первой локальной задачи начни с лайт-входа выше. Три необязательные двери ниже ведут
+к полному набору скиллов, публичному реестру агентов и вкладам. Машина остаётся твоей.
 
 Три двери. Бери любую, можно все три.
 
-## Дверь 1: твоя машина (15 минут)
+## Дверь 1: полный набор скиллов и ежедневное обновление (необязательно)
 
 ```bash
 npx skills add tonydzi/second-brain-starter-kit

---

**Claude:**

You've hit your session limit · resets 11:40pm (Europe/London)
