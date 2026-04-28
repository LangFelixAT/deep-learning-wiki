# Noise Conditional Score Networks

## Metadata
- Type: concept
- Status: developing

## Short definition
Score networks conditioned on the noise level of a Gaussian-perturbed data distribution.

## Intuition
NCSNs estimate score fields for several smoothed versions of the data distribution. High noise levels make the distribution easier to traverse, while low noise levels move sampling closer to the original data distribution.

## Mathematical formulation
- Related math: [[Score Matching]], [[Annealed Langevin Dynamics]]
- Perturbed distribution: `q_sigma(x) = integral p_data(t) N(x; t, sigma^2 I) dt`.
- NCSN target: `s_theta(x, sigma_i) approx grad_x log q_{sigma_i}(x)`.
- Combined objective: a weighted sum of denoising score matching losses over noise levels.

## Historical development
Introduced in [[2019 Generative Modeling by Estimating Gradients of the Data Distribution]] as a way to train one conditional score network across multiple Gaussian noise levels.

## Related papers
- [[2019 Generative Modeling by Estimating Gradients of the Data Distribution]]

## Related concepts
- [[Score-Based Generative Models]]
- [[Annealed Langevin Dynamics]]
- [[Denoising]]
- [[Diffusion Models]]

## Open questions
- Needs verification: how later score-based models modify or generalize NCSNs.
