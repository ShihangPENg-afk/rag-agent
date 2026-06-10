# 项目总览（简历 / 面试版）

围绕 **PDF 技术手册知识处理**，我完成了两个**相关但完全解耦**的独立项目：**rag-agent** 负责可检索、可推理的问答服务；**llm-finetune-manual** 负责领域微调数据与 LoRA 训练验证。二者共享业务场景，但代码、依赖与部署互不引用；**LoRA 微调模型尚未接入 rag-agent**，问答生成仍调用 DashScope 在线 API。

**rag-agent（Agentic RAG）** 基于 FastAPI + LangGraph：PDF 上传后切块、向量化并建立进程内 FAISS 索引。`/ask/` 主路径由 planner 拆子问题、agent 调用检索等工具、evaluator 汇总证据后作答，保留经典 RAG 对照链路。工程上提供 **Docker** 部署与 4 步 Smoke Test 验收；使用 **RAGAS** 在 3 条样本基线上测得 faithfulness 0.8750、answer_relevancy 0.8858（在线 API 环境，非全量评估）。知识库为进程内存，无持久化与 CI/CD。

**llm-finetune-manual（LoRA 微调）** 跑通 PDF → Alpaca 数据集（132 条）→ LLaMA-Factory LoRA 微调 → 权重保存全流程：以 Qwen2-7B-Instruct 为基座，在本地 CPU 抽样 50 条、1 epoch 完成流程验证，产出 adapter 权重。定位为**管线可复现验证**，非可用领域模型；before/after 评测与 GPU 全量训练尚未完成。

面试可强调：Agent 编排与工具化 RAG、Docker 可复现交付、RAGAS 质量基线、LoRA 数据与训练链路，以及对已完成演示与未生产化边界的清晰把控。
