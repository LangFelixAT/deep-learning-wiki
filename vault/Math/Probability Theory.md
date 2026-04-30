# Probability Theory

## Metadata
- Type: math
- Status: stub

## Goal
Define the probability tools needed for deep learning notes.

## Canonical notation
- $x$: observed variable or data sample.
- $z$: latent variable.
- $p(x)$: probability mass or density function.
- $p(x,z)$: joint distribution.
- $p(z|x)$: conditional distribution.
- $E_p[f(x)]$: expectation of $f(x)$ under distribution $p$.

## Definitions
- A probability distribution assigns mass or density to possible outcomes.
- A joint distribution $p(x,z)$ describes two variables together.
- A marginal distribution sums or integrates out variables, for example $p(x) = \int p(x,z) dz$ in the continuous latent-variable case.
- A conditional distribution describes one variable given another, for example $p(z|x)$.
- An expectation averages a function under a distribution.

## Assumptions
- Variables may be discrete or continuous; sums and integrals should be chosen accordingly.
- Densities are defined with respect to an underlying measure. Needs verification: this measure-theoretic detail is not developed in the wiki yet.
- Support matters when comparing distributions with [[KL Divergence]].

## Derivation
- Marginalization removes a variable from a joint distribution:


$$
p(x) = \int p(x,z) dz
$$

- Conditioning relates joint, marginal, and conditional distributions:


$$
p(x,z) = p(z|x) p(x) = p(x|z) p(z)
$$

- Skipped steps: discrete versions with sums, measure-theoretic assumptions, and normalization conditions.

## Interpretation
- Probability notation is the base language for latent-variable models, Bayesian inference, variational inference, diffusion processes, and score-based models.
- Many deep learning objectives can be read as optimizing likelihoods, expectations, divergences, or bounds involving probability distributions.

## Common mistakes
- Mixing probability mass functions and probability density functions without checking whether sums or integrals are appropriate.
- Forgetting that conditional distributions depend on the variable being conditioned on.
- Treating unnormalized scores as probabilities before accounting for the normalizing constant.

## Related concepts
- [[Bayesian Inference]]
- [[Maximum Likelihood Estimation]]
- [[KL Divergence]]
- [[ELBO]]
- [[Variational Inference]]
