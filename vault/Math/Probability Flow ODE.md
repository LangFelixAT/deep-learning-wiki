# Probability Flow ODE

## Metadata
- Type: math
- Status: partially verified

## Goal
Define the deterministic process associated with a score-based SDE.

## Definitions
- Source: [[2021 Score-Based Generative Modeling through SDEs]].
- For a diffusion process, there exists a deterministic ODE with the same marginal densities $p_t(x)$ as the SDE.
- Probability flow ODE:

$$
dx = \left[f(x,t) - \frac{1}{2} g(t)^2 \nabla_x \log p_t(x)\right] dt
$$
- With a learned score model, use $s_{\theta}(x,t) \approx \nabla_x \log p_t(x)$.
- In practice, sampling requires numerically integrating this ODE with finitely many model evaluations.

## Assumptions
- The score is known or accurately estimated.
- The ODE shares marginal distributions with the SDE under the conditions stated in the paper. Needs verification: formal assumptions are not expanded here.

## Derivation
- Start from the forward SDE coefficients $f(x,t)$ and $g(t)$.
- Replace the stochastic reverse process with a deterministic flow that has matching time marginals.
- Substitute the learned score network for the true score.
- [[2022 Elucidating the Design Space of Diffusion-Based Generative Models]] emphasizes that using the ODE for sampling requires numerical integration: choose discrete times, choose an integration scheme, and evaluate the denoiser or score field along the trajectory.
- [[2022 DPM-Solver]] treats the diffusion ODE as semi-linear and designs higher-order solvers that exploit this structure.
- Skipped steps: derivation from the Fokker-Planck equation / probability flow argument.

## Interpretation
- The probability flow ODE gives a deterministic sampling path associated with the stochastic SDE.
- It shares the same marginal distributions $p_t(x)$ as the SDE, but produces deterministic trajectories.
- In EDM's design-space view, sampler quality depends partly on numerical-analysis choices such as step spacing and integration order.
- DPM-Solver emphasizes that higher-order ODE methods can reduce discretization error and therefore reduce the number of required sampling steps.
- The paper notes that it enables deterministic sampling and exact likelihood computation; details are outside this foundational note.

## Common mistakes
- Assuming the ODE path has the same individual trajectories as the SDE.
- Confusing matching marginal distributions with matching sample paths.
- Treating likelihood computation details as part of the basic definition.
- Ignoring discretization error when turning the continuous ODE into a finite-step sampler.

## Related concepts
- [[Forward SDE]]
- [[Reverse-Time SDE]]
- [[Score Matching]]
- [[Diffusion Models]]
- [[Diffusion ODE Solvers]]
- [[2021 Score-Based Generative Modeling through SDEs]]
- [[2022 Elucidating the Design Space of Diffusion-Based Generative Models]]
- [[2022 DPM-Solver]]
