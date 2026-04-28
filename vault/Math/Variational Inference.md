# Variational Inference

## Metadata
- Type: math
- Status: partially verified

## Goal
Approximate difficult posterior inference with an optimized distribution family.

## Definitions
- Variational inference approximates an intractable posterior distribution with a tractable distribution family.
- In [[2019 Introduction to Variational Autoencoders]], the true posterior is `p_theta(z|x)` and the approximate posterior, or inference model, is `q_phi(z|x)`.
- The variational parameters are `phi`.
- Central identity: `log p_theta(x) = ELBO(q_phi) + D_KL(q_phi(z|x) || p_theta(z|x))`.
- In VAEs, the inference model is amortized: one parameterized function `q_phi(z|x)` is shared across datapoints.

## Assumptions
- The latent variable model defines a tractable joint density `p_theta(x,z)`.
- The marginal likelihood `p_theta(x) = integral p_theta(x,z) dz` may be intractable.
- The posterior `p_theta(z|x)` may be intractable because it depends on `p_theta(x)`.
- The approximate posterior family `q_phi(z|x)` is chosen so expectations and densities needed by the ELBO can be estimated or computed.
- Needs verification: precise support conditions for `q_phi(z|x)` relative to `p_theta(z|x)` are not yet fully stated here.

## Derivation
- Introduce `q_phi(z|x)` to approximate `p_theta(z|x)`.
- Rewrite `log p_theta(x)` as the sum of an ELBO and `D_KL(q_phi(z|x) || p_theta(z|x))`.
- Since KL divergence is non-negative, maximizing the ELBO maximizes a lower bound on `log p_theta(x)`.
- In the VAE framing, optimize `theta` and `phi` jointly so the generative model and inference model improve together.
- Skipped steps: full algebraic derivation of the ELBO identity; see [[ELBO]].

## Interpretation
- Variational inference turns an intractable posterior inference problem into an optimization problem over a chosen approximate posterior family.
- Variational inference turns inference into optimization over distributions `q_phi(z|x)`, where the objective is the [[ELBO]].
- In VAEs, optimizing this objective requires gradient estimators for expectations under `q_phi(z|x)`; for continuous latent variables, [[Reparameterization Trick]] provides one such estimator.
- Amortized variational inference uses a learned inference model to avoid separate per-datapoint optimization.

## Common mistakes
- Needs development.

## Related concepts
- [[ELBO]]
- [[KL Divergence]]
- [[Bayesian Inference]]
- [[Variational Autoencoders]]
- [[Amortized Variational Inference]]
- [[Reparameterization Trick]]
- [[2019 Introduction to Variational Autoencoders]]
