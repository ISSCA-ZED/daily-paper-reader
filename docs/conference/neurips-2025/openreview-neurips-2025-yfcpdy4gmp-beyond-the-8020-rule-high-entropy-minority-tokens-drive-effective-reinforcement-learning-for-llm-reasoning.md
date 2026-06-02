---
title: "Beyond the 80/20 Rule: High-Entropy Minority Tokens Drive Effective Reinforcement Learning for LLM Reasoning"
title_zh: 超越80/20法则：高熵少数令牌驱动LLM推理的有效强化学习
authors: "Shenzhi Wang, Le Yu, Chang Gao, Chujie Zheng, Shixuan Liu, Rui Lu, Kai Dang, Xiong-Hui Chen, Jianxin Yang, Zhenru Zhang, Yuqiong Liu, An Yang, Andrew Zhao, Yang Yue, Shiji Song, Bowen Yu, Gao Huang, Junyang Lin"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=yfcpdY4gMP"
tags: ["query:key-tokens"]
score: 9.0
evidence: 令牌熵模式作为推理中关键分叉令牌的重要性度量
tldr: "现有强化学习方法虽能提升LLM推理能力，但其内部机制尚不明确。本文从令牌熵模式的新视角，发现推理链中仅约20%的高熵令牌在语义上充当关键分叉点，引导模型走向不同推理路径。通过深入分析这些高熵令牌对推理性能的影响，揭示了少数关键令牌驱动有效强化学习的原理。该工作为理解推理中的令牌重要性提供了新度量，并具有优化强化学习训练的潜力。"
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-neurips-2025-yfcpdy4gmp/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1444, \"height\": 598, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-yfcpdy4gmp/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1243, \"height\": 556, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-yfcpdy4gmp/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 759, \"height\": 590, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-yfcpdy4gmp/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1424, \"height\": 416, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-yfcpdy4gmp/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1454, \"height\": 1975, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-yfcpdy4gmp/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1449, \"height\": 1992, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-yfcpdy4gmp/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1459, \"height\": 838, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-yfcpdy4gmp/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1449, \"height\": 647, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-yfcpdy4gmp/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1144, \"height\": 557, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-yfcpdy4gmp/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1448, \"height\": 647, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-yfcpdy4gmp/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1383, \"height\": 651, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-yfcpdy4gmp/fig-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1321, \"height\": 2127, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-yfcpdy4gmp/fig-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1354, \"height\": 2143, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-yfcpdy4gmp/fig-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 1350, \"height\": 2108, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-yfcpdy4gmp/fig-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 1338, \"height\": 2124, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-yfcpdy4gmp/fig-016.webp\", \"caption\": \"\", \"page\": 0, \"index\": 16, \"width\": 1344, \"height\": 2119, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-yfcpdy4gmp/fig-017.webp\", \"caption\": \"\", \"page\": 0, \"index\": 17, \"width\": 1354, \"height\": 874, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-neurips-2025-yfcpdy4gmp/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1466, \"height\": 205, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-yfcpdy4gmp/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1444, \"height\": 1274, \"label\": \"Table\"}]"
motivation: 现有RLVR方法对推理机制理解不足，希望从令牌熵角度揭示关键令牌如何影响推理。
method: 通过分析CoT推理中的令牌熵模式，识别高熵令牌作为关键分叉点，并研究其与推理性能的关系。
result: "发现仅约20%的高熵令牌是关键分叉，它们引导模型走向不同推理路径，显著影响推理表现。"
conclusion: 令牌熵可作为衡量推理中令牌重要性的有效指标，为优化强化学习训练提供新视角。
---

## Abstract
Reinforcement Learning with Verifiable Rewards (RLVR) has emerged as a powerful approach to enhancing the reasoning capabilities of Large Language Models (LLMs), yet its underlying mechanisms remain insufficiently understood. In this work, we undertake a pioneering exploration of RLVR through the novel perspective of token entropy patterns, comprehensively analyzing how different tokens influence reasoning performance. By examining token entropy patterns in Chain-of-Thought (CoT) reasoning, we observe that only a small fraction (approximately 20\%) of tokens exhibit high entropy, and these tokens semantically act as critical forks that steer the model toward diverse reasoning pathways. We further demonstrate that moderately increasing the entropy of these high-entropy tokens via decoding temperature adjustments leads to improved performance, quantitatively confirming their role as decision points in reasoning. We ultimately refine RLVR by restricting policy gradient updates to these forking tokens. Despite utilizing only 20\% of tokens, our approach achieves comparable performance to full-gradient updates on the Qwen3-8B base model. Moreover, it demonstrates remarkable improvements on the larger Qwen3-32B base model, boosting AIME'25 scores by 11.04 and AIME'24 scores by 7.71. In contrast, training exclusively on the 80\% lowest-entropy tokens leads to a marked decline in performance. These findings indicate that the efficacy of RLVR primarily arises from optimizing the high-entropy tokens that dictate key reasoning directions. Collectively, our results suggest promising avenues for optimizing RLVR algorithms by strategically leveraging the potential of these high-entropy minority tokens to further enhance the reasoning abilities of LLMs.

---

## 论文详细总结（自动生成）

# 论文总结：Beyond the 80/20 Rule: High-Entropy Minority Tokens Drive Effective Reinforcement Learning for LLM Reasoning

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **研究动机**：强化学习（RLVR）已被证明能有效提升大语言模型（LLM）的推理能力，然而其内在机制尚不清晰。现有方法对所有令牌统一计算梯度，忽略了不同令牌在推理过程中的不同功能角色，可能限制了性能的进一步提升。
- **核心问题**：究竟哪些令牌对推理性能贡献最大？能否从令牌熵（token entropy）的角度揭示RLVR的作用机理，并据此优化训练，实现更高效的推理强化学习？
- **整体含义**：本文首次从令牌熵的视角分析RLVR机制，发现只有少量（约20%）的高熵令牌扮演着关键“分叉”角色，它们决定了推理方向，而低熵令牌则跟随既定路径。进一步证实了高熵令牌的训练贡献几乎主导了整个RLVR的性能提升，而低熵令牌贡献微弱甚至有害。基于此，通过仅保留高熵令牌的梯度更新，可在不牺牲性能甚至显著提升性能的同时大幅节省计算量，并呈现模型规模正向扩展趋势。

## 2. 论文提出的方法论：核心思想、关键技术细节

### 核心思想
- 在CoT推理中，令牌熵分布呈现明显的“长尾”特征：大多数令牌（约80%）熵值很低（接近0），仅有约20%的令牌熵值较高。这些高熵令牌在语义上往往是连词、转折词、假设词等逻辑连接点，它们充当推理路径的“分叉点”（forking tokens），引导模型走向不同的推理方向。低熵令牌则多为后缀、代码片段、数学表达式等确定性内容。
- RLVR训练过程中，模型基本保留了基座模型的熵模式（高熵与低熵令牌分布基本不变），主要变化在于高熵令牌的熵值有所提升，低熵令牌变化极小。
- 因此，RLVR的效果主要源自对高熵分叉令牌的优化，低熵令牌作用甚微。基于此，提出仅对高熵令牌进行策略梯度更新，其余令牌的梯度被掩盖。

### 关键技术细节
- **令牌熵计算**：  
  \[
  H_t = -\sum_{j=1}^V p_{t,j}\log p_{t,j},\quad \mathbf{p}_t = \pi_\theta(\cdot|q,o_{<t}) = \text{Softmax}(\mathbf{z}_t/T)
  \]  
  其中 \(T\) 为解码温度。
- **RLVR优化目标（基于DAPO）**：  
  标准DAPO的优化目标为：
  \[
  J_{\text{DAPO}}(\theta) = \mathbb{E}_{B\sim D,(q,a)\sim B,\{o_i\}_{i=1}^G\sim\pi_{\theta_{\text{old}}}(\cdot|q)}\left[\frac{1}{\sum_{i=1}^G|o_i|}\sum_{i=1}^G\sum_{t=1}^{|o_i|}\min\left(r_{it}(\theta)\hat{A}_{it},\text{clip}(r_{it}(\theta),1-\epsilon_{\text{low}},1+\epsilon_{\text{high}})\hat{A}_{it}\right)\right]
  \]  
  本文仅保留高熵令牌的梯度：
  \[
  J_{\text{HighEnt}}(\theta) = \mathbb{E}_{B,\{o_i\}}\left[\frac{1}{\sum_{i=1}^G\sum_{t=1}^{|o_i|}\mathbb{I}[H_{it}\geq\tau_B^\rho]}\sum_{i=1}^G\sum_{t=1}^{|o_i|}\mathbb{I}[H_{it}\geq\tau_B^\rho]\min\bigl(r_{it}(\theta)\hat{A}_{it},\text{clip}(r_{it}(\theta),\dots)\hat{A}_{it}\bigr)\right]
  \]  
  其中 \(\rho\) 是保留的高熵令牌比例（默认为20%），\(\tau_B^\rho\) 是在当前batch内按熵排序的阈值。
- 其他超参数与DAPO保持一致：clip-higher（\(\epsilon_{\text{high}}=0.28,\epsilon_{\text{low}}=0.2\)）、overlong reward shaping、动态采样等。训练batch size=512，mini-batch size=32，learning rate=1e-6，无KL散度损失和熵损失。

## 3. 实验设计：数据集、基准、对比方法

- **训练数据集**：DAPO-Math-17K（包含17000道数学题）。
- **评测基准**（6个标准数学推理数据集）：
  - AIME'24、AIME'25、AMC'23、MATH500、Minerva、OlympiadBench（均为零样本测试）。
  - 此外还在代码推理基准LiveCodeBench（v5, 2024.08-2025.02）上测试了跨领域泛化能力。
- **对比方法**：
  - 基线：vanilla DAPO（使用全部令牌的梯度）。
  - 对比变体：仅保留高熵令牌（top 10%、20%、50%），以及仅保留低熵令牌（bottom 80%）。
- **评估方式**：每个问题生成16个独立回答（temperature=1.0），报告平均准确率和平均响应长度。

## 4. 资源与算力

- **计算资源**：使用NVIDIA A100 80G GPU，每个实验配置8个节点，每个节点8张GPU，共64张GPU。
- **预估训练时间**：
  - 8B模型：每mini-batch约0.5~1.5小时（随响应长度增长）。
  - 14B模型：约0.8~2.2小时。
  - 32B模型：约1~3小时。
- 论文未给出完整训练轮次总时长，但提供了梯度步数等信息（如32B模型训练了约1400步）。由于具体超参数已公开，实验可复现。

## 5. 实验数量与充分性

- **主要实验**：在三个模型规模（Qwen3-8B/14B/32B）上进行RLVR对比，涵盖6个基准数据集，并报告了16次评估的平均值，统计结果比较可靠。
- **消融实验**：
  - 改变保留比例 \(\rho\)（10%、20%、50%、100%（全量）、bottom 80%）。
  - 分析熵的变化趋势（Figure 6）。
  - 跨领域泛化测试（LiveCodeBench，Figure 9）。
  - 增大最大输出长度（从20480增加到29696）的额外实验。
  - 在非Qwen模型（Llama-3.1-8B）上进行了验证（但性能较低，附注说明）。
- **充分性评价**：实验较为充分，验证了高熵令牌驱动性能提升的核心结论，消融实验覆盖了关键变量（比例、模型大小、领域、温度调节等），评估指标（Acc@16）稳健。不足之处在于仅基于数学推理训练数据，且模型仅为Qwen系列为主，Llama实验性能较低且需冷启动SFT，泛化性论证不够强。但整体可支撑主要结论。

## 6. 论文的主要结论与发现

- **发现1（熵模式）**：CoT中约80%的令牌熵极低（<10⁻²），约20%的令牌熵较高（>0.672）。高熵令牌多为逻辑连接词、假设词等，充当“分叉点”；低熵令牌为语法后缀、数学表达式等确定性内容。
- **发现2（熵调节实验）**：提高高熵令牌的解码温度会提升推理性能，降低则会显著降低性能；而低熵令牌的温度变化影响较小。验证了高熵令牌作为分叉点需维持高熵。
- **发现3（RLVR动态）**：RLVR训练基本保留基座模型的熵模式，主要调整高熵令牌的熵值，低熵令牌变化极小。
- **发现4（仅高熵令牌训练）**：保留top 20%高熵令牌的梯度，在8B模型上性能与全量相当；在14B和32B模型上显著超越全量（如32B在AIME'25提升11.04分，AIME'24提升7.71分）。仅用低熵80%令牌则性能严重下降。
- **发现5（比例最优）**：保留20%高熵令牌效果最佳（平衡探索与稳定性），偏离此比例（10%或50%/100%）会导致整体熵下降，性能受损。
- **发现6（规模扩展）**：策略优势随模型规模增大而增强（32B > 14B > 8B），表明更大模型能更好利用高熵令牌的探索能力。
- **发现7（泛化性）**：在LiveCodeBench代码任务上，仅用top 20%高熵令牌仍显著优于全量DAPO，表明泛化能力增强。

## 7. 优点

- **视角新颖**：首次系统地从令牌熵角度阐释RLVR机制，揭示了不同令牌的功能差异，为理解强化学习在LLM推理中的作用提供了新框架。
- **方法简洁有效**：提出的“仅更新高熵令牌梯度”方法简单易行，无需额外模型或复杂设计，却能在大模型上取得显著性能提升（甚至超越全量），且训练更高效（计算量降至20%）。
- **实验设计全面**：在多模型规模（8B/14B/32B）、多基准（数学+代码）、多种消融设置（不同比例、温度调节、长短上下文）下验证，结论稳健。
- **结果具有突破性**：32B模型在AIME'24达到63.5（SoTA < 600B参数模型），扩展到更长上下文后达68.1，显示出强大潜力。
- **理论与应用结合**：不仅揭示了机制，还直接提出可应用的训练优化策略，启发未来算法设计。

## 8. 不足与局限

- **模型与任务覆盖有限**：主要基于Qwen系列模型，仅在Llama-3.1-8B上做了较弱验证（性能极低）；仅专注于数学推理任务（DAPO-Math-17K训练集），虽在代码任务上测试了泛化，但缺乏编程专用训练数据。结论能否推广到其他类型推理（如科学、常识推理）尚待验证。
- **实验统计 rigor 不足**：未提供误差棒或多次重复实验的结果（受限于计算资源），可能引入随机性影响。虽然每个问题采样16次取平均，但整体训练过程未进行多次独立重复。
- **对超参数敏感性的分析不够**：主要设定 \(\rho=20\%\)，但未系统探索不同\(\rho\)值在其他模型或数据集上的最优选择，作者也承认不同设置下最优值可能不同。
- **对低熵令牌作用的解释不够深入**：实验表明低熵令牌贡献微弱甚至有害，但并未详细分析其原因（例如是否因为低熵令牌梯度信号微弱或噪声大）。
- **局限性的明确陈述**：论文在“Limitations”部分自述了实验无法扩展到其他模型族（如LLaMA有困难）、数据集仅限数学领域、以及关键比例可能需调整等，态度坦诚。
- **未提供开源代码**：论文声明代码将在后续开源，当前重复实验有一定门槛（尽管实验细节描述较充分）。

（完）
