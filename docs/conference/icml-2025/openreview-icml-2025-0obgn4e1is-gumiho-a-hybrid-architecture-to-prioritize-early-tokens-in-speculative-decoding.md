---
title: "Gumiho: A Hybrid Architecture to Prioritize Early Tokens in Speculative Decoding"
title_zh: Gumiho：一种优先处理早期token的推测解码混合架构
authors: "Jinze Li, Yixing Xu, Haiduo Huang, Xuanwu Yin, Dong Li, Edith C. H. Ngai, Emad Barsoum"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=0ObGn4e1IS"
tags: ["query:key-tokens"]
score: 6.0
evidence: 证明了草稿序列中早期token的重要性
tldr: 针对推测解码中所有token平等假设的问题，本文理论证明草稿序列中早期token更重要，并设计混合架构Gumiho优先处理早期token，提升解码效率。
source: ICML-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2025-0obgn4e1is/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1600, \"height\": 737, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-0obgn4e1is/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 861, \"height\": 365, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-0obgn4e1is/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 687, \"height\": 620, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-0obgn4e1is/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 684, \"height\": 515, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-0obgn4e1is/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 687, \"height\": 515, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-0obgn4e1is/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1410, \"height\": 1231, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-icml-2025-0obgn4e1is/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 855, \"height\": 281, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-0obgn4e1is/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1769, \"height\": 1224, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-0obgn4e1is/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 625, \"height\": 171, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-0obgn4e1is/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 616, \"height\": 362, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-0obgn4e1is/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1657, \"height\": 229, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-0obgn4e1is/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1771, \"height\": 830, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-0obgn4e1is/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1782, \"height\": 1181, \"label\": \"Table\"}]"
motivation: 现有推测解码假设所有token重要性相同，忽略早期token的关键性。
method: 理论证明早期token更重要，设计混合架构优先处理早期token。
result: 提出的Gumiho架构在加速解码的同时保持质量。
conclusion: token重要性差异可被利用来优化推测解码。
---

## Abstract
Speculative decoding (SPD) aims to accelerate the auto-regressive token generation process of a target Large Language Model (LLM). Some approaches employ a draft model with multiple heads to predict a sequence of future tokens, where each head handles a token in the sequence. The target LLM verifies the predicted sequence and accepts aligned tokens, enabling efficient multi-token generation. However, existing methods assume that all tokens within a sequence are equally important, employing identical head structures and relying on a single-generation paradigm, either serial or parallel. To this end, we theoretically demonstrate that initial tokens in the draft sequence are more important than later ones. Building on this insight, we propose Gumiho, a hybrid model combining serial and parallel heads. Specifically, given the critical importance of early tokens, we employ a sophisticated Transformer architecture for the early draft heads in a serial configuration to improve accuracy. For later tokens, we utilize multiple lightweight MLP heads operating in parallel to enhance efficiency. By allocating more advanced model structures and longer running times to the early heads, Gumiho achieves improved overall performance. The experimental results demonstrate that our method outperforms existing approaches, fully validating its effectiveness. Our code is available at https://github.com/AMD-AIG-AIMA/Gumiho.

---

## 论文详细总结（自动生成）

# 详细中文总结

## 论文的核心问题与整体含义

- **研究动机**：大型语言模型（LLM）的自回归生成过程存在显著延迟，推测解码（Speculative Decoding, SPD）通过使用草稿模型快速预测多个token，再由目标LLM并行验证，从而加速生成。现有方法（如Medusa、Eagle、Eagle-2）假设草稿序列中所有token重要性相同，采用统一的串行或并行结构，忽视了不同位置token对最终接受长度的影响差异。
- **核心问题**：如何在给定计算预算下，通过区分草稿序列中早期和后期token的重要性，设计更高效的混合架构，提升推测解码的整体加速比。
- **整体含义**：作者从理论上证明早期token比后期token更重要，并据此提出Gumiho混合架构，优先处理早期token（用更复杂的串行Transformer），后期token则用轻量并行MLP，在保持精度的同时提高效率。实验证明该方法在多种LLM和数据集上优于现有SOTA。

## 论文提出的方法论

- **核心思想**：基于“早期token更重要”的理论证明，将草稿模型分为两部分：
  - 早期token（论文设为前2个）：使用两层的串行Transformer，更精细地建模依赖关系，提高准确性。
  - 后期token（后5个）：使用多个轻量MLP并行预测，提高计算效率。
- **关键技术细节**：
  1. **混合头设计**：
     - 串行Transformer（$M_T$）接收来自目标LLM最后一个已验证token的隐藏状态$h_t$和对应token嵌入$e(y_t)$的拼接，经过全连接层降维，然后自回归生成前两个草稿token。
     - 并行MLP头（$M^i_M, i=1..5$）共享输入（前两个草稿token输出的拼接），各自独立预测后续5个位置的token。
  2. **完整树注意力（Full Tree Attention, FTA）**：在树候选路径选择中，允许从较长路径借用token来补充短路径，从而增加候选路径的平均长度，且不增加计算开销（借用token的QKV已计算过）。FTA确保每个候选路径的接受长度不短于原始实现。
  3. **损失函数**：结合回归损失$L_{reg}$和分类损失$L_{cls}$，权重分别为$w_{reg}=1$和$w_{cls}=0.1$，与Eagle-2一致。
- **公式/算法流程（文字说明）**：
  - 草稿生成步骤：
    1. 输入$o_t = FC(concat(e(y_t), h_t))$。
    2. 串行生成：$\hat{h}_{t+1}=M_T(o_t)$, $\hat{o}_{t+1}=FC(concat(e(\hat{y}_{t+1}), \hat{h}_{t+1}))$；同样得到$\hat{h}_{t+2}$。
    3. 并行生成：$\hat{h}_{t+2+i}=M^i_M(concat(\hat{o}_{t+1}, \hat{o}_{t+2})), i=1..5$。
    4. 通过softmax得到草稿token $\hat{y}_{t+i}$。
  - 验证阶段：目标LLM并行验证草稿序列，拒绝采样决定接受长度。
  - FTA：在树候选路径中，根据分数选择top-k路径，并用较长路径的token补充较短路径。

## 实验设计

- **使用的数据集/场景**：
  - MT-Bench（多轮对话）
  - HumanEval（代码生成）
  - GSM8K（数学推理）
  - Alpaca（通用指令跟随）
  - CNN/Daily Mail（文本摘要）
  - Natural Questions（问答）
- **Benchmark**：对比方法包括Medusa（并行MLP头）、Hydra（串行MLP头）、Eagle（串行单层Transformer）、Eagle-2（串行单层Transformer + 动态树候选）。温度设置包括0（贪心采样）和1（多样性采样）。
- **对比方法数量**：在上述6个数据集上，对不同大小和版本的LLM（Vicuna-7B/13B, Llama2-chat-7B/13B/70B, Llama3-instruct-8B/70B）进行了全面对比，并在温度0和1下分别实验。总共约包含了上百组对比实验（每个模型×每个方法×每个数据集×温度）。

## 资源与算力

- **训练**：使用8×AMD Instinct MI250 GPU训练草稿头，目标LLM固定不动。训练数据为ShareGPT数据集。训练10个epoch，学习率2e-4或1e-4（取决于模型），批量大小4。
- **推理**：使用单张MI250 GPU（70B模型需4张MI250）。另在附录B中补充了单张NVIDIA A100的结果，以体现可迁移性。
- **未明确说明**：文中未提供训练总时长、GPU内存占用等细节，但提到草稿模型相比Eagle/Medusa参数更多，训练时GPU内存消耗增加。

## 实验数量与充分性

- **充分性评价**：实验非常充分。涵盖了主流LLM家族（Vicuna, Llama2, Llama3）、不同参数量（7B~70B）、多样性的任务（对话、代码、数学、指令、摘要、问答），以及两种温度设置。此外还进行了细致的消融实验：
  1. 串行头深度（1层、2层、3层Transformer）
  2. 并行头宽度（不同MLP数量）
  3. 完整树注意力（有/无FTA）
  4. 草稿头各位置精度对比（附录D）
  5. 墙钟时间组件分析（表3）
- **客观公平性**：实验设置与Eagle-2保持一致，包括训练数据、损失函数、超参数选择、动态树候选等，确保了公平对比。同时汇报了加速比和平均接受token数（τ）两个指标。但论文未做统计显著性检验（如置信区间）。

## 论文的主要结论与发现

1. **理论证明**：草稿序列中早期token的准确性对整体接受长度贡献更大。通过重新分配各位置概率（提高早期、降低后期），可以提升平均接受token数。
2. **Gumiho的优势**：混合架构（串行Transformer早期+并行MLP后期）在速度和准确性之间取得更好平衡。相比Eagle-2，Gumiho在温度0下速度提升4.5%~15.8%，尤其在70B模型上提升显著（如LLaMA3 70B提升15.8%）。
3. **FTA有效性**：在不增加额外计算的情况下，通过借用长路径token提升候选路径长度，进一步提升了τ。
4. **消融结论**：串行头深度为2层最佳（更深增加延迟收益递减）；并行头数量为5最优（过多导致信息压缩过载）。
5. **局限性**：草稿模型参数更多，训练阶段GPU内存消耗增加。

## 优点

- **理论创新**：首次严格证明早期token的重要性，并基于此设计架构，而非仅凭直觉。
- **混合架构巧思**：将串行（高精度）和并行（高效率）自然结合，合理分配计算资源。
- **FTA机制简洁高效**：无需额外计算即可提升候选路径质量，是树注意力的巧妙扩展。
- **实验全面**：覆盖多种LLM、任务、温度设置，消融实验设计合理，验证了各组件的贡献。
- **开源代码**：提供GitHub代码，可复现。

## 不足与局限

- **训练阶段资源开销大**：草稿模型含两层Transformer+五个MLP，比Eagle的单层Transformer更重，虽然推理时效率高，但训练所需GPU内存和时长增加，可能限制资源受限场景的部署。
- **实验缺失某些维度**：未测试更大模型（如>70B或MoE架构）、未报告训练时间与显存具体数据、未做统计显著性检验（如标准差/置信区间）。未与其他非自草稿类方法（如独立草稿模型）对比，可能影响结论通用性。
- **FTA的适用范围**：FTA假设并行生成的token间可任意组合，这依赖于MLP头共享输入并独立生成。对于某些序列依赖性强的场景（如代码生成中的语法约束），这种自由组合可能产生不合法的候选，但论文未深入探讨。
- **超参数敏感性**：串行头深度、并行头数量、topk/s等关键超参数仅基于单点实验选择，未展示更大范围内的敏感性；不同目标LLM可能需要不同配置，论文仅提供一组固定超参数（附表示部分调整）。
- **应用限制**：方法属于自草稿类，需要为目标LLM定制训练草稿头，对于无法修改或访问隐藏状态的商用LLM（如GPT-4）不适用。

（完）
