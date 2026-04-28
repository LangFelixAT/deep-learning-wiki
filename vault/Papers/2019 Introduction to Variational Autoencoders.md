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
The foundational problem is learning a probabilistic model `p_theta(x)` for observed data when the model contains latent variables `z`.

For a latent-variable model, the observed-data probability is:

`p_theta(x) = integral p_theta(x,z) dz`.

In deep latent-variable models, this marginal likelihood is typically intractable, which makes direct maximum-likelihood learning difficult. The posterior

`p_theta(z|x) = p_theta(x,z) / p_theta(x)`

is also typically intractable because it depends on the same marginal likelihood. The tutorial frames VAEs as a way to make learning and inference computationally tractable by introducing an approximate posterior.

## Core ideas
- A latent-variable generative model defines a joint distribution over observed variables and unobserved variables, commonly factorized as `p_theta(x,z) = p_theta(z)p_theta(x|z)`.
- The inference problem is to recover or approximate the posterior `p_theta(z|x)` over latent variables given an observation.
- VAEs introduce an inference model, also called an encoder or recognition model, `q_phi(z|x)`, and optimize it to approximate `p_theta(z|x)`.
- The generative model, or decoder, `p_theta(x|z)` maps latent variables to a distribution over observations.
- The ELBO is optimized instead of the intractable marginal log likelihood. It is both a lower bound on `log p_theta(x)` and an objective that improves the generative model and approximate posterior together.
- Sharing one inference model across datapoints is amortized variational inference, avoiding a separate variational optimization loop for each datapoint.

## Important equations
Latent-variable marginal likelihood:

`p_theta(x) = integral p_theta(x,z) dz`.

Common latent-variable factorization:

`p_theta(x,z) = p_theta(z)p_theta(x|z)`.

Posterior identity:

`p_theta(z|x) = p_theta(x,z) / p_theta(x)`.

Approximate posterior objective:

`q_phi(z|x) ~= p_theta(z|x)`.

Example encoder parameterization:

`(mu, log sigma) = EncoderNeuralNet_phi(x)`.

`q_phi(z|x) = N(z; mu, diag(sigma))`.

ELBO decomposition:

`log p_theta(x) = L_{theta,phi}(x) + D_KL(q_phi(z|x) || p_theta(z|x))`.

ELBO:

`L_{theta,phi}(x) = E_{q_phi(z|x)}[log p_theta(x,z) - log q_phi(z|x)]`.

Lower-bound relation:

`L_{theta,phi}(x) <= log p_theta(x)`.

Dataset ELBO:

`L_{theta,phi}(D) = sum_{x in D} L_{theta,phi}(x)`.

## Claims from source
- Claim from source: VAEs provide a computationally efficient way to optimize deep latent-variable models jointly with corresponding inference models using SGD.
- Claim from source: the inference model `q_phi(z|x)` approximates the intractable posterior `p_theta(z|x)`.
- Claim from source: amortized inference avoids a per-datapoint optimization loop by sharing variational parameters across datapoints.
- Claim from source: the KL divergence `D_KL(q_phi(z|x) || p_theta(z|x))` is the gap between the ELBO and the marginal log likelihood.
- Claim from source: maximizing the ELBO approximately maximizes the marginal likelihood and minimizes the KL divergence from the approximate posterior to the true posterior.
- Claim from source: in deep latent-variable models, the marginal likelihood and posterior are typically intractable.

## My interpretation

## Connections
- [[ELBO]]
- [[KL Divergence]]
- [[Variational Inference]]
- [[Amortized Variational Inference]]
- [[Variational Autoencoders]]
