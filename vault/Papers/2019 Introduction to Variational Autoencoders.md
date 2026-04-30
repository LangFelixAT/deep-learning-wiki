# An Introduction to Variational Autoencoders

## Metadata
- Authors: Kingma, Welling
- Year: 2019
- Link: https://arxiv.org/abs/1906.02691
- Source type: paper
- Source subtype: tutorial
- Status: studied
- Reliability: high

## Scope
This is a structured tutorial/monograph on variational autoencoders and variational inference.

## One-sentence summary
Kingma and Welling present VAEs as a framework for learning deep latent-variable generative models together with amortized inference models, using the ELBO to handle intractable marginal likelihoods and posteriors.

## Covered sections
- latent variable models
- variational inference
- ELBO
- encoder/decoder structure

## Problem
The foundational problem is learning a probabilistic model $p_{\theta}(x)$ for observed data when the model contains latent variables $z$.

For a latent-variable model, the observed-data probability is:

$$
p_{\theta}(x) = \int p_{\theta}(x,z) dz
$$
In deep latent-variable models, this marginal likelihood is typically intractable, which makes direct maximum-likelihood learning difficult. The posterior

$$
p_{\theta}(z|x) = \frac{p_{\theta}(x,z)}{p_{\theta}(x)}
$$

is also typically intractable because it depends on the same marginal likelihood. The tutorial frames VAEs as a way to make learning and inference computationally tractable by introducing an approximate posterior.

## Core ideas
- A latent-variable generative model defines a joint distribution over observed variables and unobserved variables, commonly factorized as $p_{\theta}(x,z) = p_{\theta}(z)p_{\theta}(x|z)$.
- The inference problem is to recover or approximate the posterior $p_{\theta}(z|x)$ over latent variables given an observation.
- VAEs introduce an inference model, also called an encoder or recognition model, $q_{\phi}(z|x)$, and optimize it to approximate $p_{\theta}(z|x)$.
- The generative model, or decoder, $p_{\theta}(x|z)$ maps latent variables to a distribution over observations.
- The ELBO is optimized instead of the intractable marginal log likelihood. It is both a lower bound on $\log p_{\theta}(x)$ and an objective that improves the generative model and approximate posterior together.
- Sharing one inference model across datapoints is amortized variational inference, avoiding a separate variational optimization loop for each datapoint.

## Important equations
Latent-variable marginal likelihood:

$$
p_{\theta}(x) = \int p_{\theta}(x,z) dz
$$
Common latent-variable factorization:

$$
p_{\theta}(x,z) = p_{\theta}(z)p_{\theta}(x|z)
$$
Posterior identity:

$$
p_{\theta}(z|x) = \frac{p_{\theta}(x,z)}{p_{\theta}(x)}
$$
Approximate posterior objective:

$$
q_{\phi}(z|x) \approx p_{\theta}(z|x)
$$
Example encoder parameterization:

$$
(\mu, \log \sigma) = EncoderNeuralNet_\phi(x)
$$
$$
q_{\phi}(z|x) = \mathcal{N}(z; \mu, \operatorname{diag}(\sigma))
$$
ELBO decomposition:

$$
\log p_{\theta}(x) = L_{\theta,\phi}(x) + D_{KL}(q_{\phi}(z|x) \| p_{\theta}(z|x))
$$
ELBO:

$$
L_{\theta,\phi}(x) = \mathbb{E}_{q_{\phi}(z|x)}[\log p_{\theta}(x,z) - \log q_{\phi}(z|x)]
$$
Lower-bound relation:

$$
L_{\theta,\phi}(x) \le \log p_{\theta}(x)
$$
Dataset ELBO:

$$
L_{\theta,\phi}(D) = \sum_{x in D} L_{\theta,\phi}(x)
$$
## Claims from source
- Claim from source: VAEs provide a computationally efficient way to optimize deep latent-variable models jointly with corresponding inference models using SGD.
- Claim from source: the inference model $q_{\phi}(z|x)$ approximates the intractable posterior $p_{\theta}(z|x)$.
- Claim from source: amortized inference avoids a per-datapoint optimization loop by sharing variational parameters across datapoints.
- Claim from source: the KL divergence $D_{KL}(q_{\phi}(z|x) \| p_{\theta}(z|x))$ is the gap between the ELBO and the marginal log likelihood.
- Claim from source: maximizing the ELBO approximately maximizes the marginal likelihood and minimizes the KL divergence from the approximate posterior to the true posterior.
- Claim from source: in deep latent-variable models, the marginal likelihood and posterior are typically intractable.

## My interpretation

## Connections
- [[ELBO]]
- [[KL Divergence]]
- [[Variational Inference]]
- [[Amortized Variational Inference]]
- [[Variational Autoencoders]]
