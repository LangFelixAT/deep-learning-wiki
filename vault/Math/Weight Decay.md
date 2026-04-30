# Weight Decay

## Metadata
- Type: math
- Status: stub
- Last reviewed: 2026-04-30

## Goal
Define weight decay and distinguish it from related regularization ideas.

## Definitions
- Weight decay is a training mechanism that penalizes or shrinks parameter magnitudes.
- Needs verification: exact equivalence or non-equivalence to L2 regularization depends on the optimizer update rule.

## Assumptions
- Needs development.

## Derivation
- Needs source-backed derivation.

## Interpretation
- [[Adam]] is an adaptive optimizer; later [[AdamW]] work is expected to clarify how weight decay should interact with Adam-style adaptive updates.

## Common mistakes
- Assuming weight decay and L2 regularization behave identically under every optimizer.
- Explaining AdamW mechanics before ingesting an AdamW source.

## Related concepts
- [[Regularization]]
- [[Adam]]
- [[AdamW]]
- [[Optimization and Training Stability]]
