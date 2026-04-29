# Multi-Head Latent Attention

## Metadata
- Type: concept
- Status: stub
- Last reviewed: 2026-04-29

## Short definition
Multi-Head Latent Attention is an attention variant that uses latent compression of attention states to reduce KV-cache cost during inference.

## Intuition
In autoregressive decoding, the [[KV Cache]] can become a major memory bottleneck. MLA aims to store a compressed latent representation for keys and values rather than caching the full key/value tensors in the standard form.

## Mathematical formulation
- Related math: [[Scaled Dot-Product Attention]]
- In [[2024 DeepSeek-V3 Technical Report]], MLA computes a compressed KV latent `c_t^{KV}` from the token hidden state `h_t`.
- The source states that only the compressed KV latent and a decoupled RoPE key need to be cached during generation.
- Needs verification: full MLA equations and exact comparison to [[Multi-Head Attention]], [[Multi-Query Attention]], and [[Grouped-Query Attention]] should be handled in a focused follow-up.

## Historical development
[[2024 DeepSeek-V3 Technical Report]] uses MLA for efficient inference and states that it was validated in DeepSeek-V2.

## Related papers
- [[2024 DeepSeek-V3 Technical Report]]

## Related concepts
- [[KV Cache]]
- [[Multi-Head Attention]]
- [[Multi-Query Attention]]
- [[Grouped-Query Attention]]
- [[Rotary Position Embedding]]
- [[Large Language Models]]

## Open questions
- Needs verification: determine whether the DeepSeek-V2 report should be the primary MLA source.
- Needs verification: formalize the cache-size comparison against MHA, MQA, and GQA.

## My understanding
MLA is primarily an inference-efficiency idea: reduce what must be cached and read during decoding while aiming to retain strong attention performance through reconstruction/projection from latent state.

## Source notes
- [[2024 DeepSeek-V3 Technical Report]]

## Revision notes
