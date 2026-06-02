---
title: On Reasoning Strength Planning in Large Reasoning Models
title_zh: 论大型推理模型中的推理强度规划
authors: "Leheng Sheng, An Zhang, Zijian Wu, Weixiang Zhao, Changshuo Shen, Yi Zhang, Xiang Wang, Tat-Seng Chua"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=H26A7cl91u"
tags: ["query:key-tokens"]
score: 8.0
evidence: 通过激活大小因果追踪推理token数量
tldr: 大型推理模型（LRM）在生成前即在激活中预先规划推理强度（即推理token数量），且该强度由一个预分配方向向量的大小因果控制。本研究从模型激活视角揭示了这一现象的机制，为因果追踪推理token提供了新见解。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-neurips-2025-h26a7cl91u/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1439, \"height\": 524, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-h26a7cl91u/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1410, \"height\": 301, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-h26a7cl91u/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1445, \"height\": 456, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-h26a7cl91u/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1446, \"height\": 306, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-h26a7cl91u/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1452, \"height\": 297, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-h26a7cl91u/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1454, \"height\": 326, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-h26a7cl91u/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1448, \"height\": 335, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-h26a7cl91u/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1448, \"height\": 456, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-h26a7cl91u/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1312, \"height\": 503, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-h26a7cl91u/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1389, \"height\": 509, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-h26a7cl91u/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1438, \"height\": 180, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-h26a7cl91u/fig-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1422, \"height\": 276, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-h26a7cl91u/fig-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1183, \"height\": 321, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-h26a7cl91u/fig-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 1192, \"height\": 486, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-h26a7cl91u/fig-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 1181, \"height\": 327, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-h26a7cl91u/fig-016.webp\", \"caption\": \"\", \"page\": 0, \"index\": 16, \"width\": 1194, \"height\": 332, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-h26a7cl91u/fig-017.webp\", \"caption\": \"\", \"page\": 0, \"index\": 17, \"width\": 1187, \"height\": 373, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-h26a7cl91u/fig-018.webp\", \"caption\": \"\", \"page\": 0, \"index\": 18, \"width\": 1047, \"height\": 321, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-h26a7cl91u/fig-019.webp\", \"caption\": \"\", \"page\": 0, \"index\": 19, \"width\": 1455, \"height\": 321, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-h26a7cl91u/fig-020.webp\", \"caption\": \"\", \"page\": 0, \"index\": 20, \"width\": 1453, \"height\": 323, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-h26a7cl91u/fig-021.webp\", \"caption\": \"\", \"page\": 0, \"index\": 21, \"width\": 1441, \"height\": 453, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-h26a7cl91u/fig-022.webp\", \"caption\": \"\", \"page\": 0, \"index\": 22, \"width\": 1182, \"height\": 374, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-h26a7cl91u/fig-023.webp\", \"caption\": \"\", \"page\": 0, \"index\": 23, \"width\": 1403, \"height\": 1682, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-neurips-2025-h26a7cl91u/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1031, \"height\": 445, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-h26a7cl91u/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 887, \"height\": 216, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-h26a7cl91u/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1177, \"height\": 745, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-h26a7cl91u/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1313, \"height\": 603, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-h26a7cl91u/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1310, \"height\": 595, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-h26a7cl91u/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1311, \"height\": 452, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-h26a7cl91u/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 813, \"height\": 110, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-h26a7cl91u/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 555, \"height\": 203, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-h26a7cl91u/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 751, \"height\": 104, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-h26a7cl91u/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1310, \"height\": 369, \"label\": \"Table\"}]"
motivation: 解释LRM自动分配推理token数量的内在机制。
method: 分析模型激活，发现预分配方向向量大小因果控制推理token数。
result: 验证了推理token数量在激活中可预测且受向量大小因果控制。
conclusion: LRM通过激活中的方向向量预规划推理强度，实现难度感知。
---

## Abstract
Recent studies empirically reveal that large reasoning models (LRMs) can automatically allocate more reasoning strengths (\ie the number of reasoning tokens) for harder problems, exhibiting difficulty-awareness for better task performance.
While this automatic reasoning strength allocation phenomenon has been widely observed, its underlying mechanism remains largely unexplored. 
To this end, we provide explanations for this phenomenon from the perspective of model activations.
\textbf{We find evidence that LRMs pre-plan the reasoning strengths in their activations even before generation, with this reasoning strength causally controlled by the magnitude of a pre-allocated directional vector.}
Specifically, we show that the number of reasoning tokens is predictable solely based on the question activations using linear probes, indicating that LRMs estimate the required reasoning strength in advance.
We then uncover that LRMs encode this reasoning strength through a pre-allocated directional vector embedded in the activations of the model, where the vector’s magnitude modulates the reasoning strength. 
Subtracting this vector can lead to reduced reasoning token number and performance, while adding this vector can lead to increased reasoning token number and even improved performance.
We further reveal that this direction vector consistently yields positive reasoning length prediction, and it modifies the logits of end-of-reasoning token \texttt{</think>} to affect the reasoning length.
Finally, we demonstrate two potential applications of our findings: overthinking behavior detection and enabling efficient reasoning on simple problems.
Our work provides new insights into the internal mechanisms of reasoning in LRMs and offers practical tools for controlling their reasoning behaviors.
Our code is available at \url{https://anonymous.4open.science/r/LRM-plans-CoT-7E04}.

---

## 论文详细总结（自动生成）

# 详细中文总结

## 1. 论文的核心问题与整体含义（研究动机和背景）
- **研究动机**：大型推理模型（LRMs）能根据问题难度自动分配推理强度（即推理 token 数量），表现出难度感知能力，但这一现象的底层机制尚不清楚。
- **核心问题**：LRMs 是否在生成第一个推理 token 之前就已规划好推理强度？如果如此，这种规划以何种形式编码在模型内部？
- **整体含义**：从模型激活（activations）视角揭示了 LRMs 预规划推理强度，并通过预分配方向向量的大小进行因果控制，为理解和操控推理行为提供了新途径。

## 2. 论文提出的方法论（核心思想、关键技术细节、公式或算法流程）
- **核心思想**：假设 LRMs 在输入问题后、生成答案前，已将所需的推理强度以线性方向向量形式编码在残差流激活中。
- **关键技术细节**：
  - **线性探针（Linear Probe）**：在 `<think>` token 位置提取激活 $h^{(l)} \in \mathbb{R}^d$，训练 Lasso 回归模型 $\hat{Y} = H^{(l)}W^{(l)} + b^{(l)}$ 预测推理 token 数量 $Y$，损失函数含 $L_1$ 正则项。通过相关系数评估预测能力。
  - **差异均值法（Difference-in-Means）**：对不同难度等级（1~5）的问题激活计算均值差，得到四个预分配向量 $r^{(l)}_{i\leftarrow1}$。验证这些向量方向高度相似（余弦相似度 ~0.99），表明存在单一共享方向。
  - **激活操控（Activation Steering）**：将平均向量 $\overline{r^{(l)}}$ 以不同强度 $\lambda$ 叠加到原始激活 $h^{(l)}$：$h^{(l)'} = h^{(l)} + \lambda \overline{r^{(l)}}$，观察推理 token 数量和性能的变化，验证因果性。
- **算法流程**：① 提取问题激活 → ② 训练线性探针 → ③ 计算不同难度的差异向量并求平均 → ④ 注入向量进行因果干预 → ⑤ 分析 logits 变化。

## 3. 实验设计（数据集、场景、基准、对比方法）
- **主要数据集**：MATH（分 5 个难度等级），MATH500、AIME2024、OlympiadBench（用于评估性能）、MMLU（一般语言理解）、AlpacaEval（过思考检测）。
- **模型**：DeepSeek-R1-Distill-Qwen 系列（1.5B、7B、14B、32B）及 QwQ-32B。附录额外验证了 DeepSeek-R1-Distill-Llama-8B。
- **基准与对比方法**：
  - 线性探针预测与实际 token 数的相关性（Pearson r）。
  - 不同 steering 强度 ($\lambda$ 从 -0.2 到 0.2) 下推理 token 数、答案 token 数、准确率的变化。
  - 对比了直接倍乘 `</think>` logits（$\gamma$ 因子）的效果，说明单纯的 logits 修改不足以稳定控制。
  - 过思考检测：将普通问题通过过思考攻击构造为过思考问题，比较预测 token 数的差异。

## 4. 资源与算力
- 实验使用 **8 张 NVIDIA A100 GPU**。
- 总计算资源约 **80 A100 GPU 天**，主要消耗在答案生成（使用 vLLM 加速）。
- 附录中还注明温度设为 0.6，最大生成长度 16,384，rollout 次数为 8。

## 5. 实验数量与充分性
- **实验数量**：涵盖 5 种不同尺寸/类型的 LRM，4 个数学推理基准（MATH500、AIME、OlympiadBench、GPQA diamond），2 个通用基准（MMLU、AlpacaEval），以及代码生成基准（LiveCodeBench）。每条数据采用 8 次 rollout 平均。
- **充分性**：
  - 在主发现上（可预测性、方向向量存在、因果性）提供了层分析、不同模型、不同数据集的重复验证，结果趋势一致。
  - 对 logits 机制进行了多角度检验（`</think>` token 与其他 token 对比、推理相关 token 变化）。
  - 消融实验：用直接倍乘 `</think>` logits 对比，证明不是简单 logits 变化。
  - **不足**：主要基于 Qwen 系列，仅附录补充了 Llama 骨干模型；未探索更复杂探针（如 MLP）；实验主要集中在数学和部分通用任务，覆盖领域有限。

## 6. 论文的主要结论与发现
1. **推理强度可预判**：线性探针仅凭问题激活即可预测推理 token 数，相关系数超过 0.8，且随层深增加而提高。
2. **存在预分配方向向量**：不同难度问题的激活差异向量方向高度一致（余弦相似度 >0.9），且向量范数与推理 token 数正相关。
3. **方向向量因果控制推理强度**：通过激活注入（steering）可有效增加/减少推理 token 数，进而影响性能；适度正向 steering 甚至能提升性能。
4. **控制机制通过修改 `</think>` logits**：正 steering 降低 `</think>` 的 logits（更难生成），延长推理；负 steering 则相反。向量对 `</think>` 的影响显著大于其他 token。
5. **潜在应用**：可利用预测器提前检测过思考；通过负 steering 显著减少简单问题的推理 token 数而不损害性能，实现高效推理。

## 7. 优点（方法或实验设计上的亮点）
- **新颖视角**：首次从模型激活层面揭示 LRM 推理强度预规划的机制，填补了理解自动分配现象的空缺。
- **简洁而有效的方法**：线性探针 + 差异均值法 + 激活注入三者组合，既验证了存在性也建立了因果性，方法易于复现和扩展。
- **多形态证据**：不仅展示了预测相关性，还通过操控向量验证因果性，进一步探究 logits 机制，证据链完整。
- **实用潜力**：过思考检测和高效推理两个应用展示了成果的实际价值，且有案例直观展示。

## 8. 不足与局限（包括实验覆盖、偏差风险、应用限制等）
- **探针选择局限**：仅使用线性探针，未探索 MLP 等更复杂架构是否可获更好预测。
- **模型覆盖有限**：核心实验基于 Qwen 系列，虽补充了 Llama 骨干变体，但未验证其他主流 LRM（如 GPT 系列、Claude 系列）的泛化性。
- **领域偏差**：主要聚焦数学推理，其他复杂推理任务（如科学问答、逻辑推理）仅初步涉及，结论的广泛性需进一步验证。
- **负效应风险**：论文指出操控方向向量可能被恶意用于后门攻击，造成推理速度大幅减慢，存在安全隐患。
- **应用限制**：过思考检测和高效推理仅展示了潜力，尚未形成完整可部署方案，需要更多工程化努力。

（完）
