---
session: s_5e33a272
date: 2026-10-09
words: 394
turns: 2
tools: "ToolSearch, WebFetch, WebSearch"
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-10-09 · Who is Vie McCoy (OpenAI, @viemccoy on X)? Give: current role, past roles, GitHub handle i…

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_5e33a272` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

Who is Vie McCoy (OpenAI, @viemccoy on X)? Give: current role, past roles, GitHub handle if any, notable work, sources URLs. Be concise, no guessing; say unknown if not found.

---

> `ToolSearch` -- {"query": "select:WebSearch,WebFetch", "max_results": 2}

---

> `WebSearch` -- {"query": "Vie McCoy OpenAI viemccoy", "mode": "standard"}

---

> `WebSearch` -- {"query": "\"Vie McCoy\" github viemccoy", "mode": "standard"}

---

> `WebFetch` -- {"url": "https://github.com/viemccoy", "prompt": "Who is this user? Name, bio, company, location, notable repos, links."}

---

> `WebSearch` -- {"query": "Vie McCoy OpenAI researcher \"McCoy\" model behavior OR \"member of technical staff\" viemccoy X", "mode": "extended"}

---

> `WebFetch` -- {"url": "https://x.com/viemccoy/status/2039434404788060530", "prompt": "Post text, date, and author bio."}

---

**Claude:**

**Vie McCoy (@viemccoy)**

- **Current role:** I can't confirm one. A search snippet of their X profile shows a post announcing they are leaving OpenAI: "I would like to announce my decision to leave OpenAI and cease my security research on existing models in order to think really hard about alignment from first principles." The post's ID suggests it was written around 1 April 2026. That is my own calculation from the ID, not a displayed date. It falls on April Fools' Day, so it could be a joke, and I couldn't open the post to check.
- **OpenAI titles:** The X bio has changed several times. Snippets show "Spellcasting Research @OpenAI", "Entropy Research @OpenAI", and later "Behavioral Insights and Applied Mythomancy @OpenAI". These are joke-style titles. I found no official job title and no OpenAI page about them.
- **Past roles before OpenAI:** Unknown. A Medium profile calls them a "cognitive science researcher and techno-optimist", but I couldn't verify that it is the same person.
- **GitHub:** `viemccoy`, display name "vie mccoy", bio "applied thaumaturgy", website camelot.wiki. It has 16 public repos and 76 followers.
- **Notable work (GitHub):**
  - `excalibur`, an agent harness (183 stars).
  - `autoloom` (39 stars).
  - `tuneforge`.
  - `claude-nine`.
  - `loomquest`.
- **Public persona:** They post about red-teaming and "internet occultism" as a route into frontier AI research.

Sources:
- [GitHub profile](https://github.com/viemccoy)
- [X profile](https://x.com/viemccoy?lang=en)
- [Leaving-OpenAI post](https://x.com/viemccoy/status/2039434404788060530)
- [Post on breaking into frontier AI research](https://x.com/viemccoy/status/2008758627063017540)
- [Medium activity page](https://medium.com/@v_363/activity)

🧒 Простыми словами: нашёл их странички в интернете. Должность в OpenAI точно назвать не могу: в профиле смешные «заклинательные» названия. Есть пост, что они ушли из OpenAI, но он мог быть первоапрельской шуткой.
