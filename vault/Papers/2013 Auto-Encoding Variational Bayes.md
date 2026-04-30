# Auto-Encoding Variational Bayes

## Metadata
- Authors: Kingma, Welling
- Year: 2013
- Link: https://arxiv.org/abs/1312.6114
- Source type: paper
- Status: studied
- Reliability: high

## One-sentence summary
Kingma and Welling introduce SGVB and AEVB: a stochastic variational inference method for directed probabilistic models with continuous latent variables, using a reparameterized variational lower bound that can be optimized with stochastic gradients.

## Problem
The paper asks how to perform efficient approximate inference and learning in directed probabilistic models when:
- latent variables are continuous and unobserved;
- the marginal likelihood $p_{\theta}(x) = \int p_{\theta}(z)p_{\theta}(x|z) dz$ is intractable;
- the posterior $p_{\theta}(z|x)$ is intractable;
- mean-field VB expectations may also be intractable;
- the dataset is large enough that batch optimization or expensive per-datapoint sampling is impractical.

The target tasks are approximate ML or MAP estimation of model parameters, approximate posterior inference for latent variables, and approximate marginal inference for observed variables.

## Core idea
Introduce an approximate posterior, or recognition model, $q_{\phi}(z|x)$, and optimize it jointly with the generative model $p_{\theta}(x,z)$.

The key technical idea is to rewrite samples from $q_{\phi}(z|x)$ as deterministic transformations of parameter-free noise:

$$
z = g_\phi(\epsilon, x), \quad \epsilon \sim p(\epsilon)
$$
This reparameterization gives a differentiable Monte Carlo estimator of the variational lower bound, allowing optimization of both $\theta$ and $\phi$ using stochastic gradient methods.

## Method
The method starts from the variational lower bound for each datapoint:

$$
\log p_{\theta}(x^{(i)}) = D_{KL}(q_{\phi}(z|x^{(i)}) \| p_{\theta}(z|x^{(i)})) + L(\theta, \phi; x^{(i)})
$$
Because the KL term is non-negative, $L(\theta, \phi; x^{(i)})$ is a lower bound on the marginal log likelihood.

The paper then:
- defines a recognition model $q_{\phi}(z|x)$ as an approximation to the true posterior;
- reparameterizes samples from $q_{\phi}(z|x)$ using auxiliary noise;
- builds Monte Carlo estimators of the lower bound and its gradients;
- scales the estimator to minibatches;
- applies the framework to a neural-network encoder and decoder, producing the variational auto-encoder example.

In the VAE example, the prior is $p_{\theta}(z) = \mathcal{N}(0, I)$, the approximate posterior is diagonal Gaussian, and the encoder outputs the mean and standard deviation used in $z = \mu + \sigma \epsilon$.

## Important equations
Variational decomposition:

$$
\log p_{\theta}(x^{(i)}) = D_{KL}(q_{\phi}(z|x^{(i)}) \| p_{\theta}(z|x^{(i)})) + L(\theta, \phi; x^{(i)})
$$
Lower bound:

$$
L(\theta, \phi; x^{(i)}) = \mathbb{E}_{q_{\phi}(z|x)}[-\log q_{\phi}(z|x) + \log p_{\theta}(x,z)]
$$
Alternative lower bound form:

$$
L(\theta, \phi; x^{(i)}) = -D_{KL}(q_{\phi}(z|x^{(i)}) \| p_{\theta}(z)) + \mathbb{E}_{q_{\phi}(z|x^{(i)})}[\log p_{\theta}(x^{(i)}|z)]
$$
Reparameterization:

$$
z = g_\phi(\epsilon, x), \quad \epsilon \sim p(\epsilon)
$$
Generic SGVB estimator:

$$
L_A \approx (1/L) \sum_l [\log p_{\theta}(x^{(i)}, z^{(i,l)}) - \log q_{\phi}(z^{(i,l)}|x^{(i)})]
$$
Lower-variance estimator when the KL term is analytic:

$$
L_B \approx -D_{KL}(q_{\phi}(z|x^{(i)}) \| p_{\theta}(z)) + \frac{1}{L} \sum_l \log p_{\theta}(x^{(i)}|z^{(i,l)})
$$
Minibatch estimator:

$$
L(\theta, \phi; X) \approx (N/M) \sum_i L(\theta, \phi; x^{(i)})
$$
Gaussian VAE reparameterization:

$$
z^{(i,l)} = \mu^{(i)} + \sigma^{(i)} \epsilon^{(l)}, \quad \epsilon^{(l)} \sim \mathcal{N}(0, I)
$$
## Claims from source
- The paper claims the SGVB estimator can be optimized straightforwardly with standard stochastic gradient methods.
- The paper claims AEVB is efficient for i.i.d. datasets with continuous latent variables per datapoint because it learns an approximate inference model instead of running an expensive iterative inference procedure per datapoint.
- The paper claims the reparameterized estimator is differentiable with respect to the variational parameters under the stated mild differentiability conditions.
- The paper claims that, in their experiments, AEVB converged faster and reached a better lower-bound solution than wake-sleep across the reported MNIST and Frey Face settings.
- The paper claims the KL term in the VAE objective can act as a regularizer encouraging the approximate posterior to remain close to the prior.

## My interpretation

## Connections
- [[ELBO]]
- [[KL Divergence]]
- [[Variational Inference]]
- [[Variational Autoencoders]]
