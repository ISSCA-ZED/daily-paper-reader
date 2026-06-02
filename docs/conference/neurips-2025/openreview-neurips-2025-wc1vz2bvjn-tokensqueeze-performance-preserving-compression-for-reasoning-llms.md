---
title: "TokenSqueeze: Performance-Preserving Compression for Reasoning LLMs"
title_zh: "TokenSqueeze: 面向推理LLM的性能保持型压缩"
authors: "Yuxiang Zhang, Zhengxu Yu, Weihang Pan, Zhongming Jin, Qiang Fu, Deng Cai, Binbin Lin, Jieping Ye"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=Wc1VZ2bVJn"
tags: ["query:key-tokens"]
score: 6.0
evidence: 压缩推理路径同时保持性能，暗示识别重要token
tldr: 针对推理LLM长思维链导致token消耗大、延时高的问题，本文提出TokenSqueeze方法。该方法在保持性能的前提下压缩推理路径，通过在压缩过程中保留关键信息来减少token数。实验证明TokenSqueeze能够在显著降低推理成本的同时维持高精度，其成功必然依赖于对推理中重要token的识别，尽管论文未明确阐述识别机制。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-neurips-2025-wc1vz2bvjn/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1294, \"height\": 762, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-wc1vz2bvjn/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1301, \"height\": 671, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-wc1vz2bvjn/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1210, \"height\": 537, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-wc1vz2bvjn/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 713, \"height\": 469, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-wc1vz2bvjn/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1404, \"height\": 1438, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-wc1vz2bvjn/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1430, \"height\": 826, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-wc1vz2bvjn/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1423, \"height\": 911, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-neurips-2025-wc1vz2bvjn/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1456, \"height\": 731, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-wc1vz2bvjn/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1037, \"height\": 292, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-wc1vz2bvjn/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1395, \"height\": 331, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-wc1vz2bvjn/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1119, \"height\": 292, \"label\": \"Table\"}]"
motivation: 长思维链导致token消耗增加，现有压缩方法牺牲准确性。
method: 提出TokenSqueeze压缩推理路径，在保持性能的同时减少token数。
result: 在降低推理成本的同时维持了高精度。
conclusion: 为推理路径压缩提供了性能保持的方案，间接涉及关键token保留。
---

## Abstract
Emerging reasoning LLMs such as OpenAI-o1 and DeepSeek-R1 have achieved strong performance on complex reasoning tasks by generating long chain-of-thought (CoT) traces. However, these long CoTs result in increased token usage, leading to higher inference latency and memory consumption. As a result, balancing accuracy and reasoning efficiency has become essential for deploying reasoning LLMs in practical applications. Existing long-to-short (Long2Short) methods aim to reduce inference length but often sacrifice accuracy, revealing a need for an approach that maintains performance while lowering token costs. To address this efficiency-accuracy tradeoff, we propose TokenSqueeze, a novel Long2Short method that condenses reasoning paths while preserving performance and relying exclusively on self-generated data. First, to prevent performance degradation caused by excessive compression of reasoning depth, we propose to select self-generated samples whose reasoning depth is adaptively matched to the complexity of the problem. To further optimize the linguistic expression without altering the underlying reasoning paths, we introduce a distribution-aligned linguistic refinement method that enhances the clarity and conciseness of the reasoning path while preserving its logical integrity. Comprehensive experimental results demonstrated the effectiveness of TokenSqueeze in reducing token usage while maintaining accuracy. Notably, DeepSeek‑R1‑Distill‑Qwen‑7B fine-tuned by using our proposed method achieved a 50\% average token reduction while preserving accuracy on the MATH500 benchmark. TokenSqueeze exclusively utilizes the model's self-generated data, enabling efficient and high-fidelity reasoning without relying on manually curated short-answer datasets across diverse applications. Our code is available at \url{https://github.com/zhangyx1122/TokenSqueeze}.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 核心问题与整体含义（研究动机和背景）

- **问题**：新兴推理大语言模型（如 OpenAI-o1、DeepSeek-R1）通过生成极长的思维链（CoT）来提升复杂推理能力，但这导致 token 使用量激增，推理延迟和内存消耗显著增加。同时，对于简单问题，模型常存在“过度思考”现象，生成冗余步骤，降低实际应用效率。
- **背景**：已有长转短（Long2Short）方法尝试压缩输入长度，但往往牺牲准确性；在线强化学习方法虽有效但计算昂贵；离线方法多选择最短正确回答，易丢失必要推理步骤，导致“推理过度简化”问题。
- **动机**：急需一种既能显著降低 token 消耗，又能保持甚至提升模型性能的方法，且避免依赖人工标注或外部教师模型。

## 2. 方法论：核心思想、关键技术细节

- **核心思想**：将长转短问题视为一种偏好学习任务，在保持推理深度的前提下，教模型以简洁语言表达。核心在于保留自适应的推理深度（根据问题复杂度动态调整长度），并通过语言精炼和长度感知优化实现压缩。
- **关键技术细节**：
  - **自适应推理深度选择（Adaptive Reasoning Depth Selection）**：
    - 对每个问题，从模型自身采样多个回答，筛选出正确回答。
    - 定义自适应分位数 \( q = \alpha \cdot (1 - p) \)，其中 \( p \) 是正确率，\( \alpha \) 为超参数（实验设为 0.2）。
    - 根据 \( q \) 确定长度阈值，选取长度较短的正确答案作为正样本（回答配对）。
    - 优势：简单问题采用更短链，复杂问题保留更长链以捕捉必要逻辑。
  - **步内语言精炼（Intra-Step Linguistic Refinement）**：
    - 对选出的正样本中的每个推理步骤，重新采样 K 个候选改写（K=64），选择满足 KL 散度约束（阈值 ε=0.005）的最短改写，以保持语义完整性。
    - KL 散度通过局部 token 窗口近似计算（公式见论文），确保改写后模型后续分布变化极小。
  - **复合优化目标（Composite Optimization Objective）**：
    - 在标准 DPO 基础上引入长度感知边际：\( \mathcal{L}_{\text{DPO-L}} \) 包含额外项 \( \lambda \log(\ell(y_l)/\ell(y_w)) \)，根据相对长度差缩放偏好信号。
    - 联合 SFT 损失与 DPO-L 损失（权重 η=0.5），避免 DPO 单独训练导致奖励崩塌。
- **流程总结**：自采样 → 自适应深度选择 → 步内精炼 → 长度感知偏好训练。

## 3. 实验设计

- **数据集/基准**：
  - AIME24（数学竞赛题）
  - MATH500（数学问题）
  - AIME25（最新数学竞赛题）
  - LiveCodeBench（代码题，仅采用 2024.08.01-2025.01.31 的问题以避免数据泄露）
- **评价指标**：
  - Answer Accuracy（准确率）
  - Average Length of Correct Responses (Len-T)
  - Average Length of All Responses (Len-A)
  - Area Under the Curve (AUC)（在 32K token 预算下精度-长度曲线下面积）
- **对比方法**：
  - 基础模型（baseline）
  - Kimi-k1.5 (DPO)（复现版本）
  - DAST (Difficulty-Adaptive Slow-Thinking)
  - TrainEffi (Training Language Models to Reason Efficiently)
  - 消融实验额外包括：No Refinement、GPT-4o-mini Rewrite、TokenSkip Rewrite、DPO、SFT、DPO+SFT 等。
- **模型规模**：DeepSeek-R1-Distill-Qwen-7B 和 1.5B。

## 4. 资源与算力

- **算力配置**：8 × NVIDIA Tesla A100 GPU。
- **训练时长**：约一天（文中提及 “completes within approximately one day”）。
- **超参数**：学习率 5e-6，batch size 128，最大上下文长度 9000 tokens，全参数微调。
- **采样配置**：自采样温度 0.9，精炼步骤采样温度 1.0，每步 64 个候选。

## 5. 实验数量与充分性

- **实验数量**：
  - 主表（Table 1）包含 4 个数据集 × 2 种模型规模，对比 3-4 种方法。
  - 消融实验：
    - 自适应深度选择（Table 2）：4 种配置（Shortest, Q-FIX, Q-DYN w/ extra pos, Q-DYN）。
    - 步内语言精炼（Table 3）：5 种配置（Baseline, No Refinement, 4o-mini Rewrite, TokenSkip Rewrite, TokenSqueeze）。
    - 复合优化目标（Table 4）：4 种配置（DPO, SFT, DPO+SFT, TokenSqueeze）。
    - 超参数 α 影响（Figure 4）。
    - Token 预算下精度对比（Figure 3）。
- **充分性与客观性**：
  - 所有结果平均 16 次独立运行，降低方差。
  - 对比基线覆盖主流同类方法（Kimi-k1.5、DAST、TrainEffi），并复现了未开源的方法。
  - 消融实验逐一验证各组件贡献，设计合理。
  - 数据集涵盖数学和代码两类推理任务，规模适中但具代表性。
  - **可能不足**：仅测试了 Qwen 蒸馏系列模型（7B/1.5B），未在更大模型或其他架构（如 Llama）上验证；LiveCodeBench 对比方法较少。

## 6. 主要结论与发现

- TokenSqueeze 在 **显著降低 token 用量**（MATH500 上 7B 模型平均减少 51.3%）的同时，**保持甚至提升**准确率（AIME24 上 7B 准确率提升 2 个百分点）。
- AUC 指标全面优于基线和其他方法，说明在有限 token 预算下精度更高。
- 自适应深度选择优于固定最短选择，避免了过度压缩导致的性能损失。
- 步内精炼在保持逻辑完整性的同时有效缩短步内长度；GPT-4o-mini 和 TokenSkip 改写反而降低准确率。
- 复合目标（SFT + 长度感知 DPO）比单独 DPO 或 SFT 效果更好，长度正则项有助于平衡效率与精度。

## 7. 优点

- **完全自生成数据**：无需外部模型或人工标注，可扩展性强。
- **组件设计精细**：自适应选择、KL 约束精炼、长度感知目标三者有机结合。
- **实验严谨**：多次独立运行、消融实验全面、对比方法复现。
- **性能提升显著**：在压缩过半 token 的情况下仍保持甚至提升准确率，实际部署价值高。
- **兼顾多领域**：数学和代码任务均有效，表明泛化能力。

## 8. 不足与局限

- **超参数启发式确定**：KL 阈值 ε、α、λ 等通过有限实验手动设定，缺乏系统性调优或自适应机制。
- **仅离线偏好优化**：无法在训练中根据新反馈持续调整，未来可扩展为在线强化学习。
- **模型和任务覆盖有限**：仅在 DeepSeek-R1-Distill-Qwen 系列（7B/1.5B）上实验，未验证更大模型或其他架构；LiveCodeBench 仅包含部分时间段。
- **未见对“token重要性识别”的显式分析**：虽然压缩依赖于保留关键信息，但未深入探讨模型如何识别重要 token，机制解释较弱。
- **缺乏与其他长转短方法（如基于 prompt 的压缩、推理时剪枝）的系统对比**：仅对比了训练驱动方法。

（完）
