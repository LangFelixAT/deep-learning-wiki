# Image Tokenization

## Metadata
- Type: concept
- Status: stub

## Short definition
Image tokenization represents an image or image-like latent as a sequence of smaller units that can be processed by a transformer.

## Intuition
Transformers operate on sequences. Splitting an image or latent into patches turns spatial visual data into tokens.

## Core idea
- Images or latents can be split into patches.
- Each patch becomes a token.
- Tokenization makes vision data compatible with transformer blocks.
- In DiT, the tokens are latent patches rather than raw image patches.
- Tokenization changes the representation given to the model, not the underlying diffusion process by itself.

## Related concepts
- [[Diffusion with Transformers]]
- [[Latent Diffusion Models]]
- [[Transformers]]

## Open questions
- Needs verification: when to use raw image patches versus latent patches.
