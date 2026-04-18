# Workflow Recipe Fit Guide

This guide helps you pick which existing OB1 recipes to apply first based on how you already work day-to-day.

## What Exists in This Repo Right Now

Current recipes:

1. `recipes/email-history-import` — import Gmail history into searchable thoughts.
2. `recipes/chatgpt-conversation-import` — import ChatGPT export into searchable thoughts.
3. `recipes/daily-digest` — generate a daily summary from recent thoughts.

## Quick Decision Matrix

Pick the row that best matches your current bottleneck.

| Your bottleneck | Apply this first | Why it helps fastest | Risk/complexity |
|---|---|---|---|
| “I can’t find decisions trapped in old email.” | `email-history-import` | Pulls historical context into one searchable memory layer. | OAuth + API setup overhead |
| “I repeat ideas I already discussed in ChatGPT.” | `chatgpt-conversation-import` | Recovers prior AI conversations as searchable context. | Large exports can be slow |
| “I capture a lot but never review it.” | `daily-digest` | Adds a review habit automatically via digest delivery. | Cron + delivery provider config |

## Recommended Starting Order by Workflow Type

### 1) Heavy Email Workflow (operators, founders, client-facing roles)

**Order:**
1. `email-history-import`
2. `daily-digest`
3. `chatgpt-conversation-import`

**Why this order:**
- Email holds your historical commitments and decisions.
- Digest makes that memory useful daily.
- ChatGPT import then enriches reasoning history.

### 2) AI-First Workflow (prompting, prototyping, research-heavy roles)

**Order:**
1. `chatgpt-conversation-import`
2. `daily-digest`
3. `email-history-import`

**Why this order:**
- You recover prior AI context immediately.
- Digest builds reflection loop.
- Email import adds slower-moving background context.

### 3) Overloaded / Inconsistent Capture Workflow

**Order:**
1. `daily-digest`
2. `chatgpt-conversation-import`
3. `email-history-import`

**Why this order:**
- Digest delivers immediate behavioral payoff.
- Then recover missed AI context.
- Finally backfill email once momentum is established.

## 80/20 Implementation Plan (First Week)

### Day 1: Choose one “primary recipe”

Use the decision matrix and install only one recipe first.

### Day 2–3: Verify outcomes with concrete checks

- Can you retrieve at least 3 previously hard-to-find facts?
- Can you answer one real question faster than before?
- Do search results include source metadata you trust?

### Day 4: Add `daily-digest` if not already installed

Even if your primary recipe is import-focused, add digest next to keep the system active.

### Day 5–7: Run a real workflow drill

Test against a real project:

- Retrieve prior context (email + AI conversation).
- Draft next actions.
- Confirm the next day’s digest summarizes relevant work.

If this loop works once, your workflow integration is successful.

## Practical Guardrails

Use these guardrails to avoid common failure modes.

1. **Start with one source, not all sources.**
   - Avoid importing everything at once.
2. **Use incremental imports when possible.**
   - Prefer recent windows first to prove value quickly.
3. **Track a small success metric.**
   - Example: “time to find prior decision” before/after.
4. **Keep metadata consistent.**
   - Source, timestamp, and title fields should be present for reliable filtering.
5. **Add review cadence early.**
   - The digest habit is what turns storage into workflow value.

## What To Apply After Recipes

When recipes are working, extend into curated extensions in this order for broader workflow coverage:

1. `extensions/household-knowledge`
2. `extensions/home-maintenance`
3. `extensions/family-calendar`
4. `extensions/meal-planning`
5. `extensions/professional-crm`
6. `extensions/job-hunt`

This sequence compounds capabilities and avoids overbuilding too early.

## Personalization Template (Fill This In)

Copy this and fill it out before implementation:

```text
WORKFLOW FIT PLAN
-----------------------------
Primary bottleneck: ______________________
Chosen first recipe: _____________________
Success metric (1): ______________________
Data source to import first: _____________
Digest delivery channel: _________________
7-day review date: _______________________
-----------------------------
```

## Bottom Line

If you want the highest chance of workflow adoption, do **one import recipe + daily digest** first, prove value in one real project, then expand.
