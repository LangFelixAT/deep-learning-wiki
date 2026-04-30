# Maximum Likelihood Estimation

## Metadata
- Type: math
- Status: stub

## Goal
Define likelihood-based parameter estimation for model training.

## Canonical notation
- $x$: observed data.
- $\theta$: model parameters.
- $p_{\theta}(x)$: likelihood of data under parameters $\theta$.
- $\log p_{\theta}(x)$: log likelihood.
- $D = {x_i}$: dataset.

## Definitions
- Maximum likelihood estimation chooses parameters that make the observed data likely under the model.
- For independent datapoints, the likelihood is often written as a product over datapoints.
- The log likelihood turns the product into a sum, which is usually easier to optimize.
- Negative log likelihood is the loss form minimized in many training setups.

## Assumptions
- A parameterized probabilistic model $p_{\theta}(x)$ is defined.
- Datapoints are often assumed independent and identically distributed for the basic objective.
- The likelihood or an estimator/lower bound of it must be tractable enough to optimize.

## Derivation
- For a dataset $D = {x_i}$, the maximum likelihood objective is:


$$
\theta^* = \arg\max_{\theta} \prod_i p_{\theta}(x_i)
$$

- Taking logs gives:


$$
\theta^* = \arg\max_{\theta} \sum_i \log p_{\theta}(x_i)
$$

- Equivalently, training often minimizes:


$$
- \sum_i \log p_{\theta}(x_i)
$$

- In latent-variable models, $p_{\theta}(x)$ may be intractable, motivating bounds such as the [[ELBO]].
- Skipped steps: connection between MLE and empirical risk minimization / KL minimization.

## Interpretation
- MLE is one of the central training principles behind probabilistic deep learning.
- VAEs optimize a lower bound on the marginal log likelihood when exact MLE is difficult.
- Diffusion probabilistic models can also be trained through variational bounds related to likelihood.

## Common mistakes
- Confusing likelihood as a function of parameters with probability as a function of data.
- Forgetting that maximizing likelihood and minimizing negative log likelihood are equivalent objectives.
- Assuming exact likelihood is tractable for all generative models.

## Related concepts
- [[Probability Theory]]
- [[Regularization]]
- [[ELBO]]
- [[Variational Inference]]
- [[Generative Modeling]]
