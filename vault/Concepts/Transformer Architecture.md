# Transformer Architecture

## Metadata
- Type: concept
- Status: developing
- Last reviewed: 2026-04-30

## Short definition
Transformer architecture is the stack of attention, feed-forward, positional, normalization, residual, and efficiency choices that make transformer models work.

## Intuition
A transformer layer can be read as two recurring operations: tokens exchange information through attention, then each token representation is transformed by a position-wise feed-forward block. Residual connections and normalization wrap these sublayers so many layers can be stacked.

This page is a synthesis hub for transformer internals. It is broader than [[Transformers]], which is the base concept page, and less systems-focused than [[Efficient LLM Architecture]].

## Architectural skeleton
- Token representations enter a stack of transformer layers.
- [[Self-Attention]] lets positions exchange information.
- [[Multi-Head Attention]] runs several attention heads in parallel over learned query, key, and value projections.
- [[Transformer Feed-Forward Networks]] apply the same position-wise MLP to each token after attention.
- [[Residual Connections]] add sublayer inputs back to sublayer outputs.
- [[Layer Normalization]] stabilizes sublayer wrappers; [[2017 Attention Is All You Need]] uses $LayerNorm(x + Sublayer(x))$.
- [[Positional Encoding]] injects order information because self-attention alone does not encode sequence order.

## Main design axes
- Attention operation: [[Attention]], [[Self-Attention]], [[Scaled Dot-Product Attention]], [[Multi-Head Attention]]
- Positional information: [[Positional Encoding]], [[Rotary Position Embedding]], [[Rotary Position Embedding (Math)]]
- Per-token transformation: [[Transformer Feed-Forward Networks]]
- Stability scaffolding: [[Residual Connections]], [[Layer Normalization]], [[RMSNorm]], [[Normalization]]
- Sparse capacity: [[Mixture of Experts]], [[DeepSeekMoE]], [[Expert Routing]]
- Efficient attention and inference: [[KV Cache]], [[Multi-Query Attention]], [[Grouped-Query Attention]], [[Multi-Head Latent Attention]], [[FlashAttention]]
- Systems and scaling context: [[Large Language Models]], [[LLM Training Systems]], [[Efficient LLM Architecture]]

## Mathematical formulation
- Related math: [[Scaled Dot-Product Attention]], [[Layer Normalization (Math)]], [[RMSNorm (Math)]], [[Rotary Position Embedding (Math)]], [[Expert Routing]], [[Notation Conventions]]
- Core attention operation:

$$
\operatorname{Attention}(Q,K,V) = \operatorname{softmax}(QK^T / \sqrt(d_k)) V
$$
- Multi-head attention applies that operation to projected subspaces and concatenates head outputs.
- Position-wise feed-forward blocks transform each token independently after attention has mixed sequence information.
- MoE variants replace some dense feed-forward blocks with routed expert feed-forward blocks.

## Historical development
[[2017 Attention Is All You Need]] establishes the transformer layer pattern: attention sublayers, position-wise feed-forward sublayers, residual connections, normalization, and positional encodings.

[[2016 Layer Normalization]] grounds the normalization method later used as transformer scaffolding.

[[2019 Root Mean Square Layer Normalization]] grounds RMSNorm as a simpler normalization variant that later becomes relevant to transformer language-model architecture.

[[2021 RoFormer]] introduces [[Rotary Position Embedding]], changing how position enters the query/key geometry.

[[2019 Fast Transformer Decoding One Write-Head is All You Need]] shows that attention architecture affects autoregressive decoding cost through key/value memory bandwidth.

[[2023 GQA]] introduces [[Grouped-Query Attention]] as an intermediate key/value sharing pattern between full multi-head attention and multi-query attention.

[[2022 FlashAttention]] changes the computation schedule for exact attention rather than the attention function itself.

[[2021 Switch Transformers]] introduces sparse expert feed-forward layers as a way to scale transformer parameter count.

[[2024 DeepSeekMoE]], [[2024 DeepSeek-V2 Technical Report]], and [[2024 DeepSeek-V3 Technical Report]] connect transformer architecture to modern efficient LLM design through MoE feed-forward layers, MLA, KV-cache reduction, and systems co-design.

[[2022 Scalable Diffusion Models with Transformers]] shows that transformer backbones can also be used outside language modeling, operating over latent image patches in diffusion models.

## Current mental model
The transformer is not only an attention mechanism. Attention is the sequence-mixing operation, but the architecture also depends on feed-forward transformations, positional information, normalization, residual pathways, and later efficiency choices.

For modern LLMs, the same block structure remains recognizable, but important pressure points shift toward:
- reducing attention memory movement
- managing the [[KV Cache]]
- replacing dense feed-forward capacity with [[Mixture of Experts]]
- choosing positional encodings that work for long contexts
- stabilizing very deep stacks with normalization and residual design
- choosing between normalization variants such as [[Layer Normalization]] and [[RMSNorm]]

## Related papers
- [[2016 Layer Normalization]]
- [[2017 Attention Is All You Need]]
- [[2019 Root Mean Square Layer Normalization]]
- [[2019 Fast Transformer Decoding One Write-Head is All You Need]]
- [[2021 RoFormer]]
- [[2021 Switch Transformers]]
- [[2022 FlashAttention]]
- [[2022 Scalable Diffusion Models with Transformers]]
- [[2023 GQA]]
- [[2024 DeepSeekMoE]]
- [[2024 DeepSeek-V2 Technical Report]]
- [[2024 DeepSeek-V3 Technical Report]]

## Related concepts
- [[Transformers]]
- [[Attention]]
- [[Self-Attention]]
- [[Multi-Head Attention]]
- [[Scaled Dot-Product Attention]]
- [[Transformer Feed-Forward Networks]]
- [[Residual Connections]]
- [[Layer Normalization]]
- [[RMSNorm]]
- [[Positional Encoding]]
- [[Rotary Position Embedding]]
- [[Mixture of Experts]]
- [[DeepSeekMoE]]
- [[KV Cache]]
- [[Efficient LLM Architecture]]
- [[Large Language Models]]
- [[Diffusion with Transformers]]

## Open questions
- Needs verification: decoder-only LLM architecture should be grounded in a dedicated source rather than inferred from the original encoder-decoder Transformer.
- Needs verification: pre-norm versus post-norm, RMSNorm, gated MLPs, SwiGLU, and residual-stream views need source-grounded notes.
- Needs verification: modern transformer usage of RMSNorm should be grounded in model-specific architecture papers.
- Needs verification: sparse attention and XSA should be added only after source ingests.
- Open question: whether `[[Transformer Architecture]]` should eventually absorb part of `[[Transformers]]` or stay as the synthesis layer above it.

## My understanding
The transformer architecture track should be learned as a stack of design axes. The base block is attention plus feed-forward layers wrapped by residual and normalization scaffolding. Modern work then changes specific axes: attention sharing, cache representation, positional geometry, feed-forward sparsity, and systems-aware computation.

## Source notes
- [[2016 Layer Normalization]]
- [[2017 Attention Is All You Need]]
- [[2019 Root Mean Square Layer Normalization]]
- [[2019 Fast Transformer Decoding One Write-Head is All You Need]]
- [[2021 RoFormer]]
- [[2021 Switch Transformers]]
- [[2022 FlashAttention]]
- [[2022 Scalable Diffusion Models with Transformers]]
- [[2023 GQA]]
- [[2024 DeepSeekMoE]]
- [[2024 DeepSeek-V2 Technical Report]]
- [[2024 DeepSeek-V3 Technical Report]]

## Revision notes
- 2026-04-29: Created as a stub synthesis page.
- 2026-04-30: Expanded into a transformer-internals synthesis hub.
