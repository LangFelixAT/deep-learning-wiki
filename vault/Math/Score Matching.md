# Score Matching

## Metadata
- Type: math
- Status: developing

## Goal
Define objectives that learn score functions for probability models.

## Canonical notation
- $p(x)$: probability density over data or perturbed data.
- $\nabla_x \log p(x)$: score function.
- $s_{\theta}(x)$: learned score estimate.
- $s_{\theta}(x,t)$: time-dependent score estimate in diffusion/SDE notes.
- $\sigma$: Gaussian perturbation noise level.
- $q_\sigma(\tilde{x}|x)$: corruption distribution at noise level $\sigma$.
- $\epsilon_{\theta}(x_t,t)$: DDPM noise predictor; related to score estimation through parameterization-dependent scaling.

## Definitions
- Source: [[2019 Generative Modeling by Estimating Gradients of the Data Distribution]].
- The score of a probability density $p(x)$ is $\nabla_x \log p(x)$.
- The score is invariant to the normalization constant: if $p(x) = unnormalized_p(x) / Z$, then $\nabla_x \log p(x) = \nabla_x \log unnormalized_p(x)$.
- A score network $s_{\theta}(x)$ is trained to approximate $\nabla_x \log p_data(x)$.
- In continuous-time formulations, the score becomes time-dependent: $s_{\theta}(x,t) \approx \nabla_x \log p_t(x)$.
- In conditional diffusion models, the score can also be conditioned: $s_{\theta}(x,t,c) \approx \nabla_x \log p_t(x|c)$.
- Conceptually, score matching targets:

$$
1/2 E_{p_data}[||s_{\theta}(x) - \nabla_x \log p_data(x)||_2^2]
$$
- Since $\nabla_x \log p_data(x)$ is unknown, basic score matching uses an objective equivalent up to constants:

$$
E_{p_data(x)}[\operatorname{tr}(\nabla_x s_{\theta}(x)) + 1/2 ||s_{\theta}(x)||_2^2]
$$
- Denoising score matching perturbs data with $q_\sigma(\tilde{x}|x)$ and trains on:

$$
1/2 E_{q_\sigma(\tilde{x}|x)p_data(x)}[||s_{\theta}(\tilde{x}) - \nabla_{\tilde{x}} \log q_\sigma(\tilde{x}|x)||_2^2]
$$
- For Gaussian perturbation $q_\sigma(\tilde{x}|x) = \mathcal{N}(\tilde{x}; x, \sigma^2 I)$, the target is:

$$
\nabla_{\tilde{x}} \log q_\sigma(\tilde{x}|x) = -(\tilde{x} - x) / \sigma^2
$$
- [[2020 Denoising Diffusion Probabilistic Models]] connects the DDPM noise-prediction parameterization to denoising score matching over multiple noise levels.
- [[2021 Score-Based Generative Modeling through SDEs]] uses a time-dependent score model $s_{\theta}(x,t)$ to approximate $\nabla_x \log p_t(x)$ along a continuous noising process.

## Assumptions
- Samples are drawn i.i.d. from an unknown data distribution.
- The score is well-defined where the distribution has suitable support and differentiability.
- Basic score matching can fail or become inconsistent when data lie on a low-dimensional manifold in ambient space.
- Gaussian perturbations are used to make perturbed distributions better behaved for score estimation.
- In the DDPM connection, noise levels are indexed by timestep $t$, and the model predicts the Gaussian noise added to $x_0$.
- In the SDE formulation, $t$ is continuous and indexes the marginal distribution $p_t(x)$.
- For conditional generation, conditioning variable $c$ is treated as given while estimating a conditional score.

## Derivation
- Score matching avoids estimating the normalized density directly and instead learns its log-density gradient.
- The original objective involves the unknown data score, but it can be rewritten into an objective involving $s_{\theta}$ and its input derivatives.
- Denoising score matching avoids the trace term by training against the known score of the corruption distribution.
- With multiple Gaussian noise levels, train $s_{\theta}(x, \sigma_i)$ to approximate $\nabla_x \log q_{\sigma_i}(x)$ for each noise level.
- The NCSN objective combines denoising score matching losses across noise levels:

$$
L(\theta; {\sigma_i}) = (1/L) \sum_i \lambda(\sigma_i) ell(\theta; \sigma_i)
$$
- In the SDE formulation, the discrete noise-level objective becomes a continuous-time objective over $t$:

$$
E_t[\lambda(t) E_{x(0)} E_{x(t)|x(0)} ||s_{\theta}(x(t),t) - \nabla_{x(t)} \log p_{0t}(x(t)|x(0))||_2^2]
$$
- In DDPM, the variational term for the reverse mean can be reparameterized so the model predicts $\epsilon$ from $x_t$.
- The resulting weighted mean-squared noise-prediction objective resembles denoising score matching over multiple noise scales.
- Needs verification: full DDPM equivalence requires checking the weighting and parameterization details from [[2020 Denoising Diffusion Probabilistic Models]].

## Interpretation
- Score matching turns generative modeling into learning a vector field that points toward higher density.
- Denoising score matching learns scores of noise-perturbed distributions, which is useful when the original data distribution is concentrated near a low-dimensional manifold.
- DDPM uses the score-matching connection to motivate a simple denoising objective for training the reverse process.
- The SDE framework treats score estimation as learning a time-indexed vector field along a continuous path from data to noise.
- Classifier-free guidance combines conditional and unconditional score estimates at sampling time.

## Common mistakes
- Confusing the score $\nabla_x \log p(x)$ with the probability density $p(x)$ itself.
- Assuming the basic score of the unperturbed data is always well-defined in ambient space.
- Treating the multi-noise NCSN objective as identical to DDPM training without checking weighting and parameterization.

## Related concepts
- [[Score-Based Generative Models]]
- [[Noise Conditional Score Networks]]
- [[Langevin Dynamics]]
- [[Annealed Langevin Dynamics]]
- [[Diffusion Models]]
- [[Energy-Based Models]]
- [[Denoising]]
- [[Diffusion ELBO]]
- [[Classifier-Free Guidance]]
- [[2019 Generative Modeling by Estimating Gradients of the Data Distribution]]
- [[2020 Denoising Diffusion Probabilistic Models]]
- [[2021 Score-Based Generative Modeling through SDEs]]
- [[2022 Classifier-Free Diffusion Guidance]]

## Verification status
- Status: developing
- Needs verification: DDPM score-equivalence weightings and SDE objective details should be checked before exact conversion formulas are added.
