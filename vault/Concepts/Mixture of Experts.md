# Mixture of Experts

## Metadata
- Type: concept
- Status: developing
- Last reviewed: 2026-04-29

## Short definition
Mixture of Experts is a neural network design where different inputs activate different expert subnetworks rather than using the same dense parameters for every input.

## Intuition
A dense layer applies the same parameter set to every token. An MoE layer provides many possible parameter sets and uses a router to choose which expert handles each token.

This increases model capacity without requiring every token to use every parameter.

## Mathematical formulation
- Related math: [[Expert Routing]]
- In Switch-style MoE, a token representation `x` is routed to one expert `E_i`.
- The router computes probabilities over experts and selects the top expert.
- Only the selected expert processes that token.
- The expert layer typically replaces a transformer feed-forward sublayer, not the attention mechanism.
- [[DeepSeekMoE]] uses shared experts and routed experts to reduce redundancy and increase expert specialization.

## Historical development
Earlier MoE work predates transformers. [[2021 Switch Transformers]] makes a simplified transformer MoE practical by using top-1 expert routing inside feed-forward layers.

[[2024 DeepSeek-V3 Technical Report]] shows MoE as part of a modern LLM systems stack, combining sparse activation with attention-cache and training-system efficiency.

[[2024 DeepSeek-V2 Technical Report]] grounds the DeepSeek architecture context for shared experts, routed experts, and activated versus total parameters.

[[2024 DeepSeekMoE]] is the source note for the DeepSeekMoE mechanism itself, including fine-grained expert segmentation and shared expert isolation.

## Related papers
- [[2021 Switch Transformers]]
- [[2024 DeepSeekMoE]]
- [[2024 DeepSeek-V2 Technical Report]]
- [[2024 DeepSeek-V3 Technical Report]]

## Related concepts
- [[Expert Routing]]
- [[DeepSeekMoE]]
- [[Transformers]]
- [[Transformer Feed-Forward Networks]]
- [[Large Language Models]]
- [[LLM Training Systems]]
- [[Scaling Laws]]

## Open questions
- Needs verification: how modern MoE variants change routing, expert capacity, and token dropping.
- Needs verification: create separate notes for expert parallelism and sparse activation after additional sources.
- Needs verification: compare modern MoE variants beyond DeepSeekMoE against independent sources.

## My understanding
MoE is a capacity-scaling idea. Instead of making the whole model denser for every token, it gives the model a larger menu of transformations and activates a small part of that menu per token.

## Source notes
- [[2021 Switch Transformers]]
- [[2024 DeepSeekMoE]]
- [[2024 DeepSeek-V2 Technical Report]]
- [[2024 DeepSeek-V3 Technical Report]]

## Revision notes
