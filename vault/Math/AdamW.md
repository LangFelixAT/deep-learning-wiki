# AdamW

## Metadata
- Type: math
- Status: partially verified
- Last reviewed: 2026-04-30

## Goal
Define AdamW as [[Adam]] with decoupled [[Weight Decay]], and clarify why this differs from applying L2 regularization inside Adam's gradient.

## Canonical notation
- `theta_t`: parameter vector at timestep `t`.
- `g_t`: stochastic loss gradient at timestep `t`.
- `alpha`: base learning rate.
- `eta_t`: schedule multiplier used in the source paper.
- `lambda`: weight decay factor.
- `lambda'`: L2 regularization coefficient.
- `m_t`, `v_t`, `hat_m_t`, `hat_v_t`: Adam moment estimates as in [[Adam]].
- `M_t`: generic adaptive preconditioner used to reason about adaptive gradient methods.

## Definitions
- L2 regularization adds a penalty term to the optimized loss:

```text
f_t^reg(theta) = f_t(theta) + (lambda' / 2) ||theta||_2^2
```

- Weight decay directly shrinks parameters during the optimizer step.
- Decoupled weight decay applies the shrinkage term separately from the loss-gradient update.
- AdamW is Adam with weight decay decoupled from Adam's adaptive gradient scaling.

## Assumptions
- Standard SGD uses a scalar learning rate without a nontrivial adaptive preconditioner.
- Adaptive optimizers such as Adam rescale gradient coordinates using history-dependent quantities.
- Vector operations in Adam remain elementwise.
- This note ignores schedule tuning and normalized weight decay details.

## Main result
For standard SGD, L2 regularization and weight decay can be equivalent after rescaling:

```text
lambda' = lambda / alpha
```

For adaptive gradient methods, the equivalence generally fails because the L2 penalty gradient is also scaled by the adaptive preconditioner.

AdamW keeps weight decay outside the adaptive gradient step:

```text
theta_t = theta_{t-1} - eta_t * (alpha * hat_m_t / (sqrt(hat_v_t) + epsilon) + lambda theta_{t-1})
```

In this high-level AdamW form, `hat_m_t` and `hat_v_t` are computed from the loss gradient rather than from an L2-augmented gradient.

## Derivation
- Standard SGD with L2-regularized loss:

```text
theta_{t+1}
  = theta_t - alpha grad(f_t(theta_t) + (lambda' / 2) ||theta_t||_2^2)
  = theta_t - alpha grad f_t(theta_t) - alpha lambda' theta_t
```

- Standard SGD with weight decay:

```text
theta_{t+1} = (1 - lambda) theta_t - alpha grad f_t(theta_t)
```

- These match when:

```text
alpha lambda' = lambda
```

- For an adaptive optimizer with preconditioner `M_t`, L2 regularization gives:

```text
theta_{t+1} = theta_t - alpha M_t (grad f_t(theta_t) + lambda' theta_t)
```

- Decoupled weight decay gives:

```text
theta_{t+1} = (1 - lambda) theta_t - alpha M_t grad f_t(theta_t)
```

- These are not generally equivalent unless the preconditioner behaves like a scalar multiple of the identity.
- Skipped steps: the source paper's proposition proofs and experimental analysis are not expanded here.

## Interpretation
In Adam with L2 regularization, the regularization gradient enters Adam's adaptive machinery. In AdamW, the loss-gradient update is adaptive, but the weight decay is a separate parameter-shrinkage operation.

This separation makes the meaning of the weight decay coefficient cleaner: it controls shrinkage rather than a penalty gradient that is filtered through Adam's coordinatewise scaling.

## Alternative formulations
- SGDW applies the same decoupling idea to SGD with momentum. This note only keeps it as a brief comparison because the current focus is AdamW.
- The source includes schedule multipliers and normalized weight decay, but those details are outside this ingest scope.

## Common mistakes
- Calling L2 regularization "weight decay" without checking the optimizer.
- Assuming L2 regularization and weight decay are always equivalent because they are equivalent for standard SGD.
- Computing Adam moments from a gradient that includes the L2 penalty and calling the result AdamW.

## Related concepts
- [[Adam]]
- [[Weight Decay]]
- [[Gradient Descent]]
- [[Optimization and Training Stability]]

## Related papers
- [[2014 Adam]]
- [[2017 Decoupled Weight Decay Regularization]]

## Source references
- [[2017 Decoupled Weight Decay Regularization]]

## Verification status
- Status: partially verified
- Needs verification: schedule-dependent normalized weight decay and later large-model usage are outside this note.
