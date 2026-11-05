---
session: s_b9c66e08
date: 2026-10-07
words: 237
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-10-07 · Напиши ОДИН пост для X (Twitter) на АНГЛИЙСКОМ, строго <=235 знаков, от первого лица инжен…

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_b9c66e08` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

Напиши ОДИН пост для X (Twitter) на АНГЛИЙСКОМ, строго <=235 знаков, от первого лица инженера.

История (реальная, сегодня): наш трекер откликов на вакансии показывал, что по 7 заявкам в компанию DRW не пришло ни одного ответа. Ответы приходили все 7, но засчитывались ДРУГОЙ компании (OpenAI), потому что в нашей базе компания записана слагом джоб-борда (drweng), а в письме она подписывается настоящим именем (DRW). Когда я это починил, счётчик у OpenAI упал с 8 до 1, и я принял это за регрессию и чуть не откатил верную правку. На самом деле падение у вора и есть признак успеха.

Читатель: бизнесовый человек, ведёт записи по имени (CRM, счета, заявки). Он должен понять: если инструмент сшивает записи по ИМЕНИ, а не по ключу, часть записей молча засчитана не тому, и итоговое число этого не покажет.

ЖЁСТКИЕ ЗАПРЕТЫ: никакого CTA, ничего не продаём, не зовём подписаться. Без хэштегов. Без ссылок. Без длинных тире, только дефис или запятая. Не употребляй слова slug, rail, retro. Эмоция и признание своей ошибки приветствуются.

Выдай ТОЛЬКО текст поста, без кавычек и пояснений.

---

**Claude:**

Fixed a bug today: our tracker matched replies by company name. 7 DRW rejections got counted as OpenAI, because the job board stored it under a different name than the one in the email signature.

I fixed it, saw OpenAI's count drop from 8 to 1, and almost reverted the fix thinking I'd broken something. The drop was the bug leaving.
