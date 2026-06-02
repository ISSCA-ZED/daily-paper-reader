---
title: One Token Embedding Is Enough to Deadlock Your Large Reasoning Model
title_zh: 一个token嵌入足以使你的大型推理模型死锁
authors: "Mohan Zhang, Yihua Zhang, Jinghan Jia, Zhangyang Wang, Sijia Liu, Tianlong Chen"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=gBgvuTd9Hx"
tags: ["query:key-tokens"]
score: 4.0
evidence: 利用过渡token作为关键token使推理陷入死锁
tldr: 演示了仅通过训练一个对抗性token嵌入即可使大型推理模型陷入无限推理循环，该攻击利用过渡token（如“Wait”）的关键作用。这反面证实了过渡token在推理序列中的重要性，与关键token重要性研究相关。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-neurips-2025-gbgvutd9hx/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1450, \"height\": 755, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-gbgvutd9hx/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1052, \"height\": 368, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-gbgvutd9hx/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 524, \"height\": 372, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-gbgvutd9hx/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 523, \"height\": 374, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-gbgvutd9hx/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 831, \"height\": 316, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-gbgvutd9hx/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1445, \"height\": 1061, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-gbgvutd9hx/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1153, \"height\": 834, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-neurips-2025-gbgvutd9hx/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 706, \"height\": 136, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-gbgvutd9hx/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1444, \"height\": 233, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-gbgvutd9hx/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1451, \"height\": 309, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-gbgvutd9hx/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 726, \"height\": 261, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-gbgvutd9hx/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1452, \"height\": 171, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-gbgvutd9hx/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1452, \"height\": 233, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-gbgvutd9hx/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1447, \"height\": 1702, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-gbgvutd9hx/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1448, \"height\": 1737, \"label\": \"Table\"}]"
motivation: LRM的迭代思考机制存在新漏洞。
method: 训练恶意嵌入，诱导模型持续生成过渡token。
result: 成功使模型陷入无限推理循环，无法输出答案。
conclusion: 对抗性嵌入可针对关键过渡token实现攻击。
---

## Abstract
Modern large reasoning models (LRMs) exhibit impressive multi-step problem-solving via chain-of-thought (CoT) reasoning. However, this iterative thinking mechanism introduces a new vulnerability surface. We present the Deadlock Attack, a resource exhaustion method that hijacks an LRM's generative control flow by training a malicious adversarial embedding to induce perpetual reasoning loops. Specifically, the optimized embedding encourages transitional tokens (e.g., “Wait”, “But”) after reasoning steps, preventing the model from concluding its answer. A key challenge we identify is the continuous-to-discrete projection gap: naïve projections of adversarial embeddings to token sequences nullify the attack. To overcome this, we introduce a backdoor implantation strategy, enabling reliable activation through specific trigger tokens. Our method achieves a 100\% attack success rate across four advanced LRMs (Phi-RM, Nemotron-Nano, R1-Qwen, R1-Llama) and three math reasoning benchmarks, forcing models to generate up to their maximum token limits. The attack is also stealthy (in terms of causing negligible utility loss on benign user inputs) and remains robust against existing strategies trying to mitigate the overthinking issue. Our findings expose a critical and underexplored security vulnerability in LRMs from the perspective of reasoning (in)efficiency.

---

## 论文详细总结（自动生成）

好的，遵照您的要求，以下是对给定论文的详细中文总结。

### 1. 论文的核心问题与整体含义（研究动机和背景）

- **核心问题**：现代大型推理模型（LRMs）依靠链式思维（CoT）进行多步推理，但这种迭代思考机制带来了新的、未被充分探索的安全漏洞。攻击者可以利用该机制，通过最小的扰动，诱导模型进入无限推理循环，从而耗尽计算资源，实现拒绝服务（DoS）攻击。
- **研究动机**：
    - LRMs固有的“过度思考”倾向（即对简单问题生成冗长推理）被认为是一种效率问题。论文首次提出，这种倾向可被**反向利用**，成为一种**安全隐患**。
    - 现有攻击主要集中于降低模型输出准确性或绕过安全对齐，而针对LRM计算效率的**资源耗尽攻击**尚属空白。已有的“Slowdown Attack”需依赖输入问题的复杂性，无法实现普适的、无休止的循环。
    - 论文核心研究问题：**能否用极小的扰动（如单个token）劫持LRM的生成流程，触发过度计算并最终导致资源耗尽？**
- **整体含义**：论文揭露了一个在LRM安全视角下被忽视的、以推理（效率）为攻击面的严重漏洞。攻击者可以通过在开源模型供应链中植入后门，远程触发该攻击，对服务提供商造成重大经济和服务中断影响。这警示安全防御需从准确性扩展到计算鲁棒性。

### 2. 论文提出的方法论：核心思想、关键技术细节

- **核心思想**：训练一个**对抗性嵌入（adversarial embedding）**。当该嵌入被“附加”到用户输入前时，它能够劫持模型的生成控制流，强制其在每个推理步骤结尾处（句号、问号后）反复生成**过渡性token**（如“Wait”、“But”），从而阻止模型做出最终结论，陷入无限推理死循环。
- **关键技术细节**（分两步）：
    1.  **连续对抗性嵌入优化 (Continuous Adversarial Embedding Optimization)**:
        - **目标**：在嵌入空间学习一个通用向量 `e_adv`，该向量被预置在任何输入前，都能迫使模型在推理步骤结束时，最大化生成过渡性token（`T_trans`）的概率。
        - **优化目标**：最大化公式(3)中的 `J_attack`，即平均过渡token概率。
        - **训练过程**：使用小批量（如20个）训练样本（问题-答案对），通过前向传播计算损失，反向传播梯度，**仅更新**对抗性嵌入 `e_adv` 的参数（不修改原模型权重）。优化器为Adam，学习率1e-3，训练1000步。

    2.  **解决“连续到离散”投影鸿沟 (Continuous-to-Discrete Projection Gap)**:
        - **问题**：真实的攻击者只能输入离散文本token，无法直接注入连续的对抗性嵌入。直接将学习到的连续嵌入 `e_adv` 投影到最近词汇token的嵌入上（naïve projection）会完全失效。
        - **分析验证**：通过线性模式连通性（LMC）、高斯平滑鲁棒训练、迭代投影等方法，证实投影误差超过了对抗性嵌入的扰动容忍度，导致攻击失效。
        - **解决方案：后门植入（Backdoor Implantation）**：将优化的连续对抗性嵌入向量 `e_adv` **直接写入预定义触发token（如“!!!!!”）的嵌入矩阵**。这样，当输入中出现该触发token时，模型实际上在读取该对抗性嵌入，从而激活攻击。模型对不含触发token的正常输入行为完全不变，保证了隐蔽性。

### 3. 实验设计

- **基准测试数据集**：
    - 主要推理评估：**GSM8K**, **MATH500**, **MMLU-Pro (Math)**。
    - 在长上下文和鲁棒性测试中补充使用了极具挑战性的 **AIME 2024** 基准。
    - 隐蔽性评估额外使用了：**HumanEval (Python)**、**MMLU-Pro (Health)**、**CommonsenseQA**，每种500个样本。
- **评估模型**：4个先进的LRMs：
    - **Phi-RM** (Microsoft, 3.8B)
    - **Nemotron-Nano** (NVIDIA, 8B)
    - **R1-Qwen** (DeepSeek蒸馏, 7B)
    - **R1-Llama** (DeepSeek蒸馏, 8B)

- **对比方法与基线**：
    - **基线**：未受攻击的原始模型。
    - **直接嵌入攻击**：为了展示方法有效性，在完全白盒设置下直接优化连续嵌入 `e_adv`（表1）。
    - **后门攻击**：主要实验结果（表2）基于后门植入的模型。
    - **鲁棒性对比**：将后门攻击与三种旨在缓解过度思考的测试时计算策略对比：**CoD (Chain of Draft)**、**CCoT (Concise CoT)**、**NoThinking**。结果表明这些策略均无法防御该攻击。

### 4. 资源与算力

- 论文**未明确**说明训练对抗性嵌入或运行全部实验所使用的具体GPU型号、数量和总算力（如GPU-hours）。仅提到训练过程使用了Adam优化器，学习率1e-3，训练1000步即可收敛。但由于实验涉及4个7B/8B模型在多个数据集上生成最大4000个token，其计算开销是显著的。

### 5. 实验数量与充分性

- **实验数量**：论文进行了大量实验，全面覆盖了有效性、隐蔽性、鲁棒性、可扩展性和消融研究：
    - **主实验**：4个模型 × 3个基准，每种情况报告ASR、平均Token数、平均时间。
    - **鲁棒性实验**：4个模型 × 3种防御策略。
    - **隐蔽性实验**：2个模型 × 6个基准（各500样本）进行大规模验证。
    - **长上下文实验**：4个模型（含AIME） × 4个基准，扩展到20000 token限制。
    - **消融实验**：研究了嵌入长度（L）、训练集大小（N）、学习率等对训练收敛的影响。
    - **连续到离散投影挑战验证**：包含多组图（如LMC、高斯平滑、迭代投影）分析。
- **充分性与客观性**：
    - **充分性**：实验设计相当全面，不仅验证了攻击的有效性（100% ASR），还严格验证了其隐蔽性和对现有防御的鲁棒性。使用多种模型和基准（包括高难度AIME）增强了结论的泛化性。
    - **客观性与公平性**：实验对比了原始基线和三种代表性的防御策略（CoD, CCoT, NoThinking），对比设计合理。消融实验系统地分析了关键超参数的影响。论文也诚实地指出了连续到离散投影的挑战，并通过后门方案巧妙解决了该问题。整体上看，实验设计是客观且公平的。

### 6. 论文的主要结论与发现

- **攻击有效性**：提出的“死锁攻击”（Deadlock Attack）在所有4个先进LRM和3个数学推理基准上均达到了**100%的攻击成功率（ASR）**，强制模型生成到预设的最大token限制（4000 tokens）。
- **隐蔽性**：攻击是高度隐蔽的。在模型被植入后门后，对**不含触发token的正常输入**，模型在推理、代码生成、常识问答等多个基准任务上的性能损失可以忽略不计（表4和附录表A2）。
- **鲁棒性**：该攻击对现有旨在缓解过度思考的策略（CoD、CCoT、NoThinking）具有**鲁棒性**，因为这些策略无法从根本上阻止由对抗性嵌入直接驱动的内部推理循环。
- **关键发现**：发现并解决了“连续到离散投影鸿沟”这一关键挑战，证明了后门机制是实现该攻击在现实环境中部署的有效途径。
- **新颖性**：首次系统性地研究了针对LRM计算效率的资源耗尽攻击，揭示了推理机制本身是一个新的、未探索的脆弱面。

### 7. 优点：方法或实验设计上的亮点

- **方法新颖性强**：第一个提出并成功实现了利用**单个token嵌入**劫持LRM推理流程，使其陷入**无限死循环**的资源耗尽攻击。攻击角度独特，从“过度思考”这一效率问题转向安全漏洞。
- **问题剖析深入**：清晰地识别并系统分析了“连续到离散投影鸿沟”这一核心技术障碍。通过LMC、高斯平滑、迭代投影等方法进行多角度验证，逻辑严密，论述充分。
- **解决方案巧妙**：采用后门植入的策略，将连续嵌入直接写入触发token的嵌入层，完美规避了投影问题。这一方案既保证了攻击的有效性（触发激活），又保证了隐蔽性（无触发时正常），实用性极高。
- **实验设计全面且严谨**：覆盖了有效性、隐蔽性、鲁棒性、可扩展性（长上下文）、消融分析等多个维度。评估了多种模型和基准，特别是使用AIME挑战性问题排除了自然长输出的假阳性，并采用大规模样本验证隐蔽性，使得结论非常可靠。

### 8. 不足与局限：包括实验覆盖、偏差风险、应用限制

- **攻击假设与现实差距**：攻击假设攻击者对模型有**白盒访问权限**（修改嵌入层），这是后门植入的前提。虽然论文描述了发布开源后门模型的供应链攻击场景，但对已部署的、无法访问的黑盒API模型，该无法直接应用。
- **后门触发隐蔽性**：论文使用符号“!!!!!”作为触发token。虽然指定了其他替代方案（如使用同形异义词），但当前主要实验触发器并非完全不可见。在实际部署中，若攻击触发器被用户偶然输入或检测到，攻击可能失效。
- **实验覆盖的局限性**：
    - 所有实验均在数学推理模型上完成。尽管在代码和非推理任务上验证了隐蔽性，但攻击是否能在其他类型的推理模型（如科学、法律推理）或更大规模的LRM（如DeepSeek-R1 671B参数级）上同样有效，并未验证。
    - 论文未测试该攻击对使用**训练阶段对抗训练**防御的模型的鲁棒性。
    - 使用**4000 token上限**作为成功标准较为常规，但现代服务商可能设置更高上限（如32k）。论文在附录中扩展到了20k token，证实了攻击的可扩展性，但未测试极限情况。
- **资源开销**：虽然攻击本身轻量（只训练几个嵌入向量），但**检测和执行攻击需要模型进行长达最大token限制的生成**，这本身就需要消耗大量计算资源。作为DoS攻击，其成本效益分析需要进一步评估。
- **防御方向不明确**：论文指出了威胁，但对防御措施的讨论相对有限，仅指出现有基于提示或解码策略的“过度思考缓解”方法无效。提出了可能的“检测模块”（但会增加开销且可绕过），而终极防御（如识别并学习消除后门嵌入）的可行性和具体方案未深入探讨。

（完）
