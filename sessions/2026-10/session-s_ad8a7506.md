---
session: s_ad8a7506
date: 2026-10-18
words: 1113
turns: 2
tools: "Grep, ToolSearch, WebSearch"
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-10-18 · Нужно для Mac Studio оператора подобрать несколько нецензурированных LLM-моделей, которые…

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_ad8a7506` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

Нужно для Mac Studio оператора подобрать несколько нецензурированных LLM-моделей, которые будут нормально работать на его железе: 128 ГБ оперативки, текущий диск 2 ТБ.

Что нужно выяснить:
- какие модели подойдут для Mac Studio и будут давать комфортную скорость токенов;
- сколько места обычно занимают такие модели;
- хватит ли диска на 2 ТБ, если ставить несколько моделей;
- если 2 ТБ мало — быстро купить диск на 4 ТБ или больше, а диск на 2 ТБ вернуть.

Требования к моделям:
- нецензурированные / uncensored;
- без жёстких safety-ограничений и отказов на бизнес-задачи;
- не «обрезанные» и не «заблокированные» по ответам;
- желательно уровня нормальных современных Llama-подобных моделей;
- должны быстро реагировать и стабильно работать локально на Mac Studio;
- рассмотреть Llama и похожие модели, возможно через MLX/GGUF/Ollama/LM Studio, с учётом совместимости с Apple Silicon.

Также нужно проверить, есть ли такие нецензурированные модели в открытом доступе или уже поднятые где-то онлайн, чтобы можно было пользоваться через интернет. Главное условие — без цензурного фильтра.
__Перевела: GPT-5.5 + whisper__

• • • • •

Нужно для оператора подготовить подборку LLM для Mac Studio с 128 ГБ оперативки:

- Какие модели можно поставить локально и чтобы они работали с комфортной скоростью вывода токенов.
- Нужны нецензурированные / uncensored модели без жёстких ограничений, которые могут отвечать на широкий круг бизнес-вопросов.
- Рассмотреть DeepSeek, LLaMA и другие подходящие open-source модели.
- Желательный уровень качества: примерно Haiku / Sonnet, Opus не обязательно, но можно рассмотреть.
- Важно указать размер каждой модели на диске и понять, хватит ли текущего диска на 2 ТБ.
- Если 2 ТБ недостаточно, быстро купить диск на 4 ТБ или больше, а купленный 2 ТБ вернуть.
- Также проверить, есть ли уже поднятые в интернете uncensored-модели, к которым можно получить доступ онлайн без локальной установки.
__Перевела: GPT-5.5 + 11labs__

---

> `ToolSearch` -- {"query": "select:WebSearch", "max_results": 1}

---

> `Grep` -- {"pattern": "(?i)mac studio|abliterat|uncensored|нецензур", "path": "D:\\Vault\\Vault-Knowledge", "output_mode": "files_with_matches", "head_limit": 20}

---

> `Grep` -- {"pattern": "(?i)mac studio.{0,200}(llm|ollama|mlx|abliterat|uncensor)", "path": "D:\\Vault\\Vault-Knowledge\\_DR-Registry.md", "output_mode": "content", "head_limit": 10}

---

> `WebSearch` -- {"query": "best abliterated uncensored models Mac Studio 128GB MLX 2026", "mode": "extended"}

---

> `WebSearch` -- {"query": "huihui abliterated Qwen3 GLM gpt-oss 120b MLX tokens per second M4 Max 128GB", "mode": "standard"}

---

> `WebSearch` -- {"query": "uncensored LLM API online hosted Venice AI uncensored model 2026", "mode": "standard"}

---

> `WebSearch` -- {"query": "gpt-oss-120b abliterated MLX OR GLM-4.5-Air abliterated MLX size GB tok/s Mac", "mode": "standard"}

---

> `WebSearch` -- {"query": "best 4TB Thunderbolt 5 external SSD Mac Studio LLM models price 2026", "mode": "standard"}

---

**Claude:**

Диск докупать не нужно. Хороший набор из 5–6 нецензурированных моделей займёт примерно 250–400 ГБ, так что 2 ТБ хватает с большим запасом. Диск на 4 ТБ я не покупал и 2 ТБ не возвращал: это покупка, на неё нужно твоё «да». По цифрам она не нужна.

## Что ставить на Mac Studio с 128 ГБ

В таблице модели «abliterated», то есть с хирургически снятыми отказами, и uncensored-файнтюны. Все есть в форматах MLX и GGUF, работают через LM Studio или Ollama. Скорость взята из замеров сообщества на M4 Max 128 ГБ. На M3 Ultra генерация примерно такая же или немного медленнее.

| Модель | Место на диске | Память в работе | Скорость | Роль |
|---|---|---|---|---|
| **Huihui Qwen3-Next-80B-A3B abliterated** | ~45 ГБ (4-бит) | 43 ГБ | **~89 ток/с** | основная «умная», уровень около Haiku |
| **gpt-oss-120b abliterated** (MXFP4) | ~60–65 ГБ | ~60 ГБ | **65–75 ток/с** | вторая сильная, хороша в рассуждениях |
| **Huihui Qwen3.5-35B-A3B abliterated** | ~20 ГБ | 19 ГБ | **~111 ток/с** | быстрая для каждого дня |
| **Qwen 3.6/3.8-27B uncensored** (обычная модель, без MoE) | 16–24 ГБ | ~20 ГБ | ~20–30 ток/с (моя оценка, не замер) | код, агенты, картинки |
| **Dolphin Mistral 24B Venice Edition** | ~14 ГБ | ~15 ГБ | быстрая | изначально сделана без цензуры |
| Llama 4 Scout abliterated | ~60 ГБ | ~60 ГБ | 25–35 ток/с | если нужна именно Llama; по качеству слабее Qwen |
| DeepSeek V4-Flash IQ2 (эксперимент) | ~100+ ГБ | впритык | 27–34 ток/с | только поиграть: 2-битное сжатие портит качество |

**Моя рекомендация:** Qwen3-Next-80B + gpt-oss-120b + Qwen3.5-35B + Dolphin 24B. Вместе это около 140 ГБ на диске.

## Что честно надо знать

1. **Уровень Sonnet локально на 128 ГБ недостижим.** Модели такого класса (GLM-5.1 abliterated и подобные) требуют от 256 ГБ памяти. На 128 ГБ потолок примерно Haiku, и для бизнес-задач этого хватает.
2. **Abliteration немного снижает качество.** Отказы убираются, модель чуть «тупеет». Поэтому я ставил бы рядом и обычную версию той же модели, если место позволяет.
3. **Скорость падает на длинных текстах.** Цифры в таблице для контекста около 1 тысячи токенов. На документах в десятки тысяч токенов первая часть ответа будет приходить заметно дольше.

## Онлайн без цензуры, без установки

- **Venice AI:** сайт и API, модель Venice Uncensored 1.2. Стоит $0.20 за миллион токенов на входе и $0.90 за миллион на выходе.
- **OpenRouter:** там есть `venice/uncensored`, включая бесплатный вариант `:free`, и Dolphin Mistral 24B Venice Edition. Подключается одним ключом к любому клиенту.
- Через Hugging Face Inference Endpoints можно поднять любую abliterated-модель из таблицы. Это поштучно платный API, значит Tier-2 и нужен твой ОК.

## Про диск

- **Хватит ли 2 ТБ:** да. Даже «всё подряд» (7 моделей из таблицы плюс обычные версии к ним) это около 600 ГБ.
- **Если всё же нужен внешний диск:** 4 ТБ с Thunderbolt 5, например LaCie Rugged SSD Pro5, стоит около $690. Он работает только с M4 Pro или M4 Max. Покупать сейчас смысла не вижу.

**Чего я не проверил:** какой чип стоит в Mac Studio (M4 Max или M3 Ultra) и сколько места на нём свободно на самом деле. Ставить модели на сам Mac я не пробовал, все скорости взяты из чужих замеров.

**🎙 Майк:** не тратим деньги на диск. Если хочется уровня Sonnet без цензуры, нужен Mac на 256 ГБ памяти, а не диск побольше.

## 🧒 Простыми словами
Модели как фильмы на флешке: каждая весит от 15 до 65 ГБ. Шесть штук влезают в 2 ТБ, и ещё остаётся много места. Самая быстрая отвечает быстрее, чем ты читаешь. Самая умная примерно как Haiku, до Sonnet домашний Mac с 128 ГБ не дотянет. Если ставить ничего не хочется, есть Venice и OpenRouter: там такие модели уже работают в интернете.

Sources:
- [InsiderLLM: Best Local LLMs for Mac 2026](https://insiderllm.com/guides/best-local-llms-mac-2026/)
- [Apidog: 7 Best Uncensored LLMs 2026](https://apidog.com/blog/best-uncensored-llms/)
- [LocalClaw: Mac Studio M3 Ultra 128GB](https://localclaw.io/hardware/mac-studio-m3-ultra-128gb)
- [oMLX benchmark: Qwen3-Next-80B abliterated](https://omlx.ai/benchmarks/iwwd9e1y)
- [oMLX benchmark: Qwen3.5-35B abliterated](https://omlx.ai/benchmarks/a3kel9di)
- [oMLX benchmark: gpt-oss-120b](https://omlx.ai/benchmarks/xoeb7x9j)
- [HF: gpt-oss-120b MLX](https://huggingface.co/inferencerlabs/openai-gpt-oss-120b-MLX-6.5bit/blob/0edc64049e30bbcc7ec4a8ee3ad7d8089aac81bc/README.md)
- [OpenRouter: venice/uncensored](https://openrouter.ai/models/venice/uncensored)
- [OpenRouter: Dolphin Mistral 24B Venice](https://openrouter.ai/cognitivecomputations/dolphin-mistral-24b-venice-edition:free/api)
- [Tech-Insider: Venice vs Ollama vs Mistral](https://tech-insider.org/venice-ai-vs-ollama-vs-mistral-uncensored-models-2026/)
- [Macworld: best Mac SSD](https://www.macworld.com/article/353990/best-mac-portable-ssd-reviews-recommendations.html)
