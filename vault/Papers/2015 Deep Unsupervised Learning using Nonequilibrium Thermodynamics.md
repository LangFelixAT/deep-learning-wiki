# Deep Unsupervised Learning using Nonequilibrium Thermodynamics

## Metadata
- Authors: Jascha Sohl-Dickstein, Eric A. Weiss, Niru Maheswaranathan, Surya Ganguli
- Year: 2015
- Venue: ICML
- Link: https://proceedings.mlr.press/v37/sohl-dickstein15.html
- arXiv: 1503.03585
- Source type: paper
- Status: studied
- Reliability: high
- Added: 2026-04-29

## Scope
This ingest covers only foundational diffusion-model ideas: forward diffusion, learned reverse diffusion, small-step tractability, the high-level variational lower bound, likelihood/evaluation motivation, nonequilibrium-thermodynamics intuition, and historical relation to DDPM.

Excluded: detailed thermodynamic derivations, implementation details, benchmark tables beyond short source claims, modern diffusion extensions, and SDE/score reinterpretations except as brief later connections.

## One-sentence summary
Sohl-Dickstein et al. introduce diffusion probabilistic models as generative Markov chains that learn to reverse a gradual noising process from data to a tractable distribution.

## Why this paper matters
This paper is an early foundation for modern diffusion models: it frames generative modeling as learning the finite-time reversal of a diffusion process that slowly destroys data structure.

## Problem
The paper addresses the tension between flexible probabilistic models and tractable learning, sampling, inference, and probability evaluation.

Flexible models can represent rich data distributions, but evaluating, training, or sampling from them is often expensive because normalization or inference is intractable.

## Background needed
- Markov chains
- [[ELBO]]
- [[KL Divergence]]
- [[Diffusion Forward Process]]
- [[Diffusion Reverse Process]]
- Basic Gaussian transition models

## Core idea
Define a forward diffusion process that gradually transforms the data distribution into a simple tractable distribution, then learn a reverse diffusion process that transforms samples from the tractable distribution back into data-like samples.

The nonequilibrium-thermodynamics intuition is that a slow process between distributions can be easier to reverse and evaluate than a single large transformation.

## Method
- Start with data distribution $q(x^{(0)})$.
- Apply a fixed forward Markov diffusion process for `T` steps.
- Choose the terminal distribution to be analytically tractable, such as a standard Gaussian for continuous data.
- Learn the reverse Markov transitions $p(x^{(t-1)}|x^{(t)})$.
- Train by maximizing a lower bound on model log likelihood.
- Use small diffusion steps so the reverse transition can have the same simple functional form as the forward transition.

## Important equations
Forward trajectory:

$$
q(x^{(0:T)}) = q(x^{(0)}) \prod_{t=1}^T q(x^{(t)}|x^{(t-1)})
$$
Reverse trajectory:

$$
p(x^{(0:T)}) = p(x^{(T)}) \prod_{t=1}^T p(x^{(t-1)}|x^{(t)})
$$
For Gaussian diffusion, the forward transition has the form:

$$
q(x^{(t)}|x^{(t-1)}) = \mathcal{N}(x^{(t)}; \sqrt{1 - \beta_t} x^{(t-1)}, \beta_t I)
$$
The data likelihood under the model is:

$$
p(x^{(0)}) = \int p(x^{(0:T)}) dx^{(1:T)}
$$
The paper evaluates this through the ratio of reverse and forward trajectory probabilities averaged over forward trajectories.

Training maximizes model log likelihood `L`, with a lower bound `K` derived using Jensen's inequality:

$$
L >= K
$$
At a high level, the bound contains KL terms comparing the true forward-process posterior to the learned reverse transition:

$$
D_{KL}(q(x^{(t-1)}|x^{(t)},x^{(0)}) || p(x^{(t-1)}|x^{(t)}))
$$
In the paper's expanded form, this lower bound is a negative sum of such KL terms plus entropy terms from the forward process and terminal distribution. The exact expansion is not reproduced here.

## Results
- Claim from source: the paper demonstrates diffusion probabilistic models on toy, binary, MNIST, CIFAR-10, bark, and dead-leaves datasets.
- Claim from source: the method can sample, evaluate probabilities, and compute conditional/posterior probabilities under the learned model.
- Claim from source: the paper reports competitive or strong log-likelihood results on several evaluated datasets.

Benchmark details are outside this ingest scope.

## Limitations
- The reverse process requires many time steps.
- Learning and sampling cost scale with the number of diffusion steps and the cost of the transition functions.
- The paper predates modern DDPM noise-prediction parameterizations, large-scale image-generation systems, and score/SDE unifications.
- Needs verification: the precise relationship between this lower bound and later DDPM objectives depends on notation and parameterization details.

## Claim from source
- Claim from source: the method uses a Markov chain to gradually convert one distribution into another.
- Claim from source: the probabilistic model is explicitly defined as the endpoint of the learned generative Markov chain.
- Claim from source: because each step in the diffusion chain has an analytically evaluable probability, the full chain can also be analytically evaluated.
- Claim from source: for small diffusion rates, the reversal of Gaussian or binomial diffusion has the same functional form as the forward process.
- Claim from source: estimating small perturbations to a diffusion process is more tractable than explicitly describing a full flexible distribution with a single non-normalized potential function.
- Claim from source: training uses a lower bound on model log likelihood derived with Jensen's inequality.

## My interpretation
This paper gives the pre-DDPM probabilistic backbone of diffusion modeling: rather than directly generating data in one shot, define a long path between data and noise, then learn the reverse path.

The small-step argument is the key intuition: each local reverse step can be simple even if the global data distribution is complex.

## Unclear / Needs verification
- Needs verification: exact mapping between the paper's notation $x^{(t)}$ and later DDPM notation $x_t$ when comparing objectives term-by-term.
- Needs verification: how much of the paper's probability-evaluation claim carries over unchanged to later simplified DDPM training setups.
- Needs verification: full algebraic comparison between the paper's lower bound on log likelihood and DDPM's upper bound on negative log likelihood.

## Connections to concepts
- [[Diffusion Models]]
- [[Diffusion Forward Process]]
- [[Diffusion Reverse Process]]
- [[Diffusion ELBO]]
- [[Generative Modeling Timeline]]
- [[ELBO]]
- [[KL Divergence]]

## Connections to papers
- [[2020 Denoising Diffusion Probabilistic Models]]
- [[2021 Score-Based Generative Modeling through SDEs]]
- [[2022 Elucidating the Design Space of Diffusion-Based Generative Models]]

## Questions
- How exactly does the lower bound in this paper reduce or relate to the DDPM variational bound under later Gaussian parameterizations?
- Which parts of the nonequilibrium thermodynamics framing remain useful for modern diffusion intuition, and which are mostly historical?

## Follow-up reading
- [[2020 Denoising Diffusion Probabilistic Models]]
- [[2021 Score-Based Generative Modeling through SDEs]]
