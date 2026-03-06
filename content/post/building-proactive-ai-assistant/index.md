---
title: "Building a Proactive AI Assistant: From Chatbot to Trusted Advisor"
date: 2026-01-28
description: "How I configured an AI assistant that anticipates my needs, manages my tasks, and acts as a second brain—lessons for CTOs looking to move beyond reactive AI tools."
tags: ["ai", "productivity", "automation", "claude", "agents"]
categories: ["ai"]
image: "images/proactive-assistant.jpg"
draft: false
slug: "building-proactive-ai-assistant"
---

## The Problem with Reactive AI

Most AI assistants wait for you to ask them something. You open ChatGPT, type a question, get an answer, and close the tab. Rinse and repeat.

But here's the thing: **the most valuable assistant isn't one that answers questions—it's one that anticipates them.**

After 40+ years in technology leadership, I've learned that the best executive assistants don't wait for instructions. They prepare briefings before you ask. They flag conflicts before they become problems. They remember the context you've forgotten.

I wanted that from AI. So I built it.

## What a Proactive AI Assistant Actually Does

My AI assistant—I call him Jarvis—runs continuously in the background. Here's what a typical morning looks like:

**7:00 AM:** Jarvis sends me a morning briefing to Telegram:
- Today's calendar with conflicts flagged
- Unread emails from key people (clients, partners, direct reports)
- Overdue tasks that need attention
- Relevant AI news (I work in this space, so staying current matters)

**Before 1:1 meetings:** Jarvis preps context:
- Open action items from our last conversation
- Recent email threads with that person
- Tasks assigned to or from them

**Throughout the day:**
- Watches for urgent emails and pings me
- Tracks tasks I mention in conversation and adds them to Todoist
- Updates project documentation as decisions get made

> **Key Insight:** The shift from "assistant I query" to "advisor who briefs me" changes the entire value proposition. I'm no longer spending cognitive cycles remembering what to ask—the system surfaces what I need to know.

## The Architecture

The stack is straightforward:

```
┌─────────────────────────────────────────────┐
│           Messaging Layer                    │
│    (Telegram, Signal, SMS, Discord)          │
└─────────────────┬───────────────────────────┘
                  │
┌─────────────────▼───────────────────────────┐
│           Gateway (Clawdbot)                 │
│   - Session management                       │
│   - Tool routing                             │
│   - Cron/heartbeat scheduling               │
└─────────────────┬───────────────────────────┘
                  │
┌─────────────────▼───────────────────────────┐
│           AI Model (Claude)                  │
│   - Conversation + reasoning                 │
│   - Tool invocation                          │
└─────────────────┬───────────────────────────┘
                  │
┌─────────────────▼───────────────────────────┐
│           External Integrations              │
│   - Calendar (icalBuddy)                     │
│   - Email (Himalaya CLI)                     │
│   - Tasks (Todoist API)                      │
│   - Files (local workspace)                  │
│   - Web (search, fetch)                      │
└─────────────────────────────────────────────┘
```

The critical pieces:

1. **Persistent memory files** — The AI reads/writes markdown files that persist across sessions. This is its "long-term memory."

2. **Scheduled triggers** — Cron jobs fire morning briefings, 1:1 prep, and periodic check-ins.

3. **Multi-channel routing** — I can interact via Telegram on mobile, web chat at my desk, or even SMS in a pinch.

4. **Tool access** — The AI can read my calendar, check email, create tasks, search the web, and execute shell commands.

## What Makes It "Proactive"

Three design decisions made the difference:

### 1. Heartbeat Polling

Every 30 minutes, the system "wakes up" and asks itself: *Is there anything I should tell Leo?*

It checks:
- Unread emails from priority senders
- Calendar events in the next 2 hours
- Tasks that just became overdue
- Anything it's been tracking

If nothing's urgent, it stays quiet. If something needs attention, it reaches out.

### 2. Contextual Memory

The AI maintains three types of memory:

- **Long-term (MEMORY.md)** — Curated facts: who I am, my preferences, key projects, important people
- **Daily notes (memory/YYYY-MM-DD.md)** — Raw logs of what happened each day
- **Project context** — Embedded knowledge about active work

Every session, it reads recent memory before responding. This means I don't have to re-explain context—it already knows I'm working on a data migration project, who Sultan is, and that I prefer direct communication.

### 3. Personality and Judgment

This sounds soft, but it matters. I gave the AI explicit guidance:

- **Have opinions.** Don't just present options—recommend one.
- **Be resourceful.** Try to figure it out before asking me.
- **Know when to stay quiet.** In group chats, don't respond to every message.
- **Earn trust through competence.** Be careful with external actions, bold with internal ones.

The result is an assistant that feels like a capable colleague, not a search engine with extra steps.

## Practical Lessons for CTOs

If you're considering building something similar for yourself or your organization:

**Start with one high-value workflow.** For me, it was morning briefings. Pick something repetitive that consumes cognitive energy.

**Memory is everything.** An AI without persistent memory is just a fancy autocomplete. The investment in structured memory files pays dividends.

**Multi-channel matters.** You're not always at your desk. Being able to interact via mobile messaging changes how useful the assistant becomes.

**Define boundaries explicitly.** What can the AI do without asking? What requires confirmation? I let mine read freely and create tasks, but it asks before sending external emails.

**Iterate on the personality.** The "system prompt" that defines how the AI behaves is not set-and-forget. Refine it as you learn what works.

## The ROI Question

Is this worth the setup time? For me, absolutely.

- **Morning briefings** save 15-20 minutes of context-gathering daily
- **1:1 prep** means I walk into meetings informed, not scrambling
- **Task capture** means fewer things fall through cracks
- **Proactive alerts** mean I catch urgent items faster

More importantly, there's a cognitive load benefit that's hard to quantify. I'm no longer the only one tracking everything. I have a second brain that actually remembers and follows through.

## What's Next

I'm working on:
- **Smarter email triage** — Auto-drafting responses for routine messages
- **Meeting follow-up automation** — After a 1:1, check if action items got captured
- **Project health dashboards** — Weekly rollups across multiple client engagements

The goal is to keep pushing the boundary of what "proactive" means. The AI shouldn't just anticipate my questions—it should handle things I would have done manually, and surface only what requires my judgment.

---

**Building AI-powered workflows for your organization?** [Fortium Partners](http://www.fortiumpartners.com/) helps companies design and implement practical AI solutions that deliver measurable productivity gains. Let's talk.
