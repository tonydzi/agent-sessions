---
session: s_40984be0
date: 2026-10-25
words: 2317
turns: 6
tools: "Bash, ToolSearch, mcp__ccd_session_mgmt__set_session_title"
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-10-25 · Scheduled run: auto-hub-261006-silent-green-family-148

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_40984be0` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

<scheduled-task name="auto-hub-261006-silent-green-family-148" file="C:\Users\dev\.claude\scheduled-tasks\auto-hub-261006-silent-green-family-148\SKILL.md">
This is an automated run of a scheduled task. The user is not present to answer questions. For implementation details, execute autonomously without asking clarifying questions — make reasonable choices and note them in your output. "write" actions (e.g. MCP tools that send, post, create, update, or delete), only take them if the task file asks for that specific action. When in doubt, producing a report of what you found is the correct output.

Первым действием переименуй эту сессию: mcp__ccd_session_mgmt__set_session_title(session_id="self", title="🧪 · 🐹🕸 Пилот роя Coddy"), номер сессии добавь в конце по session_code.py.

ТЫ КОФАУНДЕР, а не исполнитель: дожимаешь свою часть до проверенного результата сам, вопросы оператору только из закрытого списка Tier-2 (CLAUDE.md §0.1).

ЗАКАЗ (оператор, 25.10.2026, голосом в сессии H28033): «пилот роя, да, окей». Это его согласие на смену топологии флота (§2.3) для ТЕНИ на трёх узлах, не на раскатку.

ЦЕЛЬ: живой рой Coddy на трёх узлах, тень 14 дней по §5.7, с замером. Coddy = Go-бинарь coddy-project/coddy-agent (MIT), на хабе уже 1.3.49 в C:\Users\dev\AppData\Local\Programs\coddy\coddy.exe, конфиг C:\Users\dev\.coddy\config.yaml, провайдер type: codex (подписка ChatGPT).

ПРОЧТИ ДО ДЕЙСТВИЙ:
- D:\Vault\Vault-Knowledge\03-Insights\insight-coddy-1-3-swarm-fleet-verdict-2026-10-11.md (раздел «До → после», токены, риски, второе мнение Codex);
- D:\Vault\Vault-Knowledge\03-Insights\insight-IDR-DR26-10-25-HUB-01-0946-coddy-adoption-and-contribution.md (свежий ИДР, таблица болей и метрик);
- docs/operate/swarm.md, docs/operate/serve.md, docs/operate/security.md в клоне E:\!CLAUDE-HUBPC-June26\_oss\coddy-agent (версия main da8fdeb, сверь с 1.3.49 по release notes).

ПЛАН (по шагам, каждый с уликой: команда + вывод + exit-код):
1. Маяк (ssh mayak, Linux VPS): поставить coddy 1.3.49 linux_amd64 со сверкой SHA256SUMS; `coddy serve install` (systemd user service); конфиг relay: swarm.enable: true, httpserver.enable: false, bind на Tailscale-IP Маяка (НЕ 10.0.0.0; проверь IP `tailscale ip -4`), порт 12346; три токена `openssl rand -hex 24` в ~/.coddy/.env, chmod 600; уникальный node-токен на каждый узел. Провайдера LLM на Маяке не нужно.
2. Хаб (эта машина): в config.yaml добавить swarm.join в tunnel-режиме (без advertise_url) на relay Маяка; `coddy -t` и `--dry-run` чистые; запустить `coddy serve --daemon` на loopback. permission_mode сессий = ask, `decisions` ВЫКЛЮЧЕН.
3. NODE-0X (ssh ZB): то же, что хаб. Если на NODE-0X нет Coddy — поставить 1.3.49 со сверкой SHA256SUMS.
4. Проверка: `GET /swarm/sessions` через relay показывает сессии обоих узлов; одна тестовая сессия на каждом узле в режиме ask видна в карте роя.
5. Негативные проверки (из второго мнения Codex 11.10): отозванный client-токен отбивается; повтор pairing; попытка узла читать соседа; рестарт relay (issue #639 про захват имени узла).
6. Строка в D:\Vault\Vault-Knowledge\00-System\Shadow-First-Queue.md: старт 2026-10-25, урожай 🌾 2026-11-08, метрики: доля видимых сессий от истины на узел; переподключения туннеля в сутки; число промптов разрешений и медиана ответа; 429 на 100 вызовов при Codex CLI + Coddy на одной подписке.
7. Откат назван заранее: на Маяке `coddy serve uninstall`, на хабе и NODE-0X убрать блок swarm: из config.yaml и `coddy serve stop`. 5 минут.

ГРАНИЦЫ:
- Машины коллег (Нора, Рита, Эдита) и маки в рой НЕ подключать.
- Токены и пароли только в ~/.coddy/.env и secrets\, никогда в волт, логи, шину или отчёт.
- Хаб на Windows: `coddy serve install` там нет, после перезагрузки сервер сам не встанет. Это известный пробел пилота: запиши его в метрики, обходной автозапуск только с бэкапом и откатом.
- Перед правкой общего: `python ~/.claude/scripts/onair.py declare --zone fleet/coddy-swarm --mode exclusive --task "пилот роя Coddy"`, в конце `onair close`.
- ДР-ноги через браузер в этой сессии НЕ запускать.

ДОКЛАД: в чат 03 одной строкой (`bus_send.py`) и итог в конце сессии: что поднято, улики, что не вышло и почему, ссылка на строку Shadow-First-Queue. Ретро по /retro.
</scheduled-task>

---

> `ToolSearch` -- {"query": "select:mcp__ccd_session_mgmt__set_session_title", "max_results": 1}

---

> `Bash` -- {"command": "cd ~ && python ~/.claude/scripts/session_code.py 2>&1 | head -3; cat \"C:/Users/dev/.claude/projects/P---WORKDIR-HUB/memory/coddy-harness-installed.md\" | head -40", "description": "Read session code and prior coddy memory"}

---

> `Bash` -- {"command": "python ~/.claude/scripts/session_code.py whoami 2>&1 | head -5", "description": "Get session code"}

---

**Claude:**

Номер уже выдан хуком: H29354.

---

> `mcp__ccd_session_mgmt__set_session_title` -- {"session_id": "self", "title": "🧪 · 🐹🕸 Пилот роя Coddy · H29354"}

---

> `Bash` -- {"command": "python ~/.claude/scripts/onair.py declare --zone fleet/coddy-swarm --mode exclusive --task \"пилот роя Coddy\" 2>&1 | tail -3; \"C:/Users/dev/AppData/Local/Programs/coddy/coddy.exe\" --version 2>&1 | head -3; ssh -o ConnectTimeout=10 -o BatchMode=yes mayak 'uname -a; tailscale ip -4; 

---

> `Bash` -- {"command": "python ~/.claude/scripts/onair.py declare --zone fleet/coddy-swarm --mode exclusive --title \"пилот роя Coddy\" --task \"пилот роя Coddy\" 2>&1 | tail -3\nssh mayak 'id -un; ls ~/.coddy 2>&1; systemctl --user status 2>&1 | head -2; ss -ltn | grep -E \"12346|:80 |:443 \" ; uname -m; whic

---

> `Bash` -- {"command": "python ~/.claude/scripts/onair.py declare --zone fleet-code/coddy-swarm --mode exclusive --title \"пилот роя Coddy\" --task \"пилот роя Coddy\" 2>&1 | tail -2; cd \"E:/!CLAUDE-HUBPC-June26/_oss/coddy-agent/docs/operate\"; wc -l swarm.md serve.md security.md; cat swarm.md", "descrip

---

> `Bash` -- {"command": "cd \"E:/!CLAUDE-HUBPC-June26/_oss/coddy-agent/docs/operate\"; cat serve.md | sed -n 1,200p; grep -n -i -E \"install|systemd|windows\" serve.md | sed -n 1,40p", "description": "Read serve docs"}

---

> `Bash` -- {"command": "cd /tmp 2>/dev/null; gh release view v1.3.49 --repo coddy-project/coddy-agent --json tagName,assets -q '.tagName, (.assets[]|.name)' 2>&1 | head -30", "description": "List 1.3.49 release assets"}

---

> `Bash` -- {"command": "gh release list --repo coddy-project/coddy-agent --limit 5 2>&1 | head; gh release list --repo EvilFreelancer/coddy-agent --limit 5 2>&1 | head -5; cd \"E:/!CLAUDE-HUBPC-June26/_oss/coddy-agent\" && git remote -v | head -2", "description": "Find the correct release repo"}

---

> `Bash` -- {"command": "S=\"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_40984be0/scratchpad\"; mkdir -p \"$S/dl\"; cd \"$S/dl\"; gh release view 1.3.49 --repo coddy-project/coddy-agent --json assets -q '.assets[]|.name+\" \"+(.size|tostring)' | grep -i -E \

---

**Claude:**

Скачал релиз 1.3.49 (linux и windows) и сверяю SHA256, потом ставлю на Маяк.

---

> `Bash` -- {"command": "S=\"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_40984be0/scratchpad/dl\"; cd \"$S\"; sha256sum -c SHA256SUMS --ignore-missing 2>&1; echo rc=$?\nscp -q coddy_1.3.49_linux_amd64.tar.gz mayak:/tmp/ 2>&1 | grep -v -E \"WARNING|vulnerable

---

> `Bash` -- {"command": "cd \"E:/!CLAUDE-HUBPC-June26/_oss/coddy-agent\"; grep -n -i -A60 \"^## .*swarm\" docs/reference/config.md | head -120; cat ~/.coddy/config.yaml | sed -e 's/\\(key\\|token\\)\\(.*\\):.*/\\1\\2: <redacted>/I' | head -60", "description": "Read swarm config reference and current hub co

---

> `Bash` -- {"command": "cd \"E:/!CLAUDE-HUBPC-June26/_oss/coddy-agent\"; grep -rn -l \"swarm\" docs/reference/ | head; grep -n -i \"swarm\" docs/reference/config.md | head -50", "description": "Find swarm config keys"}

---

> `Bash` -- {"command": "S=\"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_40984be0/scratchpad\"; cd \"$S\"\npython - <<'EOF'\nimport secrets\nt=lambda: secrets.token_hex(24)\nclient,pair,hub,zb=t(),t(),t(),t()\nopen(\"env.mayak\",\"w\",newline=\"\\n\").write(

---

> `Bash` -- {"command": "ssh mayak 'export PATH=$HOME/.local/bin:$PATH; coddy -t 2>&1 | tail -5; echo rc=$?; coddy serve install 2>&1 | tail -12; sleep 3; systemctl --user is-active coddy.service; ss -ltn | grep 12346; journalctl --user -u coddy.service -n 15 --no-pager 2>&1 | tail -15' 2>&1 | grep -v -E \"WARN

---

> `Bash` -- {"command": "cd \"E:/!CLAUDE-HUBPC-June26/_oss/coddy-agent\"; ls ~/.coddy/scheduler | head; sed -n 295,318p docs/reference/config.md | cut -c1-230; grep -n -E \"permission_mode|decisions\\.enable\" docs/reference/config.md | cut -c1-220 | head", "description": "Check scheduler tasks and httpser

---

> `Bash` -- {"command": "cd \"E:/!CLAUDE-HUBPC-June26/_oss/coddy-agent\"; grep -n -i \"permission\" docs/reference/config.md | cut -c1-200 | head -8\nS=\"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_40984be0/scratchpad\"\ncp ~/.coddy/config.yaml ~/.coddy

---

> `Bash` -- {"command": "cd \"E:/!CLAUDE-HUBPC-June26/_oss/coddy-agent\"; grep -n -i \"permission\" docs/reference/config.md | cut -c1-200 | head -8\nS=\"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_40984be0/scratchpad\"\ncp ~/.coddy/config.yaml ~/.coddy

---

> `Bash` -- {"command": "cd \"E:/!CLAUDE-HUBPC-June26/_oss/coddy-agent\"; grep -n -E \"permission_mode|default_mode\" docs/reference/config.md | cut -c1-260 | head -5; cat ~/.coddy/.env | cut -d= -f1", "description": "Find permission mode key"}

---

> `Bash` -- {"command": "S=\"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_40984be0/scratchpad\"; C=\"C:/Users/dev/AppData/Local/Programs/coddy/coddy.exe\"\n\"$C\" serve --daemon > \"$S/s.out\" 2>&1; echo rc=$?; cat \"$S/s.out\" | head -12; sleep 6\nssh maya

---

> `Bash` -- {"command": "tail -15 ~/.coddy/logs/serve.log | cut -c1-300; C=\"C:/Users/dev/AppData/Local/Programs/coddy/coddy.exe\"; \"$C\" serve status 2>&1 | head -6; netstat -ano | grep -E \":12345 \" | head -3", "description": "Inspect hub serve log and status"}

---

> `Bash` -- {"command": "S=\"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_40984be0/scratchpad\"\nssh ZB 'powershell -NoProfile -Command \"whoami; $env:USERPROFILE; Test-Path $env:USERPROFILE\\.codex\\auth.json; (Test-NetConnection 10.0.0.0 -Port 12346 -Wa

---

> `Bash` -- {"command": "S=\"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_40984be0/scratchpad\"; cd \"$S\"\ncat > cfg.zb <<'EOF'\n# yaml-language-server: $schema=https://coddy.dev/config.schema.json\n# Пилот роя Coddy 25.10.2026 (H29354). Откат: удалить блоки

---

> `Bash` -- {"command": "ssh ZB 'powershell -NoProfile -Command \"(Get-FileHash C:\\Users\\dev\\AppData\\Local\\Temp\\coddy.zip -Algorithm SHA256).Hash; & C:\\Users\\dev\\AppData\\Local\\Programs\\coddy\\coddy.exe serve --daemon; \\\"rc=$LASTEXITCODE\\\"\"' 2>&1 | grep -v -E \"WARNING|vulnerable|upgraded|^\\*\\*\";

---

**Claude:**

Кавычки сломались. Делаю через файл.

---

> `Bash` -- {"command": "S=\"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_40984be0/scratchpad\"; cd \"$S\"\ncat > start.ps1 <<'EOF'\n(Get-FileHash \"$env:TEMP\\coddy.zip\" -Algorithm SHA256).Hash\n& \"$env:LOCALAPPDATA\\Programs\\coddy\\coddy.exe\" serve --da

---

> `Bash` -- {"command": "ssh ZB 'powershell -NoProfile -Command \"Get-Content C:\\Users\\dev\\.coddy\\logs\\serve.log -Tail 12\"' 2>&1 | grep -v -E \"WARNING|vulnerable|upgraded|^\\*\\*\" | cut -c1-300", "description": "Read NODE-0X serve log"}

---

> `Bash` -- {"command": "S=\"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_40984be0/scratchpad\"; cd \"$S\"\ncat > start2.ps1 <<'EOF'\n$e=\"$env:LOCALAPPDATA\\Programs\\coddy\\coddy.exe\"\nGet-Process coddy -ErrorAction SilentlyContinue | Select Id,StartTime |

---

> `Bash` -- {"command": "S=\"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_40984be0/scratchpad\"\nCT=$(grep ^CODDY_SWARM_TOKEN= ~/.coddy/.env | cut -d= -f2); R=http://10.0.0.0:12346\ncurl -s -m 10 -H \"Authorization: Bearer $CT\" $R/swarm/info; echo; curl 

---

> `Bash` -- {"command": "cd \"E:/!CLAUDE-HUBPC-June26/_oss/coddy-agent\"; grep -n -i -E \"POST|/v1/chat|session\" docs/reference/http-api.md | cut -c1-210 | head -45; ls ~/.coddy/sessions | wc -l", "description": "Find session creation endpoints"}

---

> `Bash` -- {"command": "CT=$(grep ^CODDY_SWARM_TOKEN= ~/.coddy/.env | cut -d= -f2); R=http://10.0.0.0:12346\nfor n in hub-a2022bayarea NODE-0X-g8; do sid=\"sess_$(python -c 'import secrets;print(secrets.token_hex(12))')\"; echo \"$n $sid\" >> /tmp/pilot_sids.txt\n curl -s -m 120 -w \"\\nhttp=%{http_code} t=%

---

> `Bash` -- {"command": "S=\"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_40984be0/scratchpad\"; cd \"$S\"\nCT=$(grep ^CODDY_SWARM_TOKEN= ~/.coddy/.env | cut -d= -f2); PT=$(grep ^CODDY_SWARM_PAIRING_TOKEN= ~/.coddy/.env | cut -d= -f2); ZT=$(grep ^CODDY_NODE_T

---

> `Bash` -- {"command": "cd \"E:/!CLAUDE-HUBPC-June26/_oss/coddy-agent\"; grep -rn -E \"json:\\\"(advertise_url|lease_secret|instance|generation)\" internal --include=*.go | grep -v _test | head -8", "description": "Find register request schema"}

---

> `Bash` -- {"command": "cd \"E:/!CLAUDE-HUBPC-June26/_oss/coddy-agent\"; sed -n 28,48p internal/swarm/dto.go", "description": "Read register DTO"}

---

> `Bash` -- {"command": "PT=$(grep ^CODDY_SWARM_PAIRING_TOKEN= ~/.coddy/.env | cut -d= -f2); CT=$(grep ^CODDY_SWARM_TOKEN= ~/.coddy/.env | cut -d= -f2); R=http://10.0.0.0:12346\ncurl -s -m 10 -w \" http=%{http_code}\\n\" -X POST -H \"Authorization: Bearer $PT\" -H 'Content-Type: application/json' -d '{\"nam

---

> `Bash` -- {"command": "PT=$(grep ^CODDY_SWARM_PAIRING_TOKEN= ~/.coddy/.env | cut -d= -f2); CT=$(grep ^CODDY_SWARM_TOKEN= ~/.coddy/.env | cut -d= -f2); R=http://10.0.0.0:12346\nssh mayak 'systemctl --user restart coddy.service' 2>&1 | grep -v -E \"WARNING|vulnerable|upgraded|^\\*\\*\"\nfor i in 1 2 3 4 5 6

---

> `Bash` -- {"command": "CT=$(grep ^CODDY_SWARM_TOKEN= ~/.coddy/.env | cut -d= -f2); R=http://10.0.0.0:12346\nfor i in 1 2 3 4 5 6; do sleep 30; curl -s -m 10 -H \"Authorization: Bearer $CT\" $R/swarm/topology | python -c \"import sys,json;d=json.load(sys.stdin);print([(n['name'],n['uuid'][:6],n['online']) 

---

**Claude:**

Пока идёт ожидание, пишу строку в Shadow-First-Queue.

---

> `Bash` -- {"command": "cd \"D:/Vault/Vault-Knowledge/00-System\"; tail -15 Shadow-First-Queue.md | cut -c1-300; wc -l Shadow-First-Queue.md; python ~/.claude/scripts/machine_stamp.py line --agent \"Claude Code\" 2>&1 | tail -1", "description": "Inspect Shadow-First-Queue format"}

---

> `Bash` -- {"command": "cd \"D:/Vault/Vault-Knowledge/00-System\"; cp Shadow-First-Queue.md \"E:/!CLAUDE-HUBPC-June26/_app-backups/Shadow-First-Queue-H29354-20261025.before.md\"\ncat >> Shadow-First-Queue.md <<'EOF'\n\n- 🌑 coddy-swarm-pilot (H29354, старт **2026-10-25**, урожай 🌾 **2026-11-08**): рой C

---

> `Bash` -- {"command": "sleep 60; cat \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_40984be0/tasks/bu9b9sg0r.output\"; tail -5 ~/.coddy/logs/serve.log | cut -c1-250", "description": "Check recovery output"}

---

> `Bash` -- {"command": "cat \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_40984be0/tasks/bu9b9sg0r.output\"; tail -5 ~/.coddy/logs/serve.log | cut -c1-250", "description": "Read recovery output"}

---

> `Bash` -- {"command": "CT=$(grep ^CODDY_SWARM_TOKEN= ~/.coddy/.env | cut -d= -f2); R=http://10.0.0.0:12346\ncurl -s -m 10 -w \"del http=%{http_code}\\n\" -X DELETE -H \"Authorization: Bearer $CT\" $R/swarm/nodes/hub-a2022bayarea\ntimeout 100 bash -c 'until curl -s -H \"Authorization: Bearer '$CT'\" '$R'/s

---

> `Bash` -- {"command": "S=\"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_40984be0/scratchpad\"; rm -f \"$S\"/env.* /tmp/pilot_sids.txt; ls \"$S\"\npython ~/.claude/scripts/onair.py close 2>&1 | tail -2\npython ~/.claude/scripts/bus_send.py --help 2>&1 | head

---

> `Bash` -- {"command": "python ~/.claude/scripts/onair.py close 2026-10-25T153159Z-HUB-01-610ac754-fleet-code-coddy-swarm 2>&1 | tail -1\npython ~/.claude/scripts/bus_send.py --help 2>&1 | grep -E \"usage|--to|--text|--kind\" | head -6", "description": "Close onair declaration, see bus_send flags"}

---

> `Bash` -- {"command": "python ~/.claude/scripts/bus_send.py --help 2>&1 | sed -n 8,40p | cut -c1-200", "description": "Read bus_send usage"}

---

> `Bash` -- {"command": "cd ~; python ~/.claude/scripts/bus_send.py \"Пилот роя Coddy 1.3.49 (H29354): relay на Маяке 10.0.0.0:12346 + ноды хаб и NODE-0X в туннеле, /swarm/sessions видит оба узла, негативные токены 401. Находка: после рестарта relay имя узла захватывается держателем pairing-токена (issue 639 

---

**Claude:**

Пилот роя Coddy 1.3.49 поднят на Маяке, хабе и NODE-0X: `/swarm/sessions` через relay показывает оба узла. Одну проверку роя не прошёл: после рестарта relay имя узла может захватить посторонний. Тень идёт с 25.10 до 08.11. Ретро по `/retro` я не запускал.

**Что поднято**
- **Маяк (relay):** Coddy 1.3.49 (SHA256 сошёлся), служба `coddy.service` под systemd. Слушает только `10.0.0.0:12346` (Tailscale), HTTP-сервер выключен, токены в `~/.coddy/.env` с правами 600.
- **Хаб и NODE-0X (узлы):** оба в tunnel-режиме, API на loopback с bearer-токеном. Хаб запущен через `coddy serve --daemon`; NODE-0X запущен через WMI, потому что при запуске через ssh демон умирал.
- **Проверка связи:** `/swarm/topology` показывает оба узла online. Тестовый промпт «pong» через relay дал 200 на каждом узле: хаб ответил за 5 с, NODE-0X за 10,5 с.
- **Видимость сессий:** на хабе в карте 3 сессии при 4 каталогах на диске (пустые не листятся), на NODE-0X 1 из 1.
- **Режим разрешений:** отдельной настройки для него в конфиге нет, `decisions` выключен. Тестовые сессии шли в режиме `agent` с дефолтным подтверждением. Промпт разрешений я не вызывал.

**Негативные проверки**
- **Токены:** запрос без токена, с неверным токеном и с токеном узла вместо клиентского отбиваются кодом 401. Узел читать соседа через relay не может (401). Регистрация с неверным pairing-токеном отбита (401).
- **Захват имени при живой аренде:** повторная регистрация занятого имени даёт 409.
- **Рестарт relay и issue #639: воспроизведено.** В первые мгновения после рестарта pairing-токен позволил занять имя `hub-a2022bayarea`, и настоящий хаб оказался отрезан. Лечится административным `DELETE /swarm/nodes/hub-a2022bayarea` с клиентским токеном. Я так и сделал: хаб вернулся с прежним UUID.
- **Не проверено:** ротация клиентского токена, то есть «отозванный токен», отдельно не тестировалась, проверены только неверные и чужие токены. Повтор pairing тоже без отдельного теста.

**Что не вышло**
- **Автозапуск на Windows:** `coddy serve install` там нет, поэтому после ребута хаб и NODE-0X сами не поднимутся. Это записано в метрики, обходной автозапуск я не делал.
- **Команда onair:** зона `fleet/coddy-swarm` не прошла по таксономии, использовал `fleet-code/coddy-swarm`. Запись закрыта.

**Откат (5 минут)**
- Маяк: `coddy serve uninstall`.
- Хаб и NODE-0X: убрать блоки `httpserver` и `swarm` из `config.yaml` и выполнить `coddy serve stop`. Бэкап хаба: `config.yaml.bak-pre-swarm-20261025`.

**Учёт**
- **Shadow-First-Queue:** строка добавлена в конец файла, с метриками, пробелом по Windows и находкой по #639. Бэкап файла: `_app-backups/Shadow-First-Queue-H29354-20261025.before.md`.
- **Чат 03:** одна строка ушла через `bus_send.py`, обе рельсы приняли.
- **Секреты:** токены лежат только в `~/.coddy/.env` на каждой из трёх машин, во временных файлах их не осталось.

🧒 Простыми словами: на Маяке поставили «диспетчерскую», хаб и ноутбук к ней подключились и видны на одной карте. Чужие и неверные ключи диспетчерская не пускает. Но если её перезапустить, держатель общего ключа успевает выдать себя за хаб: ошибка в самой программе, мы её повторили и починили вручную. После перезагрузки Windows-машины сами не подключатся, это пока дыра.

🏛H · Sonnet 5.5 · 29354
