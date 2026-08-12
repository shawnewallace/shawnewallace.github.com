---
layout: post
title: "Generic Agents Are a Tax. Custom Agents Are an Investment."
subtitle: "A workshop experiment on writing requirements, and why the real lesson isn't 'use a custom agent' — it's 'design one properly.'"
date: 2026-08-03 12:28:07 -0400
categories: [AI, Software Engineering]
tags: [ai, agents, ai-assisted-development, github-copilot, software-engineering]
description: "A live workshop experiment comparing a generic Copilot chat to a custom Backlog Generator agent on the same requirements-writing task, and why the gap is an argument for investing engineering rigor in designing your AI assets."
thumbnail-img: /assets/img/generic-vs-custom-agents.png
thumbnail-dimensions: "width: 600px; max-width: 100%; height: auto;"
---

In the AI-augmented coding workshop I teach at Centric Consulting, where I work ([materials here](https://github.com/centricconsulting/ai-coding-workshop)), there's a module where we run the same task two ways and let the room see the gap for itself.

The task is requirements. A team wants to add a notification system to a sample app: notify a user when a task is assigned to them, when a deadline is approaching, when a task's status changes. Turn that into user stories with acceptance criteria — something a product owner could put in a sprint.

Round one, participants use standard Copilot Chat: no agent selected, just a capable model and a prompt. Round two, they select the **Backlog Generator**, a custom agent built into the workshop repo specifically for this kind of work. Same feature, same prompt, two different tools.

> *Anecdotally, across the runs I've watched, the generic pass takes about 5 times as long and burns about 5 times the tokens of the custom-agent pass, to land on requirements of similar quality.*

That token number used to be background noise — interesting, but easy to shrug off. Since the shift from flat-rate to token-based billing on June 1, 2026, it isn't background noise anymore: the tokens a generic pass burns cost real money, not just real time.

<figure class="post-figure">
  <img src="/assets/img/generic-vs-custom-agents.png" alt="Diagram comparing a generic chat pass, taking 5x the time and 5x the tokens, to a custom agent built from named components (role, context, constraints, process, output, tools, testing), reaching the same result at 1x cost" />
  <figcaption class="fig-caption">Same result, five times the cost...the difference is the design work spent up front</figcaption>
</figure>

The gap itself is worth talking about. But the headline, "custom beat generic," isn't the lesson I want people to walk away with. The lesson is underneath it: the gap only exists because *someone did design work in advance.* The Backlog Generator isn't fast because it's custom. It's fast b
ecause someone spent engineering time deciding what it should assume, what format it should output, and what it should never do, before a single participant ever typed a prompt.

## The Exercise, Concretely

This comes from Scenario 1 of [Lab 08: Workflow Agents in Action](https://github.com/centricconsulting/ai-coding-workshop/blob/main/docs/labs/lab-08-workflow-agents.md) in the workshop repo. The standard-chat prompt is generic: "Create user stories for a notification system... include acceptance criteria." The Backlog Generator agent gets the same ask, but it's not starting from nothing — its `.agent.md` definition already encodes the expected story format (INVEST principles, "As a... I want... so that..."), the level of acceptance-criteria specificity that counts as done, and the project's existing architecture conventions it should assume rather than ask about.

Standard chat has to figure out, live, in front of the room: what does a "good" user story look like here, how granular should acceptance criteria be, what's already been decided about this codebase. The custom agent already knows. That's the entire gap.

## Why This Is a Design Problem, Not a Tooling Problem

It's tempting to read "custom agent wins" as a tooling recommendation: go build agents. That's the wrong takeaway. It's the mistake I see workshop participants make in the capstone lab when they try to skip straight to a `.agent.md` file without doing the thinking that should precede it.

The [workshop's agent design guide](https://github.com/centricconsulting/ai-coding-workshop/blob/main/docs/guides/agent-design-guide.md) lays out the actual process, and none of the early steps involve writing a prompt: define the problem precisely, identify the role and perspective, define scope and boundaries (what it does and explicitly does not do), design the output format, *then* write instructions, then test against real scenarios before calling it done. A Backlog Generator agent that skipped straight to "write me a good prompt for generating backlog items" would perform closer to standard chat than to what we measure in the workshop. The value is in the decisions, not the artifact.

I made this point the spine of a talk I gave at CincyDeliver 2026, ["Agents Are Products, Not Prompts"](https://github.com/shawnewallace/agents-are-products-talk). The framework there makes the decisions explicit — a well-built agent has named components, not a paragraph: **Identity & Role**, **Responsibilities**, **Context**, **Constraints**, **Analysis Process**, **Output Format**, and **Tone**, plus a frontmatter interface (`name`, `description`, `tools`, `model`). Skip enough of those components and you tend to land in one of three failure modes: the agent is **inconsistent** (same input, different behavior), **unmaintainable** (one giant prompt nobody wants to touch), or **brittle** (requirements shift and it quietly breaks). The Backlog Generator's speed in this exercise is just what it looks like when none of those seven components got skipped.

Put plainly: **the custom agent's speed is borrowed from engineering time spent earlier, not created out of nowhere.** Someone paid the ambiguity-resolution cost once, up front, deliberately, component by component. Every generic run pays it again, live, on the clock.

## This Isn't Just About Agents

The same rigor applies to every AI asset you build into a dev process, not just agents: instructions, skills, and (in tools like Claude Code) hooks. Deciding which type an asset should be is itself part of the design work, not a detail to sort out after.

The discipline that matters isn't "generic vs. custom." It's whether you treated those assets as things worth *designing* (defined problem, defined scope, tested output format, documented constraints) or as prompts you happened to save.

## The Payoff Multiplies: Stitching Agents Into a Process

Once an agent is designed instead of prompted, a second payoff opens up — one that's easy to miss if you only ever look at agents in isolation: agents with clean components chain together.

A well-designed agent roster can span the whole SDLC — one agent for requirements, another for design review, another for QA, another for pre-merge checks — each built from the same seven components, just configured for a different role at a different point in the lifecycle. Chain them into a handoff, **Spec → Plan → Build → Review**, and "Review" stops being a human reading a diff; it becomes an agent validating the implementation against the spec it was handed, with a human approving between every step so nothing chains forward on its own.

{% include mermaid-script.html %}

```mermaid
graph LR
    A[Spec] -->|human approves| B[Plan]
    B -->|human approves| C[Build]
    C -->|human approves| D[Review]
```

That handoff only works because of the design rigor this whole post is arguing for. Output Format isn't cosmetic; it's the interface: one agent's structured output becomes the next agent's input context. A chain of well-designed agents multiplies the savings from a single one. A chain of loosely-prompted ones multiplies the ambiguity instead, and each handoff adds a new place for it to hide.

This is the version of the argument that scales past one task: design a single agent well and you save time on one job. Design a few well, with compatible interfaces, and you've built a process a human can direct instead of a task they have to keep re-explaining at every step.

## When Generic Is Still the Right Call

None of this is an argument to wrap every task in an agent. The [agent design guide's own criteria](https://github.com/centricconsulting/ai-coding-workshop/blob/main/docs/guides/agent-design-guide.md#when-to-create-an-agent) are blunt about it: a task earns an agent when it's frequent, follows a consistent pattern, requires real specialization, needs a structured output, and will repay the design time. Fewer than three of those, and a custom agent isn't worth building.

One-off, exploratory, or genuinely novel work is exactly where standard chat should stay the default. The design investment only pays off against repetition.

## The Takeaway

The number that gets people's attention is the multiple — about 5 times the time, about 5 times the tokens, same output quality. But the number isn't the point. What matters is that one of these two approaches had its ambiguity resolved by a person, in advance, on purpose; the other has to resolve it itself, from scratch, every single time it runs.

If a task is repeated often enough that this gap shows up, it's repeated often enough to justify doing the design work: define the problem, define the scope, design the output, write the constraints, test it against real scenarios.

*If this framework is useful, I go deeper on it — the full components model, plus what it takes to maintain agents like a codebase instead of a personal prompt collection — in [Agents Are Products, Not Prompts](https://github.com/shawnewallace/agents-are-products-talk), a talk I gave at CincyDeliver 2026.*
