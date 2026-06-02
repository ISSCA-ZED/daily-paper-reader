---
title: A Lens into Interpretable Transformer Mistakes via Semantic Dependency
title_zh: 透过语义依赖之镜理解可解释的Transformer错误
authors: "Ruo-Jing Dong, Yu Yao, Bo Han, Tongliang Liu"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=7v2loOdcLH"
tags: ["query:key-tokens"]
score: 4.0
evidence: 分析隐藏状态中token值随语义变化
tldr: 本文通过观察隐藏状态中token值的语义变化来研究Transformer中的语义依赖。发现大多数token在层间传播时保留原始语义，但错误答案往往源于特定token编码了错误的语义依赖。该分析直接涉及隐藏状态中关键token的检测，但侧重于错误归因而非推理序列。
source: ICML-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2025-7v2loodclh/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 775, \"height\": 278, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-7v2loodclh/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 776, \"height\": 225, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-7v2loodclh/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 784, \"height\": 487, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-7v2loodclh/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1784, \"height\": 545, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-7v2loodclh/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 846, \"height\": 1264, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-7v2loodclh/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 777, \"height\": 639, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-7v2loodclh/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1756, \"height\": 780, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-7v2loodclh/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1736, \"height\": 843, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-7v2loodclh/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1737, \"height\": 1289, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-7v2loodclh/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1736, \"height\": 842, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-7v2loodclh/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1738, \"height\": 1289, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-icml-2025-7v2loodclh/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 857, \"height\": 376, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-7v2loodclh/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 613, \"height\": 423, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-7v2loodclh/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 854, \"height\": 153, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-7v2loodclh/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1770, \"height\": 273, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-7v2loodclh/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1497, \"height\": 498, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-7v2loodclh/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1497, \"height\": 216, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-7v2loodclh/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1199, \"height\": 499, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-7v2loodclh/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1770, \"height\": 173, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-7v2loodclh/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1763, \"height\": 237, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-7v2loodclh/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 798, \"height\": 220, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-7v2loodclh/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1778, \"height\": 1732, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-7v2loodclh/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1514, \"height\": 2176, \"label\": \"Table\"}]"
motivation: 为了揭示Transformer模型在问答任务中出错的根本原因，特别是语义依赖层面的错误。
method: 分析token值在层间变化与语义变化的对应关系，识别错误token。
result: 发现模型答案错误常源于某些token编码了错误的语义依赖，且这些token在最终层保持错误信息。
conclusion: 提供了通过隐藏状态分析诊断模型错误的方法，对关键token识别有参考价值。
---

## Abstract
Semantic Dependency refers to the relationship between words in a sentence where the meaning of one word depends on another, which is important for natural language understanding.
In this paper, we investigate the role of semantic dependencies in answering questions for transformer models, which is achieved by analyzing how token values shift in response to changes in semantics.
Through extensive experiments on models including the BERT series, GPT, and LLaMA, we uncover the following key findings:
1). Most tokens primarily retain their original semantic information even as they propagate through multiple layers.
2). Models can encode truthful semantic dependencies in tokens in the final layer.
3). Mistakes in model answers often stem from specific tokens encoded with incorrect semantic dependencies. Furthermore, we found that addressing the incorrectness by directly adjusting parameters is challenging because the same parameters can encode both correct and incorrect semantic dependencies depending on the context.
Our findings provide insights into the causes of incorrect information generation in transformers and help the future development of robust and reliable models.

---

## 论文详细总结（自动生成）

# 论文中文总结

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **核心问题**：Transformer 模型（如 BERT、GPT、LLaMA）在自然语言任务中常产生错误，其内部机制尚不透明。本文旨在探究模型错误与**语义依赖（Semantic Dependency）** 编码之间的关联，即词与词之间含义上的依赖关系（如“红色苹果”中“红色”依赖于“苹果”）。
- **研究动机**：现有工作从对抗性扰动、训练数据偏差、解码错误等角度解释模型错误，但忽略了**模型内部如何表示和利用语义依赖**这一关键环节。作者认为，模型对语义依赖的错误编码（即错误地让某个 token 包含不应存在的语义信息）是导致输出错误的重要原因。
- **整体含义**：通过揭示 token 在层间传播时语义依赖的保留、编码与错误机制，为后续设计更鲁棒的 Transformer 架构提供理论依据和可解释性工具。

## 2. 论文提出的方法论：核心思想、关键技术细节、公式或算法流程

- **核心思想**：利用**令牌扰动（Token Perturbation）** 方法，将输入序列中的某个 token 替换为随机 token，观察最终层（第 L 层）各 token 表示的变化量，以此量化该 token 对其他 token 的语义依赖强度。直觉上，若两个 token 语义上相互依赖，改变其中一个会显著改变另一个的最终层表示；否则变化较小。
- **关键技术细节**：
  - **语义依赖分数**：对于输入层第 i 个 token $z^0_i$，将其替换 K 次得到 K 个扰动序列，计算最终层第 j 个 token 的平均变化：
    $$\Delta z^L_j | z^0_i = \frac{1}{K} \sum_{k=1}^K \left\| \tilde{z}^{L(k)}_j - z^{L(org)}_j \right\|_2$$
    该值越大，表示 j 对 i 的语义依赖越强。
  - **自我信息保留验证**：对每个 token $i$，检查扰动后 $\Delta z^L_i | z^0_i$ 是否大于所有 $\Delta z^L_j | z^0_i$（$j \neq i$），即最终层自身 token 是否最依赖自己。
  - **序列级语义聚合验证**：检查是否每个输入 token 的扰动都会影响所有最终层 token（$\Delta > 0$）。
  - **真实语义依赖评估**：使用 SpaCy 等语义依存解析工具获取每个词的“真实”依存词集合 $G_{z^0_i}$，然后通过扰动方法估计出高敏感 token 集合 $\hat{G}_{z^0_i}$，计算两者的重叠率（Alignment Score）。
  - **问答错误分析**：对于 SQuAD 问答任务，分别计算错误答案 token 对问题 token 的最大语义依赖分数 $\Delta'_{A_{wrong}|Q}$ 和正确答案 token 对问题 token 的最大分数 $\Delta'_{A_{correct}|Q}$，比较两者大小以判断错误是否源于错误依赖。
  - **定位注意力头**：分解注意力头输出，计算每个头对特定依赖的贡献变化，找出共用的关键注意力头组。

## 3. 实验设计：使用了哪些数据集 / 场景，它的 benchmark 是什么，对比了哪些方法

- **数据集**：
  - 通用语言理解：GLUE、Yelp、WikiText、gsm8k、OpenOrca、CNN/DailyMail（用于验证自我信息保留和序列级聚合）。
  - 问答任务：**SQuAD 1.1**（斯坦福问答数据集），作为 benchmark 测试错误与语义依赖的关系。
- **场景**：主要评估模型在**阅读理解问答（QA）** 任务中的表现，因为 QA 天然要求模型理解问题 token 与上下文 token 之间的依赖关系。
- **对比模型**（共 10 个）：
  - 编码器类型：BERT、RoBERTa、TinyRoBERTa、ALBERT、DistilBERT、DeBERTa、MobileBERT、MiniLM
  - 解码器类型：GPT-2、LLaMA3
  - 没有对比其他方法（本文是探索性研究，非对比性方法论文，主要验证内部机制）。

## 4. 资源与算力

- **文中未明确说明**使用的 GPU 型号、数量、训练时长等算力信息。仅在摘要和正文中提到 “extensive experiments”，但未提供具体硬件参数。

## 5. 实验数量与充分性

- **实验数量**：
  - Section 3（自我信息保留）：对 10 个模型，每个模型使用 6 个数据集，每个数据集超过 100,000 个 token 案例，总计超过 600,000 个案例。
  - Section 4（真实依赖对齐）：对 10 个模型，每个模型评估超过 10,000 个案例（每个案例对应一个 token 的扰动）。
  - Section 5（QA 错误分析）：对 10 个模型，每个模型处理超过 100,000 个 SQuAD 验证案例（含正确和错误答案）。
  - Section A.2（上下文影响）：超过 5,000 个案例分析。
  - 定位注意力头实验：对 8 个高精度模型（F1>0.8）分析所有失败 QA 案例。
- **充分性评价**：
  - **优点**：模型种类多样（覆盖 BERT 系列、GPT、LLaMA），数据集多样（通用文本、数学推理、情感、新闻等），案例数量大（百万级别），统计分析可靠。
  - **公平性**：实验设置客观，使用标准 SQuAD 数据集和常用评价指标（F1 分数）；对 GPT/LLaMA 采用 zero-shot 设置以对齐 BERT 评估方式（避免少样本引入偏差）。附录还使用 ChatGPT-4o 验证错误分类阈值。
  - 部分实验（如定位注意力头）只针对微调后的高精度模型，未在基础模型上重复，但可以接受因为需要模型具备高准确率才能分析错误依赖。

## 6. 论文的主要结论与发现

1. **自我信息保留**：绝大多数 token（>88-99%，不同模型差异）在通过多层 Transformer 后，其最终层表示依然主要反映其原始输入层的语义，而非被完全混合。
2. **序列级聚合**：几乎每个最终层 token 都从输入序列中所有 token 接收了部分语义信息（即使很小）。
3. **真实语义依赖编码**：模型通常能正确编码语义依赖——扰动某个 token 后，最终层变化最大的 token 往往是其语义上依赖的词，对齐得分平均在 82-93%。
4. **错误源于错误依赖**：在 QA 任务中，当模型输出错误答案时，错误答案 token 对问题 token 的语义依赖分数往往大于正确答案 token（例如 BERT 上比例达 79.07%）。反之，答案正确时正确依赖分数更高。
5. **参数共享性**：编码正确依赖和错误依赖的注意力头是**高度重叠**的（同一组头部），因此无法通过简单剪枝来修正错误依赖而不破坏正确依赖。
6. **上下文敏感性**：无关上下文的添加或顺序改变会显著影响语义依赖的排序，尤其是左侧上下文影响更大（附录 A.2）。

## 7. 优点：方法或实验设计上的亮点

- **新颖的扰动分析框架**：无需额外标注或训练，仅通过随机 token 替换和表示差异即可量化任意 token 间的语义依赖强度，具有通用性。
- **验证链条完整**：从底层机制（自我保留）到高层语义（依赖对齐），再到任务错误（QA 中的错误依赖），最后定位参数（注意力头），逻辑层层递进。
- **跨模型对比**：涵盖编码器、解码器、不同规模（MobileBERT 到 LLaMA3），结论具有泛化性。
- **定量与定性结合**：不仅提供百分比，还通过热力图（图 4b）直观展示注意力头贡献分布。
- **针对实际难题**：发现参数共享性，揭示了修正错误的深层困难，而非简单归因于某个模块，对后续研究有指导意义。

## 8. 不足与局限

- **依赖上下文答案存在**：方法要求答案 token 必须在输入上下文中出现（SQuAD 风格），无法处理模型生成全新答案（如 GPT 的生成式回答）的场景。论文承认此局限，并计划未来扩展。
- **随机扰动噪声**：替换为随机 token 可能引入语义不自然或 out-of-domain 表示，虽采用多次平均缓解，但仍有变异性。
- **仅分析最终层**：语义依赖可能在中间层形成，但论文只测量最终层，可能忽略层间动态。作者表示方法可扩展到中间层，但未实施。
- **依赖现有解析工具**：真实语义依赖使用 SpaCy 等工具获取，而非人工标注，可能引入解析误差（尽管附录用 Stanza 验证保持一致）。
- **GPT/LLaMA 的 zero-shot 性能低**：GPT-2 和 LLaMA3 的 F1 分数极低（0.78%、35.81%），导致错误分析中的案例较少且可能受生成答案形式影响。
- **未考虑 MLP 层作用**：注意力头分析只聚焦于 MHA，未探讨 FFN 层对语义依赖的贡献（论文承认这一点）。
- **算力信息缺失**：无法评估方法计算开销和可复现性。

（完）
