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

`MultiHead(Q,K,V) = Concat(head_1, ..., head_h) W^O`.

`head_i = Attention(Q W_i^Q, K W_i^K, V W_i^V)`.

- In the original Transformer base model, the paper uses `h = 8` heads with `d_k = d_v = d_model / h = 64`, so reducing each head's dimensionality keeps the total cost similar to full-dimensional single-head attention.

## Historical development
[[2017 Attention Is All You Need]] introduces multi-head attention as a central Transformer component.

[[2019 Fast Transformer Decoding One Write-Head is All You Need]] proposes [[Multi-Query Attention]] as an inference-oriented variant that keeps multiple query heads while sharing keys and values across heads.

## Related papers
- [[2017 Attention Is All You Need]]
- [[2019 Fast Transformer Decoding One Write-Head is All You Need]]

## Related concepts
- [[Attention]]
- [[Self-Attention]]
- [[Scaled Dot-Product Attention]]
- [[Multi-Query Attention]]
- [[KV Cache]]
- [[Transformers]]

## Open questions
- Needs verification: later variants such as grouped-query attention and multi-head latent attention should be grounded in separate source notes.

## My understanding
Multi-head attention is not just repetition. Each head gets its own learned projections, so heads can specialize in different interaction patterns.

## Source notes
- [[2017 Attention Is All You Need]]
- [[2019 Fast Transformer Decoding One Write-Head is All You Need]]

## Revision notes
