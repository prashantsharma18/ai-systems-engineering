---
name: architecture-bridge
description: ML-to-infrastructure analogy reference. Auto-loads silently when discussing model deployment, serving, latency, scaling, cost, or system design. Maps ML concepts to cloud infrastructure and distributed systems analogies for an SA audience.
disable-model-invocation: false
---

# Architecture Bridge — ML to Infra Analogy Reference

This skill provides system architecture context for AI/ML concepts. It loads automatically when discussions touch deployment, serving, latency, scaling, cost, or system design.

## Core Principle

Every ML concept has a structural analog in distributed systems or cloud infrastructure. When teaching or explaining, always surface this analog — it makes unfamiliar ML ideas immediately intuitive for an SA.

## Analogy Reference Table

| ML Concept | Infra Analog | Production Implication |
|---|---|---|
| Model serving | Stateless microservice | Latency SLAs, horizontal scaling, health checks |
| Batch inference | Cron job / batch ETL pipeline | Throughput vs latency trade-off, backpressure |
| Model weights | Immutable container image | Versioning, rollback, artifact registry |
| Training pipeline | CI/CD pipeline | Reproducibility, artifact provenance, test gates |
| Feature store | Redis / DynamoDB cache | Freshness vs latency trade-off, TTL management |
| Embedding vector index | Inverted search index | ANN vs exact search, recall vs speed trade-off |
| Fine-tuning | Baking config into a base image | When to bake-in vs parameterize at runtime |
| RAG | Cache-aside pattern | Cache hit rate = retrieval quality; cold start problem |
| Model monitoring | APM / distributed tracing | What is the p99 of model accuracy? Drift = degradation |
| Distributed training | Horizontal Pod Autoscaling | Communication overhead = network I/O bottleneck |
| Quantization | Gzip / minification | Accuracy-size Pareto curve; lossy vs lossless |
| A/B testing models | Blue-green deployment | Traffic splitting, rollback criteria, canary analysis |
| Prompt caching | HTTP response caching | Cache key = prompt prefix; TTL trade-offs |
| Token limits | Request payload size limits | Chunking strategy, context window = working memory |
| KV cache | Connection pool | Pre-allocated resources, eviction policy |
| LoRA adapters | Config overlays / patches | Small delta on top of base; composable |
| Inference batching | Request aggregation / debouncing | Throughput vs latency; batch size tuning |
| Model fallback | Circuit breaker pattern | Fallback to smaller/cheaper model on failure |
| Guardrails / filters | API gateway policy enforcement | Input validation, rate limiting, content policy |
| Embedding similarity | Cosine similarity = dot product | Distance metric choice affects recall |

## When to Use This Skill

Surface architecture bridge analogies:
- When introducing any serving, deployment, or infrastructure concept
- When discussing trade-offs (latency vs throughput, cost vs accuracy, freshness vs speed)
- When the learner asks "why does this work this way?" about an ML system design
- During the PRODUCTION CONTEXT step of the 8-step teaching format
- During architecture discussion portions of /study sessions

## Framing Pattern

"As a systems architect, you've seen [infra concept] in [infra context]. In ML systems, [ML concept] is structurally the same because [shared property]. The key difference is [what changes in the ML context]."

## SA Advantage Areas

These are ML domains where SA background gives the learner a head start:

- **Model serving and inference:** Already understands stateless services, SLAs, horizontal scaling
- **MLOps pipelines:** Already understands CI/CD, artifact management, environment reproducibility
- **Monitoring and observability:** Already understands metrics, traces, alerting — just new signals
- **Cost optimization:** Already understands resource right-sizing, spot vs on-demand, reservation models
- **Security:** Already understands network policies, secrets management, supply chain risks

Lean into these strengths. Connect new ML concepts to existing SA mental models aggressively.
