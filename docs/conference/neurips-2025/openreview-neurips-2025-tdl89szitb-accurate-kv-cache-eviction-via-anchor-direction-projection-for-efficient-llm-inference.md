---
title: Accurate KV Cache Eviction via Anchor Direction Projection for Efficient LLM Inference
title_zh: 通过锚点方向投影实现精确KV缓存驱逐
authors: "Zijie Geng, Jie Wang, Ziqi Liu, Feng Ju, Yiming Li, Xing Li, Mingxuan Yuan, Jianye HAO, Defu Lian, Enhong Chen, Feng Wu"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=Tdl89SZItB"
tags: ["query:key-tokens"]
score: 7.0
evidence: 基于投影的token重要性评分函数用于KV缓存
tldr: 提出AnDPro方法，通过引入基于向量投影的评分函数，精确衡量KV缓存中token的重要性，克服了传统启发式方法（如注意力权重）的局限。该方法利用token值状态的空间关系，在内存优化和推理加速上表现更优。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-neurips-2025-tdl89szitb/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 819, \"height\": 387, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-tdl89szitb/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 700, \"height\": 357, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-tdl89szitb/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 836, \"height\": 369, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-tdl89szitb/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1436, \"height\": 594, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-tdl89szitb/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 840, \"height\": 357, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-tdl89szitb/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1456, \"height\": 1076, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-tdl89szitb/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1321, \"height\": 226, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-tdl89szitb/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1439, \"height\": 708, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-tdl89szitb/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 727, \"height\": 545, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-tdl89szitb/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 731, \"height\": 521, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-tdl89szitb/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 862, \"height\": 692, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-tdl89szitb/fig-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1446, \"height\": 1864, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-tdl89szitb/fig-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1454, \"height\": 1271, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-tdl89szitb/fig-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 1359, \"height\": 736, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-tdl89szitb/fig-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 1431, \"height\": 288, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-tdl89szitb/fig-016.webp\", \"caption\": \"\", \"page\": 0, \"index\": 16, \"width\": 1445, \"height\": 501, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-tdl89szitb/fig-017.webp\", \"caption\": \"\", \"page\": 0, \"index\": 17, \"width\": 1443, \"height\": 499, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-tdl89szitb/fig-018.webp\", \"caption\": \"\", \"page\": 0, \"index\": 18, \"width\": 1440, \"height\": 549, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-tdl89szitb/fig-019.webp\", \"caption\": \"\", \"page\": 0, \"index\": 19, \"width\": 1457, \"height\": 518, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-neurips-2025-tdl89szitb/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1418, \"height\": 998, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-tdl89szitb/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1454, \"height\": 763, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-tdl89szitb/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1003, \"height\": 591, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-tdl89szitb/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1436, \"height\": 780, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-tdl89szitb/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1116, \"height\": 360, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-tdl89szitb/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1002, \"height\": 160, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-tdl89szitb/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1356, \"height\": 864, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-tdl89szitb/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1355, \"height\": 863, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-tdl89szitb/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1363, \"height\": 865, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-tdl89szitb/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1356, \"height\": 460, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-tdl89szitb/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1174, \"height\": 125, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-tdl89szitb/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 670, \"height\": 125, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-tdl89szitb/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1410, \"height\": 130, \"label\": \"Table\"}]"
motivation: 现有KV缓存驱逐策略仅用注意力权重衡量token重要性，忽略了向量空间关系。
method: 提出AnDPro，基于锚点方向投影计算token重要性分数。
result: 在多种LLM任务上，AnDPro比基线方法更准确选择重要token，提升推理效率。
conclusion: 投影式评分能更好捕捉token价值，优化KV缓存策略。
---

## Abstract
Key-Value (KV) cache eviction---which retains the KV pairs of the most important tokens while discarding less important ones---is a critical technique for optimizing both memory usage and inference latency in large language models (LLMs).
However, existing approaches often rely on simple heuristics---such as attention weights---to measure token importance, overlooking the spatial relationships between token value states in the vector space.
This often leads to suboptimal token selections and thus performance degradation.
To tackle this problem, we propose a novel method, namely **AnDPro** (**An**chor **D**irection **Pro**jection), which introduces a projection-based scoring function to more accurately measure token importance.
Specifically, AnDPro operates in the space of value vectors and leverages the projections of these vectors onto an *``Anchor Direction''*---the direction of the pre-eviction output---to measure token importance and guide more accurate token selection.
Experiments on $16$ datasets from the LongBench benchmark demonstrate that AnDPro can maintain $96.07\\%$ of the full cache accuracy using only $3.44\\%$ KV cache budget, reducing KV cache budget size by $46.0\\%$ without compromising quality compared to previous state-of-the-arts.

---

## 论文详细总结（自动生成）

# 论文总结：通过锚点方向投影实现精确KV缓存驱逐，提升LLM推理效率

## 1. 核心问题与整体含义（研究动机和背景）

- **背景**：大语言模型（LLM）中的自注意力机制需要存储Key-Value（KV）缓存来复用中间结果，但长序列下KV缓存内存和I/O开销巨大。已有研究表明注意力存在稀疏性，仅少数token对输出贡献显著，因此KV缓存驱逐策略（保留重要token、丢弃次要token）成为一种关键技术。
- **问题**：现有方法（如H2O、SnapKV、Ada-KV等）主要依赖简单的启发式规则（如注意力权重）来衡量token重要性，**忽视了token值状态在向量空间中的空间关系**，导致选择次优，影响生成质量。
- **整体含义**：论文旨在提出一种更精确的评分函数，利用向量空间几何信息指导KV缓存驱逐，从而在极低缓存预算下保持高精度，降低推理成本。

## 2. 方法论：核心思想、关键技术细节

### 核心思想
- 将KV缓存驱逐建模为组合优化问题，并松弛为稀疏优化问题。通过理论分析，发现最优解的激活变量满足形如 `s_i = a_i (θ^T v_i + b)` 的评分函数，其中 `a_i` 为注意力权重，`v_i` 为值向量，`θ` 和 `b` 为参数。
- 进一步直观设定：将**预驱逐输出向量 y 的方向**作为锚点方向（Anchor Direction），即令 `θ = y`，并设 `b = 0`，得到最终评分函数：`s_i = a_i · (y^T v_i)`。该评分同时考虑注意力权重和值向量在输出方向上的投影，能更准确反映token对最终输出的贡献。

### 关键技术细节
- **观察窗口**：沿用SnapKV的方法，保留最后若干个prompt token作为观察窗口，用窗口内query计算注意力与输出。
- **Token分块（Chunking）**：将相邻token合并为块（chunk size=4），保持语义连贯性，提高选择连续性。
- **跨头预算分配**：在每个Transformer层内，根据所有注意力头中token的评分进行统一Top-k选择，实现灵活预算分配。
- **保留首token**：始终保留第一个token（attention sink）。

### 公式流程（文字说明）
1. 对每个注意力头，利用观察窗口中的query计算所有prompt token的注意力权重 `a_i` 和预驱逐输出 `y`。
2. 将token分块后，对每个块计算加权值向量 `v_hat` 和聚合注意力 `a_hat`。
3. 计算每个块的评分：`s = a_hat * (y^T v_hat)`。
4. 所有头、所有块的评分拼接后，进行全局Top-k选择，确定保留的token集合（加上观察窗口和首token）。

## 3. 实验设计

### 数据集与场景
- **LongBench**：16个数据集，涵盖单文档QA、多文档QA、摘要、少样本学习、合成任务、代码等，平均序列长度约7,425 token。
- **Needle-in-a-Haystack（NIAH）**：长上下文检索任务，测试模型在32K~384K序列中检索“针”的能力。

### 基准（Baselines）
- H2O、StreamingLLM、SnapKV、PyramidInfer（Pyramid）、Ada-KV、CriticalKV（前SOTA）。
- 使用模型：Mistral-7B-Instruct-v0.2 和 Llama-3.1-8B-Instruct。

### 评估指标
- LongBench：各数据集标准化评分（F1、Rouge-L、Accuracy等），取平均。
- NIAH：按深度和长度计算检索正确率。

### 实验组数
- 主实验：不同预算（128/256/512/1024）下对比所有方法，共4×2模型×16数据集 = 128组主结果。
- NIAH实验：预算128，与Ada-KV、CriticalKV等对比。
- 消融实验：隔离投影评分函数贡献（5组对比）、分析各组件（分块、首token、跨头分配）影响。
- 锚点方向选择实验（不同温度系数α）、偏置b实验。
- 长上下文扩展实验（64K~384K）。
- 大模型验证（Qwen2.5-32B-Instruct）。
- 推理延迟与内存测量。

## 4. 资源与算力

- **GPU型号**：单张NVIDIA A800-80G GPU。
- **数量**：未明确说明多卡并行，推测为单卡运行各实验。
- **训练/推理时长**：未报告总耗时，但给出了不同阶段（Prefilling、KV Update、Decoding）的延迟对比。附加分析指出AnDPro引入的额外计算（Update KV Phase）时间开销很小（例如64K序列下约0.58秒）。
- 论文未提及多GPU分布式训练或大规模预训练，所有实验均为推理阶段测试。

## 5. 实验数量与充分性

- **实验数量**：非常充分。覆盖：
  - 2种主流LLM（Mistral、Llama），4种缓存预算。
  - 16个LongBench数据集 + NIAH长上下文测试。
  - 多种消融（评分函数、分块大小、首token、跨头分配等）。
  - 额外实验：长序列（384K）、大模型（32B）、推理效率（内存/延迟）、值向量分析、案例分析。
- **公平性与客观性**：
  - 基线结果部分来自原论文，部分自行复现，并在同一框架（Ada-KV）上实现。
  - 超参数对齐（观察窗口32、分块大小4等），且进行敏感性分析。
  - 消融实验严格控制变量，证明投影评分函数的独立增益。
- **充分性评价**：实验设计系统、覆盖广泛，能有力支撑方法有效性。但仍存在局限（见第8点）。

## 6. 主要结论与发现

1. **AnDPro在几乎所有设置下均达到SOTA**：在LongBench 16个数据集上，平均评分普遍高于所有基线（包括前SOTA CriticalKV和Ada-KV）。
2. **极低预算下的惊人保留率**：Mistral模型预算256时，仅用3.44%的KV缓存（256/7425）即可保留全缓存96.07%的准确率，相比CriticalKV节省46%的预算。
3. **长上下文检索能力显著提升**：NIAH测试中AnDPro得分97.37，接近全缓存99.13，大幅优于Ada-KV（91.30）和CriticalKV（92.75）。
4. **计算开销可忽略**：内存占用与解码延迟与其他驱逐方法相当，额外计算主要在KV更新阶段，时间开销极小。
5. **投影评分函数是核心贡献**：消融实验证实，无论是否搭配分块、跨头分配等技术，基于投影的评分均优于纯注意力评分。

## 7. 优点

- **理论驱动**：从组合优化问题出发，通过松弛和KKT条件推导出合理的评分函数形式，而非纯经验设计。
- **直观有效**：锚点方向（预驱逐输出方向）选择符合直觉——保留对输出方向贡献大的token。
- **性能卓越**：在极低缓存预算下保持高精度，大幅优于现有方法。
- **计算友好**：额外开销小，易于集成到现有推理框架。
- **鲁棒性强**：在多种模型、预算、任务类型上表现一致，且超参数敏感性低（b=0即可）。

## 8. 不足与局限

- **预算分配局限于层内**：论文仅实现跨头的统一预算分配，未探索层间非均匀分配（如PyramidInfer的动态层分配），作者承认该局限。
- **模型规模验证有限**：主实验仅7B/8B级别，虽补充了32B实验结果，但未在更大模型（如70B、MoE等）上系统验证。
- **长上下文极限能力未完全探索**：超过384K序列后所有方法失败，且AnDPro在256K~384K开始下降，需进一步改进。
- **可能缺乏严格统计分析**：未报告每次实验的方差或置信区间，对实验结果的可重复性有一定影响（但遵循领域惯例）。
- **应用限制**：方法适用于Prefilling阶段一次性驱逐，未讨论流式生成中持续更新的场景（已有解码变体，但实验较少）。

（完）
