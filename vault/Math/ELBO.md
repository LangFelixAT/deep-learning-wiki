# ELBO

## Metadata
- Type: math
- Status: partially verified

## Goal
Understand the evidence lower bound used in variational inference, VAEs, and diffusion models.

## Definitions
- In [[2013 Auto-Encoding Variational Bayes]], the lower bound for one datapoint is written as `L(theta, phi; x^(i))`.
- The approximate posterior is `q_phi(z|x)`.
- The true posterior is `p_theta(z|x)`.
- The joint model is `p_theta(x,z) = p_theta(z)p_theta(x|z)` in the paper's main latent-variable setup.
- The paper uses the decomposition `log p_theta(x^(i)) = D_KL(q_phi(z|x^(i)) || p_theta(z|x^(i))) + L(theta, phi; x^(i))`.

## Assumptions
- Dataset examples are assumed i.i.d. in the main AEVB setting.
- Each datapoint has an associated continuous latent variable `z`.
- The prior `p_theta(z)` and likelihood `p_theta(x|z)` come from parametric families with densities differentiable almost everywhere with respect to `theta` and `z`.
- The posterior `p_theta(z|x)` and marginal likelihood may be intractable.
- For the SGVB estimator, samples from `q_phi(z|x)` must be expressible as `z = g_phi(epsilon, x)` for auxiliary noise `epsilon ~ p(epsilon)`, under the paper's stated reparameterization conditions.
- Needs verification: exact regularity conditions are described informally in the paper as mild differentiability conditions; formal conditions should be checked before treating this as a theorem.

## Derivation
- Start with `log p_theta(x^(i))`.
- Add an approximate posterior `q_phi(z|x^(i))`.
- Decompose the marginal log likelihood into a KL divergence from `q_phi(z|x^(i))` to the true posterior plus a residual term `L(theta, phi; x^(i))`.
- Since KL divergence is non-negative, the residual term is a lower bound.
- Rewrite the lower bound as an expectation under `q_phi(z|x)`: `E_q[-log q_phi(z|x) + log p_theta(x,z)]`.
- Split the joint term into prior and likelihood to obtain the reconstruction-plus-prior form: `-D_KL(q_phi(z|x) || p_theta(z)) + E_q[log p_theta(x|z)]`.
- Apply the reparameterization `z = g_phi(epsilon, x)` so the Monte Carlo lower-bound estimator is differentiable with respect to `phi`.
- Skipped steps: full algebraic expansion of the KL decomposition and the Gaussian closed-form KL; see [[2013 Auto-Encoding Variational Bayes]] and [[KL Divergence]].

## Interpretation
- In the VAE example, the ELBO has a term that rewards explaining `x` through sampled latent variables and a KL term that keeps `q_phi(z|x)` close to the prior.
- The paper connects this objective to auto-encoders: the likelihood term corresponds to a reconstruction term, while the KL term acts as a variational regularizer.

## Common mistakes
- Needs development.

## Related concepts
- [[KL Divergence]]
- [[Variational Inference]]
- [[Variational Autoencoders]]
- [[2013 Auto-Encoding Variational Bayes]]

## Verification status
- Status: partially verified
