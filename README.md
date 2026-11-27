# 李冰杰

<p align="right"><a href="README.en.md">English</a> | <b>中文</b></p>

<p align="center"><img alt="Location" src="https://img.shields.io/badge/%F0%9F%93%8D-Shanghai%2C%20China-4B6BFB"> <img alt="School" src="https://img.shields.io/badge/%E4%B8%8A%E6%B5%B7%E7%94%B5%E6%9C%BA%E5%AD%A6%E9%99%A2-%E8%BD%AF%E4%BB%B6%E5%B7%A5%E7%A8%8B%EF%BC%88%E5%8D%93%E8%B6%8A%E7%8F%AD%EF%BC%89%202027%E5%B1%8A-1D9E75"> <img alt="Focus" src="https://img.shields.io/badge/Focus-LLM%20%E5%BA%94%E7%94%A8%E4%B8%8E%20Agent%20%E5%B7%A5%E7%A8%8B-orange"> <img alt="Looking for" src="https://img.shields.io/badge/%E5%AF%BB%E6%B1%82-2027%20%E5%B1%8A%E5%AE%9E%E4%B9%A0-E24B4A"> <img alt="Email" src="https://img.shields.io/badge/Email-jerrylbj%40foxmail.com-lightgrey"></p>

专注 **LLM 应用与 Agent 工程落地**（RAG 混合检索、多步工具编排、Eval 评测与防幻觉治理），覆盖从文档解析、双路检索、确定性工具链路到 FastAPI 后端与容器化交付的完整闭环。

比起把模型调通，我更在意定位 LLM 的**非显性失效**——那些系统不报错、但输出已经脱离依据或口径错位的问题，并用确定性校验、拒答边界与自动化回归测试把它们彻底兜住。

## 技术栈

| 方向 | 技术 |
|---|---|
| LLM 与编排 | LangGraph · LangChain · Dify 工作流 · ReAct · Function Calling · Prompt 调优 |
| 检索与解析 | RAG · MinerU · PyMuPDF · Embedding（BGE-M3）· BM25 · pgvector · FAISS · Reranker · Eval |
| 后端与存储 | Python · FastAPI（REST / WebSocket）· PostgreSQL · Redis · SQLite WAL |
| 工程与部署 | Docker Compose · Nginx · pytest · Git · Linux · Trace 观测 |
| 前端与可视化 | React 19 + TypeScript · Vite · Tailwind CSS · ECharts |

## 开源代表项目 · 微小卫星遥测异常检测与 RAG 解释系统

面向缺标注、高可靠的航天遥测场景（基于公开 **ESA OPS-SAT-AD** 真实在轨数据集：30.3 万采样点 / 2,123 段 / 9 通道）。采用“确定性分通道检测 + 本地混合 RAG + 按需调用 DeepSeek API 解释”架构，兼顾低延迟与可溯源。上海电机学院 3 人大创项目（3 人市级大创项目），任核心负责人。

<p align="center"><img alt="实时告警中心" src="https://raw.githubusercontent.com/Jerry518520/microsat-anomaly-analysis/main/docs/assets/dashboard.png" width="31%"> <img alt="算法实验" src="https://raw.githubusercontent.com/Jerry518520/microsat-anomaly-analysis/main/docs/assets/detection.png" width="31%"> <img alt="深度诊断" src="https://raw.githubusercontent.com/Jerry518520/microsat-anomaly-analysis/main/docs/assets/rag_explain.png" width="31%"></p>

| 维度 | 实测结果 |
|---|---|
| 严格段级交叉验证 F1 | **0.35 → 0.57**（不做 Point-Adjustment 刷分；工程冻结包复核 **0.6204**） |
| 本地混合检索（BM25 + FAISS） | 24 题实验舍弃降排序的 RRF 与约 0.5s 重排（提召回但致 MRR 跌至 0.807），**MRR 提至 0.885**，单次检索约 **20ms** |
| 30 万点遥测流回放 | FastAPI + WebSocket 约 114s 全量跳空档回放，合成异常段告警推送 **P95 494ms**；**SQLite 事务租约锁（WAL 模式）**防并发重触发 LLM |
| 防幻觉与事实核查 | 核验原论文并隔离 **200 条存疑历史缓存**；30 题真实问答实现 **10/10 资料不足题准确拒答**（LLM-as-a-Judge 复核，事实一致性 **1.90/2.0**） |
| 自动化测试与交付 | **445 项 pytest** 后端回归 + **35 项**浏览器端验收 + 交付文件 **SHA-256 完整性校验清单** |

- **靠实验做减法**：航天手册含大量专有传感器编号且需压低延迟，24 题对比实测发现常用 RRF 拉低排序、Cross-Encoder Rerank 虽将 usable@5 提至 1.000 但致 MRR 跌至 0.807 且 GPU 单次耗时约 0.5s，权衡后舍弃并改用文档扩充与轻量加权，兼顾精度与 20ms 级延迟。
- **定位非显性失效**：排查出配置空字符串吞掉防幻觉提示词、以及早期缓存编造磁力计轴向/单位等静默缺陷，补齐边界知识文档、通用/诊断双模板与原文页码直达溯源。
- **指标口径治理**：严守整段评估与残缺段拒判，拒绝点调整刷分，段级与点级异常占比分母严格隔离。

**仓库**：https://github.com/Jerry518520/microsat-anomaly-analysis

*(注：企业实习期间参与的内部投研财报系统与运动健康工作流项目因涉及企业合规与保密规范，均不公开源码。)*

## 我怎么看待 LLM 工程

- **先定边界，再谈智能**：凡是能用确定性规则和代码算准的（如财务勾稽、差值计算、前置校验），绝不交给大模型概率发挥；模型只做它擅长的理解与表达。
- **非显性失效必须靠回归兜底**：LLM 的很多事故不会抛异常——提示词未生效、口径串行、答对结论但指错出处，都要靠断言校验、评测集和回归测试锁死。
- **宁可拒答，绝不编造**：高可靠业务场景里，资料不足时准确拒答并给出可核验的原文出处，远比生成一段看似流利的猜测更有工程价值。

## 联系我

- **邮箱**：jerrylbj@foxmail.com
- **意向方向**：AI Agent 开发 / FDE、AI 产品经理、AI 解决方案工程师（2027 届实习）
