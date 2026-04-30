# ELBO

## Metadata
- Type: math
- Status: partially verified

## Goal
Understand the evidence lower bound as a general variational inference objective, including its use in VAEs and diffusion models.

See [[Notation Conventions]] for wiki-level notation for $p_{\theta}(x,z)$, $p_{\theta}(z|x)$, and $q_{\phi}(z|x)$.

## Canonical notation
- $x$: observed datapoint.
- $z$: latent variable.
- $p_{\theta}(x,z)$: generative joint distribution.
- $p_{\theta}(z|x)$: true posterior under the generative model.
- $q_{\phi}(z|x)$: approximate posterior or inference model.
- $ELBO$: lower bound on $\log p_{\theta}(x)$.
- $D_{KL}(q_{\phi}(z|x) || p_{\theta}(z|x))$: posterior-approximation gap between the ELBO and marginal log likelihood.

## Definitions
- In general variational inference, the ELBO is an objective optimized over an approximate posterior family.
- In [[2013 Auto-Encoding Variational Bayes]], the lower bound for one datapoint is written as $L(\theta, \phi; x^{(i)})$.
- The approximate posterior is $q_{\phi}(z|x)$.
- The true posterior is $p_{\theta}(z|x)$.
- The joint model is $p_{\theta}(x,z) = p_{\theta}(z)p_{\theta}(x|z)$ in the paper's main latent-variable setup.
- The paper uses the decomposition $\log p_{\theta}(x^{(i)}) = D_{KL}(q_{\phi}(z|x^{(i)}) || p_{\theta}(z|x^{(i)})) + L(\theta, \phi; x^{(i)})$.
- In [[2019 Introduction to Variational Autoencoders]], the ELBO is defined as $L_{\theta,\phi}(x) = E_{q_{\phi}(z|x)}[\log p_{\theta}(x,z) - \log q_{\phi}(z|x)]$.
- The tutorial presents the ELBO as the marginal log likelihood minus the posterior-approximation KL: $L_{\theta,\phi}(x) = \log p_{\theta}(x) - D_{KL}(q_{\phi}(z|x) || p_{\theta}(z|x))$.

## Assumptions
- Dataset examples are assumed i.i.d. in the main AEVB setting.
- Each datapoint has an associated continuous latent variable $z$.
- The prior $p_{\theta}(z)$ and likelihood $p_{\theta}(x|z)$ come from parametric families with densities differentiable almost everywhere with respect to $\theta$ and $z$.
- The posterior $p_{\theta}(z|x)$ and marginal likelihood may be intractable.
- For the SGVB estimator, samples from $q_{\phi}(z|x)$ must be expressible as $z = g_\phi(\epsilon, x)$ for auxiliary noise $\epsilon ~ p(\epsilon)$, under the paper's stated reparameterization conditions.
- Needs verification: exact regularity conditions are described informally in the paper as mild differentiability conditions; formal conditions should be checked before treating this as a theorem.
- In the 2019 tutorial setup, the observed datapoints are assumed i.i.d. when forming a dataset ELBO as a sum of per-datapoint ELBOs.
- The foundational derivation assumes an inference model $q_{\phi}(z|x)$ whose support and expectations make the displayed KL and ELBO terms well-defined. Needs verification: support conditions should be made explicit in a fuller derivation.

## Derivation
- Start with $\log p_{\theta}(x^{(i)})$.
- Add an approximate posterior $q_{\phi}(z|x^{(i)})$.
- Decompose the marginal log likelihood into a KL divergence from $q_{\phi}(z|x^{(i)})$ to the true posterior plus a residual term $L(\theta, \phi; x^{(i)})$.
- Since KL divergence is non-negative, the residual term is a lower bound.
- Rewrite the lower bound as an expectation under $q_{\phi}(z|x)$: $E_{q}[-\log q_{\phi}(z|x) + \log p_{\theta}(x,z)]$.
- Split the joint term into prior and likelihood to obtain the reconstruction-plus-prior form: $-D_{KL}(q_{\phi}(z|x) || p_{\theta}(z)) + E_{q}[\log p_{\theta}(x|z)]$.
- Apply the reparameterization $z = g_\phi(\epsilon, x)$ so the Monte Carlo lower-bound estimator is differentiable with respect to $\phi$.
- Skipped steps: full algebraic expansion of the KL decomposition and the Gaussian closed-form KL; see [[2013 Auto-Encoding Variational Bayes]] and [[KL Divergence]].
- The 2019 tutorial derives the same decomposition by inserting $q_{\phi}(z|x)$ into $\log p_{\theta}(x)$ and separating the result into the ELBO plus $D_{KL}(q_{\phi}(z|x) || p_{\theta}(z|x))$.

## Optimization in practice
- In VAEs, the individual-datapoint ELBO and its gradient are generally intractable, so stochastic estimators are used.
- Gradients with respect to variational parameters are difficult because the ELBO expectation is over $q_{\phi}(z|x)$, which depends on $\phi$.
- For continuous latent variables, [[Reparameterization Trick]] rewrites $z ~ q_{\phi}(z|x)$ as $z = g_\phi(\epsilon, x)$ with $\epsilon ~ p(\epsilon)$.
- This lets the ELBO estimator be represented as a differentiable computation graph and optimized with stochastic gradient methods.

## Interpretation
- The ELBO is not specific to VAEs; it is the variational objective that turns posterior inference into optimization when the marginal likelihood or posterior is intractable.
- In the VAE example, the ELBO has a term that rewards explaining $x$ through sampled latent variables and a KL term that keeps $q_{\phi}(z|x)$ close to the prior.
- The paper connects this objective to auto-encoders: the likelihood term corresponds to a reconstruction term, while the KL term acts as a variational regularizer.
- In the 2019 tutorial, the ELBO's tightness is controlled by how close the approximate posterior is to the true posterior in KL divergence.
- Maximizing the ELBO jointly improves the generative model and the inference model in the tutorial's framing.
- In DDPMs, the variational bound is applied to a Markov chain of latent variables and can be rewritten into Gaussian KL terms; see [[Diffusion ELBO]].

## Common mistakes
- Treating the ELBO as VAE-specific rather than a general variational objective.
- Forgetting that ELBO tightness depends on the posterior KL term.
- Mixing the VAE latent-variable ELBO with the diffusion Markov-chain ELBO without checking which latent variables are being bounded.

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
- Needs verification: full Gaussian closed-form KL and support conditions should be expanded in a focused derivation pass.
