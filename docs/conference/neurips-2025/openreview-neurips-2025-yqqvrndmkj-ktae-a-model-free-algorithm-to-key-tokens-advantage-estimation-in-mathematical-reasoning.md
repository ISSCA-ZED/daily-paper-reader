---
title: "KTAE: A Model-Free Algorithm to Key-Tokens Advantage Estimation in Mathematical Reasoning"
title_zh: KTAE：数学推理中关键token优势估计的无模型算法
authors: "Wei Sun, Wen Yang, Pu Jian, Qianlong Du, Fuwei Cui, Shuo Ren, Jiajun Zhang"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=yqQVRNdmKJ"
tags: ["query:key-tokens"]
score: 10.0
evidence: 直接提出推理中关键token优势估计方法
tldr: 提出KTAE算法，无需额外模型即可估计数学推理中关键token的细粒度优势，解决了现有强化学习算法中token级奖励粗糙的问题。该方法直接识别推理序列中的关键token，并赋予其更高的优势值，显著提升推理性能。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-neurips-2025-yqqvrndmkj/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1385, \"height\": 597, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-yqqvrndmkj/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1432, \"height\": 548, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-yqqvrndmkj/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1384, \"height\": 612, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-yqqvrndmkj/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1454, \"height\": 423, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-yqqvrndmkj/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1454, \"height\": 388, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-yqqvrndmkj/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1406, \"height\": 446, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-yqqvrndmkj/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1428, \"height\": 456, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-yqqvrndmkj/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1450, \"height\": 1962, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-yqqvrndmkj/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1439, \"height\": 337, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-yqqvrndmkj/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1508, \"height\": 1918, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-neurips-2025-yqqvrndmkj/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1401, \"height\": 1051, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-yqqvrndmkj/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1339, \"height\": 810, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-yqqvrndmkj/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 939, \"height\": 297, \"label\": \"Table\"}]"
motivation: 现有强化学习算法为序列中所有token分配相同优势，忽略了token贡献差异。
method: 提出KTAE，通过无模型方法估计每个token的细粒度优势。
result: 在数学推理任务上，KTAE优于GRPO等基线，尤其提升复杂问题解决率。
conclusion: 关键token优势估计能更有效指导模型学习。
---

## Abstract
Recent advances have demonstrated that integrating reinforcement learning with rule-based rewards can significantly enhance the reasoning capabilities of large language models (LLMs), even without supervised fine-tuning (SFT). However, prevalent reinforcement learning algorithms such as GRPO and its variants like DAPO, suffer from a coarse granularity issue when computing the advantage. Specifically, they compute rollout-level advantages that assign identical values to every token within a sequence, failing to capture token-specific contributions. To address this limitation, we propose Key-token Advantage Estimation (KTAE)—a novel algorithm that estimates fine-grained, token-level advantages without introducing additional models. KTAE leverages the correctness of sampled rollouts and applies statistical analysis to quantify the importance of individual tokens within a sequence to the final outcome. This quantified token-level importance is then combined with the rollout-level advantage to obtain a more fine-grained token-level advantage estimation. Empirical results show that models trained with GRPO+KTAE and DAPO+KTAE outperform baseline methods across five mathematical reasoning benchmarks. Notably, they achieve higher accuracy with shorter responses and even surpass R1-Distill-Qwen-1.5B using the same base model.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义（研究动机和背景）
- **背景**：强化学习（RL）结合基于规则的奖励能显著提升大语言模型（LLM）的数学推理能力，即使没有监督微调（SFT）。DeepSeek R1 等模型通过 RL 实现了“顿悟时刻”。
- **问题**：现有主流 RL 算法（如 GRPO、DAPO）在计算优势（advantage）时粒度粗糙——它们为同一 rollout 中的所有 token 分配相同的优势值，忽略了不同 token 对最终结果的贡献差异。这种粗粒度的赋值限制了学习效率。
- **目标**：提出一种无需额外模型、能估计每个 token 细粒度优势的算法，从而更有效地引导模型关注关键 token。

### 2. 论文提出的方法论
- **核心思想**：通过统计方法，利用采样 rollout 的正确性（正确/错误）量化每个 token 与正确 rollout 之间的关联强度和方向，得到 token 级关键值（key-token-value），并将其加到原始 rollout-level 优势上，形成 token-level 优势。
- **关键技术细节**：
  1. **构建列联表**：对每个 token，统计其在正确/错误 rollout 中出现与不出现的次数，形成 2×2 列联表。
  2. **量化关联强度**：
     - **Fisher 精确检验**：计算 p 值并通过指数变换得到关联强度得分 \( F(o_{ij}) \)（p=1 时得 0，p→0 时逼近 1）。
     - **信息增益**：计算 token 出现与否对 rollout 正确性的不确定性减少量 \( IG(o_{ij}) \)。
  3. **量化关联方向**：利用 BM25 中的词频标准化公式计算 token 在正确/错误 rollout 中的标准化频率，结合 Cohen’s h 效应量和频率比例差，得到方向得分 \( D(o_{ij}) \)，可正可负。
  4. **计算最终关键值**：将关联强度（\( h_1 F + h_2 IG \)）与方向得分相乘，再经 sigmoid 归一化后与 GRPO 的 rollout-level 优势相加，得到 token-level 优势。
- **算法流程**（Algorithm 1）：采样 G 个 rollout → 计算 GRPO 优势 → 构建 token 列联表 → 计算 \( F, IG, D \) → 得到 key-token-value → 叠加到原有优势上。

### 3. 实验设计
- **数据集**：
  - 训练集：MATH12k（初步验证）及其子集 math-level3-5（7B 模型比较实验）。
  - 测试基准：AIME24、MATH-500、AMC、Minerva、OlympiadBench，共 5 个数学推理 benchmark。
- **对比方法**：GRPO、DAPO、Oat-Zero、OpenReasoner-Zero、SimpleRL-Zero、Eurus-2-7B-PRIME、R1-Distill-Qwen-1.5B 等。
- **模型基座**：Qwen2.5-Math-1.5B（方法验证）；Qwen2.5-Math-7B（与基线对比）。
- **实验设置**：零样本贪婪解码（temperature=0），pass@1 评估，固定随机种子。

### 4. 资源与算力
- **硬件**：8 块 NVIDIA H100 80G GPU。
- **训练时间**（表 3）：在 7B 模型上，GRPO+KTAE 每步约 642 秒，DAPO+KTAE 每步约 1159 秒；相比纯 GRPO（559 秒）和 DAPO（1006 秒），KTAE 引入约 15%~77% 的额外时间，但主要取决于生成 token 数，与模型大小弱相关。
- **其他**：未报告总训练步数或总时长，但提及当前 CPU 串行实现效率低，GPU 利用率不足 1%，未来可通过工程优化大幅提升。

### 5. 实验数量与充分性
- **实验组数**：
  - 1.5B 模型：验证 KTAE 与 GRPO/DAPO 组合的效果，对比 5 个 baseline。
  - 7B 模型：与 7 个强弱基线在 5 个 benchmark 上比较（表 1）。
  - 消融实验：分别移除 Fisher、IG、tf 三个组件，观察对 accuracy、length、entropy 的影响（图 5）。
  - 训练曲线：展示 test accuracy、mean response length、generation entropy 随步骤的变化（图 4）。
  - 可视化示例：展示 KTAE 如何为正确但被规则误判为错误的 rollout 分配正负关键值（图 2），以及“aha moment”案例（附录 K）。
- **充分性**：实验覆盖了不同参数规模、多个数据集、多种基线、消融分析，较为充分。但未报告多次运行的误差棒（仅使用固定随机种子和 temperature=0 减少随机性），统计显著性未量化，存在一定偏差风险。

### 6. 论文的主要结论与发现
- KTAE 能有效提升模型在数学推理基准上的平均准确率，同时显著缩短响应长度（无需额外长度惩罚），实现更高的推理效率。
- KTAE 与 GRPO 或 DAPO 结合后，在 5 个 benchmark 上的平均分均超过原始算法及其他基线，且在 1.5B 模型上超越同基座的 R1-Distill-Qwen-1.5B。
- KTAE 可以识别关键 token（如数值、符号等），并在模型训练中诱导“顿悟时刻”式的自我反思行为。
- 消融实验表明，信息增益（IG）组件对准确率和长度控制最重要，Fisher 和 tf 组件也有贡献，三者缺一不可。

### 7. 优点
- **无需额外模型**：KTAE 完全基于采样 rollout 的统计量，不引入新的参数或模型，成本低。
- **可解释性强**：使用 Fisher 精确检验、信息增益、词频等经典统计方法，量化了 each token 与正确性的关联强度和方向。
- **避免 reward hacking**：保留原始 rollout-level 优势，关键值仅作为偏移，不易被模型利用奖励漏洞。
- **即插即用**：兼容 GRPO、DAPO 等主流算法，可直接添加。
- **高效推理**：显著缩短回答长度，提升 token 利用率，降低推理成本。

### 8. 不足与局限
- **模型规模有限**：实验仅在 1.5B 和 7B 模型上进行，未验证在更大模型（如 70B）上的效果。
- **领域局限**：仅测试了数学推理任务，未在其他规则奖励场景（如代码生成、符号推理）或连续奖励场景中验证。
- **单 token 信息量不足**：单个 token 的出现与否有时难以决定最终结果，统计可能受随机波动影响。
- **计算效率**：当前实现中 KTAE 由于缺乏 tensor 并行优化，GPU 利用率低，训练时间增加较明显（尤其是 DAPO+KTAE 组合）。
- **统计显著性缺失**：未报告多次实验的均值和方差，结果稳健性有待进一步验证。

（完）
