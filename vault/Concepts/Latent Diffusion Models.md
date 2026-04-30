# Latent Diffusion Models

## Metadata
- Type: concept
- Status: developing

## Short definition
Latent diffusion models are diffusion models that perform the noising and denoising process in a learned latent space instead of directly in pixel space.

## Intuition
Images contain many high-frequency details that are expensive to model at every diffusion step. LDMs first compress images into a perceptually useful latent representation, then spend the diffusion model's capacity on that lower-dimensional space.

## Latent space idea
- An encoder maps images into latents: $z = E(x)$.
- Diffusion is trained and sampled over latent variables $z_t$.
- The generated latent is decoded back to pixels with $D(z)$.
- The latent space is chosen to reduce dimensionality while preserving enough perceptual detail for synthesis.

## Mathematical formulation
Latent diffusion replaces pixel-space diffusion over $x_t$ with diffusion over latent variables $z_t$. See [[Latent Diffusion]] for the math note.

## Encoder and decoder role
- The encoder `E` performs the compression from image space to latent space.
- The decoder `D` maps latent samples back to image space.
- The diffusion model learns a distribution over latents, not over raw pixels.
- The autoencoder stage can be reused across diffusion models and conditioning tasks.

## Pipeline
1. Train or use an autoencoder with encoder `E` and decoder `D`.
2. Encode training images into latents $z = E(x)$.
3. Train a diffusion model to denoise noisy latents $z_t$.
4. At sampling time, start from latent noise and run the reverse diffusion process in latent space.
5. Decode the final latent sample into an image with `D`.

## Relation to DiT
[[Diffusion with Transformers]] uses the latent diffusion setup but replaces the usual U-Net denoising backbone with a transformer. In DiT, the noised latent is split into patches, and those patches become transformer tokens.

## Relation to pixel diffusion
Pixel diffusion denoises directly in image space. Latent diffusion keeps the diffusion objective but moves it to a compressed representation, reducing compute and memory costs.

## Historical development
[[2022 Latent Diffusion Models]] introduced latent diffusion as an efficient way to apply diffusion models to high-resolution image synthesis by moving denoising into an autoencoder latent space.

## Relation to CFG
[[Classifier-Free Guidance]] can be applied during latent diffusion sampling by combining conditional and unconditional predictions in latent space. The LDM paper uses classifier-free guidance as a quality-improving conditioning mechanism in some conditional settings.

## Relation to CLIP and text embeddings
Text conditioning in latent diffusion uses learned text representations as conditioning inputs. CLIP-like embeddings are one way to represent semantic text information for generative conditioning, although the original LDM paper's exact conditioning encoders vary by setting. Needs verification: track which later systems use CLIP directly versus other text encoders.

## Related papers
- [[2022 Latent Diffusion Models]]
- [[2020 Denoising Diffusion Probabilistic Models]]
- [[2022 Classifier-Free Diffusion Guidance]]
- [[2021 CLIP]]
- [[2022 Scalable Diffusion Models with Transformers]]

## Related concepts
- [[Diffusion Models]]
- [[Latent Diffusion]]
- [[Classifier-Free Guidance]]
- [[CLIP]]
- [[Diffusion with Transformers]]
- [[Image Tokenization]]
- [[Diffusion Parameterization]]

## Open questions
- Needs verification: how much compression can be used before the autoencoder bottleneck visibly limits generation quality.
- Needs verification: how later latent diffusion systems modify the conditioning and guidance setup.
