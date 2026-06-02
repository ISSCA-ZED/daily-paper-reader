---
title: "The First Few Tokens Are All You Need: An Efficient and Effective Unsupervised Prefix Fine-Tuning Method for Reasoning Models"
title_zh: 仅需前几个Token：一种高效且有效的无监督前缀微调推理方法
authors: "Ke Ji, Jiahao Xu, Tian Liang, Qiuzhi Liu, Zhiwei He, Xiaoyuan Liu, Xingyu Chen, Junying Chen, Benyou Wang, Zhaopeng Tu, Haitao Mi, Dong Yu"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=1SCMFCGliM"
tags: ["query:key-tokens"]
score: 8.0
evidence: 证明初始前缀token（少至8个）对推理性能的重要性
tldr: 针对推理模型微调需大量标注数据或采样的问题，本文提出无监督前缀微调方法UPFT。该方法基于前缀自一致性现象——不同解法共享初始推理步骤，仅利用前几个token（少至8个）进行训练即可达到与有监督微调相当的性能。实验证明了初始前缀token在推理过程中具有关键重要性，为衡量token重要性提供了简洁有效的指标。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-neurips-2025-1scmfcglim/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1449, \"height\": 638, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-1scmfcglim/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 620, \"height\": 525, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-1scmfcglim/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1274, \"height\": 560, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-1scmfcglim/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1452, \"height\": 240, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-1scmfcglim/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1364, \"height\": 2160, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-neurips-2025-1scmfcglim/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1457, \"height\": 879, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-1scmfcglim/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1444, \"height\": 725, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-1scmfcglim/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1006, \"height\": 415, \"label\": \"Table\"}]"
motivation: 推理模型微调通常需要标注数据或大量采样，成本高。
method: 利用前缀自一致性，仅对初始前缀子串（最少8个token）进行无监督微调。
result: 在推理基准上达到与拒绝采样微调相当的精度，同时大幅减少训练时间。
conclusion: 揭示了初始前缀token的关键重要性，并提供了一种轻量级训练方法。
---

## Abstract
Improving the reasoning capabilities of large language models (LLMs) typically requires supervised fine-tuning with labeled data or computationally expensive sampling. We introduce Unsupervised Prefix Fine-Tuning (UPFT), which leverages the observation of Prefix Self-Consistency -- the shared initial reasoning steps across diverse solution trajectories -- to enhance LLM reasoning efficiency. By training exclusively on the initial prefix substrings (as few as 8 tokens), UPFT  removes the need for labeled data or exhaustive sampling. Experiments on reasoning benchmarks show that UPFT matches the performance of supervised methods such as Rejection Sampling Fine-Tuning, while reducing training time by 75\% and sampling cost by 99\%. Further analysis reveals that errors tend to appear in later stages of the reasoning process and that prefix-based training preserves the model’s structural knowledge. This work demonstrates how minimal unsupervised fine-tuning can unlock substantial reasoning gains in LLMs, offering a scalable and resource-efficient alternative to conventional approaches.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 论文的核心问题与整体含义（研究动机和背景）
- **问题**：提升大型语言模型（LLM）的推理能力通常需要依赖人工标注数据或大量采样过滤（如拒绝采样微调 RFT），这些方法训练成本高、资源消耗大，且难以在无标注场景下应用。
- **动机**：观察到不同推理轨迹在初始步骤上高度一致，即**前缀自一致性**（Prefix Self-Consistency）现象。基于此，论文提出仅利用模型生成的初始前缀子串（少至 8 个 token）进行无监督微调，以极低的成本提升推理性能，摆脱对标注数据或大规模采样的依赖。
- **整体含义**：这项工作提供了一种高效、资源节约的无监督微调替代方案，在保持或接近监督方法性能的同时大幅降低计算开销。

## 2. 论文提出的方法论
### 核心思想
- **前缀自一致性**：不同解法轨迹共享相同的前缀（初始推理步骤），表明这些早期 token 包含了关键的推理信号。
- **无监督前缀微调 (UPFT)**：仅对模型生成的初始前缀 `r_{<t}` 进行监督微调（SFT），无需依据最终答案是否正确进行过滤。
- **结构微调（Structure Tuning）**：为防止模型丢失完整输出格式和指令跟随能力，额外使用小比例（通常 10%）的全轨迹无监督 SFT 进行联合训练。

### 关键技术细节
- 给定数据集 `(x, y)`（仅需输入 x，无需正确答案），从模型中采样前缀 `r_{<t} ~ p(·|x; θ)`。
- 优化目标：最大化前缀的对数似然 `log p(r_{<t} | x; θ)`，同时联合结构微调项。
- **贝叶斯视角推导**：将完整目标函数分解为前缀覆盖率和前缀准确率的期望下界，说明通过提高前缀覆盖（共享前缀）可更有效地优化下界。
- 超参数：前缀长度 t 需根据模型调整（如 Llama-3.1-8B 用 8 tokens，Qwen-Math-7B 用 32 tokens，DeepSeek-R1-Distill-Qwen-7B 用 128 tokens）。结构微调比例 p 设为 10%（LIMO 数据集为 30%）。

## 3. 实验设计
### 数据集
- **训练集**：
  - PRM-12K（12K 个 MATH 类问题）
  - OMI2（600K 数学指令微调数据）
  - LIMO（819 个高难度问题）
  - U-Hard（100K 困难问题，作者新构建）
- **测试基准**：GSM8K、MATH500、AIME2024、GPQA Diamond（四种推理基准）。

### 对比方法
- **无监督场景**：标准 SFT（使用完整生成序列，无过滤）。
- **监督场景**：RFT（拒绝采样微调，16 个样本过滤正确答案）、V-STaR（训练验证器 + best-of-N 选择）。
- **基线模型**：Llama-3.1-8B-Instruct、Qwen2.5-Math-7B-Instruct、DeepSeek-R1-Distill-Qwen-7B。

### 实验场景
- **无监督采样**：每个问题仅采样 1 个响应，不进行任何正确性过滤。
- **监督采样**：每个问题采样 16 个响应，依据真实答案过滤正确轨迹。

## 4. 资源与算力
- 论文在附录 B 列出了超参数（AdamW 优化器，学习率 1e-6 或 2e-6，warmup 0.03，余弦退火等），但**未明确说明使用的 GPU 型号、数量或具体训练时长**。
- 仅提供了相对效率数据：UPFT 比 SFT 减少 **75% 训练时间**，比 RFT 减少 **99% 采样成本**。以 Qwen-Math-7B 为例，UPFT 所需采样 token 数仅 0.6M，而 RFT 需 51.7M（减少 98.8%）。
- 总体算力信息不足，无法精确复现训练资源。

## 5. 实验数量与充分性
- **实验数量**：覆盖 4 个训练数据集、3 个模型、4 个基准、2 个场景（无监督/监督），以及详细的消融研究（前缀长度、结构微调比例）。
- **充分性**：
  - 对比方法包括 SFT/RFT/V-STaR，涵盖主流基线。
  - 消融实验系统探究了两个关键超参数的影响，并给出了最优设定。
  - 报告了多次实验结果（如不同模型 × 不同数据集），结果一致性较好。
- **客观性与公平性**：设定相同超参数、相同的贪心解码和零样本评估，确保对比公平。
- **潜在不足**：未提供统计误差棒或多次运行的标准差（虽然在 checklist 中声称有误差分析，但正文未展示），实验结果的可重复性验证待加强。

## 6. 论文的主要结论与发现
- **无监督场景**：UPFT 显著优于标准 SFT（例如，在 U-Hard 数据集上，Qwen-Math-7B 的四个基准平均准确率从 51.3% 提升至 54.5%）。
- **监督场景**：UPFT 性能与 RFT/V-STaR 相当甚至略优（DeepSeek-R1-Distill-Qwen-7B 上 UPFT 达 58.7%，RFT 为 57.2%），但采样和训练成本大幅降低。
- **效率优势**：训练序列长度平均减少 82.6%~94.7%，直接带来 6.3~16.7 倍加速。
- **错误分布**：错误倾向于出现在推理后期；前缀微调保留了模型的先验知识。
- **数据集价值**：U-Hard（困难问题）能最大化 UPFT 收益，说明复杂问题提供更丰富的前缀信号。
- **可集成性**：UPFT 可与标签过滤无缝结合，进一步提升准确率（如 DeepSeek-7B 达 58.8%）。

## 7. 优点
- **高效轻量**：仅需极少 token 训练（少至 8 个），训练时间减少 75% 以上，采样成本降低 99%。
- **无监督**：不需要标注数据，仅需问题文本和模型本身，适合现实无标注场景。
- **通用灵活**：适配多种模型架构（通用、数学专用、长推理模型）和不同规模的数据集。
- **理论基础**：从贝叶斯视角推导了前缀覆盖率和准确率的下界，为方法提供了理论支撑。
- **实验全面**：在多模型、多数据集、多基准上验证，包括无监督和监督两个场景。

## 8. 不足与局限
- **算力信息不完整**：未明确说明 GPU 型号、数量、实际训练时间，导致资源评估不透明。
- **实验统计信息不足**：未报告多次运行的误差范围或标准差，统计显著性缺乏证据。
- **模型规模局限**：仅在 7B/8B 级别模型上测试，未在更大规模（如 32B、70B）上验证泛化性。
- **前缀选择策略启发式**：前缀长度 t 基于模型人工调整，未实现自适应或样本无关的选择机制。
- **任务覆盖面窄**：仅聚焦数学（MATH、GSM8K、AIME）和科学（GPQA）推理，未涉及通用推理、代码生成或多语言任务。
- **无监督假设限制**：方法依赖“前缀自一致性”，在初始步骤分歧较大的任务（如创意写作或开放域问答）中可能不适用。
- **未提供开放代码和数据链接**（论文仅说明代码在补充材料，未提供公开仓库），可复现性待提升。

（完）
