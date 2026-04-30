# Large Language Models

## Metadata
- Type: concept
- Status: developing

## Short definition
Large neural language models trained on broad text distributions.

## Intuition
Large language models often generate text autoregressively, one token at a time. This makes decoding behavior and memory movement important parts of practical model performance.

## Mathematical formulation
- Related math: [[Scaled Dot-Product Attention]], [[Expert Routing]], [[Notation Conventions]]
- Autoregressive decoding repeatedly applies Transformer layers to a growing context.
- Cached keys and values from previous positions are reused through the [[KV Cache]].
- [[Multi-Query Attention]] reduces the number of key/value heads that must be stored and read during decoding.
- [[Grouped-Query Attention]] uses an intermediate number of key/value groups to trade off quality and KV-cache size.
- [[FlashAttention]] reduces memory traffic inside the exact attention computation itself.
- [[Mixture of Experts]] increases parameter capacity through sparse activation, often by routing tokens through expert feed-forward layers.
- [[Multi-Head Latent Attention]] reduces KV-cache cost by caching compressed latent attention state.
- [[RMSNorm]] is relevant as a later normalization choice in modern LLM architectures, but specific adoption claims should be grounded in model papers.
- [[LLM Training Systems]] covers the parallelism, precision, and communication constraints that make large-scale training feasible.

## Historical development
[[2019 Fast Transformer Decoding One Write-Head is All You Need]] is an early source connecting Transformer attention architecture to incremental decoding speed through key/value memory bandwidth.

[[2023 GQA]] introduces grouped-query attention as a practical quality/speed compromise for efficient language model inference.

[[2022 FlashAttention]] makes exact attention more memory efficient, which is relevant for longer sequences and efficient Transformer training/inference.

[[2021 Switch Transformers]] is an important source for sparse expert scaling in language models, using top-1 routing to activate one expert per token.

[[2019 Root Mean Square Layer Normalization]] is not an LLM paper, but it grounds a normalization method that becomes important in later LLM architecture notes.

[[2024 DeepSeekMoE]] introduces fine-grained expert segmentation and shared expert isolation for stronger expert specialization.

[[2024 DeepSeek-V2 Technical Report]] introduces MLA and DeepSeekMoE as mechanisms for efficient inference and economical sparse model training.

[[2024 DeepSeek-V3 Technical Report]] combines sparse MoE, MLA, multi-token prediction, and FP8/systems co-design in a modern large language model.

After the DeepSeek-V2 and DeepSeekMoE ingests, [[2024 DeepSeek-V3 Technical Report]] is best treated as a hub for combining inherited efficient-attention and MoE mechanisms with V3-specific training and balancing choices.

## Related concepts
- [[Transformers]]
- [[Efficient LLM Architecture]]
- [[Attention]]
- [[Multi-Head Attention]]
- [[Grouped-Query Attention]]
- [[Multi-Query Attention]]
- [[KV Cache]]
- [[FlashAttention]]
- [[Mixture of Experts]]
- [[DeepSeekMoE]]
- [[Expert Routing]]
- [[Multi-Head Latent Attention]]
- [[RMSNorm]]
- [[LLM Training Systems]]
- [[Scaling Laws]]

## Related papers
- [[2019 Fast Transformer Decoding One Write-Head is All You Need]]
- [[2021 Switch Transformers]]
- [[2019 Root Mean Square Layer Normalization]]
- [[2022 FlashAttention]]
- [[2023 GQA]]
- [[2024 DeepSeekMoE]]
- [[2024 DeepSeek-V2 Technical Report]]
- [[2024 DeepSeek-V3 Technical Report]]

## Open questions
- Which source should anchor decoder-only LLM architecture?
- Which source should anchor prefill/decode behavior in modern LLM serving?
