# ELBO

## Metadata
- Type: math
- Status: partially verified

## Goal
Understand the evidence lower bound as a general variational inference objective, including its use in VAEs and diffusion models.

See [[Notation Conventions]] for wiki-level notation for `p_theta(x,z)`, `p_theta(z|x)`, and `q_phi(z|x)`.

## Definitions
- In general variational inference, the ELBO is an objective optimized over an approximate posterior family.
- In [[2013 Auto-Encoding Variational Bayes]], the lower bound for one datapoint is written as `L(theta, phi; x^(i))`.
- The approximate posterior is `q_phi(z|x)`.
- The true posterior is `p_theta(z|x)`.
- The joint model is `p_theta(x,z) = p_theta(z)p_theta(x|z)` in the paper's main latent-variable setup.
- The paper uses the decomposition `log p_theta(x^(i)) = D_KL(q_phi(z|x^(i)) || p_theta(z|x^(i))) + L(theta, phi; x^(i))`.
- In [[2019 Introduction to Variational Autoencoders]], the ELBO is defined as `L_{theta,phi}(x) = E_{q_phi(z|x)}[log p_theta(x,z) - log q_phi(z|x)]`.
- The tutorial presents the ELBO as the marginal log likelihood minus the posterior-approximation KL: `L_{theta,phi}(x) = log p_theta(x) - D_KL(q_phi(z|x) || p_theta(z|x))`.

## Assumptions
- Dataset examples are assumed i.i.d. in the main AEVB setting.
- Each datapoint has an associated continuous latent variable `z`.
- The prior `p_theta(z)` and likelihood `p_theta(x|z)` come from parametric families with densities differentiable almost everywhere with respect to `theta` and `z`.
- The posterior `p_theta(z|x)` and marginal likelihood may be intractable.
- For the SGVB estimator, samples from `q_phi(z|x)` must be expressible as `z = g_phi(epsilon, x)` for auxiliary noise `epsilon ~ p(epsilon)`, under the paper's stated reparameterization conditions.
- Needs verification: exact regularity conditions are described informally in the paper as mild differentiability conditions; formal conditions should be checked before treating this as a theorem.
- In the 2019 tutorial setup, the observed datapoints are assumed i.i.d. when forming a dataset ELBO as a sum of per-datapoint ELBOs.
- The foundational derivation assumes an inference model `q_phi(z|x)` whose support and expectations make the displayed KL and ELBO terms well-defined. Needs verification: support conditions should be made explicit in a fuller derivation.

## Derivation
- Start with `log p_theta(x^(i))`.
- Add an approximate posterior `q_phi(z|x^(i))`.
- Decompose the marginal log likelihood into a KL divergence from `q_phi(z|x^(i))` to the true posterior plus a residual term `L(theta, phi; x^(i))`.
- Since KL divergence is non-negative, the residual term is a lower bound.
- Rewrite the lower bound as an expectation under `q_phi(z|x)`: `E_q[-log q_phi(z|x) + log p_theta(x,z)]`.
- Split the joint term into prior and likelihood to obtain the reconstruction-plus-prior form: `-D_KL(q_phi(z|x) || p_theta(z)) + E_q[log p_theta(x|z)]`.
- Apply the reparameterization `z = g_phi(epsilon, x)` so the Monte Carlo lower-bound estimator is differentiable with respect to `phi`.
- Skipped steps: full algebraic expansion of the KL decomposition and the Gaussian closed-form KL; see [[2013 Auto-Encoding Variational Bayes]] and [[KL Divergence]].
- The 2019 tutorial derives the same decomposition by inserting `q_phi(z|x)` into `log p_theta(x)` and separating the result into the ELBO plus `D_KL(q_phi(z|x) || p_theta(z|x))`.

## Optimization in practice
- In VAEs, the individual-datapoint ELBO and its gradient are generally intractable, so stochastic estimators are used.
- Gradients with respect to variational parameters are difficult because the ELBO expectation is over `q_phi(z|x)`, which depends on `phi`.
- For continuous latent variables, [[Reparameterization Trick]] rewrites `z ~ q_phi(z|x)` as `z = g_phi(epsilon, x)` with `epsilon ~ p(epsilon)`.
- This lets the ELBO estimator be represented as a differentiable computation graph and optimized with stochastic gradient methods.

## Interpretation
- The ELBO is not specific to VAEs; it is the variational objective that turns posterior inference into optimization when the marginal likelihood or posterior is intractable.
- In the VAE example, the ELBO has a term that rewards explaining `x` through sampled latent variables and a KL term that keeps `q_phi(z|x)` close to the prior.
- The paper connects this objective to auto-encoders: the likelihood term corresponds to a reconstruction term, while the KL term acts as a variational regularizer.
- In the 2019 tutorial, the ELBO's tightness is controlled by how close the approximate posterior is to the true posterior in KL divergence.
- Maximizing the ELBO jointly improves the generative model and the inference model in the tutorial's framing.
- In DDPMs, the variational bound is applied to a Markov chain of latent variables and can be rewritten into Gaussian KL terms; see [[Diffusion ELBO]].

## Common mistakes
- Needs development.

## Related concepts
- [[KL Divergence]]
- [[Variational Inference]]
- [[Variational Autoencoders]]
- [[Reparameterization Trick]]
- [[Diffusion ELBO]]
- [[2013 Auto-Encoding Variational Bayes]]
- [[2019 Introduction to Variational Autoencoders]]
- [[2020 Denoising Diffusion Probabilistic Models]]

## Verification status
- Status: partially verified
