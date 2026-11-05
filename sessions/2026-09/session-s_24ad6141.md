---
session: s_24ad6141
date: 2026-09-25
words: 1947
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-25 · You are a strict SIGNAL filter for a senior AI engineer building real

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_24ad6141` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

You are a strict SIGNAL filter for a senior AI engineer building real
systems (Claude Code, agents, RAG, LLM apps). You are given the TITLE, CHANNEL and
a SAMPLE of a video transcript. Decide if it carries PRACTICALLY-USEFUL, durable
knowledge a practitioner could ACT on — as opposed to an advertisement, a hype/news
rehash, or content-free chatter.

Return ONE JSON object, NOTHING else. Schema (all scores 0.0-1.0).
IMPORTANT: write "why", and every "claim" and "actionable", in RUSSIAN (the reader
is a Russian-speaking engineer). Keep "topic" as a short english slug. Keep the
"type" values as the english enum below.
{
  "is_ad": bool,                // the item is primarily promotional/sponsored
  "is_news_rehash": bool,       // just "X released Y" hype with no transferable how-to
  "topic": "short-slug",        // e.g. agentic-coding, rag, evals, prompting, infra
  "signal": float,              // density of useful practitioner knowledge
  "novelty": float,             // non-obvious to a senior AI eng in 2026 (self-assessed)
  "actionability": float,       // can the engineer DO something concrete with it
  "evidence": float,            // grounded in demo/benchmark/real experience vs hot takes
  "durability": float,          // how long it stays true
  "volatility": "volatile|medium|stable",
  "half_life_days": int,        // ~60 volatile, ~365 medium, ~1825 stable
  "why": "одно предложение ПО-РУССКИ",
  "knowledge_units": [          // 0-5 atomic, transferable claims; [] if none
    {"claim": "ПО-РУССКИ", "type": "workflow|tactic|tool-caveat|principle|benchmark", "actionable": "ПО-РУССКИ"}
  ]
}

TITLE: GPT 6 + Hyperframe = Crazy combo for expert-level videos
CHANNEL: AI Jason (lang=en)
TRANSCRIPT SAMPLE:
Thanks HubSpot for sponsoring this video. So when we talk about hyperframe or remote type of AI generated per launch video, many people's impression are still those type of PowerPoint slides type of video that looks really boring and not interesting. But things actually changed dramatically for the past few months ever since model like fable was introduced and it went even further with the recent launch of GPD6 Astra. Video editing capability just went out of roof. For example, I just feed this video I download from YouTube to Astra with hyperframe and with just one shot after 32 minutes and basically replicate this video pixel perfectly, which is absolutely insane because there's so many visual details to get it right. And I personally has been using Fable and Astra with Hyperframe to generate all those super high quality launch videos for my own product and it has reached over 1 million views with those AI generated product content. And the most crazy example I personally experienced is this Fable 5.1 launch video for my product track. So my team literally just saw the Fable 5.1 release announcement during the morning and we decided to do a launch with this and we have around 4 hours to prepare the whole launch campaign including this high fidelity video that looks definitely not like a powerpoints plus a landing page like this that looks also again not vibe coded and everything prepared within 4 hours and we got more than 100k views on Twitter. And this is a wake when my team start doing those type of video based launch and it really drives the growth of a product out the roof. So if you're building and distributing products, mastering your skills of making those launch videos with hyperframe or reotion is a must have skill that will give you huge amount of advantage. And this is what I want to talk about today. I'll talk you through how does those frameworks works and also make a video from scratch like this together so you can understand how I make it and what's my preferred workflow. But before we dive into this, part of the reason we can generate amazing videos with frameworks like hyperframe is because modern harness like codeex or cloud code wrap the model with contest use and many other features to unleash mod's power. And there's probably a 10x difference between someone who just simply prompts the agent and hope for the best versus someone who fully utilize every single tip and tricks. And that's why I want to introduce you this free cloud code playbook I put together with HubSpot. It covers core principles I use for prompting those agents as well as how I structure my agent.mmd and cloud.md and project contacts to make the most out of it as well as different hooks and guarios that put together to making sure my agent actually follow SOPs and how do I keep long running work on track with task state as well as different layers of setup for each project when I have so many parallel sessions running at the same time even including some of tips and learnings I got that allow me to cut the API bills by 70% % but still have the same quality output. This is something I wish I had when I getting started. It's completely free. Now let's get back to how to make those awesome hyperframe videos. So cool idea here is that we're going to make videos using HTML which is the thing that large model is really good at and this is possible because now we have new frameworks like hyperframe or remotion. before those frameworks show up. The way human make video is in software like after effect and typically in those software the video is composite of layers effects key frames and automation is only possible by those editor's own API which model is not trained on top of it and more importantly there's no easy way for model to understand what our screen look like at at 1 minute 3 seconds and hyperframe team initially actually experimented using JSON or XML to introduce a data structure that model can output to describe a video but just the help model visualize and understand what does each frame look like and that makes model ineffective in terms of editing and modifying the video but things really change when they go down this HTML CSS and JavaScript route because model is really good at writing HTML. So the way hyperframe works is that it allow you or model to express video timeline in HTML. So you can add those data composition ID and when does this part of video start how long the duration will be and wrap the actual visual under those diff so that model can still output the design in normal HTML and CSS and control the animation using JavaScript which means it can reuse animation library like gap to write animations but just bind the DOM elements to the video timelines. So it became very easy for the model to be able to capture any frame at any given time and this at crux is what hyperframe or remote does and the only difference is that hyperframe is optimized for HTML, CSS and JavaScript versus remotion is designed for react and CSS. So both works but I personally found model is actually more creative or more free to design things in HTML. Also hyperframe comes with a whole bunch of different skills. When you try to install the hyperframe skills, it probably feels pretty overwhelming because there are so many different skills. You might not know which one to use. But in short, there are two sets of skills that introduce. And one must install skill is just this hyperframes core. It talk about the core space of hyperframe and there's some related skills around it like hyperframe CRI, animations and key frames. And they also have this hyperframes registry which allow agent to search in a big library. They provide for different view and animation components. And meanwhile they also provide a set of use case based skills that can be loaded on demand like product launch videos, faceless explainer, music to video, PR to video. For example, I just pointed to this website to video skills and ask it to 
...[middle elided]...
he quality for one two three really well the scene number four almost just one shot get a really good result. It follow all the patterns that we defined earlier. Uh then it is moving the camera to the right and the whole thing is really high quality. Um then I'm going to do next which is this uh prove screen. Um and again I just have like lots of detailed feedback and guidance about the visual. So firstly the visual looks bad just align quality we have on the one to four composition and also start frame with big header text in the middle with Apple Nike ad type motion and camera movement. uh first they focusing on most accurate weight people finder weight new line for agents then show codeex cloud code open claw her logo and uh um I point to loop hub so loop hub is just a open source package that has uh almost all the logo of major AI provider and harness and then translate to this people search bench of B2B perspecting where cloud initially show 43% with a bar chart then cloud plus track reaching 78% almost double the amount and again using the bar chart to contrast then show the four charts with nice translation. Okay, so after a few rounds of uh iteration back and forth u probably for uh like one and a half hours I got a version that I'm like pretty happy with. It has all the animation the story line is correct. Um it showcase the core features that um our product actually offer which is you know connect to also different um systems and uh you can do waterfall uh to routing through different providers so that you can get the data or information you need with the cheapest pos possible price. Um and uh you can see all the animation like feels actually pretty smooth um and tells the story right. Um the coursing here is really you just need to spend time um to update the details u frame by frame. So I'm pretty happy with this one. Uh and lastly let's just add some music. So I prompt it next I want to choose some music. H actually comes with a quite big music library.

---

**Claude:**

```json
{
  "is_ad": true,
  "is_news_rehash": true,
  "topic": "ai-video-generation",
  "signal": 0.35,
  "novelty": 0.35,
  "actionability": 0.4,
  "evidence": 0.35,
  "durability": 0.25,
  "volatility": "volatile",
  "half_life_days": 75,
  "why": "Видео наполовину реклама (спонсор HubSpot + промо собственного продукта автора) и хайп вокруг GPT-6/Fable, но внутри есть конкретное техническое объяснение архитектуры Hyperframe/Remotion и рабочего процесса генерации видео.",
  "knowledge_units": [
    {
      "claim": "Hyperframe и Remotion описывают таймлайн видео через HTML/CSS/JS (атрибуты вроде data-composition-id, старт/длительность на div), а не через JSON/XML — потому что модели гораздо лучше пишут и понимают HTML, чем абстрактные схемы данных, и это позволяет модели точно понять, как выглядит любой конкретный кадр.",
      "type": "principle",
      "actionable": "При выборе инструмента для AI-генерации видео/анимации предпочитать фреймворки, представляющие сцену в виде HTML/DOM с временными метками, а не в виде кастомного JSON-формата — это снижает ошибки модели при редактировании конкретных кадров."
    },
    {
      "claim": "Hyperframe заточен под чистые HTML/CSS/JS (с возможностью подключать библиотеки анимации типа GSAP), тогда как Remotion заточен под React+CSS; по опыту автора модель более креативна и свободна именно в чистом HTML-варианте.",
      "type": "tool-caveat",
      "actionable": "Если нужен максимальный контроль и React-совместимость — брать Remotion; если важна скорость и креативность генерации моделью с нуля — пробовать Hyperframe."
    },
    {
      "claim": "Качественное AI-сгенерированное launch-видео получается не с одного прохода, а через ~1.5 часа итеративной правки: детальный текстовый фидбек по каждой сцене (композиция, движение камеры, текст, переходы) подаётся агенту заново, пока результат не устроит.",
      "type": "workflow",
      "actionable": "Закладывать в план не 'один промпт = готовое видео', а цикл из многих раундов конкретной покадровой критики агенту (что не так в композиции/анимации/тексте), это и есть основной путь к качеству."
    }
  ]
}
```
