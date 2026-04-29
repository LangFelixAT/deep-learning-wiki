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

## Method
- Uses [[Multi-Head Latent Attention]] for efficient inference by compressing keys and values into a latent representation.
- Uses DeepSeekMoE for feed-forward layers, with shared experts and routed experts.
- Uses auxiliary-loss-free load balancing by adjusting expert-specific routing biases.
- Uses a small complementary sequence-wise balance loss to prevent extreme imbalance within a sequence.
- Uses multi-token prediction as an additional training objective.
- Uses FP8 mixed precision and training-system optimizations as part of a broader algorithm/framework/hardware co-design.

## Important equations
The full MLA and DeepSeekMoE derivations are out of scope for this map ingest.

High-level MLA compression:

`c_t^{KV} = W^{DKV} h_t`

The source states that only the compressed KV latent and a decoupled RoPE key need to be cached during generation.

High-level DeepSeekMoE output structure:

`h'_t = u_t + shared expert outputs + gated routed expert outputs`

The routed experts are selected by top-k affinity scores, while shared experts are always included.

## Results
- Claim from source: DeepSeek-V3 has 671B total parameters with 37B activated for each token.
- Claim from source: DeepSeek-V3 adopts MLA and DeepSeekMoE architectures validated in DeepSeek-V2.
- Claim from source: The report introduces an auxiliary-loss-free load balancing strategy for DeepSeekMoE.
- Claim from source: The model uses a multi-token prediction objective that the authors report as beneficial to performance.
- Claim from source: The report validates FP8 mixed-precision training on an extremely large-scale model.

## Limitations
- This report is broad and contains many mechanisms that require focused follow-up notes.
- MLA and DeepSeekMoE are inherited from earlier DeepSeek sources, so this note should not be treated as the full origin of those mechanisms.
- Many claims are tied to the authors' implementation and hardware stack.
- Benchmark and post-training claims were intentionally not ingested in detail.

## Claim from source
- DeepSeek-V3 is a Mixture-of-Experts model.
- It uses 671B total parameters and activates 37B parameters per token.
- MLA is used for efficient inference.
- DeepSeekMoE is used for cost-effective training.
- Auxiliary-loss-free load balancing aims to reduce the performance degradation associated with auxiliary load-balancing losses.
- Multi-token prediction is used as an additional training objective.

## My interpretation
DeepSeek-V3 is best understood as a co-design paper: architecture choices, routing choices, precision choices, and distributed training choices are presented as mutually reinforcing parts of one system.

For the wiki, the report should act as a hub. The detailed math of MLA, DeepSeekMoE, FP8 training, and multi-token prediction should be strengthened through separate focused passes.

## Unclear / Needs verification
- Needs verification: full MLA derivation and exact relationship to MHA/MQA/GQA.
- Needs verification: DeepSeekMoE details should be compared against the original DeepSeekMoE source.
- Needs verification: auxiliary-loss-free load balancing should get a separate math note after focused reading.
- Needs verification: FP8 training details should be grounded in a training-systems or numerical-precision source.

## Connections to concepts
- [[Large Language Models]]
- [[Transformers]]
- [[Mixture of Experts]]
- [[Expert Routing]]
- [[Multi-Head Latent Attention]]
- [[KV Cache]]
- [[LLM Training Systems]]
- [[Rotary Position Embedding]]

## Connections to papers
- [[2017 Attention Is All You Need]]
- [[2021 Switch Transformers]]
- [[2019 Fast Transformer Decoding One Write-Head is All You Need]]
- [[2023 GQA]]

## Questions
- Which source should anchor MLA in detail?
- Which source should anchor DeepSeekMoE in detail?
- Should multi-token prediction become a math page or a training-objective concept page?

## Follow-up reading
- DeepSeek-V2 for MLA and DeepSeekMoE context.
- DeepSeekMoE paper for expert routing details.
- FP8 training sources for numerical training details.
