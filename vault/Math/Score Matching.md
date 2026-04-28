# Score Matching

## Metadata
- Type: math
- Status: developing

## Goal
Define objectives that learn score functions for probability models.

## Definitions
- Score matching learns score functions, i.e. gradients of log densities. Needs verification: add a source-backed canonical definition.
- [[2020 Denoising Diffusion Probabilistic Models]] connects the DDPM noise-prediction parameterization to denoising score matching over multiple noise levels.

## Assumptions
- Needs development.
- In the DDPM connection, noise levels are indexed by timestep `t`, and the model predicts the Gaussian noise added to `x_0`.

## Derivation
- In DDPM, the variational term for the reverse mean can be reparameterized so the model predicts `epsilon` from `x_t`.
- The resulting weighted mean-squared noise-prediction objective resembles denoising score matching over multiple noise scales.
- Needs verification: full equivalence requires checking the weighting and parameterization details from the paper.

## Interpretation
- DDPM uses the score-matching connection to motivate a simple denoising objective for training the reverse process.

## Common mistakes
- Needs development.

## Related concepts
- [[Diffusion Models]]
- [[Energy-Based Models]]
- [[Denoising]]
- [[Diffusion ELBO]]
- [[2020 Denoising Diffusion Probabilistic Models]]
