# Denoising Diffusion Implicit Models

## Metadata
- Authors: Song, Meng, Ermon
- Year: 2020
- Venue: ICLR 2021
- Link: https://arxiv.org/abs/2010.02502
- Source type: paper
- Status: studied
- Reliability: high

## Scope
This ingest covers only foundational DDIM ideas: relation to DDPM, shared training objective, non-Markovian reverse process, deterministic sampling when $\eta = 0$, faster sampling with fewer steps, and the role of $\epsilon_{\theta}(x_t,t)$.

## One-sentence summary
DDIM generalizes DDPM sampling to a family of non-Markovian generative processes that use the same trained noise-prediction model but can sample deterministically and in fewer steps.

## Problem
DDPMs can produce high-quality samples, but sampling requires simulating a long reverse Markov chain, often with hundreds or thousands of sequential denoising steps.

## Core ideas
- DDIM keeps the DDPM training objective based on predicting Gaussian noise $\epsilon$.
- The paper observes that the DDPM objective depends on the marginals $q(x_t|x_0)$, not uniquely on one Markovian forward joint distribution.
- By choosing non-Markovian inference processes with the same marginals, the paper obtains alternative generative processes without retraining the neural network.
- A parameter controlling sampling stochasticity gives DDPM-like stochastic sampling for one setting and deterministic DDIM sampling when $\eta = 0$.
- Sampling can use a subsequence of timesteps, reducing the number of reverse updates.

## Important equations
DDPM-style marginal noising form:

$$
x_t = \sqrt{\bar{\alpha}_t} x_0 + \sqrt{1 - \bar{\alpha}_t} \epsilon, \quad \epsilon \sim \mathcal{N}(0,I)
$$
Noise-prediction estimate of the clean sample:

$$
\hat{x}_0 = \frac{x_t - \sqrt{1 - \bar{\alpha}_t} \epsilon_{\theta}(x_t,t)}{\sqrt{\bar{\alpha}_t}}
$$
DDIM-style sampling update:

$$
x_{t-1} = \sqrt{\bar{\alpha}_{t-1}} \hat{x}_0 + \sqrt{1 - \bar{\alpha}_{t-1} - \sigma_t^2} \epsilon_{\theta}(x_t,t) + \sigma_t \epsilon
$$
The deterministic DDIM case sets $\sigma_t = 0$, commonly described through $\eta = 0$.

Needs verification: the paper's notation uses $\alpha_t$ for what many later notes call $\bar{\alpha}_t$; this note uses $\bar{\alpha}_t$ for consistency with the existing wiki.

## Claims from source
- Claim from source: DDIMs use the same training procedure as DDPMs.
- Claim from source: non-Markovian diffusion processes can lead to the same DDPM training objective.
- Claim from source: the same trained model can be used with different generative processes by changing the sampling process.
- Claim from source: when the sampling noise coefficient is zero, the generative process is deterministic and defines an implicit probabilistic model.
- Claim from source: DDIMs can generate samples much faster than DDPMs in wall-clock time, with the paper reporting 10x to 50x speedups for comparable quality in its experiments.

## Limitations
- The paper still uses an iterative denoising process; DDIM reduces the number of steps but does not make generation one-shot.
- Faster sampling trades computation against sample quality.
- The deterministic sampler depends on the quality of the trained noise-prediction model.
- This note does not cover interpolation, reconstruction, architecture details, implementation settings, or later diffusion variants.

## My interpretation
DDIM separates the learned denoising model from the exact stochastic reverse chain used by DDPM: once $\epsilon_{\theta}(x_t,t)$ is trained, the sampler can choose a shorter and less stochastic trajectory through the same noise marginals.

## Connections
- [[Diffusion Models]]
- [[Diffusion Reverse Process]]
- [[DDIM Sampling]]
- [[2020 Denoising Diffusion Probabilistic Models]]
- [[2021 Score-Based Generative Modeling through SDEs]]
