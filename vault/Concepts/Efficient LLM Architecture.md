# Efficient LLM Architecture

## Metadata
- Type: concept
- Status: developing
- Last reviewed: 2026-04-29

## Short definition
Efficient LLM architecture studies how transformer language models reduce memory, compute, and communication cost while preserving model quality.

## Intuition
Large language models are constrained by more than parameter count. During training and inference, bottlenecks come from attention computation, KV-cache memory, feed-forward capacity, routing balance, precision, and hardware communication.

This page is a synthesis hub for the efficient-architecture track. It organizes already-ingested notes rather than introducing a new source.

## Main design axes
- Attention computation: [[Scaled Dot-Product Attention]], [[Multi-Head Attention]], [[FlashAttention]]
- KV-cache representation: [[KV Cache]], [[Multi-Query Attention]], [[Grouped-Query Attention]], [[Multi-Head Latent Attention]], [[Multi-Head Latent Attention (Math)]]
- Sparse feed-forward capacity: [[Mixture of Experts]], [[DeepSeekMoE]], [[Expert Routing]]
- Training and systems constraints: [[LLM Training Systems]], [[Large Language Models]]
- Transformer scaffolding: [[Transformers]], [[Transformer Feed-Forward Networks]], [[Layer Normalization]], [[Residual Connections]], [[Rotary Position Embedding]]

## Historical development
- [[2017 Attention Is All You Need]] establishes the transformer architecture around self-attention and feed-forward sublayers.
- [[2019 Fast Transformer Decoding One Write-Head is All You Need]] introduces [[Multi-Query Attention]] to reduce key/value memory bandwidth during autoregressive decoding.
- [[2021 Switch Transformers]] shows sparse expert routing as a way to scale parameter count without activating all parameters per token.
- [[2022 FlashAttention]] reframes exact attention as an IO-aware algorithmic problem.
- [[2023 GQA]] places [[Grouped-Query Attention]] between MHA and MQA for quality/efficiency tradeoffs.
- [[2024 DeepSeekMoE]] refines MoE structure through fine-grained routed experts and shared expert isolation.
- [[2024 DeepSeek-V2 Technical Report]] grounds [[Multi-Head Latent Attention]] as a KV-cache reduction mechanism.
- [[2024 DeepSeek-V3 Technical Report]] combines MLA, DeepSeekMoE, load balancing, multi-token prediction, and systems co-design at large scale.

## Current mental model
Efficient LLM architecture is not one trick. It is a stack of design choices:

- [[FlashAttention]] reduces the memory traffic of exact attention computation.
- [[Multi-Query Attention]], [[Grouped-Query Attention]], and [[Multi-Head Latent Attention]] reduce KV-cache pressure during decoding.
- [[Mixture of Experts]] and [[DeepSeekMoE]] increase parameter capacity while keeping activated parameters smaller than total parameters.
- [[Expert Routing]] introduces a new optimization problem: experts must be selected, balanced, and kept useful.
- [[LLM Training Systems]] connects these architectural choices to precision, communication, and distributed training constraints.

## Related math
- [[Scaled Dot-Product Attention]]
- [[Notation Conventions]]
- [[Multi-Head Latent Attention (Math)]]
- [[Expert Routing]]
- [[Layer Normalization (Math)]]
- [[Rotary Position Embedding (Math)]]

## Related papers
- [[2017 Attention Is All You Need]]
- [[2019 Fast Transformer Decoding One Write-Head is All You Need]]
- [[2021 Switch Transformers]]
- [[2022 FlashAttention]]
- [[2023 GQA]]
- [[2024 DeepSeekMoE]]
- [[2024 DeepSeek-V2 Technical Report]]
- [[2024 DeepSeek-V3 Technical Report]]

## Related concepts
- [[Attention]]
- [[KV Cache]]
- [[Multi-Head Attention]]
- [[Multi-Query Attention]]
- [[Grouped-Query Attention]]
- [[Multi-Head Latent Attention]]
- [[FlashAttention]]
- [[Mixture of Experts]]
- [[DeepSeekMoE]]
- [[Large Language Models]]

## Open questions
- Needs verification: how [[Multi-Head Latent Attention]] compares empirically and mathematically to MQA and GQA outside the DeepSeek-V2 source.
- Needs verification: whether auxiliary-loss-free load balancing should become a dedicated math note.
- Open question: where to place paged attention and serving systems in the wiki structure.
- Open question: how to connect future sparse-attention methods such as XSA without mixing them into older attention notes too early.

## My understanding
The efficient-LLM track should be treated as a design-space map. Attention variants, MoE routing, KV-cache handling, and training systems are separate axes, but modern models combine them because the practical bottlenecks interact.

## Source notes
- [[2017 Attention Is All You Need]]
- [[2019 Fast Transformer Decoding One Write-Head is All You Need]]
- [[2021 Switch Transformers]]
- [[2022 FlashAttention]]
- [[2023 GQA]]
- [[2024 DeepSeekMoE]]
- [[2024 DeepSeek-V2 Technical Report]]
- [[2024 DeepSeek-V3 Technical Report]]

## Revision notes
- 2026-04-29: Created as the first efficient-architecture synthesis hub.
