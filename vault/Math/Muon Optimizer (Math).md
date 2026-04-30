# Muon Optimizer (Math)

## Metadata
- Type: math
- Status: partially verified
- Last reviewed: 2026-04-30

## Goal
Describe the high-level mathematical structure of Muon: momentum followed by approximate orthogonalization of hidden-layer matrix updates.

## Canonical notation
- $W_t$: hidden-layer weight matrix at timestep $t$.
- $G_t$: gradient or momentum-derived update matrix for $W_t$.
- $M_t$: momentum buffer for a matrix parameter.
- $\beta$: momentum coefficient.
- $\eta$: learning rate for the Muon update.
- $\lambda$: decoupled weight decay factor.
- $A, B$: matrix dimensions for a parameter of shape $[A, B]$.
- $Ortho(G)$: idealized semi-orthogonalized version of update matrix $G$.
- $U S V^T$: singular value decomposition of $G$.

## Definitions
- Matrix parameter: a 2D hidden-layer weight tensor that Muon is intended to optimize.
- Semi-orthogonal matrix: a rectangular matrix satisfying either $O^T O = I$ or $O O^T = I$, depending on shape.
- Orthogonalized update: an update matrix whose singular values are pushed toward a common scale.
- Newton-Schulz iteration: an iterative matrix method used by the source implementation to approximate orthogonalization.

## Assumptions
- Muon is applied to hidden matrix parameters, not all model parameters.
- Embeddings, output heads, scalar/vector parameters, gains, and biases remain on an Adam-style optimizer according to the source guidance.
- The Moonshot AI scaling report keeps non-matrix parameters on AdamW and adds weight decay plus update-scale adjustment for Muon.
- Newton-Schulz details are treated at a high level here.
- Empirical performance claims are source claims, not proof of general superiority.

## Main result
Muon can be summarized as:


$$
momentum_update -> approximate_orthogonalization -> weight_update
$$

For an update matrix $G$, the idealized orthogonalization target is:


$$
Ortho(G) = U V^T
$$

where:


$$
G = U S V^T
$$

The source implementation approximates this operation with a Newton-Schulz-style iteration rather than computing the SVD directly.

## Derivation
- Start from a gradient-like matrix update for a hidden weight matrix:


$$
G_t = \nabla_W L_t(W_t)
$$

- Maintain a momentum-style update. A simplified non-Nesterov form is:


$$
M_t = \beta M_{t-1} + (1 - \beta) G_t
$$

- Orthogonalize or approximately orthogonalize the momentum-derived update:


$$
U_t = Ortho(M_t)
$$

- Apply decoupled weight decay and the Muon update:


$$
W_{t+1} = (1 - \eta \lambda) W_t - \eta U_t
$$

- [[2025 Muon is Scalable for LLM Training]] uses a practical scaled update:


$$
W_t = W_{t-1} - \eta_t (0.2 * O_t * \sqrt(\max(A, B)) + \lambda W_{t-1})
$$

The source motivates this with a theoretical update RMS of approximately:


$$
\sqrt(1 / \max(A, B))
$$

for a full-rank matrix of shape $[A, B]$.

- Skipped steps: the exact Newton-Schulz polynomial iteration, coefficient tuning, and convergence behavior are not fully derived here.
- Skipped steps: the proof of the update RMS lemma from the Moonshot AI report is not expanded here.
- Skipped steps: the relationship to Shampoo-style preconditioning is kept high-level; [[2018 Shampoo]] grounds Shampoo itself, but this note does not derive a formal equivalence between Shampoo and Muon.

## Interpretation
Muon replaces the raw or momentum-smoothed matrix update with a matrix whose singular values are more balanced. This is different from [[AdamW]], which rescales coordinates using first and second moment estimates.

[[2024 Old Optimizer New Norm]] does not settle Muon, but it helps explain why semi-orthogonal matrix updates are interesting: they correspond to a particular matrix update geometry rather than coordinatewise scaling.

In source terms, Muon is not a universal replacement for AdamW. It is a matrix-parameter optimizer that is paired with AdamW for parameter classes that are not suitable for Muon.

The 2025 scaling report reinforces that practical Muon is a hybrid optimizer recipe, not just the bare orthogonalized update: weight decay and update RMS matching are treated as necessary scaling adjustments in that source.

## Alternative formulations
- The source describes Nesterov-style momentum as the practical default.
- The implementation supports convolution filters by flattening them into a matrix-like form.
- The Moonshot AI report scales updates by matrix shape and matches update RMS to AdamW-like magnitudes.
- The source relates Muon to [[Shampoo]] and orthogonalized-gradient methods, but exact relationships should be checked against each source before making stronger claims.

## Common mistakes
- Treating Muon as an optimizer for all parameters.
- Treating Muon as simply AdamW with different hyperparameters.
- Treating empirical speedrun claims as settled broad optimizer superiority.
- Treating the 2025 scaling report as evidence for unmodified Muon; the source modifies Muon with weight decay and update scaling.
- Confusing approximate Newton-Schulz orthogonalization with exact SVD-based orthogonalization.

## Related concepts
- [[Muon Optimizer]]
- [[Newton-Schulz Iteration]]
- [[Matrix-Aware Optimizers]]
- [[Shampoo]]
- [[Preconditioning]]
- [[Steepest Descent]]
- [[AdamW]]
- [[Gradient Descent]]
- [[Weight Decay]]

## Related papers
- [[2018 Shampoo]]
- [[2024 Old Optimizer New Norm]]
- [[2024 Muon Optimizer]]
- [[2025 Muon is Scalable for LLM Training]]

## Source references
- [[2024 Muon Optimizer]]
- [[2024 Old Optimizer New Norm]]
- [[2025 Muon is Scalable for LLM Training]]

## Verification status
- Status: partially verified
- Needs verification: full Newton-Schulz derivation, exact Shampoo/Muon relationship, norm-geometry mapping, update RMS proof details, and independent large-scale empirical validation.
