# Muon Optimizer (Math)

## Metadata
- Type: math
- Status: partially verified
- Last reviewed: 2026-04-30

## Goal
Describe the high-level mathematical structure of Muon: momentum followed by approximate orthogonalization of hidden-layer matrix updates.

## Canonical notation
- `W_t`: hidden-layer weight matrix at timestep `t`.
- `G_t`: gradient or momentum-derived update matrix for `W_t`.
- `M_t`: momentum buffer for a matrix parameter.
- `beta`: momentum coefficient.
- `eta`: learning rate for the Muon update.
- `lambda`: decoupled weight decay factor.
- `Ortho(G)`: idealized semi-orthogonalized version of update matrix `G`.
- `U S V^T`: singular value decomposition of `G`.

## Definitions
- Matrix parameter: a 2D hidden-layer weight tensor that Muon is intended to optimize.
- Semi-orthogonal matrix: a rectangular matrix satisfying either `O^T O = I` or `O O^T = I`, depending on shape.
- Orthogonalized update: an update matrix whose singular values are pushed toward a common scale.
- Newton-Schulz iteration: an iterative matrix method used by the source implementation to approximate orthogonalization.

## Assumptions
- Muon is applied to hidden matrix parameters, not all model parameters.
- Embeddings, output heads, scalar/vector parameters, gains, and biases remain on an Adam-style optimizer according to the source guidance.
- Newton-Schulz details are treated at a high level here.
- Empirical performance claims are source claims, not proof of general superiority.

## Main result
Muon can be summarized as:

```text
momentum_update -> approximate_orthogonalization -> weight_update
```

For an update matrix `G`, the idealized orthogonalization target is:

```text
Ortho(G) = U V^T
```

where:

```text
G = U S V^T
```

The source implementation approximates this operation with a Newton-Schulz-style iteration rather than computing the SVD directly.

## Derivation
- Start from a gradient-like matrix update for a hidden weight matrix:

```text
G_t = grad_W L_t(W_t)
```

- Maintain a momentum-style update. A simplified non-Nesterov form is:

```text
M_t = beta M_{t-1} + (1 - beta) G_t
```

- Orthogonalize or approximately orthogonalize the momentum-derived update:

```text
U_t = Ortho(M_t)
```

- Apply decoupled weight decay and the Muon update:

```text
W_{t+1} = (1 - eta lambda) W_t - eta U_t
```

- Skipped steps: the exact Newton-Schulz polynomial iteration, coefficient tuning, and convergence behavior are not fully derived here.
- Skipped steps: the relationship to Shampoo-style preconditioning is marked as `Needs verification` until [[Shampoo]] is ingested.

## Interpretation
Muon replaces the raw or momentum-smoothed matrix update with a matrix whose singular values are more balanced. This is different from [[AdamW]], which rescales coordinates using first and second moment estimates.

In source terms, Muon is not a universal replacement for AdamW. It is a matrix-parameter optimizer that is paired with AdamW for parameter classes that are not suitable for Muon.

## Alternative formulations
- The source describes Nesterov-style momentum as the practical default.
- The implementation supports convolution filters by flattening them into a matrix-like form.
- The source relates Muon to [[Shampoo]] and orthogonalized-gradient methods, but this wiki has not yet ingested those sources in detail.

## Common mistakes
- Treating Muon as an optimizer for all parameters.
- Treating Muon as simply AdamW with different hyperparameters.
- Treating empirical speedrun claims as settled broad optimizer superiority.
- Confusing approximate Newton-Schulz orthogonalization with exact SVD-based orthogonalization.

## Related concepts
- [[Muon Optimizer]]
- [[Newton-Schulz Iteration]]
- [[Matrix-Aware Optimizers]]
- [[Shampoo]]
- [[AdamW]]
- [[Gradient Descent]]
- [[Weight Decay]]

## Related papers
- [[2024 Muon Optimizer]]

## Source references
- [[2024 Muon Optimizer]]

## Verification status
- Status: partially verified
- Needs verification: full Newton-Schulz derivation, Shampoo relationship, and large-scale empirical claims.
