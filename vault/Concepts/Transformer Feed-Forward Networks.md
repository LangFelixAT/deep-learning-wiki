# Transformer Feed-Forward Networks

## Metadata
- Type: concept
- Status: developing
- Last reviewed: 2026-04-29

## Short definition
Transformer feed-forward networks are position-wise MLP sublayers applied independently to each token representation.

## Intuition
Attention mixes information across positions. The feed-forward block then transforms each position's representation independently with the same learned function.

## Mathematical formulation
- Related math:
- In [[2017 Attention Is All You Need]], each encoder and decoder layer contains:

`FFN(x) = max(0, xW_1 + b_1) W_2 + b_2`.

- The same feed-forward network is applied separately and identically to each position.

## Historical development
[[2017 Attention Is All You Need]] uses position-wise feed-forward networks as the second main sublayer type in transformer blocks, alongside attention.

## Related papers
- [[2017 Attention Is All You Need]]

## Related concepts
- [[Transformers]]
- [[Self-Attention]]
- [[Residual Connections]]
- [[Layer Normalization]]

## Open questions
- Needs verification: later LLM feed-forward variants such as gated MLPs and SwiGLU should be grounded in separate source notes.

## My understanding
The feed-forward block is where each token representation is nonlinearly transformed after attention has mixed sequence information.

## Source notes
- [[2017 Attention Is All You Need]]

## Revision notes
