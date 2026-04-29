# Self-Attention

## Metadata
- Type: concept
- Status: developing

## Short definition
Attention applied among elements of the same sequence or set.

## Intuition
In self-attention, each token forms attention weights over tokens from the same sequence. This lets a token representation incorporate information from other positions directly.

## Mathematical formulation
- Related math: [[Scaled Dot-Product Attention]]
- In encoder self-attention, queries, keys, and values all come from the previous layer of the same sequence.
- In decoder self-attention, masking prevents a position from attending to future positions.

## Historical development
[[2017 Attention Is All You Need]] uses stacked self-attention layers as the main replacement for recurrent sequence computation.

## Related papers
- [[2017 Attention Is All You Need]]

## Related concepts
- [[Attention]]
- [[Transformers]]
- [[Multi-Head Attention]]
- [[Positional Encoding]]

## Open questions
- Needs verification: add earlier self-attention uses cited by the Transformer paper.

## Source notes
- [[2017 Attention Is All You Need]]
