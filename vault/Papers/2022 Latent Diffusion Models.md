# High-Resolution Image Synthesis with Latent Diffusion Models

## Metadata
- Authors: Rombach et al.
- Year: 2022
- Venue: CVPR
- Link: https://arxiv.org/abs/2112.10752
- Source type: paper
- Status: studied
- Reliability: high

## Scope
This ingest covers only core conceptual ideas: diffusion in latent space, encoder/decoder roles, efficiency motivation, high-level conditioning through cross-attention, and the overall generation pipeline.

## One-sentence summary
Latent Diffusion Models run diffusion in the latent space of a pretrained autoencoder, reducing the cost of high-resolution image generation while preserving much of the flexibility of diffusion models.

## Problem
Pixel-space diffusion models can produce strong image samples but are expensive to train and sample because repeated denoising evaluations happen in high-dimensional image space.

## Core ideas
- Separate image synthesis into a perceptual compression stage and a generative diffusion stage.
- Train or use an encoder `E` that maps an image `x` to a latent `z = E(x)`.
- Train a decoder `D` that reconstructs an image from the latent, `x_hat = D(z)`.
- Run the diffusion process in latent space over `z_t` rather than directly over pixels `x_t`.
- Decode the final generated latent with a single decoder pass.
- Conditioning inputs such as text can be injected through a high-level cross-attention conditioning mechanism.

## Important equations
Encoder / decoder relation:

`z = E(x)`, `x_hat = D(z) = D(E(x))`.

Pixel diffusion objective, structurally:

`L_DM = E_{x, epsilon, t}[||epsilon - epsilon_theta(x_t,t)||_2^2]`.

Latent diffusion objective:

`L_LDM = E_{E(x), epsilon, t}[||epsilon - epsilon_theta(z_t,t)||_2^2]`.

Conditional latent diffusion:

`epsilon_theta(z_t,t,y)` where `y` is conditioning information.

## Claims from source
- Claim from source: applying diffusion models in the latent space of pretrained autoencoders reduces computational requirements compared with pixel-space diffusion.
- Claim from source: the latent space is lower-dimensional while remaining perceptually close enough to the image space for high-quality synthesis.
- Claim from source: the autoencoder stage can be trained once and reused for multiple diffusion trainings or tasks.
- Claim from source: samples from the learned latent distribution can be decoded to image space with a single decoder pass.
- Claim from source: cross-attention conditioning enables flexible conditional generation, including text-to-image and other conditioning modalities.

## Limitations
- Latent diffusion still uses sequential denoising, so sampling remains slower than one-shot generators.
- Reconstruction quality of the autoencoder can bottleneck tasks requiring fine pixel accuracy.
- This note does not include UNet architecture details, attention block internals, training tricks, dataset specifics, or implementation details.

## My interpretation
LDMs move the expensive denoising computation from pixels to a compressed image-like coordinate system: the autoencoder handles perceptual representation, and diffusion models the distribution over those representations.

## Connections
- [[Diffusion Models]]
- [[Latent Diffusion Models]]
- [[Latent Diffusion]]
- [[Classifier-Free Guidance]]
- [[Diffusion Parameterization]]
- [[Score Matching]]
