# Annealed Langevin Dynamics

## Metadata
- Type: math
- Status: partially verified

## Goal
Describe the multi-noise-level sampling procedure used by NCSNs.

## Definitions
- Source: [[2019 Generative Modeling by Estimating Gradients of the Data Distribution]].
- Annealed Langevin dynamics samples using a sequence of noise levels $\sigma_1 > ... > \sigma_L$.
- It uses a noise-conditional score network $s_{\theta}(x, \sigma_i)$.
- Update at noise level $\sigma_i$:

$$
\tilde{x}_t = \tilde{x}_{t-1} + \frac{\alpha_i}{2} s_{\theta}(\tilde{x}_{t-1}, \sigma_i) + \sqrt{\alpha_i} z_t
$$
## Assumptions
- The NCSN estimates scores of Gaussian-perturbed distributions $q_{\sigma_i}(x)$.
- The largest noise level should make modes less isolated and low-density regions easier to traverse.
- The smallest noise level should be close enough to the original data distribution.
- Needs verification: exact schedule choices are implementation details and not covered here.

## Derivation
- Start sampling from an initial noise distribution.
- Run Langevin dynamics using the score for the highest-noise distribution.
- Use the final samples as initialization for the next lower noise level.
- Continue until the smallest noise level is reached.
- Skipped steps: convergence analysis and schedule derivation.

## Interpretation
- Annealing helps move samples through smoother high-noise distributions before refining them near the data distribution.
- This addresses the paper's low-density-region and slow-mixing concerns.

## Common mistakes
- Treating annealed Langevin dynamics as ordinary Langevin dynamics at one fixed noise level.
- Assuming the noise schedule is irrelevant.
- Confusing the sampling noise in Langevin updates with the data perturbation noise levels.

## Related concepts
- [[Langevin Dynamics]]
- [[Noise Conditional Score Networks]]
- [[Score-Based Generative Models]]
- [[Score Matching]]
- [[2019 Generative Modeling by Estimating Gradients of the Data Distribution]]
