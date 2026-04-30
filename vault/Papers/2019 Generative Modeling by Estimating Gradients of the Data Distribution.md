# Generative Modeling by Estimating Gradients of the Data Distribution

## Metadata
- Authors: Yang Song, Stefano Ermon
- Year: 2019
- Venue: NeurIPS
- Link: https://arxiv.org/abs/1907.05600
- Source type: paper
- Status: studied
- Reliability: high

## Scope
This ingest covers the foundational score-based framework: score definition, score matching, manifold/low-density issues, Gaussian perturbations, NCSNs, annealed Langevin dynamics, and a high-level relation to DDPM.

## One-sentence summary
Song and Ermon propose score-based generative modeling: estimate gradients of noise-perturbed data densities at multiple noise levels, then generate samples using annealed Langevin dynamics.

## Problem
The paper studies how to generate samples from an unknown data distribution without explicitly learning a normalized density or using adversarial training.

A naive score-based approach faces two major obstacles:
- if data lie on a low-dimensional manifold, the ambient-space score $\nabla_x \log p_{\mathrm{data}}(x)$ may be undefined or score matching may be inconsistent;
- low-density regions have few data samples, making score estimation inaccurate and Langevin dynamics mixing slow.

## Core ideas
- Learn the score function $\nabla_x \log p_{\mathrm{data}}(x)$ directly with score matching.
- Use Langevin dynamics to sample using only an estimated score function.
- Perturb data with multiple Gaussian noise levels so the perturbed distributions have broader support and fill low-density regions.
- Train one noise-conditional score network $s_{\theta}(x, \sigma)$ to estimate scores for all noise levels.
- Sample with annealed Langevin dynamics, starting from a high-noise score and gradually moving to lower-noise scores near the data distribution.

## Important equations
Score function:

$$
s_p(x) = \nabla_x \log p(x)
$$
Basic score matching target:

$$
\frac{1}{2}\mathbb{E}_{p_{\mathrm{data}}}\left[\left\|s_{\theta}(x) - \nabla_x \log p_{\mathrm{data}}(x)\right\|_2^2\right]
$$
Equivalent score matching objective up to a constant:

$$
\mathbb{E}_{p_{\mathrm{data}}(x)}\left[\operatorname{tr}(\nabla_x s_{\theta}(x)) + \frac{1}{2}\left\|s_{\theta}(x)\right\|_2^2\right]
$$
Denoising score matching objective for perturbation $q_\sigma(\tilde{x}|x)$:

$$
\frac{1}{2}\mathbb{E}_{q_\sigma(\tilde{x}|x)p_{\mathrm{data}}(x)}\left[\left\|s_{\theta}(\tilde{x}) - \nabla_{\tilde{x}} \log q_\sigma(\tilde{x}|x)\right\|_2^2\right]
$$
Gaussian perturbation:

$$
q_\sigma(\tilde{x}|x) = \mathcal{N}(\tilde{x}; x, \sigma^2 I)
$$
Gaussian denoising target:

$$
\nabla_{\tilde{x}} \log q_\sigma(\tilde{x}|x) = -\frac{\tilde{x} - x}{\sigma^2}
$$
Noise conditional score network target:

$$
s_{\theta}(x, \sigma_i) \approx \nabla_x \log q_{\sigma_i}(x)
$$
Multi-noise objective:

$$
L(\theta; \{\sigma_i\}) = \frac{1}{L} \sum_i \lambda(\sigma_i) \ell(\theta; \sigma_i)
$$
Langevin dynamics:

$$
\tilde{x}_t = \tilde{x}_{t-1} + \frac{\epsilon}{2} \nabla_x \log p(\tilde{x}_{t-1}) + \sqrt{\epsilon} z_t
$$
Annealed Langevin update:

$$
\tilde{x}_t = \tilde{x}_{t-1} + \frac{\alpha_i}{2} s_{\theta}(\tilde{x}_{t-1}, \sigma_i) + \sqrt{\alpha_i} z_t
$$
## Claims from source
- Claim from source: the score is the gradient of the log-density with respect to the input.
- Claim from source: score matching can train a score network to estimate the data score without first estimating the data density.
- Claim from source: data on low-dimensional manifolds can make the score undefined in the ambient space and make score matching inconsistent.
- Claim from source: low-density regions hinder score estimation and slow Langevin dynamics mixing.
- Claim from source: perturbing data with Gaussian noise at multiple magnitudes helps address these two difficulties.
- Claim from source: NCSNs jointly estimate scores for multiple noise-perturbed distributions.
- Claim from source: annealed Langevin dynamics starts with high-noise scores and gradually anneals to low-noise scores for sampling.
- Claim from source: the method requires no adversarial training, no MCMC sampling during training, and no special model architectures for tractability.

## Limitations
- The framework depends on choosing useful noise levels and a sampling schedule.
- Sampling uses iterative Langevin dynamics rather than a single forward pass.
- The paper notes architecture design matters for high-quality image generation, but this note does not ingest architecture details.
- This note does not cover detailed experimental tables, implementation settings, or later extensions.

## My interpretation
This paper shifts generative modeling from density estimation to vector-field estimation: learn where probability density increases, then use a stochastic sampler to move noise toward data-like regions.

## Connections
- [[Score Matching]]
- [[Score-Based Generative Models]]
- [[Noise Conditional Score Networks]]
- [[Langevin Dynamics]]
- [[Annealed Langevin Dynamics]]
- [[Denoising]]
- [[Diffusion Models]]
- [[Energy-Based Models]]
