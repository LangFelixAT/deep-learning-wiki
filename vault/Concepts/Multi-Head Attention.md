# Multi-Head Attention

## Metadata
- Type: concept
- Status: developing
- Last reviewed: 2026-04-29

## Short definition
Multi-head attention runs several attention heads in parallel over learned projections of queries, keys, and values.

## Intuition
A single attention head produces one weighted combination of values. Multiple heads let the model attend through different representation subspaces and positions at the same time.

## Mathematical formulation
- Related math: [[Scaled Dot-Product Attention]]
- In [[2017 Attention Is All You Need]]:

$$
\operatorname{MultiHead}(Q,K,V) = \operatorname{Concat}(head_1, ..., head_h) W^O
$$
$$
head_i = \operatorname{Attention}(Q W_i^Q, K W_i^K, V W_i^V)
$$
- In the original Transformer base model, the paper uses $h = 8$ heads with $d_k = d_v = d_model / h = 64$, so reducing each head's dimensionality keeps the total cost similar to full-dimensional single-head attention.

## Historical development
[[2017 Attention Is All You Need]] introduces multi-head attention as a central Transformer component.

[[2019 Fast Transformer Decoding One Write-Head is All You Need]] proposes [[Multi-Query Attention]] as an inference-oriented variant that keeps multiple query heads while sharing keys and values across heads.

[[2023 GQA]] introduces [[Grouped-Query Attention]] as an intermediate point between full multi-head attention and multi-query attention.

[[2024 DeepSeek-V2 Technical Report]] introduces [[Multi-Head Latent Attention]] as another efficient-attention variant, using latent key/value compression rather than only key/value head sharing.

## Related papers
- [[2017 Attention Is All You Need]]
- [[2019 Fast Transformer Decoding One Write-Head is All You Need]]
- [[2022 FlashAttention]]
- [[2023 GQA]]

## Related concepts
- [[Attention]]
- [[Self-Attention]]
- [[Scaled Dot-Product Attention]]
- [[Notation Conventions]]
- [[Grouped-Query Attention]]
- [[Multi-Query Attention]]
- [[Multi-Head Latent Attention]]
- [[KV Cache]]
- [[FlashAttention]]
- [[Transformers]]
- [[Efficient LLM Architecture]]

## Open questions
- Needs verification: compare MHA, MQA, GQA, and MLA across independent sources rather than only their introducing papers.

## My understanding
Multi-head attention is not just repetition. Each head gets its own learned projections, so heads can specialize in different interaction patterns.

## Source notes
- [[2017 Attention Is All You Need]]
- [[2019 Fast Transformer Decoding One Write-Head is All You Need]]
- [[2023 GQA]]

## Revision notes
