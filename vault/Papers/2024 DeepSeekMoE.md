# DeepSeekMoE

## Metadata
- Authors: Damai Dai, Chengqi Deng, Chenggang Zhao, R.X. Xu, Huazuo Gao, Deli Chen, Jiashi Li, Wangding Zeng, Xingkai Yu, Y. Wu, Zhenda Xie, Y.K. Li, Panpan Huang, Fuli Luo, Chong Ruan, Zhifang Sui, Wenfeng Liang
- Year: 2024
- Venue: technical report
- Link: https://arxiv.org/abs/2401.06066
- arXiv: 2401.06066
- Source type: paper
- Status: studied
- Reliability: high
- Added: 2026-04-29

## Scope
This ingest focuses on grounding [[DeepSeekMoE]] as the source for the MoE mechanism reused by [[2024 DeepSeek-V2 Technical Report]] and [[2024 DeepSeek-V3 Technical Report]].

Covered: motivation for improving conventional MoE, expert redundancy and specialization issues, fine-grained expert segmentation, shared expert isolation, routed experts versus shared experts, top-k routed expert selection at a high level, relation to [[Mixture of Experts]] and [[Expert Routing]], relation to [[2021 Switch Transformers]], and how DeepSeekMoE prepares V2/V3.

Excluded: full benchmark tables, full training setup, dataset details, hardware/system implementation details, hyperparameter sweeps, V2/V3-specific details except as later connections, and unrelated MoE variants beyond brief comparison.

## One-sentence summary
DeepSeekMoE proposes fine-grained expert segmentation and shared expert isolation to improve expert specialization in MoE language models.

## Why this paper matters
This paper is the primary source for the DeepSeekMoE mechanism later used in [[2024 DeepSeek-V2 Technical Report]] and [[2024 DeepSeek-V3 Technical Report]].

## Problem
Conventional MoE layers can scale parameter count with sparse activation, but the paper argues that they can suffer from weak expert specialization.

The source identifies two issues:
- Claim from source: knowledge hybridity, where a limited number of experts must absorb diverse knowledge.
- Claim from source: knowledge redundancy, where different experts may learn overlapping common knowledge.

## Background needed
- [[Mixture of Experts]]
- [[Expert Routing]]
- [[Transformer Feed-Forward Networks]]
- [[Large Language Models]]
- [[2021 Switch Transformers]]

## Core idea
DeepSeekMoE restructures the MoE feed-forward layer so that routed experts are smaller and more numerous, while some experts are isolated as shared experts that are always active.

## Method
- Start from a conventional transformer MoE layer that replaces an FFN with routed expert FFNs.
- Split each conventional expert into `m` smaller experts by reducing the FFN intermediate hidden dimension.
- Increase the number of activated experts from `K` to `mK` to keep the computational cost comparable.
- Isolate $K_s$ experts as shared experts that are always active.
- Reduce the number of activated routed experts by $K_s$ so shared expert isolation keeps the computational cost comparable.
- Route each token among the remaining routed experts using top-k token-to-expert affinity scores.
- Use load-balancing losses to reduce routing collapse and computation imbalance.

## Important equations
Generic top-k MoE layer:

$$
h_t^l = \sum_i g_{i,t} FFN_i(u_t^l) + u_t^l
$$

Fine-grained expert segmentation:

$$
h_t^l = \sum_{i=1}^{mN} g_{i,t} FFN_i(u_t^l) + u_t^l
$$

DeepSeekMoE with shared expert isolation:

$$
h_t^l = \sum_{i=1}^{K_s} FFN_i(u_t^l) + \sum_{i=K_s+1}^{mN} g_{i,t} FFN_i(u_t^l) + u_t^l
$$

At a high level, routed expert gates are nonzero only for experts selected by top-k affinity scores.

Needs verification: full balance-loss derivations should stay in [[Expert Routing]] or a later MoE-routing math note.

## Results
- Claim from source: DeepSeekMoE 2B achieves comparable performance with GShard 2.9B, which has 1.5x expert parameters and computation.
- Claim from source: DeepSeekMoE 2B nearly approaches the performance of a dense counterpart with the same number of total parameters.
- Claim from source: DeepSeekMoE 16B achieves comparable performance with LLaMA2 7B while using about 40% of the computations.
- Claim from source: preliminary 145B scaling experiments show advantages over GShard and performance comparable with DeepSeek 67B using less computation.

## Limitations
- The paper's specialization claims are supported by its experiments and analysis, but this ingest does not reproduce the full evidence.
- The exact balance-loss and training details are not expanded here.
- Later DeepSeek-V2/V3 change the surrounding architecture and training system.

## Claim from source
- Fine-grained expert segmentation increases the flexibility of activated expert combinations.
- Shared expert isolation aims to capture common knowledge and reduce redundancy among routed experts.
- DeepSeekMoE is designed to improve expert specialization compared with conventional top-k MoE.

## My interpretation
DeepSeekMoE is not just "more experts." Its central move is to separate two roles: shared experts absorb common knowledge, while routed fine-grained experts specialize in narrower knowledge regions.

This makes it an important successor to simpler sparse-routing designs such as [[2021 Switch Transformers]].

## Unclear / Needs verification
- Needs verification: how robust the "knowledge hybridity" and "knowledge redundancy" framing is across independent MoE studies.
- Needs verification: compare the balance-loss formulation carefully against [[2021 Switch Transformers]] and V2/V3.
- Needs verification: create a dedicated math note if MoE routing variants become too large for [[Expert Routing]].

## Connections to concepts
- [[DeepSeekMoE]]
- [[Mixture of Experts]]
- [[Expert Routing]]
- [[Transformer Feed-Forward Networks]]
- [[Large Language Models]]

## Connections to papers
- [[2021 Switch Transformers]]
- [[2024 DeepSeek-V2 Technical Report]]
- [[2024 DeepSeek-V3 Technical Report]]

## Questions
- Should expert specialization get its own concept page after more MoE sources?
- Should MoE balance losses be split into a dedicated math note?

## Follow-up reading
- [[2024 DeepSeek-V2 Technical Report]]
- [[2024 DeepSeek-V3 Technical Report]]
