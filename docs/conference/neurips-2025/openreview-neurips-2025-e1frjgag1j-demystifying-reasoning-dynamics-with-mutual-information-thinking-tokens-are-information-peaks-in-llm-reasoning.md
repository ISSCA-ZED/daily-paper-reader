---
title: "Demystifying Reasoning Dynamics with Mutual Information: Thinking Tokens are Information Peaks in LLM Reasoning"
title_zh: 用互信息解密推理动态：思考令牌是LLM推理中的信息峰值
authors: "Chen Qian, Dongrui Liu, Haochen Wen, Zhen Bai, Yong Liu, Jing Shao"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=E1FrjgaG1J"
tags: ["query:key-tokens"]
score: 10.0
evidence: 利用隐藏状态的互信息识别推理过程中的思考令牌作为信息峰值
tldr: 大推理模型内部机制不透明。本文从信息论角度，追踪推理过程中中间表示与正确答案之间的互信息变化，发现互信息峰值现象：在特定生成步骤互信息突然显著增加。理论分析表明互信息增加会降低预测错误概率。这些互信息峰值对应关键的思考令牌，揭示了推理动态的核心。该工作为理解LLM推理中关键令牌的作用提供了因果性解释。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-neurips-2025-e1frjgag1j/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1430, \"height\": 434, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-e1frjgag1j/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1386, \"height\": 520, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-e1frjgag1j/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1389, \"height\": 598, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-e1frjgag1j/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1478, \"height\": 720, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-e1frjgag1j/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1451, \"height\": 469, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-e1frjgag1j/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 708, \"height\": 410, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-e1frjgag1j/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1457, \"height\": 411, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-e1frjgag1j/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1455, \"height\": 416, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-e1frjgag1j/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1310, \"height\": 2300, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-e1frjgag1j/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1229, \"height\": 2357, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-e1frjgag1j/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1315, \"height\": 2335, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-e1frjgag1j/fig-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1242, \"height\": 2368, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-e1frjgag1j/fig-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1314, \"height\": 2338, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-e1frjgag1j/fig-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 1242, \"height\": 2373, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-e1frjgag1j/fig-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 1316, \"height\": 2335, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-e1frjgag1j/fig-016.webp\", \"caption\": \"\", \"page\": 0, \"index\": 16, \"width\": 1243, \"height\": 2377, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-e1frjgag1j/fig-017.webp\", \"caption\": \"\", \"page\": 0, \"index\": 17, \"width\": 1309, \"height\": 2342, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-e1frjgag1j/fig-018.webp\", \"caption\": \"\", \"page\": 0, \"index\": 18, \"width\": 1210, \"height\": 2344, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-e1frjgag1j/fig-019.webp\", \"caption\": \"\", \"page\": 0, \"index\": 19, \"width\": 1311, \"height\": 2327, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-e1frjgag1j/fig-020.webp\", \"caption\": \"\", \"page\": 0, \"index\": 20, \"width\": 1234, \"height\": 2360, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-neurips-2025-e1frjgag1j/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1447, \"height\": 343, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-e1frjgag1j/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1468, \"height\": 279, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-e1frjgag1j/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 779, \"height\": 283, \"label\": \"Table\"}]"
motivation: 缺乏对推理模型内部机制的理解，希望从信息论角度识别关键思考令牌。
method: 追踪推理过程中中间隐藏状态与正确答案间的互信息，检测互信息峰值作为关键令牌。
result: 发现互信息峰值现象，且峰值对应关键思考令牌，互信息增加与预测错误降低相关。
conclusion: 互信息峰值揭示了推理中的关键令牌，为理解推理机制提供了信息论框架。
---

## Abstract
Large reasoning models (LRMs) have demonstrated impressive capabilities in complex problem-solving, yet their internal reasoning mechanisms remain poorly understood.
In this paper, we investigate the reasoning trajectories of LRMs from an information-theoretic perspective. 
By tracking how mutual information (MI) between intermediate representations and the correct answer evolves during LRM reasoning, we observe an interesting MI peaks phenomenon: the MI at specific generative steps exhibits a sudden and significant increase during LRM's reasoning process. 
We theoretically analyze such phenomenon and show that as MI increases, the probability of model's prediction error decreases.
Furthermore, these MI peaks often correspond to tokens expressing reflection or transition, such as "Hmm", "Wait" and "Therefore," which we term as the thinking tokens.
We then demonstrate that these thinking tokens are crucial for LRM's reasoning performance, while other tokens has minimal impacts.
Building on these analyses, we propose two simple yet effective methods to improve LRM's reasoning performance, by delicately leveraging these thinking tokens.
Overall, our work provides novel insights into the reasoning mechanisms of LRMs and offers practical ways to improve their reasoning capabilities.
The code is available at \url{https://github.com/ChnQ/MI-Peaks}.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义（研究动机和背景）

大型推理模型（Large Reasoning Models, LRMs）在数学、编程等复杂推理任务上表现出色，但其内部推理机制仍是一个“黑箱”。现有研究多关注输入输出行为，缺乏对中间推理过程如何影响最终答案的深入理解。本文旨在从**信息论视角**揭示LRM推理的动态机制，具体通过追踪每个生成步骤的隐藏表示与正确答案之间的**互信息（Mutual Information, MI）** 演化，探究是否存在对推理结果起关键作用的“信息峰值”，并据此改进推理性能。

### 2. 论文提出的方法论

#### 核心思想
在LRM的自回归生成过程中，计算第 \(t\) 步的隐藏表示 \(\mathbf{h}_t\) 与正确答案表示 \(\mathbf{h}_y\) 之间的MI，得到MI序列 \(I(\mathbf{h}_1; \mathbf{h}_y), I(\mathbf{h}_2; \mathbf{h}_y), \dots, I(\mathbf{h}_T; \mathbf{h}_y)\)。观察发现，某些步骤的MI会突然显著升高，称为**MI峰值**。这些峰值对应的令牌大多为“Hmm”、“Wait”、“Therefore”等表示反思、转折或自我校正的**思考令牌**。

#### 关键技术细节
1. **MI估计**：使用**希尔伯特-施密特独立性准则（HSIC）** 近似MI（公式(22)），采用高斯核函数，带宽经网格搜索确定。
2. **MI峰值定义**：基于四分位距（IQR）：\(O = \{ t : m_t > Q_3 + \tau \cdot IQR(m) \}\)，\(\tau=1.5\)。
3. **令牌解码**：通过语言模型输出头将MI峰值处的表示 \(\mathbf{h}_t\) 投射到词表空间，贪婪解码获得对应令牌。
4. **理论分析**：
   - **定理1（下界）**：预测错误率 \(p_e \ge \frac{1}{\log(|\mathcal{Y}|-1)}\left[ H(y) - \sum_j I(y; h_j|h_{<j}) - H_b(p_e) \right]\)
   - **定理2（上界）**：\(p_e \le \frac{1}{2} \left[ H(y) - \sum_j I(y; h_j|h_{<j}) \right]\)
   - 核心结论：累积MI越高，预测错误概率的上下界越紧，模型更易得出正确答案。

#### 提出方法
1. **Representation Recycling (RR)**：在MI峰值对应的表示经过某一Transformer层后，不直接传给下一层，而是**将该表示再次输入相同层**进行一次额外处理，以深化信息提取。触发条件：模型生成了预先统计的思考令牌时。
2. **Thinking Token based Test-time Scaling (TTTS)**：在测试时若还有剩余令牌预算，强制模型以思考令牌开头继续生成额外推理步骤，从而持续提升性能。

### 3. 实验设计

- **数据集**：
  - **主实验**：MATH训练集（用于观察MI轨迹）、GSM8K、MATH500、AIME24（用于评估推理性能）。
  - **泛化性验证**：GPQA（科学）、MedQA（医疗）。
- **模型**：
  - LRMs：DeepSeek-R1-Distill系列（7B/8B/14B/32B/70B）、QwQ-32B。
  - 非推理基座：Llama-3.1-8B、Qwen2.5-Math-7B、Qwen2.5-14B/32B、Llama-3.3-70B-Instruct等。
- **对比方法**：
  - 原始LRM vs. 对应非推理LLM（观察MI峰值差异）。
  - 抑制“思考令牌” vs. 抑制相同数量的“非思考令牌”（验证关键性）。
  - RR与原始LRM对比。
  - TTTS与原始LRM在不同令牌预算下的对比。

### 4. 资源与算力

文中在附录B明确说明：
> “All experiments are conducted on four NVIDIA A100 GPUs.”

未提及具体的训练时长或总GPU小时数。由于方法均为推理时干预（无训练），算力消耗主要来自推理和MI计算。

### 5. 实验数量与充分性

- **MI峰值现象验证**：在6个LRM（7B~70B）和4个基座模型上，对MATH训练集100个样本逐一绘制MI轨迹，并统计峰值比例、间隔等（表1）。
- **思考令牌识别与抑制**：在多个模型上展示令牌频率分布（图4/附录D.2），并设计抑制实验（图5），比较抑制思考令牌 vs. 非思考令牌的效果。
- **RR方法**：在2个LRM（8B, 7B）上评估GSM8K、MATH500、AIME24三个基准。
- **TTTS方法**：在LLaMA-8B上评估GSM8K、MATH500、AIME24，改变令牌预算。
- **泛化性**：将MI峰值现象扩展到GPQA和MedQA（表3），并检查对应令牌。

**充分性评价**：实验覆盖多模型、多规模、多领域（数学/科学/医疗），消融对比充分，控制变量得当（抑制数量一致）。局限性在于主要聚焦数学类推理，虽有两个额外领域验证，但泛化性证据仍有限。

### 6. 论文的主要结论与发现

1. **MI峰值现象**：LRM推理过程中，少量步骤（<5%）出现MI显著尖峰，分布稀疏且非均匀。
2. **思考令牌**：MI峰值对应的令牌多为“Hmm”、“Wait”、“Therefore”等反思、转折性表达；抑制它们会严重损害推理性能，而抑制其他令牌影响甚微。
3. **理论关联**：更高的累积MI（尤其是峰值的贡献）能收紧预测错误概率的上界和下界，从而提升推理正确率。
4. **非推理模型无此现象**：对应基座模型（如Llama-3.1-8B）的MI峰值更弱，表明该现象来自推理增强训练。
5. **改进方法有效**：
   - Representation Recycling (RR) 在多个基准上持续提升性能，尤其在AIME24上提升显著（DeepSeek-R1-Distill-Llama-8B相对提高20%）。
   - Thinking Token based Test-time Scaling (TTTS) 在增加推理预算时，性能稳定提升，优于原始LRM。

### 7. 优点

- **新颖视角**：首次从信息论（互信息）角度系统解释LRM推理动态，提出“信息峰值-思考令牌”关联。
- **理论+实验结合**：在Fano不等式基础上推导出误差边界与累积MI的关系，为现象提供理论支持。
- **实用方法**：RR和TTTS均为训练无关、简单易实现的方法，却能在多个基准上带来一致改进，具有实际应用价值。
- **严谨分析**：通过抑制实验、基座对比、区间统计等充分验证了MI峰值和思考令牌的因果重要性。

### 8. 不足与局限

- **粒度局限**：仅分析令牌级别的MI动态，未考虑按语义片段或逻辑步骤划分，可能遗漏更宏观的推理结构。
- **MI峰值成因未深究**：论文指出现象可能源于推理增强训练，但未进一步探究训练过程中的成因（如强化学习如何塑造这些峰值）。
- **计算开销**：RR需要在推理时触发额外前向计算（同一层重复处理），TTTS则增加生成长度，虽无训练成本但推理时间可能增加。
- **领域覆盖**：主要实验基于数学推理，虽然扩展至科学和医疗，但领域多样性仍有限，其在更广泛推理任务（如常识推理、多跳问答）中的普遍性有待验证。
- **HSIC近似误差**：MI估计依赖HSIC，且需要网格搜索带宽，可能存在近似偏差。
- **未讨论错误积累与步骤长度的关系**：虽然理论部分提及了噪声函数扩展的可能性（附录C），但正文实验中未考虑过长推理导致性能下降的情况。

（完）
