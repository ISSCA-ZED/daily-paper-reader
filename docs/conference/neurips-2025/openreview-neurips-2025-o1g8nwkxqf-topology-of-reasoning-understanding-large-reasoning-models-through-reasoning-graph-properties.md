---
title: "Topology of Reasoning: Understanding Large Reasoning Models through Reasoning Graph Properties"
title_zh: 推理拓扑：通过推理图属性理解大型推理模型
authors: "Gouki Minegishi, Hiroki Furuta, Takeshi Kojima, Yusuke Iwasawa, Yutaka Matsuo"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=o1g8NWkxqf"
tags: ["query:key-tokens"]
score: 6.0
evidence: 聚类每个推理步骤的隐藏状态表示以分析推理图
tldr: 为理解大型推理模型的内在机制，本工作通过聚类每个推理步骤的隐藏状态表示提取推理图，并系统分析其环度、直径和小世界特性。实验发现蒸馏推理模型表现出显著的循环结构和大直径，揭示了推理过程的结构化特征。该方法从隐藏状态层面展示了推理步骤的拓扑属性，为分析关键token所处的结构位置提供了新视角，但未直接识别关键token本身。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-neurips-2025-o1g8nwkxqf/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1442, \"height\": 487, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-o1g8nwkxqf/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 548, \"height\": 375, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-o1g8nwkxqf/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1442, \"height\": 369, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-o1g8nwkxqf/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1413, \"height\": 686, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-o1g8nwkxqf/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1436, \"height\": 419, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-o1g8nwkxqf/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1436, \"height\": 564, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-o1g8nwkxqf/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1432, \"height\": 359, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-o1g8nwkxqf/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 565, \"height\": 247, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-o1g8nwkxqf/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1448, \"height\": 486, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-o1g8nwkxqf/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1462, \"height\": 666, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-o1g8nwkxqf/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1440, \"height\": 367, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-o1g8nwkxqf/fig-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1413, \"height\": 423, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-o1g8nwkxqf/fig-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1420, \"height\": 426, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-o1g8nwkxqf/fig-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 639, \"height\": 393, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-o1g8nwkxqf/fig-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 1451, \"height\": 492, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-o1g8nwkxqf/fig-016.webp\", \"caption\": \"\", \"page\": 0, \"index\": 16, \"width\": 1445, \"height\": 522, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-neurips-2025-o1g8nwkxqf/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 877, \"height\": 328, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-o1g8nwkxqf/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1450, \"height\": 1884, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-o1g8nwkxqf/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 926, \"height\": 345, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-o1g8nwkxqf/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1178, \"height\": 654, \"label\": \"Table\"}]"
motivation: 大型推理模型成功的内在机制尚不明确，缺乏结构化的分析方法。
method: 提取推理图并分析环度、直径和小世界指数等图属性。
result: 发现蒸馏模型具有更多循环和更大的图直径，呈现小世界特性。
conclusion: 推理图属性揭示了推理步骤的结构模式，有助于理解关键步骤的分布。
---

## Abstract
Recent large-scale reasoning models have achieved state-of-the-art performance on challenging mathematical benchmarks, yet the internal mechanisms underlying their success remain poorly understood. In this work, we introduce the notion of a reasoning graph, extracted by clustering hidden‐state representations at each reasoning step, and systematically analyze three key graph-theoretic properties: cyclicity, diameter, and small-world index, across multiple tasks (GSM8K, MATH500, AIME~2024). Our findings reveal that distilled reasoning models (e.g., DeepSeek-R1-Distill-Qwen-32B) exhibit significantly more recurrent cycles (about 5 per sample), substantially larger graph diameters, and pronounced small-world characteristics (about 6x) compared to their base counterparts. 
Notably, these structural advantages grow with task difficulty and model capacity, with cycle detection peaking at the 14B scale and exploration diameter maximized in the 32B variant, correlating positively with accuracy.  
Furthermore, we show that supervised fine-tuning on an improved dataset systematically expands reasoning graph diameters in tandem with performance gains, offering concrete guidelines for dataset design aimed at boosting reasoning capabilities. By bridging theoretical insights into reasoning graph structures with practical recommendations for data construction, our work advances both the interpretability and the efficacy of large reasoning models.

---

## 论文详细总结（自动生成）

# 中文论文总结

## 1. 核心问题与研究动机
大型推理模型（如 DeepSeek-R1）在数学推理任务中取得了突破性进展，但其内部机制仍不清晰。现有解释多停留在行为层面（如“aha moment”），缺乏结构化的定量分析。本文提出**推理图（Reasoning Graph）** 概念，通过提取并分析推理步骤隐藏状态构成的图结构属性（循环、直径、小世界特性），揭示推理模型性能提升的内在原因。

## 2. 方法论

### 核心思想
- 将模型推理过程视为在隐空间中的节点间路径。
- 对每一步（按换行分隔的推理片段）的最后一层隐藏状态取均值，并用 K-means 聚类（K=200）得到图节点（每个聚类质心对应一个节点）。
- 将模型输出序列中相邻步骤分配到最近质心，形成有向边，构建每个样本的推理图 G=(V,E)。

### 关键图属性测量
- **循环（Cycle）**：检测重复访问同一节点（排除连续相同节点），定义循环检测比例（含至少一个循环的样本比例）和循环数（单个节点最大重复访问次数）。
- **直径（Diameter）**：使用 Dijkstra 算法计算图中所有可达节点对之间的最短路径最大值，反映模型探索的广度。
- **小世界指数（Small-World Index）**：将图无向化后计算聚类系数 C 和平均路径长度 L，并与等效随机图（Erdős–Rényi）的 C_rand、L_rand 比较：S = (C/C_rand) / (L/L_rand)。S 越大表示局部聚类密集且全局连通性高。

### 默认实验设置
- 提取隐藏层为最后 90% 深度（如 64 层模型中为第 58 层）。
- 聚类数 K=200。

## 3. 实验设计

### 数据集与 Benchmark
- 主要数学任务：GSM8K（简单）、MATH500（中等）、AIME 2024（困难）。
- 非数学辅助任务：StrategyQA（多跳问答）、LogicalDeduction（BIG-Bench 逻辑推理）。

### 对比模型
- **推理模型**：DeepSeek-R1-Distill-Qwen 系列（1.5B、7B、14B、32B）。
- **基础模型**：对应原始 Qwen2.5 / Llama-3.1 等同规模模型。
- **微调基模型**：Qwen2.5-32B-Instruct，使用 s1 数据集（v1.0 与 v1.1）进行监督微调。

### 对比方法
- 推理模型 vs 基础模型（各规模）。
- 不同 SFT 数据质量（s1 v1.0 vs v1.1，以及 LIMO 对比）。
- 不同层深度（0.1–0.9 比例）与不同聚类数 K（50/100/200）的消融实验。

## 4. 资源与算力
- **训练**：8× NVIDIA H200 GPU，使用 FSDP 全分片数据并行，bf16 精度。
- **推理**：1× NVIDIA H200 GPU。
- 未明确报告训练总时长，但给出了微调超参数（5 epochs、学习率 1e-5、余弦衰减等）。

## 5. 实验数量与充分性
- 覆盖 **3 个主要数学数据集 + 2 个非数学任务**，验证通用性。
- 比较了 **4 种模型规模**（1.5B–32B）下的推理图属性。
- 进行了 **层深度、聚类数 K 等超参数消融**，结果稳定。
- **SFT 实验**：对比两个版本数据（v1.0 与 v1.1）在不同训练步数下的直径变化，并额外对比 LIMO 数据。
- 实验设计客观、公平，重复性良好（代码开放）。

## 6. 主要结论与发现

1. **循环结构**：推理模型显著多于基础模型（约 5 个循环/样本），循环检测比例随任务难度递增（GSM8K→MATH500→AIME 2024），且随模型规模增大而上升（14B 达 100%，但存在语言混合导致假循环）。
2. **图直径**：推理模型直径远大于基础模型，且随层深度增加而增大，表明模型在更深层探索更广的推理状态空间。
3. **小世界特性**：推理模型具有更高的聚类系数和更长的平均路径长度，小世界指数约为基础模型的 6 倍，有利于局部细化和跨区域跳转。
4. **模型规模影响**：32B 模型直径最大、循环数最多、小世界指数最高，准确率也最高；14B 虽循环检测比例最高但因语言混合导致性能下降。
5. **SFT 数据质量**：高质量数据（s1 v1.1）诱导出更大的图直径，且直径随训练步长增加，与性能提升正相关。
6. **解释已知现象**：循环结构对应“aha moment”（自我修正）；冗余循环可解释“过度思考”；极大直径可能对应“思考不足”。

## 7. 方法的优点

- **新颖性**：首次从图论视角系统分析推理模型内部状态结构，将行为现象（aha moment）量化。
- **可解释性**：三种图属性（循环、直径、小世界）都能直观对应推理行为的改进。
- **实用性**：为 SFT 数据集设计提供可量化指标（图直径），指导更有效的数据构建。
- **鲁棒性**：跨不同任务、模型规模、层深度等实验一致性强。

## 8. 不足与局限

- **未触及细粒度机制**：仅分析隐藏状态序列的宏观图结构，未进行特征级（如稀疏自编码器）或电路级（如注意力头）分析。
- **训练动态不明**：未解释这些图特性在训练过程中如何涌现（如 RL 训练中的变化）。
- **应用指导有限**：虽提供数据质量指标，但未给出直接用于构建更优模型的算法化建议。
- **计算资源限制**：仅使用 8 GPU 进行单次微调，未报告大规模重复实验误差。
- **语言混合问题**：在 14B 模型中检测到语言切换导致的虚假循环，需进一步区分有益循环与噪声。

（完）
