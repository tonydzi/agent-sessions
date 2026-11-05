---
session: s_d17a8a86
date: 2026-10-14
words: 1922
turns: 2
tools: "Bash, ToolSearch, WebSearch"
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-10-14 · Нужен точечный веб-поиск по первичным источникам для исследовательского дизайна, не Deep R…

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_d17a8a86` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

Machine: HUB-01 (Хаб) · Agent: Codex · Operator: dev · 2026-10-14

Нужен точечный веб-поиск по первичным источникам для исследовательского дизайна, не Deep Research и не обзорный блог.

Гипотеза оператора: малую языковую модель можно дообучать эффективнее при фиксированных данных и вычислениях, если (a) использовать интервальное расписание с фазами replay/consolidation вместо сплошной подачи данных и (b) подбирать или маршрутизировать данные по измеримому профилю способностей модели. Цель: домашний воспроизводимый эксперимент на одной consumer GPU, пригодный для публичного benchmark/GitHub demo.

Найди 8-12 первичных источников 2020-2026: peer-reviewed papers, arXiv papers с официальным кодом, официальные репозитории. Покрой data pruning/selection, curriculum/interleaving, continual learning/replay/consolidation, catastrophic forgetting, specialization or mixture-of-experts routing. Для каждого дай прямую ссылку, модель/масштаб, что реально доказано, что НЕ доказано, и применимость к малому LoRA/QLoRA эксперименту. Отдельно перечисли конфаунды: дополнительные optimizer steps, разные данные, order effects, checkpoint selection, wall-clock idle time, seed variance.

В конце предложи минимальный 2x2 factorial experiment при фиксированных unique examples, optimizer steps, tokens, base model, rank, seed budget и evaluation budget. Не антропоморфизируй модель. Не утверждай, что пауза сама по себе полезна без механизма.

---

> `ToolSearch` -- {"query": "select:WebSearch,WebFetch", "max_results": 2}

---

> `WebSearch` -- {"query": "LESS: Selecting Influential Data for Targeted Instruction Tuning arXiv github", "mode": "standard"}

---

> `WebSearch` -- {"query": "LIMA less is more for alignment arXiv; Deduplicating training data makes language models better; Beyond neural scaling laws data pruning arXiv", "mode": "standard"}

---

> `WebSearch` -- {"query": "LoRA Learns Less and Forgets Less arXiv Biderman", "mode": "standard"}

---

> `WebSearch` -- {"query": "Scaling Laws for Forgetting When Fine-Tuning Large Language Models arXiv", "mode": "standard"}

---

> `WebSearch` -- {"query": "Mixture-of-LoRA experts routing arXiv official code: LoRAHub, MoLE, MixLoRA, LoRAMoE", "mode": "standard"}

---

> `WebSearch` -- {"query": "Curriculum learning language models pretraining arXiv \"curriculum\" fine-tuning order effects data ordering \"Skill-It\" skills-based framework", "mode": "standard"}

---

> `WebSearch` -- {"query": "Experience replay continual learning language models forgetting \"Rehearsal\" continual fine-tuning LLM replay arXiv 2024 \"Simple and Scalable Strategies to Continually Pre-train\"", "mode": "standard"}

---

> `WebSearch` -- {"query": "spaced repetition / distributed vs massed training neural networks LLM \"spaced\" training schedule arXiv; \"Sleep\" consolidation replay deep learning complementary learning systems", "mode": "standard"}

---

> `WebSearch` -- {"query": "Scaling Data-Constrained Language Models Muennighoff arXiv repeated data epochs github", "mode": "standard"}

---

> `WebSearch` -- {"query": "Skill-it github HazyResearch official code; Revisiting Replay and Gradient Alignment continual pretraining arXiv; Bethune scaling laws forgetting pretraining data injection 2502.06042", "mode": "standard"}

---

> `Bash` -- {"command": "python ~/.claude/scripts/machine_stamp.py sig --model \"Sonnet 5.5\" 2>&1 | tail -2", "description": "Get fleet message signature line"}

---

**Claude:**

**Как делалось.** Я сам прогнал 10 запросов встроенным WebSearch. Рельса `web>gemini` не использовалась, это отход от плана рельс. Аннотации ниже взяты из выдачи поиска. Полные тексты статей я не читал. Данные, помеченные «(память)», я не проверял в этой сессии. Их надо сверить по первоисточнику до публичного релиза.

## Источники (12)

**Отбор и прунинг данных**

1. **LESS** (Xia et al., ICML 2024). [arXiv 2402.04333](https://arxiv.org/abs/2402.04333), код [princeton-nlp/LESS](https://github.com/princeton-nlp/LESS).
   - Масштаб: модели 7B-13B (память).
   - Доказано: отбор 5% данных по сходству градиентов (прогрев через LoRA) с примерами целевой способности часто обгоняет обучение на всём наборе. Малая модель может отбирать данные для большей.
   - Не доказано: что работает на узком домашнем бюджете. Затраты на сбор градиентов по всему пулу не входят в «эффективность».
   - Для вас: ближе всего к пункту (b). Сама техника построена на LoRA.

2. **LIMA** (Zhou et al., NeurIPS 2023). [arXiv 2305.11206](https://arxiv.org/abs/2305.11206).
   - Масштаб: 65B, 1000 отобранных примеров.
   - Доказано: на малом наборе хорошего качества получается сильный результат в экспертной оценке людей.
   - Не доказано: что причина именно в «отборе». Критики указывают, что тестовые промпты подбирали сами авторы. Контрольного сравнения «отбор против случайной выборки того же размера» нет.
   - Для вас: хорошая мотивация, но не доказательство для малой модели.

3. **Deduplicating Training Data** (Lee et al., ACL 2022). [arXiv 2107.06499](https://arxiv.org/abs/2107.06499).
   - Доказано: дедупликация снижает запоминание дословного текста в 10 раз. Нужно меньше шагов до того же качества.
   - Не доказано: перенос на дообучение маленьких наборов, масштаб здесь вообще не мой фокус.
   - Для вас: обязательный шаг предобработки, иначе «повтор» смешается с дубликатами.

4. **Sorscher et al., Beyond neural scaling laws** (NeurIPS 2022). [arXiv 2206.14486](https://arxiv.org/abs/2206.14486).
   - Масштаб: ResNet, CIFAR-10/SVHN/ImageNet. Это зрение, не языковые модели.
   - Доказано: при хорошей метрике прунинга зависимость от объёма данных становится лучше степенного закона.
   - Не доказано: для языковых моделей. Лучшие метрики дороги и требуют разметки.
   - Для вас: теоретическая рамка, прямо переносить нельзя.

**Порядок, curriculum, повторы**

5. **Skill-it** (Chen et al.). [arXiv 2307.14430](https://arxiv.org/abs/2307.14430).
   - Масштаб: LEGO-синтетика и Natural Instructions, небольшие модели (память).
   - Доказано: есть порядок освоения навыков. Онлайн-пересэмплирование смеси навыков по текущим потерям даёт выигрыш при дообучении. Это ближе всего к вашему «профилю способностей».
   - Не доказано: на реальных способностях большой модели. Цифры расходятся между версиями (36.5 против 37.5 п.п.), проверить по финальной версии. Официальный репозиторий я не нашёл.
   - Для вас: основа для (b), если считать профиль как потери по навыкам.

6. **Curriculum for LLM pretraining** (EACL 2026). [arXiv 2506.11300](https://arxiv.org/abs/2506.11300).
   - Масштаб: больше 200 моделей, до 100B токенов, предобучение.
   - Доказано: curriculum ускоряет раннюю и среднюю фазу на 18-45% шагов. Как «разогрев» перед случайной выборкой даёт до 3.5%.
   - Не доказано: для дообучения. Выигрыш с масштабом может уменьшаться.
   - Для вас: порядок сам по себе даёт эффект, значит порядок надо контролировать.

7. **Learning dynamics of curricula** (Elgaar, Amiri). [arXiv 2601.21698](https://arxiv.org/abs/2601.21698).
   - Масштаб: Pythia, до 160M для малых моделей.
   - Доказано: curriculum меняет шум градиентов и насыщение выходного слоя, а не последовательность фаз обучения.
   - Не доказано: для LoRA. Эффект зависит от размера модели и убывает с ростом.

8. **Scaling Data-Constrained LMs** (Muennighoff et al., NeurIPS 2023 и JMLR 2025). [arXiv 2305.16264](https://arxiv.org/abs/2305.16264), код [huggingface/datablations](https://github.com/huggingface/datablations).
   - Масштаб: до 9B параметров, 900B токенов, 400 прогонов.
   - Доказано: до примерно 4 эпох повторов потеря почти не отличается от уникальных данных. Дальше отдача падает.
   - Не доказано: для дообучения на инструкциях. Повторы не отличены от «разнесённых повторов».
   - Для вас: даёт честную нулевую гипотезу. Повтор данных сам по себе может быть безвреден, значит «replay-фаза» должна выигрывать именно за счёт механизма.

**Replay, консолидация, забывание**

9. **Ibrahim et al., Continual pre-training** [arXiv 2403.08763](https://arxiv.org/abs/2403.08763) (идентификатор подтверждён только по ссылке alphaXiv).
   - Масштаб: до 10B параметров, сотни млрд токенов.
   - Доказано: повторный прогрев и спад learning rate плюс replay дают результат на уровне полного переобучения. Replay сравнивался при равных вычислениях.
   - Не доказано: для LoRA. Смешаны эффекты LR-расписания и replay.
   - Для вас: прямой конфаунд, расписание LR надо фиксировать между ветками.

10. **Abbes et al., Revisiting Replay and Gradient Alignment** (CoLLAs 2025/2026). [arXiv 2508.01908](https://arxiv.org/abs/2508.01908).
    - Масштаб: Llama-семейство, 100B токенов на язык.
    - Доказано: replay и выравнивание градиентов (Meta-Experience Replay) стабилизируют обучение при малых накладных расходах.
    - Не доказано: на малом бюджете. Репозиторий не подтверждён.
    - Для вас: даёт механизм для фазы «консолидации».

11. **Biderman et al., LoRA Learns Less and Forgets Less** (TMLR 2024). [arXiv 2405.09673](https://arxiv.org/abs/2405.09673).
    - Масштаб: Llama-2 7B/13B (память), код и математика.
    - Доказано: LoRA уступает полному дообучению в обучении и меньше забывает. Кривая «обучение против забывания» у них похожа.
    - Не доказано: что результат переносится на другие домены и на QLoRA. Число токенов в версиях отличается (10B или 20B).
    - Для вас: прямое руководство по рангу и по выбору метрик забывания.

12. **Kalajdzievski, Scaling Laws for Forgetting** [arXiv 2401.05605](https://arxiv.org/abs/2401.05605), и **Béthune et al., Forgetting with Pretraining Data Injection** (ICML 2025) [arXiv 2502.06042](https://arxiv.org/abs/2502.06042).
    - Доказано: у LoRA забывание растёт степенным образом от числа шагов и параметров, и ранняя остановка его не устраняет. Подмешивание около 1% данных предобучения предотвращает забывание.
    - Не доказано: что то же верно для малых моделей и для других распределений.
    - Для вас: даёт готовое определение replay как подмешивания (контроль доли), и это дешёвая нулевая гипотеза.

**Маршрутизация и специализация (пункт b, часть про routing)**
- [MoLE](https://arxiv.org/abs/2404.13628), код [yushuiwx/MoLE](https://github.com/yushuiwx/MoLE).
- [MixLoRA](https://arxiv.org/abs/2404.15159). Репозиторий в выдаче не показан, проверить отдельно.
- [LD-MoLE](https://arxiv.org/abs/2509.25684), код [eshentw/LD-MoLE](https://github.com/eshentw/LD-MoLE).

Все три доказывают только выигрыш на своих бенчмарках при дополнительных параметрах и дополнительном роутере. Равенства по числу параметров и шагов с обычной LoRA и качества маршрутизации как отдельной причины в них нет. Для вашего эксперимента маршрутизатор лучше не вводить в первый раунд. Сначала профиль служит только для отбора данных.

**Пробел.** Работы про интервальные или «разнесённые» расписания для LLM я не нашёл. Нашёл психологию и биологию (spaced против massed) и компьютерное зрение (Wake-Sleep Consolidated Learning). Для языковых моделей прямой первичной поддержки гипотезы (a) в выдаче нет. Это не вердикт «нет такого», это «я не нашёл, поиск был ограничен». Идёт ли здесь механизм через регуляризацию, перестановку порядка или распределение градиентов, остаётся предположением.

## Конфаунды

- **Дополнительные шаги оптимизатора.** Replay-фазы часто добавляют шаги. Фиксируем общее число шагов и токенов.
- **Разные данные.** Отбор по профилю меняет состав. Фиксируем размер пула и число уникальных примеров. Затраты на отбор отчитываем отдельно.
- **Эффект порядка.** Любое «интервальное» расписание меняет порядок. Контроль: случайный порядок с теми же повторами.
- **Расписание LR.** Рестарты LR (см. источник 9) ведут к выигрышу, не связанному с replay. Держим одну кривую LR по номеру шага.
- **Выбор чекпоинта.** Только финальный или заранее объявленные шаги. «Лучший чекпоинт по dev» запрещён.
- **Простой по часам.** Пауза не меняет веса. Если в интервальной ветке есть простой, он не участвует в механизме. Механизм обязан быть выражен в данных, LR или усреднении весов, иначе «пауза» ничего не объясняет.
- **Разброс по seed.** Дисперсия LoRA велика. Нужно ≥5 seed на ячейку, парные seed для инициализации адаптера и перемешивания.
- **Утечка профиля.** Пробный набор для профиля не должен пересекаться с тестовым.
- **Дубликаты.** Без дедупликации «повтор» смешивается с дублями.

## Минимальный план 2×2

**Фиксируем.** Базовая модель 1-3B в 4-бит QLoRA, один ранг (например 16), одна кривая LR по шагам, одинаковые N уникальных примеров (скажем 5000, после дедупликации), одинаковый мультимножество примеров (каждый показан ровно k раз, например 2), одинаковое число шагов и токенов, 5 парных seed, один fixed-eval набор.

**Фактор A, расписание.**
- A0: сплошное, случайное перемешивание по эпохам.
- A1: K блоков. В каждом блоке новая порция плюс доля replay из предыдущих порций. Общее мультимножество примеров и число шагов те же, что в A0. Идеальной «паузы» нет: только смена состава данных, при желании усреднение весов между блоками.

**Фактор B, данные.**
- B0: случайные N примеров из пула.
- B1: те же N, но выбранные по профилю способностей. Профиль считаем на базовой модели по потерям на пробном наборе навыков (Skill-it) либо по сходству градиентов (LESS).

**Прогонов:** 4 ячейки × 5 seed = 20.

**Оценка.** Целевая метрика на отложенном наборе, набор удержания базовых навыков (замер забывания), плюс отдельно стоимость отбора. Анализ: двухфакторная модель с взаимодействием A×B, доверительные интервалы бутстрэпом, заранее зафиксированные гипотезы. Если A1 выигрывает только при условии A×B≠0, то эффект расписания зависит от данных, а не универсален.

**Дешёвые контрольные ветки (по бюджету, отдельно от 2×2).**
- A0 с теми же повторами, но с подмешиванием 1% данных предобучения (источник 12).
- A1 без replay-доли (только смена порядка).

Это разделяет «порядок», «повтор» и «replay» как причины.

🧒 **Простыми словами:** я нашёл 12 серьёзных работ про то, как выбирать данные и как не забывать старое при дообучении. Про «паузы между порциями» для языковых моделей прямых работ не нашлось, поэтому это пока догадка, а не факт. Чтобы честно проверить, берём четыре одинаковых по размеру прогона: обычный или с порциями, случайные данные или подобранные. Меняем только это, всё остальное держим одинаковым и повторяем по 5 раз.

🏛H · Sonnet 5.5 · 83821

Sources:
- [LESS arXiv](https://arxiv.org/abs/2402.04333), [LESS code](https://github.com/princeton-nlp/LESS)
- [LIMA](https://arxiv.org/abs/2305.11206)
- [Deduplicating Training Data](https://arxiv.org/abs/2107.06499)
- [Beyond neural scaling laws](https://arxiv.org/abs/2206.14486)
- [Skill-it](https://arxiv.org/abs/2307.14430)
- [Curriculum for LLM pretraining](https://arxiv.org/abs/2506.11300)
- [Learning dynamics of curricula](https://arxiv.org/abs/2601.21698)
- [Scaling Data-Constrained LMs](https://arxiv.org/abs/2305.16264), [datablations](https://github.com/huggingface/datablations)
- [Continual pre-training strategies](https://arxiv.org/abs/2403.08763)
- [Revisiting Replay and Gradient Alignment](https://arxiv.org/abs/2508.01908)
- [LoRA Learns Less and Forgets Less](https://arxiv.org/abs/2405.09673)
- [Scaling Laws for Forgetting](https://arxiv.org/abs/2401.05605)
- [Forgetting with Pretraining Data Injection](https://arxiv.org/abs/2502.06042)
- [MoLE](https://arxiv.org/abs/2404.13628), [MoLE code](https://github.com/yushuiwx/MoLE)
- [MixLoRA](https://arxiv.org/abs/2404.15159)
- [LD-MoLE](https://arxiv.org/abs/2509.25684), [LD-MoLE code](https://github.com/eshentw/LD-MoLE)
