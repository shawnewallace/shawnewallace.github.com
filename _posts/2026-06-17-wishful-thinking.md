---
layout: post
title: "Wishful Thinking?"
subtitle: "A working developer's honest take on where AI actually stands in software engineering"
date: 2026-06-17 09:00:00 -0400
categories: [AI, Software Engineering]
tags: [ai, software-engineering, career, agentic-ai, developer-tools]
description: "Two years into working with AI tools every day, here's my honest assessment of what's changed, what hasn't, and why I'm cautiously optimistic about the future of software engineering as a profession."
thumbnail-img: /assets/img/wishful-thinking.png
---

I've been building software with AI tools in the mix for about two years now. Not as an observer or a skeptic writing hot takes from the sidelines. Actually using these things, every day, on real projects. I've been asked for my take enough times that I figured I'd write it down. So here's my honest, mid-2026 take. Caveat upfront: this stuff is moving fast. Anything could change. But this is where I think we are right now.

## AI is good at code. It's not good at *software.*

The most important distinction I can make: generative AI is excellent at writing code. It's fast, it's often correct, and it handles boilerplate that used to eat up hours of a developer's day. For an experienced engineer, it's an incredible accelerant. I feel the difference every week.

But writing code and engineering software are not the same thing. A system isn't a pile of code; it's a set of decisions about structure, boundaries, tradeoffs, and constraints. How do you slice the problem? Where do the services break apart? What breaks under load? How do you know when it's *done*? How do you know when it's *correct*? Those questions require judgment, and judgment is expensive to develop and hard to fake.

AI can envision the rough shape of a system. It can write the pieces once you've made the architectural decisions. But the composing, the connective tissue, the judgment calls about what matters — that part still belongs to humans. At least for now.

<figure class="post-figure">
  <img src="/assets/img/wishful-thinking.png" alt="A senior engineer gestures across a bridge toward a junior developer, with AI-generated code on one side and architectural diagrams on the other" />
  <figcaption class="fig-caption">The bridge still needs a builder — and someone to teach the next one how to cross it</figcaption>
</figure>

## The split that isn't being talked about enough

Here's the pattern I keep seeing: AI is expanding the reach of senior engineers and quietly leaving junior engineers behind.

Studies confirm what many of us already feel. Experienced developers with strong "taste" (a sense of what good code looks like, what a bad architectural choice looks like a mile away) are getting a meaningful productivity boost from AI tools. They know when to trust the output and when to push back. They know that a `sleep()` isn't a fix for a race condition, even if a frontier model tells them it is.

Early-career developers don't have that yet. And this is where it gets tricky: a junior developer can now use AI to produce code that *looks* senior. It ships. It passes review. But they didn't understand what they wrote, and they didn't learn from writing it. That's a different kind of problem than writing bad code. Bad code is at least educational. Rubber-stamping AI output isn't.

Scott Hanselman and Mark Russinovich put it well at Microsoft Build this year: senior engineers who know what they're doing *get a boost* from AI. Early-in-career people, without the context to evaluate what the AI is producing, can actually be *dragged down* by it.

## The preceptorship problem

Here's the part that deserves more attention.

How does someone become a senior engineer? Traditionally, you come in junior, you get thrown into the deep end, you break things, you fix things, you pair with someone more experienced, you read code you didn't write, you learn from it. You develop taste by exposure. It takes years.

AI now handles the tasks junior developers used to learn on. Bug fixes, build pipelines, test generation. These used to be entry-level work. Now they're AI work. So if you bring an early-career engineer in today, what exactly are they going to do to build that foundation?

At Microsoft Build, Hanselman and Russinovich proposed something they call a *preceptorship* model, borrowing the concept from nursing. In hospitals, a nurse preceptor isn't just a senior nurse who happens to share a shift. They're formally trained to develop other nurses. The responsibility is explicit: your job is to make more seniors. The onus is on the experienced person, not on the junior to claw their way up.

They published a paper on this in *Communications of the ACM*: ["Redefining the Software Engineering Profession for AI"](https://dl.acm.org/doi/10.1145/3779312). The idea is straightforward: pair early-career developers with senior engineers who use AI augmentation *together*, with the senior explaining their thinking, questioning the output, and actively teaching, not just producing. The goal is to engage the junior's brain, not bypass it.

I think they're right. And the stakes are real: if we stop developing junior engineers, we don't have fewer engineers now — we have a hollow pipeline in five years.

## What AI still doesn't do

The list of what's still firmly human is longer than the discourse suggests. I've written about what this looks like in practice — [encoding process into artifacts](/2026-06-03-ai-dev-flow/) and [making those artifacts travel across a team](/2026-06-10-the-instructions-are-the-process/) — but the short version is: the judgment that makes any of that work is still entirely human.

Envisioning the problem in the first place. AI is great at executing against a well-defined spec, but someone has to decide what the right problem is. That's product thinking, stakeholder communication, and judgment about what matters. None of which is in the model.

Testing *strategy*, as opposed to test authoring. AI can write tests for you. It cannot tell you whether you're testing the right things, whether your coverage strategy is sound, whether you're testing behavior or implementation. Those require someone who understands the system's intent.

Infrastructure judgment. Knowing which cloud primitive to reach for, when to use a queue versus a database, how to think about failure modes at scale — this is hard-won knowledge that doesn't translate cleanly into a prompt.

Knowing when something is done and correct. This is subtle but important. AI can keep generating solutions. It takes a human to say: this is good enough, ship it. Or: no, this is wrong, here's why. That final arbitration requires accountability and context that models don't have.

## So: is this "still" a real job?

I caught myself using the word "still" in a draft of this post ("software developers *still* need to...") and it struck me as funny. It's a word that implies imminent departure, like we're on borrowed time. I'm not sure that's right.

The data tells a different story. Software development job postings in the US are up roughly 10% year over year, according to Indeed data tracked by the Federal Reserve Bank of St. Louis. They're still below the post-pandemic hiring boom, but the trend is recovering. The narrative of wholesale replacement isn't showing up in hiring numbers. What's happening is a *reshaping* of who gets hired and what for.

Companies are concentrating hiring at the senior end, because that's where the AI multiplier effect is strongest. That's rational in the short term. It's a problem in the medium term, for exactly the reasons above.

We're not being replaced. We're being restructured. And the profession survives and grows if we're intentional about solving the pipeline problem before it becomes a crisis.

## The real wishful thinking

When I called this post "Wishful Thinking," I was thinking about the hope that things will just... work out. That the junior pipeline will sort itself out, that AI will figure out system design, that the market will correct on its own.

That's the wishful thinking worth worrying about.

The grounded hope is that we'll build more software than ever, more complex than ever, and we'll need more skilled people to build and maintain it. That's not wishful thinking. That's the trajectory.

But we have to earn it. And this isn't abstract for me — my son is four years into his career as a software developer, and I think about this pipeline problem with him in mind. We have to deliberately bring new engineers up as AI paves over the traditional on-ramps. We have to formalize knowledge transfer when a senior and junior work alongside an AI agent. And we have to stop declaring the problem solved just because AI can write the code.

The job of software engineering isn't going away. But it's changing shape fast, and the shape it takes is partly up to us.

---

*This is my personal read on the industry as of June 2026. Things will likely look different by the time you read this. For the Microsoft Build session that inspired the preceptorship discussion, see [BRK247: Scott and Mark learn...how agents reshape software engineering](https://build.microsoft.com/en-US/sessions/BRK247). Software development job posting data from [FRED, Federal Reserve Bank of St. Louis / Indeed](https://fred.stlouisfed.org/series/IHLIDXUSTPSOFTDEVE).*
