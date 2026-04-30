# Fast Transformer Decoding: One Write-Head is All You Need

## Metadata
- Authors: Noam Shazeer
- Year: 2019
- Venue: arXiv
- Link: https://arxiv.org/abs/1911.02150
- arXiv: 1911.02150
- Source type: paper
- Status: studied
- Reliability: high
- Added: 2026-04-29

## Scope
This ingest covers the decoding-time bottleneck in autoregressive Transformers, key/value memory bandwidth during incremental decoding, the difference between multi-head and multi-query attention, shared keys and values across heads, effects on cache size and memory reads, the speed/quality tradeoff, and high-level relation to later efficient LLM inference.

Excluded: detailed benchmark tables, TPU/kernel implementation details, full machine translation setup, training hyperparameters, unrelated architecture changes, and modern GQA/MLA/FlashAttention details except as future connections.

## One-sentence summary
Shazeer introduces multi-query attention, a Transformer attention variant that keeps multiple query heads but shares one set of key and value projections to reduce memory bandwidth during incremental decoding.

## Why this paper matters
The paper identifies key/value memory reads as a major bottleneck in autoregressive Transformer decoding and proposes a simple architectural change that directly reduces the size of cached keys and values.

## Problem
Transformer training can parallelize across sequence positions, but autoregressive generation cannot: each next token depends on previous generated tokens. During incremental decoding, each step must read stored keys and values from previous positions, which can make memory bandwidth a bottleneck.

## Background needed
- [[Transformers]]
- [[Attention]]
- [[Self-Attention]]
- [[Multi-Head Attention]]
- [[KV Cache]]

## Core idea
In standard multi-head attention, each attention head has separate key and value projections. In multi-query attention, the model keeps multiple query heads but shares a single set of keys and values across all heads.

This removes the head dimension from the stored key/value tensors while retaining multiple query heads.

The paper's "one write-head" wording refers to writing one shared set of keys and values, not to using only one query head.

## Method
- Start from Transformer multi-head attention.
- Analyze batched training attention versus incremental decoding attention.
- Show that incremental decoding repeatedly reloads large cached key/value tensors.
- Modify attention so $P_q$ remains per-head, while $P_k$ and $P_v$ are shared across heads.
- Compare quality and speed against multi-head baselines and smaller-head alternatives.

## Important equations
Standard multi-head projections in the paper's notation. Here $\operatorname{einsum}$ denotes Einstein-summation tensor indexing notation:

$$
Q = \operatorname{einsum}(\text{"bnd,hdk->bhnk"}, X, P_q)
$$
$$
K = \operatorname{einsum}(\text{"bmd,hdk->bhmk"}, M, P_k)
$$
$$
V = \operatorname{einsum}(\text{"bmd,hdv->bhmv"}, M, P_v)
$$
Multi-query attention keeps per-head queries but removes the head dimension from keys and values:

$$
Q = \operatorname{einsum}(\text{"bnd,hdk->bhnk"}, X, P_q)
$$
$$
K = \operatorname{einsum}(\text{"bmd,dk->bmk"}, M, P_k)
$$
$$
V = \operatorname{einsum}(\text{"bmd,dv->bmv"}, M, P_v)
$$
Incremental multi-head attention stores previous keys and values with shapes like $prev_K: [b,h,m,k]$ and $prev_V: [b,h,m,v]$.

Incremental multi-query attention stores previous keys and values with shapes like $prev_K: [b,m,k]$ and $prev_V: [b,m,v]$.

Under the paper's simplifying assumptions, incremental multi-head attention has memory-access/computation ratio:

$$
\Theta\left(\frac{n}{d} + \frac{1}{b}\right)
$$
Incremental multi-query attention changes this to:

$$
\Theta\left(\frac{1}{d} + \frac{n}{d h} + \frac{1}{b}\right)
$$
The source emphasizes the reduction of the `n / d` term by a factor of the number of heads `h`.

## Results
- Claim from source: multi-query attention greatly reduces memory-bandwidth requirements in incremental decoding.
- Claim from source: in the reported experiments, multi-query models decode much faster than the multi-head baseline.
- Claim from source: the multi-query models incur only minor quality degradation compared with the multi-head baseline and compare favorably with simpler alternatives that reduce head count or key/value dimensionality.

Detailed benchmark tables are outside this ingest scope.

## Limitations
- The experiments are limited to the paper's translation and language-modeling setups.
- The paper predates later grouped-query attention and modern LLM serving systems.
- Quality/speed tradeoffs may differ by architecture scale, hardware, and deployment setup.

## Claim from source
- Claim from source: incremental Transformer inference can be memory-bandwidth limited because it repeatedly loads large key/value tensors.
- Claim from source: multi-query attention is identical to multi-head attention except that different heads share one set of keys and values.
- Claim from source: removing the head dimension from `K` and `V` reduces the problematic memory-access term by a factor of `h` under the paper's simplifying assumptions.
- Claim from source: local attention and multi-query attention are orthogonal approaches.
- Claim from source: multi-query attention enables faster decoding with only minor quality degradation in the evaluated settings.

## My interpretation
This paper reframes attention efficiency around serving-time memory movement, not just arithmetic complexity. The key insight is that during decoding, the KV cache is repeatedly read, so reducing key/value heads can matter more than preserving the exact standard multi-head structure.

## Unclear / Needs verification
- Needs verification: how the exact speed/quality tradeoff transfers to modern decoder-only LLMs.
- Needs verification: the historical path from multi-query attention to grouped-query attention should be grounded in a later GQA source.
- Needs verification: interactions with FlashAttention, paged attention, and modern KV-cache systems require separate source notes.

## Connections to concepts
- [[Multi-Query Attention]]
- [[KV Cache]]
- [[Multi-Head Attention]]
- [[Attention]]
- [[Self-Attention]]
- [[Transformers]]
- [[Large Language Models]]

## Connections to papers
- [[2017 Attention Is All You Need]]

## Questions
- Which source should anchor grouped-query attention?
- Which source should anchor KV-cache paging and modern serving systems?
- How should the wiki separate architectural attention variants from implementation-level attention kernels?

## Follow-up reading
- grouped-query attention
- FlashAttention
- paged attention
- decoder-only LLM architecture papers
