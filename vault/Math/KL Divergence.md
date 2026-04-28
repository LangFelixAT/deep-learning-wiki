# KL Divergence

## Metadata
- Type: math
- Status: partially verified

## Goal
Measure difference between probability distributions.

## Definitions
- In [[2013 Auto-Encoding Variational Bayes]], `D_KL(q_phi(z|x) || p_theta(z|x))` measures the divergence between the approximate posterior and the true posterior.
- The ELBO decomposition relies on KL non-negativity.
- The VAE objective often uses `D_KL(q_phi(z|x) || p_theta(z))`, the divergence from the approximate posterior to the prior.
- General definition: D_KL(q(z) || p(z)) = E_q[log q(z) - log p(z)]
- In [[2019 Introduction to Variational Autoencoders]], `D_KL(q_phi(z|x) || p_theta(z|x))` is the gap between `log p_theta(x)` and the ELBO.

## Assumptions
- The distributions being compared must be valid probability distributions over the same latent variable.
- In the paper's Gaussian VAE example, the prior is `N(0, I)` and the approximate posterior is a diagonal Gaussian.
- Needs verification: support conditions for finite KL should be stated explicitly in a fuller math note.
- For the ELBO identity, `q_phi(z|x)` and `p_theta(z|x)` are distributions over the same latent variable conditioned on the same observation.

## Derivation
- In the ELBO decomposition, the marginal log likelihood is rewritten as a KL term plus a lower-bound term.
- Non-negativity of KL gives the lower-bound inequality.
- For the Gaussian VAE example, the paper uses an analytic expression for `-D_KL(q_phi(z|x) || p_theta(z))`, avoiding Monte Carlo estimation of that term.
- Skipped steps: full Gaussian KL derivation from Appendix B.
- The 2019 tutorial also relates maximum likelihood to minimizing `D_KL(q_D(x) || p_theta(x))`, where `q_D(x)` is the empirical data distribution.
- The tutorial relates ELBO maximization to minimizing a joint-space KL between an empirical-plus-inference distribution and the model joint distribution. Needs verification before expanding beyond the foundational identity.

## Interpretation
- In the VAE objective from the paper, the KL-to-prior term discourages the encoder distribution from drifting too far from the latent prior.
- This makes the latent space usable for generation by sampling from the prior and decoding.
- In the ELBO identity, a smaller posterior KL means a tighter lower bound on the marginal log likelihood.

## Common mistakes
- Needs development.

## Related concepts
- [[ELBO]]
- [[Variational Inference]]
- [[Variational Autoencoders]]
- [[2013 Auto-Encoding Variational Bayes]]
- [[2019 Introduction to Variational Autoencoders]]

## Verification status
- Status: partially verified
