---
title: Demystifying Long Chain-of-Thought Reasoning
title_zh: 揭秘长链式推理
authors: "Shiming Yang, Yuxuan Tong, Xinyao Niu, Graham Neubig, Xiang Yue"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=OLodUbcWjB"
tags: ["query:key-tokens"]
score: 7.0
evidence: 研究长链式推理的机制
tldr: 针对大型语言模型中的长链式推理（CoT）机理尚不明确的问题，本文通过监督微调和强化学习实验，系统研究了长CoT推理的关键因素，发现了三个重要结论，为理解和训练长CoT推理提供了指导。
source: ICML-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2025-olodubcwjb/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1774, \"height\": 453, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-olodubcwjb/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1767, \"height\": 387, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-olodubcwjb/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 851, \"height\": 374, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-olodubcwjb/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 852, \"height\": 377, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-olodubcwjb/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1773, \"height\": 444, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-olodubcwjb/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1776, \"height\": 474, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-olodubcwjb/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1777, \"height\": 430, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-olodubcwjb/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1773, \"height\": 440, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-olodubcwjb/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1735, \"height\": 382, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-olodubcwjb/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 973, \"height\": 540, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-olodubcwjb/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 874, \"height\": 456, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-olodubcwjb/fig-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 887, \"height\": 538, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-olodubcwjb/fig-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 885, \"height\": 568, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-olodubcwjb/fig-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 1326, \"height\": 578, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-olodubcwjb/fig-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 1749, \"height\": 992, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-icml-2025-olodubcwjb/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 862, \"height\": 298, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-olodubcwjb/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 864, \"height\": 347, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-olodubcwjb/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 858, \"height\": 325, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-olodubcwjb/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 853, \"height\": 282, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-olodubcwjb/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 857, \"height\": 338, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-olodubcwjb/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 880, \"height\": 442, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-olodubcwjb/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 672, \"height\": 132, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-olodubcwjb/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1697, \"height\": 264, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-olodubcwjb/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1710, \"height\": 1076, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-olodubcwjb/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1856, \"height\": 1319, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-olodubcwjb/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1687, \"height\": 1113, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-olodubcwjb/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1687, \"height\": 1113, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-olodubcwjb/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1684, \"height\": 659, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-olodubcwjb/table-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 1701, \"height\": 2184, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-olodubcwjb/table-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 1779, \"height\": 1411, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-olodubcwjb/table-016.webp\", \"caption\": \"\", \"page\": 0, \"index\": 16, \"width\": 1703, \"height\": 172, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-olodubcwjb/table-017.webp\", \"caption\": \"\", \"page\": 0, \"index\": 17, \"width\": 1465, \"height\": 1228, \"label\": \"Table\"}]"
motivation: 长CoT推理的涌现条件和训练设计选择尚不清楚。
method: 通过大量SFT和RL实验，系统分析长CoT推理的机制。
result: 识别出三个关键发现，阐明长CoT推理的涌现条件。
conclusion: 揭示了长CoT推理的内部机制，为RL训练提供指导。
---

## Abstract
Scaling inference compute has become a key driver of advanced reasoning in large language models (LLMs). A proven approach for scaling inference compute is to generate long chains-of-thought (CoTs), enabling models to engage in structured reasoning strategies such as backtracking and error correction. Reinforcement learning (RL) has emerged as a crucial method for developing these capabilities, yet the conditions under which long CoTs emerge remain unclear, and RL training requires careful design choices. In this study, we systematically investigate the underlying *mechanics of long CoT reasoning*—examining the factors that enable models to generate extended reasoning trajectories. Through extensive supervised fine-tuning (SFT) and RL experiments, we identify three key findings: 1) while SFT is not strictly necessary, it significantly simplifies training and improves efficiency; 2) reasoning capabilities tend to emerge with increased training compute but are not guaranteed, making reward shaping essential for stabilizing CoT length growth; and 3) scaling verifiable reward signals is critical for RL, and we find that leveraging noisy, web-extracted solutions with filtering mechanisms shows promising potential, particularly in out-of-distribution (OOD) reasoning tasks such as STEM problem-solving. These insights provide practical guidance for optimizing training strategies to enhance long CoT reasoning in LLMs.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义（研究动机和背景）
- **核心问题**：尽管通过强化学习（RL）训练大型语言模型（LLMs）生成长链式推理（long CoT）已取得进展，但长CoT的涌现条件仍不明确，且RL训练存在诸多设计选择上的不确定性。
- **研究背景**：长CoT通过回溯、错误修正等结构化策略提升模型在复杂推理任务（如数学竞赛、博士级科学问题）上的表现。先前工作主要依赖可验证奖励稳定RL，但缺乏对长CoT学习机制的系统理解。

### 2. 论文提出的方法论：核心思想、关键技术细节、公式或算法流程
- **核心思想**：通过监督微调（SFT）和强化学习（RL）实验，系统探究影响长CoT生成的关键因素，并针对训练不稳定性提出优化策略。
- **关键技术细节**：
  - **模型初始化**：基于Llama-3.1-8B和Qwen2.5-7B-Math，长CoT数据通过从QwQ-32B-Preview蒸馏收集（拒绝采样），短CoT数据从Qwen2.5-Math-72B-Instruct蒸馏。
  - **SFT模式**：对比长CoT与短CoT作为初始化，发现长CoT SFT显著提升性能上限并便于后续RL改进。
  - **RL奖励设计**：提出**余弦长度缩放奖励（Cosine Reward）**，公式为：
    \[
    \text{CosFn}(t, T, \eta_{\min}, \eta_{\max}) = \eta_{\min} + \frac12(\eta_{\max} - \eta_{\min})\left(1 + \cos\left(\frac{t\pi}{T}\right)\right)
    \]
    该奖励随生成长度平滑变化：正确回答短者获更高奖励，错误回答短者受更重惩罚，额外设超出长度惩罚\(r_e\)。
  - **重复惩罚**：为抑制长度奖励黑客行为，引入N-gram重复惩罚，在重复出现的n-gram上逐token施加负奖励，并使用低折扣因子使其聚焦局部。
  - **多折扣因子GAE**：修改PPO的GAE公式，为正确性奖励和重复惩罚分别设置不同折扣因子\(\gamma_c\)和\(\gamma_p\)，以平衡长期规划与局部反馈。

### 3. 实验设计：数据集、基准、对比方法
- **数据集与基准**：
  - **MATH-500**：数学领域内（in-domain）基准。
  - **AIME 2024**：数学域外（out-of-domain）基准。
  - **TheoremQA**：STEM域外基准。
  - **MMLU-Pro-1k**：通用推理域外基准。
  - **训练数据**：主要使用MATH训练集（7500样本），另引入WebInstruct-462k（含噪声的网页提取问答）以扩展可验证信号。
- **对比方法**：
  - **SFT阶段**：长CoT vs 短CoT；构造式长CoT（基于动作提示框架） vs 蒸馏式长CoT（来自QwQ-32B-Preview）。
  - **RL阶段**：经典奖励（正确+1，错误0） vs 余弦长度缩放奖励；有无重复惩罚；不同折扣因子组合；不同上下文窗口大小（4K/8K/16K）；不同模型规模（1.5B/8B/32B）。
  - **验证器**：规则基验证器（基于标准答案） vs 模型基验证器（Qwen2.5-7B-Instruct作为评判员）。
  - **数据噪声**：纯MATH、纯WebInstruct（无过滤）、两者混合、过滤后数据。

### 4. 资源与算力
- 论文未明确报告使用的GPU型号、数量及具体训练时长。仅在§6.1提到，受限于开源RL框架（OpenRLHF）的低硬件利用率和同步顺序执行，未能成功在32B模型上进行大规模实验（所需GPU数量过大）。实验主要基于8B和7B模型，推测使用普通商用GPU（如A100或类似），但无精确数据。

### 5. 实验数量与充分性
- **实验组数**：较为丰富，涵盖：
  - SFT缩放（4种N：32/64/128/256/192等）
  - SFT+RL联合实验（4个基准、多种初始化）
  - 奖励设计对比（经典 vs 余弦，含重复惩罚消融）
  - 折扣因子消融（表6有6种组合）
  - 上下文窗口大小消融（3种）
  - 模型规模消融（1.5B/8B/32B）
  - 噪声数据实验（表3-5，含不同验证器和过滤策略）
  - REINFORCE与PPO对比（仅初步）
- **充分性**：实验设计较全面，控制变量清晰，涵盖主要影响因素。但作者也指出REINFORCE更不稳定且未充分调优，32B实验受限，部分超参数（如学习率、KL系数）未大规模探索。总体对长CoT训练提供了有力消融证据，但通用性仍需更多领域的验证。

### 6. 论文的主要结论与发现
- **SFT关键性**：长CoT SFT并非必须，但能显著简化训练并提升后续RL效果；长CoT SFT的性能上限远高于短CoT，且更易通过RL进一步改进。
- **奖励塑形稳定长度**：余弦长度缩放奖励能稳定COt长度增长，避免早期上下文窗口溢出，同时提升准确率；重复惩罚可缓解长度奖励黑客行为（如重复内容）。
- **可验证奖励扩展**：引入网络级噪声数据（WebInstruct）结合过滤，在域外STEM任务上取得显著提升；模型基验证器在未过滤数据上表现更好，规则基验证器在过滤后更优。
- **模型大小无关性**：余弦奖励在1.5B、8B、32B规模下均能稳定长度并改善性能。
- **折扣因子设计**：正确性奖励需高折扣因子（鼓励长期规划），重复惩罚需低折扣因子（提供局部反馈）；错误组合（如正确性折扣过低）会降低分支探索和最终性能。

### 7. 优点
- **系统性**：首次全面拆解长CoT训练中SFT、奖励设计、数据扩展、模型规模等因素的影响，提供可操作的工程指导。
- **奖励函数创新**：余弦长度缩放奖励简洁且有效，平滑处理长度与正确性的矛盾，易于调参。
- **噪声数据利用**：展示如何通过过滤和混合策略，利用大规模网络数据弥补人工标注可验证数据的不足，具有现实应用价值。
- **实验透明度**：公开代码，详细记录超参数和实验设置，便于复现和扩展。

### 8. 不足与局限
- **领域局限性**：实验主要基于数学推理（MATH、AIME、TheoremQA中的数学部分），对常识推理、规划等领域的泛化性未验证。
- **基础设施限制**：未能在32B模型上完成完整RL实验，REINFORCE算法调优不充分，可能错过更高效方案。
- **重复惩罚副作用**：惩罚重复可能抑制有益的自我修正或分步探索，论文未深入分析其长期影响。
- **超参数敏感性**：余弦奖励的参数（\(r_c^0, r_c^L, r_w^0, r_w^L\)）及折扣因子需仔细调整，未提供自动化调优方法。
- **数据偏差**：WebInstruct数据的过滤过程（基于短形式答案）可能丢弃正确答案，且模型基验证器易被欺骗，论文仅初步对比，未全面评估噪声影响。
- **计算资源报告缺失**：未披露训练所需GPU类型、数量、时长，影响可重复性和成本评估。

（完）
