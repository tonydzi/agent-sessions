---
session: s_0d4ae6a5
date: 2026-10-06
words: 786
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-10-06 · Scheduled run: auto-hub-261006-hollow-guard-portability-macos

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_0d4ae6a5` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

<scheduled-task name="auto-hub-261006-hollow-guard-portability-macos" file="C:\Users\dev\.claude\scheduled-tasks\auto-hub-261006-hollow-guard-portability-macos\SKILL.md">
This is an automated run of a scheduled task. The user is not present to answer questions. For implementation details, execute autonomously without asking clarifying questions — make reasonable choices and note them in your output. "write" actions (e.g. MCP tools that send, post, create, update, or delete), only take them if the task file asks for that specific action. When in doubt, producing a report of what you found is the correct output.

ПЕРВЫМ ДЕЙСТВИЕМ переименуй себя: mcp__ccd_session_mgmt__set_session_title со значением "AUTO-hub-261006-hollow-guard-portability-macos".

Перед работой прочти $OBSIDIAN_VAULT/08-Templates/seed-stop-dup-block.md и выполни его (анти-дубль ОБЯЗАТЕЛЕН: эта ветка уже дважды терялась в гонке за прогретые слоты в ночь 06.10 — две другие сессии перетёрли слот).

# Задача: портировать сторож полых пакетов на не-Windows узлы

## Откуда это (замер, не гипотеза)
05.10.2026, сессия ДР по n8n (DR26-10-05-HUB-01-1355). Авария 02.10 на хабе HUB-01
жила ТРИ ДНЯ и держала заложников:
- роутер голосовых потерял 59 voice_task (мост отдавал 503, воркфлоу n8n Htwy1403XdfAVEEY);
- индекс RAG стоял замороженным 3 ночи (ночной реиндекс умирал на `import numpy` ->
  `No module named 'numpy._utils'`);
- `Brain Gold Eval Nightly` отчитывался exit 0, пока его выход лежал от 02.10.

Корень: обход AppData снёс `.py` из site-packages системного Python 3.12, нативные
`.pyd`/`.dll` выжили -> пакет ИМПОРТИРУЕТСЯ, но ПОЛЫЙ (`import torch` проходит,
`torch.cuda` нет). Класс `python-env-destroyed-takes-hostages`: 7 датированных случаев при
пороге 3. Тот же дефект кусал NODE-0X 07.08.2026 — реиндекс падал МОЛЧА 7 суток.

Построен сторож (всё уже есть на хабе и в зеркале транзита):
- `~/.claude/scripts/_shared/hollow_package_guard.py` — движок, проба по ПОДМОДУЛЮ;
- `_probe_hollow_guard.py` — read-only проба (шаг verify в посылках);
- `_test_hollow_package_guard.py` — регресс, 12 инвариантов, ~3с;
- рот: выход `~/.claude/state/hollow_package_guard.json`, зарегистрирован в
  `output_freshness` как артефакт `hollow-package-guard`, max_age_h=30;
- OS-задача `hollow-package-guard` ежедневно 04:50, пускается из `~/.brain-venv`, чтобы
  переживать смерть системного python;
- посылка `hollow-package-guard-20261005` (payloads + CHECKSUMS + MANIFEST) на
  HUB-01 и NODE-0X-2023PAL, подписана Ed25519.

Доказано на хабе: задача отработала сама (LastTaskResult=0), выход перезаписан
20:25:34 -> 20:30:22, `output_freshness` видит строку, регресс GREEN.

## ЧТО НЕ СДЕЛАНО — твоя работа
Деталь ХАБО-ФОРМНАЯ. Реестр `interpreters()` знает три Windows-пути: системный Python312,
`~/.brain-venv`, `D:/Vault/_imports/.venv-diar`. На macOS и Linux он вернёт ПУСТОЙ
список, сторож выдаст OK при нуле проб, а `not_judged` назовёт все три. То есть на
не-Windows узле это СЛЕПОЙ ПРИБОР, а не рабочий.

Отставшие ПОИМЁННО: NODE-0X, NODE-0X, NODE-0X, FLEET-ANCHOR (linux VPS).
⛔ NODE-0X и EDITKA НЕ трогай — не-антоновские узлы, канон read-only.

## Шаги
1. Заменить захардкоженные пути на обнаружение интерпретаторов по ОС: `sys.executable`,
   `shutil.which("python3")`, venv'ы узла. Обойти ВСЕ, не один: в сессии 05.10 я заявил
   «.brain-venv не существует», потому что искал в двух каталогах из трёх, а он лежит в
   `C:\Users\dev\.brain-venv` (память check-all-places-not-one).
2. Пробы задавать ПО ПОТРЕБИТЕЛЮ узла. Правило из движка: пишем РОВНО тот import, который
   делает живой потребитель, и ничего больше. Я внёс `torchvision.io` для `.brain-venv`,
   которого там нет и который никто не импортирует — сторож честно покраснел на моей
   ошибке. Красный без потребителя = шум, а не сигнал.
3. ПРОБА ПО ВЕРХНЕМУ УРОВНЮ НЕ ГОДИТСЯ: у полого пакета она ПРОХОДИТ. Только подмодуль.
4. Сохранить инвариант «красный ПО ПРАВИЛЬНОЙ ПРИЧИНЕ»: первая версия самотеста прошла,
   покраснев `No module named 'fakehollow'` — то есть доказала реакцию на ОТСУТСТВУЮЩИЙ
   пакет, а не на полый, и была фальшивой. Сейчас тест требует в причине отсутствующую
   начинку (`cannot import name 'guts'`).
5. Сохранить инвариант «тест пишет в ВРЕМЕННЫЙ путь»: первая версия положила в боевой
   артефакт фикстуру `test-cheap` (память test-fixtures-write-into-live-secrets).
6. Доставка: груз уже в `_transit/scripts-from-HUB-01/_shared/` (курьер
   `publish_scripts.py --kind scripts`, md5 сверены по трём файлам). Принимающая половина —
   `fleet_tools_sync.py --source HUB-01 --kind scripts --apply`.
   ВАЖНО: `scripts/_shared` НЕ СИНКАЕТСЯ — с 30.09 `~/.claude/.stignore` это БЕЛЫЙ СПИСОК
   ровно канонических документов. Докстринг `output_freshness.py` про «путешествует ровно
   одна папка scripts/_shared/**» ПРОТУХ — поправь его заодно, это найденный дефект.
7. На каждый не-Windows узел — своя посылка через `deploy_register.py`. Гейты там строгие
   и ПРАВЫ (в сессии 05.10 они поймали меня 4 раза из 4): `prose_tier1` (apply одной
   командой), `test_as_step` (verify read-only пробой, не тестом), `nodelocal_path`
   ($VARS вместо абсолютных путей), `sender_only_cargo` (груз обязан быть достижим
   получателю). Не обходи их — переделай шаг.
8. Отпечаток автора: коммит с трейлерами Assisted-by/Machine/Account/Operator, либо строка
   в `change_ledger.py add`, если коммит снял авто-бэкап-демон (он транспорт, не автор).

## Приёмка
Красный/зелёный на КАЖДОМ целевом узле: сторож краснеет на подсунутом полом пакете и
зеленеет на целом, выход пишется и виден сторожу свежести. «exit 0» без свежего выхода НЕ
считается: в этой истории ровно ложная зелень дала 3 дня тишины. Итог положить в чат
целиком (оператор читает сессию сам) и строкой в `session_retro_digest.py add`.

Канон: CLAUDE.md §5.5 (сторож не живёт в том, что сторожит; рутина называет свой выход;
прибор не имеет права быть слепым), §5.8 (тест+док+счётчик), §7.3-бис (починка
раскатывается на ВЕСЬ флот, отставшие названы поимённо), §10.3 ($VARS, не хардкод).
Память: hub-python312-stdlib-destroyed-20261002, check-all-places-not-one,
instrument-must-not-be-blind, red-first-or-the-test-is-fake, zero-harvest-is-not-green.
</scheduled-task>

---

**Claude:**

You've hit your session limit · resets 3:10pm (Europe/London)
