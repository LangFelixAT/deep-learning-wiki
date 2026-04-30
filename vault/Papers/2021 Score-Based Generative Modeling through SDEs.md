# Score-Based Generative Modeling through Stochastic Differential Equations

## Metadata
- Authors: Song, Sohl-Dickstein, Kingma, Kumar, Ermon, Poole
- Year: 2021
- Venue: ICLR
- Link: https://arxiv.org/abs/2011.13456
- Source type: paper
- Status: studied
- Reliability: high

## Scope
This ingest covers foundational concepts only: forward SDEs, reverse-time SDEs, time-dependent scores, probability flow ODEs, predictor-corrector sampling, and conceptual links to DDPM and score matching.

## One-sentence summary
Song et al. unify score-based generative models and diffusion probabilistic models through continuous-time SDEs, where a forward SDE maps data to noise and a learned score field defines the reverse generative process.

## Problem
The paper asks how to generalize discrete noise-perturbation generative models into a continuous-time framework that supports flexible sampling and unifies prior score-based and diffusion approaches.

## Core ideas
- A forward SDE gradually transforms data into a tractable prior distribution by injecting noise.
- A reverse-time SDE transforms prior noise back into data, but requires the score $\nabla_x \log p_t(x)$ at each time.
- A time-dependent score network $s_{\theta}(x,t)$ estimates the score field of intermediate perturbed distributions.
- SMLD and DDPM can be viewed as discretizations of different SDEs.
- A probability flow ODE has the same marginal distributions as the SDE but gives a deterministic trajectory.
- Predictor-corrector samplers combine a numerical reverse-SDE step with score-based correction steps such as Langevin dynamics.

## Important equations
Forward SDE:

$$
dx = f(x,t) dt + g(t) dw
$$
Reverse-time SDE:

$$
dx = [f(x,t) - g(t)^2 \nabla_x \log p_t(x)] dt + g(t) d w_bar
$$
Time-dependent score model:

$$
s_{\theta}(x,t) \approx \nabla_x \log p_t(x)
$$
Continuous score matching objective:

$$
E_t[\lambda(t) E_{x(0)} E_{x(t)|x(0)} ||s_{\theta}(x(t),t) - \nabla_{x(t)} \log p_{0t}(x(t)|x(0))||_2^2]
$$
Probability flow ODE:

$$
dx = [f(x,t) - 1/2 g(t)^2 \nabla_x \log p_t(x)] dt
$$
## Claims from source
- Claim from source: a forward SDE can smoothly transform a complex data distribution into a known prior distribution by injecting noise.
- Claim from source: the corresponding reverse-time SDE transforms the prior distribution back into the data distribution by removing noise.
- Claim from source: the reverse-time SDE depends on the time-dependent score of the perturbed data distribution.
- Claim from source: SMLD and DDPM can be treated as discretizations of separate SDEs.
- Claim from source: predictor-corrector samplers combine numerical SDE solvers with score-based MCMC approaches.
- Claim from source: the probability flow ODE has the same marginal probability densities as the SDE.

## Limitations
- Formal SDE existence and uniqueness conditions are not expanded in this note.
- Numerical solvers and predictor-corrector samplers introduce discretization and tuning choices.
- This note does not cover inverse problems, applications, architecture details, experimental results, or detailed likelihood computation.

## My interpretation
The paper turns score-based generation into a continuous-time geometry: learn the score field along a path from data to noise, then integrate either a stochastic reverse process or a deterministic probability-flow process back toward data.

## Connections
- [[Forward SDE]]
- [[Reverse-Time SDE]]
- [[Probability Flow ODE]]
- [[Score Matching]]
- [[Langevin Dynamics]]
- [[Diffusion Models]]
- [[Score-Based Generative Models]]
- [[2020 Denoising Diffusion Probabilistic Models]]
- [[2019 Generative Modeling by Estimating Gradients of the Data Distribution]]
