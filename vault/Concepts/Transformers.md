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
- Positional information can be injected through absolute encodings, as in [[2017 Attention Is All You Need]], or through methods such as [[Rotary Position Embedding]] that alter query/key geometry.
- [[Mixture of Experts]] can replace some dense feed-forward sublayers with routed expert feed-forward layers.
- [[Multi-Head Latent Attention]] changes how attention state is represented and cached for efficient inference.

## Historical development
[[2017 Attention Is All You Need]] introduces the Transformer for sequence transduction and argues that attention alone can replace recurrence and convolution in the model architecture.

[[2019 Fast Transformer Decoding One Write-Head is All You Need]] identifies incremental decoding memory bandwidth as a Transformer inference bottleneck and introduces [[Multi-Query Attention]].

[[2023 GQA]] introduces [[Grouped-Query Attention]] as an intermediate key/value sharing pattern between multi-head and multi-query attention.

[[2022 FlashAttention]] improves Transformer efficiency by making exact attention IO-aware rather than changing the model's attention pattern.

[[2021 Switch Transformers]] introduces a simplified sparse expert feed-forward layer for scaling transformer parameter count with roughly fixed per-token expert compute.

[[2024 DeepSeekMoE]] refines MoE feed-forward layers through fine-grained expert segmentation and shared expert isolation.

[[2024 DeepSeek-V2 Technical Report]] introduces [[Multi-Head Latent Attention]] and uses [[DeepSeekMoE]] inside a transformer language model.

[[2024 DeepSeek-V3 Technical Report]] combines MoE feed-forward scaling with MLA-based attention-cache compression and training-system co-design.

[[2022 Scalable Diffusion Models with Transformers]] applies transformer backbones to diffusion models by operating on latent patch tokens.

## Related papers
- [[2016 Layer Normalization]]
- [[2017 Attention Is All You Need]]
- [[2019 Fast Transformer Decoding One Write-Head is All You Need]]
- [[2021 Switch Transformers]]
- [[2022 FlashAttention]]
- [[2024 DeepSeekMoE]]
- [[2024 DeepSeek-V2 Technical Report]]
- [[2024 DeepSeek-V3 Technical Report]]
- [[2023 GQA]]
- [[2021 RoFormer]]
- [[2022 Scalable Diffusion Models with Transformers]]

## Related concepts
- [[Attention]]
- [[Self-Attention]]
- [[Scaled Dot-Product Attention]]
- [[Multi-Head Attention]]
- [[Grouped-Query Attention]]
- [[Multi-Query Attention]]
- [[KV Cache]]
- [[FlashAttention]]
- [[Multi-Head Latent Attention]]
- [[Positional Encoding]]
- [[Rotary Position Embedding]]
- [[Transformer Feed-Forward Networks]]
- [[Mixture of Experts]]
- [[DeepSeekMoE]]
- [[Expert Routing]]
- [[Residual Connections]]
- [[Layer Normalization]]
- [[Large Language Models]]
- [[LLM Training Systems]]
- [[Image Tokenization]]
- [[Diffusion with Transformers]]

## Open questions
- Which later source should anchor decoder-only transformer language models?

## Source notes
- [[2016 Layer Normalization]]
- [[2017 Attention Is All You Need]]
- [[2019 Fast Transformer Decoding One Write-Head is All You Need]]
- [[2021 Switch Transformers]]
- [[2022 FlashAttention]]
- [[2024 DeepSeekMoE]]
- [[2024 DeepSeek-V2 Technical Report]]
- [[2024 DeepSeek-V3 Technical Report]]
- [[2023 GQA]]
- [[2021 RoFormer]]
- [[2022 Scalable Diffusion Models with Transformers]]
