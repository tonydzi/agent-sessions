---
session: s_9770c627
date: 2026-10-17
words: 359
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-10-17 · Classify this Claude Code session as HUMAN or SERVICE by its CONTENT

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_9770c627` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

Classify this Claude Code session as HUMAN or SERVICE by its CONTENT.
HUMAN = a real person (dev/colleague) actively typing: natural questions, instructions in their own words, back-and-forth, corrections. Title may look technical -- judge by whether a human is conversing.
SERVICE = automated/headless run with NO human conversing: first message is a skill loader ('Base directory for this skill: ...'), a scheduled routine that runs itself and reports (digest/sync/export), an inbox-robot/machine-bus handoff, or only templated prompts + tool results.
Answer with EXACTLY ONE WORD: SERVICE or HUMAN.

=== SESSION EXCERPT ===
### dev

Ты — «Vault Janitor», ночной Sonnet-уборщик Obsidian-волта оператора на МАЯКЕ (fleet-anchor VPS; волт = /root/Obsidian/Vault-Knowledge). Находишь заметки-сироты и их логичных «родителей» и АВТО-ПРИМЕНЯЕШЬ high-confidence связи безопасного класса детерминированным применителем (одобрено оператором 2026-07-01). оператор видит итог в недельном дайджесте.
PY=/home/dev/venv/bin/python; IMP=/root/Obsidian/_imports (используй эти пути в командах).

⛔ ЖЕЛЕЗНЫЕ ПРАВИЛА:
1. БЕЗОПАСНЫЙ КЛАСС = только high-confidence, где действие — ТОЛЬКО ДОБАВИТЬ входящую [[ссылку]] в «## Связано» родителя-КОНТЕНТ-заметки. Применение — ТОЛЬКО через $PY $IMP/orphan-scan/relink_apply.py <json> --apply (детерминированный, идемпотентный, кап ≤5 на родителя, отклоняет MOC/index/битые). ТЫ САМ никогда не редактируешь заметки и не создаёшь их.
2. НЕ авто-трогай массовые классы: 07-People/person-* и родителей-MOC/index.
3. ПЕРЕД --apply всегда сначала $PY $IMP/vault_backup.py "janitor auto-relink" (git-откат).
4. ТОКЕН-ЭКОНОМИЯ: детерминированный пикер + $PY $IMP/brain_ask.py находят кандидатов; Sonnet только судит топ-K. Никогда не сканируй весь волт. Грунт — субагентами model:'sonnet'.
5. ИДЕМПОТЕНТНО: не обрабатывай сироту, уже стоящую в очереди (пикер отсекает сам).

ШАГИ:
A. ДЕТЕКТ (0 токенов): $PY $IMP/orphan-scan/janitor_pick.py → до 30 строк rel_path<TAB>basename. Вернул 0 строк = ценный слой исчерпан (не сбой) → сразу FINAL STEP.
B. СУДИ (Sonnet-субагенты, батчами ~8): на каждого кандидата субагент model:'sonnet': «Прочитай сироту <rel_path> (корень волта /root/Obsidian/Vault-Knowledge). Тема 1-
...
на 2026-10-16:** 29 сирот обработано · 17 авто-связано (HIGH, parent — обычная заметка) · 12 HIGH отклонены применителем технически (parent в `_Inbox/`, оставлены оператору в очереди) · 19 в очередь на ревью (MED) · 2 без дома. Scoped git-снимок сделан (полный `vault_backup.py` снова упёрся в посторонний tripwire 482 удалений — не трогал, не мой). `validate_links.py`: 0 новых битых ссылок. Реиндекс уже шёл другим писателем (lock, пропущено). Дайджест пуст. Хартбит `vault-janitor-nightly` поставлен.
=== END ===

---

**Claude:**

SERVICE
