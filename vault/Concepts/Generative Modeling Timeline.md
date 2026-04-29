# Generative Modeling Timeline

## Metadata
- Type: concept
- Status: developing

## Short definition
Timeline of important generative modeling ideas covered by the wiki.

## Intuition
This page tracks how the current generative-modeling path moves from latent-variable likelihood models toward score-based and diffusion-based generation.

## Timeline
- 2013: [[2013 Auto-Encoding Variational Bayes]] introduces the VAE example using stochastic variational inference and the reparameterization trick.
- 2015: [[2015 Deep Unsupervised Learning using Nonequilibrium Thermodynamics]] introduces diffusion probabilistic models as learned reversals of gradual noising processes.
- 2019: [[2019 Generative Modeling by Estimating Gradients of the Data Distribution]] develops score-based generative modeling with noise-conditional score networks and annealed Langevin dynamics.
- 2020: [[2020 Denoising Diffusion Probabilistic Models]] develops DDPMs with a variational training objective and simplified noise-prediction loss.
- 2020: [[2020 Denoising Diffusion Implicit Models]] introduces DDIM sampling with the DDPM training objective.
- 2021: [[2021 Score-Based Generative Modeling through SDEs]] unifies score-based and diffusion models through SDEs.
- 2022: [[2022 Latent Diffusion Models]] moves diffusion into learned latent space for efficient high-resolution synthesis.

## Open questions
- Needs verification: add GANs, normalizing flows, and energy-based models once their anchor sources are ingested.

## Related concepts
- [[Diffusion Models]]
- [[Diffusion Design Space]]
- [[Variational Autoencoders]]
- [[Score-Based Generative Models]]
- [[Deep Learning Timeline]]
