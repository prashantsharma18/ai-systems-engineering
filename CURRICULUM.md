# AI Systems Engineering — Curriculum

A structured learning roadmap for an AI Systems Engineer / AI Platform Architect track. Optimized for a Senior Solution Architect background: deep on infra/cloud, new to ML theory.

**How to read this file:**
- Sub-topics are listed in the recommended study order
- Status markers: `[ ]` not started · `[~]` in progress · `[x]` complete
- Update status markers as you progress — this file is your map; `LEARNING_LOG.md` is your position
- You can add sub-topics, adjust order, or add notes at any time

---

## Phase 1 — Foundations (Weeks 1–7)

Two parallel tracks. Alternate days: Python on Mon/Wed/Fri, Math on Tue/Thu.

### Track A · 01-python · 3 weeks

**Profile skip:** Basic syntax, basic OOP — assumed known. Start at data structures.

| # | Sub-topic | Status | Notes |
|---|-----------|--------|-------|
| 1 | data-structures-performance-tradeoffs | [ ] | lists vs deques vs dicts — time complexity matters for data pipelines |
| 2 | iterators-generators-comprehensions | [ ] | pull-based processing, memory efficiency for large datasets |
| 3 | concurrency-async-for-data-loading | [ ] | asyncio, threading, multiprocessing — when to use which in ML |
| 4 | type-hints-and-protocols | [ ] | production Python: contracts and duck typing |
| 5 | testing-with-pytest | [ ] | unit + integration tests for ML code |
| 6 | packaging-and-virtual-environments | [ ] | uv, pyproject.toml, reproducible environments |
| 7 | numpy-and-vectorized-computation | [ ] | foundation for tensor operations |
| 8 | memory-layout-and-broadcasting | [ ] | critical for performance reasoning |
| 9 | data-analysis-with-pandas | [ ] | ML preprocessing and pipelines |

---

### Track B · 02-math-for-ml · 4 weeks

**Profile skip:** Formal proofs, measure theory, Fourier analysis, multivariate calculus beyond chain rule.

| # | Sub-topic | Status | Notes |
|---|-----------|--------|-------|
| 1 | vectors-and-matrix-operations | [ ] | dot products, matrix multiply — the language of ML |
| 2 | matrix-transformations-and-eigenvalues | [ ] | what a transformation does to space; PCA intuition |
| 3 | gradients-and-chain-rule | [ ] | the engine of learning — how error flows backwards |
| 4 | probability-distributions | [ ] | Gaussian, Bernoulli, categorical — what they model |
| 5 | bayes-theorem-and-conditional-probability | [ ] | the update rule for beliefs |
| 6 | maximum-likelihood-estimation | [ ] | how model training is actually a probability problem |

---

## Phase 2 — ML Core (Weeks 8–18)

Sequential. Complete 03 before 04.

### 03-ml-fundamentals · 4 weeks

**Prerequisites:** Phase 1 complete
**Profile skip:** Unsupervised learning depth, dimensionality reduction depth, SVM internals

| # | Sub-topic | Status | Notes |
|---|-----------|--------|-------|
| 1 | supervised-learning-framework | [ ] | inputs → model → loss → update: the universal ML loop |
| 2 | train-validation-test-splits | [ ] | experimental discipline; preventing data leakage |
| 3 | dataset-leakage-and-bias | [ ] | one of the most common real-world ML failures |
| 4 | feature-engineering-for-ml | [ ] | encoding, scaling, handling nulls — last mile before training |
| 5 | loss-functions-and-objectives (session 1) | [ ] | cross-entropy, MSE — "a loss function is your SLA definition" |
| 6 | loss-functions-and-objectives (session 2) | [ ] | custom losses, loss landscapes, why choice of loss matters |
| 7 | gradient-descent-and-optimization | [ ] | SGD, Adam, learning rate schedules |
| 8 | regularization-and-overfitting | [ ] | L1/L2, dropout, early stopping — the bias-variance trade-off |
| 9 | model-evaluation-and-metrics | [ ] | accuracy, precision, recall, AUC, calibration — picking the right metric |
|10 | cross-validation | [ ] | robust evaluation for small datasets |

> **Note:** `loss-functions` is the most important concept in this domain and deserves 2 full sessions. It is the bridge between "optimizing a formula" and "defining what the system should do."

---

### 04-deep-learning · 5 weeks

**Prerequisites:** Domain 03 complete
**Profile skip:** CNN depth, RNN depth, custom CUDA kernels
**Deep-dive:** Transformer architecture and attention (essential for LLM work), training dynamics

| # | Sub-topic | Status | Notes |
|---|-----------|--------|-------|
| 1 | neural-networks-as-function-approximators | [ ] | what a neural net is actually doing |
| 2 | backpropagation-intuition | [ ] | chain rule applied — not the math, the mechanics |
| 3 | activation-functions-and-normalization | [ ] | ReLU, LayerNorm, BatchNorm — what they fix |
| 4 | training-dynamics-and-debugging-loss-curves | [ ] | reading loss curves, diagnosing instability — production skill |
| 5 | attention-mechanism-deep-dive | [ ] | the key primitive behind all modern LLMs |
| 6 | transformer-architecture-full | [ ] | encoder, decoder, self-attention, positional encoding |
| 7 | mixed-precision-and-training-at-scale | [ ] | fp16, bf16, gradient checkpointing, distributed basics |
| 8 | brief-CNNs-overview | [ ] | overview only — convolutions, pooling, not depth |
| 9 | brief-RNNs-overview | [ ] | overview only — LSTMs, GRUs, why transformers replaced them |

---

## Phase 3 — LLMs + Production AI (Weeks 19–28)

Two parallel tracks. 3 days/week on LLMs, 2 days/week on MLOps.

### Track C · 05-llms-and-genai · 5 weeks

**Prerequisites:** Domain 04 complete
**Profile skip:** None — all sub-topics are core for this profile
**Note:** This domain aligns most directly with the AI Systems Engineer target role

| # | Sub-topic | Status | Notes |
|---|-----------|--------|-------|
| 1 | tokenization-and-vocabulary | [ ] | BPE, SentencePiece — what the model actually sees |
| 2 | embeddings-and-vector-representations | [ ] | how meaning is represented numerically |
| 3 | attention-as-information-routing | [ ] | revisit attention from a systems perspective |
| 4 | LLM-architecture-GPT-and-beyond | [ ] | GPT, Llama, Mistral — architecture families |
| 5 | prompt-engineering-systematic | [ ] | zero-shot, few-shot, chain-of-thought — systematic approach |
| 6 | embeddings-for-semantic-search | [ ] | cosine similarity, semantic retrieval |
| 7 | vector-databases-and-indexing | [ ] | FAISS, HNSW, Pinecone — ANN search |
| 8 | RAG-architecture-and-patterns | [ ] | retrieval-augmented generation — design patterns |
| 9 | fine-tuning-LoRA-and-PEFT | [ ] | when to fine-tune vs prompt, LoRA mechanics |
| 10 | LLM-application-patterns | [ ] | chains, routers, structured output, tool calling |
| 11 | agentic-systems-and-tool-use | [ ] | agents, planning, multi-step reasoning, tool integration |

---

### Track D · 06-mlops-and-ai-systems · 6 weeks

**Prerequisites:** Domain 03 complete, Domain 04 partially complete
**Profile skip:** Spark internals, deep data engineering theory
**Deep-dive:** Inference latency optimization, serving architecture, monitoring — SA instincts directly applicable

| # | Sub-topic | Status | Notes |
|---|-----------|--------|-------|
| 1 | model-serving-patterns-fastapi-triton | [ ] | REST serving, batching, async inference |
| 2 | inference-optimization-quantization-batching | [ ] | quantization, KV cache, continuous batching |
| 3 | monitoring-drift-and-failure-modes | [ ] | what to monitor, what breaks silently |
| 4 | training-pipelines-orchestration | [ ] | MLflow, pipeline design, artifact management |
| 5 | data-engineering-for-ml-basics | [ ] | feature stores, data versioning — concepts only |
| 6 | cloud-ml-infrastructure | [ ] | GPU instances, spot training, managed serving (SageMaker, Azure ML) |
| 7 | ai-security-basics | [ ] | prompt injection, model extraction, supply chain risks |

---

## Phase 4 — Architecture and Systems (Weeks 29–35)

Sequential. Complete Phase 3 before starting.

### 07-mcp · 2 weeks

**Prerequisites:** Domain 05 complete

| # | Sub-topic | Status | Notes |
|---|-----------|--------|-------|
| 1 | protocol-specification-and-design | [ ] | MCP spec — tools, resources, prompts |
| 2 | server-implementation-from-scratch | [ ] | build a working MCP server |
| 3 | tool-design-patterns | [ ] | good tool interfaces, error handling, schema design |
| 4 | multi-server-orchestration | [ ] | composing multiple MCP servers |

---

### 09-ai-system-architecture · 4 weeks

**Prerequisites:** Domains 04 + 05 + 06 complete

| # | Sub-topic | Status | Notes |
|---|-----------|--------|-------|
| 1 | AI-system-design-patterns | [ ] | patterns for production AI systems |
| 2 | multi-model-pipeline-design | [ ] | routing, ensembling, cascades |
| 3 | cost-optimization-architecture | [ ] | caching, model sizing, batching strategy |
| 4 | reliability-and-safety-patterns | [ ] | fallbacks, guardrails, circuit breakers for AI |
| 5 | AI-platform-architecture-capstone | [ ] | end-to-end platform design — synthesis project |

---

## Time Budget Summary

| Domain | Phase | Duration | Days/Week | Style |
|--------|-------|----------|-----------|-------|
| 01-python | 1 | 3 weeks | 3 | Parallel with 02 |
| 02-math-for-ml | 1 | 4 weeks | 2 | Parallel with 01 |
| 03-ml-fundamentals | 2 | 4 weeks | 5 | Sequential |
| 04-deep-learning | 2 | 5 weeks | 5 | Sequential |
| 05-llms-and-genai | 3 | 5 weeks | 3 | Parallel with 06 |
| 06-mlops-and-ai-systems | 3 | 6 weeks | 2 | Parallel with 05 |
| 07-mcp | 4 | 2 weeks | 5 | Sequential |
| 09-ai-system-architecture | 4 | 4 weeks | 5 | Sequential |

**Total estimated duration:** ~33 weeks at 2–3 hours/day, 5 days/week

---

## Notes on Domain 08 (Claude Code)

Domain 08 is the infrastructure running this learning companion system itself. It is not included in the curriculum sequence above. You can explore Claude Code features organically as you use this system, or add it as a dedicated study period after Phase 4.
