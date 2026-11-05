---
session: s_bed891fa
date: 2026-10-07
words: 1233
turns: 3
tools: "ToolSearch, WebFetch, WebSearch"
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-10-07 · Who is Mehdi Tabdili (email [EMAIL]), founder of Saena AI Group (saenaaigroup.com), an Ant…

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_bed891fa` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

Who is Mehdi Tabdili (email [EMAIL]), founder of Saena AI Group (saenaaigroup.com), an Anthropic Claude implementation partner / CPN firm? Find: his background, LinkedIn/company size, whether Saena AI Group is listed in Anthropic's official Claude Partner Network directory, and when the company was founded. Also: what exactly does the Anthropic Claude Partner Network (CPN) require to join, and are there other routes to resell/implement Claude for B2B (e.g. AWS Bedrock / GCP Vertex partner resale, Anthropic's referral or solutions partner tracks)? Answer concisely with sources.

---

> `ToolSearch` -- {"query": "select:WebSearch,WebFetch", "max_results": 5}

---

**Claude:**

Starting research on Mehdi Tabdili / Saena AI Group and the Anthropic Claude Partner Network — this is a quick factual lookup, so I'll run it myself via web search rather than routing it out.

🚂 Рельсы: это разовый фактологический поиск (не DR/стратегия) → делаю САМ через WebSearch, outsource не нужен — объём не тянет на класс `web>gemini`.

---

> `WebSearch` -- {"query": "Mehdi Tabdili Saena AI Group founder"}

---

> `WebSearch` -- {"query": "Saena AI Group saenaaigroup.com Anthropic Claude partner"}

---

> `WebSearch` -- {"query": "Anthropic Claude Partner Network CPN how to join requirements"}

---

> `WebFetch` -- {"url": "https://saenaaigroup.com/", "prompt": "Extract all information about: company founding date, founder background (Mehdi Tabdili), company size/team, claims about being an Anthropic Claude Partner Network member, services offered, any badges/logos referencing Anthropic."}

---

> `WebFetch` -- {"url": "https://claude.com/partners", "prompt": "Does this page list or let me search for a partner named \"Saena AI Group\" or \"Saena\"? What does the page say about how the Claude Partner Network / CPN works, tiers, and how to find/verify a partner in an official directory?"}

---

> `WebSearch` -- {"query": "\"Saena AI Group\" LinkedIn company"}

---

> `WebFetch` -- {"url": "https://saenaaigroup.com/about", "prompt": "Extract any bio information about the founder (Mehdi Tabdili), company founding date, team size, headquarters, and any claims about Anthropic Claude Partner Network membership or certification."}

---

> `WebSearch` -- {"query": "site:claude.com partners services directory list"}

---

> `WebSearch` -- {"query": "Mehdi Tabdili World Bank quantitative Saena"}

---

> `WebFetch` -- {"url": "https://partnerhub.claude.com/directory/", "prompt": "Search this directory page's content for any partner named \"Saena\" or \"Saena AI Group\". List what partners are visible and whether there's a search/filter mechanism described."}

---

> `WebSearch` -- {"query": "\"Saena AI Group\" partnerhub.claude.com OR \"claude.com/partners\" directory"}

---

> `WebSearch` -- {"query": "Anthropic AWS Bedrock Marketplace reseller partner Claude GCP Vertex partner resale program"}

---

> `WebFetch` -- {"url": "https://partnerhub.claude.com/directory/?q=saena", "prompt": "Does this page show any search results for \"saena\"? Report exactly what partner names, if any, appear, and whether the page says \"no results\" or similar."}

---

> `WebSearch` -- {"query": "Anthropic \"referral partner\" OR \"solutions partner\" program Claude become partner reseller B2B"}

---

> `WebFetch` -- {"url": "https://saena.ai/about", "prompt": "Extract founder bio (Mehdi Tabdili), founding year of the company, team size, and relationship (if mentioned) to \"Saena AI Group\" / saenaaigroup.com."}

---

**Claude:**

Here's what I found. This is a thin, mostly self-asserted web presence — flagging that clearly below rather than overstating confidence.

## Mehdi Tabdili
- **Day job:** Investment Officer at the **World Bank Group**, where he builds quantitative/risk tools for a $100B+ internal portfolio and for 60+ central bank clients; previously Financial Officer at World Bank (2014–2019) building C++/Java pricing tools for fixed-income/derivatives desks. 16+ years in quant finance.
- No independent bio confirms an AI/ML or enterprise-software background — his documented track record is quantitative finance, not AI implementation.

## Saena — two faces, one domain
- **saena.ai** was originally pitched as an "AI investment platform for retail investors" (AI-driven stock/crypto model portfolios), per Tracxn listed as founded **2020**, Washington DC, unfunded.
- **saena.ai/about now 301-redirects to saenaaigroup.com** — i.e., it's the same underlying entity/domain, repositioned as "Saena AI Group," a Claude-implementation consultancy for financial services/federal/regulated industries (NetSuite/CRM integration, workflow automation, agentic AI, training).
- No separate LinkedIn company page, employee count, or founding date specific to "Saena AI Group" turned up — no sign of a team beyond Tabdili himself in anything public.

## Is Saena AI Group in Anthropic's official CPN directory?
**Not that I could find — but I can't rule it out with certainty.** saenaaigroup.com's own footer claims "Certified Claude Partner · Official Member," but:
- Anthropic's official directory (**partnerhub.claude.com/directory**) is a JS-rendered, filterable search tool. A static fetch of it and a `?q=saena` query both showed only the visible Global Premier logos (Accenture, Deloitte, BCG, etc.) with no Saena match and no "0 results" message either — meaning the fetch likely isn't rendering the live search index fully. Per my own search-completeness standard, this is "I didn't find it," not "it doesn't exist."
- Given the lowest tier (**Select**) requires **10 active Claude-certified individuals + 2 production joint customers + 1 public story**, and there's no evidence of a team beyond one person, it would be surprising if Saena AI Group cleared even the entry bar — but the self-badge could also just be unverified marketing.

**Recommendation if this matters for a decision:** check `partnerhub.claude.com/directory` live in a browser and search "Saena" directly, rather than trust either their badge or my static fetch.

## What the CPN (Services Track) actually requires
Launched/formalized June 3, 2026, backed by a $100M fund, free to join:
| Tier | Certified people | Production joint customers (trailing 12mo) | Public stories |
|---|---|---|---|
| Select | 10 | 2 | 1 |
| Preferred | 100 | 15 | 3 |
| Global Premier | 1,000 | 100 (3+ regions) | 15 + joint biz plan |

Hard requirement at every tier: **at least one person holding the Claude Certified Architect (CCA) credential**, via Anthropic Academy. POCs/pilots don't count — deployments must be in production, with client references willing to talk to Anthropic.

## Other routes to resell/implement Claude for B2B
1. **AWS Bedrock Marketplace — Anthropic Authorized Reseller.** A separate, Anthropic-gated accreditation (stricter than other Bedrock model resale) — companies like Cloudvisor, Classmethod, Skaylink, Solita, Opti9 have it. Lets a reseller bill Claude usage directly to enterprise customers bundled with their own consulting.
2. **Claude for Enterprise Referral Partner program** — commission for referring qualified orgs who become Claude for Enterprise customers; much lower bar than CPN.
3. **GCP Vertex AI** — Claude models are available there, but I found no equivalent "authorized reseller" partner program for Vertex specifically (vs. the explicit AWS one) — treat as "not found," not confirmed absent.
4. **Powered by Claude directory** — for product companies built on Claude (not implementation/reselling), separate from the Services Track.

Sources: [Saena AI Group](https://saenaaigroup.com/), [saena.ai](https://saena.ai/), [Mehdi Tabdili LinkedIn](https://www.linkedin.com/in/mehdi-tabdili-a968729/), [Saena — Tracxn](https://tracxn.com/d/companies/saena/__vZfB8xvOKPlLcvcRyQITmk1s7V1rTjKubVu_ywBOUtw), [Claude Partners](https://claude.com/partners), [Claude Partner Hub Directory](https://partnerhub.claude.com/directory/), [Anthropic: $100M for the Claude Partner Network](https://www.anthropic.com/news/claude-partner-network), [Anthropic: Services Track and Partner Hub](https://www.anthropic.com/news/services-track-partner-hub), [Cloudvisor — Anthropic Authorized Reseller for Bedrock](https://www.insidenova.com/online_features/press_releases/cloudvisor-becomes-an-anthropic-authorized-reseller-for-amazon-bedrock-bringing-claude-to-startups-on-aws/article_s_453ed36e.html), [Become a Claude for Enterprise referral partner](https://www.anthropic.com/referral?p=969)

🧒 Простыми словами: Мехди — финансист из Всемирного банка (считает риски на $100 млрд портфеле), не AI-инженер. Его сайт сменил вывеску с «инвестплатформы» на «мы внедряем Клода» и сам себе написал в подвале «мы официальный партнёр Anthropic» — но в настоящем списке партнёров Anthropic я его не нашёл (хотя поиск был не стопроцентный, сайт у них с JS). Войти в партнёрскую сеть реально — бесплатно, но нужно минимум 10 сертифицированных людей и 2 реальных клиента в проде, а у него не видно команды вообще. Проще и быстрее для реселлинга Клода — через AWS Bedrock (туда уже есть отдельная, тоже проверяемая Anthropic-ом, программа реселлеров).
