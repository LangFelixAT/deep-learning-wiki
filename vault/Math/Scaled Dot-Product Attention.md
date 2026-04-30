# Scaled Dot-Product Attention

## Metadata
- Type: math
- Status: partially verified
- Last reviewed: 2026-04-29

## Goal
Define the attention operation used as the core computation in the original Transformer.

## Canonical notation
- $Q$: query matrix
- $K$: key matrix
- $V$: value matrix
- $d_k$: key/query dimensionality
- See [[Notation Conventions]] for cross-page attention notation.

## Definitions
- Source: [[2017 Attention Is All You Need]].
- An attention function maps queries and key-value pairs to outputs.
- The output is a weighted sum of values.
- The weights are computed from query-key compatibility scores.

## Assumptions
- Queries and keys have dimension $d_k$.
- Values have dimension $d_v$.
- The attention operation is applied to matrices of queries, keys, and values.

## Main result
$$
\operatorname{Attention}(Q,K,V) = \operatorname{softmax}\left(\frac{QK^T}{\sqrt{d_k}}\right) V
$$
## Derivation
- Compute dot-product scores between queries and keys: $QK^T$.
- Scale the scores by $\frac{1}{\sqrt{d_k}}$.
- Apply softmax row-wise to obtain attention weights.
- Multiply the attention weights by $V$ to produce weighted sums of values.
- Skipped steps: gradient analysis of the softmax saturation issue.

## Interpretation
The query-key dot product measures compatibility. The softmax turns compatibilities into weights over values. The scaling factor reduces the magnitude of dot products when $d_k$ is large.

[[2021 RoFormer]] modifies query and key representations with rotary position embeddings before this dot product, so the compatibility score can depend on relative position.

[[2019 Fast Transformer Decoding One Write-Head is All You Need]] keeps the same dot-product attention operation but changes how keys and values are shared across heads in [[Multi-Query Attention]]. This mainly affects the stored key/value tensors used during decoding, not the basic $\operatorname{softmax}\left(\frac{QK^T}{\sqrt{d_k}}\right) V$ operation.

[[2023 GQA]] likewise keeps the same attention operation while choosing an intermediate number of shared key/value groups.

[[2022 FlashAttention]] also computes the same attention function, but changes the memory schedule: it avoids materializing the full $QK^T$ and $\operatorname{softmax}(QK^T)$ matrices in slow memory.

[[Multi-Head Latent Attention]] changes the query/key/value parameterization and cache representation while still using scaled dot-product compatibility inside each attention head.

## Alternative formulations
- Additive attention uses a feed-forward network for compatibility scoring.
- Unscaled dot-product attention omits the $\frac{1}{\sqrt{d_k}}$ factor.
- [[FlashAttention]] is not an approximation to scaled dot-product attention; it is an exact IO-aware implementation strategy.

## Common mistakes
- Forgetting that $Q$, $K$, and $V$ are learned projections, not necessarily raw token embeddings.
- Treating attention weights as explanations without checking the model and task context.
- Omitting the scaling factor when describing the original Transformer.
- Assuming [[FlashAttention]] changes the attention function or turns exact attention into a linear-time attention method.

## Related concepts
- [[Attention]]
- [[Self-Attention]]
- [[Multi-Head Attention]]
- [[Grouped-Query Attention]]
- [[Multi-Query Attention]]
- [[KV Cache]]
- [[FlashAttention]]
- [[Multi-Head Latent Attention]]
- [[Rotary Position Embedding]]
- [[Transformers]]

## Related papers
- [[2017 Attention Is All You Need]]
- [[2019 Fast Transformer Decoding One Write-Head is All You Need]]
- [[2022 FlashAttention]]
- [[2023 GQA]]
- [[2024 DeepSeek-V2 Technical Report]]
- [[2021 RoFormer]]

## Source references
- [[2017 Attention Is All You Need]]
- [[2019 Fast Transformer Decoding One Write-Head is All You Need]]
- [[2022 FlashAttention]]
- [[2023 GQA]]
- [[2024 DeepSeek-V2 Technical Report]]

## Verification status
- Status: partially verified
- Needs verification: deeper variance/gradient explanation for why scaling stabilizes softmax should be checked against a math source.
