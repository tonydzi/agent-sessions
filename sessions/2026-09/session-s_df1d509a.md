---
session: s_df1d509a
date: 2026-09-25
words: 2070
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-25 · You are a strict SIGNAL filter for a senior AI engineer building real

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_df1d509a` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

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

TITLE: Robotics Has Been Stuck for 70 Years — Deepak Pathak, Skild AI
CHANNEL: AI Engineer (lang=en)
TRANSCRIPT SAMPLE:
[music] I think uh all of you know here that how much progress has AI made in the last five years. Uh seems like it's more than uh last 100 years of progress. And what is happening especially in AI is AI came for language then speech audio video and everybody's excitement is next is robotics okay and this excitement has is going on peak uh this year uh for some reason which is still beyond my uh understanding and you can also see uh leaders like Jensen talking about physical AI as the next frontier of robotics. So it seems like if you open Twitter or LinkedIn, it seems like robots robotics is already here and we'll have home robots in our homes sometime by December uh as uh as it's being said by multiple people. But I'm here to highlight that robotics has been almost here for the last 70 years [sighs] now. Those of you who got into robotics in the last four or five years, go and take any any any course in robotics and if you can distinguish the videos in robotics from 30 years ago versus today, uh I owe you a dinner. So to give you an example, let's look at this robot. So this robot here is an image and the goal of this robot is to look at this image of blocks and arrange these blocks in front of it so that it looks the same pattern as in the image. Okay, this is an extremely simple task. But if you think about this, it's a 3D block. You have to look at understand 3D from each side. And the robot can do this pretty precisely. Any guesses how old this result is? Anyone? It's a guess. You can make any guess. Huh? >> 40 years. Okay, that's the highest. [panting] This is from 1960s. This is way before there were computers. Uh, okay. So, this is this is called MIT copy demo. Uh, this was the start of uh this is this predates AI. Uh, as you know, today look at this one. >> One exhibit at the Nuclear Congress in Philadelphia has the perfect formula for >> what's happening here. The guy behind the scene is controlling these robots, a leader follower system. And if you look at any big lab, any big company, any big academic lab, how they get data, they use teley operation system, which follows the exact same principles. Any guesses for the year for this one? >> Now, everybody would correct aggressively on the year, but this is from 1957, 68 years ago. Okay? Ask anybody in your family who is older than actually they may not be around like so because this is for 60 you have to ask somebody who is [ВОЗРАСТ] what was the state of technology at that time like RAM for few KB of RAM you would have a size of a room uh like this big of a setup and this is from that time when people could make it work on not just this you keep coming back every decade the videos look as cool like here is robot a humanoid juggling playing foosball uh with human and this is also from you can see this is all they were all predate deep learning this from 8 years ago so this robot is a result from Berkeley can clean up the whole table can arrange items in a in a in a box this was done by one grad student with a single GPU machine nothing more than that okay now this picture of and if I colorize all these videos from past and apply genai filter for the modern voice you cannot tell that this [laughter] video is from 19657 or this is from today And these are not even the oldest results the oldest ones go to 1940s. Okay. So what is this that if you look at last 70 years tech every other technology every other technology has come way far language understanding computer vision mobile phone chips why is robotics is stuck in this primitive age uh for for this long and the reason is uh a general brain. Robotics has always been approached as a hardware problem from ground up and this the reason that everything around robotics has progressed but robotics is still stuck in the same land from the last 70 years. So there's a very famous paradox called Morave paradox. I don't know if you know about Moravec. He was also a CMU professor and I'm also CMU professor so have to quote him for sure. He was one of the founding figures in in AI. After 30 years of working in robotics he arrived at a very simple conclusion. Hard is easy, easy is hard. Okay. Whatever human believe to be hard is extremely easy for computers and vice versa. And you can see it happening right in front of your eyes. You would say doing math is hard. Math Olympiad gold medal is really really hard. Climbing a stair oh super easy. Now look around you in technology where we are in terms of what has been solved and what's not being solved. So this is robotics for you. Okay. It's very it is not yet another application of AI. It is what AI was founded for in the very beginning and has made very little progress towards. This is not yet another application where deep networks can come in and attack the field. This is has to be thought of with fundamentally first principles from the ground up. This is a very famous example of where you can have a you know a computer beat uh Gary Casper on chess in '90s but you can you still don't have a a a computer or robot that can pick up the chess pieces and arrange them on any chess board. Now, so how do we go about solving this? Okay, so on a more positive note, uh we have a magic sauce for AI success, right? You get big data set, you train big models and magic happens. Okay, now we know this template is working well very well in many topics. Okay, now can we apply the same recipe to robotics? Well, it's not uh directly applicable because we have no data. There is no internet of robotics data and as I said earlier you can go and collect data uh manually on the robot called telly operation and as you notice teley operation is not [ВОЗРАСТ] thing this is a 68 or [ВОЗРАСТ] thing so the the funny part is if you go back and you look at the whole evolution of GPD3 GPD4 models go back to GPD3 uh three years ago seems like a like a lifetime ago GPD3 only began working and caught people's attention when you could train those models on trillions of tok
...[middle elided]...
problem. It's not mobility problem. And we already have been delivering uh packages to with working behind the scene with many partners to delivering packages to front door of the houses uh in these areas. same setup works across warehouses and all this. Um now just to close the talk uh close the topic I mentioned this is an omnibody brain and I hope it's very clear why it's extremely essential to have an omnibody brain to build data flywheel but there's one extra benefit and the benefit is your robots may break over time and uh or the safety uh scenarios and safety is a byproduct of this omnibody brain because if you have a we can put the I'm just skipping very fast here so you can see the online this is all online uh but we can put the same brain across each of these systems each of these robots and in this case we did not even train on these robots. This is completely zero shot transfer to all these humanoids and all these things and even if the robot breaks like here the leg breaks it can recover within milliseconds because when your leg breaks your three-legged robot is a new robot. So it doesn't really matter what's the shape of the robot is anything changing here we disabled the legs of the robot it learns to learn it learns to walk on two legs in just three trials. So what you are seeing on screen is all the training for the robot that they are that that is happening in these systems. So it's it adapts in few milliseconds to uh uh 30 seconds or so. And like one example here it's it's going on wheels. You jam the wheel it starts walking. So this is a another byproduct of omnibody brain. Safety takes a very different meaning uh with these kind of models. when the robot can fly like or sorry when the robots can walk or or operate with only half the body. I removed some of the gory scenes from this but we also cut the robot in half and it can still work uh with both the two halves separately but for that you can go to YouTube uh and that's all I have. Thank you.

---

**Claude:**

```json
{
  "is_ad": false,
  "is_news_rehash": false,
  "topic": "generalist-robot-policies",
  "signal": 0.5,
  "novelty": 0.3,
  "actionability": 0.25,
  "evidence": 0.6,
  "durability": 0.6,
  "volatility": "medium",
  "half_life_days": 540,
  "why": "Доклад про то, почему робототехника топчется на месте 70 лет и как идея единой 'omnibody' модели на разных телах роботов пытается решить проблему нехватки данных — интересно как контекст про generalization и data flywheel, но узко-специфично для физической робототехники и мало применимо напрямую к LLM/агентным инженерам.",
  "knowledge_units": [
    {
      "claim": "Единая 'omnibody' модель, обученная на данных сразу с множества разных тел роботов, решает проблему отсутствия интернет-масштабного датасета для робототехники и создаёт data flywheel по аналогии с LLM.",
      "type": "principle",
      "actionable": "При дефиците данных в узкой предметной области рассмотреть обучение одной генералистской модели на разнородных, но смежных источниках вместо узкоспециализированной модели под один сценарий."
    },
    {
      "claim": "Модель, обученная на одном наборе роботов, демонстрирует zero-shot перенос на роботов, которых никогда не видела, включая измененную геометрию тела (например, сломанную ногу), и адаптируется за секунды-минуты.",
      "type": "benchmark",
      "actionable": "Использовать устойчивость к out-of-distribution конфигурациям среды/интерфейса как метрику робастности агентной системы, а не только точность на обучающем распределении."
    },
    {
      "claim": "Парадокс Моравека (то, что легко людям — тяжело ИИ, и наоборот) остаётся верным спустя десятилетия, несмотря на взрывной прогресс языковых моделей.",
      "type": "principle",
      "actionable": "Не полагаться на человеческую интуицию сложности задачи при оценке, что ИИ 'скоро автоматизирует' — моторные/физические задачи систематически недооцениваются по сложности."
    },
    {
      "claim": "Основной метод сбора данных для роботов сегодня — телеоперация, та же техника, что использовалась 68 лет назад, а не масштабный сбор данных из интернета как для текстовых LLM.",
      "type": "tool-caveat",
      "actionable": "Учитывать, что заявления о скором появлении бытовых роботов упираются в объём и разнообразие teleop-данных, а не в архитектуру моделей — полезный фильтр при оценке хайпа."
    }
  ]
}
```
