# Reparameterization Trick

## Metadata
- Type: math
- Status: partially verified

## Goal
Explain how VAEs estimate gradients of ELBO expectations when the expectation is taken over $q_{\phi}(z|x)$, a distribution that depends on variational parameters.

## Definitions
- Source: [[2019 Introduction to Variational Autoencoders]], Sections 2.3-2.5.
- The VAE ELBO contains an expectation over the inference model $q_{\phi}(z|x)$.
- The stochastic gradient problem is harder for $\phi$ because $q_{\phi}(z|x)$ itself depends on $\phi$.
- Reparameterization writes a random sample $z \sim q_{\phi}(z|x)$ as a deterministic differentiable function of parameter-free noise:

$$
z = g_\phi(\epsilon, x), \quad \epsilon \sim p(\epsilon)
$$
- Factorized Gaussian example:

$$
\epsilon \sim \mathcal{N}(0, I)
$$

$$
(\mu, \log \sigma) = EncoderNeuralNet_\phi(x)
$$

$$
z = \mu + \sigma \epsilon
$$

## Assumptions
- The latent variable $z$ is continuous.
- The encoder and generative model are differentiable.
- The distribution $q_{\phi}(z|x)$ admits a differentiable reparameterization using noise whose distribution does not depend on $\phi$ or $x$.
- Not all distributions admit a simple reparameterization; the trick applies directly to specific families such as Gaussians.
- The ELBO terms $\log p_{\theta}(x,z)$ and $\log q_{\phi}(z|x)$ can be evaluated or estimated for the sampled $z$.
- Needs verification: exact regularity conditions for interchanging gradient and expectation are not fully stated here.

## Derivation
- Start with the single-datapoint ELBO:

$$
L_{\theta,\phi}(x) = \mathbb{E}_{q_{\phi}(z|x)}[\log p_{\theta}(x,z) - \log q_{\phi}(z|x)]
$$
- Gradients with respect to $\theta$ are comparatively direct because $\theta$ appears inside the integrand.
- Gradients with respect to $\phi$ are harder because the sampling distribution $q_{\phi}(z|x)$ depends on $\phi$.
- Reparameterize samples from $q_{\phi}(z|x)$ as $z = g_\phi(\epsilon, x)$ with $\epsilon \sim p(\epsilon)$.
- Rewrite the expectation over $q_{\phi}(z|x)$ as an expectation over $p(\epsilon)$.

$$
\mathbb{E}_{q_{\phi}(z|x)}[f(z)] = \mathbb{E}_{p(\epsilon)}[f(g_\phi(\epsilon, x))]
$$
- Form a Monte Carlo estimator:

$$
\epsilon \sim p(\epsilon)
$$

$$
z = g_\phi(\epsilon, x)
$$

$$
\tilde{L}_{\theta,\phi}(x) = \log p_{\theta}(x,z) - \log q_{\phi}(z|x)
$$
- Because $z$ is now expressed as a differentiable function of $\phi$, gradients of the expectation with respect to $\phi$ can be estimated by backpropagation through the transformed sample.
- Skipped steps: full measure-change derivation and log-density/Jacobian details.

## Interpretation
- Claim from source: for continuous latent variables and differentiable encoder/generative model, the reparameterization trick lets the ELBO be differentiated with respect to both $\theta$ and $\phi$.
- Claim from source: the resulting stochastic estimate allows ELBO optimization with SGD.
- My interpretation: the trick externalizes randomness into $\epsilon$, so the random node no longer blocks gradient flow through the latent sample.
- Needs verification: alternative gradient estimators such as score-function estimators exist, but they are often discussed as having higher variance than reparameterization-style estimators.

## Common mistakes
- Treating samples from $q_{\phi}(z|x)$ as if gradients can automatically pass through them without reparameterization.
- Forgetting that the basic trick described here assumes continuous latent variables.
- Confusing the sampled latent variable $z$ with the noise variable $\epsilon$.
- Assuming every approximate posterior has a simple reparameterization. Needs verification for each distribution family.

## Related concepts
- [[ELBO]]
- [[Variational Inference]]
- [[Variational Autoencoders]]
- [[Amortized Variational Inference]]
- [[2019 Introduction to Variational Autoencoders]]
