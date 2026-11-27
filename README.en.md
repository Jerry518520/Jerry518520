# Jerry Li (李冰杰)

<p align="right"><b>English</b> | <a href="README.md">中文</a></p>

<p align="center"><img alt="Location" src="https://img.shields.io/badge/%F0%9F%93%8D-Shanghai%2C%20China-4B6BFB"> <img alt="School" src="https://img.shields.io/badge/Shanghai%20Dianji%20University-Software%20Engineering%20(Honors)%202027-1D9E75"> <img alt="Focus" src="https://img.shields.io/badge/Focus-LLM%20%26%20Agent%20Engineering-orange"> <img alt="Looking for" src="https://img.shields.io/badge/Looking%20for-AI%20Internship-E24B4A"> <img alt="Email" src="https://img.shields.io/badge/Email-jerrylbj%40foxmail.com-lightgrey"></p>

Software Engineering undergraduate focused on **LLM & Agent engineering** — covering document parsing, hybrid RAG retrieval, deterministic tool orchestration, evaluation harnesses, FastAPI backends, and containerized delivery.

Rather than stopping at "the prompt works," I focus on catching **silent LLM failures** — cases where nothing crashes yet outputs drift from source evidence or mix up definitions — and locking them down with deterministic guardrails, refusal boundaries, and automated regression tests.

## Tech Stack

| Area | Technologies |
|---|---|
| LLM & Orchestration | LangGraph · LangChain · Dify Workflows · ReAct · Function Calling · Prompt Engineering |
| Parsing & RAG | MinerU · PyMuPDF · Embedding (BGE-M3) · BM25 · pgvector · FAISS · Reranker · Eval |
| Backend & Storage | Python · FastAPI (REST / WebSocket) · PostgreSQL · Redis · SQLite WAL |
| Engineering & Ops | Docker Compose · Nginx · pytest · Git · Linux · Trace Observability |
| Frontend | React 19 + TypeScript · Vite · Tailwind CSS · ECharts |

## Featured Open-Source Project · Microsatellite Telemetry Anomaly Detection & RAG Explainer

Built on the public **ESA OPS-SAT-AD** real on-orbit telemetry dataset (303,493 points / 2,123 segments / 9 channels). Combines deterministic per-channel anomaly detection, local hybrid RAG over aerospace handbooks, and on-demand DeepSeek API explanations with page-level source traceability. Project lead of a 3-person undergraduate innovation project (in exchange with the Innovation Academy for Microsatellites, CAS).

<p align="center"><img alt="Real-time alert center" src="https://raw.githubusercontent.com/Jerry518520/microsat-anomaly-analysis/main/docs/assets/dashboard.png" width="31%"> <img alt="Algorithm benchmark" src="https://raw.githubusercontent.com/Jerry518520/microsat-anomaly-analysis/main/docs/assets/detection.png" width="31%"> <img alt="In-depth diagnosis" src="https://raw.githubusercontent.com/Jerry518520/microsat-anomaly-analysis/main/docs/assets/rag_explain.png" width="31%"></p>

| Dimension | Measured Result |
|---|---|
| Strict Segment-level CV F1 | **0.35 → 0.57** (without Point-Adjustment inflation; frozen benchmark **0.6204**) |
| Local Hybrid Retrieval (BM25 + FAISS) | 24-query ablation dropped rank-hurting RRF & ~0.5s Cross-Encoder reranking (MRR dropped to 0.807); **MRR → 0.885**, ~**20ms** per query |
| 300k-Point Stream Replay | FastAPI + WebSocket ~114s full replay; synthetic anomaly alert push **P95 494ms**; **SQLite transactional lease lock (WAL)** prevents duplicate LLM calls |
| Hallucination & Fact Audit | Audited source papers & quarantined **200 legacy cached records**; **10/10** insufficient-evidence refusal across 30-query eval (LLM-as-a-Judge factuality **1.90/2.0**) |
| Verification & Delivery | **445 pytest** backend tests + **35** browser E2E checks + **SHA-256** delivery integrity manifest |

**Repository**: https://github.com/Jerry518520/microsat-anomaly-analysis

*(Note: Enterprise internal tools built during internships are kept private for confidentiality and compliance.)*

## How I Approach LLM Engineering

- **Deterministic logic first**: calculations, accounting reconciliations, and precondition checks belong in code, not probabilistic generation.
- **Guard against silent failures**: unapplied system prompts, mixed reporting scopes, and wrong page citations rarely raise exceptions — they require assertions, eval sets, and regression suites.
- **Refusal beats fabrication**: in high-reliability workflows, accurately declining unanswerable queries with verifiable source citations is far more valuable than fluent guessing.

## Contact

- **Email**: jerrylbj@foxmail.com
- **Open to**: AI Agent / FDE Intern, AI Product Manager Intern, AI Solutions Engineer Intern
