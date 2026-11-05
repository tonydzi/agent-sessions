---
session: s_0027b714
date: 2026-10-11
words: 1311
turns: 2
tools: "ToolSearch, WebFetch, WebSearch"
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-10-11 · Research task (use live web search, cite URLs, retrieval date October 2026). Audience: a p…

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_0027b714` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

Research task (use live web search, cite URLs, retrieval date October 2026). Audience: a power user with several Macs (Apple Silicon + Intel Mac Pro 2019), Windows PCs, an iPhone, and Tailscale already installed on every machine.

Questions:
1. Jump Desktop (jumpdesktop.com): current prices on iOS, macOS, Windows clients; is "Jump Desktop Connect" host still free; which protocol (Fluid) and does it support direct peer-to-peer connection or always relay; macOS permissions required for the host (Screen Recording, Accessibility, Login Items); does it work headless / after reboot / with FileVault; can Mac-to-Mac and iPhone-to-Mac both be driven from one Jump account.
2. Screens 5 (edovia.com): current pricing model (subscription vs one-time), "Screens Connect" host, protocols (VNC/RDP), quality vs Jump Desktop Fluid for remote control of a Mac from an iPhone/iPad and from another Mac, direct connection via Tailscale IP without Screens Connect.
3. For controlling a Mac from an iPhone over the internet with the best image quality and lowest latency when both ends are on the same Tailscale tailnet: ranked recommendation among Jump Desktop, Screens 5, RustDesk, Apple's built-in Screen Sharing (High Performance mode, macOS Sonoma+, requires Apple Silicon), Windows App (Microsoft) for RDP to Windows PCs. State any caveats about Apple's High Performance Screen Sharing from iPhone (is there an iOS client at all).
4. Is there any remote-control product actually named "Jem", "Gem" or "Jam" for iPhone/Mac? (a voice transcription said "джем"; the likely intended word is "Jump"). Answer briefly.
Return a compact table and a one-paragraph verdict.

---

> `ToolSearch` -- {"query": "select:WebSearch,WebFetch", "max_results": 2}

---

> `WebSearch` -- {"query": "Jump Desktop pricing iOS macOS Windows Jump Desktop Connect free Fluid peer-to-peer", "mode": "standard"}

---

> `WebSearch` -- {"query": "Screens 5 Edovia pricing subscription one-time Screens Connect VNC", "mode": "standard"}

---

> `WebSearch` -- {"query": "macOS Sonoma High Performance Screen Sharing Apple Silicon iPhone iOS client", "mode": "standard"}

---

> `WebFetch` -- {"url": "https://jumpdesktop.com/faq/", "prompt": "Extract: pricing for iOS, macOS, Windows clients; Jump Desktop Connect free?; Fluid protocol; peer-to-peer vs relay; macOS permissions for host; headless/FileVault/reboot behavior; Mac-to-Mac and iPhone-to-Mac with one account."}

---

> `WebFetch` -- {"url": "https://jumpdesktop.com/pricing-plans.html", "prompt": "Extract all pricing: free tier, team plans, iOS/Mac/Windows app prices, Jump Desktop Connect, Fluid, cloudless/peer-to-peer vs relayed features per tier."}

---

> `WebFetch` -- {"url": "https://help.edovia.com/en/screens-5/faq/s5-pricing", "prompt": "Extract exact prices (monthly, annual, lifetime), what's included, Screens Connect pricing, platforms."}

---

> `WebSearch` -- {"query": "Jump Desktop Connect macOS permissions Screen Recording Accessibility FileVault headless login window reboot", "mode": "standard"}

---

> `WebSearch` -- {"query": "Screens 5 connect directly Tailscale IP VNC without Screens Connect Mac iPhone quality vs Jump Desktop Fluid", "mode": "standard"}

---

> `WebFetch` -- {"url": "https://apps.apple.com/app/id364876095", "prompt": "Price of the app, in-app purchases, description of Fluid, direct connection, Tailscale, requirements."}

---

> `WebSearch` -- {"query": "Jump Desktop Fluid direct connection peer-to-peer relay fallback Tailscale IP address", "mode": "standard", "allowed_domains": ["jumpdesktop.com", "support.jumpdesktop.com"]}

---

> `WebSearch` -- {"query": "RustDesk iOS client Mac host screen recording permission latency 2026 relay direct", "mode": "standard"}

---

> `WebSearch` -- {"query": "Jump Desktop Connect not starting up after reboot FileVault login window unattended", "mode": "standard", "allowed_domains": ["support.jumpdesktop.com", "jumpdesktop.com"]}

---

**Claude:**

Я просмотрел официальные страницы Jump Desktop, Screens (Edovia), RustDesk и Apple. Прямого сравнения качества картинки Screens 5 и Jump Fluid не нашёл, поэтому рейтинг ниже построен на архитектуре протоколов, а не на замерах. Дата поиска: 11.10.2026.

| Вопрос | Jump Desktop | Screens 5 |
|---|---|---|
| **Цена** | iOS: $14.99 разово ([App Store](https://apps.apple.com/app/id364876095)). Windows-клиент бесплатный. Mac-клиент это разовая покупка, цену страница не показывает. Старая сторонняя цифра $34.99 не проверена ([AnyViewer](https://www.anyviewer.com/how-to/jump-desktop-vs-teamviewer-2578.html)). Покупки iOS и Mac раздельные. | Подписка $3.99 в месяц или $29.99 в год, пожизненная $199.99 ([Edovia](https://help.edovia.com/en/screens-5/faq/s5-pricing)). Цены на разных страницах Edovia расходятся ($24.99 в год, $119 и $139.99 за пожизненную), поэтому сверьте в App Store. Платформы: iPhone, iPad, Mac, Vision Pro. |
| **Хост** | Jump Desktop Connect для Mac и Windows, отдельной цены нет ([pricing](https://jumpdesktop.com/pricing-plans.html)). Бесплатный тариф: 1 виртуальный дисплей, до 20 Мбит/с. | Screens Connect для Mac и Windows. Цену я не нашёл, поэтому «бесплатен ли он» осталось непроверенным. |
| **Протокол** | Свой Fluid, шифрование DTLS. Mac, iPhone, Windows и Android работают с одним аккаунтом. | VNC, по заявлению Edovia также RDP (не проверял). |
| **Прямое соединение** | Сначала пробует прямое, потом падает на релей. Если видит интерфейс Tailscale, идёт по нему. Нужны UDP-порты 35384-35484. Принудительно прямое: «Direct Connections Only». Режим Cloudless Fluid (подключение по IP без облака Jump) только в Enterprise, $14.99 за пользователя в месяц ([docs](https://docs.jumpdesktop.com/deployment/connectivity-options/), [форум](https://support.jumpdesktop.com/hc/en-us/community/posts/43160868665741-Tailscale)). | Подключение по Tailscale IP без Screens Connect документировано: `tailscale ip -4`, затем custom connection ([Edovia](https://help.edovia.com/en/screens-5/how-to/connect-via-tailscale)). Начиная с 5.3 есть встроенная интеграция с аккаунтом Tailscale. |
| **Права на Mac-хосте** | Screen Recording, Accessibility, а с macOS 14 ещё Remote Desktop для unattended-доступа. Для macOS Ventura и новее нужно разрешить фон в Login Items, иначе «Initializing» после перезагрузки ([статья](https://support.jumpdesktop.com/hc/en-us/articles/14343257696269-Mac-Jump-Desktop-Connect-does-not-run-after-reboot-stuck-on-Initializing)). | Встроенный Screen Sharing/VNC включается в настройках Mac. Для Screens Connect права я не проверял. |
| **Без монитора и после перезагрузки** | Работает без экрана и после перезагрузки, но при включённом FileVault Mac после обычной перезагрузки остаётся офлайн, пока кто-то не введёт пароль. Лечится командой `sudo fdesetup authrestart` перед каждой плановой перезагрузкой. После отключения питания или сбоя без человека не обойтись ([статья](https://support.jumpdesktop.com/hc/en-us/articles/id_e41944f5-Mac-Computer-shown-as-offline-after-restarting-the-Mac-Filevault)). | Те же ограничения FileVault, так как это свойство macOS, а не приложения. |

**Остальные кандидаты:**
- **Встроенный Screen Sharing (High Performance).** Нужны Apple Silicon на обоих концах и macOS 14 или новее. Это только Mac-к-Mac, iOS-клиента для этого режима нет (ни один источник его не упоминает). Intel Mac Pro 2019 не подходит ни как хост, ни как клиент ([Apple](https://support.apple.com/guide/remote-desktop/apdf8e09f5a9/mac)). Рекомендуемая полоса: 75 Мбит/с на один 4K-дисплей, UDP-порты 5900-5902.
- **RustDesk.** iOS-клиент управляет Mac, на хосте нужны Accessibility и Screen Recording, иногда ещё Input Monitoring. Предпочитает прямое соединение, релей запасной ([RustDesk](https://rustdesk.com/blog/rustdesk-remote-control-android-ios)). Замеров задержки и качества нет.
- **Windows App (RDP).** Я его не искал. Это стандартный путь к Windows-машинам, и по Tailscale-адресу он работает так же, как в локальной сети.

**«Джем».** Продукта для удалённого управления с названием Jem, Gem или Jam для iPhone или Mac я не знаю, но отдельным поиском это не проверял. Скорее всего речь о Jump Desktop.

**Вердикт.** Для iPhone→Mac по Tailscale с лучшей картинкой и минимальной задержкой я бы расставил так:
1. **Jump Desktop.** Fluid идёт по интерфейсу Tailscale напрямую, один аккаунт покрывает Mac и iPhone, 4:4:4 цвет и до 480 fps есть уже в бесплатном тарифе хоста. Платите $14.99 за iOS плюс цену Mac-клиента.
2. **Screens 5.** Надёжный VNC по Tailscale IP, но стоит дороже и по протоколу ему сложно тягаться с Fluid.
3. **RustDesk.** Бесплатный запасной вариант.
4. **Apple High Performance.** Лучший вариант только для Mac-к-Mac на Apple Silicon, с iPhone он недоступен, а ваш Intel Mac Pro 2019 его не поддерживает.
5. **Windows App/RDP.** Для Windows-машин он первый выбор, но для управления Mac не подходит.

Главное предупреждение: если на хосте включён FileVault, перед каждой плановой перезагрузкой делайте authrestart, иначе Mac не вернётся в сеть. Самые достоверные факты выше про Jump Desktop (цены, порядок «прямое, потом релей», FileVault). Про Screens 5 надёжны режим подключения по Tailscale и цены с учётом расхождения между страницами.

🧒 Простыми словами: Jump Desktop похож на хорошую рацию, которая сама находит прямую дорогу между телефоном и компьютером по Tailscale. Screens 5 тоже умеет так ходить, но он дороже и устроен проще. Встроенное в Apple «быстрое» управление работает только с одного Mac на другой, с iPhone и с вашего старого Mac Pro оно не заработает. Если на Mac включено шифрование диска, перед перезагрузкой надо ввести специальную команду, иначе он «уснёт» и не проснётся без вас рядом.

Sources:
- [Jump Desktop pricing](https://jumpdesktop.com/pricing-plans.html)
- [Jump Desktop on the App Store](https://apps.apple.com/app/id364876095)
- [Jump Desktop connectivity options](https://docs.jumpdesktop.com/deployment/connectivity-options/)
- [Jump Desktop forum: Tailscale](https://support.jumpdesktop.com/hc/en-us/community/posts/43160868665741-Tailscale)
- [Jump Desktop: FileVault article](https://support.jumpdesktop.com/hc/en-us/articles/id_e41944f5-Mac-Computer-shown-as-offline-after-restarting-the-Mac-Filevault)
- [Jump Desktop: Initializing after reboot](https://support.jumpdesktop.com/hc/en-us/articles/14343257696269-Mac-Jump-Desktop-Connect-does-not-run-after-reboot-stuck-on-Initializing)
- [Screens 5 pricing](https://help.edovia.com/en/screens-5/faq/s5-pricing)
- [Screens 5 over Tailscale](https://help.edovia.com/en/screens-5/how-to/connect-via-tailscale)
- [Apple High Performance Screen Sharing](https://support.apple.com/guide/remote-desktop/apdf8e09f5a9/mac)
- [RustDesk iOS/Android guide](https://rustdesk.com/blog/rustdesk-remote-control-android-ios)
- [AnyViewer: Jump Desktop comparison](https://www.anyviewer.com/how-to/jump-desktop-vs-teamviewer-2578.html)
