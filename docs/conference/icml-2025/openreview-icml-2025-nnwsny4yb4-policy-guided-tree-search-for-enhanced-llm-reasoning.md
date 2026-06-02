---
title: Policy Guided Tree Search for Enhanced LLM Reasoning
title_zh: 策略引导树搜索增强大语言模型推理
authors: Yang Li
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=NNWSNy4YB4"
tags: ["query:key-tokens"]
score: 6.0
evidence: 策略引导的树搜索用于推理序列
tldr: 当前大语言模型在复杂推理任务中面临启发式依赖和计算开销大的问题。本文提出Policy-Guided Tree Search (PGTS)框架，通过强化学习与树搜索结合，学习一个策略动态决定推理路径的扩展或回溯。实验表明该方法在数学推理和逻辑推理任务上有效，提升了推理效率。
source: ICML-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2025-nnwsny4yb4/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 863, \"height\": 372, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-nnwsny4yb4/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1500, \"height\": 422, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-nnwsny4yb4/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 820, \"height\": 361, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-nnwsny4yb4/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1422, \"height\": 1368, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-nnwsny4yb4/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1319, \"height\": 1780, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-nnwsny4yb4/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1302, \"height\": 1982, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-nnwsny4yb4/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1324, \"height\": 2212, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-icml-2025-nnwsny4yb4/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1750, \"height\": 804, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-nnwsny4yb4/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 867, \"height\": 255, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-nnwsny4yb4/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 698, \"height\": 345, \"label\": \"Table\"}]"
motivation: 大语言模型在复杂推理中依赖预定义启发式和穷举搜索，效率低下。
method: 提出PGTS，结合强化学习和树搜索，学习动态策略指导推理路径探索。
result: 在数学推理和逻辑推理任务上验证了有效性。
conclusion: PGTS通过学习策略消除手动启发式，提升了推理效率。
---

## Abstract
Despite their remarkable capabilities, large language models often struggle with tasks requiring complex reasoning and planning. While existing approaches like Chain-of-Thought prompting and tree search techniques show promise, they are limited by their reliance on predefined heuristics and computationally expensive exploration strategies. We propose Policy-Guided Tree Search (PGTS), a framework that combines reinforcement learning with structured tree exploration to efficiently navigate reasoning paths. Our key innovation is a learned policy that dynamically decides between expanding, branching, backtracking, or terminating exploration, eliminating the need for manual heuristics or exhaustive search. Experiments across mathematical reasoning, logical deduction, and planning benchmarks demonstrate that PGTS achieves superior reasoning performance while significantly reducing computational costs compared to existing methods. These results establish PGTS as a scalable and effective solution for tackling complex reasoning tasks with LLMs.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 核心问题与整体含义
- **研究动机**：大型语言模型（LLM）在复杂推理和规划任务中表现不佳。现有的方法（如思维链提示、树搜索）依赖预定义启发式规则或穷举搜索，导致计算开销大、适应性差。
- **整体含义**：本文提出Policy-Guided Tree Search (PGTS)，通过强化学习训练一个策略，动态决定何时扩展、分支、回溯或终止探索，从而高效导航推理路径，消除对手动启发式的依赖，提升推理性能并降低计算成本。

## 2. 方法论
- **核心思想**：将推理过程建模为树搜索马尔可夫决策过程（TS-MDP），策略网络基于图Transformer（GPS架构）处理部分探索的推理树，学习四种动作：
  - **Expand**：从当前节点生成下一个推理步骤
  - **Branch**：探索当前节点的兄弟节点（替代路径）
  - **Backtrack**：回退到之前节点（可回退多步）
  - **Terminate**：结束搜索（当得到满意答案时）
- **关键技术细节**：
  - 状态表示：节点特征来自LLM的隐藏状态（最后token的最后一层），边特征为即时奖励（基于步骤似然）
  - 动作约束：通过深度和宽度限制保证有限动作空间，并用二进制掩码禁止无效动作
  - 奖励设计：包含任务相关奖励和动作成本（cost），平衡准确性与效率
  - 训练算法：使用Proximal Policy Optimization (PPO)，以最大化累积奖励为目标，并行收集轨迹并更新策略
- **算法流程**（文字说明）：
  - 初始化策略和价值网络
  - 循环采样任务，从根节点开始
  - 在每个时间步，计算有效动作掩码，策略输出动作概率，采样动作执行，获得下一状态和奖励
  - 存储轨迹，计算折扣回报和优势
  - 使用PPO更新策略和价值网络（包含熵正则化）

## 3. 实验设计
- **数据集与场景**：
  - 数学推理：GSM8K、MATH500、AQUA
  - 常识推理：StrategyQA
  - 逻辑推理：PrOntoQA、GPQA
  - 规划任务：Blocksworld（4步和8步）
- **基准方法**：
  - 主要对比：Chain-of-Thought (CoT) 和 Monte Carlo Tree Search (MCTS)
  - 增强：自一致性（SC）用于CoT和PGTS；MCTS报告最佳路径、加权聚合及Oracle（使用真实答案）
- **实验设置**：
  - 使用LLaMA3.1-8B和LLaMA3.1-70B作为基础模型，推理温度0.6，top-p=0.9
  - PGTS策略使用1000个训练样本（数据集训练集），树宽度限制为4
  - 消融实验：训练样本数（图3展示收敛）、树宽度（表2）、策略网络变体（表3：GPS、SAN、SLM、LLM Agent）

## 4. 资源与算力
- 论文未明确说明训练所用的GPU型号、数量及训练时长。仅提到使用LLaMA3.1-8B和70B进行推理，策略网络训练使用1000个样本，架构轻量（两个GPS层+线性层），因此训练资源需求不大。但具体硬件细节缺失。

## 5. 实验数量与充分性
- 实验覆盖7个数据集（含多个子任务），涉及数学、常识、逻辑、规划四种推理类型，共约**20+组**对比结果（含不同方法和自一致性设置）。
- 消融实验包括：
  - 训练样本数对性能的影响（图3）
  - 树宽度对准确性和token开销的影响（表2）
  - 四种策略网络架构对比（GPS vs SAN vs SLM vs LLM Agent）
- 充分性与客观性：
  - 对比了多个强基线（CoT、MCTS及其变体），且对MCTS提供了Oracle上界
  - 实验设计较全面，但GPQA任务上PGTS表现明显低于MCTS，说明在某些复杂任务上仍存差距
  - 训练数据量固定为1000样例，未讨论过拟合或数据量更少时的泛化性

## 6. 主要结论
- PGTS在多数任务上显著优于CoT（如MATH上从34.40%提升至41.00%），且计算成本远低于MCTS（如GSM8K仅使用CoT 1.29倍的token，而MCTS需13.33倍）
- 结合自一致性（SC）后，PGTS进一步提升性能，并在部分任务上超越MCTS（如Blocksworld 8步：PGTS-SC 6.99% vs MCTS 6.29%）
- PGTS能有效缓解“过度思考”问题（通过终止动作及早停止），同时动态平衡探索与利用

## 7. 优点
- **无需手动启发式**：学习策略自动适应不同任务，无需预定义搜索规则
- **无需真实推理链标注**：训练时仅需使用任务奖励（可通过最终答案监督），减轻数据依赖
- **计算高效**：相比MCTS大幅减少token使用量（树搜索更聚焦于高价值路径）
- **可扩展性**：策略网络基于图神经网络，可自然处理不同大小的推理树；框架与具体LLM解耦
- **消融实验完整**：验证了策略网络组件、树宽度、训练数据量等关键因素的作用

## 8. 不足与局限
- **推理链忠实性未保证**：论文指出不生成必然忠诚于人类理解的推理步骤，存在误导风险，尤其在关键应用中
- **复杂任务性能不足**：在GPQA（高难度综合题）上PGTS明显落后于MCTS，说明策略可能无法充分建模复杂推理的多样性
- **资源信息缺失**：未报告训练硬件和耗时，降低可复现性
- **训练数据量有限**：仅使用1000样本，未探索更大训练集或跨任务泛化的效果
- **中间奖励简单**：当前使用步骤的似然作为即时奖励，未与自评估或过程奖励模型结合，可能错失更丰富的信号
- **未与最先进推理方法比较**：未与o1-like、图思维（GoT）等最新方法对比（但论文2025年接收，可能较新）

（完）
