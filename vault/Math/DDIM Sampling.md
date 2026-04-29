# DDIM Sampling

## Metadata
- Type: math
- Status: partially verified

## Goal
Define the DDIM sampling update and how it differs from DDPM sampling.

## Definitions
- Source: [[2020 Denoising Diffusion Implicit Models]].
- `epsilon_theta(x_t,t)` is the trained DDPM-style noise-prediction network.
- `alpha_bar_t` denotes the cumulative noise schedule term used in the DDPM marginal:

`x_t = sqrt(alpha_bar_t) x_0 + sqrt(1 - alpha_bar_t) epsilon`.

- The clean-sample prediction is:

`x0_hat = (x_t - sqrt(1 - alpha_bar_t) epsilon_theta(x_t,t)) / sqrt(alpha_bar_t)`.

- `eta` controls the stochasticity of the DDIM/DDPM-family sampling update through `sigma_t`.

## Assumptions
- The model was trained with the DDPM noise-prediction objective.
- Sampling uses a chosen decreasing sequence of timesteps.
- The forward marginals `q(x_t|x_0)` match the DDPM marginals.
- Needs verification: this note uses the common later notation `alpha_bar_t`; the DDIM paper writes the corresponding cumulative quantity as `alpha_t`.

## Sampling update
For a step from `t` to `t-1`, DDIM sampling can be written as:

`x_{t-1} = sqrt(alpha_bar_{t-1}) x0_hat + sqrt(1 - alpha_bar_{t-1} - sigma_t^2) epsilon_theta(x_t,t) + sigma_t epsilon`,

where `epsilon ~ N(0,I)` when stochastic noise is used.

For accelerated sampling, the same form is applied over a subsequence of timesteps rather than every `t = T, ..., 1`.

## Role of eta
- `eta` controls `sigma_t`, the amount of new noise injected at each sampling step.
- Larger `eta` makes the process more stochastic.
- `eta = 0` sets `sigma_t = 0`.
- Needs verification: exact `sigma_t(eta)` depends on the chosen timestep subsequence and schedule notation.

## Deterministic eta = 0 case
When `eta = 0`, the sampling update becomes deterministic and no new noise is injected. The trajectory is fixed by the initial latent `x_T`, the predicted `x0_hat`, and the chosen timestep schedule.

## Derivation
- Start from DDPM marginals `q(x_t|x_0)` and a trained noise predictor `epsilon_theta(x_t,t)`.
- Estimate `x_0` from `x_t` and the predicted noise.
- Choose a reverse transition that preserves the same forward marginals while allowing a non-Markovian sampling process.
- Set `sigma_t` through `eta`; when `eta = 0`, remove newly sampled noise from the update.
- Skipped steps: full derivation of the DDIM non-Markovian family and exact `sigma_t` formula.

## Relation to DDPM sampling
- DDPM sampling uses a learned Markov reverse chain with stochastic Gaussian transitions.
- DDIM uses the same trained noise-prediction model but can sample through a non-Markovian generative process.
- For particular variance choices, the generalized process recovers DDPM-like sampling.
- DDIM can skip timesteps, reducing the number of sequential model evaluations.

## Interpretation
DDIM changes the sampler, not the training objective. It reuses `epsilon_theta(x_t,t)` to move along a chosen denoising trajectory, optionally without injecting fresh noise at each step.

Needs verification: deterministic DDIM sampling is closely related to solving a probability flow ODE corresponding to the underlying diffusion process.

## Common mistakes
- Thinking DDIM requires retraining a DDPM model.
- Treating deterministic DDIM sampling as the same process as DDPM sampling.
- Forgetting that fewer sampling steps can trade speed against quality.
- Confusing predicted noise `epsilon_theta(x_t,t)` with newly sampled noise `epsilon`.

## Related concepts
- [[Diffusion Models]]
- [[Diffusion Reverse Process]]
- [[2020 Denoising Diffusion Implicit Models]]
- [[2020 Denoising Diffusion Probabilistic Models]]
