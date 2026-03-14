---
name: log
description: Append a dated session entry to LEARNING_LOG.md. Run at the end of each study session to record what was studied, the key insight, and what to study next.
argument-hint: "[optional: 'topic | insight | next' pipe-separated to log in one line]"
disable-model-invocation: true
allowed-tools: Read, Edit
---

# /log — Session Logger

Appends a new dated entry to LEARNING_LOG.md in the canonical format.

## Step 1: Read Current Log

Read `/home/psharma/projects/ai-systems-engineering/LEARNING_LOG.md` to understand the current state and most recent entry.

## Step 2: Collect Entry Data

**If `$ARGUMENTS` is non-empty:**
Parse as pipe-separated fields: `topic | insight | next`
Example: `/log "01-python / iterators | generators are pull-based | 02-math vectors"`
Use these values directly. Skip the questions below.

**If `$ARGUMENTS` is empty:**
Ask these three questions, one at a time. Wait for each answer before asking the next:

1. "What did you study today? (domain / sub-topic)"
2. "What was your main insight or aha-moment? (one thing that changed your mental model)"
3. "What should the next session cover? (specific sub-topic)"

Also ask: "Did you complete an exercise? If so, what's the filename?" (default: "none")

## Step 3: Construct the Entry

Build the entry using the canonical format from CLAUDE.md:

```
## YYYY-MM-DD

- Studied: [domain / sub-topic]
- Completed: [exercise filename or "none"]
- Insight: [the genuine insight — not a summary]
- Next: [specific next sub-topic]

---
```

Use today's date. Format: YYYY-MM-DD.

## Step 4: Prepend to LEARNING_LOG.md

Insert the new entry at the top of the file, immediately below the header section (below the `---` separator after the title and description). Maintain reverse-chronological order.

The file header looks like:
```
# Learning Log

A reverse-chronological record of weekly progress, insights, and what is coming next.

---
[NEW ENTRY GOES HERE]
## 2026-03-08
...
```

## Step 5: Confirm

Output: "Logged. Session recorded for [YYYY-MM-DD]."

The PostToolUse hook will validate the format automatically. If the hook blocks the write, fix the missing field and retry.
