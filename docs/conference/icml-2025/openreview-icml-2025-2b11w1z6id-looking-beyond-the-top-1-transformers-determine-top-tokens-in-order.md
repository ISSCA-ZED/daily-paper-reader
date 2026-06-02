---
title: "Looking Beyond the Top-1: Transformers Determine Top Tokens in Order"
title_zh: 超越Top-1：Transformer按顺序决定Top token
authors: "Daria Lioubashevski, Tomer M. Schlank, Gabriel Stanovsky, Ariel Goldstein"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=2B11W1Z6ID"
tags: ["query:key-tokens"]
score: 6.0
evidence: 分析Transformer如何依次决定top token，与推理中token重要性相关
tldr: "本文揭示Transformer在预测中按顺序决定top-k token，存在\"饱和事件\"。该发现适用于语言、视觉和语音模型，表明token重要性具有层次结构。为理解推理中的token优先级提供了新视角。"
source: ICML-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2025-2b11w1z6id/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1141, \"height\": 839, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-2b11w1z6id/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1411, \"height\": 796, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-2b11w1z6id/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1177, \"height\": 1015, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-2b11w1z6id/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 636, \"height\": 719, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-2b11w1z6id/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1606, \"height\": 632, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-2b11w1z6id/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 886, \"height\": 657, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-2b11w1z6id/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1748, \"height\": 512, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-2b11w1z6id/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 885, \"height\": 689, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-2b11w1z6id/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 886, \"height\": 690, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-2b11w1z6id/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1762, \"height\": 673, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-2b11w1z6id/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 875, \"height\": 669, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-icml-2025-2b11w1z6id/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 869, \"height\": 280, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-2b11w1z6id/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 869, \"height\": 209, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-2b11w1z6id/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 891, \"height\": 295, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-2b11w1z6id/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 413, \"height\": 314, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-2b11w1z6id/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1070, \"height\": 498, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-2b11w1z6id/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1116, \"height\": 385, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-2b11w1z6id/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1069, \"height\": 555, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-2b11w1z6id/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1416, \"height\": 304, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-2b11w1z6id/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1417, \"height\": 302, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-2b11w1z6id/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1594, \"height\": 282, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-2b11w1z6id/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1241, \"height\": 304, \"label\": \"Table\"}]"
motivation: 理解Transformer在输出固定后内部仍然进行的计算。
method: 分析饱和事件，扩展至top-k token的顺序决策。
result: 发现token按排名顺序被依次决定，且普遍存在。
conclusion: token决策顺序是Transformer的内在属性，可用于解释推理过程。
---

## Abstract
Uncovering the inner mechanisms of Transformer models offers insights into how they process and represent information. In this work, we analyze the computation performed by Transformers in the layers after the top-1 prediction remains fixed, known as the “saturation event”. We expand this concept to top-k tokens, demonstrating that similar saturation events occur across language, vision, and speech models. We find that these events occur in order of the corresponding tokens’ ranking, i.e., the model first decides on the top ranking token, then the second highest ranking token, and so on. This phenomenon seems intrinsic to the Transformer architecture, occurring across different variants, and even in untrained Transformers. We propose that these events reflect task transitions, where determining each token corresponds to a discrete task. We show that it is possible to predict the current task from hidden layer embedding, and demonstrate that we can cause the model to switch to the next task via intervention. Leveraging our findings, we introduce a token-level early-exit strategy, surpassing existing methods in balancing performance and efficiency and show how to exploit saturation events for better language modeling.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **核心问题**：Transformer模型在做出top-1预测后，后续层仍然执行大量计算，但这些计算的目的尚不明确。论文旨在理解模型在“饱和事件”（saturation event）之后究竟在做什么。
- **背景**：先前工作（Geva et al., 2022）发现，模型在早期层就确定了top-1 token并在后续层保持固定，即饱和事件。本文将此概念扩展至top-k token，并揭示模型是按排名顺序依次决定这些token的。
- **研究意义**：揭示Transformer内部计算机制，为模型可解释性提供跨模态的普适框架，并探索实际应用（如早期退出、改善语言建模）。

## 2. 论文提出的方法论：核心思想、关键技术细节

- **核心思想**：将饱和事件从top-1扩展到top-k，提出“任务转换”（task-transition）机制：模型将决定每个排名位置的token视为一个独立任务，按顺序执行，即先决定第1名token，再决定第2名，依此类推。任务切换发生在对应的饱和层。
- **关键技术细节**：
  - **定义k-th饱和层**：对于第k个排名token，其身份在后续所有层中保持不变的最早层l_k。
  - **有序性度量**：使用严格Kendall's τ系数衡量token排名与饱和层排名之间的对齐程度，将并列视为不一致。
  - **任务探测实验**：训练逻辑回归分类器，从隐藏层嵌入中预测当前正在执行的任务编号（1~5）。通过对比随机嵌入的基线，验证任务信息是否编码在表示中。
  - **因果干预实验**：将样本s1的饱和层激活注入到样本s2的后续层中，观察能否触发s2提前进入任务2，以此验证饱和层包含“切换信号”。
  - **领域适应性**：对文本、视觉、语音模型分别使用logit lens或类logit lens投影到对应输出空间。

## 3. 实验设计：数据集/场景、基准、对比方法

- **文本模型**：Llama3-8B, GPT2-XL, Mistral-7B, Falcon-7B；数据集MMLU（1K随机问题，约60K-100K tokens）。
- **视觉模型**：ViT-L/16（ImageNet预训练+微调）；数据集CIFAR-10（5K随机图像）。
- **语音模型**：Whisper-large；数据集LibriSpeech（5K随机音频）。
- **多模态扩展**：LLaVa-1.5-7B（MMMU视觉问答），Qwen-Audio（LibriSpeech）。
- **基准对比（早期退出）**：与softmax响应和隐藏状态饱和两种置信度方法比较，评估准确率和加速比。
- **语言建模改进实验**：在top-1预测错误时，比较第2/3/4名token在达到饱和（提前i层）与未饱和时的预测准确率。

## 4. 资源与算力

- 论文未明确说明使用的GPU型号、数量或训练时长。仅提及使用了量化模型（8-bit quantized）以减少资源消耗。实验规模较小（如1K-5K样本），推断所需算力不高，但未提供具体硬件信息。

## 5. 实验数量与充分性

- **实验数量**：覆盖4种文本LLM、1种视觉ViT、1种语音Whisper、2种多模态模型（LLaVa, Qwen-Audio），以及随机初始化Llama3-8B。每个模态均进行了有序性验证、任务探测、因果干预等主要实验。早期退出实验使用CNN/DM数据集（100文本）。
- **充分性**：实验设计较全面，跨模态、跨架构、带控制条件（随机初始化、随机嵌入对比）。但也存在不足：各模型使用相同实验范式，但语音模型仅观察到前3个token有序，作者给出了合理猜测但缺乏更多验证；视觉模型仅用CIFAR-10（较简单），未在ImageNet上直接测试；消融实验未对架构组件（如注意力层、FFN）进行系统分析。
- **客观性**：统计显著性检验（t检验、Kendall's τ置换检验、二项检验）增强了结果可靠性。基线方法公平比较，但早期退出实验仅用静态传播近似，未完全模拟动态解码的实际开销。

## 6. 论文的主要结论与发现

- **主要发现1**：Transformer模型在决定top-k token时严格按排名顺序，第1名先饱和，第2名次之，以此类推。该现象在语言、视觉、语音模型中普遍存在，甚至在随机初始化的未训练模型中也出现（前3名）。
- **主要发现2**：该现象可由“任务转换”机制解释：每个排名对应一个独立任务，信息编码在隐藏层嵌入中，可通过简单分类器预测任务编号。因果干预证实饱和层包含触发任务切换的信号。
- **主要发现3**：基于任务探测的早期退出策略在准确率-加速权衡上优于现有方法（softmax响应、状态饱和度）。此外，top-k token达到饱和时（尤其是top-1错误时）比未饱和时更准确，可用于改进解码。

## 7. 优点

- **创新性**：首次系统揭示top-k token有序饱和现象，并提出任务转换机制，超越了仅关注top-1的传统视角。
- **跨模态普适性**：验证了文本、视觉、语音多个模态，表明该现象是Transformer架构的内在特性，而非特定领域 artifact。
- **方法论严谨**：结合观察性分析（有序性度量）、表征探测（任务分类）和因果干预（激活注入），形成完整证据链。控制实验（随机初始化、随机嵌入）排除了数据偏差。
- **实用价值**：提出了可直接应用的早期退出策略和语言建模改进思路，结果具有实际潜力。

## 8. 不足与局限

- **实验覆盖有限**：
  - 视觉模型仅用CIFAR-10，未在更复杂的ImageNet-1K上验证；语音模型仅用LibriSpeech，且仅观察到前3名有序，后几名退化。
  - 未测试更大规模模型（如Llama3-70B、GPT-4），也未覆盖编码器-解码器架构的编码器部分。
  - 早期退出实验仅在Llama3-8B上评估，未验证泛化性。
- **架构机制未充分解释**：
  - 未通过消融实验定位产生有序饱和的具体组件（如注意力、FFN、层归一化等）。
  - 未解释模型如何在饱和后保持token固定（如是否存在抑制机制）。
- **潜在偏差**：
  - 对MMLU等Benchmark的数据泄漏未控制；仅假设数据可能见过，未分析影响。
  - 语音模型中Whisper的退化仅归因于跨注意力，缺乏直接证据。
- **应用限制**：
  - 早期退出策略需额外训练分类器，且仅适用于token级，未在序列级验证。
  - 语言建模改进仅基于条件概率比较，未在实际生成任务中测试。

（完）
