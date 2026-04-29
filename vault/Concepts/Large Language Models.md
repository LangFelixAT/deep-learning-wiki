# Large Language Models

## Metadata
- Type: concept
- Status: developing

## Short definition
Large neural language models trained on broad text distributions.

## Intuition
Large language models often generate text autoregressively, one token at a time. This makes decoding behavior and memory movement important parts of practical model performance.

## Mathematical formulation
- Related math: [[Transformers]]
- Autoregressive decoding repeatedly applies Transformer layers to a growing context.
- Cached keys and values from previous positions are reused through the [[KV Cache]].
- [[Multi-Query Attention]] reduces the number of key/value heads that must be stored and read during decoding.

## Historical development
[[2019 Fast Transformer Decoding One Write-Head is All You Need]] is an early source connecting Transformer attention architecture to incremental decoding speed through key/value memory bandwidth.

## Related concepts
- [[Transformers]]
- [[Attention]]
- [[Multi-Head Attention]]
- [[Multi-Query Attention]]
- [[KV Cache]]
- [[Scaling Laws]]

## Related papers
- [[2019 Fast Transformer Decoding One Write-Head is All You Need]]

## Open questions
- Which source should anchor decoder-only LLM architecture?
- Which source should anchor prefill/decode behavior in modern LLM serving?
