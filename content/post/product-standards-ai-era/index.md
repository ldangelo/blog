---
title: "Product Standards in the AI Era: Who Reviews the AI's Work?"
date: 2026-01-30
description: "When your PM uses AI to write PRDs, you need new review processes. Here's what I'm implementing at a client."
tags: ["ai", "product-management", "process", "quality"]
categories: ["ai"]
image: "images/product-standards.jpg"
draft: true
slug: "product-standards-ai-era"
---

## The PRD That Broke My Brain

Last week, I reviewed a Product Requirements Document that was clearly AI-generated. Not because it was bad—it was actually well-structured, hit all the standard sections, and used proper formatting. 

The problem? It was *confidently wrong* about three critical technical constraints, proposed a timeline that ignored two hard dependencies, and suggested an architecture that would have violated our compliance requirements.

The PM who submitted it is talented. They'd used Claude to "help" write the PRD, and the output *looked* professional. But nobody had actually verified the AI's assumptions against reality.

This is the new failure mode in product organizations: polished documentation that nobody deeply understood before it shipped upstream.

## The Uncomfortable Truth

AI makes everyone more productive at *generating* artifacts. It does not automatically make those artifacts *correct*.

This creates a dangerous dynamic:
- **Volume goes up**: PRDs, specs, designs flow faster
- **Review bandwidth stays flat**: Same humans, same hours
- **Scrutiny per document drops**: More to review = less depth per review
- **Errors propagate further**: Bad assumptions get locked in earlier

We've accidentally created a documentation speedrun where the fastest team wins, regardless of whether they're running toward a cliff.

## The Old Model Is Dead

Traditional product review processes assumed a bottleneck at creation:
- PM spends days writing PRD
- Engineers review, push back on feasibility
- Back-and-forth iteration
- Final document represents shared understanding

The time investment in writing created natural pause points. Nobody wanted to rewrite a PRD from scratch, so they'd check assumptions upfront.

Now? AI drafts a PRD in 10 minutes. Rewriting is nearly free. So people ship drafts earlier, iterate in-flight, and treat documentation as disposable.

This isn't inherently wrong. But it requires a fundamentally different review posture.

## What I'm Implementing

At a current client (enterprise healthcare SaaS), I'm rolling out a three-layer review framework for AI-assisted product documentation:

### Layer 1: Authorship Transparency

**Requirement**: Every document must indicate AI involvement level.

Not as a scarlet letter—as context for reviewers. We use a simple header:

```markdown
## Authorship
- Primary: [PM Name]
- AI Assistance: Claude (structure, initial draft)
- Verified By: [Name] (technical feasibility), [Name] (compliance)
```

This shifts the conversation from "did you use AI?" to "who verified what?"

The PM still owns the document. AI assistance is expected. But reviewers know which sections need extra scrutiny.

### Layer 2: Assumption Callouts

**Requirement**: AI-generated sections must explicitly flag their assumptions.

We added a mandatory `## Assumptions` section that must list:
- Technical constraints assumed (verified/unverified)
- Timeline dependencies assumed (verified/unverified)
- Resource availability assumed (verified/unverified)

The "verified/unverified" tag is the key. It tells reviewers exactly where to focus their limited attention.

Example:
```markdown
## Assumptions
- [ ] **Unverified**: API rate limits can support 10K concurrent users
- [x] **Verified by DevOps**: Database can handle projected load (email from Jim, 1/28)
- [ ] **Unverified**: Legal has approved data retention changes
```

### Layer 3: Structured Technical Review

**Requirement**: Engineering review happens *before* PRD leaves draft status.

This sounds obvious. It wasn't happening consistently.

The old flow:
1. PM writes PRD
2. PM presents to stakeholders
3. Engineering gets PRD after it's "approved"
4. Engineers find problems
5. Awkward rework cycle

The new flow:
1. PM drafts PRD (with AI assist)
2. Engineering lead does feasibility review (30 min max)
3. Blockers flagged before any stakeholder presentation
4. PM revises or escalates tradeoffs
5. PRD enters formal review with technical sign-off

We added a simple checklist that engineering must complete:

```markdown
## Technical Feasibility Review
- [ ] Architecture approach is viable
- [ ] Timeline accounts for known dependencies  
- [ ] No compliance/security blockers identified
- [ ] Resource estimates are realistic
- Reviewer: _____________  Date: _____________
```

No checklist, no stakeholder meeting. Simple gate.

## The Human in the Loop Isn't Optional

Here's the uncomfortable part: these controls require human time.

AI saves time on creation. It doesn't save time on verification. In fact, it might increase verification burden because you can't assume the author deeply understands what they've written.

This is the trade-off nobody wants to discuss:

| AI Benefit | Hidden Cost |
|------------|-------------|
| Faster drafts | More documents to review |
| Lower barrier to contribution | Variable quality floor |
| Consistent formatting | Consistent errors harder to spot |
| "Sounds right" output | "Actually right" still needs humans |

Organizations that embrace AI for productivity without adjusting review processes are building technical debt in their decision-making, not just their code.

## Practical Implementation

If you're introducing similar controls, here's what worked:

### Start With High-Stakes Documents

Don't try to review everything. Focus controls on:
- PRDs for new features
- Architecture Decision Records
- Security/compliance-impacting changes
- Customer-facing documentation

Low-stakes internal docs can remain fast and loose.

### Make Templates Mandatory

The assumptions and verification sections only work if they're baked into templates. Optional fields get skipped.

We updated Notion templates so new PRDs auto-include the required sections. Can't forget what's pre-populated.

### Timebox Reviews

"Engineering must review" becomes a bottleneck if it's unbounded. 

We set a 30-minute cap for feasibility reviews. If an engineer can't assess feasibility in 30 minutes, the PRD isn't clear enough—send it back for clarification.

### Track the Metrics

We're monitoring:
- PRD revision rate after technical review (should decrease over time)
- Blockers found post-stakeholder approval (should be near zero)
- Time from draft to approval (should stay reasonable)

Early signal: revision rate dropped 40% in the first month. PMs are front-loading technical conversations because they know the gate is coming.

## The Cultural Shift

The hardest part isn't process. It's mindset.

PMs initially felt like the new requirements were "gatekeeping" or "slowing things down." Some pushback was legitimate—we over-engineered the first version and had to simplify.

But the real shift happened when we reframed it:

**Old framing**: "We don't trust AI-generated content"
**New framing**: "We verify all critical assumptions, regardless of source"

The controls apply to *all* PRDs, not just AI-assisted ones. That removed the stigma. And frankly, human-written PRDs needed the same scrutiny—they just used to get it organically through the slower writing process.

## Where This Is Heading

AI-generated content is going to keep getting better. The line between "AI-assisted" and "AI-authored" will blur. Eventually, these controls will feel quaint.

But we're not there yet. Today, in 2026, AI produces *plausible* content that requires *verification*. The organizations that build verification into their workflows will make fewer expensive mistakes.

The ones that assume AI output is correct by default? They'll learn the hard way, probably during a production incident or a missed compliance deadline.

---

## The Bottom Line

Using AI for product documentation is smart. Trusting AI output without verification is reckless.

Build the review process *now*, while the stakes are still manageable. Future you will thank present you when that first AI-hallucinated requirement doesn't make it to production.

---

*Leo D'Angelo is a Partner at Fortium Partners, providing fractional CTO services to growth-stage companies. He's currently helping enterprise clients navigate the intersection of AI productivity and operational rigor.*
