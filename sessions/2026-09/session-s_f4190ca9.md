---
session: s_f4190ca9
date: 2026-09-19
words: 1665
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-19 · You are a strict SIGNAL filter for a senior AI engineer building real

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_f4190ca9` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

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

TITLE: Homa: The End of TCP for AI Clusters — John Ousterhout, Stanford
CHANNEL: AI Engineer (lang=en)
TRANSCRIPT SAMPLE:
[music] Please welcome to the stage the professor emmeritus at Stanford University, John Sterhout. Good morning. It's really great to be here to talk about the network side of AI applications and in particular to make the case that latency matters and it's probably going to be mattering more in the future. But I just want to say this is a talk is unusual for me. I've never before given a talk where there are fog generators in the auditorium. Just a really San Francisco experience, I guess. So, it's it's well known that AI workloads depend on really great networking performance in order to achieve their own performance. And of course, that's because the workloads are so large that they have to be distributed across machines and then you have to communicate between the machines. But what I want to talk about today is that it seems that those workloads are changing. And so I hope to do three things over the next 15 or 20 minutes. First to convince you that in fact the workloads are changing and that whereas the workloads used to be completely dominated by large transfers where throughput is the key metric that matters that we're seeing more and more smaller transfers where the latency is crucial. The second thing I hope to do is to convince you that legacy protocols like TCP and RDMMA are poorly suited to this environment. They weren't designed for this environment and unfortunately they suffer from very high tail latency when you mix small messages with large ones. I'll talk a little bit about why that's the case. Then third, I'd like to introduce Homo which is a new protocol we've developed at Stanford that actually was designed in a clean slate redesign to handle data center workloads like these and in fact it does quite well on those workloads and can reduce tail latency by an order of magnitude or more. So I'll tell you a little bit about Homa. So let's dive in. First, workloads. Historically, AI workloads have consisted of enormous transfers between machines, and that's all that really mattered. Gigabytes of data for things like weight gradients and and so on. In these workloads, what you really care about is throughput, how many gigabits per second you can pump through the pipes. And these are relatively easy workloads for networks because if it takes a while to set up the connection and start the transfer, it doesn't matter. The transfers go on for so long that all that really matters is the throughput. And so in these environments, TCP and RDMA perform pretty well. Uh, by the way, when I say RDMA, what I really mean is Rocky RDMA over converged Ethernet, which is the underlying transport that's used by RDMA for most purposes today. So anyhow, the old workloads, big transfers, throughput matters, uh the legacy protocols work pretty well. However, it appears that the workloads are changing. They're becoming more granular with smaller chunks of computation and smaller exchanges of data. And this seems to be particularly true in the world of inference and also in agentic workloads. Not so much for training workloads are still massive transfers. And so what's happening is that more and more there are small message exchanges typically for things like metadata and coordination such as checking to see if a particular entry is present in a KV cache that's distributed or doing barrier synchronization at the end of periods of compute. And for these workloads what really matters is latency. That is what's the roundtrip time to send some small piece of data across the network do a little bit of computation and get a small result back again. And in fact, it isn't just just latency or average latency that matters. What really matters is tail latency. That is, you'd like to know that if we send a whole lot of small messages, all of them will complete quickly. So, for example, we typically measure things like 99th percentile latency. And if we have high tail latency, that can limit the overall throughput of the system. So, here's an example. Suppose a common thing is to take a workload and split it up across several nodes which do intensive computation using their GPUs for some period of time and then once they've all finished their computation you do some small exchange between the nodes exchange data meta data and then it'll go on to the next round of computation and while that exchange is happening that synchronization is happening the GPUs are sitting idle so if even one of those exchanges takes a long time. It turns out the whole process stalls. You need all of those exchanges to complete before you can go on to the next phase of computation. Now, if the computation phase is say 5 seconds and it takes a few milliseconds for the exchange, you know, not a not a problem. And that's historically what it's been. But now with agentic workloads where you're trying to pump out tokens relatively rapidly at a regular rate, the periods of computation are getting down into sort of the millisecond time scale. And if it also takes milliseconds to do that synchronization, then you're wasting a significant fraction of your GPU resources waiting for the the synchronization to occur. So I'm curious. I'd like to just do a a quick audience poll here. Is there anybody here where you have reason to believe that the latency of small messages is impacting the overall throughput of your applications? If so, can you just raise your hand? See, is there anybody out there today? Actually, more hands than I expected. So quite a few people out there are raising their hands. I think this problem is likely to get worse as the trends continue. So what's going on? Why is tail latency bad? Well, typically the cause is congestion resulting from incast. So incast is when several nodes all decide simultaneously to transfer data to some destination node. And if they all send large messages, well, the links are the same everywhere in the network. So three nodes can transfer three times as fast as one node can possibly receive. And so
...[middle elided]...
s length. And then P99 is the 99th percentile, i.e. tail latency for messages of this length. So I want to point out two things. First, the P99 for short messages is dramatically better for HOM. So with TCP it's more than a millisecond tail latency. Home is less than 100 microsconds about 13 times faster. Second interestingly you might think that because Homa favors shorter messages that long messages suffer and get worse performance. It turns out that's actually not the case. Even on the longest messages, Hom is almost a factor of two better than TCP. I don't have time to explain that today, but it has to do with the fact that HOMA uses run to completion approaches which are much more effective than fair than the fair scheduling used by TCP. So, just to wrap up, the role of short messages in AI appears to be increasing. I think I think it's likely that it's going to continue to increase. We'll see over the next year or two if that happens. And I just want to pose a question to you. You know, as you're running your applications and measuring performance and seeing what the bottlenecks are, ask yourself, is high latency for short messages affecting your throughput? If the answer is yes, then just know there is a solution available. You should give HOMA a try. You can probably reduce your tail latency by an order of magnitude or more. And by the way, this is Home is basically my life mission right now. I'm sort of semi-retired from Stanford. The reason I did that is so I can spend 100% of my time hacking on Homa. So I'd be delighted to work with you and help you if you decide you want to experiment with Homa. If you need help getting started, answer questions, bug fixes, whatever, you know, I'd be happy to work with you to try and make you successful with it. So if that is interesting, feel free to contact me. My email is on the slide or you can Google me too and find me over the internet. So thanks very much for listening and hope to hear from some of you. >> [music]

---

**Claude:**

You've hit your weekly limit · resets 4am (Europe/London)
