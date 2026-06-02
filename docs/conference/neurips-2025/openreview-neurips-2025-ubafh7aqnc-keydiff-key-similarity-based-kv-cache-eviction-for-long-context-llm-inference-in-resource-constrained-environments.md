---
title: "KeyDiff: Key Similarity-Based KV Cache Eviction for Long-Context LLM Inference in Resource-Constrained Environments"
title_zh: "KeyDiff: 基于键相似性的KV缓存驱逐用于资源受限环境下的长上下文LLM推理"
authors: "Junyoung Park, Dalton Jones, Matthew J Morse, Raghavv Goel, Mingu Lee, Christopher Lott"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=uBaFH7aQnC"
tags: ["query:key-tokens"]
score: 7.0
evidence: 基于键相似性识别需要保留的最重要token
tldr: 针对长上下文推理中资源受限的问题，本文提出基于键相似性的KV缓存驱逐方法KeyDiff。该方法利用几何上独特的键往往具有高注意力分数的现象，仅通过键相似性就能高效识别需要保留的最重要token，且无需依赖注意力分数因而可兼容FlashAttention等优化注意力机制。实验表明在严格内存限制下KeyDiff能够有效保留关键token并维持长上下文推理性能。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-neurips-2025-ubafh7aqnc/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1235, \"height\": 423, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-ubafh7aqnc/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1431, \"height\": 383, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-ubafh7aqnc/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 602, \"height\": 404, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-ubafh7aqnc/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1415, \"height\": 316, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-ubafh7aqnc/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 504, \"height\": 396, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-ubafh7aqnc/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1457, \"height\": 305, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-ubafh7aqnc/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1430, \"height\": 356, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-ubafh7aqnc/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1419, \"height\": 317, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-ubafh7aqnc/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1410, \"height\": 318, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-ubafh7aqnc/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1414, \"height\": 318, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-ubafh7aqnc/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1400, \"height\": 346, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-ubafh7aqnc/fig-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 722, \"height\": 270, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-ubafh7aqnc/fig-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1332, \"height\": 566, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-ubafh7aqnc/fig-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 861, \"height\": 704, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-ubafh7aqnc/fig-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 1311, \"height\": 512, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-ubafh7aqnc/fig-016.webp\", \"caption\": \"\", \"page\": 0, \"index\": 16, \"width\": 960, \"height\": 784, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-ubafh7aqnc/fig-017.webp\", \"caption\": \"\", \"page\": 0, \"index\": 17, \"width\": 1425, \"height\": 450, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-ubafh7aqnc/fig-018.webp\", \"caption\": \"\", \"page\": 0, \"index\": 18, \"width\": 1418, \"height\": 385, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-ubafh7aqnc/fig-019.webp\", \"caption\": \"\", \"page\": 0, \"index\": 19, \"width\": 740, \"height\": 364, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-neurips-2025-ubafh7aqnc/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1446, \"height\": 947, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-ubafh7aqnc/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 900, \"height\": 306, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-ubafh7aqnc/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 913, \"height\": 406, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-ubafh7aqnc/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1164, \"height\": 850, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-ubafh7aqnc/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1223, \"height\": 1379, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-ubafh7aqnc/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1163, \"height\": 847, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-ubafh7aqnc/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1222, \"height\": 1374, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-ubafh7aqnc/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1081, \"height\": 668, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-ubafh7aqnc/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 794, \"height\": 949, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-ubafh7aqnc/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1076, \"height\": 2152, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-ubafh7aqnc/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1361, \"height\": 2138, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-ubafh7aqnc/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1042, \"height\": 2133, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-ubafh7aqnc/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1047, \"height\": 2129, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-ubafh7aqnc/table-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 1015, \"height\": 2141, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-ubafh7aqnc/table-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 514, \"height\": 178, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-ubafh7aqnc/table-016.webp\", \"caption\": \"\", \"page\": 0, \"index\": 16, \"width\": 516, \"height\": 176, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-ubafh7aqnc/table-017.webp\", \"caption\": \"\", \"page\": 0, \"index\": 17, \"width\": 1051, \"height\": 176, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-ubafh7aqnc/table-018.webp\", \"caption\": \"\", \"page\": 0, \"index\": 18, \"width\": 1223, \"height\": 374, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-ubafh7aqnc/table-019.webp\", \"caption\": \"\", \"page\": 0, \"index\": 19, \"width\": 627, \"height\": 206, \"label\": \"Table\"}]"
motivation: 长上下文推理中KV缓存过大，资源受限环境下需要高效识别重要token。
method: 利用键独特性和高注意力分数的关联，提出基于键相似性的驱逐策略。
result: 在严格内存限制下有效保留关键token并维持推理性能。
conclusion: 提供了一种无需注意力分数的关键token识别方法，适用于资源受限场景。
---

## Abstract
We demonstrate that geometrically distinctive keys during LLM inference tend to have high attention scores. Based on the phenomenon we propose KeyDiff, a training-free KV cache eviction method based solely on key similarity. Unlike other KV cache eviction methods, KeyDiff can process arbitrarily long prompts within strict resource constraints and efficiently generate responses.
We provide a theoretical basis for KeyDiff by relating key diversity with attention scores. These results imply  KeyDiff can efficiently identify the most important tokens to retain. Notably KeyDiff does not rely on attention scores, allowing the use of optimized attention mechanisms like FlashAttention. Under a strict memory allowance, we demonstrate the effectiveness of KeyDiff for the Llama and Qwen model families by observing a performance gap of less than 0.04\% with 8K cache budget (~23\% KV cache reduction) from the non-evicting baseline on LongBench for Llama 3.1-8B and Llama 3.2-3B. We also observe near baseline performance for Deepseek-R1-Distill-Llama-8B on the Math500 reasoning benchmark and decrease end-to-end inference latency by up to 30\% compared to the other token-eviction methods.

---

## 论文详细总结（自动生成）

# 论文结构化总结

## 1. 核心问题与整体含义（研究动机和背景）
- **问题**：长上下文 LLM 推理中，KV 缓存内存占用随输入线性增长，成为资源受限环境（如边缘设备）的瓶颈。现有缓存驱逐方法（如 H2O、TOVA、SnapKV）依赖注意力分数，需要全 prompt 注意力，不适用于块式流式处理，且计算注意力分数本身代价高。
- **背景**：块式逐块推理可满足严格内存约束，但注意力分数在局部块中无法反映全局重要性，导致现有方法性能下降。作者观察到几何上独特的键（低平均余弦相似度）往往获得高注意力分数，据此提出基于键相似性的驱逐方法。

## 2. 方法论
### 核心思想
- 利用键的独特性（低余弦相似度）作为 token 重要性的代理，无需计算注意力分数。
### 关键技术细节
- **KeyDiff 算法**：  
  1. 对缓存中所有键计算两两余弦相似度矩阵 CosSim(K)，然后求和（与全 1 向量相乘）。  
  2. 选择负余弦相似度最大的 N 个键（即总相似度最小的键）保留。  
- **高效变体**：  
  - 用缓存的键均值 \(\mu(K)\) 作为锚点，计算每个键与锚点的余弦相似度，取其最小的 N 个。复杂度 O(n)，与块大小和缓存预算线性相关。  
  - 可选保留最近 token 的滑动窗口（如 10%-20% 预算），提升推理和代码任务性能。  
- **理论支撑**：  
  - Lemma 3.1 将注意力权重 w 与键-查询余弦相似度下界关联。  
  - Theorem 3.2 将键-均值余弦相似度与注意力权重负相关，表明 KeyDiff 选择的键最可能对齐查询。

## 3. 实验设计
### 数据集 / 场景
- **Needle-In-a-Haystack**：事实检索，文档长度 1k-30k 字符，针深度变化。
- **LongBench**（多任务英文子集）：包含单/多文档 QA、摘要、小样本学习、合成、代码等 21 个任务，51% 的 prompt 长度超过 8K。
- **Math-500**：数学推理基准，随机采样 5 次，使用 Top-p=0.95，温度=0.95 生成。
### 对比方法
- H2O、TOVA、SnapKV、Sink Attention（StreamingLLM）、KeyL2Norm、无驱逐基线。
### 模型
- Llama 3.1-8B-Instruct、Llama 3.2-3B-Instruct、Qwen 2.5-3B/7B-Instruct、DeepSeek-R1-Distill-Llama/Qwen-8B/7B。
### 设置
- 块大小 B=128（主实验），对比 B=64、256。
- 缓存预算 2K、4K、6K、8K。
- 使用贪婪解码（LongBench）和采样（Math-500）。

## 4. 资源与算力
- 所有实验在 **NVIDIA A100 80GB GPU** 上运行。
- 未明确说明训练时长、GPU 数量或总计算量（论文未涉及训练，仅推理）。

## 5. 实验数量与充分性
- **Needle-In-a-Haystack**：1 个模型（Llama 3.2-3B），缓存 6K，对比 4 种方法，展示不同长度/深度的热力图。
- **LongBench**：完整 21 个任务，2 个模型（Llama 8B/3B），4 个缓存预算，5 种对比方法 + 自身消融，共约 2×4×6×21≈1008 个指标（部分省略）。额外报告了 Qwen 3B/7B 结果、不同块大小、滑动窗口组合。
- **Math-500**：2 个蒸馏模型（Llama-8B、Qwen-7B），5 种随机种子，2 种方法 + 无驱逐基线，3 种最大生成长度，内含子集分析。
- **消融实验**：锚点选择（均值 vs 中位数 vs 两两）、相似度度量（余弦 vs 点积 vs 欧氏距离）、滑动窗口比例（10%/20%）。
- **补充实验**：Phonebook Lookup、RULER 基准、Android 端侧延迟。
- **评析**：实验覆盖多模型、多任务、多种约束条件，比较方法全面，控制变量合理，统计信息充分（随机采样 5 次）。但未提供误差棒或置信区间（LongBench 为确定性贪婪解码）。整体充分、客观、公平。

## 6. 主要结论与发现
- KeyDiff 在严格缓存约束下显著优于所有对比方法，在 LongBench 上 8K 预算时与无驱逐基线准确率差距 < 0.04%（Llama 8B/3B），6K 预算时差距约 1.5%。
- 在 Math-500 推理任务上，KeyDiff 搭配滑动窗口可达与无驱逐基线接近甚至略优的准确率，并优于 SnapKV。
- 端到端推理延迟（TTFT）相比 TOVA 和 SnapKV 降低约 30%，因为 KeyDiff 不依赖注意力分数，可与 FlashAttention 结合。
- 消融验证余弦相似度优于点积和欧氏距离；锚点选择对结果不敏感。

## 7. 优点
- **创新性**：首次系统性地利用键几何独特性（低余弦相似度）作为 token 重要性信号，而非注意力分数。
- **理论支撑**：提供 Lemma 和 Theorem 解释为何低余弦相似度键对应高注意力权重的查询对齐。
- **高效性**：O(n) 复杂度，避免材料化注意力矩阵，兼容 FlashAttention，显著降低延迟。
- **鲁棒性**：在块式推理下保持良好性能，对锚点选择不敏感，可自然地集成滑动窗口。
- **全面验证**：覆盖检索、综合长文本、推理等场景，跨模型家族（Llama、Qwen、DeepSeek-R1 蒸馏）。
- **实际意义**：适合于边缘设备等资源受限场景，同时保持高准确率。

## 8. 不足与局限
- **架构限制**：仅实验于 GQA 架构（Llama、Qwen），未评估 MLA（如 DeepSeek-V2）等变体。作者在结论中承认这是未来工作。
- **性能下降情况**：在 Qwen-7B 蒸馏模型上，KeyDiff 表现略逊于无驱逐基线（但与其他方法持平），可能因更高 KV 压缩比使驱逐更敏感。
- **Needle-In-a-Haystack**：随上下文超过 20k 字符，KeyDiff 精度开始落后于无驱逐基线（但仍优于对比方法）。
- **代码未开源**：论文未提供开源实现，可能影响复现性（但方法描述足够详细）。
- **GPU 单一**：仅使用 NVIDIA A100，未验证其他硬件（如 AMD、Apple Silicon）的延迟行为。
- **缺乏统计显著性报告**：LongBench 为确定性贪婪解码，但 Math-500 的 5 次采样未给出置信区间或标准差。

（完）
