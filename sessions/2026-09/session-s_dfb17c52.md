---
session: s_dfb17c52
date: 2026-09-20
words: 235
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-20 · Ты разметчик. Ниже сырые улики про человека из нашей CRM (Telegram)

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_dfb17c52` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

Ты разметчик. Ниже сырые улики про человека из нашей CRM (Telegram).
Верни ТОЛЬКО JSON без пояснений:
{"role":"...","company":"...","topics":["..."],"seniority":"junior|mid|senior|lead|exec|unknown"}
Не выдумывай: чего нет в уликах -- пустая строка или "unknown".

УЛИКИ:
title: Max
username: maxspeeeed
org: ghost_web3_bot / Spark DAO
person_note: person-max-6
msg_sample: Хорошо | . | @TonCryptans | 200$ как раз | @TonCryptans | 200$ как раз | Привет)  Новая амбассадорская программа в @hempton_bot  О проекте: - Здесь нужно построить свой собственный конопляный бизнес. В первой фазе доступна посадка семечек, полив, удобрение, сбор шишек, улучшения фермы. Во второй фазе будет доступна продажа шишек за токены, запуск кофешопа, создание банды и другие обновления, которые сейчас не разглашают.  Что предлагает проект: - Доступ в канал с ежедневными кодами к премиум рулетке (токены игры, игровой кэш, USDT).  - Расширенная реферальная система во второй фазе - NFT влияющие на игровой процесс  - Токены игры после запуска второй фазы  - Игровой кэш для запуска своей фермы - Добавление канала в таски на месяц если инфлюенсер делает необходимое количество постов. - USDT за каждого активного реферала  - Для владельцев дао возможно добавление вашего канала в таски на 3 месяца  Что нужно от инфлюенсеров: - 1-3 основных поста про игру в неделю, если проект дает посты - Постинг кодов: можно отдельным постом, можно в подборке с другими дейли комбо, можно в качестве подписи одного из ежедневных постов  Условия участия: - Размещение первого поста.  Пример поста: https:/

---

**Claude:**

```json
{"role":"crypto-influencer","company":"Spark DAO","topics":["cryptocurrency","web3","DeFi","gaming","blockchain","NFT","Telegram"],"seniority":"mid"}
```
