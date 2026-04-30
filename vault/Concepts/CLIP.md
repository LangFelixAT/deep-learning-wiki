# CLIP

## Metadata
- Type: concept
- Status: developing

## Short definition
CLIP is a vision-language representation model that embeds images and text into a shared semantic space.

## Intuition
If an image and a caption describe the same thing, their embeddings should be close. If they do not match, their embeddings should be farther apart.

## Joint embedding idea
- An image encoder maps images to image embeddings.
- A text encoder maps text to text embeddings.
- Both embeddings live in a shared space.
- Similarity in this space measures image-text alignment.

## Contrastive learning idea
- Matched image-text pairs are positive pairs.
- Mismatched image-text pairs are negative pairs.
- Training increases similarity for positives and decreases similarity for negatives.
- Related math: [[Contrastive Learning]].

## Mathematical formulation
At this level, the core formulation is a contrastive objective over image-text embedding similarities. See [[Contrastive Learning]] for the math note.

## Semantic meaning of embeddings
CLIP embeddings are not labels themselves. They are vector representations where visual and linguistic concepts can be compared by similarity.

## Role in conditioning
Text embeddings from CLIP-like models can act as conditioning inputs for generative models. In diffusion systems, such embeddings can tell the denoising model what semantic content the sample should move toward.

These embeddings are typically provided as additional inputs to the denoising network, for example through cross-attention or conditioning channels.

This makes CLIP part of the bridge between representation learning and multimodal generation, but later systems may use different text encoders or multimodal embedding models.

## Historical development
[[2021 CLIP]] introduced contrastive image-text pretraining as a way to learn transferable visual representations from natural language supervision.

## Related papers
- [[2021 CLIP]]
- [[2022 Latent Diffusion Models]]

## Related concepts
- [[Contrastive Learning]]
- [[Latent Diffusion Models]]
- [[Diffusion Models]]
- [[Classifier-Free Guidance]]
- [[Generative Modeling]]

## Open questions
- Needs verification: how CLIP-style embeddings differ from other text embeddings when used for diffusion conditioning.
- Needs verification: which later generative systems use CLIP directly versus CLIP-like or transformer text embeddings.
- Needs verification: broader multimodal representation learning should be grounded by sources beyond CLIP.
