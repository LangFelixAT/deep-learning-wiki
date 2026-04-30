# Weight Decay

## Metadata
- Type: math
- Status: partially verified
- Last reviewed: 2026-04-30

## Goal
Define weight decay and distinguish it from related regularization ideas.

## Definitions
- Weight decay is a training mechanism that penalizes or shrinks parameter magnitudes.
- L2 regularization adds a penalty term to the loss, often written `(lambda' / 2) ||theta||_2^2`.
- For standard SGD, L2 regularization and weight decay can be equivalent after rescaling the coefficient by the learning rate.
- For adaptive optimizers, this equivalence does not generally hold because L2 penalty gradients are affected by adaptive coordinatewise scaling.

## Assumptions
- The SGD equivalence assumes a scalar learning rate and no nontrivial adaptive preconditioner.
- Adaptive optimizer statements depend on the optimizer's preconditioning or coordinatewise scaling.

## Derivation
- Standard SGD with L2 regularization:

```text
theta_{t+1} = theta_t - alpha grad f_t(theta_t) - alpha lambda' theta_t
```

- Standard SGD with weight decay:

```text
theta_{t+1} = (1 - lambda) theta_t - alpha grad f_t(theta_t)
```

- These match when `lambda' = lambda / alpha`.
- For adaptive methods, the L2 term is also transformed by the adaptive preconditioner, while decoupled weight decay applies parameter shrinkage separately.

## Interpretation
- [[AdamW]] clarifies that weight decay should be separated from Adam's adaptive gradient scaling if the goal is the original weight-decay behavior.

## Common mistakes
- Assuming weight decay and L2 regularization behave identically under every optimizer.
- Calling an L2 penalty inside [[Adam]] "weight decay" without checking whether the decay is decoupled.

## Related concepts
- [[Regularization]]
- [[Adam]]
- [[AdamW]]
- [[Optimization and Training Stability]]

## Related papers
- [[2017 Decoupled Weight Decay Regularization]]

## Source references
- [[2017 Decoupled Weight Decay Regularization]]

## Verification status
- Status: partially verified
- Needs verification: broader regularization theory should be grounded in separate sources.
