# Variational Autoencoders

## Metadata
- Type: concept
- Status: developing

## Short definition
Latent-variable generative model trained using ELBO.

## Intuition
A variational autoencoder combines a probabilistic encoder with a probabilistic decoder. In [[2013 Auto-Encoding Variational Bayes]], the encoder is the recognition model $q_{\phi}(z|x)$, which maps an observed datapoint to a distribution over latent codes. The decoder is $p_{\theta}(x|z)$, which maps a latent code to a distribution over possible observations.

The auto-encoder analogy comes from sampling a latent code from the encoder and scoring how well the decoder explains the original input, while also regularizing the encoder distribution toward the prior.

[[2019 Introduction to Variational Autoencoders]] frames the encoder and decoder as two coupled but independently parameterized models: the inference model approximates the generative model's posterior, while the generative model supplies the latent-variable structure that the inference model learns to invert approximately.

## Mathematical formulation
- Related math: [[ELBO]], [[KL Divergence]]
- Source formulation: maximize an ELBO of the form $-D_{KL}(q_{\phi}(z|x) || p_{\theta}(z)) + E_q[\log p_{\theta}(x|z)]$.
- This objective is a lower bound on the marginal log likelihood $\log p_{\theta}(x)$.
- General tutorial formulation: $L_{\theta,\phi}(x) = E_{q_{\phi}(z|x)}[\log p_{\theta}(x,z) - \log q_{\phi}(z|x)]$.

## Role of latent variables
The latent variable `z` is unobserved and is interpreted in the paper as a code or latent representation. The learned encoder approximates the intractable posterior over this code for a given datapoint.

In the 2019 tutorial, latent variables make the marginal model $p_{\theta}(x)$ flexible, but they also introduce the integral $p_{\theta}(x) = \int p_{\theta}(x,z) dz$, which is typically intractable in deep latent-variable models.

## Relation to ELBO
VAEs in this paper are trained by optimizing the [[ELBO]] using the reparameterization trick. The ELBO supplies both the reconstruction-like likelihood term and the KL regularization term.

The tutorial emphasizes the identity $\log p_{\theta}(x) = ELBO + D_{KL}(q_{\phi}(z|x) || p_{\theta}(z|x))$: improving the ELBO both tightens the bound and improves the approximate posterior, within the chosen inference family.

## Training with reparameterization
In the 2019 tutorial, VAE training uses stochastic gradient optimization of the ELBO. The difficulty is that the ELBO expectation is over $q_{\phi}(z|x)$, which depends on the encoder parameters $\phi$.

For continuous latent variables, [[Reparameterization Trick]] rewrites latent samples as $z = g_\phi(\epsilon, x)$, with noise $\epsilon$ drawn from a distribution independent of $\phi$. This makes the sampled latent code part of a differentiable computation graph, so gradients can be backpropagated through the encoder and decoder.

## Historical development
[[2013 Auto-Encoding Variational Bayes]] introduces the AEVB algorithm and gives the neural-network encoder/decoder example that the paper calls the variational auto-encoder.

## Related concepts
- [[ELBO]]
- [[KL Divergence]]
- [[Variational Inference]]
- [[Amortized Variational Inference]]
- [[Reparameterization Trick]]

## Related papers
- [[2013 Auto-Encoding Variational Bayes]]
- [[2019 Introduction to Variational Autoencoders]]

## Open questions
- Needs verification: how this paper's framing relates historically to Rezende, Mohamed, and Wierstra 2014 and later VAE terminology.
