# Tools and Libraries

Key tools and libraries in the AI/ML ecosystem with usage notes.

---

## Core Python

- **NumPy** — Foundational array library. Understanding broadcasting and vectorization is essential.
- **Pandas** — Tabular data manipulation. The standard for data preprocessing in ML pipelines.
- **Matplotlib / Seaborn** — Visualization. Seaborn for statistical plots, Matplotlib for full control.

---

## Machine Learning

- **scikit-learn** — Classical ML algorithms, preprocessing, pipelines, and model evaluation. The reference implementation for most classical algorithms.
- **XGBoost / LightGBM** — Gradient boosted trees. Dominant for tabular data in production.

---

## Deep Learning

- **PyTorch** — Primary deep learning framework. Dynamic computation graph, research-friendly, increasingly production-ready.
- **HuggingFace Transformers** — Pre-trained model hub and training utilities. The standard for working with transformer models.
- **HuggingFace Datasets** — Efficient dataset loading and processing for NLP and vision tasks.

---

## LLMs and GenAI

- **Anthropic SDK** — Python/TypeScript SDK for the Claude API. Primary tool for this repo's LLM work.
- **LangChain** — LLM application framework. Useful for chains, agents, and RAG pipelines.
- **LlamaIndex** — Data framework for LLM applications. Strong for document indexing and RAG.
- **FAISS** — Facebook AI Similarity Search. Efficient vector similarity search for RAG.
- **ChromaDB** — Lightweight local vector database. Good for prototyping RAG pipelines.

---

## MLOps

- **FastAPI** — High-performance Python web framework. Standard for ML model serving APIs.
- **MLflow** — Experiment tracking, model registry, and deployment. Open source, widely adopted.
- **Docker** — Containerization for reproducible ML environments and serving.
- **Evidently** — ML monitoring and data drift detection. Open source, easy to integrate.
- **Prefect / Airflow** — Workflow orchestration for ML pipelines.

---

## Agentic AI

- **Claude Code** — Anthropic CLI for agentic coding workflows. Also exposes the Agent SDK.
- **MCP SDK** — Official SDK for building Model Context Protocol servers and clients.

---

## Development

- **uv** — Fast Python package manager. Recommended for new projects.
- **pytest** — Testing framework. Pair with `pytest-cov` for coverage.
- **ruff** — Fast Python linter and formatter. Replaces flake8, black, and isort.
- **Jupyter** — Interactive notebooks for exploration and teaching.
