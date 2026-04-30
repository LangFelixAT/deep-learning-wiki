# Regularization

## Metadata
- Type: math
- Status: developing
- Last reviewed: 2026-04-30

## Goal
Track methods that constrain learning to improve generalization or optimization behavior.

## Definitions
- L2 regularization adds a squared-parameter penalty to the loss, often written $\frac{\lambda'}{2}\|\theta\|_2^2$.
- [[Weight Decay]] directly shrinks parameters during an optimizer step.
- [[2017 Decoupled Weight Decay Regularization]] shows that L2 regularization and weight decay are equivalent for standard SGD after coefficient rescaling, but not generally equivalent for adaptive optimizers.

## Assumptions
- The equivalence between L2 regularization and weight decay depends on the optimizer.
- Adaptive optimizer statements should be checked against the optimizer's update rule.

## Derivation
- Detailed derivations belong in [[Weight Decay]] and [[AdamW]].

## Interpretation
- Regularization can enter either through the objective being optimized or through the optimizer update itself. AdamW is important because it separates these two mechanisms for Adam-style adaptive optimization.

## Common mistakes
- Treating every parameter-shrinking mechanism as identical to L2 regularization.
- Calling L2 regularization "weight decay" without checking how the optimizer applies it.

## Related concepts
- [[Weight Decay]]
- [[AdamW]]
- [[Maximum Likelihood Estimation]]

## Related papers
- [[2017 Decoupled Weight Decay Regularization]]

## Verification status
- Status: developing
- Needs verification: broader regularization taxonomy requires separate sources.
