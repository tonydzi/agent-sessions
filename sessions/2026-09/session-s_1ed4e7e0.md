---
session: s_1ed4e7e0
date: 2026-09-25
words: 2086
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-25 · You are a strict SIGNAL filter for a senior AI engineer building real

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_1ed4e7e0` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

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

TITLE: Building the Engine While Flying the Plane: Launching the Figma MCP Server — [ИМЯ] [ИМЯ], Figma
CHANNEL: AI Engineer (lang=en)
TRANSCRIPT SAMPLE:
[music] All right, get started. [ИМЯ], I'm [ИМЯ] and [СКРЫТО] and I'm going to talk to you about how we built Figma's first MCP server in about 3 months. Um, and in case you don't know what it is, the Figma MCP server is a way for you to send context between production uh code and design and vice versa. AI tools don't need to build a dedicated integration. They can just use our Figma MCP and they kind of get started. So, taking you back to November 2024, long long time ago, Anthropic released the MCP server spec and uh everyone in the world of AI was sort of starting to use it and experiment with it. Um but outside of anthropic none of the other AI agents or labs were really using it. So OpenAI cursor VS Code they didn't support it yet. Um once we got access to the feature in cursor however uh we were able to kind of ideate and understand what it was capable of and we got something a little bit closer to an actual product and that's where my story begins. Um [СКРЫТО] and I saw our internal demo and I really wanted to use it. I thought it'd be great for non-designers uh to kind of be able to use Figma. Um, [СКРЫТО]. It was kind of my 20% project that we didn't we didn't really have 20% projects, but I really wanted to work on it, so I did. Um, and so I got staffed with some other folks um on the team. [СКРЫТО]. That's a peep. It's a candy if you don't know. Um, they're delicious. And I I just want to be very clear um I'm going to say I a lot and we there was a big team behind this so it's not just me and they're all fantastic. Um a few weeks later after we started getting our initial architecture sorted a new version of the spec dropped uh deprecating the support type that we were going to use which was server events and while the MCP spec was sort of chugging along clients were adding features and support in different paces. Uh cloud had early support cloud desktop but cloud code you was wasn't really supported uh with all the complete set of features. OpenAI and VS Code didn't h have support until that spec update and then it wasn't even then uh VS Code didn't go out of uh didn't get to G until July. It didn't mean that all the features were implemented either. There are lots of different pieces um and in many cases only tools were supported. VS Code was truly like the golden client. Uh they eventually supported kind of all pieces of the spec, but it was it was hard to kind of understand what you were building towards because clients supported so many different things. [snorts] But even though we didn't know exactly what the MCP server spec would be supported, we we knew that it would be extremely powerful and a great product uh for us to to utilize. And so we started building um and so taking a a more highle re recap about a year ago uh we launched our local MCP server. And what local means it was heavily designed for developer use cases. You kind of had to know what you were doing a little bit and we targeted developers because they were the first to adopt AI workflows. they would use a single plop prompt like help me implement this and a developer could pull everything that they would normally get from Figma's dev mode into their coding agent. This include things like component data, spacing, variables um and from there we just kept adding more and more re read tools like for fig jam for make um etc. But they all shared this kind of uh mutual goal to make Figma context available for develop develop developers wherever they are. So, Figma, if you don't know about Figma, um Figma is a canvas. Um and it's represented as a scene graph in C++. It's a graph of connected nodes, not unlike the HTML DOM. And we had a number of different ways we could represent the scene graph. We had this internal representation which was kind of akin to JSX or XML, effectively converting the scene graph into JSS tags and XML tags and passing those to the agent. It was abstract and sparse, but it didn't have super rigorous fidelity. Another option that we had internally was um D2R which is our like way of saying a react tailwind representation. Uh and the reason we had this is Figma has a sites product and so we already had a way of basically converting the scene graph into HTML. If you actually copy the output of the Figma MCP today and you paste into like a simple MCP or simple HTTP server, it should be pixel perfect. Um and if it's not, file a bug. Uh but um we had a hunch that this representation would be the best one because lots of the models were sort of rldled on this React Tailwind type of code. Um and we we had a suspicion that it would work really well. The last one that we kind of considered was just a plain image. But back in early 2025, 2025 agents weren't great at converting images directly to HTML or CSS or sort of other languages. And so we kind of use that as an additional piece of context, not as the sole one. And to give you what what this kind of looks like in practice, on the left here we have a a Figma frame and on the right we have the React Tailwind code. Um you can also see at the very top the image can crew meetup uh link. Uh we also basically abstract out the images within the code or sorry within the scene graph and put them at the top level. Our first attempt was just passing B 64 data into the code and that was just a terrible idea. It it just blew up the context window and was bad all around. um don't do that. Um we'd also pass an image of the current node to the agent as well. While the image by itself did not do a good job of converting to uh code, having the code context plus the image actually had better agentic output. So what do I mean by better? How did we know what was better? We tried to do evals. Um and so we did some sort of very simple eval to start with a mix of quantitative and
...[middle elided]...
ng this part was just the beginning. Um we had a lot of improvements that we wanted to make and we immediately started working on the remote server as soon as we launched. Um clients were on different timelines and we were still trying to figure out you know where we're going but we knew we wanted to get the remote server out so that's what we worked on. Um in September we launched the remote server. We ged both servers in October 2025. Um, and then we started adding read and write capabilities and kind of all these things combined ended up making for Figma one of the fastest growing products that they've ever had, which was not something we expected when we started working on this. Um, so late last year, I started working on a slightly different thing. Um, we started to see some research that designers really wanted to shift to writing production code in certain cases and we didn't really have a dedicated product for this. So I started hacking with a bunch of MCP MCP folks at an offsite and [СКРЫТО] uh which is kind of Figma's agent solution for for working on on git GitHub and and local code bases. Um and the reason I bring this up is only slightly self- serving but it relates to this this next slide. Um if there's one thing you want to take away from this talk it's that we're so early like this has not been a long time. The MC MCP spec is only two years old and we're still figuring out the best way to do things. And then second, um, Figma's done a great job of letting engineers build and figure out, uh, what's next and letting them run with it run with it. I wasn't staffed on MCP. I wasn't staffed on our make product, but I ended up helping them be built um, just because I was kind of given the leeway to do so and learning a ton along the way. Um, that's all for my talk. I'll be around today and tomorrow, but feel free to reach and happy to talk about MCP, Figma and all that. Thanks so much for your time.

---

**Claude:**

```json
{
  "is_ad": false,
  "is_news_rehash": false,
  "topic": "mcp-context-serialization",
  "signal": 0.62,
  "novelty": 0.45,
  "actionability": 0.6,
  "evidence": 0.7,
  "durability": 0.45,
  "volatility": "medium",
  "half_life_days": 365,
  "why": "Реальный разбор архитектурных решений при постройке Figma MCP server — как кодировать дизайн для LLM и почему это сработало — но контекст сильно завязан на специфику Figma и быстро меняющийся MCP-спек.",
  "knowledge_units": [
    {
      "claim": "Представление сцены как React+Tailwind кода зашло лучше, чем абстрактный JSX/XML-дамп графа сцены, потому что модели сильно RLHF'нуты именно на таком коде",
      "type": "tactic",
      "actionable": "При проектировании MCP/контекст-сервера конвертируй внутреннее представление в тот формат кода, на котором модель обучена лучше всего (например React+Tailwind), а не в абстрактный внутренний DSL"
    },
    {
      "claim": "Передача изображений как base64 напрямую в контекст раздувает окно контекста и работает плохо",
      "type": "tool-caveat",
      "actionable": "Не пихай base64-картинки в промпт как основной контекст; используй ссылки/сжатое представление, а изображение — только как дополнительный сигнал"
    },
    {
      "claim": "Комбинация текстового кода-контекста + изображения текущего узла давала лучший агентный результат, чем одно изображение отдельно",
      "type": "tactic",
      "actionable": "Для задач code-from-design используй мультимодальный контекст: текстовое представление структуры плюс скриншот, не полагайся только на vision"
    },
    {
      "claim": "Поддержка MCP-спека клиентами (Claude Desktop, Claude Code, OpenAI, VS Code) развивалась крайне неравномерно — VS Code получил полную поддержку только в июле, спустя много месяцев после релиза спека",
      "type": "tool-caveat",
      "actionable": "Проектируя под MCP, закладывайся на то, что разные клиенты поддерживают разное подмножество спека, и явно проверяй фичи (tools/resources/events) под каждый таргет клиент, а не полагайся на спек как единый стандарт"
    },
    {
      "claim": "Перед выбором формата представления контекста команда прогнала количественные и качественные evals разных вариантов (JSX-подобный дамп vs React-Tailwind vs изображение)",
      "type": "workflow",
      "actionable": "Не выбирай формат сериализации контекста интуитивно — построй простой eval, сравнивающий кандидатов на реальных агентных задачах, прежде чем коммититься"
    }
  ]
}
```
