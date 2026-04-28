# Langevin Dynamics

## Metadata
- Type: math
- Status: partially verified

## Goal
Describe the sampling procedure that uses a score function to generate samples.

## Definitions
- Source: [[2019 Generative Modeling by Estimating Gradients of the Data Distribution]].
- Langevin dynamics can sample from a density `p(x)` using the score `grad_x log p(x)`.
- Langevin dynamics targets samples from a distribution `p(x)` whose score `grad_x log p(x)` is known or estimated.
- Update:

`tilde_x_t = tilde_x_{t-1} + epsilon/2 * grad_x log p(tilde_x_{t-1}) + sqrt(epsilon) z_t`.

- `z_t ~ N(0,I)`.

## Assumptions
- The score function is available or estimated.
- The source states exact sampling requires limiting conditions such as small step size and many steps, under regularity conditions.
- In practice, the paper assumes the error is negligible when step size is small and the number of steps is large.

## Derivation
- Use the score to move samples toward higher-density regions.
- Add Gaussian noise at each step to maintain stochastic exploration.
- Replace the true score with a learned score network for score-based generative modeling.
- Skipped steps: continuous-time derivation and convergence proof.

## Interpretation
- Langevin dynamics is the sampling half of score-based generative modeling.
- It only needs the score, not the normalized density.

## Common mistakes
- Forgetting the noise term.
- Assuming finite-step Langevin dynamics is exact without qualification.
- Using inaccurate scores in low-density regions and expecting reliable sampling.

## Related concepts
- [[Score Matching]]
- [[Annealed Langevin Dynamics]]
- [[Score-Based Generative Models]]
- [[2019 Generative Modeling by Estimating Gradients of the Data Distribution]]
