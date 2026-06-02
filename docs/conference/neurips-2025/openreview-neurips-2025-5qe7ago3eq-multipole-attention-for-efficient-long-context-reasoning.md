---
title: Multipole Attention for Efficient Long Context Reasoning
title_zh: 用于高效长上下文推理的多极注意力
authors: "Coleman Richard Charles Hooper, Sebastian Zhao, Luca Manolache, Sehoon Kim, Michael W. Mahoney, Sophia Shao, Kurt Keutzer, Amir Gholami"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=5Qe7AGO3Eq"
tags: ["query:key-tokens"]
score: 6.0
evidence: 利用token重要性选择关键token以实现高效注意力
tldr: 提出Multipole Attention方法，仅对最重要的token计算精确注意力，其余使用近似，从而加速长上下文推理。该方法通过token重要性度量来区分关键与非关键token，在保持推理准确性的同时大幅减少计算量。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-neurips-2025-5qe7ago3eq/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1446, \"height\": 467, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-5qe7ago3eq/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1448, \"height\": 538, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-5qe7ago3eq/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1426, \"height\": 672, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-5qe7ago3eq/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1442, \"height\": 563, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-5qe7ago3eq/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1430, \"height\": 658, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-5qe7ago3eq/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1439, \"height\": 858, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-neurips-2025-5qe7ago3eq/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 858, \"height\": 215, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-5qe7ago3eq/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 682, \"height\": 360, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-5qe7ago3eq/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 681, \"height\": 358, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-5qe7ago3eq/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1443, \"height\": 333, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-5qe7ago3eq/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 707, \"height\": 121, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-5qe7ago3eq/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 941, \"height\": 121, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-5qe7ago3eq/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1291, \"height\": 180, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-5qe7ago3eq/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1290, \"height\": 178, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-5qe7ago3eq/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1422, \"height\": 152, \"label\": \"Table\"}]"
motivation: 长推理链导致KV缓存压力大，稀疏注意力可能引入错误。
method: Multipole Attention仅对最重要token计算精确注意力，其余近似。
result: 在长推理任务上，速度提升显著且精度损失极小。
conclusion: 基于token重要性的选择性注意力可兼顾效率与质量。
---

## Abstract
Large Reasoning Models (LRMs) have shown promising accuracy improvements on complex problem-solving tasks. While these models have attained high accuracy by leveraging additional computation at test time, they need to generate long chain-of-thought reasoning in order to think before answering, which requires generating thousands of tokens.
While sparse attention methods can help reduce the KV cache pressure induced by this long autoregressive reasoning, these methods can introduce errors which disrupt the reasoning process.
Our work addresses these challenges by introducing Multipole Attention, which accelerates autoregressive reasoning by only computing exact attention for the most important tokens, while maintaining approximate representations for the remaining tokens. 
Our method first performs clustering to group together semantically similar key vectors, and then uses the cluster centroids both to identify important key vectors and to approximate the remaining key vectors in order to retain high accuracy.
Additionally, in order to accelerate long generation tasks, we design a fast cluster update process to quickly re-cluster the input and previously generated tokens, thereby allowing for  accelerating attention to the previous output tokens.
We evaluate our method using emerging LRMs such as Qwen-8B and Deepseek-R1-Distil-Qwen2.5-14B, demonstrating that our approach can maintain accuracy on complex reasoning tasks even with aggressive attention sparsity settings.
We also provide kernel implementations to demonstrate the practical efficiency gains from our method, achieving up to 4.5$\times$ speedup for attention in long-context reasoning applications.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 论文的核心问题与整体含义（研究动机和背景）
- **研究动机**：大型推理模型（LRMs）在复杂问题求解中表现出高精度，但其生成的长链思维推理（chain-of-thought）需要生成数千个token，导致自回归解码时KV缓存内存压力巨大。
- **问题背景**：现有稀疏注意力方法虽能减少KV缓存占用，但会引入误差，破坏推理过程；且很多方法需要对prompt进行预处理，难以在线处理新生成的推理token。
- **整体含义**：本文旨在在不牺牲推理精度的前提下，加速长上下文推理，提出一种既能精确关注关键token又能近似保留上下文信息的注意力机制。

## 2. 论文提出的方法论
- **核心思想**：仅对最重要的token计算精确注意力，对剩余token使用聚类中心近似表示，从而同时实现高效和准确。
- **关键技术细节**：
  - **聚类与中心点**：使用k-means对键向量（key vectors）进行语义聚类，每个簇计算一个代表性子中心（key centroid）和值中心（value centroid）。
  - **重要性识别**：将当前查询（query）与各簇中心点比较，估计每个簇的注意力得分，选出得分高的簇中的键进行精确注意力计算。
  - **多极近似（Multipole Approximation）**：对低分簇，直接用簇中心点的注意力得分代替该簇所有键的注意力，并加权求和得到近似输出。
  - **层次化扩展**：可构建多层次中心点（粗粒度→细粒度），逐级细化，减少中心点比较开销。
  - **快速在线聚类更新**：采用分块聚类（blockwise clustering）和滑动窗口策略，仅更新新生成token所在块，并通过少量k-means迭代优化，避免全局重聚类。
- **算法流程**（文字说明）：
  1. 预填充阶段：对输入序列进行k-means分组聚类，计算每个簇的键中心点和值中心点。
  2. 生成阶段每一步：
     - 将当前查询与所有簇中心点比较，得到各簇重要性得分。
     - 根据预算（token budget）选择重要性最高的簇，加载其所有键进行精确注意力计算。
     - 对低分簇，直接使用其值中心点与查询-中心点得分的乘积作为近似贡献。
     - 合并精确与近似结果得到最终注意力输出。
     - 每生成一定数量的token，执行快速聚类更新（仅处理新块），保持索引新鲜。

## 3. 实验设计
- **数据集**：
  - LongBenchV2：包含复杂真实世界长上下文问题（文档问答、对话理解、代码理解等），分易/难、短/中/长（<32K/32K-128K/128K+）子集。
  - GSM-Infinite：合成数学推理任务（1步和2步运算），测试8K和16K上下文长度。
- **基准模型**：
  - Qwen3-8B
  - DeepSeek-R1-Distil-Qwen-14B
- **对比方法**：
  - 全注意力基线（FlashDecoding）
  - Squeezed Attention（语义聚类稀疏注意力，但无近似）
  - QUEST（基于位置分组的稀疏注意力）
  - 层次化版本：Squeezed Attention-H、Multipole Attention-H
  - 此外在附录中对非推理长上下文模型（Llama-3.1-8B-Instruct）进行了LongBenchV1上的对比，包括DuoAttention和TOVA。
- **主要指标**：准确率（accuracy），以及注意力运行时间加速比。

## 4. 资源与算力
- **GPU型号**：A6000和A100两种平台用于内核基准测试。
- **具体说明**：实验在A6000和A100上进行内核运行时间测量；训练和预训练未涉及（使用已发布模型进行推理）。未给出具体GPU数量或训练时长，仅提及使用A6000（24GB？）和A100（40/80GB？）进行评估。

## 5. 实验数量与充分性
- **实验数量**：
  - 在LongBenchV2上对两个模型（Qwen3-8B、DeepSeek-R1-Distil-Qwen-14B）进行了评估，每个实验3次重复并取平均。
  - 在GSM-Infinite上对Qwen3-8B进行了8K和16K两种上下文长度、1步和2步运算的测试。
  - 在LongBenchV1上对Llama-3.1-8B-Instruct进行了11个子任务的评估（附录）。
  - 系统基准测试：A6000和A100上不同批大小（1/4/16）和不同稀疏度（90%/95%）的注意力运行时间。
  - 消融实验：中心点数量（1/128至1/8）、分块大小（2K/4K/8K/16K）。
  - 层次化变体对比。
- **充分性与客观性**：
  - 覆盖了多个数据集（真实、合成、长/短上下文）和多个模型，对比了多种基线方法（Squeezed Attention、QUEST、DuoAttention、TOVA）。
  - 实验设计较为全面，但仅在两个具体推理模型上进行主要评估，对更广泛的模型泛化性有限。
  - 对比方法均调整至相同token预算（考虑元数据开销）以确保公平。

## 6. 论文的主要结论与发现
- **主要发现**：Multipole Attention能在激进稀疏（如128或512 token预算）下保持与全注意力基线几乎一致的准确率，显著优于Squeezed Attention等仅精确加载的方法。
- **加速效果**：在A6000上最多实现4.5倍注意力速度提升，在A100上最多2.8倍。
- **层次化变体**在相同内存操作下实现了更高精度，优于单层方法。
- **快速聚类更新**仅引入3-5%的解码开销，使方法可用于在线生成。

## 7. 优点
- **创新点**：
  - 首次将近似注意力与语义聚类结合，同时实现精确和近似计算，既保留了关键token的精确性，又通过中心点保留了全局上下文信息。
  - 提出快速在线聚类更新策略，使方法适用于长生成场景。
  - 层次化扩展进一步降低了中心点比较开销。
- **实验设计亮点**：
  - 在多个复杂推理任务上验证，并包含短/中/长上下文分割，显示方法在不同长度下的鲁棒性。
  - 系统实现使用自定义Triton内核，并提供了详细运行时间分析，证明了实际效率。
  - 消融实验清晰展示了超参数（中心点数量、分块大小）的影响。

## 8. 不足与局限
- **未加速预填充阶段**：方法仅加速生成（解码）阶段，不加速预填充（prefill）部分的注意力。
- **实现额外开销**：需要额外存储中心点，且需集成到现有LLM推理框架中，工程实现复杂度较高。
- **泛化性验证有限**：主要测试了两种推理模型，推理场景之外仅在一个非推理模型（Llama-3.1-8B-Instruct）上进行LongBenchV1实验，覆盖不够广泛。
- **实验规模与复现性**：未提供所有实验的完整随机种子和误差线，仅有3次重复的平均值，统计显著性未量化。
- **理论分析缺失**：未对近似误差进行理论界分析。

（完）
