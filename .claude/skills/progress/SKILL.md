---
name: progress
description: Show a summary of learning progress across all 9 domains. Reads LEARNING_LOG.md and CURRICULUM.md to infer completion status, sub-topics remaining, and estimated completion date at current pace.
argument-hint: "[optional domain number, e.g. '03' for ML Fundamentals drill-down]"
disable-model-invocation: true
allowed-tools: Read
---

# /progress — Learning Progress Summary

Shows where you are across all 9 domains based on LEARNING_LOG.md entries.

## Step 1: Read Files

Read:
- `/home/psharma/projects/ai-systems-engineering/LEARNING_LOG.md` — all entries
- `/home/psharma/projects/ai-systems-engineering/CURRICULUM.md` — sub-topic lists per domain

## Step 2: Infer Domain Status

For each domain, scan LEARNING_LOG.md entries for "Studied:" fields.

Status rules:
- **Not Started** — no log entries for this domain
- **In Progress** — at least one log entry for this domain, but not all non-skipped sub-topics covered
- **Complete** — all non-skipped sub-topics appear in the log

Count unique sub-topics studied per domain (from "Studied:" fields) vs total non-skipped sub-topics in CURRICULUM.md.

## Step 3: Calculate Pace

- Count total sessions in LEARNING_LOG.md (each dated entry = one session)
- Calculate sessions per week based on date span
- Use this rate to estimate completion dates

## Step 4: Display Summary

If no domain number argument:

```
Learning Progress — [YYYY-MM-DD]
════════════════════════════════════════════════════

Phase 1 — Foundations
  01-python         [Status]   Last: [sub-topic]   [X/6] sub-topics   Est: [date or "—"]
  02-math-for-ml    [Status]   Last: [sub-topic]   [X/6] sub-topics   Est: [date or "—"]

Phase 2 — ML Core
  03-ml-fundamentals  [Status]   Last: [sub-topic]   [X/7] sub-topics   Est: [date or "—"]
  04-deep-learning    [Status]   Last: [sub-topic]   [X/9] sub-topics   Est: [date or "—"]

Phase 3 — LLMs + Production AI
  05-llms-and-genai         [Status]   Last: [sub-topic]   [X/8] sub-topics   Est: [date or "—"]
  06-mlops-and-ai-systems   [Status]   Last: [sub-topic]   [X/7] sub-topics   Est: [date or "—"]

Phase 4 — Architecture
  07-mcp                    [Status]   Last: [sub-topic]   [X/4] sub-topics   Est: [date or "—"]
  09-ai-system-architecture [Status]   Last: [sub-topic]   [X/5] sub-topics   Est: [date or "—"]

════════════════════════════════════════════════════
Pace: ~[N] sessions/week
At this pace, core curriculum complete by approximately: [date]

Next recommended session: [domain] / [sub-topic]
```

Status legend: [ ] Not Started  [~] In Progress  [x] Complete

## Step 5: Domain Drill-Down (if argument provided)

If `$ARGUMENTS` is a domain number (e.g., "03"):

```
Domain 03 — ML Fundamentals
════════════════════════════
Status: In Progress
Last studied: [date] — [sub-topic]
Sessions in this domain: [N]

Sub-topics:
  [x] supervised-learning-framework          (2026-03-15)
  [x] loss-functions-and-objectives-1        (2026-03-16)
  [~] loss-functions-and-objectives-2        (in progress)
  [ ] gradient-descent-and-optimization
  [ ] regularization-and-overfitting
  [ ] model-evaluation-and-metrics
  [ ] feature-engineering-for-ml

Recommended next: gradient-descent-and-optimization
Estimated completion: [date]
```
