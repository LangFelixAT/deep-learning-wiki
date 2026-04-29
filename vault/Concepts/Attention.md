# Attention

## Metadata
- Type: concept
- Status: developing

## Short definition
Mechanism for weighting information by relevance.

## Intuition
Attention maps a query and a set of key-value pairs to an output. The output is a weighted sum of values, where weights come from how compatible the query is with each key.

## Mathematical formulation
- Related math: [[Scaled Dot-Product Attention]], [[Self-Attention]]
- In [[2017 Attention Is All You Need]], attention uses queries `Q`, keys `K`, and values `V`.
- The attention weights are produced by applying softmax to query-key compatibility scores.

## Historical development
[[2017 Attention Is All You Need]] uses attention as the central sequence operation inside the Transformer architecture.

## Related papers
- [[2017 Attention Is All You Need]]

## Related concepts
- [[Transformers]]
- [[Self-Attention]]
- [[Multi-Head Attention]]
- [[Scaled Dot-Product Attention]]

## Open questions
- Needs verification: add earlier attention sources to distinguish pre-transformer attention from transformer self-attention.

## Source notes
- [[2017 Attention Is All You Need]]
