# DeepSeekMoE

## Metadata
- Type: concept
- Status: stub
- Last reviewed: 2026-04-29

## Short definition
DeepSeekMoE is a Mixture-of-Experts feed-forward architecture using fine-grained routed experts and shared experts.

## Intuition
Standard MoE routing can send tokens to specialized experts, but experts may learn redundant knowledge. DeepSeekMoE separates some capacity into shared experts while routing tokens among finer-grained routed experts.

## Mathematical formulation
- Related math: [[Expert Routing]]
- Source context: [[2024 DeepSeek-V2 Technical Report]]
- The feed-forward output combines the residual input, shared expert outputs, and gated routed expert outputs.
- Routed experts are selected by top-k token-to-expert affinity scores.
- Shared experts are always included.
- Needs verification: full DeepSeekMoE derivation should be grounded in the original DeepSeekMoE paper.

## Historical development
[[2024 DeepSeek-V2 Technical Report]] uses DeepSeekMoE for economical training and states that it follows the DeepSeekMoE architecture. [[2024 DeepSeek-V3 Technical Report]] reuses DeepSeekMoE as part of its larger architecture.

## Related papers
- [[2024 DeepSeek-V2 Technical Report]]
- [[2024 DeepSeek-V3 Technical Report]]

## Related concepts
- [[Mixture of Experts]]
- [[Expert Routing]]
- [[Transformer Feed-Forward Networks]]
- [[Large Language Models]]
- [[LLM Training Systems]]

## Open questions
- Needs verification: ingest the original DeepSeekMoE source before expanding shared/routed expert claims.
- Needs verification: compare DeepSeekMoE routing and load balancing with [[2021 Switch Transformers]].

## My understanding
DeepSeekMoE is a refinement of sparse feed-forward scaling: it keeps the MoE idea of conditional expert activation, but adds structure to reduce redundancy and improve specialization.

## Source notes
- [[2024 DeepSeek-V2 Technical Report]]
- [[2024 DeepSeek-V3 Technical Report]]

## Revision notes
