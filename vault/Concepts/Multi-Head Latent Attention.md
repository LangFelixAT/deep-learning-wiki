# Multi-Head Latent Attention

## Metadata
- Type: concept
- Status: developing
- Last reviewed: 2026-04-29

## Short definition
Multi-Head Latent Attention is an attention variant that uses latent compression of attention states to reduce KV-cache cost during inference.

## Intuition
In autoregressive decoding, the [[KV Cache]] can become a major memory bottleneck. MLA aims to store a compressed latent representation for keys and values rather than caching the full key/value tensors in the standard form.

## Mathematical formulation
- Related math: [[Scaled Dot-Product Attention]], [[Multi-Head Latent Attention (Math)]]
- Primary source context: [[2024 DeepSeek-V2 Technical Report]]
- MLA computes a compressed KV latent from token hidden state `h_t`.
- Keys and values can be reconstructed from this latent with up-projection matrices.
- The source states that, with decoupled RoPE, DeepSeek-V2 caches the compressed KV latent plus a decoupled RoPE key during generation.
- In the source's notation, MHA caches `2 n_h d_h l` elements per token, while MLA caches `(d_c + d_h^R) l` elements per token.
- See [[Multi-Head Latent Attention (Math)]] for the math-note version of the MLA equations.

## Historical development
[[2024 DeepSeek-V2 Technical Report]] introduces MLA to reduce KV-cache cost relative to standard [[Multi-Head Attention]]. It compares MLA with [[Grouped-Query Attention]] and [[Multi-Query Attention]] as KV-cache reduction approaches.

[[2024 DeepSeek-V3 Technical Report]] reuses MLA and states that the architecture was validated in DeepSeek-V2.

## Related papers
- [[2024 DeepSeek-V2 Technical Report]]
- [[2024 DeepSeek-V3 Technical Report]]

## Related concepts
- [[KV Cache]]
- [[Multi-Head Attention]]
- [[Multi-Query Attention]]
- [[Grouped-Query Attention]]
- [[Rotary Position Embedding]]
- [[Large Language Models]]

## Open questions
- Needs verification: compare MLA, MHA, MQA, and GQA using sources beyond DeepSeek-V2.

## My understanding
MLA is primarily an inference-efficiency idea: reduce what must be cached and read during decoding while aiming to retain strong attention performance through reconstruction/projection from latent state.

## Source notes
- [[2024 DeepSeek-V3 Technical Report]]
- [[2024 DeepSeek-V2 Technical Report]]

## Revision notes
