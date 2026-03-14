---
name: exercise
description: Generate a practical coding exercise for any AI/ML topic. Classifies as Jupyter notebook or Python script, flags GPU requirements, and provides a production-framed exercise with starter code and success criteria.
argument-hint: "[topic, e.g. 'gradient descent' or 'attention mechanism']"
disable-model-invocation: true
allowed-tools: Read
---

# /exercise — Practical Exercise Generator

Generates a focused coding exercise with a production angle. Does not solve — guides and hints only.

## Step 1: Determine Topic

If `$ARGUMENTS` is non-empty: use the specified topic.
If `$ARGUMENTS` is empty: read `LEARNING_LOG.md`, extract the most recent "Studied:" field, use that topic.

## Step 2: Classify Format

Decide: Jupyter notebook or Python script?

- **Python script (.py)** — DEFAULT for:
  - Algorithm implementation (gradient descent, backprop, attention)
  - Data structure or utility building
  - API or service integration
  - Anything that should run as a module

- **Jupyter notebook (.ipynb)** — ONLY for:
  - Exploratory data analysis
  - Plotting training curves or loss landscapes
  - Visual comparison of model outputs
  - Step-by-step interactive exploration where output inspection matters

## Step 3: GPU Check

Would this exercise require >1 GPU-hour at standard cloud rates (e.g., ~$1-3/hr on RunPod or Lambda)?

If yes:
1. Offer a CPU-runnable alternative first
2. Explain the trade-off: "The CPU version teaches the same concept; GPU is only needed to see the speed difference at scale"
3. For GPU exercises, mention cheapest options: RunPod (~$0.2-0.5/hr for A4000), Lambda Labs, or Google Colab free tier

## Step 4: Generate Exercise

Output the exercise in this structure:

---
**Exercise: [Title]**
**Topic:** [sub-topic slug]
**Format:** [Python script / Jupyter notebook]
**Estimated time:** [X minutes]
**File path:** `[domain-folder]/[notebooks or src]/[topic]-exercise.[py or ipynb]`

---

**Context**
In a production AI system, this comes up when: [1-2 sentences connecting to real systems]

**Task**
[Clear description of what to build. Include:]
- What the code must do
- Any constraints (e.g., "do not use sklearn's built-in X", "use only NumPy", "must handle batch inputs")
- What "done" looks like

**Starter Code**
```python
# [Enough scaffolding to avoid setup friction]
# [Imports, data setup, function signatures with TODOs]
# [Do NOT implement the core logic — leave that for the learner]
```

**Stretch Goal (Production Angle)**
[An extension that adds a real-world dimension — error handling, batching, logging, benchmarking, or deployment consideration]

**You got it right if:**
1. [Checkable assertion — specific output, behavior, or test]
2. [Checkable assertion]
3. [Checkable assertion]

---

## Step 5: After Presenting

Wait for the learner to attempt the exercise. Do not solve it.

When helping:
- Give hints, not solutions
- Ask "what do you think is happening here?" before explaining
- Point to the relevant concept from the teaching session
- If stuck for >10 minutes on the same point, give a more direct hint

When the exercise is complete:
- Suggest committing the file to the repo
- Offer to run `/log` to record the completion
