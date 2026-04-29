# Layer Normalization

## Metadata
- Type: concept
- Status: developing
- Last reviewed: 2026-04-29

## Short definition
Layer normalization normalizes a layer's summed inputs across features within a single training case.

## Intuition
Batch normalization uses statistics across a mini-batch. Layer normalization instead uses statistics within one example, so it does not depend on batch size and uses the same computation during training and testing.

In the original Transformer, layer normalization is part of the sublayer wrapper that stabilizes stacked attention and feed-forward blocks.

## Mathematical formulation
- Related math: [[Layer Normalization (Math)]]
- In [[2016 Layer Normalization]], the mean and variance are computed over the summed inputs to all hidden units in a layer for one training case.
- [[2017 Attention Is All You Need]] uses:

`LayerNorm(x + Sublayer(x))`.

## Historical development
[[2016 Layer Normalization]] introduces the method as an alternative to batch normalization that is easier to apply to recurrent and sequence models.

[[2017 Attention Is All You Need]] uses layer normalization as architectural scaffolding in Transformer sublayer wrappers.

## Related papers
- [[2016 Layer Normalization]]
- [[2017 Attention Is All You Need]]

## Related concepts
- [[Transformers]]
- [[Residual Connections]]
- [[Normalization]]
- [[Layer Normalization (Math)]]

## Open questions
- Needs verification: pre-norm versus post-norm Transformer variants should be grounded in later sources.
- Needs verification: RMSNorm should be grounded in its own source note.

## My understanding
Layer normalization is especially natural for sequence models because the normalization statistics are local to one example and one layer/timestep.

## Source notes
- [[2016 Layer Normalization]]
- [[2017 Attention Is All You Need]]

## Revision notes
