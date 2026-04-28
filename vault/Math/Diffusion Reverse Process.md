# Diffusion Reverse Process

## Metadata
- Type: math
- Status: partially verified

## Goal
Define the learned denoising chain used to sample from a DDPM.

## Definitions
- Source: [[2020 Denoising Diffusion Probabilistic Models]].
- The reverse process is the learned joint distribution:

`p_theta(x_0:T) = p(x_T) prod_{t=1}^T p_theta(x_{t-1}|x_t)`.

- The prior is `p(x_T) = N(0,I)`.
- Reverse transitions are Gaussian:

`p_theta(x_{t-1}|x_t) = N(x_{t-1}; mu_theta(x_t,t), Sigma_theta(x_t,t))`.

## Assumptions
- Reverse transitions are parameterized as Gaussian conditionals.
- In the foundational DDPM setup, the model predicts noise `epsilon_theta(x_t,t)` to parameterize the reverse mean.
- Variances are treated as fixed time-dependent constants in the core setup covered here.
- Needs verification: exact variance choices and their effects are implementation details outside this note.

## Derivation
- The reverse model learns to approximate the reverse of the fixed noising chain.
- DDPM parameterizes the mean using a network that predicts the noise added at timestep `t`:

`mu_theta(x_t,t) = 1/sqrt(alpha_t) * (x_t - beta_t/sqrt(1 - alpha_bar_t) * epsilon_theta(x_t,t))`.

- Sampling starts with `x_T ~ N(0,I)`.
- For `t = T, ..., 1`, sample Gaussian noise `z` and compute:

`x_{t-1} = 1/sqrt(alpha_t) * (x_t - (1 - alpha_t)/sqrt(1 - alpha_bar_t) * epsilon_theta(x_t,t)) + sigma_t z`.

- At the final step the paper's algorithm sets `z = 0`.
- Skipped steps: derivation from the Gaussian posterior mean and variance formulas.

## Interpretation
- The reverse process is a denoising chain: each step predicts how to move from a noisier latent to a slightly cleaner one.
- The learned model does not generate a sample in one step; it iteratively denoises.

## Common mistakes
- Confusing the fixed forward transition `q(x_t|x_{t-1})` with the learned reverse transition `p_theta(x_{t-1}|x_t)`.
- Assuming the reverse process exactly inverts the forward process without learning.
- Treating `epsilon_theta` as added noise rather than predicted noise.

## Related concepts
- [[Diffusion Models]]
- [[Diffusion Forward Process]]
- [[Denoising]]
- [[Score Matching]]
- [[2020 Denoising Diffusion Probabilistic Models]]
