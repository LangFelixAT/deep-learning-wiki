# Amortized Variational Inference

## Metadata
- Type: concept
- Status: developing

## Short definition
Amortized variational inference uses a shared inference model to approximate posteriors across datapoints.

## Intuition
The inference problem in latent-variable models is to infer hidden variables after observing data. In [[2019 Introduction to Variational Autoencoders]], this posterior is `p_theta(z|x)`, and it is typically intractable because it depends on the marginal likelihood `p_theta(x)`.

Variational inference introduces an approximate posterior `q_phi(z|x)` and chooses its parameters so it is close to the true posterior. In the amortized setting, the same parameterized inference model is reused across datapoints instead of optimizing separate variational parameters for each datapoint.

## Mathematical formulation
- Related math: [[Variational Inference]], [[ELBO]], [[KL Divergence]]
- Tutorial formulation: optimize `q_phi(z|x)` through the ELBO, using the identity `log p_theta(x) = L_{theta,phi}(x) + D_KL(q_phi(z|x) || p_theta(z|x))`.

## Generative model and inference model
The generative model `p_theta(x,z)` describes how latent variables and observations are jointly distributed. The inference model `q_phi(z|x)` approximates the reverse inference direction from observation to latent variables.

In VAEs, this inference model is amortized: the same parameterized encoder is reused across datapoints instead of optimizing separate variational parameters for each datapoint.

## Historical development
Needs verification from source notes beyond [[2019 Introduction to Variational Autoencoders]].

## Related papers
- [[2019 Introduction to Variational Autoencoders]]
- [[2013 Auto-Encoding Variational Bayes]]

## Related concepts
- [[Variational Autoencoders]]
- [[Variational Inference]]
- [[ELBO]]
- [[KL Divergence]]

## Open questions
- Needs verification: relationship between classical per-datapoint VI and amortized VI across different source treatments.
