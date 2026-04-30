# Preconditioning

## Metadata
- Type: math
- Status: developing
- Last reviewed: 2026-04-30

## Goal
Define preconditioning as the transformation of gradients before an optimization step, with emphasis on why it matters for adaptive and matrix-aware optimizers.

## Canonical notation
- `theta_t`: parameter vector at timestep `t`.
- `g_t`: gradient at timestep `t`.
- `P_t`: preconditioner.
- `alpha`: learning rate.
- `||.||`: update norm in steepest-descent views.

## Definitions
- Preconditioner: a matrix or operator that transforms the gradient direction before the update.
- Coordinatewise preconditioner: a diagonal or elementwise scaling of the gradient.
- Full-matrix preconditioner: a dense matrix that can mix coordinates in the update.
- Structured preconditioner: a cheaper approximation that uses known parameter structure, such as matrix or tensor dimensions.
- Update geometry: the implicit shape of allowed or preferred updates, often described by a norm.

## Assumptions
- The objective is differentiable with respect to parameters.
- The preconditioner is chosen to make optimization better conditioned or better scaled.
- The exact meaning of `P_t` depends on the optimizer source.

## Main result
A generic preconditioned gradient step can be written as:

```text
theta_{t+1} = theta_t - alpha P_t g_t
```

For coordinatewise methods, `P_t` is effectively diagonal. For matrix-aware methods, `P_t` may use matrix or tensor structure.

From the steepest-descent perspective in [[2024 Old Optimizer New Norm]], choosing an update norm is another way to specify optimizer geometry.

## Derivation
- Start from gradient descent:

```text
theta_{t+1} = theta_t - alpha g_t
```

- Insert a transformation before the gradient is applied:

```text
theta_{t+1} = theta_t - alpha P_t g_t
```

- If `P_t` rescales coordinates independently, the update resembles diagonal adaptive methods.
- If `P_t` mixes coordinates or acts along tensor dimensions, the update can reflect richer geometry.
- Skipped steps: curvature-based derivations and second-order methods are not developed here.

## Interpretation
Preconditioning changes the geometry of the update. Instead of asking only "how large should the learning rate be?", it asks "in which transformed coordinate system should the gradient step be taken?"

In this wiki, [[Adam]] and [[AdamW]] provide coordinatewise adaptive scaling, while [[Shampoo]] is a source-grounded example of structure-aware preconditioning.

[[Steepest Descent]] reframes this: different optimizers can be viewed as choosing different norms for measuring updates. This makes the difference between coordinatewise and matrix-aware methods more explicit.

## Alternative formulations
- Preconditioning can be written as left-multiplying a flattened gradient.
- For matrix parameters, structured methods may apply separate transformations along rows and columns instead of forming one full matrix.
- A norm-based view can describe similar geometry without explicitly presenting the method as a preconditioner.

## Common mistakes
- Treating all adaptive optimizers as the same kind of preconditioning.
- Assuming a preconditioner must be a full dense matrix.
- Describing preconditioning as a guarantee of faster training without checking assumptions and source evidence.

## Related concepts
- [[Gradient Descent]]
- [[Steepest Descent]]
- [[Adam]]
- [[AdamW]]
- [[Shampoo]]
- [[Matrix-Aware Optimizers]]
- [[Optimization and Training Stability]]

## Related papers
- [[2018 Shampoo]]
- [[2024 Old Optimizer New Norm]]

## Source references
- [[2018 Shampoo]]
- [[2024 Old Optimizer New Norm]]

## Verification status
- Status: developing
- Needs verification: stronger links to second-order optimization and curvature should be grounded in later sources.
