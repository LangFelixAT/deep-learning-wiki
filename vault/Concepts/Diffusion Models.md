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
- In DDPM, predicting the added noise `epsilon` is closely related to estimating the score of a Gaussian-perturbed distribution. Needs verification: exact scaling and weighting depend on parameterization.
- In [[2021 Score-Based Generative Modeling through SDEs]], diffusion models are interpreted in continuous time with a [[Forward SDE]] from data to noise and a [[Reverse-Time SDE]] from noise back to data.

## Historical development
[[2020 Denoising Diffusion Probabilistic Models]] demonstrates high-quality image synthesis with diffusion probabilistic models and highlights a connection to denoising score matching.

[[2019 Generative Modeling by Estimating Gradients of the Data Distribution]] develops a score-based framework using multiple Gaussian noise levels and annealed Langevin dynamics. At a high level, DDPM's noise-prediction objective is related to denoising score matching, but the exact correspondence depends on parameterization and weighting. Needs verification.

[[2021 Score-Based Generative Modeling through SDEs]] presents SMLD and DDPM as discretizations of different SDEs. In that framing, DDPM is related to a variance-preserving SDE. Needs verification: exact discretization details are not expanded here.

## Basic sampling idea
Sampling starts from `x_T ~ N(0, I)` and repeatedly applies the learned reverse transition until reaching `x_0`.

## Related concepts
- [[ELBO]]
- [[Score Matching]]
- [[Denoising]]
- [[Diffusion Forward Process]]
- [[Diffusion Reverse Process]]
- [[Diffusion ELBO]]
- [[Score-Based Generative Models]]
- [[Noise Conditional Score Networks]]
- [[Annealed Langevin Dynamics]]
- [[Forward SDE]]
- [[Reverse-Time SDE]]
- [[Probability Flow ODE]]
- [[2019 Generative Modeling by Estimating Gradients of the Data Distribution]]
- [[2020 Denoising Diffusion Probabilistic Models]]
- [[2021 Score-Based Generative Modeling through SDEs]]

## Open questions
- Needs verification: how later diffusion literature generalizes the DDPM setup.
