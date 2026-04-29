# LLM Inference Systems

## Metadata
- Type: concept
- Status: stub
- Last reviewed: 2026-04-29

## Short definition
Synthesis page for serving and inference constraints in large language models.

## Intuition
LLM inference is shaped by prefill/decode behavior, KV-cache memory, memory bandwidth, batching, and serving-system choices. This page is a placeholder for future source-grounded work.

## Mathematical formulation
- Related math: [[Scaled Dot-Product Attention]], [[Multi-Head Latent Attention (Math)]], [[Notation Conventions]]

## Historical development
Current grounded notes cover attention-side cache reduction and IO-aware attention, but not serving systems in depth.

## Related papers
- [[2019 Fast Transformer Decoding One Write-Head is All You Need]]
- [[2022 FlashAttention]]
- [[2023 GQA]]
- [[2024 DeepSeek-V2 Technical Report]]
- [[2024 DeepSeek-V3 Technical Report]]

## Related concepts
- [[Efficient LLM Architecture]]
- [[KV Cache]]
- [[Large Language Models]]
- [[Multi-Query Attention]]
- [[Grouped-Query Attention]]
- [[Multi-Head Latent Attention]]
- [[LLM Training Systems]]

## Open questions
- Needs verification: paged attention, continuous batching, prefill/decode separation, and serving-system bottlenecks need dedicated source ingests.

## My understanding
This page should stay separate from [[Efficient LLM Architecture]] if serving systems become a major track.

## Source notes
- [[2019 Fast Transformer Decoding One Write-Head is All You Need]]

## Revision notes
- 2026-04-29: Created as a stub synthesis page.
