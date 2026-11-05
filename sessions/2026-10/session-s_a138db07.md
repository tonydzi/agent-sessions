---
session: s_a138db07
date: 2026-10-18
words: 1050
turns: 3
tools: "Bash, Read, ToolSearch, WebFetch, WebSearch, Write"
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-10-18 · Мне нужна такая помпа. Найти в продаже. В чем ее фишка? Провести ДР

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_a138db07` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

Мне нужна такая помпа. Найти в продаже. В чем ее фишка? Провести ДР

E:\!CLAUDE-HUBPC-June26\downloads\photo_2026-10-17_16-53-48 (69).jpg
E:\!CLAUDE-HUBPC-June26\downloads\photo_2026-10-17_16-53-48 (70).jpg
E:\!CLAUDE-HUBPC-June26\downloads\photo_2026-10-17_16-53-48 (71).jpg

---

> `Read` -- {"file_path": "E:\\!CLAUDE-HUBPC-June26\\downloads\\photo_2026-10-17_16-53-48 (69).jpg"}

---

> `Read` -- {"file_path": "E:\\!CLAUDE-HUBPC-June26\\downloads\\photo_2026-10-17_16-53-48 (70).jpg"}

---

> `Read` -- {"file_path": "E:\\!CLAUDE-HUBPC-June26\\downloads\\photo_2026-10-17_16-53-48 (71).jpg"}

---

> `ToolSearch` -- {"query": "select:WebSearch,WebFetch", "max_results": 2}

---

> `WebSearch` -- {"query": "Steinklauber Pumpen Tauchpumpe Klarwasser Flachsauger", "mode": "standard"}

---

> `WebSearch` -- {"query": "Steinklauber submersible pump model", "mode": "standard"}

---

> `WebSearch` -- {"query": "\"Steinklauber\" Pumpe", "mode": "extended"}

---

> `WebSearch` -- {"query": "steinklauber.at Tauchpumpe Schmutzwasser Kunststoff", "mode": "extended"}

---

> `WebFetch` -- {"url": "http://www.debini.de/schildeschermaschinenverleih/pumpen.htm", "prompt": "Find any Steinklauber pump mentions, models, specs, and images descriptions."}

---

> `WebFetch` -- {"url": "https://www.steinklauber.at", "prompt": "List products: submersible pumps (Tauchpumpen), model names, specs, prices, and whether they sell online. Mention any OEM brand."}

---

> `Bash` -- {"command": "curl -sk -m 20 http://www.debini.de/schildeschermaschinenverleih/pumpen.htm | iconv -f latin1 -t utf-8 | sed 's/<[^>]*>/ /g' | grep -i -B3 -A8 steinkl | head -60; for d in steinklauber.com steinklauber.at www.steinklauber.com; do echo \"== $d\"; curl -sIk -m 10 https://$d | head -3; don

---

> `WebSearch` -- {"query": "Steinklauber SDA Tauchpumpe willhaben OR ebay", "mode": "extended"}

---

> `WebFetch` -- {"url": "https://picclick.de/Tauchmotorpumpe-SDA-1000-WA-Baugleich-261198085303.html", "prompt": "Give full listing description, specs, and which KSB model is equivalent."}

---

> `WebSearch` -- {"query": "KSB Ama-Drainer N 301 302 303 Merkmale Restwasser Schwimmer Preis", "mode": "standard"}

---

> `WebFetch` -- {"url": "https://www.motralec.com/public/fichiers/docs/Ksb-AMA-DRAINER-N-301-302-303-358.pdf", "prompt": "Extract: design features (body material, shaft seal, motor cooling, residual water level mm, free passage solids mm, float switch type, dry-run capability, max temperature, discharge connection,

---

> `WebSearch` -- {"query": "KSB Ama-Drainer N 302 SE kaufen Preis", "mode": "standard"}

---

> `Bash` -- {"command": "cd \"C:/Users/dev/.claude/projects/P---WORKDIR-HUB/s_a138db07/tool-results/\" && python -c \"\nimport sys\ntry:\n import fitz\n d=fitz.open('webfetch-1792297811835-in5sqq.pdf'); t=''.join(p.get_text() for p in d)\nexcept ImportError:\n from pypdf

---

> `Bash` -- {"command": "cd \"C:/Users/dev/.claude/projects/P---WORKDIR-HUB/s_a138db07/tool-results/\" && grep -v motralec ama.txt | sed -n '1,400p' | grep -v \"^\\s*$\" | head -220", "description": "Read the extracted catalog text"}

---

> `WebSearch` -- {"query": "KSB Ama-Drainer N 302 SE preço Portugal OR comprar", "mode": "extended"}

---

> `WebSearch` -- {"query": "KSB Ama-Drainer N 301 SE Preis 2026 shop", "mode": "extended"}

---

**Claude:**

Есть ответ по сути. Теперь регистрирую ДР по канону, чтобы веер внешних LLM перепроверил и добрал цены.

---

> `Bash` -- {"command": "cd ~/.claude/scripts 2>/dev/null; ls dr_registry.py spawn_queue.py 2>&1; python dr_registry.py --help 2>&1 | head -20; python spawn_queue.py --help 2>&1 | head -20", "description": "Check DR registry and spawn queue tools"}

---

> `Bash` -- {"command": "cd ~/.claude/scripts; python dr_registry.py new --help 2>&1 | head -30; python spawn_queue.py add --help 2>&1 | head -30", "description": "Show options for DR new and spawn add"}

---

> `Bash` -- {"command": "cd ~/.claude/scripts; python dr_registry.py new \"pump-steinklauber-ksb-ama-drainer\" --for \"покупка помпы оператору: аналог Steinklauber SDA = KSB Ama-Drainer, где купить и чем заменить\" 2>&1 | tail -5", "description": "Register new DR number in registry"}

---

> `Write` -- {"file_path": "E:\\!CLAUDE-HUBPC-June26\\docs\\dr-prompts\\DR26-10-18-HUB-01-0531-pump-ksb.md", "content": "---\ndr: DR26-10-18-HUB-01-0531\nfor: покупка помпы оператору (аналог Steinklauber SDA = KSB Ama-Drainer)\ncreated: 2026-10-18\n---\nMachine: HUB-01 (Хаб) · Agent: Claude Code · Opera

---

> `Bash` -- {"command": "cd ~/.claude/scripts; python spawn_queue.py add --task-id dr-pump-ksb-20261018 --description \"🔬 · 💧🛒 ДР помпа KSB Ama-Drainer (DR26-10-18-HUB-01-0531)\" --prompt \"/dr-fanout DR26-10-18-HUB-01-0531. Промпт: E:/!CLAUDE-HUBPC-June26/docs/dr-prompts/DR26-10-18-HUB-01-0531-pump-ksb.md

---

**Claude:**

## Что это за помпа

**Это KSB Ama-Drainer под чужой наклейкой.** Steinklauber Pumpsysteme GmbH — дилер насосов из Граца (Австрия). Их модели SDA 500 WA и SDA 1000 WA на барахолках продают с пометкой «baugleich KSB AMA-Drainer 301», то есть «конструктивно идентична». KSB — крупный немецкий производитель промышленных насосов. Корпус на твоих фото совпадает с серией Ama-Drainer N 301/302/303: сверху ручка, сбоку вертикальный выход под резьбовой штуцер, внизу сетчатая «юбка».

Круглая бобышка со штырём сверху — это, скорее всего, крепление рычага поплавкового выключателя, а сам поплавок отломан. Это я вывел по фото, документом не подтверждено 🤔.

## В чём фишка (из каталога KSB)

- **Сальники как у промышленной помпы:** три уплотнения вала и масляная камера между ними. У дешёвых помп из строительного магазина обычно одно уплотнение, поэтому они и текут.
- **Терпит горячую воду:** до 50 °C постоянно и до 90 °C эпизодически.
- **Встроенный обратный клапан:** вода из шланга не стекает обратно.
- **Нержавейка в моторной части:** корпус мотора из стали 1.4301, вал 1.4057. Корпус насоса из полипропилена с 30% стекловолокна, он не ржавеет и держит удары.
- **Мусор до 10 мм**, то есть грязная вода подходит. Откачивает до остатка около 15 мм.
- **Подшипники без обслуживания**, есть термозащита, герметичность IP68, погружение до 2 м.
- **Версия «C»** работает с морской и солёной водой.

Коротко: снаружи простая пластиковая помпа, а внутри немецкая конструкция, рассчитанная на десятилетия работы.

## Где купить (цены с сайтов на 18.10, доставка из Германии)

| Модель | Напор / расход | Цена |
|---|---|---|
| N 301 SE (аналог твоей) | 6,5 м / 10 м³/ч | [Pumpe24 €150](https://www.pumpe24.de/pumpe-ksb-ama-drainer-n301-se-mit-3m-kabel.html) (по акции, старая цена €189) · [1A-Pumpen €179](https://www.1a-pumpen.de/db/ksb-ama-drainer-n-301-se) · [DMT €213](https://dmt-onlineshop.de/Forst-Gartentechnik/Pumpen-Zubehoer/Pumpen/KSB-Schmutzwasser-Tauchmotorpumpen-Ama-Drainer-N-301-SE-neue-Ausfuehrung::401350.html) |
| N 302 SE (мощнее) | 10 м / 12 м³/ч | [1A-Pumpen €315](https://www.1a-pumpen.de/db/ksb-ama-drainer-n-302-se) |
| N 30x SE/NE | то же | плюс ручной режим без поплавка, ~€344 |

Б/у на [eBay.de](https://www.ebay.de/b/Ama-Drainer/bn_7005626437) встречается за копейки: SDA 1000 WA ушла за €17,81. В Великобритании серию N помечают как заменённую новой «Series 3» (артикулы 48242504/05). **Моя рекомендация:** бери **N 301 SE за €150–180**. Если нужен напор выше 6 метров, бери N 302.

## Про ДР

ДР зарегистрирован как **DR26-10-18-HUB-01-0531**, промпт лежит в [DR26-10-18-HUB-01-0531-pump-ksb.md](docs/dr-prompts/DR26-10-18-HUB-01-0531-pump-ksb.md). Веер внешних LLM поставлен в очередь сессий: `spawn_queue add`, ответ «OK, 232 pending». ⚠️ Очередь длинная, сам веер ещё не запущен. ДР должен добить:

- цены в Португалии (OLX PT);
- преемника Series 3;
- поплавок отдельно как запчасть: возможно, проще починить старую помпу за €20–30.

🎙 Майк: проверь, работает ли мотор. Если поплавок просто отломан, старую можно воскресить запчастью, а новая нужна только как вторая.

**Проверено:** бренд и его связь с KSB по объявлениям, характеристики по каталогу KSB (PDF, извлёк текст), цены по поиску. **Не проверено:** назначение штыря, цены в Португалии, наличие на сегодня.

🧒 **Простыми словами:** твоя помпа на самом деле немецкий KSB, только с другой этикеткой. Это как Тойота, продаваемая под чужим значком. Внутри у неё масло и тройные сальники, поэтому она служит годами. Новая такая же стоит около €150–180 в немецких магазинах.

Источники: [bdb.at Steinklauber](https://www.bdb.at/firmeninfo/STEINKLAUBER-PUMPSYSTEME-GMBH-150423), [picclick SDA 1000 WA = KSB 301](https://picclick.de/Tauchmotorpumpe-SDA-1000-WA-Baugleich-261198085303.html), [каталог KSB Ama-Drainer N](https://www.motralec.com/public/fichiers/docs/Ksb-AMA-DRAINER-N-301-302-303-358.pdf), [Anchor Pumps (Series 3)](https://www.anchorpumps.com/ksb-ama-drainer-n-301-se-ne-submersible-dirty-water-pump-240v), [geizhals](https://geizhals.de/ksb-ama-drainer-n-301-elektro-schmutzwassertauchpumpe-a1197315.html)
