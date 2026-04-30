# Denoising Diffusion Probabilistic Models

## Metadata
- Authors: Ho, Jain, Abbeel
- Year: 2020
- Venue: NeurIPS
- Link: https://arxiv.org/abs/2006.11239
- Source type: paper
- Status: studied
- Reliability: high

## Scope
This ingest covers only foundational DDPM material: forward noising, reverse denoising, variational training, denoising score-matching connection, and basic sampling.

## One-sentence summary
Ho, Jain, and Abbeel present diffusion models as latent-variable Markov chains trained by a variational bound to reverse a fixed Gaussian noising process, with a simplified denoising objective connected to score matching.

## Problem
The paper studies how to train diffusion probabilistic models to generate data samples by learning a finite-time reverse Markov chain.

The central problem is that the model must learn reverse transitions that undo a known forward process which gradually destroys signal by adding Gaussian noise to data.

## Core ideas
- Define a fixed forward process $q(x_1:T|x_0)$ that gradually adds Gaussian noise to data.
- Define a learned reverse process $p_{\theta}(x_0:T)$ that starts from Gaussian noise and samples backward toward data.
- Train the reverse process with a variational bound on negative log likelihood.
- Use tractable Gaussian posteriors from the forward process to rewrite the bound into KL terms.
- Parameterize the reverse-process mean by predicting the injected noise $\epsilon$.
- This noise-prediction objective resembles denoising score matching over multiple noise levels.
- Sampling starts from $x_T ~ \mathcal{N}(0, I)$ and repeatedly applies learned reverse transitions.

## Important equations
Reverse-process latent-variable model:

$$
p_{\theta}(x_0:T) = p(x_T) \prod_{t=1}^T p_{\theta}(x_{t-1}|x_t)
$$
Reverse transition:

$$
p_{\theta}(x_{t-1}|x_t) = \mathcal{N}(x_{t-1}; \mu_\theta(x_t,t), \sigma_\theta(x_t,t))
$$
Forward noising process:

$$
q(x_1:T|x_0) = \prod_{t=1}^T q(x_t|x_{t-1})
$$
Forward transition:

$$
q(x_t|x_{t-1}) = \mathcal{N}(x_t; \sqrt(1 - \beta_t) x_{t-1}, \beta_t I)
$$
Closed-form noisy sample:

$$
q(x_t|x_0) = \mathcal{N}(x_t; \sqrt(\bar{\alpha}_t) x_0, (1 - \bar{\alpha}_t) I)
$$
Variational bound on negative log likelihood:

$$
L = E_q[-\log p_{\theta}(x_{0:T}) + \log q(x_{1:T}|x_0)], \quad E[-\log p_{\theta}(x_0)] \le L
$$
Forward-process posterior used in the rewritten bound:

$$
q(x_{t-1}|x_t,x_0) = \mathcal{N}(x_{t-1}; \mu_tilde_t(x_t,x_0), \beta_tilde_t I)
$$
Noise-prediction parameterization:

$$
\mu_{\theta}(x_t,t) = 1/\sqrt(\alpha_t) * (x_t - \beta_t / \sqrt(1 - \bar{\alpha}_t) * \epsilon_{\theta}(x_t,t))
$$
Simplified training objective:

$$
L_{simple}(\theta) = E_{t,x_0,\epsilon}[||\epsilon - \epsilon_{\theta}(\sqrt(\bar{\alpha}_t)x_0 + \sqrt(1 - \bar{\alpha}_t)\epsilon, t)||^2]
$$
Basic sampling step:

$$
x_{t-1} = 1/\sqrt(\alpha_t) * (x_t - (1 - \alpha_t)/\sqrt(1 - \bar{\alpha}_t) * \epsilon_{\theta}(x_t,t)) + \sigma_t z
$$
## Claims from source
- Claim from source: diffusion models are parameterized Markov chains trained using variational inference to produce samples matching data after finite time.
- Claim from source: reverse transitions are learned to reverse a diffusion process that gradually adds noise until signal is destroyed.
- Claim from source: with small Gaussian noising steps, conditional Gaussian reverse transitions are sufficient for a simple neural-network parameterization.
- Claim from source: their parameterization reveals an equivalence with denoising score matching over multiple noise levels during training and annealed Langevin dynamics during sampling.
- Claim from source: their simplified objective is a weighted variant of the variational bound and gives better sample quality in their experiments.
- Claim from source: their models achieve high sample quality, but their log likelihoods are not competitive with other likelihood-based models.

## Limitations
- The paper reports that sample quality is strong while log likelihood is not competitive with other likelihood-based generative models.
- The foundational sampling procedure requires many reverse-process steps.
- Needs verification: the exact equivalence to denoising score matching depends on the chosen reverse-process parameterization and weighting.
- This note does not cover implementation details, detailed experimental tables, or later diffusion extensions.

## My interpretation
DDPMs can be read as variational latent-variable models where the encoder-like forward process is fixed and destructive, and learning focuses on a decoder-like reverse denoising chain.

## Connections
- [[Diffusion Models]]
- [[Diffusion Forward Process]]
- [[Diffusion Reverse Process]]
- [[Diffusion ELBO]]
- [[Denoising]]
- [[Score Matching]]
- [[ELBO]]
- [[Variational Inference]]
