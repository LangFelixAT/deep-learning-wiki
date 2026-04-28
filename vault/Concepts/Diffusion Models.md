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
- [[2020 Denoising Diffusion Implicit Models]] uses the same trained noise-prediction objective as DDPM but changes the sampling process.
- In [[2021 Score-Based Generative Modeling through SDEs]], diffusion models are interpreted in continuous time with a [[Forward SDE]] from data to noise and a [[Reverse-Time SDE]] from noise back to data.
- [[2022 Elucidating the Design Space of Diffusion-Based Generative Models]] frames diffusion models as separable design choices: parameterization, denoiser preconditioning, sampler, schedule, and training objective.

## Historical development
[[2020 Denoising Diffusion Probabilistic Models]] demonstrates high-quality image synthesis with diffusion probabilistic models and highlights a connection to denoising score matching.

[[2019 Generative Modeling by Estimating Gradients of the Data Distribution]] develops a score-based framework using multiple Gaussian noise levels and annealed Langevin dynamics. At a high level, DDPM's noise-prediction objective is related to denoising score matching, but the exact correspondence depends on parameterization and weighting. Needs verification.

[[2021 Score-Based Generative Modeling through SDEs]] presents SMLD and DDPM as discretizations of different SDEs. In that framing, DDPM is related to a variance-preserving SDE. Needs verification: exact discretization details are not expanded here.

[[2020 Denoising Diffusion Implicit Models]] introduces DDIM sampling, which reuses a DDPM-trained `epsilon_theta(x_t,t)` model with a non-Markovian generative process. It can sample deterministically when `eta = 0` and can use fewer denoising steps for faster generation.

DDIM can be interpreted as selecting a deterministic trajectory consistent with the diffusion marginals. Needs verification: the precise ODE connection depends on the continuous-time formulation and timestep schedule.

[[2022 Elucidating the Design Space of Diffusion-Based Generative Models]] argues that many diffusion formulations are equivalent or closely related after reparameterization. This separates modeling choices, such as what denoiser is learned, from parameterization and sampler choices, such as how noise levels are traversed.

## Basic sampling idea
Sampling starts from `x_T ~ N(0, I)` and repeatedly applies the learned reverse transition until reaching `x_0`.

DDIM changes this basic sampling story by allowing a shorter timestep trajectory and, when `eta = 0`, a deterministic map from the initial `x_T` to the final sample.

The EDM design-space view treats deterministic sampling as numerical integration of an ODE driven by a denoiser or score model.

EDM emphasizes that sampling quality depends strongly on numerical discretization choices, not only on the learned model.

## Related concepts
- [[ELBO]]
- [[Score Matching]]
- [[Denoising]]
- [[Diffusion Forward Process]]
- [[Diffusion Reverse Process]]
- [[Diffusion ELBO]]
- [[Diffusion Parameterization]]
- [[Diffusion Design Space]]
- [[DDIM Sampling]]
- [[Score-Based Generative Models]]
- [[Noise Conditional Score Networks]]
- [[Annealed Langevin Dynamics]]
- [[Forward SDE]]
- [[Reverse-Time SDE]]
- [[Probability Flow ODE]]
- [[2019 Generative Modeling by Estimating Gradients of the Data Distribution]]
- [[2020 Denoising Diffusion Probabilistic Models]]
- [[2020 Denoising Diffusion Implicit Models]]
- [[2021 Score-Based Generative Modeling through SDEs]]
- [[2022 Elucidating the Design Space of Diffusion-Based Generative Models]]

## Open questions
- Needs verification: how later diffusion literature generalizes the DDPM setup.
