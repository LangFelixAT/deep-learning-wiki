# DeepSeekMoE

## Metadata
- Type: concept
- Status: developing
- Last reviewed: 2026-04-29

## Short definition
DeepSeekMoE is a Mixture-of-Experts feed-forward architecture using fine-grained routed experts and shared experts.

## Intuition
Standard MoE routing can send tokens to specialized experts, but experts may learn redundant knowledge. DeepSeekMoE separates some capacity into shared experts while routing tokens among finer-grained routed experts.

[[2024 DeepSeekMoE]] frames the problem as two failure modes of conventional MoE: knowledge hybridity and knowledge redundancy.

## Mathematical formulation
- Related math: [[Expert Routing]]
- Primary source: [[2024 DeepSeekMoE]]
- The feed-forward output combines the residual input, shared expert outputs, and gated routed expert outputs.
- Routed experts are selected by top-k token-to-expert affinity scores.
- Shared experts are always included.
- Fine-grained expert segmentation splits conventional experts into more smaller experts while increasing the number of activated routed experts to preserve comparable compute.
- Shared expert isolation reserves some experts for common knowledge and routes only among the remaining experts.
- Needs verification: full balance-loss derivation should be handled in [[Expert Routing]] or a future MoE-routing math note.

## Historical development
[[2024 DeepSeekMoE]] introduces DeepSeekMoE as an MoE architecture aimed at stronger expert specialization.

[[2024 DeepSeek-V2 Technical Report]] uses DeepSeekMoE for economical training and states that it follows the DeepSeekMoE architecture. [[2024 DeepSeek-V3 Technical Report]] reuses DeepSeekMoE as part of its larger architecture.

## Related papers
- [[2024 DeepSeekMoE]]
- [[2024 DeepSeek-V2 Technical Report]]
- [[2024 DeepSeek-V3 Technical Report]]

## Related concepts
- [[Mixture of Experts]]
- [[Expert Routing]]
- [[Transformer Feed-Forward Networks]]
- [[Large Language Models]]
- [[LLM Training Systems]]

## Open questions
- Needs verification: compare [[2024 DeepSeekMoE]] routing and load balancing with [[2021 Switch Transformers]].
- Needs verification: decide whether expert specialization deserves a separate concept page.

## My understanding
DeepSeekMoE is a refinement of sparse feed-forward scaling: it keeps the MoE idea of conditional expert activation, but adds structure to reduce redundancy and improve specialization.

The important distinction from a simpler MoE layer is that not all experts play the same role: some are shared by all tokens, and the rest are routed specialists.

## Source notes
- [[2024 DeepSeekMoE]]
- [[2024 DeepSeek-V2 Technical Report]]
- [[2024 DeepSeek-V3 Technical Report]]

## Revision notes
