---
session: s_6b95372b
date: 2026-10-02
words: 637
turns: 1
tools: "PowerShell, Read"
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-10-02 · Scheduled run: railc-login-account-a-param-20261001

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_6b95372b` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

<scheduled-task name="railc-login-account-a-param-20261001" file="C:\Users\dev\.claude\scheduled-tasks\railc-login-account-a-param-20261001\SKILL.md">
This is an automated run of a scheduled task. The user is not present to answer questions. For implementation details, execute autonomously without asking clarifying questions — make reasonable choices and note them in your output. "write" actions (e.g. MCP tools that send, post, create, update, or delete), only take them if the task file asks for that specific action. When in doubt, producing a report of what you found is the correct output.

СНАЧАЛА прочитай и исполни блок STOP-DUP: D:\Vault\Vault-Knowledge\08-Templates\seed-stop-dup-block.md. Работа уже сделана другой сессией — не дублируй, доложи чем закрыто и выключись.

OUTCOME: беседы claude.ai аккаунта «a» снова доезжают в волт, и `claudeai_sync.py` перестаёт падать в ABORT. Всё — БЕЗ рук оператора.

КОНТЕКСТ, замеренный 01.10.2026 на хабе (сессия bus-debt-drain), улики проверены дважды:
· `claudeai_sync.py` отбивает ABORT «MOC would shrink 540 -> 446 rows» — это ЗАЩИТА, не баг: в урожае нет беспед аккаунта «a», поэтому MOC бы усох.
· Аккаунт a2 забран, 9 беседы, рельса рабочая: `railc_login_a2.py` + `pull_rail_c.py --profile=a2`.
· ❗ВАЖНАЯ ПОПРАВКА К ПРЕЖНИМ ДОКЛАДАМ: «сессия Firefox на хабе разлогинена» — НЕВЕРНО. Профиль Firefox `418toca9.dev-clean-*` ЗАЛОГИНЕН в claude.ai, но под аккаунтом `[EMAIL]` (проверено запросом к /api/organizations с его куками, HTTP 200, имя организации видно). Это же знание уже стояло в docstring railc_login_a2.py от 30.08 («the Firefox cookie source is signed into bbplatinum, never a2»). Инъекция кук Firefox НЕ может дать сессию ни a2, ни a — нужен отдельный профиль.
· Дверь входа есть и не требует оператора: `~/.claude/secrets/gmail-a-apppassword.env` (пароль приложения для ящика «a») + читалка `~/.claude/scripts/_shared/magic_mail.py` (IMAP, только чтение, адрес/пароль берёт из MAGIC_MAIL_USER / MAGIC_MAIL_PASS / MAGIC_MAIL_HOST). `oauth_probe.py` подтверждает: gmail:a OK (а вот gmail:a2 и gcal:a2 мертвы, invalid_grant — это ДРУГАЯ задача).

SCOPE:
1. ПАРАМЕТРИЗУЙ, НЕ КОПИРУЙ. `railc_login_a2.py` жёстко прошит под a2 (адрес, org a673590f, профиль `_chrome_profile_a2`). Сделай из него один скрипт с параметром аккаунта (`--account a|a2`), реестр значений — в JSON рядом. Копия скрипта под каждый аккаунт ЗАПРЕЩЕНА (память measure-before-you-swap-embedder: сменную деталь делай параметром). Старое имя оставь шимом, если его кто-то зовёт по расписанию — проверь grep по scheduled-tasks.
2. ПОРЯДОК ВХОДА, не перепутай (грабли 01.10): сперва ЗАПУСКАЕШЬ скрипт (он открывает окно и ЖДЁТ ссылку, окно ожидания ~420с), и ТОЛЬКО ПОТОМ идёшь за письмом. Если забрать ссылку заранее — она протухнет, пока скрипт просит новую.
3. Ссылку входа возьми через `magic_mail.py` с паролём приложения из secrets (НЕ через Gmail-коннектор: он смотрит в a2). Положи ссылку туда, куда скрипт её ждёт ($SCRATCH/magic_link.txt). ⛔ Ссылка одноразовая: после использования УДАЛИ файл, в волт и логи она не попадает.
4. ⛔ НЕ ЖМИ «Continue with Google» — попап отдельным окном, автоматизация его не видит, вкладка вешается на спиннере (прямая мина в docstring).
5. Забери урожай: `pull_rail_c.py` для аккаунта a, затем `claudeai_sync.py` — ABORT должен уйти САМ, потому что MOC больше не усыхает. ⛔ Не обходи защиту флагом и не форси: если ABORT остался, значит урожай не полный — назови чего не хватает.
6. Проверь второй раз ДРУГИМ методом: число строк MOC до и после + имя организации в ответе /api/organizations должно стать аккаунтом «a», не bbplatinum.

DoD: (а) один параметризованный скрипт, копий нет, старый путь не сломан; (б) сессия аккаунта «a» живёт в своём профиле (улика: /api/organizations отдаёт его организацию); (в) `claudeai_sync.py` проходит без ABORT, названы строки MOC до/после; (г) magic_link.txt удалён; (д) строка в журнале поломок про класс «инъекция кук даёт ЧУЖОЙ аккаунт» через selfheal.py journal.
ГРАНИЦЫ: ⛔ пароли в формы входа НЕ вводим ни из secrets, ни из чата — только почтовая дверь (это жёсткий запрет, не лень); ⛔ автологин в ChatGPT не трогай (там профиль светит navigator.webdriver=True и это пометит аккаунт оператора роботом — отдельное решение оператора); Tier-2 — стоп и аск в чат 02.
ДОКЛАД: строкой в чат 03 через `python ~/.claude/scripts/bus_send.py HUB-01 "TASK: ..."`.
</scheduled-task>

---

> `Read` -- {"file_path": "D:\\Vault\\Vault-Knowledge\\08-Templates\\seed-stop-dup-block.md"}

---

> `PowerShell` -- {"command": "Get-Date -Format \"yyyy-MM-dd HH:mm:ss zzz\"; hostname", "description": "Get current time and hostname"}
