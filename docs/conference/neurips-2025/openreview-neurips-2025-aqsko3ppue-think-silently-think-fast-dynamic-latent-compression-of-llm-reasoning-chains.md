---
title: "Think Silently, Think Fast: Dynamic Latent Compression of LLM Reasoning Chains"
title_zh: 静默思考，快速思考：LLM推理链的动态潜在压缩
authors: "Wenhui Tan, Jiaze Li, Jianzhong Ju, Zhenbo Luo, Ruihua Song, Jian Luan"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=AQsko3PPUe"
tags: ["query:key-tokens"]
score: 4.0
evidence: 通过合并token嵌入压缩推理链，涉及推理序列
tldr: 为缓解Token级别推理链计算效率低下的问题，本文提出压缩潜在推理框架CoLaR。该方法通过两阶段训练：在监督微调中引入辅助的下一个压缩嵌入预测目标，将连续token的嵌入按随机采样因子合并，从而在潜在空间中动态压缩推理链。实验表明该方法在保持推理性能的同时显著减少了推理步骤，但并未直接评估或识别关键token的重要性。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-neurips-2025-aqsko3ppue/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1450, \"height\": 357, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-aqsko3ppue/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1449, \"height\": 429, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-aqsko3ppue/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1439, \"height\": 603, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-aqsko3ppue/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 660, \"height\": 390, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-aqsko3ppue/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 660, \"height\": 389, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-aqsko3ppue/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 956, \"height\": 559, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-aqsko3ppue/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1020, \"height\": 382, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-aqsko3ppue/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 689, \"height\": 406, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-neurips-2025-aqsko3ppue/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1496, \"height\": 518, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-aqsko3ppue/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1495, \"height\": 335, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-aqsko3ppue/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1520, \"height\": 225, \"label\": \"Table\"}]"
motivation: Token级别的推理链计算昂贵且效率低下。
method: 提出CoLaR框架，通过辅助压缩嵌入预测目标在潜在空间动态合并token嵌入。
result: 在保持性能的同时显著减少了推理步骤。
conclusion: 实现了推理链的潜在压缩，但未聚焦于关键token识别。
---

## Abstract
Large Language Models (LLMs) achieve superior performance through Chain-of-Thought (CoT) reasoning, but these token-level reasoning chains are computationally expensive and inefficient.
In this paper, we introduce Compressed Latent Reasoning (CoLaR), a novel framework that dynamically compresses reasoning processes in latent space through a two-stage training approach.
First, during supervised fine-tuning, CoLaR extends beyond next-token prediction by incorporating an auxiliary next compressed embedding prediction objective. This process merges embeddings of consecutive tokens using a compression factor $c$ randomly sampled from a predefined range, and trains a specialized latent head to predict distributions of subsequent compressed embeddings. Second, we enhance CoLaR through reinforcement learning (RL) that leverages the latent head's non-deterministic nature to explore diverse reasoning paths and exploit more compact ones.
This approach enables CoLaR to: i) **perform reasoning at a dense latent level** (i.e., silently), substantially reducing reasoning chain length, and ii) **dynamically adjust reasoning speed** at inference time by simply prompting the desired compression factor.
Extensive experiments across four mathematical reasoning datasets demonstrate that CoLaR achieves 14.1% higher accuracy than latent-based baseline methods at comparable compression ratios, and reduces reasoning chain length by 53.3% with only 4.8% performance degradation compared to explicit CoT method. Moreover, when applied to more challenging mathematical reasoning tasks, our RL-enhanced CoLaR demonstrates performance gains of up to 5.4% while dramatically reducing latent reasoning chain length by 82.8%.
The code and models will be released upon acceptance.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 论文的核心问题与整体含义（研究动机和背景）
- **核心问题**：大型语言模型（LLM）通过链式思维（Chain-of-Thought, CoT）推理获得优异性能，但生成 token 级别的推理链计算成本高昂、效率低下，在高并发场景下尤其严重。
- **研究动机**：现有方法多在 token 级别进行优化（如跳过冗余 token、提示生成更简洁推理），或采用固定长度的潜在空间推理，缺乏动态适应性和探索-利用能力。
- **整体含义**：提出一种在潜在空间中动态压缩推理链的框架 CoLaR，通过将多个 token 的语义合并为一个潜在变量，大幅减少推理步骤，同时通过强化学习进一步提升准确率和压缩比。

## 2. 论文提出的方法论
### 2.1 核心思想
- 采用两阶段训练：**监督微调（SFT）** + **强化学习（RL）**。
- SFT 阶段引入辅助任务——**下一个压缩嵌入预测**，使模型学会在潜在空间中进行自回归推理。
- 推理时可动态调整压缩因子 $c$（通过提示指定），实现推理速度的灵活控制。

### 2.2 关键技术细节
- **嵌入压缩模块**：将连续 $c$ 个 reasoning token 的嵌入求和后除以 $\sqrt{c}$（保持分布方差稳定），得到压缩嵌入 $e^c$。
- **潜在头（Latent Head）**：一个两层 MLP，输出下一个压缩嵌入的均值 $\hat{\mu}$ 和标准差 $\hat{\sigma}$（概率分布），使用**重参数化技巧**采样 $\hat{e} = \hat{\mu} + \hat{\sigma}\epsilon$，实现多样化推理。
- **损失函数**：
  - 语言建模损失（$L_{comp}$）：随机采样每组压缩 token 中的一个 token 作为标签，训练语言头预测。
  - 潜在损失（$L_{latent}$）：可选 NLL 或 soft-MSE（含熵正则项，鼓励探索）。
- **RL 阶段**：使用 GRPO 算法，对同一问题采样多组输出，计算群体归一化奖励，并采用**按 token 平均奖励**的设计，鼓励更短的正确推理路径。
- **推理时**：由潜在头自回归生成压缩嵌入，由语言头决定何时终止推理并输出答案。

## 3. 实验设计
### 3.1 数据集与场景
- **小学数学推理**：GSM8k-Aug（385k 训练样本）、GSM8k-hard、SVAMP、MultiArith。
- **更具挑战性的数学推理**：MATH（7.5k 训练，5k 测试）。
- **额外基准测试**：GPQA（物理/化学/生物，用于缩放实验）。

### 3.2 对比方法
- **显式推理基线**：CoT（完整推理链）、iCoT（逐步内化推理步骤）。
- **潜在推理基线**：Coconut（固定长度潜在推理）、Distill（复现 CODI，自蒸馏固定长度）。
- **其他效率方法**：TokenSkip（跳过冗余 token）。
- **消融变体**：Deterministic Latent head（DL）、无压缩 token 监督（OC）、均值池化（MP）、NLL 损失。

### 3.3 评估指标
- **准确率（Acc.）**：答案正确率。
- **推理链长度（#L）**：平均 token/潜在变量数量。
- 所有结果报告 5 次随机种子的平均值和 95% 置信区间。

## 4. 资源与算力
- **硬件**：SFT 阶段使用 8 张 A100 GPU（分布式数据并行）；RL 阶段使用单张 A100 GPU。
- **超参数**：总 batch size 256（SFT）；RL 中 rollout batch size 8，group size G=8。
- **训练时长**：最多 50 个 epoch 或 12 小时（取先到者），选择验证集最佳 checkpoint。
- **未明确的细节**：文中未报告每个实验的具体 GPU 运行时间（小时数），仅给出上限。

## 5. 实验数量与充分性
- **实验数量**：涵盖主要对比实验（表 1）、消融实验（表 1 灰色部分）、RL 实验（表 2）、缩放实验（表 3）、动态压缩因子分析（图 4、5）、层间分析（图 6）、案例研究（图 3）、训练曲线（图 7）等多组实验，总计超过 10 组独立实验。
- **充分性**：实验覆盖了多个数据集、多种基线、多种压缩因子、不同模型规模（1B/3B/8B），以及消融分别检验各组件贡献。公平性方面，所有方法初始化为 CoT-SFT 权重，使用相同训练/推理设置，报告置信区间，重复 5 次。
- **客观性**：结果支持论文主要主张，无明显偏袒。

## 6. 论文的主要结论与发现
- CoLaR 在同类压缩比下相比潜在基线（Coconut）准确率提升 **14.1%**。
- 相比显式 CoT，推理链长度减少 **53.3%**，准确率仅下降 **4.8%**（c=2）。
- 在 MATH 数据集上，RL 后准确率提升 **5.36%**，同时长度减少 **82.8%**。
- 动态压缩因子训练使模型能泛化到未见过的因子（如训练 c∈{1,3,5,7}，测试 c∈{2,4,6}）。
- 模型规模越大，CoLaR 的压缩和准确率增益越显著（例如 8B 模型在 GPQA 上超越 CoT 教师）。
- 概率潜在头对于 RL 探索至关重要；确定性潜在头在复杂问题上表现更差。
- 平均奖励设计促进更短推理路径的利用。

## 7. 优点
- **方法创新**：首次在潜在推理中支持动态压缩因子，并引入概率潜在头实现探索-利用。
- **效率显著**：在极低性能损失下大幅降低推理步骤，实用价值高。
- **解释性**：通过余弦相似度将潜在变量解码为 token，使“潜在思考”过程透明化。
- **鲁棒性**：在 OOD 数据集（MultiArith）上表现接近显式 CoT，优于其他潜在基线。
- **缩放性**：验证了方法在 1B 到 8B 模型上均有效，且 RL 提升随模型质量增强。

## 8. 不足与局限
- **性能天花板**：除 GPQA 外，CoLaR 尚未全面超越显式 CoT 的准确率（仅逼近）。
- **压缩因子的离散性**：无法推广到非整数压缩因子（如 c=1.5）或大于训练最大因子（c>c_max），受 token 化约束。
- **潜在风险**：可能放大推理偏差或被滥用于生成更令人信服的错误信息，需要下游监控。
- **实验覆盖**：仅在数学推理数据集上验证，未涉及常识推理、代码生成等更广泛任务。
- **训练成本**：需两阶段训练（SFT+RL），且未报告完整 GPU 小时数，复现成本较高。

（完）
