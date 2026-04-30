# Shampoo

## Metadata
- Type: math
- Status: partially verified
- Last reviewed: 2026-04-30

## Goal
Define the high-level Shampoo optimizer update as tensor-aware preconditioning for matrix and tensor parameters.

## Canonical notation
- `W_t`: matrix-valued parameter at timestep `t`.
- `G_t`: gradient matrix for `W_t`.
- `eta`: learning rate or stepsize.
- `L_t`: left Shampoo preconditioner for matrix rows.
- `R_t`: right Shampoo preconditioner for matrix columns.
- `epsilon`: small positive initialization constant for preconditioners.
- `k`: order of a tensor parameter.

## Definitions
- Preconditioning: transforming the gradient before the parameter update, usually to account for geometry or gradient scale.
- Full-matrix preconditioner: a preconditioner over a flattened parameter vector; expressive but expensive for large tensors.
- Coordinatewise adaptive method: an optimizer such as diagonal AdaGrad, [[Adam]], or [[AdamW]] that rescales each coordinate separately.
- Tensor-aware preconditioning: using the matrix or tensor shape of a parameter when constructing the update.
- Matrix inverse power: a matrix function such as `L_t^(-1/4)` computed from a positive definite preconditioner.

## Assumptions
- The parameter has matrix or tensor structure.
- Preconditioners are positive definite or stabilized with `epsilon I`.
- The matrix update below follows the source's matrix case; tensor notation is kept high-level here.
- Full convergence analysis and trace inequality proof details are outside this note.

## Main result
For a matrix parameter, Shampoo maintains separate left and right gradient accumulators:

```text
L_t = L_{t-1} + G_t G_t^T
R_t = R_{t-1} + G_t^T G_t
```

and updates:

```text
W_{t+1} = W_t - eta L_t^(-1/4) G_t R_t^(-1/4)
```

This approximates a richer preconditioned update while avoiding the full preconditioner over `vec(W_t)`.

## Derivation
- Start from a gradient update for a matrix parameter:

```text
W_{t+1} = W_t - eta G_t
```

- Full-matrix preconditioning would flatten `W_t` and apply a preconditioner over all `mn` coordinates. For `W_t in R^{m x n}`, this would require a matrix of size `mn x mn`.
- Shampoo instead accumulates row-side and column-side gradient statistics:

```text
L_t = L_{t-1} + G_t G_t^T
R_t = R_{t-1} + G_t^T G_t
```

- Apply inverse matrix powers on both sides of the gradient:

```text
preconditioned_gradient = L_t^(-1/4) G_t R_t^(-1/4)
```

- Use this transformed gradient in the update:

```text
W_{t+1} = W_t - eta * preconditioned_gradient
```

- Skipped steps: proof of the `1/4` exponent, convergence guarantees, and matrix trace inequalities from the source.
- Skipped steps: the full tensor-order-`k` derivation. The source generalizes by maintaining one preconditioner per tensor dimension and applying inverse factors along those dimensions.

## Interpretation
Shampoo is matrix-aware because it treats a weight matrix as a matrix, not as an unrelated list of coordinates. The left preconditioner captures row-side structure, and the right preconditioner captures column-side structure.

Compared with coordinatewise methods such as [[Adam]] or [[AdamW]], Shampoo can represent richer update geometry. Compared with a full preconditioner over the flattened parameter, Shampoo is cheaper because it stores and applies smaller per-dimension matrices.

[[2024 Old Optimizer New Norm]] adds a complementary interpretation: Shampoo without accumulation produces a semi-orthogonal update direction and can be viewed as steepest descent under a spectral-norm geometry.

This makes Shampoo an important bridge toward [[Matrix-Aware Optimizers]] and a historical comparison point for [[Muon Optimizer]].

## Alternative formulations
- For higher-order tensors, Shampoo maintains one preconditioner for each tensor dimension.
- The source relates Shampoo to full-matrix AdaGrad and diagonal AdaGrad. The matrix/tensor form can be read as a structured compromise between full preconditioning and diagonal preconditioning.
- The norm-geometry view treats Shampoo without accumulation as related to spectral steepest descent.
- Needs verification: practical implementations may use approximations, update-frequency tricks, or distributed variants that are outside the 2018 source scope.

## Common mistakes
- Treating Shampoo as just a scalar learning-rate schedule.
- Treating Shampoo as coordinatewise like AdamW. Shampoo uses matrix/tensor structure.
- Assuming the full-matrix preconditioner is explicitly formed.
- Importing distributed Shampoo, SOAP, or Muon details into the original Shampoo paper without a separate source.

## Related concepts
- [[Matrix-Aware Optimizers]]
- [[Preconditioning]]
- [[Steepest Descent]]
- [[Muon Optimizer]]
- [[Muon Optimizer (Math)]]
- [[Adam]]
- [[AdamW]]
- [[Optimization and Training Stability]]

## Related papers
- [[2018 Shampoo]]
- [[2024 Old Optimizer New Norm]]
- [[2024 Muon Optimizer]]

## Source references
- [[2018 Shampoo]]
- [[2024 Old Optimizer New Norm]]

## Verification status
- Status: partially verified
- Needs verification: full tensor derivation, convergence proof, practical no-accumulation relationship, and modern large-scale optimizer comparisons.
