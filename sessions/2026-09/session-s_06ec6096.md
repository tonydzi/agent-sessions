---
session: s_06ec6096
date: 2026-09-04
words: 1029
turns: 4
tools: "Bash, Read"
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-04 · Scheduled run: fb-reply-daily

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_06ec6096` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

<scheduled-task name="fb-reply-daily" file="C:\Users\dev\.claude\scheduled-tasks\fb-reply-daily\SKILL.md">
This is an automated run of a scheduled task. The user is not present to answer questions. For implementation details, execute autonomously without asking clarifying questions — make reasonable choices and note them in your output. "write" actions (e.g. MCP tools that send, post, create, update, or delete), only take them if the task file asks for that specific action. When in doubt, producing a report of what you found is the correct output.

---
name: fb-reply-daily
description: 1×/сутки (16:00 хаба, cron 0 16 * * *; прежнее «13:30» в прозе было устаревшим, сверено с реестром 01.09) ответить на ВСЕ свежие комменты под постами оператора в Facebook в режиме ПРОВОКАТОР (приказ dev 05.08.2026 - задираться, спорить, не поддакивать) + лайк-хвост. Строго на хабе HUB-01 (IP-гейт). Процедура и все грабли = скилл /fb-reply; здесь только порядок прогона. Восстановлена 25.08.2026 по приказу оператора (рутины ответов на FB-комменты на хабе не существовало - была только утренняя сводка Pub-Comments-Morning-03). [HUB HUB-01; account tonydzi]
---

Суточный прогон ответов на комментарии под постами оператора в Facebook. Вся механика, грабли DOM и правила тона живут в одном месте: C:\Users\dev\.claude\skills\fb-reply\SKILL.md - прочитай его ЦЕЛИКОМ и следуй ему, здесь только каркас прогона. Прозу про код заново не писать.

0. РЕЛЬСА = FIREFOX, И ЧТЕНИЕ, И ЗАПИСЬ (приказ оператора 01.09.2026 голосом трижды: «всегда работаем через Firefox»). Chrome-MCP из /fb-reply §3 - УСТАРЕВШИЙ путь: не звать, тулы не грузить, «расширение не подключено» больше не причина завершать прогон. Улика перевода: Chrome-рельса FB простояла разлогиненной 12 суток (19.08-01.09), живая FB-сессия всё это время лежала в Firefox; запись доказана 01.09 в 12:18 (ответ Fiona [ФАМИЛИЯ] опубликован и подтверждён после релоада).
   Профиль: клон системного `646yqiss.default-release` в `~/.claude/browser-profiles/fbreply`. Обновить куки перед прогоном:
   `python -c "import sys,os;sys.path.insert(0,os.path.expanduser('~/.claude/scripts/_shared'));import firefox_selenium as fs;print(fs.clone_profile(r'C:\Users\dev\AppData\Roaming\Mozilla\Firefox\Profiles\646yqiss.default-release', os.path.expanduser('~/.claude/browser-profiles/fbreply')))"`
   Различай корни: (а) редирект на login.php / нет cookie c_user = FB-сессия разлогинена = руки оператора, аск класса D через approval.py в 02 (см. 0.5); (б) залогинен, но комментов ноль = так и доложи, это не сбой; (в) Firefox не поднялся = назови ошибку драйвера, не выдавай за «нет комментов».

0.5 ПРЕДЧЕК ЖИВОСТИ FB-СЕССИИ (0 LLM, 0 сети, доли секунды -- ДО любого захода в браузер):
   python "%USERPROFILE%/.claude/scripts/_shared/fb_session_check.py"
   exit 0 = сессия жива, иди дальше. exit 1 (мертва) ИЛИ exit 2 (не определил) = СТОП ЗДЕСЬ,
   в браузер НЕ ходим (полный заход стоит прогона, а разлогин виден с диска бесплатно):
     - подними аск класса D: python "%USERPROFILE%/.claude/scripts/approval.py" ask "FB-сессия
       на хабе разлогинена (<вывод предчека>), FB-лейн стоит. Нужны руки: открыть Firefox на
       хабе -> facebook.com -> войти." --cat D
     - НЕ поднимай четвёртый одинаковый аск, если такой уже висит (кап 5, дубли 25.08/31.08);
     - выполни FINAL STEP (heartbeat) и заверши прогон строкой о причине в 03.
   ПОЧЕМУ ЭТОТ ШАГ ЕСТЬ: класс fb-session-logged-out, 4 датированных случая (23.08, 25.08,
   31.08, 01.09). Смерть сессии замечалась ТОЛЬКО полным браузерным заходом раз в сутки ->
   FB-лейн простоял 19.08-01.09 (12 суток, 0 ответов). Сторож той же сессии живёт СНАРУЖИ,
   в cron_watchdog.py (алерт в 03, если мертва >6ч) -- §5.5, сторож не в том, что сторожит.
   Рельса чтения = Firefox (приказ оператора 01.09): куки лежат в cookies.sqlite открыто.
   ТОЛЬКО ЧТЕНИЕ: логины/куки не трогаем.

1. ПРЕДОХРАНИТЕЛЬ: python "%USERPROFILE%\.claude\scripts\fb_guard.py" status
   reply на дневном лимите или на паузе = доложи и остановись.

2. СБОР: вход через ленту уведомлений facebook.com/notifications (стена пермалинков не отдаёт - грабля 28.07). Собери посты с новыми комментами за последние ~48ч, по каждому посту - комментаторов через JS из /fb-reply §1.2, разверни свёрнутые ветки, отсей уже отвеченное (дедуп §1.4) и свои вчерашние ветки ПРОВЕРЬ на новые реплики - держать ветку 2-3 хода это штатная часть прогона.

3. ЧЕРНОВИКИ строго по /fb-reply §2 (режим ПРОВОКАТОР): отвечаем на ВСЁ, 7 из 10 с возражением/подколом, каждый второй кончается вопросом, цель ≤5 слов (потолок 7), дерзость по тезису и никогда по человеку, хард-стопы §2.5 (деньги/юридическое/медицина/политика/чужие посты) - молчание.

4. ГЕЙТ ПАЧКИ (обязателен, не на глаз): python ~/.claude/scripts/fb_reply_gate.py check <batch.json> --coverage-answered <N> --coverage-total <M>
   FAIL = переписать пачку, не постить.

5. ПОСТИНГ через готовый движок, прозу про DOM заново не писать:
   `python "%USERPROFILE%\.claude\scripts\fb_reply_post.py" --plan <plan.json>`
   plan.json = [{"author","url","text"}]; движок сам держит guard (check до, record после, пауза 300с), сам доказывает публикацию релоадом + развёрнутыми ветками + серверной меткой возраста (/fb-reply §3.8''), сам переживает три граблей Лисы (выбор композера, ввод через ActionChains, доразворачивание веток) - они описаны в его docstring. Сначала прогнать `--dry` на 2-3 позициях: прицел дешевле промаха. Судить по post_log.json (stage=done + proof), НЕ по коду возврата.
   Автор в plan.json обязан быть привязан к ТОМУ посту, под которым лежит его коммент: один человек комментирует несколько постов, и автоподстановка «первый попавшийся пост этого автора» уводит ответ в чужой тред (поймано 01.09 на Tessa [ФАМИЛИЯ]).
   Гейт Норы снят 06.08, "+" оператора на ответы под СВОИМИ постами не ждём (класс B, журналим постфактум); хард-стопы §2.5 и стоп-краны account-safety не ослаблены.

6. ЛАЙК-ХВОСТ по /fb-reply §3-бис (like_own под guard, из JS, ≤5 лайков за вызов, сверка что мы на нужном посте).

7. СОВЕТЫ ИЗ КОММЕНТОВ - в реестр кредита (alpha_credit.py add, /fb-reply §3-трис).

8. ОТЧЁТ в 03 (chat_REDACTED) через python "%USERPROFILE%\.claude\scripts\bus_send.py": сколько комментов найдено / отвечено / отложено (лимит/пауза), reply N/40, like_own N/60, сколько веток продолжено, сколько советов в кредит. Сбой = назвать КОРЕНЬ, тихий ноль запрещён.

Границы: только посты оператора; строго хаб HUB-01 (IP-гейт reglament-ip-sensitive-deystviya-tolko-s-haba); любое предупреждение FB / checkpoint = немедленный СТОП + доклад; Tier-2 - к оператору через approval.py; логин/2FA не трогаем.

FINAL STEP (выполнять ВСЕГДА, даже при пустом/заблокированном прогоне - детерминированный heartbeat для крон-сторожа): python "%USERPROFILE%\.claude\scripts\cron_heartbeat.py" fb-reply-daily
</scheduled-task>

---

**Claude:**

You've hit your weekly limit · resets Sep 6, 5am (Europe/London)

---

**User:**

Try again

---

**Claude:**

пятница, вечер, 22:15, 4 сентября 2026

Продолжаю прогон `fb-reply-daily`. Начинаю с шага 0.5 — предчек живости FB-сессии, до захода в браузер.

---

> `Bash` -- {"command": "python \"$USERPROFILE/.claude/scripts/_shared/fb_session_check.py\"; echo \"EXIT=$?\"", "description": "Предчек живости FB-сессии"}

---

> `Bash` -- {"command": "python \"$USERPROFILE/.claude/scripts/fb_guard.py\" status; echo \"EXIT=$?\"", "description": "Статус предохранителя fb_guard"}

---

> `Bash` -- {"command": "cd \"$USERPROFILE\" && python -c \"import sys,os;sys.path.insert(0,os.path.expanduser('~/.claude/scripts/_shared'));import firefox_selenium as fs;print(fs.clone_profile(r'C:\\Users\\dev\\AppData\\Roaming\\Mozilla\\Firefox\\Profiles\\646yqiss.default-release', os.path.expanduser('~/.cl

---

> `Bash` -- {"command": "wc -l \"$USERPROFILE/.claude/skills/fb-reply/SKILL.md\" 2>/dev/null; ls \"$USERPROFILE/.claude/skills/fb-reply/\"", "description": "Размер и состав скилла fb-reply"}

---

> `Bash` -- {"command": "cd \"$USERPROFILE/.claude/projects/P---WORKDIR-HUB/memory\" && for f in fb-write-via-firefox-gotchas.md fb-feed-stalls-in-hidden-tab.md always-firefox-fb-carveout-removed.md; do echo \"=== $f ===\"; cat \"$f\" 2>/dev/null; done", "description": "Читаю память по граблям FB"}

---

> `Read` -- {"file_path": "C:\\Users\\dev\\.claude\\skills\\fb-reply\\SKILL.md"}
