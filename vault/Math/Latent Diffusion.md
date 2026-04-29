# Latent Diffusion

## Metadata
- Type: math
- Status: partially verified

## Goal
Formulate diffusion modeling in a learned latent space rather than directly in pixel space.

## Definitions
- Source: [[2022 Latent Diffusion Models]].
- `x` is an image in pixel space.
- `E` is an encoder and `D` is a decoder.
- The latent representation is:

`z = E(x)`.

- Reconstruction is:

`x_hat = D(z) = D(E(x))`.

## Formulation in latent space
Instead of corrupting and denoising `x_t`, latent diffusion corrupts and denoises `z_t`.

The latent diffusion objective is structurally:

`L_LDM = E_{E(x), epsilon, t}[||epsilon - epsilon_theta(z_t,t)||_2^2]`.

For conditional generation:

`epsilon_theta(z_t,t,y)`.

## Relation between x and z
- `x` lives in pixel space.
- `z` lives in the learned latent space.
- The encoder moves from `x` to `z`.
- The decoder moves from `z` back to image space.
- The diffusion model is trained on noisy versions of `z`, not noisy versions of `x`.

## Where diffusion happens
- Forward noising: applied to latent `z`.
- Reverse denoising: learned over latent states `z_t`.
- Final image synthesis: decode the final latent with `D`.

## Connection to existing diffusion math
- The objective mirrors the DDPM noise-prediction objective, replacing `x_t` with `z_t`.
- The same ideas from [[Diffusion Forward Process]], [[Diffusion Reverse Process]], and [[Score Matching]] apply after changing the data space from pixels to latents.
- Conditioning and [[Classifier-Free Guidance]] can be applied to latent predictions.

## Assumptions
- The autoencoder latent space preserves enough perceptual information for the target task.
- The autoencoder must be trained so that latent compression is perceptually meaningful, not merely low-dimensional.
- The latent representation has lower computational cost than pixel space.
- The decoder can map generated latents back to images with acceptable reconstruction quality.

## Derivation
- Train or choose an autoencoder giving `z = E(x)`.
- Apply the diffusion forward process to `z`.
- Train `epsilon_theta(z_t,t)` to predict the latent noise.
- Sample by reversing the latent noising process.
- Decode the final latent.
- Skipped steps: autoencoder training objective and architecture-specific details.

## Interpretation
Latent diffusion changes the domain of diffusion, not the basic denoising principle. It trades direct pixel modeling for a compressed representation where diffusion is cheaper.

## Common mistakes
- Thinking latent diffusion removes the diffusion sampling loop.
- Confusing the autoencoder latent with the noise latent `z_t` at a diffusion timestep.
- Assuming the decoder is optional; generated latents still need to be mapped back to pixels.
- Treating latent diffusion as unrelated to DDPM-style noise prediction.

## Related concepts
- [[Latent Diffusion Models]]
- [[Diffusion Models]]
- [[Diffusion Forward Process]]
- [[Diffusion Reverse Process]]
- [[Score Matching]]
- [[Classifier-Free Guidance]]
- [[2022 Latent Diffusion Models]]
