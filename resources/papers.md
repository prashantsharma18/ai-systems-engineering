# Papers

Research papers worth reading. Each entry includes a one-paragraph summary and why it matters.

---

## Foundational

- **Attention Is All You Need** (Vaswani et al., 2017). Introduced the transformer architecture. Everything in modern LLMs descends from this paper. Read alongside an annotated implementation.

- **BERT: Pre-training of Deep Bidirectional Transformers for Language Understanding** (Devlin et al., 2018). Established the pre-train / fine-tune paradigm for NLP. Understanding BERT is prerequisite to understanding GPT.

- **Language Models are Few-Shot Learners** (Brown et al., 2020 — GPT-3 paper). Demonstrated emergent few-shot capabilities at scale. The paper that shifted the field toward prompting over fine-tuning.

---

## RAG and Retrieval

- **Retrieval-Augmented Generation for Knowledge-Intensive NLP Tasks** (Lewis et al., 2020). The original RAG paper. Defines the retrieval + generation architecture that most RAG systems are built on.

---

## Fine-Tuning

- **LoRA: Low-Rank Adaptation of Large Language Models** (Hu et al., 2021). Introduced efficient fine-tuning via low-rank weight updates. The basis for most practical LLM fine-tuning workflows today.

---

## Agents and Tool Use

- **ReAct: Synergizing Reasoning and Acting in Language Models** (Yao et al., 2022). Introduced the Reason + Act (ReAct) prompting pattern. Foundation for most LLM agent frameworks.

---

## Evaluation

- **RAGAS: Automated Evaluation of Retrieval Augmented Generation** (Es et al., 2023). Defines metrics for evaluating RAG systems without human labels. Practical for production RAG evaluation.
