# Scaled Dot-Product Attention

## Metadata
- Type: math
- Status: partially verified
- Last reviewed: 2026-04-29

## Goal
Define the attention operation used as the core computation in the original Transformer.

## Canonical notation
- `Q`: query matrix
- `K`: key matrix
- `V`: value matrix
- `d_k`: key/query dimensionality

## Definitions
- Source: [[2017 Attention Is All You Need]].
- An attention function maps queries and key-value pairs to outputs.
- The output is a weighted sum of values.
- The weights are computed from query-key compatibility scores.

## Assumptions
- Queries and keys have dimension `d_k`.
- Values have dimension `d_v`.
- The attention operation is applied to matrices of queries, keys, and values.

## Main result
`Attention(Q,K,V) = softmax(QK^T / sqrt(d_k)) V`.

## Derivation
- Compute dot-product scores between queries and keys: `QK^T`.
- Scale the scores by `1 / sqrt(d_k)`.
- Apply softmax row-wise to obtain attention weights.
- Multiply the attention weights by `V` to produce weighted sums of values.
- Skipped steps: gradient analysis of the softmax saturation issue.

## Interpretation
The query-key dot product measures compatibility. The softmax turns compatibilities into weights over values. The scaling factor reduces the magnitude of dot products when `d_k` is large.

## Alternative formulations
- Additive attention uses a feed-forward network for compatibility scoring.
- Unscaled dot-product attention omits the `1 / sqrt(d_k)` factor.

## Common mistakes
- Forgetting that `Q`, `K`, and `V` are learned projections, not necessarily raw token embeddings.
- Treating attention weights as explanations without checking the model and task context.
- Omitting the scaling factor when describing the original Transformer.

## Related concepts
- [[Attention]]
- [[Self-Attention]]
- [[Multi-Head Attention]]
- [[Transformers]]

## Related papers
- [[2017 Attention Is All You Need]]

## Source references
- [[2017 Attention Is All You Need]]

## Verification status
- Status: partially verified
- Needs verification: deeper variance/gradient explanation for why scaling stabilizes softmax should be checked against a math source.
