---
session: s_1cd95dfa
date: 2026-10-29
words: 536
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-10-29 · Read-only independent review of provisional solar purchase opinion, do not execute actions…

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_1cd95dfa` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

Read-only independent review of provisional solar purchase opinion, do not execute actions. House consumes 4643kWh/30days, tariff marginal 0.22646637 EUR/kWh VAT included. Quote latest evidence: 29.7kWp panels, 3xHuawei SUN2000-12K-MAP0 three-phase, SmartGuard63A-T0, one LUNA2000-21-S1 20.7kWh; 20.7kVA grid. Unverified shading half array reported installer. Ideal PVGIS south30 Sintra47.8MWh/year. I favor Huawei architecture but want priced2x12K alternative because DC/AC1.24 versus0.825 for3; not conclude third is unnecessary without string voltages/currents/phase backup demand. Battery may provide under4hours at average6.45kW, not whole night. Economic savings must exclude fixed grid fees and include forgone export/battery losses; no quote total retrieved yet. Where might I be wrong? Name strongest counterargument and acceptance checks. Under400words Russian. No private data or files needed.

---

**Claude:**

**Простыми словами:** ваш вывод в целом разумный, но он держится на двух непроверенных допущениях: затенении и режиме работы дома. Я ничего не запускал и не искал, это разбор только по вашим цифрам.

**Что сходится.** 4643 кВт·ч за 30 дней даёт 6,45 кВт в среднем, как у вас. DC/AC считается верно: 29,7/24 = 1,24 и 29,7/36 = 0,825. Батарея на 20,7 кВт·ч при 6,45 кВт хватает примерно на 3,2 часа, то есть не на всю ночь.

**Где вы можете ошибаться**
1. **Одно месяце мало.** 30 дней могут быть зимой или летом. Без годового профиля потребления нельзя оценить долю самопотребления, а от неё зависят все деньги.
2. **47,8 МВт·ч в год это идеал.** Если половина массива затенена, реальная выработка может быть заметно ниже. Тогда пик мощности тоже ниже, и аргумент про третий инвертор слабеет.
3. **Лимит сети 20,7 кВА.** Три инвертора по 12 кВт дают 36 кВт, а в сеть всё равно не выйдет больше 20,7 кВА. Третий инвертор помогает только собственному потреблению и резерву.
4. **Экономия.** Считайте только самопотреблённые кВт·ч по 0,2265 €. Вычтите потери батареи (цикл около 90%, проверить по даташиту) и добавьте упущенную цену экспорта. Постоянные платежи за сеть в экономию не входят. Итоговой цены у вас нет, поэтому окупаемость пока гипотеза.

**Сильнейший довод против вас.** Вы хотите оценить вариант 2×12K, потому что у него DC/AC выше (1,24). Но для Синтры с юго-югозападной ориентацией клиппинг при 1,24 обычно мал. Он составляет доли процента годовой энергии, и затенение его ещё уменьшит. Дом в среднем потребляет 6,45 кВт, а пики ограничены 20,7 кВА. Поэтому вариант 2×12K, скорее всего, терять почти ничего не будет, а стоить будет дешевле. Довод за третий инвертор остаётся один: резерв по фазам и MPPT. Он зависит от напряжений и токов строк, и это нужно проверять отдельно. Ваша осторожность («не заключать про лишний третий») верна, но обратное тоже недоказано.

**Что проверить до покупки**
- Годовые данные счётчика (15 минут) и пиковую мощность.
- Расчёт затенения по часам (PVGIS с горизонтом или установщик). Это замена словам «половина массива».
- Напряжения и токи строк: Voc при −10 °C, Isc, число входов MPPT на каждом инверторе.
- Какие потребители нужны при отключении сети и их фазы. Проверьте, что SmartGuard 63A держит этот бэкап.
- Цену двух вариантов (2×12K и 3×12K) с монтажом. Считайте окупаемость на одинаковых допущениях.
- Максимальную мощность заряда и разряда батареи и условия гарантии.
- Условия экспорта и тариф на излишки.

**Вердикт:** ⚠️ рекомендация пока предварительная. Для архитектуры Huawei доказательств достаточно. Для третьего инвертора их нет ни в ту, ни в другую сторону.

🏛H · Sonnet 5.5 · 18695
