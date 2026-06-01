---
layout: post
title: "???"
subtitle: "!!!"
categories: [Software Engineering, AI]
tags: [AI, Software Engineering, Productivity, Team Leadership, AI-Assisted Development]
comments: true
social-share: true
thumbnail-img: /assets/img/operationalizing-ai-assisted-dev.png
thumbnail-dimensions: "width: 600px; max-width: 100%; height: auto;"
---

# AI Changes the Development Process More Than the Code

There’s a misconception forming around AI-assisted development: that the main change is faster coding.

It’s true. It’s just not the important part.

Here’s the shift that matters. Coding used to be the expensive thing, and documentation was optional. That’s inverting. Implementation is becoming cheap, and clarity is becoming the expensive part.

The reason is simple. Your requirements, your constraints, your architectural decisions — these used to be documentation for humans. Now they’re inputs for agents. The same artifact a developer used to skim is something a machine now reads, applies, and acts on.

That one change rewires the economics of the whole process.

## This Isn’t “Just Write Things Down”

Mature engineering organizations have always had versions of these artifacts. None of this is new advice.

What’s new is the payoff.

For decades, the case for clear requirements and recorded decisions was a discipline argument: do it because it’s professional, because future-you will thank you, because the new hire needs it. The return was real but diffuse, and easy to defer.

Now the return is immediate. A clear artifact produces better output the moment an agent consumes it. A vague one produces vague work just as fast. The cost of ambiguity moved from “someday” to “this sprint.”

That’s why the artifacts suddenly matter more. Not because we discovered documentation. Because documentation started paying for itself.

## A Chain Where Ambiguity Compounds

The modern AI-assisted lifecycle increasingly looks like this:

**Work Item → PRD → TRD → ADR → Implementation → Validation**

It’s less a set of documents and more a dependency chain. Each stage feeds the next, and each one consumes what came before.

- The **work item** defines intent.
- The **PRD** — product requirements document — defines product behavior.
- The **TRD** — technical requirements document — defines technical execution.
- The **ADR** — architectural decision record — captures decisions and their reasoning.
- **Implementation** turns it into code.
- **Validation** checks all of it against the artifacts above.

The important property of a chain is that weakness propagates. A vague work item produces a thin PRD, which produces an underspecified TRD, which produces an implementation that drifts. Ambiguity doesn’t stay contained. It compounds downstream.

The best way to see this is to follow one feature down the chain.

## One Feature, Down the Chain

Start with a typical ticket:

> “Add the ability for users to export their account data.”

Hand that to an agent and watch it guess. Which data? What format? Synchronous or a background job? What about large accounts, rate limits, the privacy implications of bundling everything into one file? It will make a dozen decisions you never made, and most of them will be wrong for your system.

Now give it a **PRD**. It defines the product intent: who needs export and why, that the output is a portable archive the user can hand to another service, that “account data” means profile, activity history, and uploaded files — but not internal audit logs. Success means a user can self-serve an export without opening a support ticket.

The guessing narrows. The agent now knows what it’s building and for whom.

Add the **TRD**. Export runs as an asynchronous job, not a blocking request. The archive is generated server-side, written to object storage, and delivered as a time-limited signed URL. One export per account per hour. The contract is a single endpoint with a documented response schema.

The space of valid implementations just collapsed to a handful.

Add the **ADR** that records *why*: async-to-storage over a synchronous download, because exports for large accounts blow past request timeouts and we’d rather not hold a connection open for ninety seconds. The alternative — streaming the response — was considered and rejected for exactly that reason.

Now the agent isn’t just constrained. It understands the constraint well enough not to “helpfully” reintroduce the synchronous version next sprint.

The implementation that comes out the other end is close to what a senior engineer would have written. Because the senior thinking happened upstream, in the artifacts, where the agent could read it.

## “Isn’t This the Documentation Burden We Hated?”

It’s the obvious objection, and it deserves a straight answer.

Yes, this front-loads work. No, it isn’t the old burden.

The documentation everyone hated had no return at the point of writing. You wrote it, filed it, and hoped someone read it. Here, the artifact pays off the moment it’s consumed — the export feature came out clean *because* the PRD and TRD existed. The cost and the payoff finally sit in the same place.

Two fair follow-ups:

*Isn’t this just waterfall again?* No. The flow is a dependency order, not a phase gate. Agents collapse the timeline — you might draft the PRD, the TRD, and a first implementation in a single afternoon, looping between them. What matters is that the constraints exist when the code gets written, not that the stages land on separate weeks of the calendar.

*What about artifacts going stale?* That’s the real risk, and a stale artifact is worse than none — a confident, wrong ADR misleads an agent faster than silence ever could. Which is exactly why validation stops being optional.

## Validation Keeps It Honest

In the old model, testing happened mostly after implementation. Now validation can run continuously, and it has something concrete to check against.

Agents can compare:

- implementation against the TRD,
- APIs against the OpenAPI spec,
- events against the schema registry,
- architecture against the ADRs.

This is what keeps the chain from rotting. When the code drifts from the TRD, or someone quietly reintroduces the synchronous export the ADR ruled out, validation catches the gap. The artifacts stay honest because something is continuously checking the work against them.

Documentation that’s enforced is documentation that survives.

## What This Does to a Team

The obvious story is that your best engineers get faster. That’s not the interesting part.

The interesting part is what happens at the bottom of the team.

When clarity drives output, a team’s floor rises. A junior developer with a solid PRD, a constraining TRD, and a set of ADRs — plus an agent — can ship work that used to require a senior. The senior judgment didn’t disappear. It moved into the artifacts, and the agent applies it on every task.

This is the real uplift. Not that the top gets higher, but that the bottom stops producing junior-quality work.

And the artifacts don’t just produce the work. They teach.

A junior who reads “why Kafka instead of RabbitMQ, and what we gave up to get there” learns reasoning, not just patterns. The context that used to live in senior heads and buried Slack threads becomes legible. Your architectural memory turns into a curriculum.

But there’s a catch worth naming.

Output uplift is not the same as capability uplift.

If the artifacts do the thinking, a developer can ship senior-level work without developing senior-level judgment. You can build a team whose output climbs while its depth stalls — and that holds up fine until the artifacts run out: a genuinely novel problem, an edge the ADRs never anticipated, or the day someone has to write the *next* decision record.

The uplift is real. But it has to be deliberate. The artifacts should be scaffolding people learn from, not a crutch they hide behind.

## The Real Shift

The biggest change here isn’t that AI replaces developers.

It’s that the distance between idea, specification, architecture, implementation, and validation is collapsing. Work that used to span a quarter of handoffs can happen in a tight loop, with agents carrying it between stages.

The teams that thrive won’t be the ones with the cleverest prompts.

They’ll be the ones with clear standards, honest decision records, and the discipline to write down what they mean.

AI rewards organizational clarity.

That may turn out to be the biggest engineering shift of all.