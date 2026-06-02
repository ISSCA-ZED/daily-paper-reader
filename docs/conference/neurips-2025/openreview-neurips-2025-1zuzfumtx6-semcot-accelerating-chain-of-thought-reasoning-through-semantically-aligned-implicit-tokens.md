---
title: "SemCoT: Accelerating Chain-of-Thought Reasoning through Semantically-Aligned Implicit Tokens"
title_zh: SemCoT：通过语义对齐的隐式token加速链式推理
authors: "Yinhan He, Wendy Zheng, Yaochen Zhu, Zaiyi Zheng, Lin Su, Sriram Vasudevan, Qi Guo, Liangjie Hong, Jundong Li"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=1ZuzFUMtx6"
tags: ["query:key-tokens"]
score: 5.0
evidence: 使用隐藏嵌入（隐式token）进行推理步骤
tldr: 提出SemCoT方法，将推理步骤编码为隐藏嵌入（隐式token），加速链式推理。该方法涉及对隐藏状态中推理token的语义对齐分析，与关键token的隐藏状态研究相关，但主要目标为加速而非分析。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-neurips-2025-1zuzfumtx6/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1432, \"height\": 491, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-1zuzfumtx6/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1449, \"height\": 702, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-1zuzfumtx6/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1449, \"height\": 486, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-1zuzfumtx6/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 916, \"height\": 460, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-1zuzfumtx6/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1439, \"height\": 512, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-1zuzfumtx6/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1447, \"height\": 602, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-1zuzfumtx6/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1449, \"height\": 602, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-1zuzfumtx6/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1444, \"height\": 858, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-1zuzfumtx6/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1444, \"height\": 864, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-1zuzfumtx6/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1427, \"height\": 788, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-1zuzfumtx6/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1427, \"height\": 787, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-1zuzfumtx6/fig-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1433, \"height\": 767, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-1zuzfumtx6/fig-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1428, \"height\": 790, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-1zuzfumtx6/fig-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 1431, \"height\": 796, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-1zuzfumtx6/fig-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 1451, \"height\": 793, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-1zuzfumtx6/fig-016.webp\", \"caption\": \"\", \"page\": 0, \"index\": 16, \"width\": 1453, \"height\": 759, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-1zuzfumtx6/fig-017.webp\", \"caption\": \"\", \"page\": 0, \"index\": 17, \"width\": 1435, \"height\": 778, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-neurips-2025-1zuzfumtx6/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1439, \"height\": 885, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-1zuzfumtx6/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1468, \"height\": 2049, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-1zuzfumtx6/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1460, \"height\": 1762, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-1zuzfumtx6/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1065, \"height\": 266, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-1zuzfumtx6/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 687, \"height\": 269, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-1zuzfumtx6/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1514, \"height\": 2080, \"label\": \"Table\"}]"
motivation: 显式CoT推理冗长，隐式CoT丢失语义对齐。
method: 将推理步骤编码为与自然语言语义对齐的隐式token。
result: 在保持推理准确性的同时显著减少生成token数。
conclusion: 语义对齐的隐式token能有效加速CoT。
---

## Abstract
Chain-of-Thought (CoT) enhances the performance of Large Language Models (LLMs) on reasoning tasks by encouraging step-by-step solutions. However, the verbosity of CoT reasoning hinders its mass deployment in efficiency-critical applications. Recently, implicit CoT approaches have emerged, which encode reasoning steps within LLM's hidden embeddings (termed ``implicit reasoning'') rather than explicit tokens. This approach accelerates CoT reasoning by reducing the reasoning length and bypassing some LLM components. However, existing implicit CoT methods face two significant challenges: (1) they fail to preserve the semantic alignment between the implicit reasoning (when transformed to natural language) and the ground-truth reasoning, resulting in a significant CoT performance degradation, and (2) they focus on reducing the length of the implicit reasoning; however, they neglect the considerable time cost for an LLM to generate one individual implicit reasoning token. To tackle these challenges, we propose a novel semantically-aligned implicit CoT framework termed **SemCoT**. In particular, for the first challenge, we design a contrastively trained sentence transformer that evaluates semantic alignment between implicit and explicit reasoning, which is used to enforce semantic preservation during implicit reasoning optimization. To address the second challenge, we introduce an efficient implicit reasoning generator by finetuning a lightweight language model using knowledge distillation. This generator is guided by our sentence transformer to distill ground-truth reasoning into semantically aligned implicit reasoning, while also optimizing for accuracy. SemCoT is the first approach that enhances CoT efficiency by jointly optimizing token-level generation speed and preserving semantic alignment with ground-truth reasoning. Extensive experiments demonstrate the superior performance of SemCoT compared to state-of-the-art methods in both efficiency and effectiveness. Our code can be found at https://github.com/YinhanHe123/SemCoT/.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 核心问题与整体含义（研究动机和背景）
- **研究动机**：Chain-of-Thought (CoT) 能显著提升大语言模型（LLM）在推理任务上的表现，但其生成的显式推理步骤冗长，导致推理时间过长，不适合效率敏感的应用。
- **现有隐式 CoT 方法**：将推理步骤编码为 LLM 的隐藏嵌入（隐式 token），从而减少推理长度并跳过一些 LLM 组件。但存在两大挑战：
  1. **语义对齐不足**：隐式推理与真实推理（自然语言）之间的语义对齐差，导致性能下降。
  2. **生成速度瓶颈**：现有方法只关注减少推理长度，却忽略了生成单个隐式 token 的时间成本（尤其在大规模 LLM 中，如 DeepSeek-R1 生成一个 token 约需 0.1 秒）。

## 2. 方法论
- **核心思想**：提出 **SemCoT** 框架，通过两个步骤联合优化隐式 CoT 的语义对齐和生成效率。
- **第一步：语义对齐评估**
  - 训练一个定制的句子变换器（customized sentence transformer），采用对比学习，评估隐式推理与真实推理之间的语义对齐程度。
  - 该变换器由 LLM 的中间五层、池化层和线性层构成，计算两个推理的语义嵌入的余弦相似度。
  - 训练数据：使用 GPT-4o-mini 为每个真实推理生成一个“最紧凑但语义对齐”的推理文本，形成正负样本对。
  - 损失函数：对比损失 \( \mathcal{L}_{\text{sim}} \)。
- **第二步：高效隐式推理生成**
  - 使用轻量级语言模型（如从原 LLM 蒸馏或剪枝得到的 Sheared-LLaMA-1.3B 或 mistral-1.1b-testing）作为隐式推理生成器。
  - 在轻量级 LM 后加一个线性投影层，将其最后一层隐藏嵌入映射到 LLM 的嵌入空间，作为隐式推理 token。
  - 优化目标：结合两个损失：
    - 预测损失 \( \mathcal{L}_{\text{pred}} \)：使 LLM 能根据隐式推理正确生成答案（交叉熵）。
    - 语义对齐损失 \( \mathcal{L}_{\text{sem}} \)：使用第一步训练好的句子变换器，最小化隐式推理与真实推理语义嵌入的余弦距离。
  - 总损失：\( \mathcal{L}_{\text{total}} = \lambda \mathcal{L}_{\text{sem}} + (1-\lambda) \mathcal{L}_{\text{pred}} \)。
- **推理阶段**：将查询与 k 个 `<CoT>` token 拼接，由轻量级 LM 生成隐式推理，再送入 LLM 生成最终答案。

## 3. 实验设计
- **数据集**：5 个代表性数据集，涵盖三种推理类型：
  - **数学推理**：GSM8K、SVAMP、MultiArith
  - **常识推理**：CommonsenseQA
  - **符号推理**：CoinFlip
- **评估 LLM**：Llama-2-7b-chat-hf 和 Mistral-7B-Instruct-v0.2（两个 7B 模型）。
- **轻量级 LM**：
  - 对 Llama-2 使用 Sheared-LLaMA-1.3B
  - 对 Mistral 使用 mistral-1.1b-testing
- **对比的基线方法**：
  - Pause、ICoT-SI、COCONUT、CODI、SoftCoT
- **评估指标**：答案准确率（Acc，%）和平均壁钟推理时间（Time，秒）。
- **实现细节**：句子变换器输出维度 768；训练时隐式 token 数为 5，评估时减为 1；优化器 AdamW；推理时最多生成 30 个答案 token。

## 4. 资源与算力
- 论文在附录 C 中提及：“All experiments on multiple machines with NVIDIA H100 80GB GPUs running CUDA 12.4”，但未明确给出使用的 GPU 数量、训练时长等具体数值。因此，算力消耗未详细量化。

## 5. 实验数量与充分性
- **实验数量**：
  - 主实验（表 1）：5 个数据集 × 2 个 LLM × 6 种方法 = 60 组条目（含准确率和时间，每个实验重复 3 次取均值标准差）。
  - 消融实验（图 3、图 6、图 7）：3 种变体（SemCoT-NSA、SemCoT-NST、SemCoT-NLL）在全部 5 个数据集和 2 个 LLM 上进行，共约 30 组比较。
  - 参数敏感性实验（图 4、图 8、图 9）：考察 λ 和隐式 token 数 M 的影响，涵盖所有数据集和 LLM。
  - 案例研究（图 5、附录 D.3）：对 SemCoT 与 COCONUT 等基线进行 PCA 可视化，展示语义对齐效果。
- **充分性评价**：实验覆盖多领域、多模型，消融和敏感性分析完备，重复次数合理（3 次），报告了误差棒。整体设计客观公平。

## 6. 主要结论与发现
- **效率与效果双优**：SemCoT 在大多数数据集和 LLM 上取得了最高的准确率，同时推理时间接近最快（略慢于 SoftCoT 但准确率更高）。
- **语义对齐有效**：消融实验显示，移除语义对齐损失（SemCoT-NSA）会导致性能明显下降；使用自定义句子变换器比简单用余弦相似度（SemCoT-NST）更好。
- **轻量级 LM 优于全模型微调**：SemCoT-NLL（用原 LLM 生成隐式推理）性能低于 SemCoT，可能因为灾难性遗忘。
- **隐式 token 数越少效果越好**：使用 1 个隐式 token 时准确率最高，表明隐式推理可以高度压缩信息。

## 7. 优点
- **方法创新性**：首次联合优化 token 级生成速度与语义对齐，提出定制句子变换器来弥合隐式嵌入与自然语言的语义鸿沟。
- **高效性**：使用剪枝/蒸馏的轻量级 LM 大幅降低单 token 生成时间，且线性投影层能有效对齐嵌入空间。
- **实验扎实**：涵盖 5 个数据集、2 种 LLM、5 个基线，消融和参数分析全面，结果统计可靠。
- **可复现性**：提供了开源代码链接，并披露了关键超参数。

## 8. 不足与局限
- **额外训练开销**：句子变换器需要额外训练，可能不适用于资源受限环境。
- **泛化性有限**：仅测试了 Llama-2 和 Mistral 系列 7B 模型，未在更大规模或不同架构的 LLM 上验证。
- **领域覆盖不足**：未涉及专业领域（如医学、法律）或极长链推理任务。
- **隐性推理不可解释**：隐式 token 无法直接解码为人类可读的推理过程，降低了可解释性。
- **潜在风险**：高效推理可能被恶意利用（如生成虚假信息、自动化攻击），且可能因追求速度而牺牲推理质量。

（完）
