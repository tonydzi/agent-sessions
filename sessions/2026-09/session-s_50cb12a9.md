---
session: s_50cb12a9
date: 2026-09-22
words: 234
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-22 · Ты разметчик. Ниже сырые улики про человека из нашей CRM (Telegram)

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_50cb12a9` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

Ты разметчик. Ниже сырые улики про человека из нашей CRM (Telegram).
Верни ТОЛЬКО JSON без пояснений:
{"role":"...","company":"...","topics":["..."],"seniority":"junior|mid|senior|lead|exec|unknown"}
Не выдумывай: чего нет в уликах -- пустая строка или "unknown".

УЛИКИ:
title: Alk0n0lik
username: Alk0n0lik
org: Titan22
person_note: person-vasiliy
msg_sample: Привет, сори что задержался) Решалось мое нахождение дальше в команде и я решил её покинуть | Да, давай я как раз с небольшого больничного вышел | Сейчас рынок тяжелый поэтому готов вашим друзьям уступить по цене | Привет, мы как раз недавно сделали очень понятную и простую презентацию по запуску мемов  https://drive.google.com/file/d/1bp8S4rLTUD7_0XzTBEfn-ESSdNa9Tygk/view?usp=sharing | Titan22 is a modern market maker that combines technology and professionalism of the team. Our main goal is to bring income using market imperfections. We also provide a full service with a full trader and support team available 24/7.  Here are the main areas in which we work:  DEX: - all chain - volumetric timing - sales with minimal pressure on the market - organic share sales - price support / aggressive selling - snipe token - Protection from MEV  CEX: - CEX access assistance - liquidity provision and spread narrowing (grid) - proper candlestick construction (candle closer) - volume management - increasing the depth of bets - price equalization, neutralization of arbitrage windows  Links Website | Twitter | Deck | Meet | Titan is a crypto hedge fund that focused on market making: improving the e

---

**Claude:**

```json
{"role":"trader","company":"Titan22","topics":["crypto","market_making","DEX","CEX","trading","tokenomics"],"seniority":"mid"}
```
