---
name: explain
description: Explain any AI/ML concept using the 8-step teaching format from CLAUDE.md. Also auto-triggers when a user asks 'what is X' or 'explain X' in conversation. Tailored for an SA audience with production context and infra analogies.
argument-hint: "[concept to explain, e.g. 'attention mechanism' or 'batch normalization']"
disable-model-invocation: false
---

# /explain — On-Demand Concept Explanation

Teaches any AI/ML concept using the full 8-step format. Useful mid-session when a new term appears, or for standalone deep dives.

## Step 1: Parse Concept

Use `$ARGUMENTS` as the concept to explain.

If no arguments provided, ask: "What concept would you like me to explain?"

## Step 2: Apply 8-Step Teaching Format

Follow the complete 8-step sequence defined in CLAUDE.md:

1. **INTUITION** (2-3 sentences, zero jargon)
2. **ANALOGY** (cloud/infra/systems engineering analog, 4-6 sentences)
3. **HOW IT WORKS** (mechanism, 1-2 paragraphs)
4. **THE MATH** (one equation in plain English — skip if no meaningful math)
5. **CODE** (runnable example, <30 lines, shows output, uses tech stack)
6. **PRODUCTION CONTEXT** (where this appears in real AI systems, concrete failure mode)
7. **COMMON MISTAKES** (2-3 engineer-level mistakes)
8. **CHECK YOUR UNDERSTANDING** (2-3 application questions — wait for answers)

Refer to `teach-concept/SKILL.md` for detailed guidance on each step.

## Step 3: Offer Next Step

After the explanation:

"Want to practice this with an exercise? Or shall we continue with the current session topic?"

If in the middle of a /study session, remind the learner which topic the session was covering so they can choose to return to it.

## Note on Auto-Triggering

This skill auto-loads (disable-model-invocation: false) when users ask concept questions in conversation. When auto-triggered mid-session, keep the explanation focused — use the 8-step format but be concise. Offer to go deeper after the main session continues.
