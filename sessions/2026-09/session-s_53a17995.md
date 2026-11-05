---
session: s_53a17995
date: 2026-09-20
words: 277
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-20 · Ты разметчик. Ниже сырые улики про человека из нашей CRM (Telegram)

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_53a17995` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

Ты разметчик. Ниже сырые улики про человека из нашей CRM (Telegram).
Верни ТОЛЬКО JSON без пояснений:
{"role":"...","company":"...","topics":["..."],"seniority":"junior|mid|senior|lead|exec|unknown"}
Не выдумывай: чего нет в уликах -- пустая строка или "unknown".

УЛИКИ:
title: Ayush ☘️
username: hackedbyayush
msg_sample: Interested | Awesome | Sure 😊 | Done bro ,  My intro :  Ayush is Client Success Manager at Crypto Promoters Global (One stop Shop for everything you need to start and Run a Web3 Project) Worked with 500+ Projects and Provided them with Exponential Results including Geojam , Alkimi , BSCPAD , Tron pad , Iconx etc.. | 1) He has "on" in last of his all usernames even his channels username   2) I found Same Profile pics of a Boy in his all 3 Alts , when I pointed it out he Immediately changed the Profile pictures but I was quick enough to Take Screenshots as proof | He used his Alt to promote his Yt channel in Kols group, I reached him out and We Finalised a deal later i Cross checked his username from the Yt channel   Once I got assured I paid him 50% and Decided to pay 50% after he will share Private video link  https://youtu.be/ALnkPlSH4Gg (the video link)   Once I completed 100% payment he stopped replying and Never Made it public, I tried to raise my voice in the Kols group but he used to delete my messages and misuse his admin Powers   And One day he kicked me out of the group | I have Solid Proofs | Hi bro he is Max  @wumon @maxliston @intermon  These all accounts are of same Pe

---

**Claude:**

```json
{"role":"Client Success Manager","company":"Crypto Promoters Global","topics":["web3","crypto","project promotion","marketing","kols"],"seniority":"mid"}
```
