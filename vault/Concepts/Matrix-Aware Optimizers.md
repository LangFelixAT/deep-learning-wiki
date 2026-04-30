# Matrix-Aware Optimizers

## Metadata
- Type: concept
- Status: developing
- Last reviewed: 2026-04-30

## Short definition
Matrix-aware optimizers use the structure of matrix or tensor parameters when constructing updates, rather than treating every coordinate independently.

## Intuition
Coordinatewise optimizers such as [[AdamW]] adapt each parameter coordinate separately. Matrix-aware optimizers ask whether a whole weight matrix should be updated according to its matrix geometry.

[[2024 Old Optimizer New Norm]] sharpens this intuition: the difference is not only implementation detail, but also the norm used to measure an update.

## Mathematical formulation
- [[Preconditioning]] is the broad idea: transform the gradient before applying the update.
- [[Steepest Descent]] explains why choosing an update norm can change the direction of the update.
- [[Shampoo]] is a source-grounded example that maintains smaller preconditioners along matrix or tensor dimensions.
- [[Muon Optimizer (Math)]] is a later emerging example that changes matrix update geometry through approximate orthogonalization.

## Historical development
[[2018 Shampoo]] grounds this page as a tensor-aware preconditioning method. [[2024 Muon Optimizer]] later connects Muon to Shampoo and other matrix/orthogonalization-based optimizer ideas, but Muon should not be read back into the original Shampoo source.

[[2024 Old Optimizer New Norm]] adds a norm-geometry view: Adam-like, Shampoo-like, and related optimizers can be compared by asking which norm defines their steepest descent direction.

[[2025 Muon is Scalable for LLM Training]] adds a practical scaling lesson: matrix-aware updates may need parameter-shape-dependent scaling and a hybrid optimizer setup for non-matrix parameters.

## Related papers
- [[2018 Shampoo]]
- [[2024 Old Optimizer New Norm]]
- [[2024 Muon Optimizer]]
- [[2025 Muon is Scalable for LLM Training]]

## Related concepts
- [[Muon Optimizer]]
- [[Muon Optimizer (Math)]]
- [[Preconditioning]]
- [[Steepest Descent]]
- [[Shampoo]]
- [[Newton-Schulz Iteration]]
- [[AdamW]]
- [[Weight Decay]]
- [[Optimization and Training Stability]]

## Open questions
- Needs verification: how to organize Shampoo, Muon, SOAP, update RMS scaling, and other matrix-aware optimizers into a clean design space after more sources are ingested.

## Source notes
- [[2018 Shampoo]]
- [[2024 Old Optimizer New Norm]]
- [[2024 Muon Optimizer]]
- [[2025 Muon is Scalable for LLM Training]]
