# Diffusion Parameterization

## Metadata
- Type: math
- Status: partially verified

## Goal
Track how diffusion models can be expressed through different but related parameterizations of noise, signal, and network outputs.

## Definitions
- Source: [[2022 Elucidating the Design Space of Diffusion-Based Generative Models]].
- See [[Notation Conventions]] for the wiki-level distinction between DDPM-style $\epsilon_{\theta}$, score-style $s_{\theta}$, $\sigma$, and $\bar{\alpha}_t$.
- EDM describes noisy data distributions as $p(x; \sigma)$, where $\sigma$ is the standard deviation of added Gaussian noise.
- A noisy sample is represented as:

$$
x = y + n, \quad y \sim p_{\mathrm{data}}, \quad n \sim \mathcal{N}(0, \sigma^2 I)
$$
- A denoiser $D(x; \sigma)$ predicts the clean signal from a noisy input at noise level $\sigma$.
- For Gaussian corruption $x = y + n$ with $n ~ \mathcal{N}(0, \sigma^2 I)$, the score and denoiser are related by:

$$
\nabla_x \log p(x; \sigma) = (D(x; \sigma) - x) / \sigma^2
$$
## Assumptions
- The denoiser relation above assumes Gaussian corruption with noise scale $\sigma$.
- The mappings between $\epsilon$ prediction, score prediction, and denoiser prediction require a known noise schedule.
- Source-specific notation must be checked before transferring coefficients between papers.

## Sigma parameterization
- $\sigma$ directly measures corruption strength as a noise standard deviation.
- Sampling moves from high $\sigma$ toward $\sigma = 0$.
- In some formulations, $\sigma$ is parameterized as a function of time $t$; choosing $\sigma(t) = t$ is convenient but non-unique.
- Needs verification: older VP/DDPM notation often uses cumulative products such as $\bar{\alpha}_t$; mapping those to $\sigma$ depends on the chosen scaling convention.

## Relationship between x, noise, and network input
- The network usually does not have to operate on raw $x$ directly.
- EDM writes the denoiser around a raw neural network $F_\theta$:

$$
D_\theta(x; \sigma) = c_skip(\sigma) x + c_out(\sigma) F_\theta(c_in(\sigma) x; c_noise(\sigma))
$$
- $c_in(\sigma)$ scales the noisy input.
- $c_noise(\sigma)$ encodes the noise level as a conditioning input.
- $c_skip(\sigma)$ controls how much of the noisy input bypasses the raw network.
- $c_out(\sigma)$ scales the raw network output.

## Preconditioning idea
- Preconditioning separates the denoiser definition from the raw neural network output.
- The goal is to keep network inputs, targets, and gradient magnitudes better behaved across noise levels.
- The paper's specific EDM coefficients are design choices, not definitions of diffusion models in general.

## Mapping between parameterizations
- DDPM-style $\epsilon_{\theta}$, score prediction, and denoiser prediction can often be converted into one another when the noise schedule is known.
- EDM's framework treats many previous formulations as different choices of schedule, signal scaling, denoiser parameterization, and sampler.
- Needs verification: exact mappings should be checked source-by-source because notation differs across DDPM, DDIM, SDE, and EDM papers.

## Derivation
- Start with Gaussian corruption $x = y + n$.
- Define a denoiser $D(x; \sigma)$ trained to estimate the clean $y$.
- Under Gaussian corruption, use the denoising-score relation to obtain the score from the denoiser.
- Substitute the score or denoiser into an ODE sampler.
- Skipped steps: appendix-level conversions among VP, VE, iDDPM, and DDIM parameterizations.

## Interpretation
Parameterization choices change the coordinates used to train and sample a diffusion model. They can strongly affect optimization and numerical behavior without necessarily changing the underlying denoising problem.

## Common mistakes
- Treating $\epsilon$ prediction, score prediction, and denoiser prediction as unrelated objectives.
- Assuming a coefficient formula from one paper transfers directly to another notation.
- Confusing a sampler schedule with the learned model itself.

## Related concepts
- [[Diffusion Models]]
- [[Diffusion Design Space]]
- [[Probability Flow ODE]]
- [[Score Matching]]
- [[DDIM Sampling]]
- [[2022 Elucidating the Design Space of Diffusion-Based Generative Models]]
- [[Notation Conventions]]
