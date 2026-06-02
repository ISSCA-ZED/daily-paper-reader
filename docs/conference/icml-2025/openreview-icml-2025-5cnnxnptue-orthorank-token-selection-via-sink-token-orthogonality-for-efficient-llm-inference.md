---
title: "OrthoRank: Token Selection via Sink Token Orthogonality for Efficient LLM inference"
title_zh: OrthoRank：通过Sink Token正交性实现高效LLM推理的令牌选择
authors: "Seungjun Shin, Jaehoon Oh, Dokwan Oh"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=5CnnxNPtuE"
tags: ["query:key-tokens"]
score: 8.0
evidence: 分析sink token隐藏状态跨层相似性
tldr: 本文深入研究了大语言模型中的sink token，发现随着层数加深，sink token与其他token的隐藏状态余弦相似度增加，且sink token自身的隐藏状态几乎不变。基于此，提出OrthoRank方法通过选择与sink token正交的token来精简输入，实现对关键token的识别。该工作直接使用隐藏状态分析来揭示token之间的关系。
source: ICML-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2025-5cnnxnptue/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1747, \"height\": 580, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-5cnnxnptue/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1392, \"height\": 787, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-5cnnxnptue/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 786, \"height\": 744, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-5cnnxnptue/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 852, \"height\": 429, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-5cnnxnptue/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 852, \"height\": 358, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-5cnnxnptue/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1563, \"height\": 652, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-5cnnxnptue/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 673, \"height\": 443, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-5cnnxnptue/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 850, \"height\": 325, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-5cnnxnptue/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1249, \"height\": 1923, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-5cnnxnptue/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1253, \"height\": 1875, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-5cnnxnptue/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1424, \"height\": 1660, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-5cnnxnptue/fig-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1252, \"height\": 1119, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-5cnnxnptue/fig-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1608, \"height\": 920, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-5cnnxnptue/fig-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 862, \"height\": 542, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-icml-2025-5cnnxnptue/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 861, \"height\": 311, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-5cnnxnptue/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 861, \"height\": 305, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-5cnnxnptue/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 737, \"height\": 566, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-5cnnxnptue/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 851, \"height\": 162, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-5cnnxnptue/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 857, \"height\": 283, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-5cnnxnptue/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 857, \"height\": 140, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-5cnnxnptue/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1078, \"height\": 1190, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-5cnnxnptue/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1776, \"height\": 450, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-5cnnxnptue/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 826, \"height\": 231, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-5cnnxnptue/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1758, \"height\": 1760, \"label\": \"Table\"}]"
motivation: 为了理解sink token在深层隐藏状态中的行为，并利用其特性选择关键token以减少计算。
method: 分析sink token与其他token隐藏状态的相似性，并基于正交性设计token选择策略。
result: OrthoRank在多个基准上减少输入token数量同时保持推理性能。
conclusion: 揭示了sink token的隐藏状态变化规律，并提供了基于隐藏状态的关键token选择方法。
---

## Abstract
Attention mechanisms are central to the success of large language models (LLMs), enabling them to capture intricate token dependencies and implicitly assign importance to each token. Recent studies have revealed the sink token, which receives disproportionately high attention despite their limited semantic role. In this paper, we first expand the relationship between the sink token and other tokens, moving beyond attention to explore their similarity in hidden states, considering the layer depth. We observe that as the layers get deeper, the cosine similarity between the normalized hidden states of the sink token and those of other tokens increases, and that the normalized hidden states of the sink token exhibit negligible changes. These imply that other tokens consistently are directed toward the sink token throughout the layers. Next, we propose a dynamic token selection method, called OrthoRank, using these findings to select important tokens. Specifically, in a certain layer, we define token importance by the speed at which the token moves toward the sink token. This is converted into orthogonality with the sink token, meaning that tokens that are more orthogonal to the sink token are assigned greater importance. Finally, through extensive experiments, we demonstrated that our method results in lower perplexity and higher zero-shot accuracy compared to layer pruning methods at the same sparsity ratio with comparable throughput, while also achieving superior performance on LongBench.

---

## 论文详细总结（自动生成）

# OrthoRank：通过Sink Token正交性实现高效LLM推理的令牌选择

## 1. 核心问题与整体含义

- **研究背景**：大型语言模型（LLM）在各类任务中表现出色，但推理计算成本高昂，尤其是实时应用场景。现有轻量化方法中，层剪枝虽然简单有效，但存在固有局限性：它使用固定剪枝决策应用于所有输入令牌，无法适应不同令牌的计算需求——某些令牌在深层可能不再需要进一步处理，而其他令牌仍受益于计算。
- **核心问题**：能否在不额外训练的情况下，在每个层识别哪些令牌有利于计算？换句话说，是否存在一种无需训练路由器或分类器的动态令牌选择机制？
- **研究动机**：论文从“注意力汇（attention sink）”现象出发，首次将其与隐藏状态空间中的行为联系起来。通过分析隐藏状态的余弦相似性，发现随着层数加深，其他令牌逐渐向sink令牌靠拢，而sink令牌自身几乎静止。这为动态令牌选择提供了理论基础：与sink令牌更正交（即移动速度更快）的令牌更值得计算。
- **整体意义**：提出了OrthoRank方法，通过令牌与sink令牌的正交性动态选择重要令牌，在保持与层剪枝相同稀疏度和可比吞吐量的情况下，实现了更低的困惑度和更高的零样本准确率，并优于LongBench任务。

## 2. 方法论

### 核心思想
- 基于两个关键观察：
  1. 从注意力汇发生的层之后，sink令牌与其他令牌的归一化隐藏状态余弦相似度随层数增加而增加（即角度减小）。
  2. sink令牌自身的归一化隐藏状态跨层几乎不变（余弦相似度接近1），而其他令牌随层增加逐渐偏离早期状态。
- 因此，其他令牌在隐藏状态空间中正被“吸引”向sink令牌。令牌的重要性可定义为它向sink令牌移动的速度，即对cosine相似度关于该令牌隐藏状态的梯度范数。

### 关键技术细节
- **重要性度量公式推导**：
  - 定义cosine相似度的梯度：\(\frac{\partial}{\partial \bar{h}_i} \cos(\bar{h}_0, \bar{h}_i)\)。
  - 通过简化假设（除sink令牌外各令牌归一化隐藏状态范数近似相等），梯度范数平方正比于 \(1 - \cos^2(\bar{h}_0, \bar{h}_i)\)。
  - 因此，\(\lvert \cos(\bar{h}_0, \bar{h}_i) \rvert\) 越小，令牌重要性越高，即与sink令牌更正交的令牌更重要。
- **实现策略**：
  - 对每个层，计算每个令牌与sink令牌（第一个令牌）归一化隐藏状态的内积绝对值 \(| \bar{h}_0^\top \bar{h}_i |\)。
  - 选择内积绝对值最小的 top k 令牌（即最正交的令牌），对它们执行完整的层运算（Query、Key、Value、FFN等）。
  - 未选择的令牌仅参与Key-Value计算（用于支持选中令牌的注意力），但不更新自身的隐藏状态，通过残差连接跳过。
- **选择性应用层**：为了避免在注意力汇发生前的层以及靠近输出的关键层使用该策略，OrthoRank并非应用于所有层，而是结合层剪枝方法选择哪些层应用token选择。具体地，使用类似SLEB的迭代评估方法，测量在特定层应用token选择后的性能影响，确定最优的“OrthoRank层”集合。

### 算法流程（文字描述）
1. 使用校准集（Wikitext-2）评估每个层应用token选择的效果，选择性能影响最小的层作为OrthoRank层。
2. 设定总稀疏度（如20%），确定需要应用token选择的层数量（如30%的层），每层内只计算33%的令牌。
3. 推理时，对于OrthoRank层：
   - 输入归一化隐藏状态，计算每个令牌与sink令牌的内积绝对值。
   - 排除sink令牌本身（设为无穷大）。
   - 选择内积绝对值最小的k个令牌（按排序后保留原始索引）。
   - 仅对这些选中令牌执行Query、Key、Value和FFN计算；未选中令牌的KV值仍然计算以供选中令牌使用。

## 3. 实验设计

### 数据集与场景
- **语言建模**：使用Wikitext-2（校准集）和C4验证集（性能测试），测量困惑度（PPL）。
- **零样本任务**：PIQA、WinoGrande（WG）、HellaSwag（HS）、ARC-Easy、ARC-Challenge，使用LM Evaluation Harness。
- **长上下文**：LongBench（包括NarrativeQA、Qasper、MultiFieldQA等16个子任务），分别测试校准长度为2048、4096、8192。
- **生成质量**：TruthfulQA（MC1和BLEU生成分数）。
- **吞吐量**：在单张A6000 GPU上，批大小32，序列长度2048，平均50次。

### 基准方法
- **SLEB**（Song et al., 2024）：迭代层剪枝方法，使用类似指标评估哪些层可跳过。
- **Shortened LLaMA**（Kim et al., 2024）：一次性层剪枝方法，无需微调。
- **随机选择**：随机选择33%令牌。
- **正交性逆选择**：选择与sink令牌内积最大的令牌（即最不正交的）。
- **注意力基线**：基于注意力分数选择令牌。

### 模型范围
- Llama-2（7B、13B、70B）、Llama-3（8B）、Llama-3.1（70B）、Mistral（7B）、Mixtral（8×7B）。

## 4. 资源与算力

- 文中仅提到在单张A6000 GPU上测量吞吐量（批大小32，序列长度2048，平均50次），未明确说明训练时长或总算力消耗。
- 由于OrthoRank不涉及额外训练（仅需要校准集进行评估），因此计算资源主要用于推理评估和校准步骤，但具体GPU数量、总推理时间等未提供。
- 与需训练的早期退出或混合深度方法相比，OrthoRank更节约资源，但论文未给出定量对比。

## 5. 实验数量与充分性

### 实验组数
- **主要结果表**：表1（困惑度）覆盖5种模型×2种稀疏度×2种方法（SLEB, +OrthoRank），外加Shortened LLaMA对比；表2（零样本）类似；表3（LongBench）覆盖稀疏度、校准长度等组合；表4（TruthfulQA）4种模型。
- **消融实验**：表5对比了7种选择标准、阶段、KV计算等；图7分析不同令牌/层稀疏度组合；图8对比稀疏度从10%到50%；表6对比注意力选择。
- **诊断实验**：图2-3展示余弦相似度变化；图4展示逐层选择性能；图6展示吞吐-性能权衡。

### 充分性与公平性
- **充分性**：涵盖多个模型族、多种任务类型（语言建模、零样本、长文本、事实性）、多个稀疏度等级（10%、20%为主，部分扩展到50%），消融实验全面（包括随机、逆选择、归一化阶段、KV计算必要性、注意力基线等）。实验设计较为充分。
- **客观性**：所有对比均在相同稀疏度下进行，且使用公开数据集和标准评估工具（LM Evaluation Harness、LongBench）。与SLEB和Shortened LLaMA公平比较，均不进行微调。
- **偏差风险**：校准集仅用Wikitext-2，可能对特定领域有偏向；但所有方法均使用同一校准集，因此比较是公平的。

## 6. 主要结论与发现

- **发现1**：在注意力汇出现后的层中，sink令牌与其他令牌的归一化隐藏状态余弦相似度随层数加深而逐渐增加，而sink令牌自身几乎不变，表明其他令牌正持续向sink令牌靠拢。
- **发现2**：基于上述发现，提出令牌重要性指标——与sink令牌的正交性（即较小的内积绝对值），并验证了比随机选择和逆选择更优的层性能。
- **主要结论**：将OrthoRank与层剪枝（SLEB）结合，在相同总稀疏度下，正交性选择的令牌显著优于仅剪枝方法，困惑度更低、零样本准确率更高、LongBench表现更好，同时吞吐量增益接近稀疏度比例（约1.18×）。
- **附加结论**：未选择令牌需要计算KV值以维持性能；归一化隐藏状态比原始隐藏状态更适合作为选择依据；正交性选择优于基于注意力分数的选择（注意力选择带来额外开销且性能较差）。

## 7. 优点

- **无需额外训练**：OrthoRank完全基于预训练模型的隐藏状态特性，不训练路由器或分类器，可直接应用于现有LLM，实用性高。
- **理论基础扎实**：从sink令牌现象出发，通过余弦相似度分析揭示隐藏状态空间中的动态模式，提供了可解释的令牌重要性度量。
- **计算效率高**：仅需计算内积（矩阵乘法），与FlashAttention等融合内核兼容，不引入显著开销。
- **灵活性与选择性**：并非所有层都应用token选择，而是结合层剪枝评估选择最优层，避免在关键层过度削减。
- **实验广泛且深入**：覆盖多种模型规模（7B~70B）、多种任务类型，消融实验全面证明了各设计选择的有效性。

## 8. 不足与局限

- **对极长上下文的适应性有限**：虽然LongBench上表现优于SLEB，但在8192长度下部分任务（如PCount）出现异常值，且校准长度增加时性能并不总是提升（见表3），表明该方法对长上下文处理的稳定性有待验证。
- **sink令牌的普遍性假设**：论文主要以第一个令牌作为sink，但已知某些模型（如Chat版本）中分隔符也可作为sink，论文未系统性考虑这类情况，可能降低跨模型泛化性。
- **稀疏度上限限制**：实验指出40%以上稀疏度时性能急剧下降（图14），且在高稀疏度下逆选择可能表现更好，说明正交性标准在极低计算预算下可能失效。
- **理论分析简化**：梯度推导假设非sink令牌范数相等，实际近似成立但存在偏差（图12显示sink令牌范数明显更大），可能影响重要性排序的精确性。
- **未评估训练兼容性**：论文仅关注推理加速，未讨论该方法是否影响微调或后续训练，对于需要连续训练的部署场景（如持续学习）可能不适用。
- **资源报告不完整**：未明确给出总计算预算、校准时间开销、不同模型所需的GPU时间等，难以复现计算成本。

（完）
