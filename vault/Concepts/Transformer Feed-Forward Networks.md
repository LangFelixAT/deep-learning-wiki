# Transformer Feed-Forward Networks

## Metadata
- Type: concept
- Status: developing
- Last reviewed: 2026-04-29

## Short definition
Transformer feed-forward networks are position-wise MLP sublayers applied independently to each token representation.

## Intuition
Attention mixes information across positions. The feed-forward block then transforms each position's representation independently with the same learned function.

## Mathematical formulation
- Related math: [[Expert Routing]]
- In [[2017 Attention Is All You Need]], each encoder and decoder layer contains:

`FFN(x) = max(0, xW_1 + b_1) W_2 + b_2`.

- The same feed-forward network is applied separately and identically to each position.
- In [[2021 Switch Transformers]], some dense feed-forward sublayers are replaced by sparse expert feed-forward layers selected by [[Expert Routing]].
- [[2024 DeepSeekMoE]] further refines MoE feed-forward layers with fine-grained routed experts and shared experts.

## Historical development
[[2017 Attention Is All You Need]] uses position-wise feed-forward networks as the second main sublayer type in transformer blocks, alongside attention.

[[2021 Switch Transformers]] treats the feed-forward sublayer as the natural place to add [[Mixture of Experts]] capacity.

[[2024 DeepSeekMoE]] focuses on expert specialization inside MoE feed-forward layers.

## Related papers
- [[2017 Attention Is All You Need]]
- [[2021 Switch Transformers]]
- [[2024 DeepSeekMoE]]

## Related concepts
- [[Transformers]]
- [[Self-Attention]]
- [[Residual Connections]]
- [[Layer Normalization]]
- [[Mixture of Experts]]
- [[DeepSeekMoE]]
- [[Expert Routing]]

## Open questions
- Needs verification: later LLM feed-forward variants such as gated MLPs and SwiGLU should be grounded in separate source notes.
- Needs verification: modern MoE feed-forward variants should be grounded in later source notes.

## My understanding
The feed-forward block is where each token representation is nonlinearly transformed after attention has mixed sequence information.

## Source notes
- [[2017 Attention Is All You Need]]
- [[2021 Switch Transformers]]
- [[2024 DeepSeekMoE]]

## Revision notes
