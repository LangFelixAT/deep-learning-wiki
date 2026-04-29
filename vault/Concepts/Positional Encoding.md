# Positional Encoding

## Metadata
- Type: concept
- Status: developing

## Short definition
Information added to sequence models so position can influence computation.

## Intuition
Self-attention by itself does not encode token order. Positional encodings inject information about absolute or relative position so the model can use sequence order.

Absolute positional encodings attach position information to each token. Relative methods make attention depend on distances or offsets between tokens.

## Mathematical formulation
- Related math: [[Transformers]], [[Scaled Dot-Product Attention]], [[Rotary Position Embedding (Math)]]
- [[2017 Attention Is All You Need]] adds positional encodings to token embeddings at the bottoms of the encoder and decoder stacks.
- The paper uses sinusoidal encodings with sine on even dimensions and cosine on odd dimensions.
- [[2021 RoFormer]] introduces [[Rotary Position Embedding]], which rotates query and key representations so their dot product depends on relative position.

## Historical development
[[2017 Attention Is All You Need]] uses sinusoidal positional encodings and also reports learned positional embeddings as a comparison.

[[2021 RoFormer]] introduces RoPE as a multiplicative positional encoding for self-attention.

## Related papers
- [[2017 Attention Is All You Need]]
- [[2021 RoFormer]]

## Related concepts
- [[Transformers]]
- [[Attention]]
- [[Self-Attention]]
- [[Rotary Position Embedding]]
- [[Rotary Position Embedding (Math)]]

## Open questions
- Needs verification: later RoPE scaling and long-context methods should be grounded in their own source notes.

## Source notes
- [[2017 Attention Is All You Need]]
- [[2021 RoFormer]]
