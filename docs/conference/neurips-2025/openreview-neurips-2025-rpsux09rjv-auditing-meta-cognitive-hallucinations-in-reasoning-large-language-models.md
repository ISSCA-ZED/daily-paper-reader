---
title: Auditing Meta-Cognitive Hallucinations in Reasoning Large Language Models
title_zh: 审计推理大语言模型中的元认知幻觉
authors: "Haolang Lu, Yilian Liu, Jingxin Xu, Guoshun Nan, Yuanlong Yu, Zhican Chen, Kun Wang"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=rPsUx09RJV"
tags: ["query:key-tokens"]
score: 4.0
evidence: 审计CoT轨迹中的幻觉因果关系，涉及推理序列分析
tldr: 该论文致力于理解推理大语言模型中幻觉的产生与演化机制。通过审计长链思维轨迹并评估模型在错误或偏见性论断上的认知置信度，论文揭示了受限知识领域下幻觉的因果关系。研究发现推理模型在长CoT设置下会出现特定的认知偏差模式，为改善推理序列的可靠性提供了诊断工具，但并未直接关注关键token的识别或重要性度量。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-neurips-2025-rpsux09rjv/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1445, \"height\": 517, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-rpsux09rjv/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1419, \"height\": 779, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-rpsux09rjv/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 683, \"height\": 690, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-rpsux09rjv/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1388, \"height\": 818, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-rpsux09rjv/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1387, \"height\": 814, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-rpsux09rjv/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 526, \"height\": 477, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-rpsux09rjv/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 579, \"height\": 489, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-rpsux09rjv/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1448, \"height\": 302, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-rpsux09rjv/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1450, \"height\": 311, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-rpsux09rjv/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1449, \"height\": 309, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-rpsux09rjv/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1450, \"height\": 310, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-neurips-2025-rpsux09rjv/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1451, \"height\": 341, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-rpsux09rjv/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1446, \"height\": 574, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-rpsux09rjv/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 737, \"height\": 720, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-rpsux09rjv/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1445, \"height\": 252, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-rpsux09rjv/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1454, \"height\": 612, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-rpsux09rjv/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1452, \"height\": 1008, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-rpsux09rjv/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1137, \"height\": 220, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-rpsux09rjv/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 629, \"height\": 178, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-rpsux09rjv/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1201, \"height\": 138, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-rpsux09rjv/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 933, \"height\": 179, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-rpsux09rjv/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1353, \"height\": 1046, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-rpsux09rjv/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1447, \"height\": 372, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-rpsux09rjv/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1460, \"height\": 1450, \"label\": \"Table\"}]"
motivation: 现有方法无法全面洞察幻觉在推理链中的产生与演化。
method: 通过审计CoT轨迹并评估模型认知置信度，分析幻觉因果关系。
result: 发现长CoT设置下模型出现特定的认知偏差模式。
conclusion: 为推理序列的可靠性提供了诊断方法，但未涉及关键token识别。
---

## Abstract
The development of Reasoning Large Language Models (RLLMs) has significantly improved multi-step reasoning capabilities, but it has also made hallucination problems more frequent and harder to eliminate. While existing approaches address hallucination through external knowledge integration, model parameter analysis, or self-verification mechanisms, they fail to provide a comprehensive insight into how hallucinations **emerge** and **evolve** throughout the reasoning chain. In this work, we investigate hallucination causality under constrained knowledge domains by auditing the Chain-of-Thought (CoT) trajectory and assessing the model's cognitive confidence in potentially erroneous or biased claims.
Analysis reveals that in long-CoT settings, RLLMs may iteratively reinforce biases and errors through flawed reflective processes, ultimately inducing hallucinated reasoning paths.
Counterintuitively, even with interventions at hallucination origins, reasoning chains display pronounced ''chain disloyalty'', resisting correction and sustaining flawed trajectories.
We further point out that existing hallucination detection methods are *less reliable and interpretable than previously assumed*, especially in complex multi-step reasoning contexts.
Unlike circuit tracing that requires access to model parameters, our auditing **enables more interpretable long-chain hallucination attribution in black-box settings**, demonstrating stronger generalizability and practical utility.
Our code is available at [this link](https://github.com/Winnie-Lian/AHa_Meta_Cognitive).

---

## 论文详细总结（自动生成）

好的，以下是根据您提供的论文内容生成的结构化、深入、客观的中文总结。

---

### 论文详细总结

#### 1. 核心问题与整体含义（研究动机和背景）

*   **核心问题**：推理大语言模型（RLLMs）虽然通过链式思维（CoT）和自我反思大幅提升了多步推理能力，但也引入了更频繁、更隐蔽的幻觉问题。现有方法（如外部知识融合、模型参数分析、自我验证）无法提供关于幻觉在推理链中如何**产生和演化**的全面洞见。
*   **背景与动机**：在长链式思维（Long-CoT）生成过程中，模型可能在早期引入一个微小错误，并通过“反思”机制反复强化这个错误，最终形成一个看似合理但事实错误的答案。这种现象类似于“认知偏差”，使得用户难以从最终答案中察觉潜在的幻觉。作者旨在通过审计CoT轨迹，揭示幻觉的因果机制，为提升模型可靠性提供诊断工具。

#### 2. 方法论：核心思想、关键技术细节、公式

*   **核心思想**：
    1.  **可控环境构建**：在一个受限且可验证的知识领域（基于RFC技术文档）内，设计两种类型的幻觉场景（Type I：见过但未掌握的知识；Type II：未见或错误的知识），以可控地复现幻觉。
    2.  **CoT轨迹建模**：将长CoT形式化为一个结构化推理过程，包含推理节点（claims）、主路径（Main path）、反思链接（Reflection links）和丢弃边（Drop edges）。
    3.  **元认知置信度审计**：引入“元认知置信度”`conf(c)`概念，量化模型对自身知识状态的信念，而非论断的客观正确性。作者假设模型在反思过程中会偏向于与用户输入语义一致的内容（Prompt-Aligned Bias），并据此建立了置信度更新的数学框架。

*   **关键技术细节与公式**：
    *   **幻觉分类**：
        *   **Type I (Seen but Unlearned)**：训练数据中存在该知识，但模型未有效学习。
        *   **Type II (Unseen or Incorrect)**：训练数据中不存在该知识（无论是事实还是谬误）。
    *   **推理过程建模（公式1）**：
        `CoT = M({ci or cki} | main path ∧ refl(cp = cq) ∧ ∃ cm ⊣ ∅ )`
        表示CoT由推理节点、主路径、可选的“反思”连接和“丢弃”边组成。
    *   **置信度更新公式（公式2, 3）**：
        `cq+1 ← Refine(cq | Feedback(cq-1, cq), g(cq, prompt))`
        `∆conf(cp, cq) = α · f(cp-1, cq) + (1-α) · g(cq, prompt)`
        *   `Feedback`：捕捉上一步推理对当前论断置信度的影响。
        *   `g`：表示“提示对齐的元认知偏差”，即模型倾向于根据论断与用户提示的语义相似度来调整其“自我感觉确定性”。
        *   `α`：是平衡两种影响的超参数。
    *   **算法流程**：通过审计CoT，追踪错误知识（`k`）如何被引入、通过反思（`refl`）被强化或纠正，并最终导致幻觉答案。例如，模型可能通过自我提问（self-query）或引入不合理假设（`if`条件句）来巩固错误论点。

#### 3. 实验设计：数据集、场景与对比方法

*   **数据集**：作者构建了一个**受控幻觉审计数据集**，基于RFC（Request for Comments）文档。数据集分为四个子集：
    *   **Type I** (Seen but Unlearned, 439个问题)
    *   **Type I Control** (Correct Answer, 500个问题)
    *   **Type II** (Unseen or Incorrect, 484个问题)
    *   **Type II Control** (Error Rejected, 92个问题)
    *   总计1515个独特问题，每个问题采样5个答案进行分析。
*   **场景**：模型在受限的RFC知识领域内回答特定问题，以评估其在大规模CoT推理中的幻觉行为。
*   **Benchmark与对比方法**：
    *   **主要检测方法对比**：评估了7种主流幻觉检测方法在长CoT场景下的表现。
        1.  **内部信号探测**：Logit Entropy, Attention Strength, Spectral Entropy, HDM2 model.
        2.  **语义一致性检查**：CCP (Claim-Conditioned Perplexity), SelfCheckGPT, Semantic Entropy.
    *   **上游干预实验**：设计了三类编辑干预（在首次幻觉前、中、后纠正错误知识），评估其对下游推理和最终答案的影响。

#### 4. 资源与算力

*   **测试模型**：主要使用 **DeepSeek-R1** 进行数据生成和审计。部分检测方法使用了 **DeepSeek-R1-Distill-Qwen-14B** 和 **GPT-4o**。
*   **硬件环境**：
    *   **服务器**：Ubuntu 20.04.1 LTS, Intel Xeon Gold 6248R CPU, 502 GiB RAM.
    *   **GPU**：2块 **NVIDIA A100-SXM4-80GB** GPUs.
    *   **软件**：Python 3.9, PyTorch 2.2.0, CUDA 12.2.
*   **效率分析**：论文详细分析了不同检测方法的计算成本（附录E.3）。例如，Semantic Entropy方法需要约 `17.2 * S * T`（S为句子数，T为推理时间），而Logit Entropy这类内部信号方法仅需约 `T`。未提供总训练时长或全部实验的累计算力时间。

#### 5. 实验数量与充分性

*   **实验数量**：研究进行了多组大规模实验，包括：
    *   幻觉复现的统计分析（Table 1）。
    *   包含五大维度、多个细粒度指标的**行为模式分析**（Table 2）。
    *   在不同干预点进行的**上游干预实验**（Figure 3, 4, 5）。
    *   对7种现有检测方法的**全面性能评估**（Table 3）。
    *   额外的消融和鲁棒性分析（如通用性评估B.2，困惑度分析E.4）。
*   **充分性与客观性**：
    *   **充分**：实验覆盖了问题定义、机理分析、干预测试和方法对比等多个方面，设计严谨，因果链路清晰。行为分析引入了**人工验证**，确保了标注质量。
    *   **公平**：对比方法均采用其论文中的标准实现或在验证集上调优后的最佳阈值。研究明确指出了自身方法的局限性，并在不同模型（Claude-3.7-Sonnet, Qwen3）上验证了结论的通用性，增加了说服力。
    *   **客观**：所有关键发现（Obs I-VII）都基于量化数据（如百分比、次数）和具体的CoT案例分析，没有模糊或无法验证的断言。

#### 6. 主要结论与发现

1.  **幻觉根源**：幻觉源于模型对**错误知识的过度自信**。模型无法准确评估从其错误记忆中调用信息的元认知置信度，导致错误得以传播。
2.  **反思的放大效应**：反思行为（Reflection）在幻觉情况下**频率更高**（约2.12倍），并且会**放大而非纠正错误**。模型通过自我提问、无根据假设等方式巩固了其错误认知。
3.  **提示对齐偏差**：模型存在强烈的“提示对齐偏差”，倾向于顺从用户提示中的错误信息。即便模型能识别出外部错误知识，也常会生成新的内部错误知识来合理化这些外部错误，而非拒绝纠正。
4.  **当前方法的缺陷**：
    *   **干预效果有限**：即使在上游关键点进行纠正编辑，也仅有22.5%的案例能成功逆转幻觉，表明模型对既有错误路径有很强的“路径依赖性”。
    *   **检测方法不可靠**：现有幻觉检测方法（尤其是语义一致性方法）在长CoT场景下表现不佳（AUROC多低于55%），且会混淆新颖正确与重复错误的论断。Semantic Entropy方法虽然准确率略高（78.95%），但计算成本极高。

#### 7. 优点

1.  **方法论创新**：首次将“元认知置信度”引入LLM幻觉研究，并用形式化模型解释了模型如何在反思中进行错误强化。区别于需要模型内部参数的电路追踪方法，该方法**在黑盒设置下更具可解释性和通用性**。
2.  **实验设计严谨**：通过构建基于RFC文档的**受控知识环境**，成功复现并区分了两种类型的幻觉，为后续研究提供了宝贵的基准。实验分析从宏观统计到微观个案，层层深入。
3.  **洞察深刻**：揭示了“反思未必带来纠正”、“提示偏差是认知污染源”等反直觉的洞见，对RLLM的可靠性设计具有重要的指导意义。
4.  **公平性考量**：在多个主流模型上验证了其发现的通用性，对比实验方法全面，评估指标不仅包括答案正确性，也涵盖了推理过程的忠实度。

#### 8. 不足与局限

1.  **模型单一性**：尽管验证了通用性，但**主要实验仅基于DeepSeek-R1**一个模型。不同架构或训练策略的模型可能在幻觉模式上存在差异。
2.  **元认知置信度的定量限制**：论文将`conf(c)`作为一个定性的解释框架，**缺乏对置信度变化的直接量化度量**。作者在局限性中承认这一点，并提出了未来通过熵、logit边界等指标进行量化的方向。
3.  **缓解策略缺失**：论文**并未提出有效的幻觉缓解策略**。研究发现现有的编辑干预效果甚微，指出这仍是未来需要探索的重要方向。当前工作更侧重于“诊断”而非“治疗”。
4.  **隐藏状态与黑盒的矛盾**：虽然声称方法适用于黑盒，但在检测方法评估部分（Table 3）仍对比了需访问内部状态的“Logit/Attention/Spectral Entropy”方法，其审计方法本身可能还是需要模型输出的token级概率信息，并非严格的黑盒。
5.  **结论泛化风险**：所审计的受控环境是高度专业化的RFC领域，结论能否完美泛化到更开放、知识更模糊的日常推理场景尚存疑。

（完）
