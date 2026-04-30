# Diffusion Forward Process

## Metadata
- Type: math
- Status: partially verified

## Goal
Define the noising process that gradually transforms data into a tractable distribution.

## Definitions
- Sources: [[2015 Deep Unsupervised Learning using Nonequilibrium Thermodynamics]], [[2020 Denoising Diffusion Probabilistic Models]].
- $x_0$ is a data sample.
- $x_1, ..., x_T$ are latent variables with the same dimensionality as $x_0$.
- The forward process is a Markov chain:

$$
q(x_1:T|x_0) = \prod_{t=1}^T q(x_t|x_{t-1})
$$
- In the 2015 paper, the forward trajectory is written with superscript time notation:

$$
q(x^{(0:T)}) = q(x^{(0)}) \prod_{t=1}^T q(x^{(t)}|x^{(t-1)})
$$
- Gaussian transition:

$$
q(x_t|x_{t-1}) = \mathcal{N}(x_t; \sqrt{1 - \beta_t}x_{t-1}, \beta_t I)
$$
- Let $\alpha_t = 1 - \beta_t$ and $\bar{\alpha}_t = \prod_{s=1}^t \alpha_s$.

## Assumptions
- The forward process uses Gaussian noise.
- The 2015 paper also discusses binomial diffusion, but this note focuses on the Gaussian form that connects most directly to DDPMs.
- In the 2015 paper, the Gaussian forward diffusion schedule can be learned or selected; in the DDPM setup summarized here, the variance schedule $\beta_1, ..., \beta_T$ is fixed.
- The process gradually destroys signal so that late $x_T$ is close to Gaussian noise.
- Needs verification: exact conditions under which $x_T$ is sufficiently close to $\mathcal{N}(0,I)$ depend on the variance schedule.

## Derivation
- Because each step is Gaussian and linear in $x_{t-1}$, the marginal noised sample at arbitrary timestep has closed form:

$$
q(x_t|x_0) = \mathcal{N}(x_t; \sqrt{\bar{\alpha}_t}x_0, (1 - \bar{\alpha}_t)I)
$$
- Equivalently, one can sample:

$$
x_t = \sqrt{\bar{\alpha}_t}x_0 + \sqrt{1 - \bar{\alpha}_t}\epsilon, \quad \epsilon \sim \mathcal{N}(0,I)
$$
- Skipped steps: induction over Gaussian transitions.

## Interpretation
- The forward process is the destructive direction: it slowly removes data structure.
- In DDPM, the forward process is not learned.
- It provides supervised-like noisy targets for learning the reverse denoising transitions.
- In the 2015 framing, slow noising is motivated by nonequilibrium thermodynamics: a gradual path can make the reverse process locally simple.

## Common mistakes
- Treating the DDPM forward process as a learned encoder.
- Forgetting that $x_t$ has the same dimensionality as the data.
- Confusing $\beta_t$ with learned reverse-process variance.

## Related concepts
- [[Diffusion Models]]
- [[Diffusion Reverse Process]]
- [[Diffusion ELBO]]
- [[2015 Deep Unsupervised Learning using Nonequilibrium Thermodynamics]]
- [[2020 Denoising Diffusion Probabilistic Models]]
