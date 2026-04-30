# DeepSeek-V2 Technical Report

## Metadata
- Authors: DeepSeek-AI
- Year: 2024
- Venue: technical report
- Link: https://arxiv.org/abs/2405.04434
- arXiv: 2405.04434
- Source type: paper
- Status: studied
- Reliability: high
- Added: 2026-04-29

## Scope
This ingest focuses on grounding mechanisms reused by [[2024 DeepSeek-V3 Technical Report]]: [[Multi-Head Latent Attention]], [[KV Cache]] reduction, low-rank key-value compression, cached latent representations, decoupled [[Rotary Position Embedding]], relationship to [[Multi-Head Attention]], limited comparison to [[Multi-Query Attention]] and [[Grouped-Query Attention]], and high-level [[DeepSeekMoE]] structure.

Excluded: full benchmark tables, full training data details, post-training/RL details, hardware/system implementation details, full derivation of every MLA equation, long-context/YaRN details except as future connection, DeepSeek-V3 changes, DeepSeek-R1 reasoning content, and political/economic discussion.

## One-sentence summary
DeepSeek-V2 introduces a sparse MoE language model using MLA to compress KV-cache state for efficient inference and DeepSeekMoE to scale feed-forward capacity economically.

## Why this paper matters
This is the better grounding source for [[Multi-Head Latent Attention]] than the DeepSeek-V3 report, because it directly motivates MLA against MHA/GQA/MQA and explains the low-rank KV compression and decoupled RoPE design.

It also clarifies which mechanisms in [[2024 DeepSeek-V3 Technical Report]] are inherited architecture choices rather than new V3-only ideas.

## Problem
Scaling dense LLMs increases training cost and can reduce inference throughput. Standard [[Multi-Head Attention]] also creates a large [[KV Cache]] during generation, limiting batch size and sequence length in deployment.

## Background needed
- [[Transformers]]
- [[Multi-Head Attention]]
- [[KV Cache]]
- [[Multi-Query Attention]]
- [[Grouped-Query Attention]]
- [[Rotary Position Embedding]]
- [[Mixture of Experts]]
- [[Expert Routing]]

## Core idea
DeepSeek-V2 combines two efficiency mechanisms inside a transformer: MLA compresses key/value attention state into a latent vector for inference, while DeepSeekMoE uses sparse expert feed-forward layers to increase total capacity with fewer activated parameters per token.

## Method
- MLA applies low-rank joint compression to keys and values.
- During inference, MLA caches the compressed KV latent rather than full per-head keys and values.
- Because RoPE is position-sensitive, the paper decouples RoPE into additional query/key components so key/value compression remains compatible with efficient inference.
- DeepSeekMoE uses fine-grained expert segmentation and shared expert isolation.
- The model uses routed experts plus shared experts in feed-forward layers.
- Device-limited routing and balance losses are introduced to control communication and load imbalance, but full training-system details are out of scope here.

## Important equations
See [[Multi-Head Latent Attention (Math)]] for the focused math note.

Standard MHA cache requirement from the source:

$2 n_h d_h l$ elements per token.

MLA low-rank KV compression:

$$
c_t^{KV} = W^{DKV} h_t
$$

$$
k_t^C = W^{UK} c_t^{KV}
$$

$$
v_t^C = W^{UV} c_t^{KV}
$$

With decoupled RoPE, the source states DeepSeek-V2 caches:

$(d_c + d_h^R) l$ elements per token.

High-level DeepSeekMoE output:

$$
h'_t = u_t + shared expert outputs + gated routed expert outputs
$$

Needs verification: full MLA equations and DeepSeekMoE balance losses should be expanded only in focused math notes.

## Results
- Claim from source: DeepSeek-V2 has 236B total parameters and 21B activated parameters per token.
- Claim from source: MLA significantly compresses the KV cache into a latent vector.
- Claim from source: DeepSeek-V2 reduces KV cache by 93.3% compared with DeepSeek 67B.
- Claim from source: MLA's KV cache is comparable to GQA with 2.25 groups under the paper's chosen dimensions, while the source reports stronger performance than MHA.
- Claim from source: DeepSeekMoE uses fine-grained expert segmentation and shared expert isolation.

## Limitations
- The paper reports many empirical comparisons, but this ingest only captures the mechanism-level claims.
- DeepSeekMoE is still partly inherited from the separate DeepSeekMoE source.
- The source's performance comparisons depend on the studied model/configuration.
- Long-context, training data, and alignment details were intentionally left out.

## Claim from source
- MHA's large KV cache is an inference-efficiency bottleneck.
- MQA and GQA reduce KV cache but the source says they do not match MHA performance in the paper's ablations.
- MLA uses low-rank key-value joint compression to reduce the KV cache.
- Decoupled RoPE is used because applying RoPE directly to compressed keys would interfere with the inference-time absorption of projection matrices.
- DeepSeekMoE uses fine-grained expert segmentation and shared expert isolation to improve expert specialization and reduce redundancy.

## My interpretation
DeepSeek-V2 is the key bridge between earlier efficient attention ideas and the DeepSeek-V3 architecture map. It reframes KV-cache reduction as an attention-parameterization problem rather than only a head-sharing problem like MQA or GQA.

## Unclear / Needs verification
- Needs verification: expand full MLA derivation from Appendix C if a math page is created.
- Needs verification: compare the paper's MHA/GQA/MQA ablations with later independent evaluations.
- Needs verification: ground DeepSeekMoE in its original paper before treating this as the full source.

## Connections to concepts
- [[Multi-Head Latent Attention]]
- [[KV Cache]]
- [[DeepSeekMoE]]
- [[Mixture of Experts]]
- [[Expert Routing]]
- [[Large Language Models]]
- [[Transformers]]
- [[Rotary Position Embedding]]

## Connections to papers
- [[2017 Attention Is All You Need]]
- [[2019 Fast Transformer Decoding One Write-Head is All You Need]]
- [[2023 GQA]]
- [[2024 DeepSeek-V3 Technical Report]]

## Questions
- Should MLA get a separate math note after Appendix C is studied carefully?
- Should DeepSeekMoE be grounded next from Dai et al. 2024 rather than this report?

## Follow-up reading
- DeepSeekMoE paper.
- Focused MLA derivation pass.
