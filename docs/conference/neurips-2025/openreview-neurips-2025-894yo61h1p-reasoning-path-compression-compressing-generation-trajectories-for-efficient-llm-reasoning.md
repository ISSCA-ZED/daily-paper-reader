---
title: "Reasoning Path Compression: Compressing Generation Trajectories for Efficient LLM Reasoning"
title_zh: 推理路径压缩：压缩生成轨迹以实现高效的LLM推理
authors: "Jiwon Song, Dongwon Jo, Yulhwa Kim, Jae-Joon Kim"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=894Yo61h1P"
tags: ["query:key-tokens"]
score: 8.0
evidence: 使用重要性分数识别关键token进行压缩
tldr: 该论文针对大语言模型推理路径过长导致内存和吞吐量瓶颈的问题，提出了一种无需训练的推理路径压缩方法RPC。该方法利用最近查询窗口计算每个缓存条目的重要性分数，并仅保留高重要性token的KV缓存，从而在不显著影响精度的前提下大幅减少内存占用并提高生成速度。实验表明RPC在多种推理任务上有效平衡了效率与准确性，为基于token重要性度量的推理加速提供了实用方案。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-neurips-2025-894yo61h1p/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1409, \"height\": 732, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-894yo61h1p/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1424, \"height\": 410, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-894yo61h1p/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1277, \"height\": 397, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-894yo61h1p/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1423, \"height\": 468, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-894yo61h1p/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 483, \"height\": 580, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-894yo61h1p/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1351, \"height\": 379, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-894yo61h1p/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1363, \"height\": 802, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-894yo61h1p/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1344, \"height\": 491, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-neurips-2025-894yo61h1p/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1413, \"height\": 555, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-894yo61h1p/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1411, \"height\": 382, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-894yo61h1p/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1205, \"height\": 323, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-894yo61h1p/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1211, \"height\": 167, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-894yo61h1p/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1384, \"height\": 242, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-894yo61h1p/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1324, \"height\": 1051, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-894yo61h1p/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1273, \"height\": 1049, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-894yo61h1p/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1440, \"height\": 293, \"label\": \"Table\"}]"
motivation: 长推理路径增加内存使用并降低吞吐量，限制推理模型部署。
method: 提出RPC方法，通过最近查询窗口计算重要性分数，压缩KV缓存中的低重要性条目。
result: 实验显示RPC在不牺牲推理准确性的情况下显著降低了内存占用并提升了生成速度。
conclusion: RPC提供了一种训练无关且高效的推理加速方法，基于token重要性实现。
---

## Abstract
Recent reasoning-focused language models achieve high accuracy by generating lengthy intermediate reasoning paths before producing final answers.
While this approach is effective in solving problems that require logical thinking, long reasoning paths significantly increase memory usage and reduce throughput of token generation, limiting the practical deployment of such models.
We propose Reasoning Path Compression (RPC), a training-free method that accelerates inference by leveraging the semantic sparsity of reasoning paths.
RPC periodically compresses the KV cache by retaining cache entries that receive high importance score, which are computed using a selector window composed of recently generated queries.
Experiments show that RPC improves generation throughput of QwQ-32B by up to 1.60$\times$ compared to the inference with full KV cache, with an accuracy drop of 1.2\% on the AIME 2024 benchmark.
Our findings demonstrate that semantic sparsity in reasoning traces can be effectively exploited for compression, offering a practical path toward efficient deployment of reasoning LLMs. Our code is available at https://github.com/jiwonsong-dev/ReasoningPathCompression.

---

## 论文详细总结（自动生成）

# 论文总结：Reasoning Path Compression: Compressing Generation Trajectories for Efficient LLM Reasoning

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **核心问题**：大型推理语言模型（如 OpenAI o1、DeepSeek-R1、QwQ-32B）在解决复杂推理任务时，会生成很长的中间推理路径（可长达数万 token），导致 KV 缓存急剧膨胀，显著增加内存使用并降低生成吞吐量，限制了实际部署。
- **研究背景**：现有 KV 缓存压缩方法（如 SnapKV、H2O、TOVA）主要针对长输入序列进行压缩，不适用于生成长的推理输出。训练式推理缩短方法（如 LightThinker）在复杂推理任务上精度下降严重。
- **整体含义**：论文提出一种无需训练的推理路径压缩方法（RPC），利用推理路径的语义稀疏性（冗余、重复），通过周期性压缩 KV 缓存，在保持高精度的同时大幅提升推理效率和降低内存占用。

## 2. 论文提出的方法论：核心思想、关键技术细节、公式或算法流程

- **核心思想**：推理路径中存在语义稀疏性（大量重复或冗余的逻辑步骤），因此可以丢弃低重要性的 KV 缓存条目，而不破坏推理连贯性。RPC 使用最近生成的 token（称为 selector window）的注意力权重来评估历史 token 的重要性，仅保留高重要性的条目。
- **关键技术细节**：
  - **周期性压缩**：设置压缩间隔 \(P\) 和选择窗口大小 \(R\)。每生成 \(P\) 个新 token 触发一次压缩，使用最新的 \(R\) 个 token 作为查询，计算所有历史 token 的重要性分数。
  - **重要性评分**：在每个注意力层，对选择窗口内每个查询 token 在所有注意力头上计算对历史 token 的注意力权重，进行局部平均池化（窗口大小 \(w=3\)）后求和平均，得到每个历史 token 的重要性。
    \[
    \text{Importance}(t) = \frac{1}{2w+1} \cdot \frac{1}{R \cdot H} \sum_{i=-w}^{w} \sum_{r=1}^{R} \sum_{h=1}^{H} \text{Attn}_h^\ell(q_r, k_{t+i})
    \]
  - **保留策略**：在每个压缩周期，从当前保留的缓存和新生成的 \(P\) 个 token 中，根据重要性保留 top-\(N \cdot \frac{P}{c}\) 个（\(c\) 为压缩比，默认 4×），并始终保留选择窗口内的 \(R\) 个 token。
- **算法流程（文字说明）**：
  - 初始化 KV 缓存 \(C_{KV}\) 和选择器查询缓存 \(C_Q\)。
  - 每一步生成时，如果当前步属于选择窗口范围（根据 \(P\) 和 \(R\) 判定），则将当前查询加入 \(C_Q\)。
  - 每 \(P\) 步（即压缩时刻），计算当前 \(C_{KV}\) 中所有 token 的重要性，保留重要性最高的前 \(N \cdot P/c\) 个 token，再加上选择窗口内最近的 \(R\) 个 token，更新 \(C_{KV}\)，并清空 \(C_Q\)。

## 3. 实验设计：数据集、基准、对比方法

- **数据集**：
  - **AIME 2024**（数学推理）
  - **LiveCodeBench**（代码推理）
  - **IFEval**（指令跟随）
- **模型**：
  - DeepSeek-R1-Distill-Qwen-7B（7B 参数）
  - QwQ-32B（32B 参数）
- **对比方法**：
  - **Full KV Cache**（无压缩基线）
  - **H2O**（基于重击者的 KV 缓存压缩）
  - **TOVA**（基于 RNN 式门控的压缩）
  - **LightThinker**（训练式推理压缩方法）
  - **RPC**（提出方法，带 \(P=4096\) 和 \(P=1024\) 两种设置）
- **评估指标**：pass@1 准确率（AIME 取 8 次、LiveCodeBench 取 4 次、IFEval 取 1 次）、生成吞吐量（tokens/s）、峰值内存（GB）。

## 4. 资源与算力

- **文中明确说明**：
  - DeepSeek-R1-Distill-Qwen-7B 实验在 **单块 NVIDIA H100 SXM GPU** 上完成。
  - QwQ-32B 实验在 **4 块 NVIDIA H100 SXM GPU** 上完成。
  - 使用 FlashAttention-2 作为注意力内核，基于 HuggingFace Transformers v4.45。
  - 最大生成 token 数设为 32768，批次大小设为 16（在吞吐量/内存实验中部分使用了 8、16、32）。
- **训练时长**：RPC 无需训练，仅推理阶段应用，故未报告训练时间。

## 5. 实验数量与充分性

- **主要实验组**：
  - 准确率对比（表 1）：在 3 个数据集上对比 4 种方法，涵盖两种模型。
  - 冗余率分析（图 6）：基于句子嵌入相似度，在 AIME 2024 上比较全 KV 与 RPC 的语义冗余。
  - 效率评估（图 7、表 5、表 6）：测量不同生成长度和批次大小下的吞吐量和峰值内存。
  - 消融实验（图 8、表 2）：研究压缩间隔 \(P\) 和选择窗口大小 \(R\) 的影响。
  - 聚合粒度实验（表 4）：比较 layer-wise、group-wise、head-wise 的重要性聚合方式。
  - 激进压缩实验（表 7）：8× 压缩比下的表现。
- **充分性评价**：实验覆盖了多种推理任务、多模型规模、多压缩配置；对比了训练式和推理式基线；消融分析全面；效率实验包括不同批次大小和输出长度。整体实验设计较为充分、客观，但缺少统计误差棒（文中注明未提供）。公平性方面，为 H2O/TOVA 设置了与 RPC 相同总体压缩比的固定预算，LightThinker 的报告压缩比由其自身决定。

## 6. 论文的主要结论与发现

- **核心结论**：RPC 在 4× 压缩下，QwQ-32B 在 AIME 2024 上准确率仅下降 1.2%（从 79.5% 到 78.3%），生成吞吐量提升最高 1.60×，峰值内存降低超 50%，并解决了 32K 输出长度下的 OOM 问题。
- **其他发现**：
  - 推理路径的语义稀疏性可被量化和利用：3-gram 熵分析表明推理 LLM 比非推理 LLM 具有更高冗余。
  - 周期性压缩比逐点压缩更高效，选择窗口大小推荐 32，压缩间隔推荐 1024 或 4096。
  - 对于更简单的 IFEval 任务，RPC 甚至略有准确率提升，表明冗余对复杂推理的影响更大。

## 7. 优点

- **无需训练**：RPC 是训练无关方法，可即插即用于任何推理 LLM，无需修改模型或重新训练。
- **动态适应性**：定期重新评估所有缓存 token（包括之前保留的和新生成的），使上下文自然更新，避免旧推理步骤僵化。
- **高效性与实用性**：显著降低内存占用和提升吞吐量，尤其适用于长生成场景；实际解决了 32B 模型在 32K 输出下的 OOM 问题。
- **鲁棒性**：在复杂推理基准（AIME、LiveCodeBench）上精度损失小；对简单任务（IFEval）几乎无影响。
- **设计细致**：引入局部平均池化、层级聚合等技巧稳定重要性估计；消融实验充分，参数选择有据可依。

## 8. 不足与局限

- **准确性仍有下降**：在 4× 压缩下，复杂任务（AIME）准确率下降 1.2%~2.6%；8× 压缩时下降更显著（如 DeepSeek-R1-Distill-Qwen-7B 从 55.5% 降至 47.5%）。
- **未提供误差棒**：文中未报告多次运行的统计误差，可能影响结论的可信度。
- **任务覆盖局限**：实验主要集中于数学、代码和指令跟随，未涉及其它高精度敏感领域（如医学、法律问答）。
- **对模型结构依赖**：注意力分数的计算依赖于完整注意力实现（使用 FlashAttention-2）；对于其他非标准注意力机制可能需要适配。
- **参数选择需手动调整**：压缩间隔 \(P\) 和窗口大小 \(R\) 需要在效率和精度之间权衡，缺乏自适应设置机制。
- **无理论保证**：论文仅提供经验验证，未从理论上分析压缩后推理能力保留的边界条件。

（完）
