# Diffusion ELBO

## Metadata
- Type: math
- Status: partially verified

## Goal
Describe the variational training objectives used to train diffusion probabilistic models.

## Canonical notation
- `x_0`: clean data sample.
- `x_t`: noisy sample at timestep `t`.
- `x_T`: high-noise terminal state.
- `q(x_t|x_{t-1})`: fixed forward noising transition.
- `q(x_{t-1}|x_t,x_0)`: tractable forward posterior used in DDPM derivations.
- `p_theta(x_{t-1}|x_t)`: learned reverse transition.
- `epsilon`: Gaussian noise sample.
- `epsilon_theta(x_t,t)`: learned DDPM-style noise predictor.
- `alpha_bar_t`: cumulative DDPM noise-schedule product.

## Definitions
- Sources: [[2015 Deep Unsupervised Learning using Nonequilibrium Thermodynamics]], [[2020 Denoising Diffusion Probabilistic Models]].
- DDPMs are latent-variable models with latents `x_1:T`.
- Sign convention matters:
  - the 2015 paper maximizes a lower bound `K` on log likelihood;
  - DDPM minimizes an upper bound `L` on negative log likelihood.
- In DDPM notation, training optimizes a variational bound on negative log likelihood:

`L = E_q[-log p_theta(x_0:T) + log q(x_1:T|x_0)]`.

This satisfies:

`E[-log p_theta(x_0)] <= L`.

- The bound can be rewritten into terms involving:
  - `L_T`: prior matching at the final noised state;
  - `L_{t-1}`: KL terms comparing forward posteriors to learned reverse transitions;
  - `L_0`: decoder/reconstruction term.
- In the 2015 paper, the lower bound `K` is derived by comparing forward and reverse trajectory probabilities and applying Jensen's inequality. It contains negative KL terms plus analytically computable entropy terms.

## Assumptions
- The forward posterior `q(x_{t-1}|x_t,x_0)` is tractable and Gaussian.
- The learned reverse transition `p_theta(x_{t-1}|x_t)` is Gaussian.
- Forward variances are fixed in the DDPM setup summarized here, making `L_T` constant during training.
- Needs verification: details of `L_0` for discrete image likelihoods are outside this foundational note.

## Derivation
- In the 2015 formulation, write the data likelihood as an integral over latent trajectory states, then multiply and divide by the forward trajectory distribution.
- Apply Jensen's inequality to obtain a lower bound on log likelihood.
- In the DDPM formulation, start from the corresponding variational upper bound on negative log likelihood for the latent chain.
- Rewrite the objective so each intermediate term compares:

`q(x_{t-1}|x_t,x_0)` with `p_theta(x_{t-1}|x_t)`.

- Because both distributions are Gaussian, these KL terms can be computed in closed form.
- With the noise-prediction parameterization, the intermediate objective can be written as a weighted mean-squared noise-prediction loss.
- DDPM then uses a simplified objective:

`L_simple(theta) = E_{t,x_0,epsilon}[||epsilon - epsilon_theta(sqrt(alpha_bar_t)x_0 + sqrt(1 - alpha_bar_t)epsilon,t)||^2]`.

- Skipped steps: full algebraic expansion of Eq. (5) and the Gaussian KL calculations.

## Interpretation
- The 2015 and DDPM formulations are closely related variational trajectory objectives, but their signs and notation differ.
- The DDPM objective is variational, but the simplified practical objective is a weighted variant of the variational bound.
- The simplified objective trains the model to denoise samples at randomly selected noise levels.
- Historically, [[2015 Deep Unsupervised Learning using Nonequilibrium Thermodynamics]] frames the objective as learning reverse Markov transitions that make the reverse trajectory match the forward diffusion trajectory.

## Common mistakes
- Confusing the 2015 lower bound on log likelihood with DDPM's upper bound on negative log likelihood.
- Equating the simplified objective exactly with the unweighted variational bound.
- Ignoring the role of the tractable forward posterior `q(x_{t-1}|x_t,x_0)`.
- Treating the diffusion ELBO as identical to the VAE ELBO without accounting for the Markov latent chain.

## Related concepts
- [[ELBO]]
- [[Variational Inference]]
- [[Diffusion Models]]
- [[Diffusion Forward Process]]
- [[Diffusion Reverse Process]]
- [[Score Matching]]
- [[2015 Deep Unsupervised Learning using Nonequilibrium Thermodynamics]]
- [[2020 Denoising Diffusion Probabilistic Models]]
