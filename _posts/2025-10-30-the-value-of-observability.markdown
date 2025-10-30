---
layout: post
title:  "The Value Of Observability"
date:   2025-10-30 00:59:59 +0100
categories: observability
---

![Illustrated person pointing a flashlight at a giant question mark]({{ site.baseurl }}/images/observability_1.png "Observing or Struggling")

The first time I heard about observability I was around a year into my software development career. I had not heard of it before nor was I let known that it was anything of relevance prior to that moment. Someone brought it to my attention as a, ‘hey, I think you’d be interested in this’. And he was right! As someone who’s into building technical solutions that go beyond the context of specific teams but organizations more, let me share some of the reflections that got me hooked to the topic. Now we hear the term _observability_ get tossed around a lot in software conversations, but what does it truly mean? 

Before it became part of our engineering vocabulary, it came from **control theory**—a field focused on understanding and guiding system behavior. In that context, two key ideas go hand in hand: controllability and observability.

**Controllability** describes how much influence we have over a system’s behavior. If a system is controllable, it means we can move it from one state to another by adjusting its inputs—like steering a car or tuning a thermostat to reach a specific temperature. In software, this could mean deploying changes, scaling services, or modifying configurations to achieve a desired outcome. When a system lacks controllability, even the smallest adjustment might have unpredictable results, or none at all, because we can’t reliably direct its behavior. 

![Mystery box]({{ site.baseurl }}/images/observability_2.png "Input and Output")

**Observability**, on the other hand, is about insight. It tells us how well we can understand what’s happening inside a system by looking at its outputs. The two ideas are deeply connected: we can’t control what we can’t observe, and we can’t observe meaningfully what we have no way to influence. 

Put another way, we could say observability is about **ownership**—about having enough understanding of our code, our services, and their interactions to take real responsibility for how they behave in production. It’s fundamentally about fully understanding our systems.

As Charity Majors explains in [Observability — A 3-Year Retrospective](https://thenewstack.io/observability-a-3-year-retrospective/), it’s important to know how we’ve been trying to understand our systems and the changes that have taken place so far to grasp why observability is so interesting—and necessary—especially now.

# Concepts

It is often said that observability can be achieved by building **three pillars**: metrics, logs, and traces:
- **Metrics** are measurements—numerical representations of something aggregated over time intervals. They allow us to generate histograms, counters, and other aggregates, but they typically lack a rich or broad context. They generally indicate _what_ and _when_ something happened, but don't provide the detailed information as to _why_. For the latter, we usually resort to logging.
- **Logs** are timestamped records of events in the form of string outputs, (ideally) readable and understandable by most human beings. These logs usually carry more detailed information about what and when something happened.
- **Traces** are essentially structured logs with an associated context. Traces are generated from the process of tracing: following a request from its beginning to its end, which allows us to see what components and services are used in our application. This makes it easier for us to identify inefficiencies, bottlenecks, user experience problems, and other issues.

So, does observability simply consist of these three pillars? I’d say **‘no’**. These are ultimately just three types of data, and having them does not automatically guarantee observability. We can convert traces into time-series metrics, metrics into logs, and so forth. **What matters is what you do with the data, not the data itself**. Ben Sigelman explains this better in [Three Pillars with Zero Answers](https://dzone.com/articles/three-pillars-with-zero-answers-a-new-scorecard-for-observability). 

# Observability and monitoring  

At this point, the question about the relationship between observability and **monitoring** has probably already arisen. Is monitoring the same as observability? If it is monitorable, is it observable?

![Eye looking at monitor]({{ site.baseurl }}/images/observability_3.png "Monitoring")

When monitoring, at least at its origin (and the word already says so), we look at monitors. We look at a series of panels that tell us what state our systems are in from predefined sets of telemetric data. When an anomaly occurs and we try to figure out what is happening, we are not truly inspecting what happened by following a sequence of clues; instead, we often **jump directly to an assumption**:

_“I look at my panels. I see a peak of errors at X o’clock. How weird (and how bad). It seems to occur on a particular Y cluster. Ah, the last time this happened, it was because Z was running. I’m going to check for something similar to Z. Look, here it is. Confirmed.”_

As Majors explains in her retrospective, it's as if we were dealing with a big black box. It relies heavily on intuition and past experience, rather than systematically following data to verifiable conclusions. We have to **understand the possible causes and know what to ask in advance when we look at the data**.

Perhaps there is another process we could follow. Perhaps we could start by simply asking ourselves **"what happened?"** and systematically follow the data crumbs from there to the verifiable solution, whatever it may be. Majors explains that this implies having a sequence of small, testable, or refutable hypotheses. This is possible only when our data can be broken down along every relevant dimension, **captured at the right granularity to reveal meaningful patterns**. This is difficult when working with low cardinalities and if the data is aggregated prior to writing it, which is what usually happens with metrics.

![Person follows crumbs until solution]({{ site.baseurl }}/images/observability_4.png "Following Data Crumbs")

Monitoring is useful in predictable systems—those where we already know what could go wrong and the landscape of unknowns doesn’t shift much. However, we know that this is less and less common today: serverless architectures, event-driven systems, ephemeral containers, microservices… These distributed environments change the nature of our challenges. The hardest part is no longer knowing _what_ the problem is but understanding _where_ it is and _why_—it’s recognizing that what we label as “problematic” often reflects our own design choices and how we’ve allowed our systems to evolve and interact. In landscapes filled with **unknown unknowns**, monitoring tools are not enough. **Monitorable is not observable**.

Charity Majors elaborates further on the importance of clearly defining the concept of observability in her later [Observability — The 5-Year Retrospective](https://thenewstack.io/observability-the-5-year-retrospective/).

# Conclusions

![Tangled ideas and untangled ideas]({{ site.baseurl }}/images/observability_5.png "Tangled or Untangled")

So what makes a system observable? I like Majors’ take on it. A system is observable when **we can explain the unknown unknowns by following a thread that is already there.** Observability means understanding the system without having to guess, without struggling to match patterns, and without having to deploy new code just to understand those unexpected new states.

Avoiding such blind procedures—like deploying just to obtain specific information at a specific moment or struggling through tedious troubleshooting—saves time. And that time can be invested in developing, improving, and truly **adding value**.

Thinking about observability also means **curating the information** to avoid generating unnecessary data that consumes resources. To think of observability is also to think of a **democratization process**: not only developers, engineers, or people with a technical profile who know about complex telemetry data should understand what is happening. The value of observability is truly evident when the **entire organization** can get the answers to their questions and understand how our projects, our services, and our products work.

# What’s Next?

We get it—observability is about understanding our systems. But understanding alone isn’t enough. The real challenge is knowing the **technical requirements** that make observability possible, so we don’t fall for buzzwords or shiny “observability tools” that promise insight but deliver little. 

So what do we need to achieve observability? Structured events, context-rich traces, schemaless high-cardinality storage, visual tools…? These are fascinating areas to explore, and diving into them is a journey best taken together, so take your teams along with you—there’s always more to learn and discover!

<!-- ![Illustrated person struggling with questions]({{ site.baseurl }}/images/observability_6.png "Struggling with questions") -->