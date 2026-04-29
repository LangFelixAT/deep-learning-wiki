# Diffusion with Transformers

## Metadata
- Type: concept
- Status: developing

## Short definition
Diffusion with transformers uses a transformer backbone as the denoising network inside a diffusion model.

## Intuition
A diffusion model needs a neural network that maps a noisy state and conditioning information to a denoising prediction. DiT shows that this network does not have to be a U-Net; it can be a transformer if the image or latent is represented as tokens.

## U-Net versus transformer backbone
- U-Net diffusion backbones process spatial feature maps with convolution-heavy image structure.
- Transformer diffusion backbones process a sequence of tokens.
- The diffusion objective can remain DDPM-like while the denoising backbone changes.
- This makes the backbone choice part of the diffusion design space rather than part of the diffusion objective itself.
- Needs verification: which backbone is better depends on compute budget, data, conditioning, and implementation details.

## Latent patches as tokens
- In DiT, diffusion operates in latent space.
- The noised latent `z_t` is split into patches.
- Each patch is embedded as a token.
- The transformer processes the token sequence and predicts diffusion outputs.

## Relation to latent diffusion
DiT fits naturally into [[Latent Diffusion Models]]: the autoencoder creates the latent `z`, and the transformer replaces the U-Net as the denoising model over noisy latents.

## Relation to transformer architecture
DiT is a bridge between [[Diffusion Models]] and [[Transformers]]. The image or latent is turned into tokens, making the denoising step compatible with transformer blocks without changing the high-level diffusion training objective.

## Why scaling matters
The DiT paper studies scaling through Gflops. Increasing depth/width or increasing the number of latent tokens increases compute, and the source reports that higher Gflops correlate with better sample quality in its experiments.

## Common misconceptions
- DiT does not remove the diffusion process; it changes the denoising backbone.
- DiT is not just a text-conditioning method.
- Patch tokens are not necessarily raw pixel tokens; in DiT they are latent patches.
- Scaling token count changes compute even when parameter count changes little.

## Related papers
- [[2022 Scalable Diffusion Models with Transformers]]
- [[2022 Latent Diffusion Models]]

## Related concepts
- [[Diffusion Models]]
- [[Latent Diffusion Models]]
- [[Image Tokenization]]
- [[Transformers]]
- [[Diffusion Design Space]]

## Open questions
- Needs verification: how DiT-style scaling behaves outside the class-conditional image setting studied in the paper.
- Needs verification: how later DiT variants alter conditioning and tokenization choices.
