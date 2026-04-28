# Probability Flow ODE

## Metadata
- Type: math
- Status: partially verified

## Goal
Define the deterministic process associated with a score-based SDE.

## Definitions
- Source: [[2021 Score-Based Generative Modeling through SDEs]].
- For a diffusion process, there exists a deterministic ODE with the same marginal densities `p_t(x)` as the SDE.
- Probability flow ODE:

`dx = [f(x,t) - 1/2 g(t)^2 grad_x log p_t(x)] dt`.

- With a learned score model, use `s_theta(x,t) approx grad_x log p_t(x)`.

## Assumptions
- The score is known or accurately estimated.
- The ODE shares marginal distributions with the SDE under the conditions stated in the paper. Needs verification: formal assumptions are not expanded here.

## Derivation
- Start from the forward SDE coefficients `f(x,t)` and `g(t)`.
- Replace the stochastic reverse process with a deterministic flow that has matching time marginals.
- Substitute the learned score network for the true score.
- Skipped steps: derivation from the Fokker-Planck equation / probability flow argument.

## Interpretation
- The probability flow ODE gives a deterministic sampling path associated with the stochastic SDE.
- It shares the same marginal distributions `p_t(x)` as the SDE, but produces deterministic trajectories.
- The paper notes that it enables deterministic sampling and exact likelihood computation; details are outside this foundational note.

## Common mistakes
- Assuming the ODE path has the same individual trajectories as the SDE.
- Confusing matching marginal distributions with matching sample paths.
- Treating likelihood computation details as part of the basic definition.

## Related concepts
- [[Forward SDE]]
- [[Reverse-Time SDE]]
- [[Score Matching]]
- [[Diffusion Models]]
- [[2021 Score-Based Generative Modeling through SDEs]]
