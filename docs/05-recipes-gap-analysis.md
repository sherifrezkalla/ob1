# Recipes Gap Analysis (Reference Commit vs Current Implementation)

## Scope and Limitation

I attempted to directly inspect the reference path at commit `cd349a57cd7111c889e222f7d04fd47d433b9f48` from:

- `https://github.com/NateBJones-Projects/OB1/tree/cd349a57cd7111c889e222f7d04fd47d433b9f48/recipes`

However, outbound GitHub access in this environment returned HTTP 403, so a direct remote diff was not possible.

Given that limitation, this analysis compares:

1. The **current local `recipes/` implementation**.
2. The **current local extension implementations** (as the "gold standard" for completeness and runnable quality).

Use this as a practical improvement map for your recipes.

---

## What’s Good in Current Recipes

Your recipe READMEs already have strong structure and intent:

- Clear “What It Does” sections.
- Explicit prerequisites.
- Credential tracker blocks.
- Expected outcome and troubleshooting sections.
- Consistent metadata files with difficulty, tags, and estimated time.

This gives you a strong documentation baseline.

---

## Main Gaps vs Your Stronger Implementations (Extensions)

Compared to extension docs/code quality, recipes are currently less executable.

### 1) Step-by-step sections are placeholders

In multiple recipes, the Steps block still includes TODO placeholders and high-level bullets instead of copy/paste commands.

**Impact:** Users can understand intent but cannot reliably complete setup without improvising.

### 2) Recipes don’t consistently include runnable artifacts

Extensions include concrete files (`schema.sql`, TypeScript server code, build config, package metadata). Recipes currently focus more on narrative than execution assets.

**Impact:** High variance in user success; hard to validate and maintain.

### 3) Validation flow is weaker than extensions

Extensions generally include explicit test prompts/queries and runtime checks. Recipes could define exact verification commands and expected outputs.

**Impact:** Users may think setup succeeded even when partial failures occurred.

### 4) Operational hardening patterns are under-specified

For import-style recipes (Gmail, ChatGPT exports), extensions suggest stronger patterns that recipes can borrow:

- checkpointing / resume behavior
- idempotency keys
- duplicate detection
- rate-limit/backoff strategy
- batch-size controls
- dry-run mode

**Impact:** risky on large imports and repeated runs.

### 5) Security conventions can be made more explicit

The repo strongly emphasizes secret hygiene, but recipes can tighten concrete guidance for env handling and least privilege keys.

**Impact:** users may accidentally use overly broad credentials or leak secrets in command history.

---

## What Is Most Useful to Reuse Right Now

Prioritized list of improvements you can apply to recipes quickly.

### Priority A — Make each recipe truly runnable

For each recipe folder, add:

- `scripts/` with executable import/generation scripts.
- `package.json` with `dev`, `build`, and `run` scripts.
- `.env.example` listing required environment variables.
- `CHECKLIST.md` with a start-to-finish validation flow.

### Priority B — Upgrade README steps from conceptual to deterministic

Transform each "Steps" section into:

1. exact prerequisites check command(s)
2. install/build command(s)
3. configuration command(s)
4. execution command(s)
5. verification SQL/tool command(s)
6. rollback/retry guidance

### Priority C — Add import safety controls (for import recipes)

For `email-history-import` and `chatgpt-conversation-import`:

- `--dry-run`
- `--batch-size`
- `--since` / `--after`
- `--resume-from`
- duplicate prevention by source message/conversation ID
- summary report at end (processed/inserted/skipped/failed)

### Priority D — Add minimal acceptance tests

Per recipe, define 3 checks:

1. **Schema check** (table/function exists)
2. **Write check** (one known insert succeeds)
3. **Query check** (search/filter returns expected row)

Automate with lightweight scripts where possible.

### Priority E — Standardize recipe maturity states

Add a field in `metadata.json`:

- `status`: `draft | beta | stable`

And document minimum criteria for moving to `stable` (runnable script, verified commands, troubleshooting completeness).

---

## Recipe-by-Recipe Suggestions

## `recipes/email-history-import`

Useful upgrades:

- Add OAuth bootstrap script and token caching location conventions.
- Add importer with pagination + exponential backoff.
- Store deterministic source key (Gmail message ID) in metadata for idempotent reruns.
- Provide a “small mailbox first” command path for safe initial validation.

## `recipes/chatgpt-conversation-import`

Useful upgrades:

- Add parser script for `conversations.json` with schema guards for malformed nodes.
- Add chunking policy for very long conversations before embedding.
- Persist source identifiers and import timestamp to support incremental updates.
- Emit per-conversation error log while continuing import.

## `recipes/daily-digest`

Useful upgrades:

- Include complete edge function template (not just description).
- Provide exact cron SQL statements and timezone examples.
- Add "send-to-self test" mode for manual runs.
- Add fallback delivery policy (Slack if email provider fails).

---

## Practical Implementation Plan (1–2 Days)

### Day 1

1. Pick one recipe (recommend: `chatgpt-conversation-import`).
2. Add runnable script + `.env.example` + deterministic README commands.
3. Add verification SQL and expected output examples.

### Day 2

1. Replicate the same structure for `email-history-import`.
2. Add import resilience controls and end-of-run stats.
3. Mark both as `beta` in metadata after successful local run.

Then tackle `daily-digest` with full edge function sample and cron verification.

---

## Suggested Definition of Done for Recipe Quality

A recipe is ready when it has all of the following:

- No TODO placeholders.
- End-to-end commands runnable from a clean machine.
- `.env.example` and explicit secret handling guidance.
- Idempotent rerun behavior (or clear warning if not supported).
- Verification commands with expected results.
- Troubleshooting that covers at least the top 3 failure modes.

---

## Bottom Line

Your current recipes are strong as **instructional drafts**, while your extension implementations are stronger as **production-grade templates**. The fastest win is to bring extension-level execution rigor (scripts, deterministic commands, verification checks, and safety controls) into each recipe.
