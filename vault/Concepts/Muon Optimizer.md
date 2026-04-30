# Muon Optimizer

## Metadata
- Type: concept
- Status: developing
- Last reviewed: 2026-04-30

## Short definition
Muon is an emerging neural network optimizer that applies momentum to hidden-layer matrix gradients and then approximately orthogonalizes the resulting update.

## Intuition
AdamW treats parameters largely through coordinatewise adaptive scaling. Muon instead focuses on 2D hidden weight matrices and asks whether the whole update matrix should be shaped before it is applied.

The central intuition is that hidden-layer matrix updates may be dominated by a few directions. Orthogonalizing the update is intended to spread update strength across matrix directions.

## Mathematical formulation
- Detailed math lives in [[Muon Optimizer (Math)]].
- The high-level operation is:
  - compute a momentum-style update matrix
  - approximately apply `Ortho(G)`
  - update the weight matrix using the orthogonalized update

## Historical development
Muon appears in this wiki after [[Adam]] and [[AdamW]] as a newer optimizer direction. It is not yet as historically settled as those sources.

The first source-grounded anchor here is [[2024 Muon Optimizer]], a blog/repository source. [[2018 Shampoo]] now grounds the older tensor-aware preconditioning side of the matrix-aware optimizer branch.

[[2024 Old Optimizer New Norm]] gives a supporting geometry lens for semi-orthogonal matrix updates, but it should not be treated as proof that practical Muon is broadly superior.

## Related papers
- [[2024 Muon Optimizer]]
- [[2018 Shampoo]]
- [[2024 Old Optimizer New Norm]]
- [[2014 Adam]]
- [[2017 Decoupled Weight Decay Regularization]]

## Related concepts
- [[Muon Optimizer (Math)]]
- [[Newton-Schulz Iteration]]
- [[Matrix-Aware Optimizers]]
- [[Shampoo]]
- [[Steepest Descent]]
- [[AdamW]]
- [[Weight Decay]]
- [[Optimization and Training Stability]]
- [[Transformer Feed-Forward Networks]]
- [[Attention]]

## Open questions
- Needs verification: whether Muon should be treated as a generally useful optimizer or primarily as an emerging empirical result.
- Needs verification: the exact mathematical and empirical comparison between Muon, [[Shampoo]], and the norm-geometry view.
- Needs verification: how Muon behaves for finetuning and reinforcement-learning workloads.

## My understanding
Muon is important because it points toward optimizer design that depends on parameter role and tensor shape. It should be studied as part of the broader move from scalar/coordinatewise optimization toward matrix-aware training methods.

## Source notes
- [[2024 Muon Optimizer]]
- [[2018 Shampoo]]
- [[2024 Old Optimizer New Norm]]
