---
layout: post
title: "Raise the Floor, Not the Ceiling"
subtitle: "Building an AI harness the whole team shares, one reviewed asset at a time"
date: 2026-11-18 09:00:00 -0500
categories: [AI, Software Engineering]
tags: [ai, agents, harness-engineering, claude-code, teams]
description: "Instructions, skills, hooks, and agents combine into most of the prompt before anyone types a word. Checked into the repo, they give a team a shared starting point."
---

This is a follow-on to [Let's Talk About Harnesses](/2026-10-06-lets-talk-about-harnesses/). That post laid out the vocabulary: a harness decides what's in the model's context window for any given call, split into an inner harness (what the vendor ships) and an outer harness (what you build around it). This one is about building the outer harness for a team instead of one developer at a time.

## The prompt is mostly already written

Every call to the model is stateless, so whatever ends up in context has to be assembled fresh each time. Most of that assembly can happen before anyone types anything. A system prompt, a project's rules, a loaded skill, the output of a hook, all of it lands in the window ahead of the person's actual request. What they type is the delta: "fix the flaky test in billing" instead of three paragraphs re-explaining how the repo is organized, what the test conventions are, and which service owns billing logic. The less of that delta each person supplies by hand, the more consistent the team's starting point, because everyone draws from the same base instead of improvising their own.

Not every asset earns its place in context the same way:

- **Rules and `CLAUDE.md`/`AGENTS.md`**: always loaded, part of every prompt. This is the most expensive slot, token-wise, because it's paid on every call whether or not it's relevant.
- **Skills**: a short description loads at session start; the full instructions load only when the model decides the skill applies. That's the answer to the cost of the always-loaded slot.
- **Subagents**: get their own context window, so a large or noisy task doesn't pollute the parent conversation.
- **Hooks**: deterministic code that runs on a lifecycle event, not instructions the model has to decide to follow. Some feed the prompt (a `SessionStart` hook can load the current branch's ticket into context); many never touch it at all. "Please always run the linter before you finish" is a request the model can forget or deprioritize under token pressure. A hook that runs on every file edit can't.

Logging token usage is a good example. Ask the model to summarize its usage at the end of a session and it will, sometimes, skipping it under context pressure. A `SessionEnd` hook that calls a logging script does it every time, because it isn't a request to the model at all.

## What I've actually seen teams do

I've watched client teams build over-engineered outer harnesses: layered rules files, a dozen custom agents, hooks wired into every lifecycle event, all before anyone on the team had shipped a meaningful amount of AI-assisted code. The harness is sophisticated and nobody has calibrated whether it's actually improving anything, because there's no baseline to compare it to. If you've never run the team without one, you can't tell whether a harness is earning its token cost or just adding ceremony.

Often that elaborate harness lives in one person's dotfiles, not the repo. A hero dev builds a genuinely great personal setup, ships faster, and the rest of the team keeps typing three paragraphs of context into every prompt because none of it is checked in. That doesn't help the team; it just makes the gap between the hero dev's output and everyone else's more visible. The fix isn't asking them to slow down. It's asking what in their setup can move from the dotfiles into the repo. A hero dev raises the ceiling on their own output; a shared outer harness raises the floor under everyone else's. The floor is what moves a team's output.

Both are the same mistake: sophistication standing in for impact. Call it performative productivity applied to a harness. A dozen rules files and a hook on every lifecycle event look like progress, same as a hero dev's elaborate setup, but neither has been checked against a baseline. The tell isn't how much harness exists. It's whether anyone can point to what it changed.

Checking an asset into the repo doesn't settle that question by itself, but it's the precondition for answering it. A skill or rule sitting in someone's dotfiles can't be reviewed, measured, or argued with; one sitting in the repo can be. That only pays off if the team treats it with the rigor a dependency deserves: reviewed on the way in, owned by someone, revisited when it stops earning its token cost, removed when it doesn't. Checked in and never looked at again is still performative, just with more witnesses.

When a team is about to build that elaborate harness, I usually advise starting smaller than instinct wants. Small doesn't have to mean from scratch: borrow one or two community skills that fix friction you already have, run them for a few weeks, and let whatever still hurts tell you what to add next. Two I come back to across projects, both picked individually from the agent-skills collection covered below: **interview-me**, which front-loads requirements gathering by having the model interview you about the feature before writing any code, and **spec-driven-development**, where the model produces a written spec and gets it reviewed before implementation starts. I pair the second with a TDD loop: failing tests first, iterate until they pass, then a review gate at the end. Both are cheap to adopt and their effect shows up right away, which makes them a better start than a hand-built rules file nobody has stress-tested. Spec-driven development in particular bakes the engineering rigor into the process instead of bolting it on afterward: review before implementation and review after.

## Versioned, reviewed, shared

None of this is new mechanically; it's just put where a team can see it. A new rule in `CLAUDE.md` is a diff a teammate can push back on, and a new skill gets code-reviewed like any other dependency. That's the trade this whole post is about: a shared base means less variance in output across the team, not identical output, and it isn't free. Every line in that always-loaded file is paid for on every call, and more standing context brings back context rot, the failure mode from [the harnesses post](/2026-10-06-lets-talk-about-harnesses/), moved up a level from a single session to the team's shared context.

This is also where [The Instructions Are the Process](/2026-06-10-the-instructions-are-the-process/) lands at the team level: the instructions aren't documentation of the process anymore, they *are* the process, and now more than one person is depending on them being right. It's the same argument as my CincyDeliver 2026 talk, [Agents Are Products, Not Prompts](https://github.com/shawnewallace/agents-are-products-talk): once an agent or skill is shared, it has to be maintained like a codebase, not collected like a personal prompt library.

## Three sources, one outer harness

A team's outer harness comes from three sources:

- **What you write.** Your own `AGENTS.md`, your rules, your hooks, your custom agents. This is the only source tailored to your repo and your team's actual conventions.
- **What the vendor ships.** The inner harness, free for everyone using the tool, the same system prompt and tool access regardless of which repo you point it at.
- **Community assets.** Collections like Addy Osmani's [agent-skills](https://github.com/addyosmani/agent-skills): 25 skills, nine slash commands, four reviewer personas, plus reference checklists and hooks, installable across Claude Code, Copilot, Cursor, Codex, and others with `npx skills add`.

The upside of the third source is a reviewed starting point instead of a blank file. Treat it as a menu, not a bundle: pick the one skill that fixes friction you already have, and hold it to the same bar as anything you wrote yourself. The dependency risk from earlier applies, plus one more: the same skill can behave differently across tools, because each harness loads and triggers skills its own way.

## Start with one asset, not a harness

Skip the harness-building project. Pick the one piece of context you personally retype most often, whatever you find yourself re-explaining in nearly every prompt, and check it in this week as a single rule, skill, or hook. Put it through the same review anything else in the repo gets, give it an owner, and leave it there.

Then apply the test: can anyone point to what changed because it's there? If nobody can, after honest use, it wasn't worth the tokens and it comes back out. If someone can, that's your second asset, built on the same bar instead of on momentum. Raising the floor happens one reviewed asset at a time, not with a rules file written in a weekend before anyone has used it.

---

*Sources checked November 2026. Skill, command, and persona counts and supported tools from Addy Osmani's [agent-skills](https://github.com/addyosmani/agent-skills) repository. Hook events, including `SessionStart` and `SessionEnd`, from the [Claude Code hooks reference](https://code.claude.com/docs/en/hooks).*
