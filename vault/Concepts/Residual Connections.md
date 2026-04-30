# Residual Connections

## Metadata
- Type: concept
- Status: stub
- Last reviewed: 2026-04-29

## Short definition
Residual connections add a sublayer's input back to its output.

## Intuition
Residual connections provide a direct path for information and gradients across layers.

## Mathematical formulation
- Related math: [[Layer Normalization (Math)]], [[RMSNorm (Math)]]
- In [[2017 Attention Is All You Need]], each sublayer is wrapped as:

`LayerNorm(x + Sublayer(x))`.

## Historical development
The Transformer paper uses residual connections around attention and feed-forward sublayers, citing earlier residual network work.

## Related papers
- [[2017 Attention Is All You Need]]

## Related concepts
- [[Transformers]]
- [[Transformer Architecture]]
- [[Layer Normalization]]
- [[RMSNorm]]
- [[Optimization and Training Stability]]

## Open questions
- Needs verification: residual connections should be grounded later in the original ResNet paper or a transformer-specific residual-stream source.
- Needs verification: attention residuals, gating residuals, and residual-stream views should be added only after source-grounded ingests.

## My understanding
For now, this page only records the role residual connections play in the Transformer block.

## Source notes
- [[2017 Attention Is All You Need]]

## Revision notes
