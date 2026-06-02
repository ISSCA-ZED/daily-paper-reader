---
title: "Critical Tokens Matter: Token-Level Contrastive Estimation Enhances LLM’s Reasoning Capability"
title_zh: 关键token至关重要：token级对比估计增强LLM推理能力
authors: "Zicheng Lin, Tian Liang, Jiahao Xu, Qiuzhi Liu, Xing Wang, Ruilin Luo, Chufan Shi, Siheng Li, Yujiu Yang, Zhaopeng Tu"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=fnz1g18EdI"
tags: ["query:key-tokens"]
score: 10.0
evidence: 提出推理轨迹中的关键token，并通过rollout采样识别
tldr: 针对LLM数学推理中错误往往由少数关键token导致的问题，本文提出通过rollout采样识别这些关键token，并利用对比估计进行替换。在GSM8K和MATH500上的实验表明，该方法显著提升了模型准确率。贡献在于提供了一种高效的token级推理改进方法。
source: ICML-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2025-fnz1g18edi/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1766, \"height\": 658, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-fnz1g18edi/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 693, \"height\": 510, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-fnz1g18edi/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1424, \"height\": 822, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-fnz1g18edi/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 763, \"height\": 545, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-icml-2025-fnz1g18edi/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1251, \"height\": 396, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-fnz1g18edi/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1498, \"height\": 700, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-fnz1g18edi/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1448, \"height\": 559, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-fnz1g18edi/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1166, \"height\": 145, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-fnz1g18edi/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1095, \"height\": 359, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-fnz1g18edi/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 660, \"height\": 273, \"label\": \"Table\"}]"
motivation: 数学推理中微小token变化可能导致错误，需识别关键token。
method: 通过rollout采样和对比估计识别并替换推理轨迹中的关键token。
result: 在GSM8K和MATH500上准确率显著提升。
conclusion: 识别并纠正关键token能有效增强LLM的推理能力。
---

## Abstract
Mathematical reasoning tasks pose significant challenges for large language models (LLMs) because they require precise logical deduction and sequence analysis. In this work, we introduce the concept of critical tokens -- elements within reasoning trajectories that significantly influence incorrect outcomes. We present a novel framework for identifying these tokens through rollout sampling and demonstrate their substantial divergence from traditional error tokens. Through extensive experiments on datasets such as GSM8K and MATH500, we show that identifying and replacing critical tokens significantly improves model accuracy. We propose an efficient methodology for pinpointing these tokens in large-scale datasets using contrastive estimation and extend this framework to enhance model training processes with direct preference optimization (DPO). Experimental results on GSM8K and MATH500 benchmarks with the widely used models Llama-3 (8B and 70B) and Deepseek-math (7B) demonstrate the effectiveness of the proposed approach, cDPO. Our results underscore the potential of leveraging critical tokens to reduce errors in reasoning tasks, advancing the development of AI systems capable of robust logical deduction.

---

## 论文详细总结（自动生成）

# 论文总结：Critical Tokens Matter: Token-Level Contrastive Estimation Enhances LLM's Reasoning Capability

## 1. 核心问题与整体含义（研究动机和背景）

- **研究动机**：数学推理任务需要精确的逻辑演绎和序列分析，但大语言模型（LLMs）即使使用链式思维（COT）方法，仍然容易出现推理错误。以往研究多从宏观步骤层面分析错误类型（如计算错误、遗漏步骤等），但忽略了**token级别的细微差异**对最终结果的关键影响。
- **核心问题**：在错误的推理轨迹中，是否存在某些“关键token”（critical tokens），它们对导致错误结果起决定性作用？如何系统地识别这些token，并利用它们来提升模型的推理能力？
- **整体含义**：本文首次系统定义了推理轨迹中的“关键token”，并证明它们与人类标注的错误token有显著差异。通过替换或惩罚这些关键token，可以大幅提升模型在数学推理任务上的准确率，为理解LLM推理失败机制和设计更有效的训练方法提供了新视角。

## 2. 提出的方法论

### 2.1 核心思想
- **关键token定义**：在错误推理轨迹中，那些对最终错误结果产生显著影响力的token。它们可能本身并非“计算错误”或“语义错误”，但会引导模型走向错误方向。
- **识别方法**：先通过**rollout采样**（对每个token，固定前缀并多次采样补全，计算正确率）验证关键token的存在；再提出更高效的**对比估计（Contrastive Estimation，CE）** 方法，利用正、负两个模型（分别训练于正确和错误轨迹）的token级概率差异，自动识别关键token。

### 2.2 关键技术细节
- **Rollout采样**：对错误轨迹中每个token t_i，固定前缀 {t_1,..., t_i}，进行64次rollout采样。若该token的正确率为0，且之后所有token的正确率均低于5%，则标记为关键token。
- **对比估计（CE）**：
  - 训练**正模型**（在正确轨迹上SFT）和**负模型**（在频繁出现的错误轨迹上SFT）。
  - 对于错误轨迹的每个token y_t，计算得分 s_t：
    ```
    log s_t = (1+β) log P_p(y_t | x, y_<t) - β log P_n(y_t | x, y_<t) - log Z
    ```
    其中β为缩放超参数，Z为归一化因子。得分越低，表示该token在正确模型下概率低、在错误模型下概率高，即更可能是关键token。
- **cDPO方法**：将关键token得分引入Direct Preference Optimization（DPO）中。
  - 原始DPO的奖励函数 φ(x,y) = γ log (π_θ(y|x)/π_ref(y|x))，改为token级加权形式：
    ```
    φ_s(x, y, s) = γ Σ_t (1 - s_t) log (π_θ(y_t|x,y_<t)/π_ref(y_t|x,y_<t))
    ```
  - 仅对负样本（错误轨迹）应用该加权奖励，惩罚关键token。
  - 损失函数：
    ```
    ℓ_cDPO = - Σ_i log σ( φ(x_i, y_i^p) - φ_s(x_i, y_i^n, s_i^n) )
    ```

### 2.3 算法流程（文字说明）
1. 从基座模型采样N条推理轨迹，根据答案正确性划分为正例集D_p和负例集D_n。
2. 在D_p上SFT训练正模型，在D_n中选取出现频率高的错误轨迹（覆盖50%错误情况）SFT训练负模型。
3. 对DPO训练中的每个负样本，用正、负模型通过对比估计计算每个token的关键得分s_t。
4. 基于加权奖励进行cDPO训练，降低关键token的生成概率。

## 3. 实验设计

- **数据集**：GSM8K（小学级数学应用题）和 MATH（高中数学竞赛题，评估用MATH500子集）。
- **基准方法（Baselines）**：
  - 基座模型（Base）：Llama-3-8B, Llama-3-70B, DeepSeek-Math-7B。
  - SFT：仅用正例集微调。
  - DPO（两种起点：基座模型和SFT模型）。
  - TokenDPO（2024，token级KL约束DPO）。
  - RPO（DPO + 额外NLL项，2024）。
  - 本文提出的cDPO。
- **评估指标**：Pass@1准确率（温度0），此外还测试了不同温度下Pass@1（平均10次采样）。
- **训练配置**：全部使用LoRA适配器，正/负模型训练1 epoch（lr=3e-4），偏好优化训练3 epoch（lr=2e-5，cDPO因score范围0-1改用4e-5），γ=1.0，β=1.0（消融实验β范围0.5-2.5）。采样时N=64，选择前50%高频错误轨迹训练负模型。
- **额外实验**：在Qwen-2.5-7B和Qwen-2.5-32B上进行验证。

## 4. 资源与算力

- **论文未明确说明**使用的GPU型号、数量、训练总时长等具体算力信息。
- 仅提到**效率分析**：对比估计（CE）相比rollout采样大幅降低计算成本。例如在GSM8K上，CE仅需约78,393次前向传播（训练正/负模型）+ 2n次推理，而rollout采样需要约581,425n次前向传播（n=7500时，CE成本仅为rollout的0.002%）。

## 5. 实验数量与充分性

- **主要实验**：在GSM8K和MATH500上，使用3种基座模型（Llama-3-8B/70B, DeepSeek-Math-7B），对比5种基线方法（SFT、DPO、TokenDPO、RPO、cDPO），共约3×2×6=36组核心结果（表3）。
- **消融实验**：对对比因子β在GSM8K上做了9个值的消融（表4）。
- **额外分析**：
  - 学习曲线（图4）：对比DPO、RPO、cDPO的log概率变化。
  - 关键token替换实验（图2）：替换后Pass@1从0%提升至约30%，Pass@64超90%。
  - 与rollout采样的AUC对比：CE与rollout的AUC在GSM8K上0.77，MATH上0.84。
  - 不同温度下的稳定性测试（表5）：cDPO在温度0-1.5之间表现稳定，而基座模型随温度升高急剧下降。
  - 在Qwen-2.5大模型上的验证（表6）。
- **充分性评价**：
  - **优点**：覆盖了不同规模、不同类型的模型（通用型、领域专用型），对比了多种主流推理偏好优化方法，提供了充分的消融和稳定性分析。
  - **不足之处**：
    - 仅在数学推理任务（GS8K、MATH）上测试，未扩展到其他逻辑/代码/常识推理领域。
    - 未与更近期的强化学习方法（如GRPO、在线PPO等）对比。
    - 未报告统计显著性检验的具体方法（仅提p<0.005）。
    - 资源消耗未明确，外部复现困难。

## 6. 主要结论与发现

- **关键token普遍存在**：在错误推理轨迹中，通过rollout采样几乎总能找到满足条件的关键token（GSM8K中99/100，MATH中100/100）。
- **关键token不等于传统错误token**：多数情况下（GSM8K中65%，MATH中87%）关键token与人类标注的错误token不一致，说明其能捕捉更根本的逻辑断裂。
- **替换关键token可大幅提升准确率**：移除关键token并强制模型重新生成替代token，Pass@1从0%提升至约30%，Pass@64超90%。
- **cDPO有效改善训练动态**：相比DPO和RPO，cDPO在保持正确序列高概率的同时，大幅降低错误序列的概率，实现更好的正负区分。
- **cDPO在所有设置下超越强基线**：在GSM8K（平均77.2% vs 基线67.0%）和MATH500（平均33.3% vs 32.1%）上均取得最优，并在Qwen-2.5-32B上提升至GSM8K 93.5%、MATH500 64.8%。

## 7. 优点

- **概念创新**：首次提出并实证“关键token”概念，揭示了token级别细粒度错误机制，不同于传统步骤级错误分析。
- **方法高效**：对比估计比rollout采样节省约5个数量级的计算成本，且与rollout结果高度一致（AUC>0.77），适合大规模数据。
- **训练框架实用**：cDPO将token评分直接融入DPO损失，无需外部奖励模型或人工标注，易于实现和扩展。
- **实验严谨**：多模型、多数据集、多基线对比；消融beta参数；测试不同温度下的鲁棒性；在更强模型上验证泛化。
- **结果显著**：在多个模型上一致提升1-5个绝对百分点，且在高温下保持稳定（传统方法精度急剧下降）。

## 8. 不足与局限

- **领域局限**：仅限于数学推理任务（GSM8K、MATH），未验证在常识推理、代码生成、逻辑推理等其他需要链式推理的领域的有效性。
- **对比基线范围有限**：未与最新的在线强化学习方法（如GRPO、PPO、自训练迭代优化）对比；TokenDPO和RPO的复现可能不完全对应原论文最优设置。
- **资源信息缺失**：未提供GPU型号、数量、训练总时间等关键硬件信息，影响可复现性和成本评估。
- **关键token识别依赖正/负模型**：负模型训练需选择高频错误轨迹，对多样错误类型覆盖可能不足；β参数需调优（推荐1.5-1.75）。
- **cDPO仅惩罚负样本**：未探索同时对正样本中关键token（可能正向贡献）进行鼓励，设计空间有限。
- **理论分析不足**：对比估计的分布推导（附录A）假设正负分布为同方差高斯，实际LLM token分布更复杂，理论支撑不够强。
- **潜在偏差**：关键token识别基于固定采样次数（64 rollout），对长序列或罕见错误模式可能不精确。

（完）
