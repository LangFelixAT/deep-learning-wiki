# Self-Attention

## Metadata
- Type: concept
- Status: developing

## Short definition
Attention applied among elements of the same sequence or set.

## Intuition
In self-attention, each token forms attention weights over tokens from the same sequence. This lets a token representation incorporate information from other positions directly.

## Mathematical formulation
- Related math: [[Scaled Dot-Product Attention]]
- In encoder self-attention, queries, keys, and values all come from the previous layer of the same sequence.
- In decoder self-attention, masking prevents a position from attending to future positions.

## Historical development
[[2017 Attention Is All You Need]] uses stacked self-attention layers as the main replacement for recurrent sequence computation.

[[2019 Fast Transformer Decoding One Write-Head is All You Need]] focuses on incremental self-attention during autoregressive decoding, where cached keys and values are repeatedly read.

[[2023 GQA]] introduces grouped key/value sharing for decoder attention as a quality/speed compromise between MHA and MQA.

## Related papers
- [[2017 Attention Is All You Need]]
- [[2019 Fast Transformer Decoding One Write-Head is All You Need]]
- [[2023 GQA]]

## Related concepts
- [[Attention]]
- [[Transformers]]
- [[Multi-Head Attention]]
- [[Grouped-Query Attention]]
- [[Multi-Query Attention]]
- [[KV Cache]]
- [[Positional Encoding]]

## Open questions
- Needs verification: add earlier self-attention uses cited by the Transformer paper.

## Source notes
- [[2017 Attention Is All You Need]]
- [[2019 Fast Transformer Decoding One Write-Head is All You Need]]
- [[2023 GQA]]
