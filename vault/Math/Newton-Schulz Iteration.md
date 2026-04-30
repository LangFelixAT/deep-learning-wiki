# Newton-Schulz Iteration

## Metadata
- Type: math
- Status: stub
- Last reviewed: 2026-04-30

## Goal
Track Newton-Schulz iteration as the matrix method used by [[Muon Optimizer]] for approximate update orthogonalization.

## Canonical notation
- `G`: matrix to be orthogonalized.
- `X`: iterated matrix estimate.
- `U S V^T`: singular value decomposition of `G`.

## Definitions
- Newton-Schulz iteration is an iterative matrix method.
- In the Muon source, it is used to approximate a semi-orthogonalized update matrix without computing a full SVD.

## Assumptions
- This page is currently grounded only by [[2024 Muon Optimizer]].
- Full numerical analysis is not yet ingested.

## Main result
- Needs verification: the Muon source uses a Newton-Schulz-style polynomial iteration to push update singular values toward a common scale.

## Derivation
- Needs source-grounded mathematical derivation.
- Skipped steps: convergence and coefficient selection are not yet verified.

## Interpretation
For Muon, Newton-Schulz iteration is a practical approximation tool: it makes matrix update orthogonalization cheaper than using a direct SVD.

## Alternative formulations
- The Muon source contrasts Newton-Schulz with direct SVD and coupled Newton methods.

## Common mistakes
- Treating the Muon implementation's fixed coefficients as a universal Newton-Schulz method.
- Assuming the approximation exactly equals `U V^T`.

## Related concepts
- [[Muon Optimizer]]
- [[Muon Optimizer (Math)]]
- [[Matrix-Aware Optimizers]]
- [[Shampoo]]

## Related papers
- [[2024 Muon Optimizer]]

## Source references
- [[2024 Muon Optimizer]]

## Verification status
- Status: stub
- Needs verification: full numerical-method details.
