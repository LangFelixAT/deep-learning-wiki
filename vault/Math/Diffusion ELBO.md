# Diffusion ELBO

## Metadata
- Type: math
- Status: partially verified

## Goal
Describe the variational training objective used by DDPMs.

## Definitions
- Source: [[2020 Denoising Diffusion Probabilistic Models]].
- DDPMs are latent-variable models with latents `x_1:T`.
- Training optimizes a variational bound on negative log likelihood:

`L = E_q[-log p_theta(x_0:T) + log q(x_1:T|x_0)]`.

This satisfies:

`E[-log p_theta(x_0)] <= L`.

- The bound can be rewritten into terms involving:
  - `L_T`: prior matching at the final noised state;
  - `L_{t-1}`: KL terms comparing forward posteriors to learned reverse transitions;
  - `L_0`: decoder/reconstruction term.

## Assumptions
- The forward posterior `q(x_{t-1}|x_t,x_0)` is tractable and Gaussian.
- The learned reverse transition `p_theta(x_{t-1}|x_t)` is Gaussian.
- Forward variances are fixed in the DDPM setup summarized here, making `L_T` constant during training.
- Needs verification: details of `L_0` for discrete image likelihoods are outside this foundational note.

## Derivation
- Start from the usual variational bound on negative log likelihood for the latent chain.
- Rewrite the objective so each intermediate term compares:

`q(x_{t-1}|x_t,x_0)` with `p_theta(x_{t-1}|x_t)`.

- Because both distributions are Gaussian, these KL terms can be computed in closed form.
- With the noise-prediction parameterization, the intermediate objective can be written as a weighted mean-squared noise-prediction loss.
- DDPM then uses a simplified objective:

`L_simple(theta) = E_{t,x_0,epsilon}[||epsilon - epsilon_theta(sqrt(alpha_bar_t)x_0 + sqrt(1 - alpha_bar_t)epsilon,t)||^2]`.

- Skipped steps: full algebraic expansion of Eq. (5) and the Gaussian KL calculations.

## Interpretation
- The DDPM objective is variational, but the simplified practical objective is a weighted variant of the variational bound.
- The simplified objective trains the model to denoise samples at randomly selected noise levels.

## Common mistakes
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
- [[2020 Denoising Diffusion Probabilistic Models]]
