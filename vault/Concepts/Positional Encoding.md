# Positional Encoding

## Metadata
- Type: concept
- Status: developing

## Short definition
Information added to sequence models so position can influence computation.

## Intuition
Self-attention by itself does not encode token order. Positional encodings inject information about absolute or relative position so the model can use sequence order.

## Mathematical formulation
- Related math: [[Transformers]], [[Scaled Dot-Product Attention]]
- [[2017 Attention Is All You Need]] adds positional encodings to token embeddings at the bottoms of the encoder and decoder stacks.
- The paper uses sinusoidal encodings with sine on even dimensions and cosine on odd dimensions.

## Historical development
[[2017 Attention Is All You Need]] uses sinusoidal positional encodings and also reports learned positional embeddings as a comparison.

## Related papers
- [[2017 Attention Is All You Need]]

## Related concepts
- [[Transformers]]
- [[Attention]]
- [[Self-Attention]]

## Open questions
- Needs verification: later positional encoding methods such as RoPE should be grounded in their own source notes.

## Source notes
- [[2017 Attention Is All You Need]]
