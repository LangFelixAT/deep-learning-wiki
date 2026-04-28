# Denoising

## Metadata
- Type: concept
- Status: stub

## Short definition
Denoising is the task of recovering a cleaner signal from a corrupted or noisy version.

## Intuition
In [[2020 Denoising Diffusion Probabilistic Models]], denoising appears as the learned reverse direction of a process that gradually adds Gaussian noise.

## Mathematical formulation
- Related math: [[Diffusion Reverse Process]], [[Score Matching]]
- In DDPM, the model is trained to predict the noise `epsilon` added to a clean datapoint at a randomly chosen timestep.

## Historical development
Needs verification from source notes beyond DDPM.

## Related papers
- [[2020 Denoising Diffusion Probabilistic Models]]

## Related concepts
- [[Diffusion Models]]
- [[Score Matching]]

## Open questions
- Needs verification: relationship between denoising objectives and classical denoising autoencoders.
