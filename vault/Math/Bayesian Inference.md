# Bayesian Inference

## Metadata
- Type: math
- Status: stub

## Goal
Describe inference over latent variables or parameters using probability.

## Canonical notation
- `x`: observed data.
- `z`: latent variable.
- `theta`: model parameter.
- `p(z)`: prior distribution over a latent variable.
- `p(x|z)`: likelihood of observations given latent variables.
- `p(z|x)`: posterior distribution.
- `p(x)`: marginal likelihood or evidence.

## Definitions
- Bayesian inference updates uncertainty about unknown variables after observing data.
- Prior: distribution before observing `x`.
- Likelihood: probability of observed data under a hypothesized latent variable or parameter.
- Posterior: distribution after conditioning on observed data.
- Evidence or marginal likelihood: normalizing term obtained by marginalizing over the unknown variable.

## Assumptions
- A probabilistic model defines a joint distribution.
- The posterior is well-defined when the evidence is finite and nonzero.
- Exact posterior computation may be intractable because the evidence can require a difficult sum or integral.

## Derivation
- Bayes' rule for a latent variable can be written as:

```text
p(z|x) = p(x|z) p(z) / p(x)
```

- The evidence marginalizes over the latent variable:

```text
p(x) = integral p(x|z) p(z) dz
```

- In latent-variable models, this posterior is the object approximated by [[Variational Inference]] when exact inference is difficult.
- Skipped steps: discrete case with sums and measure-theoretic assumptions.

## Interpretation
- Bayesian inference explains why posterior inference is central to VAEs and other latent-variable models.
- The difficulty of computing `p(z|x)` motivates approximate inference methods such as [[Variational Inference]].
- In this wiki, the most developed Bayesian path is through [[ELBO]] and [[Variational Autoencoders]].

## Common mistakes
- Confusing the likelihood `p(x|z)` with the posterior `p(z|x)`.
- Forgetting that the evidence `p(x)` is often the intractable term.
- Treating Bayesian inference over latent variables and Bayesian inference over model parameters as identical without specifying what is random.

## Related concepts
- [[Probability Theory]]
- [[Variational Inference]]
- [[ELBO]]
- [[KL Divergence]]
- [[Variational Autoencoders]]
