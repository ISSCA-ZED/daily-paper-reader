---
title: "System-1.5 Reasoning: Traversal in Language and Latent Spaces with Dynamic Shortcuts"
title_zh: System-1.5推理：在语言和潜在空间中通过动态捷径进行遍历
authors: "Xiaoqiang Wang, Suyuchen Wang, Yun Zhu, Bang Liu"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=MNduv07wAu"
tags: ["query:key-tokens"]
score: 8.0
evidence: 使用隐藏状态区分关键推理步骤与辅助步骤
tldr: 针对现有潜在空间推理方法对所有步骤一视同仁、浪费计算资源的问题，本文提出System-1.5推理框架。该方法通过潜在空间中的捷径路径动态分配计算资源，能够区分关键推理步骤与辅助步骤，从而在保持推理质量的前提下大幅提升效率。实验表明该方法在数学推理等任务上显著减少了不必要的计算开销，为基于隐藏状态分析的关键token（步骤）识别提供了有效的技术路线。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-neurips-2025-mnduv07wau/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1436, \"height\": 709, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-mnduv07wau/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1442, \"height\": 721, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-mnduv07wau/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 665, \"height\": 383, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-mnduv07wau/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 676, \"height\": 417, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-neurips-2025-mnduv07wau/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1447, \"height\": 313, \"label\": \"Table\"}]"
motivation: 现有潜在空间推理方法无法区分关键步骤与辅助步骤，导致计算效率低下。
method: 提出System-1.5框架，在潜在空间中通过动态捷径自适应地分配计算资源。
result: 在数学推理任务上显著减少计算开销并保持推理质量。
conclusion: 实现了基于隐藏状态的关键推理步骤区分，为高效推理提供了新范式。
---

## Abstract
Chain-of-thought (CoT) reasoning enables large language models (LLMs) to move beyond fast System-1 responses and engage in deliberative System-2 reasoning. However, this comes at the cost of significant inefficiency due to verbose intermediate output. Recent latent-space reasoning methods improve efficiency by operating on hidden states without decoding into language, yet they treat all steps uniformly, failing to distinguish critical deductions from auxiliary steps and resulting in suboptimal use of computational resources. In this paper, we propose System-1.5 Reasoning, an adaptive reasoning framework that dynamically allocates computation across reasoning steps through shortcut paths in latent space.Specifically, System-1.5 Reasoning introduces two types of dynamic shortcuts. The model depth shortcut (DS) adaptively reasons along the vertical depth by early exiting non-critical tokens through lightweight adapter branches, while allowing critical tokens to continue through deeper Transformer layers. The step shortcut (SS) reuses hidden states across the decoding steps to skip trivial steps and reason horizontally in latent space. Training System-1.5 Reasoning involves a two-stage self-distillation process: first distilling natural language CoT into latent-space continuous thought, and then distilling full-path System-2 latent reasoning into adaptive shortcut paths (System-1.5 Reasoning).Experiments on reasoning tasks demonstrate the superior performance of our method.
For example, on GSM8K, System-1.5 Reasoning achieves reasoning performance comparable to traditional CoT fine-tuning methods while accelerating inference by over 20× and reducing token generation by 91.0\% on average.

---

## 论文详细总结（自动生成）

# 论文总结：System-1.5 Reasoning: Traversal in Language and Latent Spaces with Dynamic Shortcuts

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **研究动机**：Chain-of-Thought (CoT) 推理虽然能提升 LLM 的 System-2 深思熟虑能力，但会产生冗长的中间输出，导致计算效率低下。近期潜在空间推理方法（如 Coconut、CCoT）通过直接在隐藏状态上运算避免解码为语言，提升效率，但它们对所有推理步骤一视同仁，无法区分关键推导步骤与辅助步骤，造成计算资源的次优分配。
- **核心问题**：能否根据推理步骤的复杂度动态分配计算资源，在保持性能的同时最大化效率？
- **整体含义**：本文提出 System-1.5 Reasoning 框架，在潜在空间中引入自适应捷径路径（深度捷径和步骤捷径），实现类似人类的“快慢思考”结合——非关键步骤快速处理（System-1），关键步骤深入推理（System-2），从而在保持推理质量的同时显著提升推理速度。

## 2. 论文提出的方法论

### 核心思想
- 通过两种动态捷径在潜在空间自适应分配计算：
  - **Depth Shortcut (DS，深度捷径)**：在每个 Transformer 层插入路由器-适配器模块，动态决定 token 是继续经过更深的标准层，还是通过轻量适配器分支提前退出。非关键 token 在浅层退出，关键 token 继续深入。
  - **Step Shortcut (SS，步骤捷径)**：将早期退出的隐藏状态直接复制到下一个解码步骤的同一层，从而跳过步骤间的重新计算，实现水平方向的潜在推理。

### 关键技术细节
- **架构定义**：  
  给定输入序列 X，第 l 层的隐藏状态为 \(h_{l,t}\)。深度捷径输出为适配器输出 \(g_{l-1}(h_{l-1,t})\) 与标准 Transformer 输出 \(f_l(h_{l-1,t})\) 的加权组合，权重由路由器 \(R_l\) 输出 sigmoid 值 \(w\) 决定。训练时加权，推理时根据阈值 \(\lambda_{\text{depth}}\) 二选一。步骤捷径类似，将上一解码步的隐藏状态 \(g_l(h_{l,t-1})\) 引入当前步。
- **两阶段蒸馏训练**：
  1. **语言到潜在对齐 (Language-to-Latent Alignment)**：  
     将教师模型（语言空间 CoT 微调）的最后一层隐藏状态作为目标，通过 MSE 损失对齐学生模型（潜在空间推理）的隐藏状态；同时学生模型仅对最终答案计算 NLL 损失，中间步骤只进行潜在推理。教师模型也通过 CoT 的 NLL 损失进行监督。
  2. **捷径学习 (Shortcut Learning)**：  
     冻结第一阶段训练好的 Transformer 参数，仅训练路由器-适配器模块。利用原子思维分解将 CoT 分解为有向无环图，标记独立节点为非关键步骤、派生节点为关键步骤。然后定义早期退出损失 \(L_{\text{early-exit}}\)，使非关键步骤的 token 尽早退出（权重向浅层倾斜），关键步骤的 token 深入退出（权重向深层倾斜）。同时保留最终答案的 NLL 损失。
- **推理时控制**：通过深度退出阈值 \(\lambda_{\text{depth}}\) 和最大解码步数 \(\lambda_{\text{step}}\) 两个参数灵活调整计算预算，实现可控的测试时缩放。

## 3. 实验设计

- **数据集与场景**：
  - **数学推理**：增强版 GSM8K（约 40 万题）及 OOD 评估集 GSM-HARD（将 GSM8K 数字替换为更大更难的数字）。
  - **常识推理**：StrategyQA（多跳 yes/no 问题），将注释的事实和子问题合并为连贯的 CoT 序列。
  - 每个推理步骤用原子思维分解标注关键性标签（关键/非关键）。
- **基准 (benchmark)**：与以下方法对比：
  - CoT 微调（基线）
  - 语言空间条件计算：LITE、LayerSkip（早期退出）
  - 潜在空间压缩推理：iCoT、Coconut、CODI
  - 潜在空间扩展推理：pause token
- **模型骨干**：GPT-2 124M 和 LLaMA 3.2 1B，确保与各基线公平比较。
- **评估指标**：答案准确率（Exact Match）、解码步数、每步平均 FLOPs 减少率、端到端推理加速比（壁钟时间）。

## 4. 资源与算力

- **GPU 型号**：单张 NVIDIA RTX A5000 (24GB)。
- **训练时长**：LLaMA 3.2 1B 约 26 小时，GPT-2 124M 约 5 小时（均为 8 个 epoch）。
- **超参数**：学习率 2e-5，batch size 2，AdamW 优化器，warmup 6%。
- 论文明确说明了计算资源，但未提及多卡分布式训练或更大型模型的实验，可复现性较好。

## 5. 实验数量与充分性

- **主要实验**：在 GSM8K、GSM-HARD、StrategyQA 三个数据集上进行，对比 7 种基线方法（CoT、LITE、LayerSkip、iCoT、Coconut、CODI、pause token），报告了准确率、步数、FLOPs 减少、加速比。
- **消融实验**（Figure 3）：
  - 比较不同 System-2 学生（Coconut-System-1.5、CODI-System-1.5、本文学生）对最终 System-1.5 性能的影响。
  - 探究联合学习 vs. 分阶段学习、全参数捷径学习 vs. 冻结骨干。
- **可控测试时缩放分析**（Figure 4）：改变深度阈值 \(\lambda_{\text{depth}}\) 和解码步常数 \(\lambda_{\text{step}}\)，观察性能变化，展示 Pareto 边界。
- **公平性与客观性**：各基线使用官方实现或等价设置，骨干模型一致；报告 4 次独立运行的平均结果（附录 B），但未提供误差条。实验覆盖了多个任务和多种对比方法，消融实验充分，结论具有说服力。不足在于未进行更大规模模型（如 7B+）或更多任务（如代码生成、科学推理）的验证。

## 6. 论文的主要结论与发现

- **性能与效率**：System-1.5 在 GSM8K 上准确率 46.94%，与 CoT 的 46.94% 持平，但推理加速 20.27 倍，token 生成减少 91.0%；在 StrategyQA 上准确率 48.61% 超过 CoT 的 47.62%，加速 55.65 倍。
- **优于现有潜在推理方法**：相比 iCoT、Coconut、CODI 和 pause token，System-1.5 在准确率和效率上均更优。
- **两阶段蒸馏有效性**：直接语言到潜在对齐（本文方法）比基于课程学习（如 Coconut）更有效，因为其提供更灵活的潜在结构。联合学习或全参数微调会损害性能，表明 Transformer 参数与路由参数存在优化冲突。
- **可控测试时缩放**：通过调整深度阈值和解耦步数，可以经济地扩展计算，且两个维度对性能敏感，验证了双维自适应的重要性。

## 7. 优点

- **创新性**：首次在潜在推理中同时引入深度和步骤两个维度的动态捷径，实现类人快慢思考的灵活计算分配。
- **高效性**：在保持 CoT 级别准确率的前提下，实现 20 倍以上推理加速和 90% 以上 token 减少，非常实用。
- **可控性**：通过两个超参数（深度阈值和步数）即可在推理时灵活调整计算预算，实现测试时缩放。
- **蒸馏框架**：两阶段蒸馏设计巧妙，先对齐语言和潜在空间，再学习捷径，避免了训练冲突。
- **实验全面**：涵盖数学和常识推理，对比多种基线，消融实验分析充分，验证了设计选择的有效性。

## 8. 不足与局限

- **可解释性缺失**：潜在空间推理缺乏语言中间步骤，难以理解、分析或验证模型内部逻辑，在安全关键场景存在风险。
- **规模限制**：实验仅基于 GPT-2 124M 和 LLaMA 3.2 1B，未在更大模型（如 7B/13B）或更多任务（如代码、科学推理）上验证，泛化性需进一步确认。
- **性能略低于 CoT 的潜力**：在 GSM8K 上准确率与 CoT 持平，但在更复杂任务（如 GSM-HARD）上略低于 CoT，说明压缩推理可能损失部分推理能力。
- **训练复杂度**：两阶段蒸馏需要先训练一个教师 CoT 模型，再训练学生，流程相对繁琐；且关键性标签依赖原子思维分解，可能引入噪声。
- **未报告误差条**：虽进行了多次运行，但未在结果表中报告标准差，统计显著性证据不足。

（完）
