---
title: "What Simon Willison Gets Right About Agentic Engineering (And What I'd Add From the Trenches)"
date: 2026-03-05
description: "Simon Willison's Agentic Engineering Patterns guide is the best practical resource I've seen for engineering leaders adopting AI coding agents. Here's what resonates from the field — and what's missing."
tags: ["ai", "engineering", "claude-code", "patterns", "leadership"]
categories: ["ai"]
image: "images/agentic-patterns.jpg"
draft: true
slug: "agentic-engineering-patterns"
---

# What Simon Willison Gets Right About Agentic Engineering (And What I'd Add From the Trenches)

Simon Willison recently published [Agentic Engineering Patterns](https://simonwillison.net/guides/agentic-engineering-patterns/), a living guide to getting better results out of coding agents like Claude Code and OpenAI Codex. It immediately shot to the top of Hacker News with over 500 upvotes, and for good reason — it's the most practical, opinionated guide I've seen on the subject.

As a fractional CTO who's been deploying AI coding agents across multiple client organizations for the past year, I want to unpack what resonates from the field, what I'd push further, and what I think is missing from the conversation entirely.

## "Writing Code Is Cheap Now" — Yes, But That's Not the Hard Part

Willison's opening thesis is that code production has dropped to near-zero cost, and our engineering habits haven't caught up. He's right. The entire edifice of software estimation, sprint planning, and feature prioritization was built on the assumption that developer time is scarce and expensive.

But here's what I've observed in practice: **the cost didn't disappear, it shifted.**

When I introduce Claude Code to a development team, the first week is euphoric. Engineers are producing 3-5x more code. PRs are flying. It feels like magic.

By week three, a different picture emerges. Code review queues are backed up. Test coverage is slipping because the volume of changes outpaces the testing discipline. And someone has introduced a subtle architectural inconsistency that won't surface until it becomes load-bearing.

The cost of producing code dropped. The cost of *governing* code stayed the same — or increased. This is the real leadership challenge of agentic engineering, and it's one that individual contributor guides tend to underweight.

## "Hoard Things You Know How to Do" — The Organizational Version

This is my favorite pattern in Willison's guide. His advice: collect working code examples for every interesting problem you solve. Your blog posts, repos, TIL notes, and proof-of-concepts become incredibly powerful inputs for coding agents later.

He demonstrates this beautifully with his recombination pattern — telling an agent to combine two existing working examples into something new. He had Tesseract.js for OCR and PDF.js for PDF rendering. He told Claude to combine them. Minutes later: a working browser-based PDF OCR tool.

**Where I'd push this further: make it organizational, not personal.**

At the individual level, hoarding is natural for senior engineers. But in a team context, the question becomes: where do these patterns live so that *everyone's* agents can use them?

This is exactly the problem we've been solving with CLAUDE.md files and agent instruction repositories. When I onboard a new client, one of the first things we build is a shared knowledge base that agents can reference:

- **Architecture decision records** that agents read before proposing changes
- **Code pattern libraries** with working examples of "how we do X here"
- **CLAUDE.md files** at the repo root that encode team conventions

The individual hoard becomes a team hoard. And the team hoard is what scales agentic engineering from "one productive developer" to "a productive organization."

## Red/Green TDD — The Four Words That Changed Everything

Willison identifies "Use red/green TDD" as a four-word prompt that transforms agent output quality. Write tests first, confirm they fail, then implement until they pass.

I cannot overstate how much I agree with this. In my experience across multiple engineering teams, this single pattern accounts for more quality improvement than any other intervention.

But here's the nuance from the field: **most teams don't do TDD, even without agents.**

The reality is that many organizations I work with have spotty test coverage, inconsistent testing patterns, and engineers who view tests as an afterthought. Introducing agents into this environment doesn't fix the problem — it amplifies it. Now you have 3x more untested code.

My approach has been to use the agent adoption itself as the catalyst for testing discipline:

1. **Make it non-negotiable in agent instructions.** Every CLAUDE.md includes "Always use red/green TDD. Write tests first, confirm they fail, then implement."
2. **Use the speed argument.** "Tests aren't slower with agents — they're effectively free. The agent writes them in seconds. You have no excuse."
3. **Demonstrate the feedback loop.** When an agent writes tests first, it catches its own mistakes before you review the code. This is self-correcting AI development, and it's remarkably effective.

The teams that adopt this pattern see measurably better outcomes within weeks. The teams that skip it accumulate technical debt at an accelerated rate.

## "First Run the Tests" — Establishing Context

Another brilliant four-word prompt. Start every agent session with "first run the tests." This forces the agent to discover the test suite, understand the project's scope, and enter a testing mindset.

I'd add a companion prompt that I use with every new agent session on an existing codebase:

**"Read the CLAUDE.md, then run the tests."**

This two-step opener gives the agent both the *cultural context* (how this team works, what patterns to follow, what to avoid) and the *technical context* (what the codebase does, how it's tested, what's currently passing).

It's the difference between hiring a contractor and throwing them at the code versus giving them a 10-minute orientation first. The orientation costs almost nothing and saves hours of misalignment.

## The Anti-Pattern That Keeps Me Up at Night

Willison's anti-pattern section focuses on "inflicting unreviewed code on collaborators" — filing PRs with agent-generated code you haven't reviewed yourself. He's absolutely right, and this is the single most common problem I see in organizations adopting AI coding tools.

But I'd add a more insidious variant: **the architecture drift anti-pattern.**

This is when multiple engineers are independently using agents to build features, and each agent makes locally reasonable but globally inconsistent architectural decisions. One agent builds a service with REST, another uses GraphQL, a third introduces a message queue that nobody asked for.

None of these are wrong in isolation. But collectively, you end up with a codebase that looks like it was built by a dozen different teams with different philosophies — because it was.

The fix is what I call **architectural guardrails in agent instructions:**

- Define your patterns in CLAUDE.md: "We use REST for synchronous APIs, SNS/SQS for async messaging, no GraphQL."
- Include examples of existing patterns: "Look at /src/services/patient for the canonical service implementation."
- Explicitly prohibit common agent tendencies: "Do not introduce new dependencies without human approval. Do not create new infrastructure patterns."

This isn't about limiting creativity. It's about maintaining coherence at scale — the same problem you'd have with any fast-growing engineering team, just accelerated by 10x.

## What's Missing: The Leadership Layer

Willison's guide is excellent for individual engineers. But there's a whole layer of organizational adoption that's barely discussed in the broader discourse:

**How do you manage a team that's 3x more productive but also 3x more chaotic?**

Some things I've learned:

1. **Code review becomes the bottleneck.** Plan for it. Consider dedicating senior engineers to review rather than production. The leverage is higher.

2. **Sprint velocity metrics become meaningless.** If a team was delivering 30 story points and now delivers 90, you haven't gotten 3x better — you've changed the unit of measurement. Track outcomes, not output.

3. **Junior developers need more guidance, not less.** The temptation is to hand everyone Claude Code and expect equal results. In practice, senior engineers get dramatically more value because they know what to ask for and can evaluate the output. Juniors need structured patterns and paired agent sessions.

4. **You need an AI champion on the team.** Someone who's deep in the tools, experiments with new patterns, and disseminates what works. This isn't a full-time role — it's a mindset that one or two engineers on every team should have.

## The Bottom Line

Simon Willison has given us the best practical foundation I've seen for individual agentic engineering. If you're an engineer using Claude Code or Codex, read his guide — it's essential.

What I'd add is the organizational perspective: how these patterns compose when you have 10 or 50 engineers all using agents simultaneously. That's where the real complexity lives, and it's where engineering leadership needs to evolve.

The teams that will win aren't the ones with the best individual prompt engineers. They're the ones that build systems — CLAUDE.md files, testing discipline, architectural guardrails, review processes — that make the whole organization productive with agents, not just the early adopters.

Code is cheap now. Coherence never was.

---

*Leo D'Angelo is a Partner at [Fortium Partners](https://fortiumpartners.com), where he serves as fractional CTO for growth-stage technology companies. He's been deploying AI coding agents in production engineering teams since 2025.*
