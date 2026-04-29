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
- [[Grouped-Query Attention]] uses an intermediate number of key/value groups to trade off quality and KV-cache size.
- [[FlashAttention]] reduces memory traffic inside the exact attention computation itself.

## Historical development
[[2019 Fast Transformer Decoding One Write-Head is All You Need]] is an early source connecting Transformer attention architecture to incremental decoding speed through key/value memory bandwidth.

[[2023 GQA]] introduces grouped-query attention as a practical quality/speed compromise for efficient language model inference.

[[2022 FlashAttention]] makes exact attention more memory efficient, which is relevant for longer sequences and efficient Transformer training/inference.

## Related concepts
- [[Transformers]]
- [[Attention]]
- [[Multi-Head Attention]]
- [[Grouped-Query Attention]]
- [[Multi-Query Attention]]
- [[KV Cache]]
- [[FlashAttention]]
- [[Scaling Laws]]

## Related papers
- [[2019 Fast Transformer Decoding One Write-Head is All You Need]]
- [[2022 FlashAttention]]
- [[2023 GQA]]

## Open questions
- Which source should anchor decoder-only LLM architecture?
- Which source should anchor prefill/decode behavior in modern LLM serving?
