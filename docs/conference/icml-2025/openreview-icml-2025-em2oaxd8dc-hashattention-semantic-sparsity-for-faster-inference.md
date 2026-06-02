---
title: "HashAttention: Semantic Sparsity for Faster Inference"
title_zh: HashAttention：利用语义稀疏性加速推理
authors: "Aditya Desai, Shuo Yang, Alejandro Cuadron, Matei Zaharia, Joseph E. Gonzalez, Ion Stoica"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=Em2oaXd8Dc"
tags: ["query:key-tokens"]
score: 7.0
evidence: 通过MIPS识别关键token以实现注意力稀疏性
tldr: 本文指出注意力计算中只有少数关键token对输出有显著贡献，将识别关键token建模为最大内积搜索（MIPS）问题。提出HashAttention利用离散哈希和查询键分布优化实现token选择，在保持质量的同时加速推理。该方法直接提供了度量token重要性的方案，但与推理序列上下文结合不够紧密。
source: ICML-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2025-em2oaxd8dc/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 826, \"height\": 513, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-em2oaxd8dc/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1363, \"height\": 587, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-em2oaxd8dc/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1780, \"height\": 412, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-em2oaxd8dc/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 805, \"height\": 509, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-em2oaxd8dc/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1420, \"height\": 569, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-em2oaxd8dc/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 681, \"height\": 369, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-em2oaxd8dc/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 682, \"height\": 396, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-em2oaxd8dc/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 679, \"height\": 371, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-icml-2025-em2oaxd8dc/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1773, \"height\": 701, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-em2oaxd8dc/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1758, \"height\": 199, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-em2oaxd8dc/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1604, \"height\": 246, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-em2oaxd8dc/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1768, \"height\": 194, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-em2oaxd8dc/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 897, \"height\": 124, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-em2oaxd8dc/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1181, \"height\": 501, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-em2oaxd8dc/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1298, \"height\": 460, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-em2oaxd8dc/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1801, \"height\": 461, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-em2oaxd8dc/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 918, \"height\": 195, \"label\": \"Table\"}]"
motivation: 注意力计算中token具有稀疏性，只有少数关键token重要，但现有方法难以有效利用该稀疏性。
method: 将关键token识别视为推荐问题，设计HashAttention通过哈希索引快速定位重要token。
result: 实验表明HashAttention在多种长文本任务上加速注意力计算且性能下降极小。
conclusion: 为利用token稀疏性加速推理提供了实用框架，且方法可迁移至关键token分析。
---

## Abstract
Leveraging long contexts is crucial for advanced AI systems, but attention computation poses a scalability challenge. While scaled dot-product attention (SDPA) exhibits token sparsity, i.e. only a few pivotal tokens significantly contribute to output, exploiting this sparsity remains challenging. Existing methods either suffer from quality degradation or require substantial additional resources. We show that identifying pivotal tokens is a Maximum Inner Product Search (MIPS) problem. However, existing MIPS solutions are not well-suited for SDPA, as they are not GPU-friendly and often underperform due to the separated query and key distributions. This paper introduces HashAttention, framing pivotal token identification as a recommendation problem. Given a query, HashAttention encodes keys and queries in Hamming space, capturing the required semantic similarity, using learned mapping functions. HashAttention efficiently identifies pivotal tokens for a given query using bitwise operations and computes attention using only these tokens, improving the overall attention efficiency. Trained on generic data, HashAttention reduces tokens used by up to $16\times$ with minimal quality loss, requiring only 32 bits of auxiliary memory per token. Sparsity can be further improved to $32\times$ through task-specific fine-tuning. 
On A100 GPU, at $32\times$ sparsity, incorporating HashAttention reduces attention latency by up to $4.3\times$ in GPT-FAST and $2.54\times$ in FlashDecode, and achieves up to $3.12\times$ higher throughput for GPT-FAST.

---

## 论文详细总结（自动生成）

# 论文中文详细总结

## 1. 核心问题与整体含义（研究动机和背景）

- **研究动机**：现代AI系统（如大语言模型）需要处理长上下文，但缩放点积注意力（SDPA）的计算复杂度随上下文长度呈二次增长，成为可扩展性瓶颈。
- **已知现象**：注意力计算具有天然的**token稀疏性**——仅有少数关键（pivotal）token对输出有显著贡献。利用这一稀疏性可以大幅降低计算量，但现有方法存在质量下降或需要大量额外资源的问题。
- **关键洞察**：识别关键token本质上是一个**最大内积搜索（MIPS）**问题。然而，现有MIPS方案（如图结构）对GPU不友好，且由于查询与键的分布分离，直接应用效果不佳。
- **论文目标**：提出一种GPU友好、低辅助内存的稀疏注意力方法，在保持模型质量的同时显著提升推理效率。

## 2. 论文提出的方法论

### 2.1 核心思想

- 将关键token识别视为**推荐问题**：查询（query）相当于用户，键-值对（key-value pairs）相当于项目。通过将查询和键嵌入到汉明空间（Hamming space）中，利用位运算快速找到与查询最相似的键，从而定位关键token。

### 2.2 关键技术细节

- **映射函数**：
  - 使用两个独立的可学习映射函数：`ϕ_kv`（将键-值对映射到b位汉明空间）和`ϕ_q`（将查询映射到汉明空间）。
  - 映射函数由全连接网络 + sign函数组成，输出为二进制位。训练时用tanh代替sign实现软划分。
- **相似度度量**：
  - 使用汉明距离衡量查询与键的语义相似度：`Score(k,v,q) = -H(ϕ_kv(k,v), ϕ_q(q))`。
  - 实现时，将位签名压缩为整数，通过异或和位计数运算高效计算汉明距离。
- **训练方法**：
  - 将问题建模为多标签分类：以每个attention head的真实top-k token作为标签，使用二元交叉熵损失训练映射函数，并通过权重处理类别不平衡（`class1-weight = α + β / context-length`）。
  - 训练数据：通用数据集（如OpenWebText）上训练，长度与推理时匹配；可进一步在任务特定数据上微调（HashAttention*）。
- **推理流程**：
  - 预计算键-值对的位签名并与KV缓存一并存储（仅需32 bits/token/head）。
  - 解码时计算查询的位签名，通过位操作得到汉明距离，选出top-k token，然后仅对这些token计算完整注意力。
- **理论支撑**：
  - 引理4.1：在值向量独立假设下，token贡献正比于 `ai * ||vi||2`。
  - 引理4.2：排序等价于内积 `⟨[q,1], [k, log(||v||2)]⟩`，即MIPS问题。MIPS可通过非对称变换转化为余弦相似度搜索，进而用位签名近似。

## 3. 实验设计

### 3.1 数据集与场景

- **基准测试（Benchmark）**：
  - **LongBench**（多任务长文本基准，包含英文和中文子集）
  - **RULER@16K / RULER@32K**（合成长上下文推理任务）
- **子任务覆盖**：多文档问答、摘要、合成数据、代码生成等（见表1、2、3）。

### 3.2 对比方法

- **静态稀疏**：StreamingLLM
- **KV缓存丢弃**：H2O
- **动态稀疏**：InfLLM、Double Sparsity (DS)、Quest
- **Oracle**：使用真实top-k注意力分数（理想上限）

### 3.3 评估指标

- **平均质量（accuracy/F1等）**：各基准上的得分
- **稀疏度**：使用的token数与全量token数的比例
- **辅助内存**：bits per token per attention head (PTPA)
- **效率**：延迟（ms）、吞吐量（tokens/s）

## 4. 资源与算力

- **GPU型号**：NVIDIA A100 GPU（文中明确提及）。
- **硬件数量与训练时长**：**未明确说明**。仅提及训练使用OpenWebText及LongBench部分样本，未报告训练所需GPU数量、天数或总计算量。实验推理部分在单A100上测量。
- **模型**：Llama-3.1-8B-Instruct 和 Mistral-7B-Instruct-v0.3。

## 5. 实验数量与充分性

- **质量评估**：
  - 表1：在LongBench 8个代表性任务上比较7种方法（含Oracle），使用固定token预算512。
  - 图3：在4个LongBench任务和6个RULER任务上绘制不同稀疏度下的Pareto曲线（与DS、Quest对比）。
  - 表2、3：完整LongBench和RULER@16K上16×稀疏度的详细得分。
  - 消融实验：
    - 召回率微基准（图5）：对比HashAttention与DS在不同长度下的召回率。
    - 位宽影响（表9）：16/32/64位下的交叉熵损失。
    - LSH对比（表8）：32位/256位/512位LSH vs. 32位HashAttention。
    - 余弦相似度分析（表7）：证明映射使查询与键分布更接近。
- **效率评估**：
  - 图4(a)：在GPT-FAST和FlashDecode中不同上下文长度下的延迟（32×稀疏度）。
  - 图4(b)：GPT-FAST端到端吞吐量提升（最高3.12×）。
  - 表6：SCORE计算延迟 vs. 全内积（不同位宽）。
- **充分性评估**：
  - 覆盖了多种任务类型（问答、摘要、合成、代码）和两种主流模型。
  - 对比了多种主流稀疏注意力方法，并控制辅助内存预算（32 bits PTPA）。
  - 消融实验系统，验证了位宽、训练数据、LSH替代、分布偏移等。
  - 实验设计公平，但**未包含**与MagicPig、SqueezedAttention等的直接对比（仅提及为相关/并发工作）。
  - 中文数据上质量下降较明显（表5），表明训练数据偏差可能影响泛化。

## 6. 主要结论与发现

1. **稀疏性程度**：HashAttention在通用数据集上可实现**16×稀疏度**，质量下降极小（LongBench平均-0.78点）；任务特定微调后可达**32×**。
2. **辅助内存效率**：仅需**32 bits/token/head**，远低于DS和Quest的典型配置（64-256 bits）。
3. **推理加速**：
   - 在A100上，32×稀疏度下GPT-FAST注意力延迟**降低4.3×**，FlashDecode降低**2.54×**。
   - 端到端吞吐量（GPT-FAST）**最高提升3.12×**（32K序列长度）。
4. **质量优势**：在相同辅助内存和token预算下，HashAttention在LongBench和RULER上均优于DS和Quest，达到接近全注意力的性能。
5. **召回率**：HashAttention的top-k召回率显著高于DS（图5），是质量优势的直接来源。
6. **学习优于LSH**：学习得到的位签名远优于随机投影（LSH），后者需1024位以上才能接近32位HashAttention的效果（表8）。

## 7. 优点

- **方法创新性**：首次将稀疏注意力问题明确建模为MIPS，并通过可学习的汉明嵌入高效求解，理论清晰。
- **GPU友好**：所有操作（整数位运算）可在GPU上高效并行，无需CPU offload。
- **低辅助内存**：仅32 bits/token/head，不影响原本的KV缓存内存压力。
- **可扩展性**：支持通过任务微调进一步增强稀疏性，适应特定场景。
- **系统性实验**：覆盖多模型、多基准、多对比方法，消融实验全面；效率测量考虑了实际推理框架（GPT-FAST, FlashDecode）。
- **Token级稀疏**：无需依赖页面/块结构，理论上可更精确地选取关键token（虽通过vLLM页大小为1实现，但不影响效率）。

## 8. 不足与局限

- **训练开销**：HashAttention需要针对每个模型进行至少一次训练（通用或微调），不如StreamingLLM等完全零训练方法便捷。但DS也有类似校准过程。
- **GPU算力披露不足**：未报告训练所需的具体GPU时数、超参数调优成本，难以评估部署该方法的实际资源门槛。
- **跨语言泛化**：仅使用英文数据训练，在中文LongBench子集上质量下降较大（表5低于全模型2.66点），提示多语言场景需相应训练。
- **长上下文场景覆盖**：实验仅在KV缓存完全在GPU内存的条件下进行（最长~128K）。未评估当KV缓存超出显存（需CPU offload）时的表现，而这是实际长上下文推理的关键场景。
- **对比方法的局限性**：与同时期方法（MagicPig, SqueezedAttention）未做直接对比，仅列入相关工作；部分效率对比未考虑DS在量化/反量化上的额外开销（文中已指出因排除该开销而高估DS吞吐量）。
- **理论假设**：引理4.1基于值向量独立的假设，忽略了token间的相关性，在极端情况下可能不是最优选择。但实验证明在实际应用中足够有效。
- **可迁移性**：方法主要针对key向量，未来可探索将value规范等更多信息融入哈希映射。

（完）
