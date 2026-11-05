---
session: s_63518c32
date: 2026-10-15
words: 767
turns: 3
tools: "Bash, Grep, PowerShell, Read, Write"
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-10-15 · Этот парень, используя Claude Code + YouTube, создаёт анимационные видео и зарабатывает 90…

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_63518c32` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

**Этот парень, используя Claude Code + YouTube, создаёт анимационные видео и зарабатывает 90 тысяч долларов в месяц 💰**

Видео на 10 минут стоит посмотреть, чтобы представлять, как на таком можно зарабатывать такие деньги. Сам ролик на английском, я перевёл его и вшил русские субтитры.

Он показывает всю цепочку: от сценария до готовых картинок, без аниматора и сценариста. Всё делается через Claude и Higgsfield.

**Что внутри:**
0:00 — Сколько зарабатывают безлицевые каналы
1:01 — Почему работает формат со стик-фигурками
1:56 — Берём сценарий популярного видео конкурента
3:11 — Claude пишет похожий сценарий
3:40 — Озвучка в ElevenLabs
4:51 — Озвучка → текст с таймкодами (TurboScribe)
5:50 — Подключаем Higgsfield к Claude Code
6:58 — Один промпт, и картинки генерируются сами
8:30 — Результат: все сцены в одном стиле
8:59 — Собираем видео в CapCut
9:57 — Финальный ролик

E:\!CLAUDE-HUBPC-June26\downloads\aAy92bVG8C-l1Vky_ru_1045.mp4

---

**Claude:**

Принял: пост плюс файл видео. Прямой задачи в сообщении нет, поэтому беру по канону: проверяю файл, делаю RECALL (не было ли такого у нас уже), затем разбираю содержание и кладу в волт.

---

> `PowerShell` -- {"command": "$f='E:\\!CLAUDE-HUBPC-June26\\downloads\\aAy92bVG8C-l1Vky_ru_1045.mp4'; if(Test-Path -LiteralPath $f){Get-Item -LiteralPath $f | Select Name,Length,LastWriteTime | Format-List; (Get-Command ffprobe -ErrorAction SilentlyContinue).Source; (Get-Command ffmpeg -ErrorAction SilentlyCont

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports && timeout 90 python brain_ask.py \"stick figure animated YouTube faceless Higgsfield Claude Code CapCut TurboScribe\" 2>&1 | head -40", "description": "RECALL in vault for this topic"}

---

> `Grep` -- {"pattern": "Higgsfield|faceless|стик-фигур|stick.?figure", "path": "D:\\Vault\\Vault-Knowledge", "output_mode": "files_with_matches", "head_limit": 15}

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports; ls | grep -i -E \"whisper|transcr|asr|podcast_essence\" | head -20; python - <<'EOF'\nimport shutil,glob,os\nprint('ffmpeg',shutil.which('ffmpeg'))\nfor p in glob.glob(r'C:\\Users\\dev\\**\\ffmpeg.exe',recursive=False)[:3]: print(p)\nfor root in [r'C:\\ffmpeg'

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports; sed -n 1,40p whisper_best.py; python -c \"import imageio_ffmpeg;print(imageio_ffmpeg.get_ffmpeg_exe())\" 2>&1|tail -1; where ffmpeg 2>&1|head -2", "description": "Read whisper_best usage header"}

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports; mkdir -p \"/c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_63518c32/scratchpad\"; cat > /tmp/t.py <<'EOF'\nimport sys,time\nsys.path.insert(0,r\"D:\\Vault\\_imports\")\nimport whisper_best as wb\nwb._patch_av_

---

> `Write` -- {"file_path": "C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_63518c32\\scratchpad\\t.py", "content": "import sys, time\nsys.path.insert(0, r\"D:\\Vault\\_imports\")\nimport whisper_best as wb\nif hasattr(wb, \"_patch_av_open\"):\n    wb.

---

> `Bash` -- {"command": "PYTHONIOENCODING=utf-8 timeout 580 python \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_63518c32/scratchpad/t.py\" 2>&1 | tail -5", "description": "Run local whisper transcription", "timeout": 600000}

---

> `Read` -- {"file_path": "C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_63518c32\\scratchpad\\tr.txt"}

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports; python -c \"\nimport _paths;print(_paths.originals_root())\" 2>&1|tail -2; ls /e/Obsidian/Vault-Knowledge/05-Resources | head -30; python ~/.claude/scripts/machine_stamp.py line --agent \"Claude Code (Sonnet 5.5)\"; python ~/.claude/scripts/machine_stamp.py sig 

---

> `Bash` -- {"command": "mkdir -p /e/Obsidian/_originals/video-transcripts /e/Obsidian/Vault-Knowledge/05-Resources/Video-Notes; cp \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_63518c32/scratchpad/tr.txt\" /e/Obsidian/_originals/video-transcripts/2026-10-15

---

> `Write` -- {"file_path": "D:\\Vault\\Vault-Knowledge\\05-Resources\\Video-Notes\\2026-10-15-faceless-stickfigure-youtube-claude-higgsfield.md", "content": "---\ntitle: Безлицевый YouTube со стик-фигурками на Claude + Higgsfield (разбор ролика Лео)\ndate: 2026-10-15\ntype: video-note\nsource: downloads/aAy92

---

**Claude:**

Я расшифровал ролик, сверил его с твоим постом и сохранил разбор в волт. Пост и ролик расходятся в одном месте: «90 тысяч в месяц» в видео не называют.

**Что в ролике.** Автор (Лео, продаёт курсы) показывает такую цепочку:
1. Берёт транскрипт популярного видео конкурента через youtube-to-transcript.
2. Просит Claude написать похожий сценарий.
3. Озвучивает его в ElevenLabs.
4. Прогоняет озвучку через TurboScribe, чтобы получить текст с таймкодами.
5. Подключает Higgsfield к Claude как коннектор по URL со страницы «MCP and CLI».
6. Одним большим промптом заставляет Claude сделать картинку на каждый таймкод, около 50 штук в одном стиле, и выдать таблицу «какая картинка на какой секунде».
7. Собирает видео в CapCut вручную.

**Цифры против твоего заголовка.**
- Названы 11 тыс. $ за ~90 дней при менее 5 тыс. подписчиков, 16 тыс. $ на 1,5 млн просмотров и 18 тыс. $ с одного видео.
- «90 тысяч в месяц» в видео нет. Похоже, «90» взялось из «90 дней».
- Все цифры автор назвал сам, а он продаёт обучение. Если будешь публиковать, поправь заголовок.

**Что полезно нам.** Приём «транскрипт с таймкодами, потом покадровая генерация через MCP» переносится на любые ролики. Ручной шаг 7 можно убрать: ffmpeg расставит картинки по таблице таймкодов. В ролике этого нет.

**Проверка.** Транскрипт сделан локальным whisper large-v3, язык задан английский, 124 сегмента, 645 секунд. Вшитые русские субтитры я не читал, брал только звук, поэтому твой перевод с оригиналом не сверял. Скачивание файла по ссылке не проверял, файл лежит на диске.

**Сохранено:**
- [Заметка](D:/Vault/Vault-Knowledge/05-Resources/Video-Notes/2026-10-15-faceless-stickfigure-youtube-claude-higgsfield.md)
- Оригинал транскрипта: `D:\Vault\_originals\video-transcripts\2026-10-15-faceless-stickfigure-claude-higgsfield-leo-whisper-en.txt`

Заметку я не привязывал к хабам и MOC (связь только в `related`), а `link_at_birth_lint` не запускал.

Ты не написал, что именно нужно сделать с роликом. Могу собрать наш пайплайн по этой схеме для девлога, если это цель.

🧒 **Простыми словами:** Дядька показал, как сделать мультик без художника. Робот пишет сказку, другой робот её читает вслух, третий рисует картинку на каждую секунду. Деньги, которые он называет, он назвал сам, и «90 тысяч в месяц» он не говорил. Я записал всё в нашу тетрадь, а картинки по секундам можно будет раскладывать автоматически.

🏛H · Sonnet 5.5 · 22039
