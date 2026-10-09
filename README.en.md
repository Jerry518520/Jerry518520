# Bingjie Li

<p align="right"><b>English</b> | <a href="README.md">中文</a></p>

<p align="center"><img alt="Location" src="https://img.shields.io/badge/%F0%9F%93%8D-Shanghai%2C%20China-4B6BFB"> <img alt="School" src="https://img.shields.io/badge/Shanghai%20Dianji%20University-Software%20Engineering%20(Honors)%2C%20Class%20of%202027-1D9E75"> <img alt="Focus" src="https://img.shields.io/badge/Focus-LLM%20Application%20Engineering-orange"> <img alt="Looking for" src="https://img.shields.io/badge/Open%20to-Class%20of%202027%20Internships-E24B4A"> <img alt="Email" src="https://img.shields.io/badge/Email-jerrylbj%40foxmail.com-lightgrey"></p>

I build LLM applications, focusing on shipping RAG and Agent systems end to end. I have worked across the full chain: document parsing → chunking → embedding → retrieval → prompting → generation → citation traceability → API → frontend.

Rather than just getting a model to run, I am better at locating LLM failure modes that are **not obvious** — the ones that raise no error while the output has already drifted away from its evidence — and designing fallbacks and regression tests so they cannot come back.

## Tech Stack

| Area | Technologies |
|---|---|
| LLM applications | LangGraph · LangChain · ReAct · Function Calling · Prompt engineering |
| Retrieval / RAG | BGE-M3 · FAISS · BM25 · hybrid retrieval · citation traceability |
| Backend | Python async · FastAPI · Uvicorn · REST · WebSocket |
| Frontend | React 19 + TypeScript · Vite · Tailwind CSS · ECharts |
| Engineering | Docker Compose · pytest · pre-commit · Poetry / pip |
| Algorithms | Isolation Forest · feature engineering · rule-engine gated fusion · evaluation metric design |

## Project 1 · Microsatellite Telemetry Anomaly Detection with RAG-based Explanation

Built on the public ESA OPS-SAT dataset (303,493 sampled points / 2,123 segments / 9 channels). Isolation Forest detects anomalous segments, then RAG over a satellite handbook knowledge base lets the LLM produce traceable explanations of each anomaly. Undergraduate Innovation and Entrepreneurship Training Program at Shanghai Dianji University; I was the project lead.

<p align="center"><img alt="Real-time alert center" src="https://raw.githubusercontent.com/Jerry518520/microsat-anomaly-analysis/main/docs/assets/dashboard.png" width="31%"> <img alt="Algorithm benchmark" src="https://raw.githubusercontent.com/Jerry518520/microsat-anomaly-analysis/main/docs/assets/detection.png" width="31%"> <img alt="In-depth diagnosis" src="https://raw.githubusercontent.com/Jerry518520/microsat-anomaly-analysis/main/docs/assets/rag_explain.png" width="31%"></p>

| Metric | Result |
|---|---|
| Segment-level F1 | 0.5882 → **0.6281** (+6.8%) |
| Alert false positives | **20 → 0** |
| RAG citation traceability | **200 / 200** |
| Median retrieval latency | **25 ms** |

- **Engineering trade-off**: to push median retrieval latency down to 25 ms I deliberately dropped online incremental writes in favour of offline index rebuilds. The cost is that knowledge-base updates require a rebuild; the benefit is a minimal retrieval path with predictable latency.
- **Fixing a non-obvious AI defect**: the anti-hallucination prompt was in place but never took effect — generated content drifted from the retrieved evidence while the system raised no error. I located the root cause with assertion checks, then added a "refuse to answer when nothing is retrieved" fallback and a regression test.
- **Metric governance**: segment-level and point-level anomaly rates have different denominators and must not be mixed; the two definitions are documented separately so they can never be compared across definitions.
- **Delivery**: FastAPI + React 19 with a separated frontend and backend, including live data ingestion (`/api/stream/ingest` + WebSocket alerts), API authentication and rate limiting, and SQLite alert persistence.

**Repository**: https://github.com/Jerry518520/microsat-anomaly-analysis

## Project 2 · Financial Report AI Assistant

Helping non-finance people read listed-company PDF financial reports: upload a report, then ask questions in natural language while a LangGraph Agent calls financial tools to compute metrics, generate a summary and build a capability radar chart, annotating source page numbers throughout.

<p align="center"><img alt="Kweichow Moutai 2025 annual report analysis result" src="https://raw.githubusercontent.com/Jerry518520/financial-analysis-AI-assistant/main/docs/assets/main.png" width="92%"></p>

| Metric | Result |
|---|---|
| Agent workflow | LangGraph closed loop: plan → tool call → reflect → retry, converging within at most **5 rounds** |
| Tool layer | **19** financial calculation tools |
| Document parsing | Hybrid LlamaParse parsing, solving **borderless tables** in Chinese financial-report PDFs |
| Deployment | One-command Docker Compose startup, GPU / CPU dependency separation + health checks |

**Repository**: https://github.com/Jerry518520/financial-analysis-AI-assistant

## How I Think About LLM Engineering

- **Failure modes**: most LLM problems raise no error. An anti-hallucination prompt being present does not mean it is in effect — when the output drifts away from its evidence, the system shows no reaction at all. These non-obvious failures have to be caught by assertion checks and regression tests, not by eyeballing the output.
- **Verifiability**: define your metrics clearly before talking about optimisation. Two metrics with different denominators cannot be compared directly, or your own numbers will send you optimising in the wrong direction.
- **Engineering discipline**: I would rather have the system refuse to answer than make something up. Returning "no evidence found" when retrieval comes up empty is a better engineering choice than producing a plausible-looking answer.

## Contact

- **Email**: jerrylbj@foxmail.com
- **Looking for**: internships in LLM application development / AI application development
