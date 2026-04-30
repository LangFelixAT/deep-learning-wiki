# Attention

## Metadata
- Type: concept
- Status: developing

## Short definition
Mechanism for weighting information by relevance.

## Intuition
Attention maps a query and a set of key-value pairs to an output. The output is a weighted sum of values, where weights come from how compatible the query is with each key.

## Mathematical formulation
- Related math: [[Scaled Dot-Product Attention]], [[Notation Conventions]]
- In [[2017 Attention Is All You Need]], attention uses queries `Q`, keys `K`, and values `V`.
- The attention weights are produced by applying softmax to query-key compatibility scores.

## Historical development
[[2017 Attention Is All You Need]] uses attention as the central sequence operation inside the Transformer architecture.

[[2019 Fast Transformer Decoding One Write-Head is All You Need]] shows that attention design also affects incremental decoding performance through key/value memory bandwidth.

[[2023 GQA]] adds [[Grouped-Query Attention]] as a middle point between MHA and MQA for key/value sharing.

[[2022 FlashAttention]] keeps attention mathematically exact but changes the computation schedule to reduce memory IO.

[[2024 DeepSeek-V2 Technical Report]] introduces [[Multi-Head Latent Attention]] as a later KV-cache compression approach that changes the representation of cached attention state.

## Related papers
- [[2017 Attention Is All You Need]]
- [[2019 Fast Transformer Decoding One Write-Head is All You Need]]
- [[2022 FlashAttention]]
- [[2023 GQA]]
- [[2024 DeepSeek-V2 Technical Report]]

## Related concepts
- [[Transformers]]
- [[Efficient LLM Architecture]]
- [[Self-Attention]]
- [[Multi-Head Attention]]
- [[Grouped-Query Attention]]
- [[Multi-Query Attention]]
- [[Multi-Head Latent Attention]]
- [[KV Cache]]
- [[FlashAttention]]
- [[Scaled Dot-Product Attention]]
- [[Notation Conventions]]

## Open questions
- Needs verification: add earlier attention sources to distinguish pre-transformer attention from transformer self-attention.
- Needs verification: add source-grounded notes for XSA, sparse attention, attention residuals, and other recent attention variants before expanding this page.

## Source notes
- [[2017 Attention Is All You Need]]
- [[2019 Fast Transformer Decoding One Write-Head is All You Need]]
- [[2022 FlashAttention]]
- [[2023 GQA]]
- [[2024 DeepSeek-V2 Technical Report]]
