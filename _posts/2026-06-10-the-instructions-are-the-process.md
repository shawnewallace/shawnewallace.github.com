---
layout: post
title: "The Instructions Are the Process"
subtitle: "How the development process gets encoded so agents actually follow it"
date: 2026-06-10 00:00:00 -0400
categories: [Software Engineering, AI]
tags: [AI, Software Engineering, Productivity, Team Leadership, AI-Assisted Development]
social-share: true
thumbnail-img: /assets/img/instructions-are-the-process.png
thumbnail-dimensions: "width: 600px; max-width: 100%; height: auto;"
---

The [previous post](/2026-06-03-ai-dev-flow/) closed with a claim: get the artifact chain right at the team level and you have something replicable. That's what program-scale AI adoption actually looks like.

Replication is harder than it sounds. A process travels when it's encoded. It doesn't travel on good intentions, Slack messages about how we do things here, or the institutional memory of your best senior engineer. If the process lives only in people's heads, it stays in their heads.

This post is about the encoding — what it consists of, what each layer does, and how it maps back to the data export feature from the previous post.

<figure class="post-figure">
  <img src="/assets/img/instructions-are-the-process.png" alt="The Instructions Are the Process — conceptual map" />
  <figcaption class="fig-caption">Five mechanisms that make the artifact chain run on agents instead of good intentions</figcaption>
</figure>

## The Encoding Layer

The artifact chain — Work Item → PRD → TRD → ADR → Implementation → Validation — describes *what* gets built at each stage. The encoding layer describes *how agents are constrained to follow it*. Five mechanisms do the work:

1. **Standing Instructions** — always-on rules every task inherits
2. **On-Demand Skills** — process loaded only when a trigger fires
3. **Templates and Schemas** — structure that makes each artifact machine-readable
4. **Specialized Agents** — defined roles that own the handoffs between stages
5. **Validation and Enforcement** — continuous checks against the artifacts

Each mechanism encodes one part of the chain. Together they turn a discipline argument into a system.

## Standing Instructions

Standing instructions are the rules that apply to every task, always. In practice this is a `CLAUDE.md`, `AGENTS.md`, or whatever rules file your agent reads on startup. The content matters less than the principle: these are the constraints an agent inherits before it touches anything.

For the artifact chain, standing instructions might include:

```markdown
# Engineering Standards

- Read the TRD before writing any implementation code.
- Do not contradict an accepted ADR. If a decision needs revisiting,
  surface the conflict rather than quietly working around it.
- Artifacts live in /docs/architecture. The PRD, TRD, and ADRs for
  this project are there.
- Follow the naming conventions in CONVENTIONS.md.
```

That's it. Four rules. The temptation is to keep adding — every lesson learned, every failure mode, every edge case that burned you last quarter. Resist it. An instructions file that takes five minutes to read gets skimmed. One that takes twenty minutes gets skipped. Bloat is the main way standing instructions fail: the file grows until agents start ignoring it, and then you have the illusion of process with none of the compliance.

Treat the file as code. Review it, version it, prune it when rules are no longer load-bearing.

There's a deeper reason to keep it lean: context is finite. Everything in an agent's context window competes with the task itself — the code it's reading, the artifacts it's consuming, the work it's being asked to do. Standing instructions that sprawl don't just get ignored; they crowd out the things that matter. The encoding layer is partly a context management strategy, and the size and scope of every artifact is a decision about what deserves that space.

Storing artifacts in the repo alongside the code is what makes the standing instructions work in practice. When `CLAUDE.md` points agents at `/docs`, every agent on every task finds the same PRDs, TRDs, and ADRs without being told where to look. Every team member — human or agent — works from the same source of truth. And because the artifacts live in version control, decisions change with the code in the same commit history, and PRs that update an ADR alongside the implementation make drift visible in review.

## On-Demand Skills

Not every constraint belongs in standing instructions. The distinction is progressive disclosure: a standing instruction says *always do X*; a skill says *when you're doing Y, here's how to do it right*. Some processes are expensive to carry in context at all times but critical when a specific trigger fires. On-demand skills handle this — instructions that load only when relevant. [Brady Gaster](https://github.com/bradygaster) put it well at Microsoft Build 2026: skills are "the markdown files that tell you how to use the tools properly."

For the export feature, the relevant skill might be an ADR-writing mode: a detailed prompt that loads when an agent is recording an architectural decision. It carries the full template, the reasoning conventions, the cross-reference format for related ADRs. That content would bloat the standing instructions if it were always present. As a skill, it's available precisely when needed and invisible otherwise.

Other examples of skill-appropriate process:

- A PRD refinement mode that fires when a work item is being expanded
- A schema-review checklist for events being added to the event bus
- An API design guide for new endpoints

The test for whether something is a standing instruction or a skill: would an agent need this on a task that has nothing to do with it? If not, it's a skill.

## Templates and Schemas

Standing instructions tell agents what to do. Templates and schemas tell them what the output should look like.

Structure is what makes an artifact consumable by the next agent in the chain. A PRD written in free prose can communicate intent to a human reader. It can't reliably feed a TRD-drafting agent without ambiguity about where requirements end and background begins. A templated PRD with defined sections — user story, acceptance criteria, out-of-scope items, open questions — produces output the next stage can parse.

A minimal PRD template for the export feature looks something like:

```markdown
## User Story
As a [user], I want to [action] so that [outcome].

## Acceptance Criteria
- [ ] ...

## Out of Scope
- ...

## Open Questions
- ...
```

See a [real TRD example](https://github.com/shawnewallace/spine/blob/main/docs/trd/trd-password-recovery.md) for the technical equivalent. The ADR template follows the same logic. [Michael Nygard's original format](https://cognitect.com/blog/2011/11/15/documenting-architecture-decisions) — context, decision, consequences — is short enough to stay lean and structured enough to be machine-readable. [MADR (Markdown Architectural Decision Records)](https://adr.github.io/madr/) adds a "considered options" section that's worth the extra lines when the decision space matters.

At the machine-readable edges, templates give way to schemas. The export feature's API contract lives in an OpenAPI spec. The event it emits when the archive is ready lives in the schema registry. These aren't documentation artifacts. They're executable contracts. They're what the validation layer checks against.

## Specialized Agents and the Handoffs

Templates define the shape of each artifact. Specialized agents own the transitions between them.

A specialized agent is more than a prompt with a role. Each one is a fully scoped unit: a persona that shapes how it reasons and communicates, a model selected for the demands of the work, the tools it's allowed to use, and the instructions that constrain its behavior. A BA agent drafting a PRD doesn't need code execution tools. An architect agent recording a decision doesn't need the same model as a validation agent running contract tests. Scoping the agent tightly keeps its context clean and its behavior predictable — the same logic that keeps standing instructions lean applies here.

The chain has natural agent boundaries:

- A **BA agent** takes the work item and produces the PRD. Its inputs are the ticket and any relevant product context. Its output is a templated PRD ready for technical review.
- An **architect agent** takes the PRD and produces the TRD and any ADRs the design requires. It reads existing ADRs from standing instructions before proposing new decisions.
- An **implementation agent** takes the TRD and writes code. Its standing instructions prevent it from contradicting accepted ADRs. It doesn't touch the PRD.
- A **validation agent** checks the implementation against the TRD, the API against the OpenAPI spec, and the events against the schema registry.

Follow the export feature through this:

The BA agent reads the ticket — "add the ability for users to export their account data" — and produces a PRD. It defines the user: someone offboarding who wants a portable archive. It defines scope: profile, activity history, and uploaded files; not internal audit logs. It defines success: self-serve, no support ticket required.

The architect agent reads the PRD and drafts the TRD: async job, object storage, signed URL delivery, one export per account per hour. It checks existing ADRs and finds nothing that governs large-payload delivery. It drafts a new ADR: async-to-storage over synchronous download, because exports for large accounts blow past request timeouts. Synchronous streaming was considered and rejected.

The implementation agent reads the TRD. The ADR is in its context. It builds the async job, writes to object storage, returns the signed URL. It doesn't reintroduce the synchronous path because the ADR is present and its standing instructions say not to contradict accepted decisions.

The validation agent checks the endpoint against the OpenAPI spec, checks the completion event against the schema registry, and diffs the implementation against the TRD.

Each agent has a defined input, a defined output, and a defined scope. Handoffs happen through the artifacts, not through shared state or implicit context.

## Validation and Enforcement

Validation keeps the chain honest. Here's what it looks like in practice.

Contract tests run against the OpenAPI spec on every build. If the implementation drifts from the documented contract — different response shape, undocumented field, missing error code — the build fails. This is enforced documentation. It doesn't rely on developers remembering to update the spec.

ADR conformance checks flag when an implementation pattern contradicts a recorded decision. The export feature's ADR ruled out synchronous downloads. A check that looks for blocking HTTP calls in the export module catches violations before they merge.

Schema validation runs event payloads against the schema registry. If the completion event drops a required field or changes a type, it fails before it reaches the broker.

These checks can run as pre-commit hooks, in CI, or inside an agent's own self-check loop. The location matters less than the consistency. Checks that run sometimes catch drift sometimes. Checks that always run maintain the chain.

## Start Small, Then Encode

Don't try to encode everything on day one. One `CLAUDE.md` with four rules. One ADR template. One agent with defined inputs and outputs. Run it on a single feature — the export feature, or whatever's in your current sprint — and watch where the process breaks down.

The gaps are where the next encoding goes.

A culture you can't enforce is a hope. A process you encode is a system.

---

## References

**Standing instructions and skills**

- [github/awesome-copilot](https://github.com/github/awesome-copilot) — A catalog of community-contributed custom instructions and chat modes for Copilot. Useful as a reference for what teams actually put in these files.
- [AGENTS.md](https://agents.md/) — An open, cross-tool standard for repo-level agent instructions. Claude Code reads `CLAUDE.md`, which you can symlink to `AGENTS.md` so one file serves every agent.

**Templates and schemas**

- [github/spec-kit](https://github.com/github/spec-kit) — GitHub's spec-driven-development toolkit. Its Spec → Plan → Tasks → Implement flow is the artifact chain with each phase emitting a Markdown artifact that feeds the next.
- [adr.github.io](https://adr.github.io/) — The community hub for Architecture Decision Records, with lightweight templates (Nygard's original, MADR, Y-Statement).

**Specialized agents and handoffs**

- [addyosmani/agent-skills](https://github.com/addyosmani/agent-skills) — Production-grade engineering skills (spec, plan, build, test, review) plus reusable agent personas. Addy's framing is nearly identical to the argument here: agents are capable but undisciplined unless you encode the discipline so they can't skip it.
