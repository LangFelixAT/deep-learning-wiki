# Diffusion Forward Process

## Metadata
- Type: math
- Status: partially verified

## Goal
Define the fixed noising process used by DDPMs.

## Definitions
- Source: [[2020 Denoising Diffusion Probabilistic Models]].
- `x_0` is a data sample.
- `x_1, ..., x_T` are latent variables with the same dimensionality as `x_0`.
- The forward process is a fixed Markov chain:

`q(x_1:T|x_0) = prod_{t=1}^T q(x_t|x_{t-1})`.

- Gaussian transition:

`q(x_t|x_{t-1}) = N(x_t; sqrt(1 - beta_t)x_{t-1}, beta_t I)`.

- Let `alpha_t = 1 - beta_t` and `alpha_bar_t = prod_{s=1}^t alpha_s`.

## Assumptions
- The forward process uses Gaussian noise.
- The variance schedule `beta_1, ..., beta_T` is fixed in the DDPM implementation described in the paper.
- The process gradually destroys signal so that late `x_T` is close to Gaussian noise.
- Needs verification: exact conditions under which `x_T` is sufficiently close to `N(0,I)` depend on the variance schedule.

## Derivation
- Because each step is Gaussian and linear in `x_{t-1}`, the marginal noised sample at arbitrary timestep has closed form:

`q(x_t|x_0) = N(x_t; sqrt(alpha_bar_t)x_0, (1 - alpha_bar_t)I)`.

- Equivalently, one can sample:

`x_t = sqrt(alpha_bar_t)x_0 + sqrt(1 - alpha_bar_t)epsilon`, with `epsilon ~ N(0,I)`.

- Skipped steps: induction over Gaussian transitions.

## Interpretation
- The forward process is not learned in the DDPM setup covered here.
- It provides supervised-like noisy targets for learning the reverse denoising transitions.

## Common mistakes
- Treating the DDPM forward process as a learned encoder.
- Forgetting that `x_t` has the same dimensionality as the data.
- Confusing `beta_t` with learned reverse-process variance.

## Related concepts
- [[Diffusion Models]]
- [[Diffusion Reverse Process]]
- [[Diffusion ELBO]]
- [[2020 Denoising Diffusion Probabilistic Models]]
