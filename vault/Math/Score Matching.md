# Score Matching

## Metadata
- Type: math
- Status: developing

## Goal
Define objectives that learn score functions for probability models.

## Definitions
- Source: [[2019 Generative Modeling by Estimating Gradients of the Data Distribution]].
- The score of a probability density `p(x)` is `grad_x log p(x)`.
- The score is invariant to the normalization constant: if `p(x) = unnormalized_p(x) / Z`, then `grad_x log p(x) = grad_x log unnormalized_p(x)`.
- A score network `s_theta(x)` is trained to approximate `grad_x log p_data(x)`.
- In continuous-time formulations, the score becomes time-dependent: `s_theta(x,t) approx grad_x log p_t(x)`.
- Conceptually, score matching targets:

`1/2 E_{p_data}[||s_theta(x) - grad_x log p_data(x)||_2^2]`.

- Since `grad_x log p_data(x)` is unknown, basic score matching uses an objective equivalent up to constants:

`E_{p_data(x)}[tr(grad_x s_theta(x)) + 1/2 ||s_theta(x)||_2^2]`.

- Denoising score matching perturbs data with `q_sigma(tilde_x|x)` and trains on:

`1/2 E_{q_sigma(tilde_x|x)p_data(x)}[||s_theta(tilde_x) - grad_{tilde_x} log q_sigma(tilde_x|x)||_2^2]`.

- For Gaussian perturbation `q_sigma(tilde_x|x) = N(tilde_x; x, sigma^2 I)`, the target is:

`grad_{tilde_x} log q_sigma(tilde_x|x) = -(tilde_x - x) / sigma^2`.

- [[2020 Denoising Diffusion Probabilistic Models]] connects the DDPM noise-prediction parameterization to denoising score matching over multiple noise levels.
- [[2021 Score-Based Generative Modeling through SDEs]] uses a time-dependent score model `s_theta(x,t)` to approximate `grad_x log p_t(x)` along a continuous noising process.

## Assumptions
- Samples are drawn i.i.d. from an unknown data distribution.
- The score is well-defined where the distribution has suitable support and differentiability.
- Basic score matching can fail or become inconsistent when data lie on a low-dimensional manifold in ambient space.
- Gaussian perturbations are used to make perturbed distributions better behaved for score estimation.
- In the DDPM connection, noise levels are indexed by timestep `t`, and the model predicts the Gaussian noise added to `x_0`.
- In the SDE formulation, `t` is continuous and indexes the marginal distribution `p_t(x)`.

## Derivation
- Score matching avoids estimating the normalized density directly and instead learns its log-density gradient.
- The original objective involves the unknown data score, but it can be rewritten into an objective involving `s_theta` and its input derivatives.
- Denoising score matching avoids the trace term by training against the known score of the corruption distribution.
- With multiple Gaussian noise levels, train `s_theta(x, sigma_i)` to approximate `grad_x log q_{sigma_i}(x)` for each noise level.
- The NCSN objective combines denoising score matching losses across noise levels:

`L(theta; {sigma_i}) = (1/L) sum_i lambda(sigma_i) ell(theta; sigma_i)`.

- In the SDE formulation, the discrete noise-level objective becomes a continuous-time objective over `t`:

`E_t[lambda(t) E_{x(0)} E_{x(t)|x(0)} ||s_theta(x(t),t) - grad_{x(t)} log p_{0t}(x(t)|x(0))||_2^2]`.

- In DDPM, the variational term for the reverse mean can be reparameterized so the model predicts `epsilon` from `x_t`.
- The resulting weighted mean-squared noise-prediction objective resembles denoising score matching over multiple noise scales.
- Needs verification: full DDPM equivalence requires checking the weighting and parameterization details from [[2020 Denoising Diffusion Probabilistic Models]].

## Interpretation
- Score matching turns generative modeling into learning a vector field that points toward higher density.
- Denoising score matching learns scores of noise-perturbed distributions, which is useful when the original data distribution is concentrated near a low-dimensional manifold.
- DDPM uses the score-matching connection to motivate a simple denoising objective for training the reverse process.
- The SDE framework treats score estimation as learning a time-indexed vector field along a continuous path from data to noise.

## Common mistakes
- Confusing the score `grad_x log p(x)` with the probability density `p(x)` itself.
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
- [[2019 Generative Modeling by Estimating Gradients of the Data Distribution]]
- [[2020 Denoising Diffusion Probabilistic Models]]
- [[2021 Score-Based Generative Modeling through SDEs]]
