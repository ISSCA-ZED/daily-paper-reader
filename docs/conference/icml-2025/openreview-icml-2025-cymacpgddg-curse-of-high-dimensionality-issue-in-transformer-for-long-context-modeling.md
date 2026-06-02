---
title: Curse of High Dimensionality Issue in Transformer for Long Context Modeling
title_zh: Transformer长上下文建模中的高维灾难问题
authors: "Shuhai Zhang, Zeng You, Yaofo Chen, Zhiquan Wen, Qianyue Wang, Zhijie Qiu, Yuanqing Li, Mingkui Tan"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=CYmaCpGDDG"
tags: ["query:key-tokens"]
score: 9.0
evidence: 识别注意力稀疏性并分离相关token
tldr: 针对Transformer长上下文建模中冗余注意力计算问题，本文通过将概率序列建模转化为监督学习任务，分离相关和不相关token。理论分析表明仅少数token对预测有显著贡献，为理解token重要性提供了新视角。
source: ICML-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2025-cymacpgddg/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1749, \"height\": 590, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-cymacpgddg/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 847, \"height\": 1205, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-cymacpgddg/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 825, \"height\": 404, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-cymacpgddg/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 461, \"height\": 389, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-cymacpgddg/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1068, \"height\": 503, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-cymacpgddg/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1763, \"height\": 2223, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-cymacpgddg/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1757, \"height\": 1481, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-icml-2025-cymacpgddg/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1778, \"height\": 234, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-cymacpgddg/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 860, \"height\": 237, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-cymacpgddg/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 868, \"height\": 253, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-cymacpgddg/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 994, \"height\": 196, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-cymacpgddg/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 901, \"height\": 161, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-cymacpgddg/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 992, \"height\": 196, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-cymacpgddg/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1775, \"height\": 145, \"label\": \"Table\"}]"
motivation: 长上下文建模中所有token占用相同计算资源，而注意力往往稀疏。
method: 将序列建模重新定义为监督学习，区分相关与无关token。
result: 理论证明只有少数token对预测显著贡献，揭示稀疏性。
conclusion: 为长上下文建模中的冗余消除和token重要性分析提供了理论基础。
---

## Abstract
Transformer-based large language models (LLMs) excel in natural language processing tasks by capturing long-range dependencies through self-attention mechanisms. However, long-context modeling faces significant computational inefficiencies due to redundant attention computations: while attention weights are often sparse, all tokens consume equal computational resources. In this paper, we reformulate traditional probabilistic sequence modeling as a supervised learning task, enabling the separation of relevant and irrelevant tokens and providing a clearer understanding of redundancy. Based on this reformulation, we theoretically analyze attention sparsity, revealing that only a few tokens significantly contribute to predictions. Building on this, we formulate attention optimization as a linear coding problem and propose a group coding strategy, theoretically showing its ability to improve robustness against random noise and enhance learning efficiency. Motivated by this, we propose Dynamic Group Attention (DGA), which leverages the group coding to explicitly reduce redundancy by aggregating less important tokens during attention computation. Empirical results show that our DGA significantly reduces computational costs while maintaining competitive performance.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 核心问题与整体含义（研究动机和背景）

Transformer 在长上下文建模中面临严重计算冗余：注意力权重往往高度稀疏（仅少数 token 贡献显著），但所有 token 仍占用相等的计算资源，导致效率低下。现有方法通过直接丢弃 token 来简化计算，但可能破坏关键 token 间的交互，影响性能。本文旨在 **不牺牲模型性能的前提下减少冗余计算**。作者通过将概率序列建模重新表述为监督学习任务，来区分相关和不相关 token，进而从理论和算法层面解决冗余问题。

## 2. 方法论

### 核心思想
- **监督学习形式化**：将自回归的下一 token 预测视为一个监督学习问题，将上下文 `C(y)` 分解为相关 token `x^R` 和无关 token `x^{IR}`，为冗余分析提供结构化视角。
- **注意力稀疏性理论**：证明在长上下文中，注意力权重服从 `ρ-sparse`，即只有少数 token 的概率显著大于 `1/(Lρ)`。上下文越长，稀疏性越强（定理1）。
- **组编码策略**：将优化目标建模为线性编码问题，并提出分组编码——将 `L` 个 token 分入 `k` 组，每组共享一个权重。理论表明该策略能将噪声方差降低 `1/m²`（定理2），并降低 Hessian 矩阵的条件数，加速收敛（定理3）。
- **动态组注意力 (DGA)**：
  - 通过快速采样计算所有 token 的重要性分数 `s_i`（近似注意力权重累加）。
  - 将前 `γ` 比例的 token 标记为 **焦点 token**（保持单独处理），其余为 **非焦点 token**。
  - 对非焦点 token 按组大小 `m` 分组，利用每组最后一个 token 的查询计算软权重，聚合它们的 K/V 对。
  - 引入 **互补 K/V**，为由于自回归性质无法访问组内信息的 token 补齐遗漏信息。
  - 最终用 Flash Attention 计算注意力，同时使用自定义因果掩码。

### 关键公式与算法流程
- 目标函数：`max ∏ Pθ(y|C(y))`
- 注意力稀疏性概率下界：`P_sparse(L, ρ) ≥ max_x [1 - (P_head * P_tail)^L]`
- 组编码后方差降低因子为 `1/m²`，条件数 `κ(Ḥ) ≤ κ(H)`
- DGA 算法步骤（Algorithm 1）：
  1. 计算重要性分数 `s` → 2. 划分焦点/非焦点 token → 3. 重排 K/V → 4. 聚合非焦点组 K/V → 5. 构造互补 K/V + 掩码 → 6. 执行 Flash Attention。

## 3. 实验设计

### 数据集与 Benchmark
- **预训练**：SlimPajama（627B token，LLaMA 预训练数据混合）。
- **长上下文理解**：LongBench-E（31K token，含单/多文档 QA、摘要、少样本学习、合成任务、代码）。
- **关键信息检索**：EM score（在 4K–32K 多文档上下文中找到正确答案）。
- **效率指标**：Inter-token Latency (ITL) 衡量生成速度。
- **稀疏性分析**：SlimPajama 和 WikiText2 上 100 条随机序列。

### 对比方法
- 基线模型：Vanilla Self-Attention (LLaMA2-7B)
- 高效方法：StreamingLLM, LM-Infinite, MInference
- 优化效率验证：GPT2-S 和 OPT-125M（对比 vanilla 自注意力）

## 4. 资源与算力

文中明确：
- **训练硬件**：8 × A800 GPUs
- **训练配置**：微批次大小 1，梯度累积 8 步，共训练 1000 步
- **模型规模**：LLaMA2-7B（连续预训练）、GPT2-S 和 OPT-125M（从零预训练）
- **推理测试**：单张 A800 GPU

未提及总训练时长（小时），但 7B 模型 1000 步在 8 卡上通常数小时内完成。

## 5. 实验数量与充分性

实验较为充分，涵盖六大类评估：
- **主实验**（表1-3）：LongBench-E 上 5 个任务类别 + EM score 在 4 种上下文长度的性能、ITL 对比。
- **稀疏性定量分析**（图2）：统计 100 条序列的注意力分布，验证稀疏性随长度增加。
- **优化效率**（图3a + 图4）：GPT2-S 与 OPT-125M 验证损失收敛曲线。
- **鲁棒性测试**（图3b）：在不同噪声方差下计算 KL 散度。
- **消融实验**（表4-7）：系统性地分析组大小 `m`、重要性率 `γ`、标记策略（Top-K vs Random）、互补 token 的影响。

实验的设计与对比是客观的：各对比方法采用官方默认配置，评价指标标准（PPL, EM, ITL），统计量足够（100 条随机序列）。消融实验覆盖了所有关键超参数，整体公平性较好。

## 6. 主要结论与发现

1. **注意力高度稀疏**：长上下文中只有极少 token 对预测重要，稀疏性随序列长度增强（定理1实验验证）。
2. **组编码策略有效**：降低噪声敏感度（方差降低 `1/m²`）并加速收敛（条件数下降）。
3. **DGA 计算效率显著**：在 LLaMA2-7B 上，ITL 降低至 28.80 ms（Vanilla 为 69.70 ms，快 2.42×），且优于所有对比的高效方法。
4. **性能保持**：DGA 在 LongBench-E 平均得分为 21.14（Vanilla 为 21.69），在 EM 长文本检索上表现最优（4K 和 32K 均第一）。
5. **收敛更快、更鲁棒**：预训练 loss 下降更快，对高斯噪声的 KL 散度变化更小。

## 7. 优点

- **理论驱动**：从概率建模到监督学习的独特视角，给出了注意力稀疏性的严格分析不等式，且基于线性编码理论推导了分组的好处。
- **方法新颖**：动态分组非焦点 token 而非直接丢弃，保留关键交互；引入互补 K/V 组件，避免自回归中的信息缺失。
- **实验扎实**：覆盖多个模型规模、上下文长度、任务类型，消融完整，尤其对比了 ITL 这一实用效率指标。
- **效率提升明显**：训练和推理均可加速，且性能几乎没有下降，部分场景甚至超过全注意力。

## 8. 不足与局限

- **模型规模有限**：仅在 7B 及以下模型上验证，未测试 13B/70B 等更大模型，无法确认可扩展性。
- **训练不充分**：仅 1000 步的连续预训练，离 LLM 的完整训练差距大，性能提升可能有限。
- **超参数固定**：组大小 `m=16`、重要性率 `γ=0.1` 在所有实验中统一，未探讨自适应调整机制，实际应用可能需要针对不同任务调优。
- **数据集覆盖不足**：仅使用英文 / 代码数据集，未涉及多语言或其他领域（如医学、法律）。
- **推理实现细节不够清晰**：解码阶段若生成 token 不达 `m'` 时使用标准注意力的开销未量化。
- **与 SOTA 稀疏注意力方法对比有限**：如未比较 Longformer、Big Bird 等经典方法，且 MInference 等 baseline 在部分任务上性能更好（如 Multi-Doc QA 和合成任务），DGA 在性能上未全面领先。

（完）
