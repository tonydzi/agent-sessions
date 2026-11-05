---
session: s_470af774
date: 2026-10-08
words: 3930
turns: 6
tools: "Artifact, Bash, Skill, ToolSearch, WebFetch, WebSearch, Write, computer, get_page_text, mcp__Claude_Browser__browser_batch, mcp__Claude_Browser__find, mcp__Claude_Browser__get_page_text"
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-10-08 · проведи ДР и скажи ГДЕ КУПИТЬ СЕГОДНЯ \ ЗАВТРА в СФ это

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_470af774` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

проведи ДР и скажи ГДЕ КУПИТЬ СЕГОДНЯ \ ЗАВТРА в СФ это

Найти и купить/арендовать модем или portable Wi‑Fi hotspot / роутер — коробочку, которая раздаёт интернет.  
Нужно, чтобы хорошо работал интернет в центре Сан-Франциско. Провести исследование, какой вариант/оператор лучше всего работает именно там: Verizon / T-Mobile / AT&T / 5G hotspot и т.д.

---

**Claude:**

Сессия **H49772**. Разбираюсь.

**🚂 План рельс:** живую проверку магазинов и наличия делаю САМ (WebSearch + браузер — нужны сегодняшние цены/stock, чужой LLM их не видит). На чужой бак уйдёт `second_opinion` по выбору оператора в downtown SF (codex/grok) — там нужна независимая голова, а не свежие данные.

---

> `ToolSearch` -- {"query": "select:WebSearch,WebFetch", "max_results": 5}

---

> `Bash` -- {"command": "cd ~/.claude/scripts 2>/dev/null && python rail_plan.py declare --self \"живая проверка магазинов SF (WebSearch/браузер), выбор модели хотспота, итоговый вердикт оператору\" --outsource \"second_opinion:codex,second_opinion:grok\" 2>&1 | head -20", "description": "Declare rail plan"}

---

> `WebSearch` -- {"query": "best cell network downtown San Francisco 2026 Verizon vs T-Mobile vs AT&T speed test"}

---

> `WebSearch` -- {"query": "T-Mobile 5G hotspot device 2026 buy in store prepaid data plan"}

---

> `WebSearch` -- {"query": "Verizon 5G mobile hotspot Jetpack 2026 models price in store"}

---

> `WebSearch` -- {"query": "Netgear Nighthawk M6 Pro unlocked buy Best Buy San Francisco"}

---

> `WebFetch` -- {"url": "https://carrierlytics.com/city/san-francisco-ca/", "prompt": "Report the measured median download/upload speeds, latency and reliability per carrier (Verizon, T-Mobile, AT&T) in San Francisco. Include any neighborhood-level detail for downtown / Financial District / SoMa, sample sizes and t

---

> `WebSearch` -- {"query": "Verizon prepaid hotspot plan data 100GB price 2026 \"prepaid\" mobile hotspot plans"}

---

> `WebSearch` -- {"query": "T-Mobile store Financial District San Francisco Market Street address hours"}

---

> `WebSearch` -- {"query": "Best Buy San Francisco store address [АДРЕС] hours 2026"}

---

> `mcp__Claude_Browser__preview_start` -- {"url": "https://www.bestbuy.com/site/searchpage.jsp?st=mobile+hotspot&intl=nosplash"}

---

> `WebSearch` -- {"query": "Verizon corporate store San Francisco downtown Market Street hotspot address hours 2026"}

---

> `WebSearch` -- {"query": "T-Mobile hotspot devices 2026 \"Inseego\" OR \"TCL\" OR \"Franklin\" 5G hotspot T-Mobile price"}

---

> `mcp__Claude_Browser__get_page_text` -- {"max_chars": 6000}

---

> `WebSearch` -- {"query": "Ookla Opensignal San Francisco 2026 report fastest 5G network median download carrier awards"}

---

> `mcp__Claude_Browser__browser_batch` -- {"actions": [{"name": "navigate", "input": {"url": "https://www.bestbuy.com/site/wireless-cell-phones/mobile-hotspots/pcmcat305200050002.c?id=pcmcat305200050002"}}, {"name": "get_page_text", "input": {"max_chars": 8000}}]}

---

> `WebSearch` -- {"query": "rent portable wifi hotspot San Francisco same day pickup travel wifi rental"}

---

> `WebFetch` -- {"url": "https://www.verizon.com/prepaid/plans/data-only-plans/", "prompt": "List all Verizon Prepaid data-only (hotspot/router) plans with exact data amounts and monthly prices, any 5G Ultra Wideband inclusion, and whether a device purchase is required."}

---

> `WebFetch` -- {"url": "https://prepaid.t-mobile.com/prepaid-internet", "prompt": "List all T-Mobile prepaid hotspot/tablet data plans with exact data amounts and monthly prices. Also list any hotspot devices sold with them and their prices."}

---

> `WebFetch` -- {"url": "https://www.verizon.com/internet-devices/prepaid/", "prompt": "List every prepaid hotspot device Verizon sells with exact price and network support (5G UW / C-band / mmWave). Note which are in stock."}

---

> `Bash` -- {"command": "mkdir -p \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_470af774/scratchpad\" && cat > \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_470af774/scratchpad/hotspot_secondop.md\" <<'EO

---

> `Bash` -- {"command": "cd ~/.claude/scripts && timeout 300 python llm_ask.py --class second_opinion --prompt-file \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_470af774/scratchpad/hotspot_secondop.md\" 2>&1 | tail -80", "description": "Second opinion via p

---

> `mcp__Claude_Browser__browser_batch` -- {"actions": [{"name": "navigate", "input": {"url": "https://prepaid.t-mobile.com/prepaid-internet"}}, {"name": "get_page_text", "input": {"max_chars": 6000}}]}

---

> `mcp__Claude_Browser__browser_batch` -- {"actions": [{"name": "navigate", "input": {"url": "https://prepaid.t-mobile.com/prepaid-devices?deviceType=hotspots"}}, {"name": "get_page_text", "input": {"max_chars": 5000}}]}

---

> `WebSearch` -- {"query": "T-Mobile postpaid mobile internet hotspot plan 2026 price 100GB unlimited data device"}

---

> `mcp__Claude_Browser__browser_batch` -- {"actions": [{"name": "navigate", "input": {"url": "https://www.bestbuy.com/site/searchpage.jsp?st=5g+mobile+hotspot&qp=category_facet%3DMobile%20Hotspots~pcmcat305200050002"}}, {"name": "computer", "input": {"action": "scroll", "coordinate": [700, 500], "scroll_direction": "down", "scroll_amount": 

---

> `WebFetch` -- {"url": "https://www.t-mobile.com/cell-phone-plans/affordable-data-plans/hotspots", "prompt": "List T-Mobile's current mobile hotspot data plans with exact data amounts and monthly prices (2026), including any unlimited option, deprioritization thresholds, and whether a dedicated hotspot device is r

---

> `mcp__Claude_Browser__get_page_text` -- {"max_chars": 9000}

---

> `mcp__Claude_Browser__browser_batch` -- {"actions": [{"name": "navigate", "input": {"url": "about:blank"}}, {"name": "navigate", "input": {"url": "https://www.bestbuy.com/product/netgear-nighthawk-m6-pro-5g-mmwave-wi-fi-6e-hotspot-black-unlocked/J2VY7Y4T3H"}}]}

---

> `WebSearch` -- {"query": "Netgear Nighthawk M6 MR6150 unlocked price 2026 vs M6 Pro difference buy"}

---

> `mcp__Claude_Browser__navigate` -- {"url": "https://www.bestbuy.com/product/netgear-nighthawk-m6-5g-wifi-6-hotspot-black-unlocked/J2VY7Y4CFL/sku/6530931"}

---

> `mcp__Claude_Browser__get_page_text` -- {"max_chars": 4000}

---

> `mcp__Claude_Browser__find` -- {"query": "pickup"}

---

> `WebSearch` -- {"query": "RootMetrics San Francisco metro RootScore report 2026 carrier performance"}

---

> `WebFetch` -- {"url": "https://insights.opensignal.com/reports/2026/07/usa/mobile-network-experience", "prompt": "Report per-carrier (T-Mobile, Verizon, AT&T) 5G download speed, 5G availability, reliability experience and consistent quality for the USA, and any California or San Francisco regional breakdown with 

---

> `Bash` -- {"command": "cat \"C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_470af774\\tasks\\bm3f8547v.output\" 2>/dev/null | tail -60", "description": "Check second opinion output"}

---

> `WebSearch` -- {"query": "US Mobile hotspot data only plan eSIM 2026 Warp Verizon Light Speed T-Mobile Dark Star switch networks"}

---

> `WebSearch` -- {"query": "Calyx Institute vs US Mobile hotspot unlimited data plan 2026 best data only plan hotspot"}

---

> `WebFetch` -- {"url": "https://www.usmobile.com/plans", "prompt": "List all current plans with prices, including any data-only / hotspot-only plans. State which networks are selectable (Warp/Verizon, Light Speed/T-Mobile, Dark Star/AT&T), whether eSIM activation is instant, hotspot data allowances, and whether a 

---

> `Bash` -- {"command": "cat \"C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_470af774\\tasks\\bm3f8547v.output\" 2>/dev/null | tail -100; echo \"---WC---\"; wc -c \"C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\045bb65f-

---

> `WebSearch` -- {"query": "Verizon prepaid data only plan BYOD unlocked Netgear Nighthawk M6 activate SIM compatible"}

---

> `WebSearch` -- {"query": "T-Mobile BYOD hotspot unlocked Nighthawk M6 prepaid data SIM activate 2026"}

---

> `WebSearch` -- {"query": "Verizon store Palo Alto University Avenue address hours 2026 T-Mobile Palo Alto store"}

---

> `WebSearch` -- {"query": "Best Buy nearest Palo Alto 2026 Mountain View San Carlos Sunnyvale store address hours"}

---

> `Bash` -- {"command": "wc -c \"C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_470af774\\tasks\\bm3f8547v.output\" 2>/dev/null; tail -c 3000 \"C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\045bb65f-6006-4243-813c-2a7f94a

---

> `Bash` -- {"command": "cd ~/.claude/scripts && timeout 580 python llm_ask.py --class second_opinion --engine grok --prompt-file \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_470af774/scratchpad/hotspot_secondop.md\" 2>&1 | tail -60", "description": "Second

---

> `WebSearch` -- {"query": "Inseego MiFi PRO M4 5G Verizon C-band mmWave 5G Ultra Wideband support specs 2026"}

---

> `WebSearch` -- {"query": "Orbic Speed X 5G hotspot Verizon specs C-band 5G Ultra Wideband support review"}

---

> `Bash` -- {"command": "cat \"C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_470af774\\tasks\\bs67wmrfj.output\"", "description": "Read grok second opinion"}

---

> `Bash` -- {"command": "cd ~/.claude/scripts && python llm_ask.py --list 2>&1 | head -30", "description": "List available rails"}

---

> `Bash` -- {"command": "cd ~/.claude/scripts && timeout 580 python llm_ask.py --rails grok,codex --mode all --timeout 420 --prompt-file \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_470af774/scratchpad/hotspot_secondop.md\" 2>&1 | tail -120", "description":

---

> `WebFetch` -- {"url": "https://www.rvmobileinternet.com/gear/inseego-m4000/", "prompt": "Summarize the review verdict for the Inseego MiFi PRO M4 (M4000): which carrier variants exist, prices, band support differences (mmWave, C-band), Wi-Fi version, pros and cons, and who it is recommended for versus the Netgear

---

> `WebSearch` -- {"query": "T-Mobile hotspot devices in store 2026 \"Inseego MiFi X PRO\" OR \"Franklin\" price t-mobile.com shop hotspots"}

---

> `Skill` -- {"skill": "artifact-design"}

---

**User:**

Approach this as the design lead at a small studio known for their versatility, giving every client a visual identity pitched at the treatment the task actually calls for. Make deliberate choices about palette, typography, and layout that are specific to this subject, and avoid templated designs.

## Read the request first

Calibrate treatment, not whether to design. A doc deserves the same craft as a landing page - what changes is the treatment that craft is delivered in. Format is not part of this read: author HTML, and publish Markdown only when a loaded skill explicitly instructs it - a Markdown publish keeps its filename as its title and takes almost none of the craft below, and is never a way to save time.

Many requests call for a more utilitarian treatment: a plan, a memo, a demo. Make it polished: include real typographic hierarchy, considered spacing, and a proper palette, but avoid over-designing. Most pages do not need a flashy, gigantic hero. Keep flourishes tasteful and limited.

Some requests call for an editorial treatment: a landing page, a game, an app or tool they'll keep or share.

When unsure: a well-composed page is never the wrong answer; an over-designed visual identity sometimes is.

Fundamentals below apply to everything. The editorial process after that runs only when the read above says so.

## Fundamentals for every artifact

**Honor what's already there** Look for an existing design system first - CLAUDE.md, a tokens or theme file, existing component styles. When one exists, apply it; everything below fills gaps and never overrides. Precedence is always: the user's own words, then the project's existing system, then your choices.

**Ground it in the subject.** If the subject isn't already clear, pin it: one concrete subject, its audience, and the page's single job. The subject's own world - its materials, instruments, vernacular - is where distinctive choices come from. Build with real content throughout, never lorem.

**Pair typefaces** Typography carries the page even when the page isn't about typography. Google Fonts is the one font host the Artifact CSP admits - link it directly (`<link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=...&display=swap">`); a face from anywhere else must be inlined as a @font-face data URI or it falls back silently. Either way, declare a real fallback stack. Keep running text near 65 characters wide; set a type scale and stay on it; give headings `text-wrap: balance`, body text room to breathe, and uppercase labels a touch of letter-spacing.

**Choose neutrals, don't default to them.** A pure mid-grey reads as unconsidered; a grey with a slight hue bias toward the page's accent reads as chosen. Pure white and near-black are fine grounds when they suit the subject - the point is that the neutral was picked, not inherited.

**Design both themes.** The page renders in the viewer's theme, and the viewer has three states, not two: an explicit choice stamps `data-theme="dark"` / `data-theme="light"` on the root element, and the default "system" setting stamps *nothing* - most viewers see the un-stamped document, where only `prefers-color-scheme` separates light from dark. Structure the CSS token-level for all three: the bare `:root` block defines the complete light palette (for a deliberately dark-first design, swap light and dark consistently through this whole pattern); `@media (prefers-color-scheme: dark)` redefines only the tokens, guarded as `:root:not([data-theme="light"])` so an explicit light choice beats a dark OS; `:root[data-theme="dark"]` redefines them again so the toggle also wins in the other direction. Style components through the tokens, never directly inside a media or `[data-theme]` block - a color whose only definition sits behind `[data-theme]` never applies in the un-stamped state, and the page renders one theme's text on the other theme's ground. Two more rules keep each theme resolving as a set: the artifact composites over a ground the viewer paints in *its* theme, so `body` must set an explicit `background` from a token - a transparent body silently borrows the host's ground; and every element that sets a color takes it from the same token set as the surface behind it, never a literal that only works in one theme. Before publishing, scan the stylesheet for any color declared only inside a media or `[data-theme]` block - that is the classic unreadable-artifact bug. Give the second theme the same care as the first - don't naively invert; keep contrast legible and the accent working on both grounds. A design that deliberately commits to one visual world (a neon arcade screen, a letterpress invitation) may stay single-theme - then skip the media query and stamps entirely but still paint the background and every color explicitly, so the page holds on either host ground; make it a choice, not an omission.

**Let layout do the spacing.** Lay out sibling groups with flex or grid and `gap`, not per-element margins that silently collapse or double. Wide content - tables, code, diagrams - gets `overflow-x: auto` on its own container so the page body never scrolls sideways. Reach for `font-variant-numeric: tabular-nums` wherever digits line up in columns.

**Avoid AI-generated design** AI-generated design currently clusters around a few looks: warm cream (#F4F1EA) with a serif display and terracotta accent; near-black with a lone acid-green or vermilion pop; broadsheet hairline rules with dense columns; a purple-to-blue gradient hero on white; Inter or Space Grotesk as the "safe" face; emoji as section markers; everything centered; `rounded-lg` everywhere; accent bar/rail on rounded cards. Where the user pins down a visual direction, follow it exactly - their words always win, including when they ask for one of these looks. Where nothing is specified, don't spend that freedom on one of these defaults.

**Build cleanly** Be cognizant of overlapping elements, cascade collisions, silent font fallbacks; visual bugs hide in the gap between source and output. Close every non-void element, double-quote attributes, give keyboard focus a visible state, respect `prefers-reduced-motion`. For generative or decorative graphics, reach for Canvas or WebGL rather than hand-authoring long SVG path data.

**CSS rules** When writing the CSS, watch your selector specificities. It is easy to generate classes that cancel each other out - a type-based selector like `.section` fighting an element-based one like `.cta` over padding and margins between sections. Structure the cascade so it doesn't silently undo your spacing.

**Writing the copy** Words are design material, not decoration. Write from the user's side of the screen - name things by what people recognize, not how the system is built (a person manages *notifications*, not *webhook config*). Active voice; a control says exactly what happens ("Publish", then a toast that says "Published"). Errors explain what went wrong and how to fix it - no apologies, no vagueness. Specific beats clever.

**Name the page like a product, not a caption.** The `<title>` is the artifact's name in the gallery and the browser tab, and it sets the reader's first impression of care. Give the page a real name: a short noun phrase, typically two to four words, specific to the subject - or, for a page that exists to answer one question, that question itself, which is then the page's name. Stop at the name - a title that carries its own explainer after a dash or colon reads as generated filler. The name must also identify the page among many: in the gallery it sits beside dozens of other artifacts, and a generic category label that could sit on any of them fails as a name just as surely as an appended explainer. When a candidate title pairs the name with a generic word - a greeting, a category, a page-type label - the name is the half to keep; a trim that drops the identity and keeps the generic word produces exactly the title that could sit on any page. And the rule removes explainers, it does not impose brevity: a multi-word title that already reads as one specific name is finished, and shortening it further only makes it generic. The one-sentence publish `description` is where the explanation belongs; the gallery shows it right under the title.

**Structure is information** Structural devices, numbering, eyebrows, dividers, labels, should encode something true about the content, not decorate it. Many generic designs use numbered markers (01 / 02 / 03), but that's only appropriate if the content actually is a sequence - like a real process or a typed timeline where order carries information the reader needs. Question if choices like numbered markers actually make sense before incorporating them.

**When it's a UI, not a document** A dashboard or tool is scanned and operated, not read top-to-bottom, so the craft shifts from typography to information design. Surface the summary before the detail; encode state in form as well as number - a pill, a chip, a severity stripe - so what needs attention reads at a glance. Semantic color (good / warning / critical) is separate from the accent hue and doesn't count as your accent. Give sparklines and charts the same care as type: an area fill, a faint grid, an emphasized endpoint. What's interactive should look interactive.



## Process

Before writing code, sketch a short design plan - a compact token system with color, type, and layout:
- **Color**: describe the palette as 4-6 named hex values.
- **Type**: typefaces for 2+ roles - a characterful display face used with restraint, a complementary body face, and a utility face for captions or data if needed.
- **Layout**: a layout concept in one or two sentences.

Then build, following the plan and deriving every color and type decision from it.

## When the request is editorial

The stance shifts: the client has already rejected proposals that felt templated, and is paying for a distinctive point of view. Make opinionated calls, and take one real aesthetic risk where it serves the work.

Review the design plan against the subject before building: if any part of it reads like the generic default you would produce for any similar page, revise that part, and note what you changed and why. Only after you've confirmed the plan's uniqueness do you write the code, following the revised plan exactly.

**Principles** 

- The hero is a thesis: open with the most characteristic thing in the subject's world - headline, image, live demo, interactive moment. 
- Typography carries the personality of the page. Pair the display and body faces deliberately, not the same families you would reach for on any other project, and set a clear type scale with intentional weights, widths, and spacing. Make the type treatment itself a memorable part of the design, not a neutral delivery vehicle for the content. 
- Leverage motion deliberately. Think about where and if animation can serve the subject: a page-load sequence, a scroll-triggered reveal, hover micro-interactions, ambient atmosphere. An orchestrated moment usually lands harder than scattered effects; choose what the direction calls for. However, sometimes less is more, and extra animation contributes to the feeling that the design is AI-generated. 
- Match complexity to the vision. Maximalist directions need elaborate execution; minimal directions need precision in spacing, type, and detail. Elegance is executing the chosen vision well.
- Spend your boldness in one place; keep everything around it quiet. If the accent fights the ground, shift it toward analogous or drop saturation rather than replacing it.

---

> `Bash` -- {"command": "f=\"C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_470af774\\tasks\\brqdglka5.output\"; wc -c \"$f\"; tail -c 6000 \"$f\"", "description": "Check second opinion output"}

---

> `Bash` -- {"command": "cat > \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_470af774/scratchpad/hotspot-sf.html\" <<'HTMLEOF'\n<title>Хотспот в центре SF</title>\n<link rel=\"preconnect\" href=\"https://fonts.googleapis.com\">\n<link rel=\"preconnect\" href

---

> `Write` -- {"file_path": "C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_470af774\\scratchpad\\hotspot-sf.html", "content": "<title>Хотспот в центре SF</title>\n<link rel=\"preconnect\" href=\"https://fonts.googleapis.com\">\n<link rel=\"preconnect\" h

---

> `Bash` -- {"command": "f=\"C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_470af774\\tasks\\brqdglka5.output\"; wc -c \"$f\"; cat \"$f\"", "description": "Read second opinion result"}

---

**Claude:**

Второе мнение пришло с обеих рельс и **опровергло мою первую рекомендацию** по трём пунктам. Проверяю их улики, прежде чем переписывать вывод.

---

> `WebFetch` -- {"url": "https://www.t-mobile.com/stores/pl/t-mobile-san-francisco-ca-94103-2saz/hotspots-more", "prompt": "List every hotspot device this specific store page shows, with exact price and stock status. Also report the store address, phone and today's hours if shown."}

---

> `WebFetch` -- {"url": "https://www.visible.com/plans", "prompt": "List the current Visible plans with exact monthly prices, whether taxes are included, hotspot data allowance and hotspot speed cap, and whether premium/priority data is included. Note anything about using the plan on a dedicated hotspot device."}

---

> `WebFetch` -- {"url": "https://www.androidauthority.com/t-mobile-fastest-verizon-widest-ookla-opensignal-report-3690121/", "prompt": "Which organization awarded T-Mobile 12 of 16 category awards — Ookla or Opensignal? Report the exact per-carrier 5G download/upload speeds each report gives, and which carrier each

---

> `mcp__Claude_Browser__browser_batch` -- {"actions": [{"name": "navigate", "input": {"url": "https://www.t-mobile.com/stores/pl/t-mobile-san-francisco-ca-94103-2saz/hotspots-more"}}, {"name": "get_page_text", "input": {"max_chars": 5000}}]}

---

> `WebSearch` -- {"query": "Opensignal \"12 of 16\" awards T-Mobile 2026 report Ookla Verizon coverage award which report"}

---

> `WebSearch` -- {"query": "RootMetrics San Francisco 1H 2025 RootScore tie T-Mobile 339.5 median download Verizon AT&T"}

---

> `WebSearch` -- {"query": "Franklin JEXtream RG3100 5G T-Mobile hotspot specs bands n41 n71 n25 review"}

---

> `mcp__Claude_Browser__browser_batch` -- {"actions": [{"name": "navigate", "input": {"url": "https://www.verizon.com/stores/details/california/san-francisco/sf-market-247301/"}}, {"name": "get_page_text", "input": {"max_chars": 3500}}]}

---

> `Bash` -- {"command": "python -c \"\nfrom datetime import datetime, timezone, timedelta\nu=datetime.now(timezone.utc)\nprint('UTC   ', u.strftime('%Y-%m-%d %H:%M %a'))\nprint('Lisbon', (u+timedelta(hours=1)).strftime('%Y-%m-%d %H:%M %a'))\nprint('SF PDT', (u-timedelta(hours=7)).strftime('%Y-%m-%d %H:%M %a'))\

---

**Claude:**

Панель подтвердила три реальных дефекта в моём первом выводе. Переписываю.

---

> `Write` -- {"file_path": "C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_470af774\\scratchpad\\hotspot-sf.html", "content": "<title>Хотспот в центре SF</title>\n<link rel=\"preconnect\" href=\"https://fonts.googleapis.com\">\n<link rel=\"preconnect\" h

---

> `Artifact` -- {"file_path": "C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_470af774\\scratchpad\\hotspot-sf.html", "description": "Где купить мобильный хотспот в центре Сан-Франциско сегодня: живые цены, подтверждённый сток, ловушки тарифов и вывод, пров

---

**Claude:**

**19:52 по Лиссабону · 11:52 в Сан-Франциско, четверг**

Готово: **[Хотспот в центре SF](https://claude.ai/code/artifact/s_a7e54bfa)** — живые цены, подтверждённый сток, адреса и телефоны.

## Главное

Я начал с вывода «иди в Verizon за Orbic Speed X 5G и планом 100 GB за $80». Прогнал его через две независимые модели на чужих подписках с заданием опровергнуть. Опровергли по трём пунктам, все три я проверил сам, вывод переписал.

**Что брать (две ноги, не одна):**

1. **Visible+ eSIM — $30/мес, налоги внутри.** Сеть Verizon, premium-данные без деприоритизации, хотспот без лимита по объёму со скоростью до 10 Mbps. Без магазина, активация минут за десять. Ключевое: этот тариф **никогда не падает в 128 кбит/с**, а именно обрыв, не медленность, роняет звонок.

2. **T-Mobile, 701 Market St (Market & 3rd) — Franklin JEXtream RG3100 5G за $199.99.** Страница этого магазина показывает **в наличии прямо сейчас**. Modem Snapdragon X72, Wi-Fi 7, Ethernet, два антенных порта, работает от сети без батареи. Плюс prepaid 50 GB за $50 без проверки кредита. Телефон: [ТЕЛЕФОН], открыто до 19:00, у тебя 7 часов.

Решает не отчёт, а 15 минут реального видеозвонка с ноутбука из того самого кресла, с рабочим VPN, глядя на **upload и джиттер**, а не на speedtest у окна.

## Три вещи, которые ломали мой первый вывод

**mmWave внутри зданий почти не существует:** 2.2% выборок у Verizon, около нуля у T-Mobile. Переплачивать за него незачем.

**После лимита начинается ад, и он разный.** T-Mobile prepaid → 128 кбит/с. Verizon prepaid → 3 Mbps, но только на Ultra Wideband, а внутри здания ты не на нём, значит 600 кбит/с. У Visible+ обрыва нет вообще.

**Отдельная коробочка не покупает приоритет.** T-Mobile в своей же политике пишет, что линии Mobile Internet идут ниже телефонных, а трафик с телефона обгоняет тетеринг при загрузке соты.

## По сетям честно: приборы спорят

Opensignal (июль 2026, Калифорния) даёт T-Mobile 250 Mbps против 116 у Verizon и 12 наград из 16. Ookla за 1 полугодие 2026 тоже за T-Mobile. RootMetrics, который ходит drive-тестом и ловит провалы, в 1 полугодии 2025 отдал Verizon Best 5G, Fastest 5G и Most Reliable 5G плюс первое место в 110 городах из 125.

Отдельного свежего отчёта по метро Сан-Франциско нет ни у кого. Поэтому рекомендация двуногая: две сети по $30 и $50 дешевле и надёжнее, чем одна коробочка за $600 на одном операторе.

## Что не проверено

Сток подтверждён только по T-Mobile на Market St. У Verizon наличие по сайту оператора, не по залу; страница Best Buy с остатками мне не открылась. Какой оператор повешен в DAS твоего офиса, публично не узнать вообще, это и есть причина двух ног.

🚂 **Рельсы:** веер по магазинам и живые страницы делал сам (чужой LLM сегодняшний сток не видит), панель на опровержение ушла на grok и codex, оба ответили за 206 и 275 секунд. Первая попытка second_opinion упала по таймауту 300 с, со второй попытки прошла.

🔧 **По скиллам:** подходящего скилла под «разведка покупки на земле» нет, работал руками. Кандидат на `/skill-gap` слабый: задача разовая, механизм строить не из-за одного случая.

🧒 **Простыми словами:** интернет в коробочке стоит дорого и у него есть подвох. Когда гигабайты кончаются, интернет не просто замедляется, а почти выключается, и это случается прямо посреди важного звонка. Поэтому я нашёл две вещи сразу. Первая за $30 в месяц работает через твой телефон и никогда не выключается совсем. Вторая, настоящая коробочка за $200, лежит в магазине на Market Street и ждёт тебя до семи вечера. Берёшь обе, потом сидишь в своём кафе и звонишь кому-нибудь 15 минут. Какая работает лучше, ту и оставляешь.

**19:52 по Лиссабону**
