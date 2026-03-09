# 06 — MLOps and AI Systems

Taking models from notebooks to production: serving, monitoring, pipelines, and cloud infrastructure. This is where ML meets systems engineering.

## Sub-folders

| Folder | Notes | Notebooks / Code | Status |
|--------|-------|-----------------|--------|
| [model-deployment/](./model-deployment/) | Serving patterns, REST APIs, batching, model packaging | `fastapi-model-serving/` project | Planned |
| [inference-optimization/](./inference-optimization/) | Quantization, batching strategies, vLLM, TensorRT, ONNX export | `quantization.ipynb`, `vllm-serving.ipynb` | Planned |
| [data-engineering/](./data-engineering/) | Spark, Kafka, data lakes, feature stores, ML data ingestion pipelines | `spark-for-ml.ipynb`, `feature-pipeline.ipynb` | Planned |
| [ai-security/](./ai-security/) | Prompt injection, adversarial attacks, model privacy, data governance | `prompt-injection-demo.ipynb` | Planned |
| [monitoring/](./monitoring/) | Data drift, model performance monitoring, alerting | `data-drift-detection.ipynb`, `evidently-walkthrough.ipynb` | Planned |
| [pipelines/](./pipelines/) | Pipeline patterns, orchestration, DAGs | `airflow-ml-dag.py`, `prefect-training-flow.py` | Planned |
| [cloud/](./cloud/) | AWS SageMaker, Azure ML, GCP Vertex AI — notes and walkthroughs | Notes only | Planned |
| [infrastructure/](./infrastructure/) | Docker for ML, Kubernetes workloads | Notes only | Planned |

## Projects

| Project | Description | Status |
|---------|-------------|--------|
| [fastapi-model-serving](./model-deployment/fastapi-model-serving/) | Dockerized FastAPI service for ML model inference | Planned |

## Blog Posts

| Title | Status |
|-------|--------|
| ML System Design Patterns | Planned |
| LLMOps vs MLOps | Planned |

## Why This Matters

A model that cannot be reliably deployed, monitored, and maintained is a research prototype, not an engineering asset. This section covers what turns an ML model into a production system.
