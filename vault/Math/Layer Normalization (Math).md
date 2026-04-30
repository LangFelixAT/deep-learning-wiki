# Layer Normalization (Math)

## Metadata
- Type: math
- Status: partially verified
- Last reviewed: 2026-04-29

## Goal
Define the layer normalization operation introduced in [[2016 Layer Normalization]].

## Canonical notation
- `a_i`: summed input to hidden unit `i` in a layer
- `H`: number of hidden units/features in the layer
- `mu`: mean of summed inputs within the layer for one training case
- `sigma`: standard deviation of summed inputs within the layer for one training case
- `g_i`: learned gain for unit `i`
- `b_i`: learned bias for unit `i`

## Definitions
- Source: [[2016 Layer Normalization]].
- Layer normalization computes normalization statistics across hidden units within a layer for a single training case.
- The same computation is used at training and test time.
- Learned gain and bias are applied after normalization and before the nonlinearity.

## Assumptions
- The layer has `H` hidden units or features.
- The normalization statistics are computed from summed inputs in a single example, not from a mini-batch.
- This note uses the paper's feed-forward notation and does not cover modern Transformer pre-norm/post-norm variants.

## Main result
Layer mean:

`mu = (1/H) sum_{i=1}^H a_i`.

Layer standard deviation:

`sigma^2 = (1/H) sum_{i=1}^H (a_i - mu)^2`.

`sigma = sqrt((1/H) sum_{i=1}^H (a_i - mu)^2)`.

Layer-normalized activation:

`h_i = f((g_i / sigma)(a_i - mu) + b_i)`.

## Derivation
- Start from a vector of summed inputs `a = (a_1, ..., a_H)` for one layer and one training case.
- Compute the mean over features in that layer.
- Compute the standard deviation over features in that layer.
- Center and rescale each `a_i` using the shared `mu` and `sigma`.
- Apply learned unit-specific gain `g_i` and bias `b_i`.
- Skipped steps: the paper's invariance and Fisher-geometry analysis.

## Interpretation
Layer normalization standardizes a layer's feature vector for each example independently. This avoids dependence on mini-batch size and avoids separate running averages for training and test time.

## Alternative formulations
- [[Normalization]] covers the broader family.
- Batch normalization computes statistics over training cases in a mini-batch for a given unit.
- Weight normalization normalizes using the norm of incoming weights rather than activation statistics.
- [[RMSNorm (Math)]] removes mean-centering and divides by root mean square.

## Common mistakes
- Confusing layer normalization with batch normalization.
- Assuming layer normalization needs running batch statistics at test time.
- Treating the Transformer use of LayerNorm as if this paper introduced pre-norm or post-norm Transformer variants.

## Related concepts
- [[Layer Normalization]]
- [[Normalization]]
- [[RMSNorm]]
- [[RMSNorm (Math)]]
- [[Transformers]]
- [[Residual Connections]]

## Related papers
- [[2016 Layer Normalization]]
- [[2019 Root Mean Square Layer Normalization]]
- [[2017 Attention Is All You Need]]

## Source references
- [[2016 Layer Normalization]]

## Verification status
- Status: partially verified
- Needs verification: modern Transformer-specific notation should be checked against later architecture sources.
