# Gradient Descent

## Metadata
- Type: math
- Status: developing
- Last reviewed: 2026-04-30

## Goal
Describe iterative optimization using gradients.

## Canonical notation
- `theta_t`: parameters after timestep `t`.
- `g_t`: gradient or stochastic gradient at timestep `t`.
- `alpha`: learning rate.

## Definitions
- Gradient descent updates parameters in the direction that locally decreases a differentiable objective.
- Stochastic gradient descent uses a noisy gradient estimate, often from a minibatch:

```text
theta_t = theta_{t-1} - alpha * g_t
```

## Assumptions
- The objective is differentiable with respect to parameters.
- The gradient or stochastic gradient is available.
- The update uses a learning rate `alpha`.

## Derivation
- Starting from a first-order local approximation, moving opposite the gradient decreases the objective for sufficiently small step size.
- Needs verification: a full derivation should be grounded in an optimization source.

## Interpretation
- [[Adam]] extends stochastic gradient descent by smoothing gradients with a first moment estimate and rescaling updates with a second raw moment estimate.

## Common mistakes
- Treating the learning rate as universally stable across models or parameterizations.
- Forgetting that stochastic gradients add noise relative to full-batch gradients.

## Related concepts
- [[Adam]]
- [[Optimization and Training Stability]]
