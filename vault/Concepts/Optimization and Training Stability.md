# Optimization and Training Stability

## Metadata
- Type: concept
- Status: developing
- Last reviewed: 2026-04-30

## Short definition
Synthesis page for optimization methods and training-stability mechanisms in deep learning.

## Intuition
Optimization and stability determine whether large neural networks can be trained reliably. This track should connect optimizers, normalization, residual pathways, initialization, schedules, and numerical precision.

## Mathematical formulation
- Related math: [[Gradient Descent]], [[Steepest Descent]], [[Preconditioning]], [[Adam]], [[AdamW]], [[Weight Decay]], [[Shampoo]], [[Muon Optimizer (Math)]], [[Newton-Schulz Iteration]], [[Layer Normalization (Math)]], [[RMSNorm (Math)]], [[Notation Conventions]]

## Historical development
Current grounded anchors include [[2014 Adam]], [[2017 Decoupled Weight Decay Regularization]], [[2018 Shampoo]], [[2024 Old Optimizer New Norm]], [[2016 Layer Normalization]], and [[2019 Root Mean Square Layer Normalization]].

Adam grounds the adaptive-optimizer branch: it starts from stochastic gradient optimization, adds moving averages of first and second raw gradient moments, and uses bias correction for early timesteps.

AdamW grounds the optimizer-regularization branch: it separates [[Weight Decay]] from Adam's adaptive gradient scaling, clarifying why L2 regularization and weight decay are not interchangeable for adaptive optimizers.

Shampoo grounds the preconditioning branch: it uses matrix/tensor structure to build smaller per-dimension preconditioners instead of relying only on coordinatewise adaptive scaling.

Old Optimizer, New Norm grounds the optimizer-geometry branch: it frames optimizer design as choosing both a norm and a step size, helping compare coordinatewise and matrix-aware updates.

Muon adds a later emerging matrix-aware branch: it applies momentum to hidden-layer matrix updates and then approximately orthogonalizes those updates with [[Newton-Schulz Iteration]]. This branch is less settled than AdamW and should remain marked as emerging until more sources are ingested.

## Related papers
- [[2014 Adam]]
- [[2017 Decoupled Weight Decay Regularization]]
- [[2018 Shampoo]]
- [[2024 Old Optimizer New Norm]]
- [[2024 Muon Optimizer]]
- [[2016 Layer Normalization]]
- [[2019 Root Mean Square Layer Normalization]]

## Related concepts
- [[Normalization]]
- [[Layer Normalization]]
- [[RMSNorm]]
- [[Residual Connections]]
- [[LLM Training Systems]]
- [[Scaling Laws]]
- [[Muon Optimizer]]
- [[Matrix-Aware Optimizers]]
- [[Preconditioning]]
- [[Steepest Descent]]

## Open questions
- Needs verification: large-scale Muon validation, matrix-aware optimizer comparisons, residual scaling, and initialization need source-grounded ingests.

## My understanding
This page should become the map for why optimization choices and architecture scaffolding make deep networks trainable.

## Source notes
- [[2014 Adam]]
- [[2017 Decoupled Weight Decay Regularization]]
- [[2018 Shampoo]]
- [[2024 Old Optimizer New Norm]]
- [[2024 Muon Optimizer]]
- [[2016 Layer Normalization]]
- [[2019 Root Mean Square Layer Normalization]]

## Revision notes
- 2026-04-29: Created as a stub synthesis page.
- 2026-04-30: Added Adam as the first source-grounded adaptive optimizer anchor.
- 2026-04-30: Added AdamW and decoupled weight decay as source-grounded optimizer-regularization anchors.
- 2026-04-30: Added Muon as an emerging matrix-aware optimizer anchor from blog/repository sources.
- 2026-04-30: Added Shampoo as a source-grounded preconditioning and matrix-aware optimizer anchor.
- 2026-04-30: Added Old Optimizer, New Norm as a source-grounded optimizer-geometry and steepest-descent anchor.
