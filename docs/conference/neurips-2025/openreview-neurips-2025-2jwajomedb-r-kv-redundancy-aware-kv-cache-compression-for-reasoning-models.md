---
title: "R-KV: Redundancy-aware KV Cache Compression for Reasoning Models"
title_zh: "R-KV: 推理模型的冗余感知KV缓存压缩"
authors: "Zefan Cai, Wen Xiao, Hanshi Sun, Cheng Luo, Yikai Zhang, Ke Wan, Yucheng Li, Yeyang Zhou, Li-Wen Chang, Jiuxiang Gu, Zhen Dong, Anima Anandkumar, Abedelkadir Asi, Junjie Hu"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=2jwAjomEDB"
tags: ["query:key-tokens"]
score: 4.0
evidence: 针对推理模型中的冗余令牌，间接涉及关键令牌识别
tldr: "推理模型生成长输出导致KV缓存过大。本文提出R-KV方法，对推理模型中的冗余令牌进行压缩，仅使用10%缓存即可保持近100%性能。该方法通过识别冗余令牌（即非关键令牌）来优化压缩，与关键令牌识别互补。实验显示优于现有基线。"
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-neurips-2025-2jwajomedb/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1432, \"height\": 607, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-2jwajomedb/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1438, \"height\": 629, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-2jwajomedb/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 812, \"height\": 730, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-2jwajomedb/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1312, \"height\": 873, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-2jwajomedb/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 978, \"height\": 318, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-2jwajomedb/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 709, \"height\": 791, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-2jwajomedb/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 431, \"height\": 336, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-neurips-2025-2jwajomedb/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1448, \"height\": 577, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-2jwajomedb/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1451, \"height\": 488, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-2jwajomedb/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1449, \"height\": 1018, \"label\": \"Table\"}]"
motivation: 推理模型长输出导致KV缓存过大，现有压缩方法容易失效，希望识别冗余令牌以高效压缩。
method: 提出R-KV，专门针对推理模型中的冗余令牌进行压缩，保留关键令牌信息。
result: "仅用10%缓存保持近100%性能，显著优于基线。"
conclusion: 冗余令牌的识别有助于高效KV缓存压缩，可与关键令牌分析结合。
---

## Abstract
Reasoning models have demonstrated impressive performance in self-reflection and chain-of-thought reasoning. However, they often produce excessively long outputs, leading to prohibitively large key-value (KV) caches during inference. While chain-of-thought inference significantly improves performance on complex reasoning tasks, it can also lead to reasoning failures when deployed with existing KV cache compression approaches. To address this, we propose Redundancy-aware KV Cache Compression for Reasoning models (R-KV), a novel method specifically targeting redundant tokens in reasoning models. Our method preserves nearly 100% of the full KV cache performance using only 10% of the KV cache, substantially outperforming existing KV cache baselines, which reach only 60% of the performance. Remarkably, R-KV even achieves 105% of full KV cache performance with 38% of the KV cache. This KV-cache reduction also leads to a 50% memory saving and a 2x speedup over standard chain-of-thought reasoning inference. Experimental results show that R-KV consistently outperforms existing KV cache compression baselines across two mathematical reasoning datasets.

---

## 论文详细总结（自动生成）

# 论文 R-KV 详细总结

## 1. 核心问题与整体含义（研究动机和背景）
- **问题**：大型推理模型（如 DeepSeek-R1）在复杂推理任务中会生成极长的思维链（Chain-of-Thought），导致 key-value (KV) 缓存急剧膨胀，推理时内存和计算开销不可承受。
- **现有方法失效**：传统 KV 缓存压缩方法（如 SnapKV）基于注意力分数筛选令牌，但推理模型的输出中大量冗余（如重复的自我验证、反思）会获得高注意力权重，导致关键信息被误删或冗余被保留，压缩后准确率严重下降（仅达完整缓存的 60%）。
- **整体含义**：需要一种专门针对推理模型冗余特性的压缩策略，在保留关键推理步骤的同时选择性丢弃重复、低价值的令牌，从而在不牺牲推理能力的前提下大幅降低内存占用。

## 2. 方法论：核心思想、关键技术细节
- **核心思想**：在解码过程中同时评估令牌的**重要性**和**冗余性**，通过联合得分函数选择保留的令牌，实现高效压缩。
- **技术细节**：
    - **解码时压缩**：维护两个缓冲区：固定大小的保留缓存（budget）和当前生成的临时缓冲区。每生成固定长度（如 128 个令牌）后执行一次压缩。
    - **重要性评分（§3.2）**：利用最近 α 个观察令牌的注意力权重计算每个候选令牌的重要性。支持 Multi-Head Attention 和 Grouped-Query Attention（使用 max-pooling 聚合组内分数），并对注意力分数进行滑动窗口 max-pooling 以稳定估计。
    - **冗余性评分（§3.3）**：计算每个头的 key 向量之间的余弦相似度矩阵，去除自我相似和对角线后，对每个令牌求平均相似度，再经 softmax 归一化为冗余分数。为防止误删近期可能有用的令牌，对与当前令牌最为相似的 β 个最近令牌的相似度置零。
    - **联合选择策略（§3.4）**：最终得分 \( Z_i^h = \lambda I_i^h - (1-\lambda) R_i^h \)，其中 λ 控制重要性与冗余性的权衡（实验推荐 λ=0.1）。按得分排序选出预算内的令牌保留。

<center>图：R-KV 的流程示意（原文 Figure 1）</center>

## 3. 实验设计
- **数据集**：数学推理数据集 **MATH-500**（中等难度）和 **AIME 2024**（高难度竞赛题）。
- **模型**：DeepSeek-R1-Distill-Llama-8B、DeepSeek-R1-Distill-Qwen-14B（统称 R1-Llama-8B、R1-Qwen-14B）。
- **基准方法**：
    - **FullKV**：保留完整 KV 缓存（性能上界）。
    - **SnapKV**：基于注意力的压缩方法（同样按解码间隔压缩，以公平比较）。
- **评估指标**：pass@1，每个问题生成 64 个回答（采样温度 0.6，top-p 0.95），使用非零温度避免确定性解码的波动。
- **超参数**：\( B_{\text{buffer}}=128 \), \( \alpha=8 \), 默认 \( \lambda=0.1 \)，冗余阈值 T 和 β 通过消融确定（原文未列出具体 T 值，但方法中明确使用）。

## 4. 资源与算力
- **硬件**：所有实验在 **NVIDIA A100 80G** GPU 上完成（附录 B.1 提及）。
- **算力细节**：原文**未明确说明**使用的 GPU 数量、训练时长（因方法无需训练，仅推理评估）。推理时每个实验需生成 64 个回答，覆盖多种预算设置，总计算量较大但未量化报告。

## 5. 实验数量与充分性
- **实验组数**：
    - 两个数据集 × 两种模型 × 多个 KV 缓存预算（如 128、256、512…4096 共 10 个级别）。
    - 消融实验：λ 的敏感性分析（图 6，6 个 λ 值）、注意力 vs 冗余性贡献分析（图 5）。
    - 效率分析：不同生成长度（8K、16K）下的内存节省与吞吐量对比（表 1）。
    - 案例分析：可视化比较 R-KV 与 SnapKV 的令牌选择差异（图 7）。
- **充分性与公平性**：对比方法采用相同压缩间隔和预算，消融覆盖关键参数，评估使用 64 次重复以降低方差。但**仅涵盖数学推理任务**，未测试其他领域（如代码、科学推理），泛化性有待验证。实验设计整体客观、公平。

## 6. 主要结论与发现
- **压缩性能**：R-KV 在 **10%–34%** KV 缓存预算下即可达到与 FullKV 几乎相同的准确率（且常**超越** FullKV 达 **105%**），而 SnapKV 仅能恢复约 60% 的性能。
- **固定预算下**：例如 R1-Llama-8B 在 MATH-500 上，预算 1024 时达到无损；在 AIME-24 上预算 1536 时达到无损。
- **效率提升**：相比 FullKV，R-KV 在 16K 生成长度下可实现 **9× 更大的批大小**和 **6.6× 更高的吞吐量**，同时内存节省高达 93.75%。
- **冗余性识别有效性**：R-KV 选择的令牌分布更广、语义更多样，避免了 SnapKV 的局部集中和冗余保留问题。

## 7. 优点
- **训练无关、模型无关**：无需额外训练或微调，可直接应用于任何 Transformer 模型。
- **针对性设计**：首次明确针对推理模型的长输出冗余特性，联合考虑重要性和冗余性，优于纯注意力方法。
- **解码时压缩**：在生成过程中实时压缩，避免预填充阶段的先验假设，符合长序列生成的实际需求。
- **效率双重收益**：不仅减少内存占用，还通过减小注意力计算规模带来加速，且因压缩后可以容纳更大批大小，整体吞吐量提升显著。

## 8. 不足与局限
- **任务覆盖有限**：仅在数学推理上验证，未测试 NLP 其他长输出任务（如代码生成、多步问答），冗余特性可能因任务而异。
- **超参数敏感**：λ、T、β 等参数需手动调节，且可能依赖模型和数据集（论文仅对 λ 做了系统分析，T 和 β 仅给出默认值）。
- **与高级注意力机制的兼容性**：未讨论与 paged attention 等框架的集成，实际部署中可能需要额外实现。
- **内存重分配开销**：在无原生 KV 压缩接口的推理框架中，每次压缩需分配/释放内存，可能抵消部分加速收益（论文在限制中已提及）。
- **冗余性度量基于余弦相似度**：对于语义相近但功能不同的令牌（如修正的计算步骤）可能误判为冗余，存在风险。

（完）
