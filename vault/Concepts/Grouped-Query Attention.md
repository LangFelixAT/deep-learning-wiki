# Grouped-Query Attention

## Metadata
- Type: concept
- Status: developing
- Last reviewed: 2026-04-29

## Short definition
Grouped-query attention shares each key/value head across a group of query heads, placing it between [[Multi-Head Attention]] and [[Multi-Query Attention]].

## Intuition
[[Multi-Head Attention]] gives every query head its own key and value head. [[Multi-Query Attention]] shares one key/value head across all query heads.

Grouped-query attention chooses a middle point: query heads are split into groups, and each group shares one key head and one value head. This keeps more key/value capacity than MQA while reducing the [[KV Cache]] compared with MHA.

## Mathematical formulation
- Related math: [[Scaled Dot-Product Attention]]
- Source: [[2023 GQA]]
- Let `H` be the number of query heads.
- Let `G` be the number of key/value groups.
- The paper writes `GQA-G` for grouped-query attention with `G` groups.
- `G = 1` gives MQA.
- `G = H` gives MHA.
- Intermediate `G` values share each key/value head across a group of query heads.

Relative to MHA, GQA stores `G` key/value heads instead of `H`, reducing the key/value cache head dimension by roughly `H / G`.

In [[2023 GQA]], the method is applied to decoder attention in an encoder-decoder model, not encoder self-attention.

## Historical development
[[2019 Fast Transformer Decoding One Write-Head is All You Need]] introduces MQA as a way to reduce key/value memory bandwidth during incremental decoding.

[[2023 GQA]] introduces GQA as a generalization of MQA and shows a high-level recipe for converting MHA checkpoints into MQA/GQA models through grouped key/value head pooling and uptraining.

## Related papers
- [[2023 GQA]]
- [[2019 Fast Transformer Decoding One Write-Head is All You Need]]
- [[2017 Attention Is All You Need]]

## Related concepts
- [[Attention]]
- [[Self-Attention]]
- [[Multi-Head Attention]]
- [[Multi-Query Attention]]
- [[KV Cache]]
- [[Transformers]]
- [[Large Language Models]]

## Open questions
- Needs verification: document decoder-only LLM adoption from later model papers.
- Needs verification: separate GQA from later attention variants such as MLA using their own sources.

## My understanding
GQA is the practical compromise between preserving many independent key/value heads and aggressively minimizing KV-cache memory. It makes the number of key/value heads an explicit efficiency-quality tradeoff.

## Source notes
- [[2023 GQA]]

## Revision notes
