# DeepSeek-V3 Technical Report

## Metadata
- Authors: DeepSeek-AI
- Year: 2024 preprint; 2025 arXiv version read
- Venue: technical report
- Link: https://arxiv.org/abs/2412.19437
- arXiv: 2412.19437
- Source type: paper
- Status: studied
- Reliability: high
- Added: 2026-04-29

## Scope
This ingest treats DeepSeek-V3 as a high-level architecture map for modern efficient LLM design.

Covered: sparse MoE language modeling, total versus activated parameters, relation to [[Mixture of Experts]] and [[Expert Routing]], high-level DeepSeekMoE, high-level [[Multi-Head Latent Attention]] as KV-cache compression, auxiliary-loss-free load balancing, multi-token prediction, FP8/systems co-design as brief context, and connections among MoE, attention efficiency, and LLM scaling.

Excluded: benchmark tables in detail, full training data details, post-training and reinforcement learning details, DualPipe implementation details, hardware kernels, full FP8 recipe, full MLA derivation, full DeepSeekMoE derivation, long-context techniques such as YaRN, DeepSeek-R1 reasoning content, and later DeepSeek versions.

## One-sentence summary
DeepSeek-V3 is a large sparse MoE language model that combines DeepSeekMoE, MLA-based KV-cache reduction, auxiliary-loss-free load balancing, multi-token prediction, and systems co-design to scale model capability efficiently.

## Why this paper matters
The report is useful as a map of several modern LLM design pressures at once: sparse activation, inference memory, expert routing, low-precision training, and architecture-system co-design.

After the supporting notes are grounded, this paper should be read as a hub: [[Multi-Head Latent Attention]] is primarily grounded by [[2024 DeepSeek-V2 Technical Report]], and [[DeepSeekMoE]] is primarily grounded by [[2024 DeepSeekMoE]].

## Problem
Modern LLMs need more capacity and stronger performance, but dense scaling increases computation, memory, and serving cost. DeepSeek-V3 addresses this by combining sparse MoE capacity with attention and training-system efficiency.

## Background needed
- [[Large Language Models]]
- [[Transformers]]
- [[Mixture of Experts]]
- [[Expert Routing]]
- [[KV Cache]]
- [[Multi-Head Attention]]
- [[Grouped-Query Attention]]
- [[Multi-Query Attention]]
- [[Rotary Position Embedding]]

## Core idea
DeepSeek-V3 uses a transformer-based sparse MoE architecture with 671B total parameters and 37B activated per token. The model uses MLA to reduce KV-cache cost during inference and DeepSeekMoE to scale feed-forward capacity economically.

## Inherited architecture
- From [[2024 DeepSeek-V2 Technical Report]]: [[Multi-Head Latent Attention]] for efficient inference and reduced KV-cache cost.
- From [[2024 DeepSeekMoE]]: fine-grained routed experts and shared expert isolation inside MoE feed-forward layers.
- From the broader transformer line: attention layers, feed-forward layers, normalization, and residual blocks.

## V3-specific additions
- Auxiliary-loss-free load balancing for DeepSeekMoE, using expert-specific routing biases adjusted from observed expert load.
- A complementary sequence-wise auxiliary loss with a small weight to avoid extreme imbalance within a sequence.
- Multi-token prediction as an additional training objective.
- FP8 mixed-precision training and training-system co-design as efficiency mechanisms.
- Larger sparse scale: 671B total parameters and 37B activated parameters per token.

## Method
- Uses [[Multi-Head Latent Attention]] for efficient inference by compressing keys and values into a latent representation.
- Uses DeepSeekMoE for feed-forward layers, with shared experts and routed experts.
- Uses auxiliary-loss-free load balancing by adjusting expert-specific routing biases.
- Uses a small complementary sequence-wise balance loss to prevent extreme imbalance within a sequence.
- Uses multi-token prediction as an additional training objective.
- Uses FP8 mixed precision and training-system optimizations as part of a broader algorithm/framework/hardware co-design.

## Important equations
The full MLA and DeepSeekMoE derivations are out of scope for this map ingest. See [[Multi-Head Latent Attention (Math)]] and [[DeepSeekMoE]] for grounded supporting notes.

High-level MLA compression:

$$
c_t^{KV} = W^{DKV} h_t
$$

The source states that only the compressed KV latent and a decoupled RoPE key need to be cached during generation.

High-level DeepSeekMoE output structure:

$$
h'_t = u_t + shared expert outputs + gated routed expert outputs
$$

The routed experts are selected by top-k affinity scores, while shared experts are always included.

Auxiliary-loss-free load balancing:

$$
s_{i,t} + b_i \quad \text{for top-k routing decisions; gate value uses } s_{i,t}
$$
The source states that expert bias terms are adjusted during training according to whether an expert is overloaded or underloaded.

## Results
- Claim from source: DeepSeek-V3 has 671B total parameters with 37B activated for each token.
- Claim from source: DeepSeek-V3 adopts MLA and DeepSeekMoE architectures validated in DeepSeek-V2.
- Claim from source: The report introduces an auxiliary-loss-free load balancing strategy for DeepSeekMoE.
- Claim from source: The model uses a multi-token prediction objective that the authors report as beneficial to performance.
- Claim from source: The report validates FP8 mixed-precision training on an extremely large-scale model.
- Claim from source: DeepSeek-V3 does not drop tokens during training or inference.

## Limitations
- This report is broad and contains many mechanisms that require focused follow-up notes.
- MLA and DeepSeekMoE are inherited from earlier DeepSeek sources, so this note should not be treated as the full origin of those mechanisms.
- Auxiliary-loss-free load balancing is only summarized here and should get a focused math/source pass if it becomes central.
- Many claims are tied to the authors' implementation and hardware stack.
- Benchmark and post-training claims were intentionally not ingested in detail.

## Claim from source
- DeepSeek-V3 is a Mixture-of-Experts model.
- It uses 671B total parameters and activates 37B parameters per token.
- MLA is used for efficient inference.
- DeepSeekMoE is used for cost-effective training.
- Auxiliary-loss-free load balancing aims to reduce the performance degradation associated with auxiliary load-balancing losses.
- Multi-token prediction is used as an additional training objective.
- The MTP modules can be discarded for ordinary inference according to the source.

## My interpretation
DeepSeek-V3 is best understood as a co-design paper: architecture choices, routing choices, precision choices, and distributed training choices are presented as mutually reinforcing parts of one system.

For the wiki, the report should act as a hub. The detailed math of MLA, DeepSeekMoE, FP8 training, and multi-token prediction should be strengthened through separate focused passes.

## Unclear / Needs verification
- Needs verification: full MLA derivation and exact relationship to MHA/MQA/GQA.
- Needs verification: auxiliary-loss-free load balancing should get a separate math note after focused reading.
- Needs verification: FP8 training details should be grounded in a training-systems or numerical-precision source.
- Needs verification: multi-token prediction should be grounded in a separate source if it becomes a major training-objective concept.

## Connections to concepts
- [[Large Language Models]]
- [[Transformers]]
- [[Mixture of Experts]]
- [[Expert Routing]]
- [[Multi-Head Latent Attention]]
- [[Multi-Head Latent Attention (Math)]]
- [[KV Cache]]
- [[DeepSeekMoE]]
- [[LLM Training Systems]]
- [[Rotary Position Embedding]]

## Connections to papers
- [[2017 Attention Is All You Need]]
- [[2021 Switch Transformers]]
- [[2024 DeepSeekMoE]]
- [[2024 DeepSeek-V2 Technical Report]]
- [[2019 Fast Transformer Decoding One Write-Head is All You Need]]
- [[2023 GQA]]

## Questions
- Should multi-token prediction become a math page or a training-objective concept page?
- Should auxiliary-loss-free load balancing become a dedicated math note?

## Follow-up reading
- [[2024 DeepSeek-V2 Technical Report]] for MLA context.
- [[2024 DeepSeekMoE]] for DeepSeekMoE expert structure.
- FP8 training sources for numerical training details.
