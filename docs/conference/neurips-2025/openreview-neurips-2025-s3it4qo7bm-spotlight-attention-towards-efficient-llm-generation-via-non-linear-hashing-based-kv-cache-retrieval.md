---
title: "Spotlight Attention: Towards Efficient LLM Generation via Non-linear Hashing-based KV Cache Retrieval"
title_zh: "Spotlight Attention: 基于非线性哈希KV缓存检索的高效LLM生成"
authors: "Wenhao Li, Yuxin Zhang, Gen Luo, Haiyuan Wan, ZiYang Gong, Fei Chao, Rongrong Ji"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=s3IT4Qo7bm"
tags: ["query:key-tokens"]
score: 4.0
evidence: 通过非线性哈希选择关键KV缓存，隐式识别重要令牌
tldr: LLM生成中KV缓存负担大。本文提出Spotlight Attention，使用非线性哈希函数优化查询和键的嵌入分布，动态选择关键KV缓存。该方法通过训练框架优化哈希函数，间接识别重要令牌。实验表明在保持生成质量的同时提升效率。虽不直接分析推理关键令牌，但其选择机制可用于推断令牌重要性。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-neurips-2025-s3it4qo7bm/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1419, \"height\": 521, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-s3it4qo7bm/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1422, \"height\": 316, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-s3it4qo7bm/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1441, \"height\": 580, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-s3it4qo7bm/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1411, \"height\": 281, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-s3it4qo7bm/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1448, \"height\": 705, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-s3it4qo7bm/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1421, \"height\": 527, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-s3it4qo7bm/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 434, \"height\": 319, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-s3it4qo7bm/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 673, \"height\": 365, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-s3it4qo7bm/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1448, \"height\": 722, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-s3it4qo7bm/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1442, \"height\": 1025, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-neurips-2025-s3it4qo7bm/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1449, \"height\": 256, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-s3it4qo7bm/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1456, \"height\": 351, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-s3it4qo7bm/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 646, \"height\": 290, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-s3it4qo7bm/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 701, \"height\": 228, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-s3it4qo7bm/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 706, \"height\": 190, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-s3it4qo7bm/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1448, \"height\": 221, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-s3it4qo7bm/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1446, \"height\": 277, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-s3it4qo7bm/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1450, \"height\": 316, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-s3it4qo7bm/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 597, \"height\": 142, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-s3it4qo7bm/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 823, \"height\": 138, \"label\": \"Table\"}]"
motivation: 现有线性哈希选择重要令牌效率低，希望改进哈希函数以更准确选择关键KV缓存。
method: 提出非线性哈希函数优化嵌入分布，并用Bradley-Terry损失训练以选择关键KV缓存。
result: 方法高效选择关键缓存，在生成质量和速度上均优于基线。
conclusion: 非线性哈希可有效识别重要令牌，对推理关键令牌分析具有启发意义。
---

## Abstract
Reducing the key-value (KV) cache burden in Large Language Models (LLMs) significantly accelerates inference. Dynamically selecting critical KV caches during decoding helps maintain performance. Existing methods use random linear hashing to identify important tokens, but this approach is inefficient due to the orthogonal distribution of queries and keys within two narrow cones in LLMs. We introduce Spotlight Attention, a novel method that employs non-linear hashing functions to optimize the embedding distribution of queries and keys, enhancing coding efficiency and robustness. We also developed a lightweight, stable training framework using a Bradley-Terry ranking-based loss, enabling optimization of the non-linear hashing module on GPUs with 16GB memory in 8 hours. Experimental results show that Spotlight Attention drastically improves retrieval precision while shortening the length of the hash code at least 5$\times$ compared to traditional linear hashing. Finally, we exploit the computational advantages of bitwise operations by implementing specialized CUDA kernels, achieving hashing retrieval for 512K tokens in under 100$\mu$s on a single A100 GPU, with end-to-end throughput up to 3$\times$ higher than vanilla decoding.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义

- **研究动机**：Large Language Models (LLMs) 在解码阶段面临严重的 KV cache 瓶颈，频繁的显存与缓存交换导致 GPU 利用率低下（如 LLaMA2-7B 解码时利用率低于 10%）。为加速推理，现有动态 KV cache 选择方法（如 MagicPIG）采用线性局部敏感哈希（LSH）来近似注意力的 top‑k 选择，但 LLM 中的 queries 和 keys 分布在两个近乎正交的窄锥形区域，导致线性哈希编码效率极低，通常需要 1024 位以上的长哈希码才能有效检索，这不仅占用存储还引入大量计算开销。
- **整体含义**：本文提出 **Spotlight Attention**，用**非线性 MLP 哈希函数**替代线性随机超平面划分，从而更好适配 skewed 分布，大幅缩短哈希码长度（至少 5 倍），同时保持甚至提升检索精度和生成质量，实现端到端最高 3 倍的吞吐量提升。

### 2. 论文提出的方法论

- **核心思想**：在每一注意力层中额外添加一个 **hash‑based retrieval 模块**，用 **非线性 MLP 哈希函数** 将 queries 和 keys 映射到短二值哈希码，通过 NXOR 操作快速计算 Hamming 距离，选出近似 top‑k 最重要的 KV cache 条目，仅对这些条目进行稀疏注意力计算，其余缓存保留但不参与当前步运算。
- **关键技术细节**：
    - **MLP 哈希函数**：两层 MLP（W₁, b₁, W₂），激活函数为 SiLU，输出经 sign 函数得到 ±1 的哈希码。公式：`H(x) = sign(MLP(x))`。
    - **Bradley‑Terry 排名损失**：训练时利用真实注意力分数获得 top‑k 与非 top‑k 索引集合，优化目标为让哈希距离估计的 top‑k 分数均大于非 top‑k 分数，避免对集合内部排序的“容量浪费”。损失函数为：
        `L_rank = -1/(k(n-k)) Σ_{i,j} log(sigmoid(β(B_i - C_j) - α))`
        其中 B、C 分别为估计分数中对应于真实 top‑k 和非 top‑k 的集合，β、α 为缩放和偏移超参数。
    - **可微化**：训练时用 soft sign（`γx/(1+γ|x|)`）替代 sign 以允许梯度回传；推理时恢复 sign。
    - **训练策略**：LLM 主干完全冻结，仅训练各层各头的 MLP 哈希模块（参数极小），使用少量校准数据（8192 条，来自 Book 和 Arxiv 数据集的混合），单 epoch 训练。
- **推理加速**：实现自定义 CUDA kernel 进行位打包（32 个 bool 值压缩为一个 uint32）和 NXOR GEMM（popcount 计算），使 512K tokens 的哈希检索延迟低于 100 μs。

### 3. 实验设计

- **数据集与场景**：
    - **语言建模**：PG19、ProofPile（Math）、CodeParrot（Code），评估困惑度；
    - **长上下文检索**：Needle‑in‑a‑Haystack (NIAH) 测试；
    - **下游 QA**：LongBench（含 21 个子任务，涵盖单文档、多文档、摘要、少样本、合成、代码等），使用 Rouge‑L 衡量输出相似度；
    - **效率测试**：固定上下文长度 vs 变长，固定 batch size vs 变 batch，测量端到端吞吐量及 kernel 延迟。
- **基线方法**：
    - Oracle top‑k（全精度注意力，理论上限）；
    - 线性 LSH top‑k（MagicPIG 的随机超平面哈希）；
    - Quest（块级查询感知稀疏）；
    - MagicPIG（线性 LSH + 局部窗口 + sink tokens）。
- **评估指标**：IoU（检索精度）、Perplexity、Rouge‑L、Throughput。
- **公平设置**：所有方法使用相同 token 预算（如 98% 剪枝率）或遵循各自默认配置；训练数据与测试数据分离；重复实验（效率测试取三次均值）。

### 4. 资源与算力

- **训练**：文中提到“optimization of the non‑linear hashing module on GPUs with 16GB memory in 8 hours”，但**未明确说明 GPU 型号和数量**（推测为单卡，如 RTX 4090 或 A10G）。
- **推理**：效率实验在 **8× A100 GPU** 上完成（用于 Qwen2.5‑7B 的 pipeline 并行）。
- **数据量**：训练集 8192 条样本，单 epoch。

### 5. 实验数量与充分性

- **实验组数**：相当充分。包括：
    - 语言建模 × 3 数据集 × 4 种基模型（LLaMA2‑7B/ Chat、LLaMA3‑8B、Qwen2.5‑1.5B/7B/14B）→ 多组 PPL 对比；
    - LongBench 21 子任务 × 多种剪枝率及方法 → 全面 QA 对比；
    - NIAH 测试（256‑8192 长度）→ 检索能力验证；
    - 效率测试（不同 batch/sequence length）→ 吞吐量比较；
    - 消融实验：模型尺寸、训练语料、损失函数（MSE 排名 vs 排名损失）、注意力估计方法（Hamming vs 内积）→ 关键组件分析。
- **充分性与公平性**：实验覆盖主流标准基准，与最先进方法（Quest、MagicPIG）在同等 token budget 下比较（或更少），且提供了 Oracle 上界。对比 MagicPIG 时还展示了其是否依赖局部窗口/sink tokens 的影响。实验设计较客观。

### 6. 论文的主要结论与发现

- **非线性哈希显著优于线性哈希**：在 98% 剪枝率下，Spotlight 的 IoU 达到约 0.35‑0.42（线性 LSH 仅 0.05‑0.09），且训练后提升明显。
- **更短的哈希码即可达到甚至超越长哈希码的线性方法**：Spotlight 使用 128 位哈希码，MagicPIG 至少需要 720‑1024 位，且 Spotlight 困惑度更低或持平。
- **生成质量保持良好**：在 LongBench 上，Spotlight 的输出与原始模型的 Rouge‑L 相似度最高（平均 0.58），而 Quest（1024 budget）为 0.56，MagicPIG 为 0.44。
- **效率显著提升**：端到端吞吐量最高可提升 3 倍（Qwen2.5‑7B，32K/128K 序列），哈希检索延迟对 512K tokens 低于 100 μs。
- **对多种模型和任务均有效**：在 LLaMA2/3 及 Qwen2.5 系列均表现一致。

### 7. 优点

- **方法创新性强**：首次将非线性可学习的哈希函数引入 LLM KV cache 动态检索，解决了线性哈希在 skewed 空间分布下的根本缺陷。
- **轻量高效训练**：冻结 LLM 主干，仅训练极少的 MLP 参数（每层每头一个 128‑dim MLP），使用极小校准数据（8K 条），8 小时即可完成，实用性强。
- **推理加速显著**：通过位运算和 CUDA kernel 实现极低延迟检索，且哈希码存储开销远小于 MagicPIG。
- **实验全面且公平**：覆盖多种难度任务（语言模型、长上下文检索、下游 QA），与多个强基线在剪枝预算或默认设置下对比，并提供 Oracle 上限作为参考。
- **开源开放**：提供完整代码和数据（GitHub 链接）。

### 8. 不足与局限

- **检索精确度仍有提升空间**：IoU 仅约 40%（即使使用非线性哈希），意味着仍有大量真正重要的 token 未被选中，可能导致性能损失（尤其对 prompt‑sensitive 任务）。
- **对训练数据的潜在依赖**：虽然消融表明换用 C4/GitHub Code 训练后效果仍好，但未在多领域（如医疗、法律）验证，可能存在领域偏移风险。
- **缺乏对更长上下文的验证**：效率实验虽模拟至 2M tokens，但实际 QA 任务只测试到 8K，更长序列（如 128K）下的质量和检索稳定性未详细报告。
- **未与其他新兴方法（如 StreamingLLM、H2O）在相同剪枝率下比较**：仅比较了 Quest 和 MagicPIG，遗漏部分近期工作，但可能因为篇幅或方法分类差异。
- **硬件资源要求未完全透明**：训练 GPU 型号未明确说明，影响可复现性。
- **消融实验数量偏少**：只对损失函数和估计方法做了消融，未系统探索 MLP 结构深度/宽度、哈希码长度等超参数的影响。
- **应用限制**：需要额外存储哈希码（每个 key 128 位），虽然短但仍增加约 2% 缓存（原始 KV 16‑bit 时），且训练需要少量校准数据，无法做到完全无训练迁移。

（完）
