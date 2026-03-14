---
name: study
description: Start a daily AI/ML learning session. Reads LEARNING_LOG.md and CURRICULUM.md, uses a planning agent to determine the next topic, structures a 2-3 hour session, teaches the concept, runs a practical exercise, and produces a log entry.
argument-hint: "[optional topic override, e.g. 'transformers' or '03 loss functions']"
disable-model-invocation: true
allowed-tools: Read, Edit
---

# /study — Daily Learning Session Driver

This is the primary daily command. It orchestrates the full 2-3 hour learning session.

## Step 1: Read Current State

Read the following files:
- `/home/psharma/projects/ai-systems-engineering/LEARNING_LOG.md` — find the most recent entry, extract the "Studied:" and "Next:" fields
- `/home/psharma/projects/ai-systems-engineering/CURRICULUM.md` — full curriculum map

## Step 2: Invoke Planning Agent

Use the Agent tool (subagent_type: general-purpose) with this prompt:

```
You are a learning session planner. Given the LEARNING_LOG.md and CURRICULUM.md below, determine:
1. The recommended next sub-topic to study (with rationale)
2. Any prerequisite gaps that should be addressed first
3. Whether this should be a 2h or 3h session (default 2h; suggest 3h for complex topics like transformers, attention, RAG, inference optimization)
4. Session time breakdown
5. A goal statement: "After this session the learner will be able to..."

Follow the plan-session skill logic:
- Check the "Next:" field in the last log entry as the primary signal
- Verify prerequisites are met (see prerequisite map in plan-session skill)
- Respect Phase 1 track alternation (Python Mon/Wed/Fri, Math Tue/Thu)
- If on final sub-topic of a domain, suggest a capstone exercise

LEARNING_LOG.md:
[paste full content]

CURRICULUM.md:
[paste full content]

Return your recommendation in structured format.
```

Wait for the agent to return. Use its recommendation as the session topic.

## Step 3: Handle Topic Override

If `$ARGUMENTS` is non-empty:
- Override the agent-recommended topic with the user's specification
- Acknowledge explicitly: "Overriding auto-recommended topic. Studying: [user topic] as requested."
- Proceed with the user-specified topic

## Step 4: Announce Session Plan

Present the session plan clearly:

```
Session Plan — [YYYY-MM-DD]
─────────────────────────────
Domain:    [number - name]
Topic:     [sub-topic name]
Duration:  [2h / 3h]

Time breakdown:
  [X] min  Concept teaching
  [X] min  Practical exercise
  [X] min  Production context + architecture
  [X] min  Reflection + log prep

Goal: After this session you will be able to [specific capability].
─────────────────────────────
Ready to start, or do you want to adjust?
```

Wait for user confirmation before proceeding. Accept: "go", "yes", "start", "ready", or Enter as confirmation.

## Step 5: Teach the Concept

Follow the 8-step teaching format defined in CLAUDE.md exactly:
1. INTUITION
2. ANALOGY (must be from cloud/infra/systems engineering)
3. HOW IT WORKS
4. THE MATH (skip if no meaningful math)
5. CODE (runnable, <30 lines, shows output)
6. PRODUCTION CONTEXT (name a concrete failure mode)
7. COMMON MISTAKES (engineer-level mistakes)
8. CHECK YOUR UNDERSTANDING (application questions, wait for answers)

## Step 6: Append README Note

After completing the 8-step teaching sequence, immediately append a structured note to the relevant domain README.

File path: `/home/psharma/projects/ai-systems-engineering/[domain-folder]/README.md`
Example: for domain 01-python, append to `01-python/README.md`

Use the format defined in CLAUDE.md (## Session Notes section, append-only, never overwrite above it).

## Step 7: Practical Exercise

Present an exercise for the topic just taught:

- Classify: Jupyter notebook (EDA/visualization) or Python script (implementation)?
  - Default: Python script
  - Use Jupyter only if the topic requires visualization or data exploration
- GPU check: would this require >1 GPU-hour? If yes, offer CPU alternative first
- Exercise structure:
  - Title + topic tag
  - Context: "In a production AI system, this would come up when..."
  - Task description + constraints + success criteria
  - Starter code scaffold (remove friction, don't solve it)
  - Stretch goal: production angle extension
  - 3 checkable assertions: "You got it right if..."
- Suggest file path: `[domain-folder]/[notebooks or src]/[topic-name]-exercise.[ipynb or py]`
- Do NOT solve the exercise. Guide, hint, debug — but let the learner work through it.

## Step 8: Production Context Deep-Dive

After the exercise attempt (or if learner skips exercise):
- Connect the concept to real production AI system design using architecture-bridge analogies
- Discuss: where does this appear in real systems? What breaks? What are the architectural trade-offs?
- This is a discussion, not more teaching — engage with the learner's questions and observations

## Step 9: Session Close + Log Summary

Print a complete, ready-to-use log entry:

```
Session complete.
─────────────────────────────
Log entry ready (run /log to save):

## [YYYY-MM-DD]

- Studied: [domain number] / [sub-topic]
- Completed: [exercise filename, or "none"]
- Insight: [synthesize the most important insight from this session based on the conversation]
- Next: [recommended next sub-topic from curriculum sequence]

---
─────────────────────────────
Run /log to save this entry, or:
/log "[topic] | [your insight] | [next topic]" to log in one line.
```

The Stop hook will remind you to log if you forget.
