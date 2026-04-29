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

## Historical development
Earlier MoE work predates transformers. [[2021 Switch Transformers]] makes a simplified transformer MoE practical by using top-1 expert routing inside feed-forward layers.

## Related papers
- [[2021 Switch Transformers]]

## Related concepts
- [[Expert Routing]]
- [[Transformers]]
- [[Transformer Feed-Forward Networks]]
- [[Large Language Models]]
- [[Scaling Laws]]

## Open questions
- Needs verification: how modern MoE variants change routing, expert capacity, and token dropping.
- Needs verification: create separate notes for expert parallelism and sparse activation after additional sources.

## My understanding
MoE is a capacity-scaling idea. Instead of making the whole model denser for every token, it gives the model a larger menu of transformations and activates a small part of that menu per token.

## Source notes
- [[2021 Switch Transformers]]

## Revision notes
