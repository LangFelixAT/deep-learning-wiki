# Diffusion Reverse Process

## Metadata
- Type: math
- Status: partially verified

## Goal
Define the learned denoising chain used to generate samples by reversing a diffusion process.

## Definitions
- Sources: [[2015 Deep Unsupervised Learning using Nonequilibrium Thermodynamics]], [[2020 Denoising Diffusion Probabilistic Models]].
- The reverse process is the learned joint distribution:

$$
p_{\theta}(x_0:T) = p(x_T) \prod_{t=1}^T p_{\theta}(x_{t-1}|x_t)
$$
- In the 2015 paper, the reverse trajectory is written:

$$
p(x^(0:T)) = p(x^(T)) \prod_{t=1}^T p(x^(t-1)|x^(t))
$$
- The prior is $p(x_T) = \mathcal{N}(0,I)$.
- Reverse transitions are Gaussian:

$$
p_{\theta}(x_{t-1}|x_t) = \mathcal{N}(x_{t-1}; \mu_\theta(x_t,t), \sigma_\theta(x_t,t))
$$
- [[2020 Denoising Diffusion Implicit Models]] keeps the DDPM-trained noise predictor but defines a non-Markovian generative process for sampling.

## Assumptions
- Reverse transitions are parameterized as Gaussian conditionals.
- The 2015 paper argues that when diffusion steps are small, the reversal of a Gaussian or binomial diffusion process has the same functional form as the forward process.
- In the foundational DDPM setup, the model predicts noise $\epsilon_{\theta}(x_t,t)$ to parameterize the reverse mean.
- Variances are treated as fixed time-dependent constants in the core setup covered here.
- Needs verification: exact variance choices and their effects are implementation details outside this note.

## Derivation
- The reverse model learns to approximate the reverse of the fixed noising chain.
- DDPM parameterizes the mean using a network that predicts the noise added at timestep $t$:

$$
\mu_{\theta}(x_t,t) = 1/\sqrt(\alpha_t) * (x_t - \beta_t/\sqrt(1 - \bar{\alpha}_t) * \epsilon_{\theta}(x_t,t))
$$
- Sampling starts with $x_T ~ \mathcal{N}(0,I)$.
- For $t = T, ..., 1$, sample Gaussian noise $z$ and compute:

$$
x_{t-1} = 1/\sqrt(\alpha_t) * (x_t - (1 - \alpha_t)/\sqrt(1 - \bar{\alpha}_t) * \epsilon_{\theta}(x_t,t)) + \sigma_t z
$$
- At the final step the paper's algorithm sets $z = 0$.
- Skipped steps: derivation from the Gaussian posterior mean and variance formulas.

## Interpretation
- The reverse process is a denoising chain: each step predicts how to move from a noisier latent to a slightly cleaner one.
- The learned model does not generate a sample in one step; it iteratively denoises.
- The 2015 framing explains why many small steps are useful: the global data distribution can be complex while each local reverse transition remains simple.
- In DDPM, the reverse process is modeled as a Markov chain over adjacent timesteps.
- In DDIM, sampling can follow a non-Markovian process and can become deterministic when the sampling noise coefficient is zero.

## Common mistakes
- Confusing the fixed forward transition $q(x_t|x_{t-1})$ with the learned reverse transition $p_{\theta}(x_{t-1}|x_t)$.
- Assuming the reverse process exactly inverts the forward process without learning.
- Treating $\epsilon_{\theta}$ as added noise rather than predicted noise.

## Related concepts
- [[Diffusion Models]]
- [[Diffusion Forward Process]]
- [[Denoising]]
- [[Score Matching]]
- [[DDIM Sampling]]
- [[2015 Deep Unsupervised Learning using Nonequilibrium Thermodynamics]]
- [[2020 Denoising Diffusion Probabilistic Models]]
- [[2020 Denoising Diffusion Implicit Models]]
