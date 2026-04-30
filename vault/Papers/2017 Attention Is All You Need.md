# Attention Is All You Need

## Metadata
- Authors: Ashish Vaswani, Noam Shazeer, Niki Parmar, Jakob Uszkoreit, Llion Jones, Aidan N. Gomez, Lukasz Kaiser, Illia Polosukhin
- Year: 2017
- Venue: NeurIPS / NIPS
- Link: https://arxiv.org/abs/1706.03762
- arXiv: 1706.03762
- Source type: paper
- Status: studied
- Reliability: high
- Added: 2026-04-29

## Scope
This ingest covers foundational transformer architecture ideas: self-attention, scaled dot-product attention, multi-head attention, query/key/value projections, positional encoding, encoder-decoder structure, residual connections, layer normalization, position-wise feed-forward blocks, parallelism compared with recurrence, and high-level relationship to later LLM architectures.

Excluded: detailed benchmark tables, machine-translation dataset details, optimizer/training hyperparameters beyond brief context, label smoothing, byte-pair encoding, implementation details, later transformer variants, and modern attention optimizations except as future connections.

## One-sentence summary
Vaswani et al. introduce the Transformer, an encoder-decoder sequence model built around self-attention and multi-head attention instead of recurrence or convolution.

## Why this paper matters
This paper establishes the architecture backbone for modern transformer-based language models and many later vision, diffusion, and multimodal systems.

## Problem
Recurrent sequence models process tokens sequentially, which limits parallelization across positions and makes long-range dependency learning depend on long computational paths.

The paper asks whether sequence transduction can be handled by attention mechanisms alone, without recurrent or convolutional sequence computation.

## Background needed
- [[Attention]]
- [[Self-Attention]]
- matrix multiplication
- softmax
- sequence-to-sequence encoder-decoder models
- [[Residual Connections]]
- [[Layer Normalization]]

## Core idea
Replace recurrent and convolutional sequence processing with stacked self-attention and position-wise feed-forward layers.

Self-attention lets each position directly attend to other positions in the sequence, while multi-head attention lets the model attend through multiple learned representation subspaces.

## Method
- Use an encoder-decoder architecture.
- Build each encoder layer from multi-head self-attention followed by a position-wise feed-forward network.
- Build each decoder layer from masked self-attention, encoder-decoder attention, and a position-wise feed-forward network.
- Wrap each sublayer with residual connections and layer normalization.
- Add positional encodings to token embeddings because the model has no recurrence or convolution.
- Use scaled dot-product attention as the core attention operation.

## Important equations
Scaled dot-product attention:

$$
\operatorname{Attention}(Q,K,V) = \operatorname{softmax}(QK^T / \sqrt(d_k)) V
$$
Multi-head attention:

$$
\operatorname{MultiHead}(Q,K,V) = \operatorname{Concat}(head_1, ..., head_h) W^O
$$
Each head:

$$
head_i = \operatorname{Attention}(Q W_i^Q, K W_i^K, V W_i^V)
$$
Position-wise feed-forward network:

$$
FFN(x) = \max(0, xW_1 + b_1) W_2 + b_2
$$
Sublayer wrapper:

$$
LayerNorm(x + Sublayer(x))
$$
Sinusoidal positional encoding:

$$
\operatorname{PE}(pos,2i) = sin(pos / 10000^(2i/d_model))
$$
$$
\operatorname{PE}(pos,2i+1) = cos(pos / 10000^(2i/d_model))
$$
## Results
- Claim from source: the Transformer achieves strong machine translation results while being more parallelizable and requiring less training time than the recurrent/convolutional baselines considered in the paper.
- Claim from source: self-attention has constant maximum path length between positions, while recurrent layers require a path length linear in sequence length.
- Claim from source: multi-head attention lets the model attend to information from different representation subspaces at different positions.

Detailed benchmark tables are outside this ingest scope.

## Limitations
- The source focuses on sequence transduction, especially machine translation.
- Self-attention has quadratic complexity in sequence length in the full-attention setup.
- The paper predates modern decoder-only LLMs, KV-cache optimization, RoPE, MQA/GQA/MLA, FlashAttention, and sparse attention.
- Layer normalization and residual connections are used as architecture components but not explained as standalone theory in this paper.

## Claim from source
- Claim from source: the Transformer relies entirely on attention mechanisms for sequence transduction, dispensing with recurrence and convolutions.
- Claim from source: recurrent models have inherently sequential computation across positions, limiting parallelization during training.
- Claim from source: self-attention relates different positions of a single sequence to compute a sequence representation.
- Claim from source: scaled dot-product attention divides dot products by $\sqrt(d_k)$ to counteract large dot-product magnitudes that can push softmax into small-gradient regions.
- Claim from source: multi-head attention is beneficial because it allows attention to different representation subspaces at different positions.
- Claim from source: positional encodings are added because the model contains no recurrence or convolution and therefore needs position information injected.

## My interpretation
The paper's lasting contribution is not only the attention equation. It defines a reusable block structure: token embeddings plus positional information, repeated attention and feed-forward sublayers, residual pathways, and normalization.

Modern LLM architecture can be read as a descendant of this block, with later work changing attention variants, position encodings, normalization choices, decoder-only layout, scaling, and inference systems.

## Unclear / Needs verification
- Needs verification: which later LLM architecture changes should be treated as direct descendants of this paper versus independent engineering developments.
- Needs verification: details of layer normalization should be grounded in the LayerNorm paper rather than inferred from this source.
- Needs verification: residual-stream interpretations should be grounded in later sources.

## Connections to concepts
- [[Transformers]]
- [[Attention]]
- [[Self-Attention]]
- [[Scaled Dot-Product Attention]]
- [[Multi-Head Attention]]
- [[Positional Encoding]]
- [[Residual Connections]]
- [[Layer Normalization]]
- [[Transformer Feed-Forward Networks]]
- [[Large Language Models]]

## Connections to papers
- [[2022 Scalable Diffusion Models with Transformers]]

## Questions
- How should the wiki separate encoder-decoder transformer concepts from decoder-only LLM concepts?
- Which later paper should anchor decoder-only language modeling?
- Which source should anchor the residual-stream view used in modern interpretability?

## Follow-up reading
- [[Layer Normalization]]
- RoFormer
- Fast Transformer Decoding: One Write-Head is All You Need
- FlashAttention
