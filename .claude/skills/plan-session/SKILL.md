---
name: plan-session
description: Curriculum engine and session planner for AI systems engineering learning. Given LEARNING_LOG.md and CURRICULUM.md content, returns the recommended next sub-topic, prerequisite status, and session time structure.
disable-model-invocation: false
---

# Plan Session — Curriculum Engine

This skill is invoked as a subagent by the /study command. Given the contents of LEARNING_LOG.md and CURRICULUM.md, it returns a structured session plan.

## Input

You will receive:
- Full content of LEARNING_LOG.md
- Full content of CURRICULUM.md
- Optionally: a user-specified topic override

## Output

Return a structured plan with:
1. Recommended domain + sub-topic (with rationale)
2. Prerequisite status (any gaps?)
3. Session duration recommendation (2h or 3h) and time breakdown
4. Goal statement ("After this session the learner will be able to...")

## Next-Topic Decision Algorithm

1. Read the last 5 entries in LEARNING_LOG.md
2. Extract the most recent "Studied:" field to identify current domain and sub-topic
3. Extract the "Next:" field from the most recent entry — this is a strong signal; default to it
4. Cross-reference with CURRICULUM.md to find the next sub-topic in sequence
5. Check prerequisites: are prerequisite domains >= 70% complete (by non-skipped sub-topic count)?
   - Count "x" status markers in CURRICULUM.md for each prerequisite domain
   - If < 70%, recommend the prerequisite sub-topic first and explain why
6. If the "Next:" log field and CURRICULUM.md sequence agree, use that topic
7. If the "Next:" log field conflicts with prerequisites, follow the prerequisites and explain the gap
8. If the learner is on the final sub-topic of a domain, recommend a capstone/integration exercise before moving on

## Session Time Structure

### 2-hour session
- 30 min: Concept teaching (8-step format)
- 45 min: Practical exercise
- 30 min: Production context deep-dive and architecture discussion
- 15 min: Reflection, log prep, next-topic preview

### 3-hour session
- 40 min: Concept teaching (8-step format)
- 60 min: Practical exercise (slightly harder, stretch goal included)
- 40 min: Production context deep-dive and architecture discussion
- 20 min: Preview of next topic
- 20 min: Reflection, log prep

### How to choose 2h vs 3h
Default to 2h unless the learner specifies they have 3 hours. Complex topics (transformers, attention, RAG architecture, inference optimization) warrant suggesting 3h.

## Phase-Aware Mixing Rules

Phase 1 (domains 01 + 02 in parallel):
- Alternate between tracks: Python sessions Mon/Wed/Fri, Math sessions Tue/Thu
- Never study both tracks on the same day
- If the learner has already studied Python today, recommend Math next

Phase 3 (domains 05 + 06 in parallel):
- 3 days/week on domain 05 (LLMs), 2 days/week on domain 06 (MLOps)
- Track separately in LEARNING_LOG.md entries

## Prerequisite Map

| Domain | Prerequisites |
|--------|--------------|
| 01-python | none |
| 02-math-for-ml | none |
| 03-ml-fundamentals | 01-python complete, 02-math-for-ml >= 70% |
| 04-deep-learning | 03-ml-fundamentals complete |
| 05-llms-and-genai | 04-deep-learning complete |
| 06-mlops-and-ai-systems | 03-ml-fundamentals complete, 04-deep-learning >= 50% |
| 07-mcp | 05-llms-and-genai complete |
| 09-ai-system-architecture | 04-deep-learning complete, 05-llms-and-genai complete, 06-mlops-and-ai-systems complete |

## Output Format

Return your recommendation in this format:

```
RECOMMENDED TOPIC:
  Domain: [number + name]
  Sub-topic: [sub-topic slug]
  Rationale: [1-2 sentences]

PREREQUISITES: [OK / GAPS FOUND]
  [if gaps: list specific missing sub-topics]

SESSION STRUCTURE: [2h / 3h]
  - [time]: [activity]
  - [time]: [activity]
  ...

GOAL: After this session the learner will be able to [specific capability].
```
