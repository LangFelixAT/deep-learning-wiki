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
- the marginal likelihood `p_theta(x) = integral p_theta(z)p_theta(x|z) dz` is intractable;
- the posterior `p_theta(z|x)` is intractable;
- mean-field VB expectations may also be intractable;
- the dataset is large enough that batch optimization or expensive per-datapoint sampling is impractical.

The target tasks are approximate ML or MAP estimation of model parameters, approximate posterior inference for latent variables, and approximate marginal inference for observed variables.

## Core idea
Introduce an approximate posterior, or recognition model, `q_phi(z|x)`, and optimize it jointly with the generative model `p_theta(x,z)`.

The key technical idea is to rewrite samples from `q_phi(z|x)` as deterministic transformations of parameter-free noise:

`z = g_phi(epsilon, x)`, with `epsilon ~ p(epsilon)`.

This reparameterization gives a differentiable Monte Carlo estimator of the variational lower bound, allowing optimization of both `theta` and `phi` using stochastic gradient methods.

## Method
The method starts from the variational lower bound for each datapoint:

`log p_theta(x^(i)) = D_KL(q_phi(z|x^(i)) || p_theta(z|x^(i))) + L(theta, phi; x^(i))`.

Because the KL term is non-negative, `L(theta, phi; x^(i))` is a lower bound on the marginal log likelihood.

The paper then:
- defines a recognition model `q_phi(z|x)` as an approximation to the true posterior;
- reparameterizes samples from `q_phi(z|x)` using auxiliary noise;
- builds Monte Carlo estimators of the lower bound and its gradients;
- scales the estimator to minibatches;
- applies the framework to a neural-network encoder and decoder, producing the variational auto-encoder example.

In the VAE example, the prior is `p_theta(z) = N(0, I)`, the approximate posterior is diagonal Gaussian, and the encoder outputs the mean and standard deviation used in `z = mu + sigma * epsilon`.

## Important equations
Variational decomposition:

`log p_theta(x^(i)) = D_KL(q_phi(z|x^(i)) || p_theta(z|x^(i))) + L(theta, phi; x^(i))`.

Lower bound:

`L(theta, phi; x^(i)) = E_q_phi(z|x) [-log q_phi(z|x) + log p_theta(x,z)]`.

Alternative lower bound form:

`L(theta, phi; x^(i)) = -D_KL(q_phi(z|x^(i)) || p_theta(z)) + E_q_phi(z|x^(i))[log p_theta(x^(i)|z)]`.

Reparameterization:

`z = g_phi(epsilon, x)`, with `epsilon ~ p(epsilon)`.

Generic SGVB estimator:

`L_A ~= (1/L) sum_l [log p_theta(x^(i), z^(i,l)) - log q_phi(z^(i,l)|x^(i))]`.

Lower-variance estimator when the KL term is analytic:

`L_B ~= -D_KL(q_phi(z|x^(i)) || p_theta(z)) + (1/L) sum_l log p_theta(x^(i)|z^(i,l))`.

Minibatch estimator:

`L(theta, phi; X) ~= (N/M) sum_i L(theta, phi; x^(i))`.

Gaussian VAE reparameterization:

`z^(i,l) = mu^(i) + sigma^(i) * epsilon^(l)`, with `epsilon^(l) ~ N(0, I)`.

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
