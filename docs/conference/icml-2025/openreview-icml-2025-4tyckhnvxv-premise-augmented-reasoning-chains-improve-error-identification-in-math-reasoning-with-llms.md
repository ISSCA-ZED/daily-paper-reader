---
title: Premise-Augmented Reasoning Chains Improve Error Identification in Math reasoning with LLMs
title_zh: 前提增强推理链提升数学推理中的错误识别
authors: "Sagnik Mukherjee, Abhinav Chinta, Takyoung Kim, Tarun Anoop Sharma, Dilek Hakkani Tur"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=4tYckHNVXV"
tags: ["query:key-tokens"]
score: 6.0
evidence: 识别推理链中的前提作为关键元素用于错误检测
tldr: 针对CoT推理链过长导致错误难以追踪的问题，本文提出前提增强推理链，为每一步识别其依赖的前提子集。该方法通过结构化推理步骤，提升了错误识别能力，为改进推理验证提供了新视角。
source: ICML-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2025-4tyckhnvxv/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1629, \"height\": 532, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-4tyckhnvxv/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1657, \"height\": 922, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-icml-2025-4tyckhnvxv/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1556, \"height\": 376, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-4tyckhnvxv/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1212, \"height\": 361, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-4tyckhnvxv/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1744, \"height\": 928, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-4tyckhnvxv/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 820, \"height\": 426, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-4tyckhnvxv/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 722, \"height\": 372, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-4tyckhnvxv/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 778, \"height\": 492, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-4tyckhnvxv/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 777, \"height\": 494, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-4tyckhnvxv/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1749, \"height\": 962, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-4tyckhnvxv/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1221, \"height\": 375, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-4tyckhnvxv/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1218, \"height\": 375, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-4tyckhnvxv/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1221, \"height\": 375, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-4tyckhnvxv/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1221, \"height\": 372, \"label\": \"Table\"}]"
motivation: 长推理链中步骤间依赖难以追踪，需识别关键前提。
method: 将线性推理链重构成前提增强结构，明确每一步的依赖前提。
result: 提升了数学推理中的错误识别效果。
conclusion: 前提识别有助于提高LLM推理的可靠性和可验证性。
---

## Abstract
Chain-of-Thought (CoT) prompting enhances mathematical reasoning in large language models (LLMs) by enabling detailed step-by-step solutions. However, due to the verbosity of LLMs, the resulting reasoning chains can be long, making it harder to verify the reasoning steps and trace issues resulting from dependencies between the steps that may be farther away in the sequence of steps. Importantly, mathematical reasoning allows each step to be derived from a small set of premises, which are a subset of the preceding steps in the reasoning chain. In this paper, we present a framework that identifies the premises for each step, to improve the evaluation of reasoning. We restructure conventional linear reasoning chains into Premise Augmented Reasoning Chains (PARC) by introducing premise links, resulting in a directed acyclic graph where the nodes are the steps and the edges are the premise links. Through experiments with a PARC-based dataset that we built, namely (Premises and ERrors identification in LLMs), we demonstrate that LLMs can reliably identify premises within complex reasoning chains. In particular, even open-source LLMs achieve 90% recall in premise identification.  We also show that PARC helps to identify errors in reasoning chains more reliably. The accuracy of error identification improves by 6% to 16% absolute when step-by-step verification is carried out in PARC under the premises.
Our findings highlight the utility of premise-centric representations in addressing complex problem-solving tasks and open new avenues for improving the reliability of LLM-based reasoning evaluations.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 核心问题与整体含义（研究动机与背景）

- **研究动机**：大型语言模型（LLMs）通过链式思维（CoT）提示在数学推理中取得了显著进步，但生成的推理链可能很长，导致步骤间的依赖关系难以追踪，验证推理的正确性变得困难。现有的错误识别方法要么依赖昂贵的人工标注（reference-based），要么只能给出整体分数而无法定位具体错误（reference-free），且容易受到无关上下文信息的干扰。
- **整体含义**：本文提出前提增强推理链（PARC），通过为每个推理步骤明确识别其依赖的**前提子集**（即前序步骤中的必要信息），将线性推理链转化为有向无环图，从而提升错误识别的准确性和可解释性。这项工作为LLM推理评估提供了更细粒度、更可靠的验证方法。

## 2. 方法论

- **核心思想**：数学推理中，每一步都可以从一小部分前提（前序步骤）推导出来。通过显式标注这些前提，可以剔除无关上下文，使得每个步骤的验证只依赖必要信息，从而减少LLM在长上下文中的分心，提高错误检测能力。
- **关键技术细节**：
  - **定义前提**：对于步骤 \(s_i\)，其前提 \(P_i \subseteq \{s_j \mid j < i\}\) 满足可验证性和最小性。可验证性指仅凭 \(P_i\) 即可判断 \(s_i\) 正确性；最小性指移除任意元素后步骤不再可验证。
  - **PARC构建**：将线性推理链 \(r_{\le t} = [s_1, s_2, \ldots, s_t]\) 转换为 \(r'_{\le t} = [(s_1, P_1), \ldots, (s_t, P_t)]\)，形成有向无环图。
  - **前提映射方法**：
    - **聚合式（Aggregative）**：一次查询LLM，给出当前步骤所有前提。
    - **二分式（Dyadic）**：逐对判断每个前序步骤是否为当前步骤的前提（\(O(n^2)\) 复杂度）。
  - **错误识别流程**（算法1）：
    1. 对每个步骤 \(s_k\) 提取前提 \(P_k\)。
    2. 分别检测**数学错误**（仅检查步骤本身的计算）和**逻辑不一致**（检查步骤是否与前提矛盾）。
    3. 通过图遍历检测**累积错误**：如果步骤本身正确但某个前提错误，则标记为累积错误。累积错误是本文新引入的类型，指那些局部正确但继承上游错误的步骤。
  - **验证方式**：在PARC结构中，每一步的错误分类仅在前提上下文中进行，而非全上下文。

## 3. 实验设计

- **数据集**：
  - **PERL数据集**：基于GSM8K、MATH、Orca-Math、MetaMathQA四个数学基准构建。从每个数据集中随机采样1000个样本，用Llama-3.1-8B生成推理链，再根据最终答案正误分为正/负样本，并利用GPT-4o引入合成错误（synthetic negatives）。最后用o1-Preview模型标注前提和错误类型。总计607个推理链，含2134个正确步骤、321个数学错误、443个逻辑不一致、741个累积错误。
  - **ProcessBench**：作为额外基准，仅包含到第一个错误步骤为止的标注。
- **基准方法（Baseline）**：在零样本设置下，将整个问题、已有推理链和当前步骤作为上下文，要求LLM直接分类错误类型（正确/数学错误/逻辑不一致/累积错误）。
- **对比方法**：
  - 完全上下文（Full Context）基线。
  - 本文的**前提增强验证**（PARC），包括使用oracle前提和模型自提取前提两种情况。
  - 进一步在前提映射中对比聚合式与二分式。
- **模型**：Llama 3.1 8B/70B, Qwen 2.5 7B/32B/72B, GPT4o-mini, GPT-4o。所有模型使用温度0，确保可重复性。

## 4. 资源与算力

- **未明确说明**：文中仅提到使用vLLM和AzureOpenAI进行模型服务，但未给出具体GPU型号、数量或训练时长。推测实验基于推理（inference）而非训练，因此算力需求相对较低。

## 5. 实验数量与充分性

- **实验数量**：较为充分。包括：
  - 前提映射实验：在4个数据集上测试聚合式和二分式，报告Precision/Recall/F1（表1、2）。
  - 错误识别实验：在4个数据集、3种设定（完全上下文、oracle前提、模型前提）下测试6个模型（表3），并分解为Neg/Syn/Pos三个子集。
  - 消融实验：对比oracle前提与模型前提（表4）。
  - 错误类型细粒度分析（表5）。
  - 额外在ProcessBench上验证（表6、7）。
  - 附录中提供按数据集和模型的具体子集结果（表8-12）。
- **充分性评价**：实验覆盖了多种模型规模、多个数据集、不同前提提取策略，并进行了oracle消融，设计比较全面。但主要局限在数学领域，且PERL数据集的标注依赖o1-Preview，可能存在标注噪声。

## 6. 主要结论与发现

- **前提可被高效识别**：LLMs能以高召回（≥90%）识别步骤的前提，聚合式优于二分式。
- **前提增强提升错误识别**：在PARC下进行步骤验证，错误识别准确率绝对提升6%–16%（表3）。
- **累积错误是难点**：传统的完全上下文方法对累积错误识别极差（如仅12%–13%准确率），而PARC方法显著提升其识别（例如70B模型从12%升至57.5%）。
- **合成负例高估性能**：模型在合成负例上的表现远高于真实负例，说明仅用有扰动数据评估会带来过于乐观的结果。
- **模型前提与oracle前提接近**：由于前提识别召回率高，使用模型自提取前提的误差识别性能与使用oracle前提相当。

## 7. 优点

- **方法创新**：将物理/数学推理中“前提”概念引入LLM推理评估，通过结构化解耦步骤依赖，显著提升错误定位能力。
- **细粒度评估**：不仅识别总体错误，还能区分数学错误、逻辑错误和累积错误，提供可解释的步骤级反馈。
- **参考无关性**：无需人工标注黄金推理链，适用于零样本场景。
- **广泛适用性**：模型无关，在多种开源和闭源LLM上效果一致提升。
- **新数据集**：贡献PERL数据集（含前提和错误标注），促进后续研究。

## 8. 不足与局限

- **领域局限**：仅在数学推理上验证，未扩展到其他需要多步推理的领域（如常识推理、科学推理）。
- **前提定义依赖可验证性假设**：数学推理中前提易于识别，但其他任务中前提可能模糊，且“最小性”的实现依赖LLM判断，缺乏形式化保证。
- **累积错误定义依赖前提正确性**：若前提识别有漏，可能误判。
- **数据标注偏差**：PERL的标注由o1-Preview完成，虽然人工校验10%后认同度较高，但仍存在标注噪声。
- **计算开销**：聚合式需要为每个步骤单独调用LLM，二分式复杂度为\(O(n^2)\)，在长链中代价较高。
- **错误识别仍有限**：即使PARC提升明显，模型对数学错误和逻辑不一致的识别准确率仍有较大提升空间（如表5中GPT-4o在负样本上仅55%左右）。

（完）
