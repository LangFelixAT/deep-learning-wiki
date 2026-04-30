# Adam

## Metadata
- Type: math
- Status: partially verified
- Last reviewed: 2026-04-30

## Goal
Define the Adam optimizer update rule and the role of its first moment, second raw moment, and bias-correction terms.

## Canonical notation
- `theta_t`: parameter vector after timestep `t`.
- `g_t`: stochastic gradient at timestep `t`.
- `m_t`: biased first moment estimate.
- `v_t`: biased second raw moment estimate.
- `hat_m_t`: bias-corrected first moment estimate.
- `hat_v_t`: bias-corrected second raw moment estimate.
- `alpha`: learning rate or stepsize.
- `beta_1`: exponential decay rate for the first moment estimate.
- `beta_2`: exponential decay rate for the second raw moment estimate.
- `epsilon`: small numerical constant in the denominator.

## Definitions
- Stochastic gradient: `g_t = grad_theta f_t(theta_{t-1})`, where `f_t` is a stochastic objective realization such as a minibatch loss.
- First moment estimate: an exponential moving average of gradients.
- Second raw moment estimate: an exponential moving average of elementwise squared gradients.
- Bias correction: division by `(1 - beta_1^t)` and `(1 - beta_2^t)` to counteract zero initialization of moving averages.
- Adaptive elementwise update: each coordinate is scaled by its own estimate of recent gradient magnitude.

## Assumptions
- The objective is differentiable with respect to parameters.
- Gradients are obtained stochastically, for example from minibatches or other noisy objective evaluations.
- Vector squares, square roots, and divisions are elementwise.
- `beta_1, beta_2` are in `[0, 1)`.
- `epsilon` is positive and prevents division by zero or extreme numerical instability.

## Main result
Adam updates parameters as:

```text
m_t = beta_1 m_{t-1} + (1 - beta_1) g_t
v_t = beta_2 v_{t-1} + (1 - beta_2) g_t^2
hat_m_t = m_t / (1 - beta_1^t)
hat_v_t = v_t / (1 - beta_2^t)
theta_t = theta_{t-1} - alpha * hat_m_t / (sqrt(hat_v_t) + epsilon)
```

## Derivation
- Start from stochastic gradient descent:

```text
theta_t = theta_{t-1} - alpha * g_t
```

- Replace the raw gradient direction with a smoothed first moment estimate:

```text
m_t = beta_1 m_{t-1} + (1 - beta_1) g_t
```

- Track the elementwise scale of recent gradients with a second raw moment estimate:

```text
v_t = beta_2 v_{t-1} + (1 - beta_2) g_t^2
```

- Because `m_0 = 0` and `v_0 = 0`, early estimates are biased toward zero. Correct the initialization bias:

```text
hat_m_t = m_t / (1 - beta_1^t)
hat_v_t = v_t / (1 - beta_2^t)
```

- Use the corrected first moment as the update direction and the corrected second raw moment as an elementwise scale estimate:

```text
theta_t = theta_{t-1} - alpha * hat_m_t / (sqrt(hat_v_t) + epsilon)
```

- Skipped steps: the source paper's convergence proof and regret-bound derivation are not expanded here.

## Interpretation
- `m_t` behaves like a momentum-like moving average: it reduces variance in the update direction by smoothing recent gradients.
- `v_t` estimates recent squared gradient scale per coordinate: coordinates with larger recent gradient magnitudes receive smaller effective steps.
- Bias correction matters most early in training and when `beta_1` or `beta_2` are close to 1, because zero initialization otherwise pulls the moment estimates downward.
- `alpha` controls the global step scale, while `beta_1` and `beta_2` control memory in the first and second moment estimates.
- Adam can be viewed as [[Gradient Descent]] with momentum-like smoothing and coordinatewise adaptive scaling.

## Alternative formulations
- The source notes a computationally reordered update using a time-dependent effective stepsize `alpha_t`, but the clearer algorithmic form above is the canonical form for this wiki.
- AdaMax is an Adam variant discussed in the source, but it is outside this note's current scope.

## Common mistakes
- Treating `v_t` as a centered variance. In Adam, `v_t` is a second raw moment estimate of squared gradients.
- Forgetting bias correction when reasoning about early timesteps.
- Treating `epsilon` as a learning-rate parameter. It is primarily a small denominator-stabilizing constant.
- Assuming AdamW is just Adam plus ordinary L2 regularization. Needs verification from the AdamW source.

## Related concepts
- [[Gradient Descent]]
- [[Weight Decay]]
- [[AdamW]]
- [[Optimization and Training Stability]]

## Related papers
- [[2014 Adam]]

## Source references
- [[2014 Adam]]

## Verification status
- Status: partially verified
- Needs verification: details of AdamW, convergence edge cases, and later optimizer comparisons require separate sources.
