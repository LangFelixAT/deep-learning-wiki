# Multi-Query Attention

## Metadata
- Type: concept
- Status: developing
- Last reviewed: 2026-04-29

## Short definition
Multi-query attention is an attention variant with multiple query heads but a shared set of key and value heads.

## Intuition
Standard [[Multi-Head Attention]] gives each head separate queries, keys, and values. Multi-query attention keeps separate query heads, so the model can still form different query-dependent attention patterns, but it shares the stored keys and values across heads.

This matters most during autoregressive decoding, where previous keys and values are read repeatedly from the [[KV Cache]].

The "one write-head" phrase in the source is about writing one shared key/value set, not about collapsing all attention queries into one head.

## Mathematical formulation
- Related math: [[Scaled Dot-Product Attention]]
- Source: [[2019 Fast Transformer Decoding One Write-Head is All You Need]]
- Standard multi-head attention stores keys and values with a head dimension, such as $[batch, heads, sequence, dim]$.
- Multi-query attention removes the head dimension from keys and values, using shapes like $[batch, sequence, dim]$.
- Query projections remain head-specific.
- In the source's incremental decoding analysis, this reduces the key/value memory-access term by a factor of the number of heads.

## Historical development
[[2019 Fast Transformer Decoding One Write-Head is All You Need]] introduces multi-query attention to reduce memory-bandwidth requirements during incremental Transformer decoding.

[[2023 GQA]] frames MQA as the $G = 1$ endpoint of [[Grouped-Query Attention]].

## Related papers
- [[2019 Fast Transformer Decoding One Write-Head is All You Need]]
- [[2023 GQA]]
- [[2017 Attention Is All You Need]]

## Related concepts
- [[Attention]]
- [[Self-Attention]]
- [[Multi-Head Attention]]
- [[Grouped-Query Attention]]
- [[KV Cache]]
- [[Transformers]]
- [[Large Language Models]]

## Open questions
- Needs verification: quality tradeoffs in modern decoder-only LLMs should be grounded in model-specific papers.

## My understanding
Multi-query attention is a deliberate asymmetry: keep many query heads for expressivity, but use fewer key/value heads to reduce the amount of memory that must be stored and reread during decoding.

## Source notes
- [[2019 Fast Transformer Decoding One Write-Head is All You Need]]
- [[2023 GQA]]

## Revision notes
