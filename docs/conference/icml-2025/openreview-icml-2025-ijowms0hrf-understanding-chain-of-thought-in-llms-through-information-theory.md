---
title: Understanding Chain-of-Thought in LLMs through Information Theory
title_zh: 通过信息论理解大语言模型中的思维链
authors: "Jean-Francois Ton, Muhammad Faaiz Taufiq, Yang Liu"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=IjOWms0hrf"
tags: ["query:key-tokens"]
score: 8.0
evidence: 量化每个推理步骤的信息增益来识别失败模式
tldr: 针对CoT评估需要标注数据的问题，本文从信息论角度形式化CoT推理，量化每个推理步骤的信息增益，从而无需标注即可定位失败模式。在玩具算术等任务上验证了有效性。
source: ICML-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2025-ijowms0hrf/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 856, \"height\": 197, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-ijowms0hrf/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 796, \"height\": 263, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-ijowms0hrf/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1654, \"height\": 613, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-ijowms0hrf/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 554, \"height\": 551, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-ijowms0hrf/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1031, \"height\": 2095, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-ijowms0hrf/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1044, \"height\": 2096, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-ijowms0hrf/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1042, \"height\": 2091, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-ijowms0hrf/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 888, \"height\": 441, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-ijowms0hrf/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 886, \"height\": 442, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-ijowms0hrf/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 889, \"height\": 444, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-icml-2025-ijowms0hrf/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 441, \"height\": 177, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-ijowms0hrf/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1714, \"height\": 451, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-ijowms0hrf/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1024, \"height\": 239, \"label\": \"Table\"}]"
motivation: 现有CoT评估技术需要标注数据或准确度不足。
method: 基于信息论框架量化每个推理步骤的信息增益。
result: 成功识别推理失败模式，无需昂贵标注。
conclusion: 信息增益可作为评估推理步骤质量的有效指标。
---

## Abstract
Large Language Models (LLMs) have shown impressive performance in complex reasoning tasks through the use of Chain-of-Thought (CoT) reasoning, allowing models to break down problems into manageable sub-tasks. However, existing CoT evaluation techniques either require annotated CoT data or fall short of accurately assessing intermediate reasoning steps, leading to high rates of false positives. In this paper, we formalize CoT reasoning in LLMs through an information-theoretic lens. Specifically, our framework quantifies the `information gain' at each reasoning step, enabling the identification of failure modes in LLMs without the need for expensive annotated datasets. We demonstrate the efficacy of our approach through extensive experiments on toy arithmetic, GSM8K and PRM800k datasets, where it significantly outperforms existing outcome-based methods by providing more accurate insights into model performance on individual tasks.

---

## 论文详细总结（自动生成）

# 详细中文总结

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **研究动机**：大语言模型（LLMs）通过思维链（Chain-of-Thought, CoT）在复杂推理任务上表现出色，但现有CoT评估方法存在两大问题：
  - 需要人工标注步骤级数据（如过程监督），成本高昂且难以扩展；
  - 基于最终结果的评估方法（如结果奖励模型ORM、Math-Shepherd）容易产生高误报率，尤其在中间步骤存在伪相关时。
- **核心问题**：如何在不依赖标注数据的前提下，准确识别CoT推理中每一步的正确性，从而定位失败模式。
- **整体含义**：本文从信息论角度形式化CoT推理，提出通过量化“信息增益”（Information Gain, IG）来无监督地评估每一步对正确最终答案的贡献，进而识别错误的中间步骤。

## 2. 论文提出的方法论：核心思想、关键技术细节、公式或算法流程

- **核心思想**：正确的CoT步骤应为预测最终正确答案提供有意义的信息；若某步骤不增加相关信息，则表明该步骤执行错误。
- **关键技术细节**：
  - **形式化框架**：将LLM推理视为状态更新过程，定义初始状态 \(X_0\)、任务 \(\lambda\)、更新规则 \(\Lambda\)。任务可分解为原始任务的序列（如加法、乘法）。
  - **可辨识性（Identifiability）**：若某子任务不在模型训练数据的“任务子空间”（Span(Γ_M)）中，则认为该任务不可辨识，模型无法正确执行。
  - **条件独立性（Theorem 3.3）**：当模型遇到不可辨识的子任务后，后续步骤对预测正确最终答案 \(Y\) 不再提供额外信息，即 \(Y \perp \!\!\! \perp X_j^M \mid X_{j-1}^M\)。
  - **信息增益计算**：
    - 定义信息增益为条件互信息 \(I(Y; X_j^M \mid X_{j-1}^M)\)。
    - 通过训练一个“监督模型”（supervisor model）\(g_{\text{sup}}\)，近似条件分布 \(p(Y \mid X_t^M)\)，并用交叉熵损失之差估计信息增益：
      \[
      \text{IG} \approx \mathbb{E}[\ell_{\text{CE}}(Y, g_{\text{sup}}(X_{j-1}^M))] - \mathbb{E}[\ell_{\text{CE}}(Y, g_{\text{sup}}(X_j^M))]
      \]
    - 样本级信息增益类似地定义为单个样本的交叉熵差，用于逐步检测错误。
- **算法流程**：
  1. 收集LLM在给定问题上的完整CoT输出（包括每一步的中间状态）。
  2. 训练一个监督模型（如GPT-2或Llama-3-8B），以逐步截断的CoT为输入，预测正确最终答案。
  3. 计算每一步的信息增益：前一步与当前步的交叉熵损失之差。
  4. 若某步信息增益显著下降或为负，则标记该步为潜在错误。

## 3. 实验设计：使用了哪些数据集/场景，基准是什么，对比了哪些方法

- **数据集/场景**：
  - **玩具算术（Toy Arithmetic）**：人为构造5步操作（交换、累加、反向累加、排序乘、差值），其中某一步随机或条件性错误，生成5个“LLM”模型（LLM1~LLM5）。
  - **Llama-3-8B算术**：真实模型计算 \(3x + 2y\)，分为三步（\(3x\), \(2y\), 求和），其中第三步常出错。
  - **GSM8K（受控版本）**：使用GPT-4生成答案，故意让“乘法”步骤错误，并引入“减法”作为伪相关（错误答案同时包含乘法和减法）。
  - **PRM800K**：OpenAI的数学过程监督数据集，有步级人工标签（+1正确，-1错误，0中性）。
- **基准（Baselines）**：
  - **Outcome Reward Model (ORM)**：训练二分类器预测最终答案正确的概率。
  - **Math-Shepherd (MS)**：用同一模型从每一步补全多个路径，统计正确完成的比例。
- **对比方法**：本文方法（信息增益IG）与ORM、MS在准确率、真正率（TPR）、假正率（FPR）等指标上比较。

## 4. 资源与算力：如果文中有提到，请总结使用了多少算力（GPU型号、数量、训练时长等）。若未明确说明，也请指出这一点。

- **文中未明确提及**所使用的GPU型号、数量或训练时长。仅提到：
  - 玩具实验中使用GPT-2作为监督模型。
  - 算术和GSM8K实验中使用Llama-3-8B并通过LoRA微调作为监督模型。
  - PRM800K实验中使用GPT-2监督模型。
- **缺失说明**：未报告任何算力资源细节（如A100小时数、训练轮数等），这是论文在重现性方面的一个不足。

## 5. 实验数量与充分性：大概做了多少组实验（如不同数据集、消融实验等），这些实验是否充分、是否客观、公平

- **实验组数**：
  - 玩具算术：5个LLM模型，每个对比3种方法（IG、ORM、MS），并进行了样本级检测（表1、图3）。
  - Llama-3-8B算术：一个真实模型，3种方法对比（表2上半部分、图8-10）。
  - GSM8K受控实验：对比IG和ORM（表2中间部分）。
  - PRM800K：对比IG和ORM（表2下半部分），另有样本级检测。
- **充分性评价**：
  - **优点**：覆盖了从简单到复杂、从受控到真实的数据集，包含合成错误和自然错误；对每种方法都报告了聚合指标（信息增益、正确概率）和样本级指标（准确率、TPR、FPR）；特别设计了LLM3的条件错误场景以暴露基线方法的缺陷。
  - **不足**：
    - 缺少对Math-Shepherd在GSM8K和PRM800K上的实验（文中解释为模型不可用或方法失效）。
    - 缺乏消融实验，例如不同监督模型大小、不同训练数据量对信息增益估计的影响。
    - 未在实际多种LLM（如GPT-4、Llama-2、Mistral等）上进行系统对比，仅测试了Llama-3-8B和GPT-2。
    - 实验规模较小（玩具数据使用15条样本画轨迹图，PRM800K使用了平衡子集筛选中性步骤）。
- **客观性**：阈值选择使用held-out数据集，比较公平；但ORM和MS的阈值选择未明确是否统一优化。

## 6. 论文的主要结论与发现

- **主要结论**：
  - 信息增益能有效识别CoT中的错误步骤，在玩具算术中正确标出每个LLM的错误位置。
  - 在Llama-3-8B算术中，ORM和MS因依赖最终答案正确性或无法区分步骤而失败，而IG成功定位于第三步（求和）。
  - 在GSM8K受控实验中，IG正确识别出“乘法”为错误步骤，而ORM错误地将“减法”也标记为错误（由于伪相关）。
  - 在PRM800K上，IG对人工标注的错误步骤（-1）和中性步骤（0）给出显著更低甚至为负的信息增益，而ORM的平均正确概率无法区分步级质量。
- **发现**：样本级信息增益可用于逐步检测错误，其准确率和TPR均优于ORM和MS。

## 7. 优点：方法或实验设计上有哪些亮点

- **方法层面**：
  - 首次从信息论角度严格形式化CoT推理，提供了理论保证（定理3.3）。
  - 无需任何步级标注数据，仅需问题-答案对，大幅降低评估成本。
  - 可扩展到非线性推理结构（如O1/R1风格的自纠正、回溯），通过条件独立性处理探索路径。
- **实验层面**：
  - 设计精巧的玩具数据集暴露基线方法的伪相关缺陷（LLM3的条件错误）。
  - 在多个数据集上验证，包括受控和真实场景，对比结果清晰。
  - 同时提供聚合级和样本级评价，使评估更全面。

## 8. 不足与局限：包括实验覆盖、偏差风险、应用限制等

- **实验覆盖有限**：
  - 仅测试了Llama-3-8B和GPT-2，未在其他主流模型（如GPT-4、Llama-3-70B、Mistral等）上验证。
  - 缺少消融实验（如监督模型容量、训练数据量对IG的影响）。
  - 未在开放式推理任务（如逻辑规划、常识推理）上验证，仅聚焦数学领域。
- **偏差风险**：
  - 在GSM8K实验中，GPT-4生成的答案可能已经包含系统性偏差（如乘法错误模式固定）。
  - 样本级检测的阈值选择依赖于held-out数据集，未讨论阈值敏感性。
- **应用限制**：
  - 需要额外训练一个监督模型，计算成本较高（尽管比标注数据低）。
  - 仍需对每一步进行子任务分类（如识别该步是加法还是乘法），此步骤可能引入人工或模型辅助误差。
  - 当错误步骤不减少信息增益（如随机噪声仍可能偶然增加信息）时，方法可能失效（文中未深入讨论）。
  - 论文未提供代码或数据开源说明，可复现性存疑。

（完）
