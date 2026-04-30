# FlashAttention: Fast and Memory-Efficient Exact Attention with IO-Awareness

## Metadata
- Authors: Tri Dao, Daniel Y. Fu, Stefano Ermon, Atri Rudra, Christopher Re
- Year: 2022
- Venue: arXiv
- Link: https://arxiv.org/abs/2205.14135
- arXiv: 2205.14135
- Version read: arXiv v2, 2022-06
- Source type: paper
- Status: studied
- Reliability: high
- Added: 2026-04-29

## Scope
This ingest covers why standard attention is memory-bandwidth / IO limited, the distinction between compute complexity and memory access, attention matrix materialization as the core bottleneck, tiling/blocking at a high level, online softmax conceptually, exact attention versus approximate/sparse attention, relevance to long sequences and efficient Transformer training/inference, and relationships to [[Scaled Dot-Product Attention]], [[Multi-Head Attention]], and [[KV Cache]].

Excluded: CUDA kernel implementation details, detailed backward-pass derivation, detailed benchmark tables, FlashAttention-2 and later variants, paged attention, MLA/GQA details except as future connections, and hardware-specific tuning details.

## One-sentence summary
FlashAttention is an IO-aware exact attention algorithm that computes the same scaled dot-product attention while avoiding materialization of the full attention matrix in slow GPU memory.

## Why this paper matters
The paper shifts the attention-efficiency discussion from only FLOPs to memory movement, showing that the way attention is scheduled across the memory hierarchy can dominate wall-clock speed and memory use.

## Problem
Standard attention forms the score matrix $S = QK^T$ and probability matrix $P = \operatorname{softmax}(S)$, both of size $N \times N$. For long sequences, materializing and repeatedly reading/writing these matrices in high-bandwidth memory creates large IO cost.

Approximate attention methods reduce compute, but the source argues that FLOP reduction alone does not guarantee wall-clock speedup when memory access dominates.

## Background needed
- [[Scaled Dot-Product Attention]]
- [[Attention]]
- [[Self-Attention]]
- [[Multi-Head Attention]]
- [[Transformers]]

## Core idea
Compute exact attention in blocks. Load tiles of `Q`, `K`, and `V` into fast on-chip memory, compute partial attention results, and maintain the softmax normalization statistics needed to combine blocks correctly.

The algorithm avoids writing the full `N x N` attention matrix to slow memory.

## Method
- Start from standard attention:

$$
S = QK^T
$$
$$
P = \operatorname{softmax}(S)
$$
$$
O = PV
$$
- Split `Q`, `K`, and `V` into blocks.
- Load blocks into fast SRAM rather than repeatedly materializing large intermediates in HBM.
- Use online softmax statistics so each block can contribute to the exact final softmax result.
- Store enough normalization information to avoid storing the full attention matrix.

## Important equations
Standard attention:

$$
O = \operatorname{softmax}(QK^T)V
$$
The paper computes the same output:

$$
O = \operatorname{softmax}(QK^T)V
$$
The difference is the computation schedule and memory access pattern, not the mathematical attention function.

Conceptual online softmax state:
- row maximum `m`;
- row normalization sum `l`;
- partial output `O`.

Needs verification: full online-softmax algebra and backward-pass recomputation details are not reproduced in this note.

## Results
- Claim from source: FlashAttention computes exact attention, not an approximation.
- Claim from source: FlashAttention avoids materializing the large `N x N` attention matrix in HBM.
- Claim from source: FlashAttention reduces HBM reads/writes compared with standard attention.
- Claim from source: FlashAttention requires linear additional memory in sequence length beyond inputs and output.
- Claim from source: FlashAttention speeds up model training and enables longer-context models in the reported experiments.

Detailed benchmark tables are outside this ingest scope.

## Limitations
- The paper's implementation and speedups are hardware-dependent.
- Detailed CUDA kernel design and backward-pass derivation are outside this note.
- Later FlashAttention variants are not covered here.
- The paper includes block-sparse FlashAttention, but this ingest only records the exact-attention core and mentions sparse extensions as follow-up.

## Claim from source
- Claim from source: standard attention performs HBM accesses quadratic in sequence length because it materializes `S` and `P`.
- Claim from source: many approximate attention methods reduce FLOPs but do not necessarily improve wall-clock time.
- Claim from source: IO-aware attention should account for reads/writes between levels of GPU memory.
- Claim from source: tiling plus online softmax can compute exact attention without storing the full attention matrix.
- Claim from source: recomputation can reduce memory access enough to be faster despite extra FLOPs.

## My interpretation
FlashAttention is a systems-level reordering of the same attention math. It does not ask the model to attend differently; it asks the hardware to move less data while producing the same result.

This makes it complementary to attention-architecture changes like [[Multi-Query Attention]] and [[Grouped-Query Attention]]: those reduce key/value state, while FlashAttention reduces IO from the attention computation itself.

## Unclear / Needs verification
- Needs verification: exact IO-complexity bounds should be checked in a dedicated math/systems note if needed.
- Needs verification: how FlashAttention interacts with modern KV-cache and paged-attention systems should be grounded in later sources.
- Needs verification: later FlashAttention variants require separate source notes.

## Connections to concepts
- [[FlashAttention]]
- [[Scaled Dot-Product Attention]]
- [[Attention]]
- [[Self-Attention]]
- [[Multi-Head Attention]]
- [[KV Cache]]
- [[Transformers]]
- [[Large Language Models]]

## Connections to papers
- [[2017 Attention Is All You Need]]
- [[2019 Fast Transformer Decoding One Write-Head is All You Need]]
- [[2023 GQA]]

## Questions
- Should IO-aware attention get a separate concept page after more systems papers?
- Which source should anchor paged attention and serving-time KV-cache layout?
- Which source should anchor FlashAttention-2?

## Follow-up reading
- FlashAttention-2
- paged attention
- sparse attention
- long-context Transformer systems
