# Rotary Position Embedding

## Metadata
- Type: concept
- Status: developing
- Last reviewed: 2026-04-29

## Short definition
Rotary position embedding, or RoPE, injects position information by rotating query and key vectors before attention scores are computed.

## Intuition
Instead of adding a position vector to token embeddings, RoPE rotates parts of the query and key vectors by angles determined by token position. When two rotated vectors are compared with a dot product, their relative rotation encodes relative distance.

## Mathematical formulation
- Related math: [[Rotary Position Embedding (Math)]]
- RoPE applies position-dependent rotation matrices to query and key representations.
- Absolute positions choose the rotations, while the query-key comparison exposes relative position.
- The resulting query-key dot product depends on the relative offset between positions.

## Historical development
[[2021 RoFormer]] introduces RoPE as the core positional encoding method in RoFormer.

## Related papers
- [[2021 RoFormer]]
- [[2017 Attention Is All You Need]]

## Related concepts
- [[Positional Encoding]]
- [[Self-Attention]]
- [[Scaled Dot-Product Attention]]
- [[Transformers]]
- [[Large Language Models]]

## Open questions
- Needs verification: later RoPE scaling methods should be grounded in their own source notes.
- Needs verification: document which LLM architecture papers adopt RoPE directly.

## My understanding
RoPE makes relative position appear through geometry: absolute positions determine rotations, and relative position appears when rotated queries and keys interact.

## Source notes
- [[2021 RoFormer]]

## Revision notes
