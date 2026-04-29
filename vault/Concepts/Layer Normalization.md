# Layer Normalization

## Metadata
- Type: concept
- Status: stub
- Last reviewed: 2026-04-29

## Short definition
Layer normalization is a normalization method used inside neural network layers.

## Intuition
In the original Transformer, layer normalization is part of the sublayer wrapper that stabilizes stacked attention and feed-forward blocks.

## Mathematical formulation
- Related math:
- [[2017 Attention Is All You Need]] uses:

`LayerNorm(x + Sublayer(x))`.

## Historical development
The Transformer paper uses layer normalization as architectural scaffolding, but does not introduce the method.

## Related papers
- [[2017 Attention Is All You Need]]

## Related concepts
- [[Transformers]]
- [[Residual Connections]]
- [[Normalization]]

## Open questions
- Needs verification: ingest the Layer Normalization paper for the actual definition, assumptions, and comparison to batch normalization.

## My understanding
This page is a placeholder for the architecture role of layer normalization until the dedicated source is ingested.

## Source notes
- [[2017 Attention Is All You Need]]

## Revision notes
