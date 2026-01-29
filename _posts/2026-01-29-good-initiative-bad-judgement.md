---
layout: post
subtitle: When taking action leads us astray - balancing initiative and wisdom
title: "Good Initiative, Bad Judgement"
date: 2026-01-29 08:00:00 -0400
categories: [Leadership, Software Engineering]
tags: [Leadership, Decision Making, Software Engineering, Best Practices]
comments: true
social-share: true
thumbnail-img: /assets/img/will-rogers-on-judgement.jpg
thumbnail-dimensions: "width: 600px; max-width: 100%; height: auto;"
---

## Introduction

I was reminiscing about my time in the United States Marine Corps recently and remembered a story with a lesson for all of us.

In the Marine Corps, we had a saying: "good initiative, bad judgement." It came with equal parts exasperation and respect. The phrase captures the tension between taking action and making the right call.

Every Marine has a "good initiative, bad judgement" story. Here's mine.

![Will Rogers on Judgement](/assets/img/will-rogers-on-judgement.jpg)

## What Does "Good Initiative, Bad Judgement" Mean?

This phrase describes someone who:
- Identified a problem or opportunity (good)
- Took action without being told (good)
- Made a decision that, in hindsight, was wrong (not so good)

In the Marine Corps, we used this phrase to recognize leadership and initiative while pointing out the mistake. It's a teaching moment, not criticism. We train Marines to take initiative, to lead from any position, and to make decisions without orders. But not every decision is right.

## My Favorite "Good Initiative, Bad Judgement" Story

We were training on trench warfare - specifically how to assault and clear an enemy trenchline. Training ammunition only: blanks in the rifles, practice grenades with limited charge. The doctrine is simple and proven:

1. Split your force into two elements
2. Base of fire group suppresses the trench, keeping enemy heads down
3. Assault element maneuvers to the end of the trench
4. Assault throws a fragmentation grenade into the trench
5. When the frag detonates, assault jumps in and clears

I was in the base of fire group. From our position, we watched the assault element move into place. They reached the end of the trench. They got ready to jump in. And then they just... jumped in. No grenade.

Our sergeant saw the mistake immediately. The assault team had skipped step four. They were in danger.

So he took action. He pulled out a fragmentation grenade and threw it. Perfect arc, perfect distance - it landed exactly where it needed to be.

Right at the feet of our assault element. Who were now in the trench.

The grenade detonated.

No one got hurt - training grenades are designed to make noise and teach lessons, not cause casualties. But that lesson landed harder than any classroom instruction ever could.

We laughed for days. We made fun of him as only Marines can. He took it well - he knew exactly what he'd done wrong.

## Why This Was Bad Judgement

The sergeant's instincts were correct - he spotted a serious procedural error. In actual combat, jumping into a trench without clearing it first could get Marines killed. That's good initiative.

But here's what he missed: this was training, not combat. There was no enemy in that trench. The "danger" he perceived wasn't real. The assault team would have jumped into an empty trench, realized their mistake, and learned the lesson in a safe environment.

By throwing that grenade, the sergeant:
- Created actual danger where none existed
- Potentially injured his own Marines (even training grenades can cause harm at close range)
- Would have killed Marines if this had been real combat
- Bypassed the instructors letting the mistake play out as a teaching moment
- Acted on combat instincts without considering the training context

What should he have done? Let the training play out and then point out the assault force's mistakes. That's how training works - you let Marines make mistakes in a safe environment so they learn the right way before combat.

The phrase "good initiative, bad judgement" was invented for moments exactly like this.

## The Same Pattern in Software Engineering

I see this same pattern play out in software teams. The context changes from combat to code, but the dynamic stays the same: someone spots a problem, takes action, and creates a bigger problem in the process.

### The Over-Eager Refactorer

**The Initiative:** A developer notices legacy code that could be improved and spends several days refactoring it.

**The Bad Judgement:** No one asked for the refactoring. It delayed critical features, introduced new bugs, and the "legacy" code was scheduled for deprecation next quarter.

### The Premature Optimizer

**The Initiative:** Recognizing potential performance issues, an engineer implements complex caching and optimization strategies.

**The Bad Judgement:** The optimization was premature - the feature doesn't have the user load to justify the complexity, and the added architectural complexity makes the codebase harder to maintain.

### The Helpful Debugger

**The Initiative:** A developer sees production issues and jumps in to debug and fix them immediately.

**The Bad Judgement:** They bypassed the incident response process, didn't coordinate with the on-call engineer, and their fix conflicted with the proper resolution that was already underway.

### The Autonomous Architect

**The Initiative:** An engineer designs and implements a new microservice to solve a scaling problem.

**The Bad Judgement:** The engineer decided alone without architectural review, didn't consider existing services, and created unnecessary complexity when a simpler solution existed.

Sound familiar? Different context, same core issue: good intentions, lack of judgement about when and how to act.

## Why Does This Happen?

Understanding the root causes:

### 1. **Lack of Context**
- Not understanding the full business or technical context
- Missing knowledge about parallel efforts or upcoming changes
- Incomplete visibility into strategic priorities

### 2. **Inexperience**
- Haven't seen similar situations play out before
- Lack of pattern recognition for what works and what doesn't
- Overconfidence in initial assessment

### 3. **Culture and Communication**
- Unclear decision-making authority
- Poor communication channels
- Missing feedback loops
- Emphasis on "just doing it" over thoughtful deliberation

### 4. **Individual Tendencies**
- Bias toward action over analysis
- Desire to prove value quickly
- Fear of appearing indecisive
- Not knowing when to ask for help

## The Value of Initiative

Before we focus too much on the "bad judgement" part, remember that initiative itself is incredibly valuable:

- **Speed**: Organizations that encourage initiative move faster
- **Ownership**: Initiative fosters a culture of ownership and accountability
- **Innovation**: Many great innovations come from someone just trying something
- **Growth**: Taking initiative is how individuals develop judgement over time

The goal isn't to eliminate initiative - it's to improve the judgement that guides it.

## Building Better Judgement

How do we maintain high initiative while improving judgement?

### 1. **Establish Decision Frameworks**

Create clear guidelines about when to:
- Act autonomously
- Consult with peers
- Seek approval from leadership
- Present options for decision

Example framework:
- **Reversible, low-impact**: Act, then inform
- **Reversible, high-impact**: Inform, then act
- **Irreversible, low-impact**: Consult, then act
- **Irreversible, high-impact**: Seek approval

### 2. **Practice "Pause and Question"**

Before taking action, briefly ask:
- What problem am I actually solving?
- Who else might this affect?
- What information might I be missing?
- What could go wrong?
- Is this the simplest solution?

### 3. **Create Feedback Loops**

- Regular code reviews with constructive feedback
- Post-mortems that are blameless but educational
- Mentorship programs pairing junior and senior engineers
- Architectural Decision Records (ADRs) that explain rationale

### 4. **Improve Context Sharing**

- Clear roadmaps and priorities
- Regular team syncs about ongoing work
- Accessible documentation of decisions and rationale
- Open communication channels

### 5. **Embrace "Strong Opinions, Weakly Held"**

- Have a point of view (initiative)
- Be willing to change it with new information (judgement)
- Make proposals visible for feedback before implementation

## For Leaders: Creating the Right Environment

If you're in a leadership position, you shape how "good initiative, bad judgement" moments unfold:

### Do:
- **Celebrate the initiative** even when the judgement was off
- **Make it a learning opportunity**, not a punishment
- **Share your own examples** of good initiative, bad judgement
- **Clarify decision authority** for different types of choices
- **Provide context** proactively so people can make better judgements

### Don't:
- **Punish sincere attempts** that didn't work out
- **Micromanage** in response to one bad decision
- **Create blame cultures** where people are afraid to act
- **Assume malice or incompetence** - it's usually lack of context

## Finally

"Good initiative, bad judgement" isn't pure criticism. It recognizes that taking action matters, even when the specific action was wrong. We learn from both.

If you've heard this phrase, you're not alone. Initiative is the hard part. Judgement comes with experience, context, and willingness to learn.

The best engineers and leaders show both. They got there by taking action, learning from outcomes, building context awareness, and knowing when to act versus when to consult.

If you're a leader, remember: people with initiative but imperfect judgement are far more valuable than people with neither. Your job is to develop their judgement while preserving their drive.

What examples of "good initiative, bad judgement" have you seen in your career? How did you or your team grow from those experiences? I'd love to hear your stories in the comments.
