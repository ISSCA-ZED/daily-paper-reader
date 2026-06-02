---
title: "R2R: Efficiently Navigating Divergent Reasoning Paths with Small-Large Model Token Routing"
title_zh: "R2R: 通过大小模型令牌路由高效导航分歧推理路径"
authors: "Tianyu Fu, Yi Ge, Yichen You, Enshu Liu, Zhihang Yuan, Guohao Dai, Shengen Yan, Huazhong Yang, Yu Wang"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=DpeJYRFRQY"
tags: ["query:key-tokens"]
score: 9.0
evidence: 识别导致LLM与SLM推理路径分歧的关键令牌
tldr: 大型语言模型推理开销大，蒸馏小模型性能不佳。本文发现LLM与小模型之间的推理路径分歧仅由少数令牌引起，其余令牌大多一致或中性。基于此洞察，提出R2R神经令牌路由器，仅对关键分歧令牌使用LLM，其余由小模型处理，从而兼顾效率与性能。实验证明R2R在保持推理质量的同时大幅降低推理成本。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-neurips-2025-dpejyrfrqy/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1452, \"height\": 230, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-dpejyrfrqy/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1444, \"height\": 235, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-dpejyrfrqy/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1451, \"height\": 350, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-dpejyrfrqy/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1349, \"height\": 356, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-dpejyrfrqy/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 648, \"height\": 568, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-dpejyrfrqy/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1424, \"height\": 383, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-dpejyrfrqy/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1350, \"height\": 349, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-dpejyrfrqy/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 682, \"height\": 467, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-dpejyrfrqy/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 690, \"height\": 454, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-dpejyrfrqy/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1353, \"height\": 358, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-neurips-2025-dpejyrfrqy/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1325, \"height\": 277, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-dpejyrfrqy/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1378, \"height\": 455, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-dpejyrfrqy/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1453, \"height\": 675, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-dpejyrfrqy/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 750, \"height\": 573, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-dpejyrfrqy/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1456, \"height\": 282, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-dpejyrfrqy/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1433, \"height\": 319, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-dpejyrfrqy/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1252, \"height\": 357, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-dpejyrfrqy/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 959, \"height\": 397, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-dpejyrfrqy/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1079, \"height\": 419, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-dpejyrfrqy/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 989, \"height\": 313, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-dpejyrfrqy/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1124, \"height\": 417, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-dpejyrfrqy/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 726, \"height\": 261, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-dpejyrfrqy/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1282, \"height\": 302, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-dpejyrfrqy/table-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 975, \"height\": 238, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-dpejyrfrqy/table-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 793, \"height\": 377, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-dpejyrfrqy/table-016.webp\", \"caption\": \"\", \"page\": 0, \"index\": 16, \"width\": 1078, \"height\": 730, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-dpejyrfrqy/table-017.webp\", \"caption\": \"\", \"page\": 0, \"index\": 17, \"width\": 1201, \"height\": 295, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-dpejyrfrqy/table-018.webp\", \"caption\": \"\", \"page\": 0, \"index\": 18, \"width\": 750, \"height\": 456, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-dpejyrfrqy/table-019.webp\", \"caption\": \"\", \"page\": 0, \"index\": 19, \"width\": 1331, \"height\": 279, \"label\": \"Table\"}]"
motivation: LLM推理开销大，蒸馏小模型性能下降，希望识别并利用关键分歧令牌来平衡效率与性能。
method: 提出R2R，一个神经令牌路由器，检测LLM与小模型间的关键分歧令牌，并仅对这些令牌使用LLM推理。
result: 仅少数令牌导致路径分歧，R2R在保持推理质量的同时显著降低推理开销。
conclusion: 关键推理令牌的识别可用于高效推理路由，为模型部署提供新思路。
---

## Abstract
Large Language Models (LLMs) achieve impressive reasoning capabilities at the cost of substantial inference overhead, posing substantial deployment challenges. Although distilled Small Language Models (SLMs) significantly enhance efficiency, their performance suffers as they fail to follow LLMs' reasoning paths. Luckily, we reveal that only a small fraction of tokens genuinely diverge reasoning paths between LLMs and SLMs. Most generated tokens are either identical or exhibit neutral differences, such as minor variations in abbreviations or expressions. Leveraging this insight, we introduce **Roads to Rome (R2R)**, a neural token router that selectively utilizes LLMs only for these critical, path-divergent tokens, while leaving the majority of token generation to the SLM. We also develop an automatic data generation pipeline that identifies divergent tokens and generates token-level routing labels to train the lightweight router. We apply R2R to combine R1-1.5B and R1-32B models from the DeepSeek family, and evaluate on challenging math, coding, and QA benchmarks. With an average activated parameter size of 5.6B, R2R surpasses the average accuracy of R1-7B by 1.6×, outperforming even the R1-14B model. Compared to R1-32B, it delivers a 2.8× wall-clock speedup with comparable performance, advancing the Pareto frontier of test-time scaling efficiency.

---

## 论文详细总结（自动生成）

# 论文详细中文总结：R2R: 通过大小模型令牌路由高效导航分歧推理路径

## 1. 核心问题与整体含义（研究动机和背景）

- **背景**：大型语言模型（LLM）在推理任务中表现出色，但推理成本极高（需要生成数千token的思维链）。蒸馏得到的小语言模型（SLM）虽然推理高效，但推理路径常与LLM偏离，导致性能严重下降（例如R1-1.5B在AIME上的准确率仅为R1-32B的1/4左右）。
- **关键发现**：作者通过分析发现，SLM与LLM在同一上下文下的下一个token预测中，约89%的token完全相同，5%的差异属于中性差异（如“let’s” vs “let us”），仅约6%的token才真正导致推理路径分歧（称为“divergent tokens”）。因此，性能差距主要由这些少数关键token的累积误差引起。
- **核心问题**：能否通过仅替换这些分歧token，让SLM跟随LLM的推理路径，从而以接近SLM的成本获得接近LLM的推理质量？
- **整体含义**：提出一种token级别的模型路由方法，在推理时动态决定每个token由哪个模型生成，从而在效率与性能之间取得更好的Pareto前沿。

## 2. 论文提出的方法论

### 核心思想
- **Roads to Rome (R2R)**：训练一个轻量级神经路由器，在SLM推理时实时预测当前token是否为“分歧token”，若是则立即调用LLM修正，否则由SLM继续生成。这样避免了LLM处理大多数“安全”token，同时防止了分歧累积。

### 关键技术细节
1. **分歧token的自动标注管道**：
   - 首先使用LLM生成完整响应作为目标推理路径。
   - 然后让SLM预填充该路径，识别SLM与LLM下一个token预测不同的位置（约10%）。
   - 对于每个不同的SLM token，使用LLM从该点继续生成一个完整句子（句子级continuation），同时从对应的LLM token继续生成另一个句子。
   - 使用一个LLM验证器（Qwen2.5-72B）判断这两个句子是否在语义、逻辑上产生分歧。若分歧则标记为“divergent”（需要LLM路由），否则标记为“neutral”（可接受SLM）。
   - 该标注方法大幅降低了搜索复杂度（从O(2^n)降至O(n)）。

2. **神经路由器设计**：
   - **输入特征**：SLM的top-100 logits、token嵌入、最后一层隐藏状态（利用logits熵和token频率等预测性指标）。
   - **架构**：6层前馈网络（FFN），约56M参数，输出一个[0,1]之间的分歧概率。
   - **训练**：使用交叉熵损失，通过逆类频率加权缓解类别不平衡。离线训练后，通过验证集调整路由阈值以满足目标LLM使用率。

3. **推理时路由方案**：
   - 每步SLM解码后，路由器立即预测分歧概率。若超过阈值p_th，则丢弃SLM当前token，让LLM生成一个替换token（通过高效prefill）。否则使用SLM的token。
   - 与投机解码（speculative decoding）不同，R2R无需周期性验证和回滚，避免了无效计算。

### 公式与算法流程（文字说明）
- 定义一个路由函数R(S_{<i}, θ_s, θ_l)，根据上下文选择模型。
- 路径跟随策略：若SLM和LLM下一个token相同，或经过句子级续写验证判定为中性，则选择SLM；否则路由到LLM。
- 实际推理时，由训练好的神经网络近似这一策略。

## 3. 实验设计

### 数据集和场景
- **数学推理**：AIME 2024–2025（共60题）。
- **研究级问答**：GPQA-Diamond（198题）。
- **代码生成**：LiveCodeBench 2024-08至2025-01。
- **额外泛化测试**：Arena-Hard（对话）、MMLU-Redux-Philosophy（哲学问答）。
- **训练数据来源**：Bespoke-Stratos-17k数据集中的数学、代码、QA问题，利用R1-32B生成响应后标注。

### Benchmark
- 所有实验使用贪心解码（temperature=0），最大输出长度32K token。
- 效率指标：平均每token激活参数量（¯M）、总成本（C = ¯M × 平均输出token数）、真实壁钟速度。

### 对比方法
- **蒸馏模型**：R1-7B、R1-14B（蒸馏自R1-32B）。
- **查询级路由（QR）**：RouteLLM框架下的SW、MF、BERT、LLM四种变体。
- **投机解码**：EAGLE2、HASS（均使用R1-32B作为LLM）。
- **基线和极值**：纯SLM（R1-1.5B）和纯LLM（R1-32B）。
- **额外验证**：Qwen3系列（0.6B~32B）、MoE模型（Qwen3-30BA3B）。

## 4. 资源与算力

- **数据生成**：在8张NVIDIA A800-80GB GPU上运行，总耗时约56小时（448 GPU小时），生成760万个token级别的路由标签。
  - 各阶段耗时：LLM响应生成35小时，SLM预填充0.1小时，LLM续写7小时，验证14小时。
- **路由器训练**：未明确总时长，但提到训练50个epoch，早停，使用单张GPU（推断可行）。
- **推理**：使用2张A800-80GB GPU，采用SGLang框架进行张量并行。R2R的56M参数路由器部署在GPU上，开销极小（占推理总时间的5.96%）。

## 5. 实验数量与充分性

- **主要性能比较**（表2、图5）：在三个基准上对比超过10种方法，覆盖不同参数规模。
- **效率对比**（表3）：包括壁钟延迟、输出速度、计算量和内存访问分析。
- **消融实验**（表4）：路由目标（divergent vs different vs 简化输入）、输入特征（去掉logits、token嵌入等）、不同SLM-LLM组合，全面验证设计选择。
- **路由行为分析**（图6）：LLM使用率在思考与回复阶段、每个思考内部的分布，提供定性洞察。
- **泛化性实验**：
  - 跨基准泛化（Arena-Hard、MMLU-Redux-Philosophy）。
  - 跨模型族泛化（R1→Qwen3）。
  - 跨不同LLM组合（0.6B+8B的router迁移到0.6B+32B）。
- **采样方法扩展**（表18）：验证在nucleus采样和temperature下仍然有效。
- **MoE兼容性**（表14）：将R2R应用于MoE LLM，进一步改善效率。
- **总成本-性能对比**（图11）。
- **局限性分析**：系统性失败案例分析（表16）。

**充分性与公平性评价**：实验设计全面，覆盖多种任务、模型和配置；对比方法均为领域内最新或强基线；效率指标硬件无关（平均参数）和硬件相关（壁钟速度）兼顾；使用贪心解码确保可重复性；消融实验针对每个关键组件。整体实验充分且客观。

## 6. 主要结论与发现

1. **R2R显著推进了Pareto前沿**：以平均5.6B参数（仅使用11-15% LLM token）达到R1-14B级甚至超过的性能（平均准确率46% vs R1-14B的43%），同时速度比R1-32B快2.8倍。
2. **分歧token的识别是关键**：仅替换分歧token而非所有不同token，就能以极低LLM使用率实现高质量推理。
3. **SLM logits和token频率是强预测指标**：分歧token的平均熵是非分歧token的3.8倍，低频率token更易分歧。
4. **路由器自动学习路由模式**：LLM在思考的开头和结尾更频繁被使用，而回复阶段使用率低，模式符合直觉。
5. **泛化性强**：在未训练的基准（对话、哲学）和不同模型族上仍能超越蒸馏模型。
6. **与MoE等正交技术兼容**：可以进一步降低平均参数量。

## 7. 优点

- **新颖的token级路由范式**：不同于粗糙的查询级路由，R2R在token粒度动态切换模型，更精细地平衡成本和效果。
- **自动数据标注流程有效**：句子级路径跟随策略大幅降低了标注复杂度，同时保证质量（与人类专家验证结果高度一致）。
- **路由器设计轻巧且有效**：仅56M参数，利用SLM自带的logits和hidden states作为输入，无需额外计算，推理开销极小（<6%）。
- **即时路由消除回滚**：对比投机解码，R2R不必等待周期性验证，避免了无效的draft和回滚，对系统级批量服务尤其友好。
- **实验非常全面**：覆盖数学、代码、QA、对话、哲学等多领域，检验了蒸馏、查询级路由、投机解码等多种基线，并在不同模型族（DeepSeek、Qwen3）和架构（密集、MoE）上验证了泛化性。
- **效率分析细致**：除壁钟速度外，还分析了计算量（TFLOPs）和内存访问量，证明内存带宽是主要瓶颈且R2R显著降低。
- **公开代码和模型**：有助于复现和后续研究。

## 8. 不足与局限

- **贪心解码的局限性**：主要针对贪心采样设计和测试，虽然提供了nucleus采样的初步实验，但全面性不足（如temperature、top-k等未深入探索）。
- **验证器依赖**：标注阶段依赖另一个LLM（Qwen2.5-72B）作为验证器，引入额外计算开销和潜在的偏差（如验证器本身可能不够鲁棒）。
- **路由器泛化边界**：虽然跨基准和模型族表现良好，但训练数据主要来自数学、代码、QA领域，对极度专业或长尾领域（如法律、医学）的泛化性未验证。
- **句子级假设的简化**：使用句子级continuation代替完整路径，虽已验证近似性好，但可能漏掉跨句子才显现的分歧（如篇章层面逻辑重组），论文通过N句子实验表明影响微小，但未覆盖所有场景。
- **系统级优化有限**：虽然实现了SGLang集成，但仅用2张GPU，未评估更大规模部署（如多节点、连续批量）下的调度开销。
- **未与其他最近token级方法对比**：论文提到CITER、RSD等并发工作，但没有实验对比，比较范围局限于查询级路由和投机解码。
- **准确性上限**：R2R的准确率仍低于纯LLM（R1-32B）约8个百分点（92%），部分问题因推理未完成（32K token限制）导致，需要更仔细的处理。
- **阈值选择依赖验证集**：用户需根据验证集调整阈值，若目标任务分布与验证集差异大，可能需要重新标定，增加了使用成本。

（完）
