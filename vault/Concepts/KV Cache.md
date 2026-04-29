# KV Cache

## Metadata
- Type: concept
- Status: developing
- Last reviewed: 2026-04-29

## Short definition
The KV cache stores previously computed attention keys and values so autoregressive decoding can reuse them at later token positions.

## Intuition
During autoregressive generation, a Transformer produces one token at a time. For each new token, the model must attend back to earlier positions. Recomputing all previous keys and values would be wasteful, so inference systems store them in a cache.

The cache speeds computation but creates a memory problem: every decoding step reads cached keys and values from prior positions.

## Mathematical formulation
- Related math: [[Scaled Dot-Product Attention]]
- In standard multi-head attention, cached keys and values have a head dimension, such as `[batch, heads, sequence, dim]`.
- In [[Multi-Query Attention]], cached keys and values share across query heads, reducing the cache shape to something like `[batch, sequence, dim]`.
- Exact tensor layout is implementation-dependent.

## Historical development
[[2019 Fast Transformer Decoding One Write-Head is All You Need]] frames key/value memory bandwidth as a central bottleneck for incremental Transformer decoding and proposes [[Multi-Query Attention]] to reduce cache size and reads.

## Related papers
- [[2019 Fast Transformer Decoding One Write-Head is All You Need]]

## Related concepts
- [[Attention]]
- [[Self-Attention]]
- [[Multi-Head Attention]]
- [[Multi-Query Attention]]
- [[Transformers]]
- [[Large Language Models]]

## Open questions
- Needs verification: add paged attention and modern KV-cache management from serving-system sources.
- Needs verification: separate prefill versus decode behavior should be grounded in a later inference-systems source.

## My understanding
The KV cache is where attention architecture becomes a systems issue. The model has already computed useful state, but serving speed depends heavily on how much of that state must be moved through memory each token.

## Source notes
- [[2019 Fast Transformer Decoding One Write-Head is All You Need]]

## Revision notes
