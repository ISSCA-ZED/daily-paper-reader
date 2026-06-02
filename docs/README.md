<div class="dpr-home-notice-card">
  <h3 class="dpr-home-notice-title">🚀 Start Here</h3>
  <ul class="dpr-home-notice-list">
    <li><a href="#/tutorial/README">使用教程</a></li>
  </ul>
</div>

## 每次日报
- 最新运行日期：2026-06-02
- 运行时间：2026-06-02 21:49:26 UTC
- 运行状态：成功
- 本次总论文数：17
- 精读区：6
- 速读区：11

### 今日简报（AI）
今日推荐17篇论文，精读6篇，重点聚焦多模态推理与结构化剪枝。最值得关注的是精读高分论文《MuCRASP》（9.0分），以及速读中《GeneralThinker》《CIRF》《VisionPulse》三篇（均8.0分），分别涉及领域通用推理、链式思维标记化与动态视觉稀疏性。建议普通读者优先精读《MuCRASP》以了解多模态推理剪枝前沿，再选择性速读其余三篇扩展推理效率优化思路。
- 详情：[/202606/02/README](/202606/02/README)

### 精读区论文标签
1. [MuCRASP: Multimodal Chain-of-thought Reasoning aware Structured Pruning](/202606/02/2605.25842v1-mucrasp-multimodal-chain-of-thought-reasoning-aware-structured-pruning)  
   标签：评分：9.0/10、query:key-tokens
   evidence：识别出pivot token是链式推理的关键
2. [MuCRASP: Multimodal Chain-of-thought Reasoning aware Structured Pruning](/202606/02/2605.25842v2-mucrasp-multimodal-chain-of-thought-reasoning-aware-structured-pruning)  
   标签：评分：9.0/10、query:key-tokens
   evidence：推理中关键token的重要性；识别对CoT关键的枢轴token
3. [Revealing Algorithmic Deductive Circuits for Logical Reasoning](/202606/02/2605.27824v1-revealing-algorithmic-deductive-circuits-for-logical-reasoning)  
   标签：评分：9.0/10、query:key-tokens
   evidence：定位负责推理步骤的注意力头并追踪token级电路
4. [Integrated and Cross-Architecture Interpretation of LLM Reasoning](/202606/02/2605.28006v1-integrated-and-cross-architecture-interpretation-of-llm-reasoning)  
   标签：评分：9.0/10、query:key-tokens
   evidence：通过隐藏状态分析隔离推理关键token
5. [Unlocking the Black Box of Latent Reasoning: An Interpretability-Guided Approach to Intervention](/202606/02/2606.01243v1-unlocking-the-black-box-of-latent-reasoning-an-interpretability-guided-approach-to-intervention)  
   标签：评分：9.0/10、query:key-tokens
   evidence：推理中关键token的隐藏状态分析
6. [Detecting Unfaithful Chain-of-Thought via Circuit-Guided Internal-External Discrepancy](/202606/02/2605.25603v1-detecting-unfaithful-chain-of-thought-via-circuit-guided-internal-external-discrepancy)  
   标签：评分：8.0/10、query:key-tokens
   evidence：推理token的因果追踪；使用电路引导的内外不一致性

### 速读区论文标签
1. [GeneralThinker: Domain-General Reasoning through Likelihood-Guided Answer-Conditioned Optimization](/202606/02/2605.27934v1-generalthinker-domain-general-reasoning-through-likelihood-guided-answer-conditioned-optimization)  
   标签：评分：8.0/10、query:key-tokens
   evidence：引入基于答案条件似然的令牌级信用分配
2. [CIRF: Tokenizing Chain-of-Thoughts into Reusable Functional Units for Efficient Latent Reasoning in Large Language Models](/202606/02/2605.28292v1-cirf-tokenizing-chain-of-thoughts-into-reusable-functional-units-for-efficient-latent-reasoning-in-large-language-models)  
   标签：评分：8.0/10、query:key-tokens
   evidence：将思维链分词化为可重用的功能单元，直接用离散功能token建模推理序列
3. [VisionPulse: Dynamic Visual Sparsity for Efficient Multimodal Reasoning](/202606/02/2605.31457v1-visionpulse-dynamic-visual-sparsity-for-efficient-multimodal-reasoning)  
   标签：评分：8.0/10、query:key-tokens
   evidence：在多模态推理中基于关键程度逐步动态剪枝视觉token
4. [CausalFlow: Causal Attribution and Counterfactual Repair for LLM Agent Failures](/202606/02/2605.25338v1-causalflow-causal-attribution-and-counterfactual-repair-for-llm-agent-failures)  
   标签：评分：7.0/10、query:key-tokens
   evidence：通过步骤级反事实干预计算因果责任分数，识别故障步骤，方法论上等价于推理token的因果追踪
5. [IndexMem: Learned KV-Cache Eviction with Latent Memory for Long-Context LLM Inference](/202606/02/2605.25475v1-indexmem-learned-kv-cache-eviction-with-latent-memory-for-long-context-llm-inference)  
   标签：评分：7.0/10、query:key-tokens
   evidence：使用可学习索引器预测KV重要性以保留token，直接为transformer推理开发token重要性度量
6. [Selective Latent Thinking: Adaptive Compression of LLM Reasoning Chains](/202606/02/2605.25745v1-selective-latent-thinking-adaptive-compression-of-llm-reasoning-chains)  
   标签：评分：7.0/10、query:key-tokens
   evidence：token重要性度量；选择性压缩冗余跨度保留精度关键token
7. [Reasoning-preserved Efficient Distillation of Large Language Models via Activation-aware Initialization](/202606/02/2605.29327v1-reasoning-preserved-efficient-distillation-of-large-language-models-via-activation-aware-initialization)  
   标签：评分：7.0/10、query:key-tokens
   evidence：分析隐藏表示秩塌缩导致多步推理退化
8. [Unlocking the Working Memory of Large Language Models for Latent Reasoning](/202606/02/2605.30343v1-unlocking-the-working-memory-of-large-language-models-for-latent-reasoning)  
   标签：评分：7.0/10、query:key-tokens
   evidence：使用记忆块（特殊token序列）替代自回归推理步骤，直接处理语言模型中的推理序列
9. [ROSD: Reflective On-Policy Self-Distillation for Language Model Reasoning across Domains](/202606/02/2605.28014v1-rosd-reflective-on-policy-self-distillation-for-language-model-reasoning-across-domains)  
   标签：评分：6.0/10、query:key-tokens
   evidence：提供密集令牌级监督以进行定向推理纠正
10. [Reasoning that Travels: Dissecting How Chain-of-Thought Transfers Across Models](/202606/02/2605.28913v1-reasoning-that-travels-dissecting-how-chain-of-thought-transfers-across-models)  
   标签：评分：6.0/10、query:key-tokens
   evidence：剖析思维链推理序列如何跨模型传递
11. [Rethinking Stepwise Model Routing: A Cost-Efficient Table Reasoning Perspective](/202606/02/2605.29319v1-rethinking-stepwise-model-routing-a-cost-efficient-table-reasoning-perspective)  
   标签：评分：6.0/10、query:key-tokens
   evidence：区分表格令牌和文本令牌的不确定性度量用于路由决策


<div class="dpr-home-promo-card">
  <h3 class="dpr-home-promo-title">💬 社区与支持</h3>
  <ul class="dpr-home-promo-list">
    <li>欢迎 Star / Fork / Issue / PR</li>
    <li>QQ群：583867967（欢迎交流，已有：1151人）</li>
  </ul>
</div>
