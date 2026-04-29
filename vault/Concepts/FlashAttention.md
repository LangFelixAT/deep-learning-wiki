# FlashAttention

## Metadata
- Type: concept
- Status: developing
- Last reviewed: 2026-04-29

## Short definition
FlashAttention is an IO-aware exact attention algorithm that avoids materializing the full attention matrix in slow memory.

## Intuition
Standard attention is often described by its arithmetic cost, but wall-clock time also depends on memory movement. FlashAttention keeps the same [[Scaled Dot-Product Attention]] result while changing how the computation is scheduled.

Instead of writing the full `N x N` attention matrix to memory, it processes attention in blocks and keeps only the information needed to combine those blocks into the exact final softmax output.

## Mathematical formulation
- Related math: [[Scaled Dot-Product Attention]]
- Source: [[2022 FlashAttention]]
- Standard attention computes `S = QK^T`, `P = softmax(S)`, and `O = PV`.
- FlashAttention computes the same `O = softmax(QK^T)V`.
- The difference is that `Q`, `K`, and `V` are processed in tiles, and the softmax normalization is accumulated online.
- The attention matrix is not materialized as a full `N x N` object in high-bandwidth memory.
- The source keeps the exact quadratic attention computation; the linear-memory claim is about additional memory beyond inputs and outputs, not a linear-time attention model.

## Historical development
[[2022 FlashAttention]] argues that many attention algorithms focused on FLOPs while neglecting IO. It introduces FlashAttention as an exact attention algorithm designed around the GPU memory hierarchy.

## Related papers
- [[2022 FlashAttention]]
- [[2017 Attention Is All You Need]]

## Related concepts
- [[Attention]]
- [[Self-Attention]]
- [[Scaled Dot-Product Attention]]
- [[Multi-Head Attention]]
- [[KV Cache]]
- [[Transformers]]
- [[Large Language Models]]

## Open questions
- Needs verification: later FlashAttention variants should be ingested separately.
- Needs verification: relationship to paged attention and modern serving systems needs later sources.
- Needs verification: decide whether IO-aware algorithms deserve a broader concept page.

## My understanding
FlashAttention is not an attention variant in the modeling sense. It is an implementation-level algorithm for the same attention function, designed so the model spends less time moving large intermediate matrices through memory.

## Source notes
- [[2022 FlashAttention]]

## Revision notes
