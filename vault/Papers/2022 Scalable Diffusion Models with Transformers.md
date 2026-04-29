# Scalable Diffusion Models with Transformers

## Metadata
- Authors: Peebles, Xie
- Year: 2022
- Link: https://arxiv.org/abs/2212.09748
- Source type: paper
- Status: studied
- Reliability: high

## Scope
This ingest covers only DiT as an architectural bridge: replacing U-Net backbones with transformers, operating on latent patches, patch/token representation, relation to latent diffusion, high-level conditioning, and scaling behavior with model size, token count, and Gflops.

## One-sentence summary
DiT shows that diffusion models can replace the standard U-Net backbone with a transformer operating on latent patches, and that sample quality improves predictably with increased transformer compute.

## Problem
Diffusion image models commonly use convolutional U-Net backbones, while transformers have become a scalable default architecture in many other domains. The paper asks whether transformer backbones can serve as scalable diffusion model backbones for images.

## Core ideas
- Replace the commonly used diffusion U-Net backbone with a transformer.
- Use the [[Latent Diffusion Models]] framework so the transformer operates on latent representations rather than raw pixels.
- Split the noised latent into patches and embed those patches as a sequence of tokens.
- Process the token sequence with transformer blocks to predict diffusion outputs.
- Treat conditioning, such as timestep and class label, as extra information supplied to the transformer at a high level.
- Analyze model scaling through forward-pass complexity measured in Gflops.

## Important equations or structural notation
Latent input:

`z = E(x)`.

Patch/token count for a square latent of spatial size `I x I` with patch size `p`:

`T = (I / p)^2`.

Patch-token view:

`z_t -> patchify(z_t) -> token sequence -> transformer -> diffusion prediction`.

Needs verification: exact output heads and conditioning block variants are architecture-specific and not expanded in this note.

## Claims from source
- Claim from source: DiT replaces the commonly used U-Net backbone with a transformer that operates on latent patches.
- Claim from source: DiTs are trained as latent diffusion models, using a VAE latent space.
- Claim from source: increasing transformer depth/width or increasing the number of input tokens increases Gflops.
- Claim from source: higher DiT Gflops correlate with lower FID in the experiments.
- Claim from source: the source argues that the U-Net inductive bias is not necessary for strong diffusion model performance in the studied setting.
- Claim from source: scaling model compute is important; increasing sampling compute alone does not fully compensate for smaller model compute.

## Limitations
- This note does not include benchmark tables, dataset details, implementation details, training hyperparameters, transformer internals, attention explanations, or later DiT variants.
- The paper's scaling conclusions are empirical and tied to the studied model family and training setup.
- Needs verification: how broadly the Gflops-quality relationship transfers across datasets, conditioning types, and later systems.

## My interpretation
DiT makes diffusion look more like the broader transformer scaling story: once images or latents are represented as tokens, the denoising backbone can be treated as a scalable sequence model rather than a hand-designed convolutional image network.

## Connections
- [[Diffusion with Transformers]]
- [[Image Tokenization]]
- [[Latent Diffusion Models]]
- [[Latent Diffusion]]
- [[Diffusion Models]]
- [[Diffusion Design Space]]
- [[Transformers]]
- [[Classifier-Free Guidance]]
