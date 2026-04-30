# Matrix-Aware Optimizers

## Metadata
- Type: concept
- Status: stub
- Last reviewed: 2026-04-30

## Short definition
Matrix-aware optimizers use the structure of matrix or tensor parameters when constructing updates, rather than treating every coordinate independently.

## Intuition
Coordinatewise optimizers such as [[AdamW]] adapt each parameter coordinate separately. Matrix-aware optimizers ask whether a whole weight matrix should be updated according to its matrix geometry.

## Mathematical formulation
- Needs development.
- Current anchors: [[Muon Optimizer (Math)]], [[Shampoo]], and [[Newton-Schulz Iteration]].

## Historical development
Needs source-grounded development. [[2024 Muon Optimizer]] links Muon to [[Shampoo]] and other matrix/orthogonalization-based optimizer ideas, but those bridge sources still need separate ingests.

## Related papers
- [[2024 Muon Optimizer]]

## Related concepts
- [[Muon Optimizer]]
- [[Muon Optimizer (Math)]]
- [[Shampoo]]
- [[Newton-Schulz Iteration]]
- [[AdamW]]
- [[Optimization and Training Stability]]

## Open questions
- Needs verification: how to organize Shampoo, Muon, SOAP, and other matrix-aware optimizers into a clean design space.

## Source notes
- [[2024 Muon Optimizer]]
