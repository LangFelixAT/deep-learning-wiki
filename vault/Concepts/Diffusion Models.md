# Diffusion Models

## Metadata
- Type: concept
- Status: developing

## Short definition
Generative models that learn to reverse a gradual noising process.

## Intuition
In [[2020 Denoising Diffusion Probabilistic Models]], a diffusion model starts with data `x_0`, applies a fixed forward process that gradually adds Gaussian noise, and learns a reverse process that denoises from `x_T` back to a sample resembling data.

## Mathematical formulation
- Related math: [[Diffusion Forward Process]], [[Diffusion Reverse Process]], [[Diffusion ELBO]], [[Score Matching]], [[ELBO]]
- Forward process: `q(x_t|x_{t-1})` adds Gaussian noise according to a variance schedule.
- Reverse process: `p_theta(x_{t-1}|x_t)` is a learned Gaussian transition.
- Training uses a variational bound and, in DDPM, a simplified noise-prediction objective.

## Historical development
[[2020 Denoising Diffusion Probabilistic Models]] demonstrates high-quality image synthesis with diffusion probabilistic models and highlights a connection to denoising score matching.

## Basic sampling idea
Sampling starts from `x_T ~ N(0, I)` and repeatedly applies the learned reverse transition until reaching `x_0`.

## Related concepts
- [[ELBO]]
- [[Score Matching]]
- [[Denoising]]
- [[Diffusion Forward Process]]
- [[Diffusion Reverse Process]]
- [[Diffusion ELBO]]
- [[2020 Denoising Diffusion Probabilistic Models]]

## Open questions
- Needs verification: how later diffusion literature generalizes the DDPM setup.
