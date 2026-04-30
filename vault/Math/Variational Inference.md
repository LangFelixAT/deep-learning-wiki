# Variational Inference

## Metadata
- Type: math
- Status: partially verified

## Goal
Approximate difficult posterior inference with an optimized distribution family.

## Definitions
- Variational inference approximates an intractable posterior distribution with a tractable distribution family.
- In [[2019 Introduction to Variational Autoencoders]], the true posterior is $p_{\theta}(z|x)$ and the approximate posterior, or inference model, is $q_{\phi}(z|x)$.
- The variational parameters are $\phi$.
- Central identity: $\log p_{\theta}(x) = ELBO(q_{\phi}) + D_{KL}(q_{\phi}(z|x) || p_{\theta}(z|x))$.
- In VAEs, the inference model is amortized: one parameterized function $q_{\phi}(z|x)$ is shared across datapoints.

## Assumptions
- The latent variable model defines a tractable joint density $p_{\theta}(x,z)$.
- The marginal likelihood $p_{\theta}(x) = \int p_{\theta}(x,z) dz$ may be intractable.
- The posterior $p_{\theta}(z|x)$ may be intractable because it depends on $p_{\theta}(x)$.
- The approximate posterior family $q_{\phi}(z|x)$ is chosen so expectations and densities needed by the ELBO can be estimated or computed.
- Needs verification: precise support conditions for $q_{\phi}(z|x)$ relative to $p_{\theta}(z|x)$ are not yet fully stated here.

## Derivation
- Introduce $q_{\phi}(z|x)$ to approximate $p_{\theta}(z|x)$.
- Rewrite $\log p_{\theta}(x)$ as the sum of an ELBO and $D_{KL}(q_{\phi}(z|x) || p_{\theta}(z|x))$.
- Since KL divergence is non-negative, maximizing the ELBO maximizes a lower bound on $\log p_{\theta}(x)$.
- In the VAE framing, optimize $\theta$ and $\phi$ jointly so the generative model and inference model improve together.
- Skipped steps: full algebraic derivation of the ELBO identity; see [[ELBO]].

## Interpretation
- Variational inference turns an intractable posterior inference problem into an optimization problem over a chosen approximate posterior family.
- Variational inference turns inference into optimization over distributions $q_{\phi}(z|x)$, where the objective is the [[ELBO]].
- In VAEs, optimizing this objective requires gradient estimators for expectations under $q_{\phi}(z|x)$; for continuous latent variables, [[Reparameterization Trick]] provides one such estimator.
- In DDPMs, variational inference trains a learned reverse Markov chain against a fixed forward noising process; see [[Diffusion ELBO]].
- Amortized variational inference uses a learned inference model to avoid separate per-datapoint optimization.

## Common mistakes
- Treating the approximate posterior $q_{\phi}(z|x)$ as the true posterior.
- Forgetting that the variational family limits how close the approximation can get.
- Confusing inference optimization over $q_{\phi}$ with learning only the generative parameters $\theta$.
- Ignoring support assumptions when using the KL identity.

## Related concepts
- [[ELBO]]
- [[KL Divergence]]
- [[Bayesian Inference]]
- [[Variational Autoencoders]]
- [[Amortized Variational Inference]]
- [[Reparameterization Trick]]
- [[Diffusion ELBO]]
- [[2019 Introduction to Variational Autoencoders]]
- [[2020 Denoising Diffusion Probabilistic Models]]
