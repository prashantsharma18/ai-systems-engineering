---
name: teach-concept
description: Teaching format engine for AI/ML concepts. Auto-loads when explaining technical concepts to an experienced engineer learning a new domain. Defines the canonical 8-step teaching sequence with detailed section guidance.
disable-model-invocation: false
---

# Teach Concept — Internal Teaching Engine

This skill defines the canonical 8-step teaching format used by /study and /explain.

## The 8-Step Teaching Sequence

### Step 1: INTUITION
- Length: 2-3 sentences, zero jargon, no formulas
- Goal: plain English core idea — what is this, fundamentally?

### Step 2: ANALOGY
- Length: 4-6 sentences
- Source: MUST come from cloud/infra/systems engineering (K8s, API gateway, CI/CD, Redis, circuit breaker, blue-green deployment, container images, load balancer)
- Goal: transfer mental model from known infra domain to new ML domain

### Step 3: HOW IT WORKS
- Length: 1-2 paragraphs, mechanism-focused
- Include: inputs, transformation, output — no math notation here

### Step 4: THE MATH
- One equation + 2-3 sentences of plain English interpretation
- Explain what each variable means and what happens at extreme values
- SKIP ENTIRELY if the concept has no meaningful mathematical form

### Step 5: CODE
- Under 30 lines of Python
- Must run without modification — no placeholder variables
- Must include print() showing meaningful output
- Use tech stack: PyTorch, scikit-learn, HuggingFace, NumPy as appropriate
- Comments explain the what and why, not just restate the code

### Step 6: PRODUCTION CONTEXT
- 1 paragraph
- Must reference at least one of: model serving, training pipeline, data ingestion, inference latency, monitoring
- Must name a concrete failure mode: "In production, this breaks when..."
- Connect to SA background: "As a systems architect, you've seen this in [infra context]..."

### Step 7: COMMON MISTAKES
- 2-3 bullet points
- Engineer-level mistakes only: scaling, architecture decisions, configuration, misuse of abstractions
- Format: mistake + why wrong + what to do instead

### Step 8: CHECK YOUR UNDERSTANDING
- 2-3 numbered questions requiring application, not recall
- Good pattern: "If you changed X to Y, what would happen and why?"
- Bad pattern: "What is the definition of X?"
- Present questions, then wait — do not answer immediately

## README Note Format

After completing the 8-step sequence, append to the relevant domain README under "## Session Notes":

```
---

### [Concept Name]
> Added: YYYY-MM-DD

**Intuition:** [1-2 sentences]

**Production use:** [key sentence from Step 6]

**Key code pattern:**
[condensed code, 10 lines max]

**Common mistake:** [most important mistake from Step 7]

**Practice:** [exercise filename or "none"]
```

Create "## Session Notes" section if it does not exist. Never modify content above it.
