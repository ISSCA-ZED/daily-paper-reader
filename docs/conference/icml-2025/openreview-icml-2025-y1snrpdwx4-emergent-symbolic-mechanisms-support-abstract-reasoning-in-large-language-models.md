---
title: Emergent Symbolic Mechanisms Support Abstract Reasoning in Large Language Models
title_zh: 涌现符号机制支撑大语言模型中的抽象推理
authors: "Yukang Yang, Declan Iain Campbell, Kaixuan Huang, Mengdi Wang, Jonathan D. Cohen, Taylor Whittington Webb"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=y1SnRPDWx4"
tags: ["query:key-tokens"]
score: 7.0
evidence: 涌现的符号机制将token转化为抽象变量，识别关键token的角色
tldr: 本文揭示了大语言模型中支持抽象推理的涌现符号架构。早期层中的符号抽象头根据token间关系将输入token转换为抽象变量，中间层进行序列归纳，后期层执行检索。该工作揭示了推理过程中token如何被转化为抽象符号，对理解关键token的因果作用有启示。
source: ICML-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2025-y1snrpdwx4/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1326, \"height\": 697, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-y1snrpdwx4/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1641, \"height\": 1019, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-y1snrpdwx4/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1658, \"height\": 918, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-y1snrpdwx4/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1680, \"height\": 1006, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-y1snrpdwx4/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1424, \"height\": 1587, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-y1snrpdwx4/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1421, \"height\": 1587, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-y1snrpdwx4/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1420, \"height\": 1585, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-y1snrpdwx4/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1677, \"height\": 584, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-y1snrpdwx4/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1170, \"height\": 618, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-y1snrpdwx4/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1178, \"height\": 1238, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-y1snrpdwx4/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1726, \"height\": 871, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-y1snrpdwx4/fig-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1728, \"height\": 872, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-y1snrpdwx4/fig-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1471, \"height\": 959, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-y1snrpdwx4/fig-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 1471, \"height\": 965, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-y1snrpdwx4/fig-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 1678, \"height\": 503, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-y1snrpdwx4/fig-016.webp\", \"caption\": \"\", \"page\": 0, \"index\": 16, \"width\": 1288, \"height\": 618, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-y1snrpdwx4/fig-017.webp\", \"caption\": \"\", \"page\": 0, \"index\": 17, \"width\": 1463, \"height\": 706, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-y1snrpdwx4/fig-018.webp\", \"caption\": \"\", \"page\": 0, \"index\": 18, \"width\": 1738, \"height\": 2172, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-y1snrpdwx4/fig-019.webp\", \"caption\": \"\", \"page\": 0, \"index\": 19, \"width\": 1170, \"height\": 2177, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-y1snrpdwx4/fig-020.webp\", \"caption\": \"\", \"page\": 0, \"index\": 20, \"width\": 1738, \"height\": 1619, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-y1snrpdwx4/fig-021.webp\", \"caption\": \"\", \"page\": 0, \"index\": 21, \"width\": 1735, \"height\": 2173, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-y1snrpdwx4/fig-022.webp\", \"caption\": \"\", \"page\": 0, \"index\": 22, \"width\": 1741, \"height\": 1076, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-y1snrpdwx4/fig-023.webp\", \"caption\": \"\", \"page\": 0, \"index\": 23, \"width\": 1824, \"height\": 560, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-y1snrpdwx4/fig-024.webp\", \"caption\": \"\", \"page\": 0, \"index\": 24, \"width\": 1751, \"height\": 1074, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-y1snrpdwx4/fig-025.webp\", \"caption\": \"\", \"page\": 0, \"index\": 25, \"width\": 1287, \"height\": 571, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-icml-2025-y1snrpdwx4/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1421, \"height\": 169, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-y1snrpdwx4/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1252, \"height\": 292, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-y1snrpdwx4/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 979, \"height\": 164, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-y1snrpdwx4/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 810, \"height\": 746, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-y1snrpdwx4/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 621, \"height\": 216, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-y1snrpdwx4/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 796, \"height\": 202, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-y1snrpdwx4/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 894, \"height\": 115, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-y1snrpdwx4/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 885, \"height\": 166, \"label\": \"Table\"}]"
motivation: 为了探究大语言模型抽象推理的内部机制，特别是是否依赖结构化推理。
method: 通过分析模型内部注意力头和MLP的行为，识别出符号抽象头、符号归纳头和检索头三类计算单元。
result: 发现这些符号机制在多个抽象推理任务中涌现，且其功能与推理正确性相关。
conclusion: 表明LLM的推理能力依赖于符号化处理，为理解关键token的抽象化提供了新视角。
---

## Abstract
Many recent studies have found evidence for emergent reasoning capabilities in large language models (LLMs), but debate persists concerning the robustness of these capabilities, and the extent to which they depend on structured reasoning mechanisms. To shed light on these issues, we study the internal mechanisms that support abstract reasoning in LLMs. We identify an emergent symbolic architecture that implements abstract reasoning via a series of three computations. In early layers, *symbol abstraction heads* convert input tokens to abstract variables based on the relations between those tokens. In intermediate layers, *symbolic induction heads* perform sequence induction over these abstract variables. Finally, in later layers, *retrieval heads* predict the next token by retrieving the value associated with the predicted abstract variable. These results point toward a resolution of the longstanding debate between symbolic and neural network approaches, suggesting that emergent reasoning in neural networks depends on the emergence of symbolic mechanisms.

---

## 论文详细总结（自动生成）

# Emergent Symbolic Mechanisms Support Abstract Reasoning in Large Language Models — 详细中文总结

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **研究动机**：大语言模型（LLM）在多种推理任务中展现出令人瞩目的能力，但其是否真正具备结构化、类人的抽象推理能力，还是仅仅依赖统计近似，学术界存在激烈争论。
- **核心问题**：LLM 内部的何种机制支撑了抽象推理？这些机制是否具有符号处理的特性（如变量不变性、间接引用）？
- **整体含义**：论文旨在揭示 LLM 中涌现的符号机制，说明神经网络可以通过学习自身发展出类似符号系统的计算结构，从而为符号主义与连接主义的长期争论提供一种可能的调和方案。研究工作表明，LLM 的推理能力并非简单的“随机鹦鹉”式模仿，而是依赖于高度结构化的符号处理过程。

## 2. 论文提出的方法论：核心思想、关键技术细节、流程

### 核心思想
- 论文识别出一个**三阶段涌现符号架构**：
  1. **符号抽象头（Symbol Abstraction Heads）**：位于早期层，根据 token 之间的关系将输入 token 转换为抽象变量（符号）。
  2. **符号归纳头（Symbolic Induction Heads）**：位于中间层，在抽象变量序列上进行序列归纳，预测下一个抽象变量。
  3. **检索头（Retrieval Heads）**：位于后期层，根据预测的抽象变量检索对应的 token 值，完成最终预测。

### 关键技术细节
- **符号抽象头**：实现了一种涌现的关系注意力机制。键（key）和查询（query）编码 token，值（value）编码 token 在实例中的相对位置，使得输出仅反映关系模式而与 token 身份无关，从而得到抽象变量表示。
- **符号归纳头**：不同于标准的归纳头（基于字面 token 的 bigram 统计），符号归纳头在抽象变量序列上进行归纳。通过分析发现，这些头的查询和键主要编码 token 在实例内的相对位置，值则编码抽象变量。
- **检索头**：执行间接引用（indirection）——用抽象变量作为指针，检索与其关联的具体 token 值。
- **因果中介分析（Causal Mediation Analysis, CMA）**：设计两种条件（抽象变量中介分析 & token 中介分析），通过激活替换（activation patching）分离出对抽象变量 vs 具体 token 有因果作用的注意力头。
- **表征相似性分析（RSA）**：比较注意力头输出/键/查询/值的相似性矩阵与假设的抽象变量相似性矩阵或 token 相似性矩阵，验证各头的功能角色。

### 算法/流程简述
- 给定一对上下文 (c1, c2) 和预训练语言模型 f，计算因果中介得分 s = [f(c*_1)[y_{c*_1}] – f(c*_1)[y_{c1}]] – [f(c1)[y_{c*_1}] – f(c1)[y_{c1}]]。其中 c*_1 表示将从 c2 的指定层/位置/头的激活值替换到 c1 后的上下文。通过在不同位置（每个实例的第三项、序列最后位置）进行替换，分别定位三类头。
- **解码分析**：训练线性分类器从符号抽象头和符号归纳头的输出中解码抽象变量（A vs B），测试集使用完全不同的 token 集，验证表示的跨 token 不变性。

## 3. 实验设计

### 数据集/场景
- **主要任务**：代数规则归纳任务（Identity Rules Task），涉及 ABA 或 ABB 两类规则，每个问题提供 2-shot 示例，token 随机采样自模型词表，保证示例内无重复 token。
- **补充任务**：
  - 字母串类比任务（Letter String Analogies），涉及 successor 或 predecessor 关系。
  - 词汇类比任务（Verbal Analogies），涉及 synonym 或 antonym 关系。
- 所有任务均设计为可构建“相同 token 但不同规则”的上下文对，从而支持因果中介分析的解构设计。

### Benchmark
- 主要评估指标：2-shot 准确率（代数规则归纳任务为 95%，字母串类比为 99.2%/82.0%，词汇类比为 77.0%/88.4%）。
- 使用因果中介得分衡量各注意力头的因果作用。
- 消融实验测量概率下降曲线。
- 与标准归纳头（prefix matching score）和函数向量（average indirect effect）进行对比。

### 对比的方法/模型
- **模型家族**：GPT-2 (124M, 335M, 774M, 1.5B)、Gemma-2 (2B, 9B, 27B)、Qwen2.5 (7B, 14B, 32B, 72B)、Llama-3.1 (8B, 70B)，共 13 个模型。
- **内部对比**：符号抽象头、符号归纳头、检索头三阶段架构 vs 随机头/对照组（替换为同层最低得分头）。
- **机制对比**：符号归纳头 vs 标准归纳头（prefix matching score），符号归纳头 vs 函数向量头（average indirect effect）。

## 4. 资源与算力

- **硬件**：Llama-3.1 70B 和 Qwen2.5 72B 实验在 2× NVIDIA 80G H100 GPU 上进行；其他较小模型在单张 H100 GPU 上运行。
- **格式**：所有模型权重以 bfloat16 加载。
- **训练时长**：论文未报告具体的训练时长或实验总 GPU 小时数，仅描述了推理和分析所需硬件配置。

## 5. 实验数量与充分性

### 实验数量
- 主要任务（代数规则归纳）：对 13 个模型在多种 shot 数（1-10）下测试准确率，每个模型在每个规则下使用 500 个 prompt。
- 因果中介分析：每个任务（抽象/ token 中介）使用 200 个 prompt（100 对 × 两个方向）。
- 注意力分析：对每个 head 平均 1378 个 ABA 和 ABB prompt。
- 表征相似性分析：40 组 token 集。
- 消融实验：40 个非重叠 prompt，逐步消融 top h 个头。
- 解码分析：训练 200 prompt，验证 100，测试 200（测试集 token 完全未见）。
- 字母串/词汇类比任务：各 100 对 prompt（两个方向）。
- 统计分析：排列检验（5000 次重复）控制 family-wise error rate p<0.05。

### 充分性与客观性
- **充分**：研究覆盖三个不同复杂度的推理任务，跨四个模型家族、多个规模，且三类机制均经过因果、表征、注意力的多角度验证。
- **公平**：采用双重分离设计（抽象 vs token 中介）避免混淆；消融实验设对照（替换为最低得分头）和随机基线；与标准归纳头、函数向量对比阐明独特性。
- **客观**：所有统计结果基于严格排列检验，仅展示显著的头。

## 6. 论文的主要结论与发现

- LLM 在执行抽象推理时，其内部涌现出一套**三阶段符号处理架构**：早期层符号抽象头将 token 转化为抽象变量，中间层符号归纳头在变量序列上归纳规则，后期层检索头将预测的变量检索为具体 token。
- 这套机制在 Llama-3.1、Gemma-2、Qwen2.5 中均被发现，但在 GPT-2 家族中不明显（GPT-2 在任务上表现差，且缺乏符号抽象头）。
- 符号归纳头与标准归纳头（基于 token 的 bigram 匹配）**几乎不重叠**，但**与函数向量高相关**（r=0.86），表明函数向量本质上可视为符号归纳的产物。
- 符号抽象头在实例层面编码关系信息，符号归纳头将其跨实例聚合，形成对任务规则的抽象表示。
- 在复杂任务（字母串、词汇类比）中同样存在类似的三阶段机制，尽管头部的特异性有所分化。
- 解码分析证明：符号抽象头和符号归纳头的输出中包含一个**对 token 身份不变的子空间**，能够泛化到全新 token 集上识别抽象变量（测试准确率 >98%）。

## 7. 优点

- **方法创新**：首次系统性地将因果中介分析与表征相似性分析结合，精确定位了三种功能不同的注意力头，并揭示了它们之间的交互架构。
- **设计精巧**：通过“相同 token 不同规则”的上下文对实现抽象与 token 的双重解离，使因果推断具有强可解释性。
- **跨模型/任务验证**：覆盖多种模型家族和三个不同复杂度的任务，结论具有较好的泛化性。
- **机制性深度**：不仅识别了头部功能，还通过 RSA 分析了键、查询、值的语义内容；并通过解码分析验证抽象表示的不变性，提供了机制层面的直接证据。
- **理论贡献**：为“LLM 是否具备真正推理能力”的争论提供了有力的内部机制证据，并沟通了符号主义与连接主义。

## 8. 不足与局限

- **实验覆盖**：主要测试的任务集中在简单的规则归纳和类比类比上，未涉及更复杂的组合推理、数学推理或规划任务，结论的外推性需要进一步验证。
- **模型范围**：虽然测试了 13 个模型，但所有模型均为公开的英文预训练模型，未包括非英文模型或近期更大规模的模型（如 GPT-4、Claude），且 GPT-2 系列表现较差，表明该架构可能只在特定规模/训练数据量下涌现。
- **机制精确性**：论文指出抽象表示并非完全纯净，头部输出中仍保留部分 token 信息，说明符号处理是近似而非完美的——但该“不纯性”是否与人类认知中的内容效应一致有待探讨。
- **因果中介的局限性**：激活替换仅扰动特定位置，无法完全排除跨层交互的复杂非线性影响；且中介分析仅验证了“充分性”和“必要性”（通过消融），但未揭示所有协同工作机制。
- **应用限制**：研究主要聚焦于分析现有模型，未提出改进训练或架构的方法，实际应用价值尚不明确。
- **能耗与可复现性**：未详细报告总 GPU 小时数或完整代码库链接（仅宣称将开源），对复现和能耗评估造成一定障碍。

（完）
