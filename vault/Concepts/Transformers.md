# Transformers

## Metadata
- Type: concept
- Status: developing

## Short definition
Transformers are neural network architectures built around attention mechanisms rather than sequence-aligned recurrence or convolution.

## Intuition
Transformers process data as sequences of tokens. Each layer lets tokens exchange information through [[Self-Attention]], then applies a position-wise feed-forward transformation.

The key shift in [[2017 Attention Is All You Need]] is that sequence positions can be processed in parallel during training, while attention directly connects distant positions.

## Mathematical formulation
- Related math: [[Scaled Dot-Product Attention]], [[Self-Attention]]
- A transformer layer is built from attention sublayers, [[Transformer Feed-Forward Networks]], residual connections, and normalization.
- In the original encoder-decoder transformer, encoder layers use self-attention, while decoder layers use masked self-attention plus encoder-decoder attention.
- [[2017 Attention Is All You Need]] uses `LayerNorm(x + Sublayer(x))`; the normalization method itself is introduced in [[2016 Layer Normalization]].

## Historical development
[[2017 Attention Is All You Need]] introduces the Transformer for sequence transduction and argues that attention alone can replace recurrence and convolution in the model architecture.

[[2022 Scalable Diffusion Models with Transformers]] applies transformer backbones to diffusion models by operating on latent patch tokens.

## Related papers
- [[2016 Layer Normalization]]
- [[2017 Attention Is All You Need]]
- [[2022 Scalable Diffusion Models with Transformers]]

## Related concepts
- [[Attention]]
- [[Self-Attention]]
- [[Scaled Dot-Product Attention]]
- [[Multi-Head Attention]]
- [[Positional Encoding]]
- [[Transformer Feed-Forward Networks]]
- [[Residual Connections]]
- [[Layer Normalization]]
- [[Large Language Models]]
- [[Image Tokenization]]
- [[Diffusion with Transformers]]

## Open questions
- Which later source should anchor decoder-only transformer language models?

## Source notes
- [[2016 Layer Normalization]]
- [[2017 Attention Is All You Need]]
- [[2022 Scalable Diffusion Models with Transformers]]
