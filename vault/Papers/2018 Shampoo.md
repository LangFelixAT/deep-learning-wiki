# Shampoo: Preconditioned Stochastic Tensor Optimization

## Metadata
- Authors: Vineet Gupta; Tomer Koren; Yoram Singer
- Year: 2018
- Venue: arXiv preprint
- Link: https://arxiv.org/abs/1802.09568
- arXiv: 1802.09568
- Source type: paper
- Status: studied
- Reliability: high
- Added: 2026-04-30

## Scope
This note focuses on Shampoo as structure-aware preconditioning for matrix and tensor parameters: why preconditioning is useful, why full-matrix preconditioning is expensive, how Shampoo maintains per-dimension preconditioners, and why this matters for [[Matrix-Aware Optimizers]].

Excluded: full convergence proof, matrix trace inequality derivations, detailed benchmark tables, implementation details, distributed Shampoo variants, SOAP, Muon derivation, and large-scale LLM training claims.

## One-sentence summary
Shampoo is a preconditioned stochastic optimizer that approximates full-matrix adaptive preconditioning for tensor parameters by maintaining smaller preconditioners along each tensor dimension.

## Why this paper matters
Shampoo anchors the wiki's matrix-aware optimizer branch before [[Muon Optimizer]]: it shows how optimizer updates can use matrix or tensor structure rather than only coordinatewise scaling.

## Problem
Full-matrix preconditioning can capture relationships between parameters, but for large neural network layers the full preconditioner is too large to store and too expensive to update.

## Background needed
- [[Gradient Descent]]
- [[Adam]]
- [[AdamW]]
- [[Preconditioning]]
- [[Matrix-Aware Optimizers]]

## Core idea
Many neural network parameters are naturally matrices or tensors. Shampoo uses this structure by maintaining separate preconditioning matrices for each dimension, rather than flattening the whole tensor and building one enormous preconditioner.

## Method
For a matrix parameter $W_t$ and gradient $G_t$, Shampoo maintains a left preconditioner and a right preconditioner:


$$
L_t = L_{t-1} + G_t G_t^T
R_t = R_{t-1} + G_t^T G_t
$$

The update uses matrix inverse powers on both sides of the gradient:


$$
W_{t+1} = W_t - \eta L_t^{-1/4} G_t R_t^{-1/4}
$$

For higher-order tensors, the source generalizes this idea by maintaining one preconditioner per tensor dimension and applying the inverse factors along those dimensions.

## Important equations
Matrix Shampoo update:


$$
L_t = L_{t-1} + G_t G_t^T
R_t = R_{t-1} + G_t^T G_t
W_{t+1} = W_t - \eta L_t^{-1/4} G_t R_t^{-1/4}
$$

The source initializes preconditioners with a small positive multiple of the identity for numerical stability.

Needs verification: exact tensor notation and exponent placement should be checked before using the tensor update as a derivation source in other notes.

## Results
The paper reports faster convergence than commonly used stochastic optimization methods in its experiments, with per-step runtime claimed to be comparable to SGD, AdaGrad, and Adam in the reported settings.

This note does not ingest benchmark tables.

## Limitations
- The convergence analysis is not expanded in this wiki note.
- The source's experimental results should not be treated as broad modern LLM optimizer evidence.
- Shampoo requires matrix inverse powers or approximations, so its practical cost depends on parameter shapes and implementation choices.

## Claim from source
- Preconditioned gradient methods are powerful but full preconditioning is often prohibitively expensive.
- Machine learning parameter spaces often have tensor structure, such as matrices for dense layers and higher-order tensors for convolution filters.
- Shampoo maintains a set of preconditioning matrices, each operating on a single tensor dimension.
- In the matrix case, Shampoo uses left and right preconditioners instead of one full preconditioner over the flattened parameter.
- The paper provides convergence guarantees in a stochastic convex setting.
- The proof relies on new matrix trace inequalities.
- The paper reports empirical convergence improvements over commonly used optimizers in its experiments.

## My interpretation
Shampoo is best understood as a bridge between coordinatewise adaptive optimizers such as [[Adam]] or [[AdamW]] and more geometric optimizers that reason about whole matrices. It does not merely change the scalar learning rate; it changes the geometry of the update.

## Unclear / Needs verification
- Needs verification: how much of Shampoo's theoretical framing transfers to nonconvex large-scale neural network training.
- Needs verification: practical comparisons with modern optimizers should use later sources.

## Connections to concepts
- [[Shampoo]]
- [[Preconditioning]]
- [[Matrix-Aware Optimizers]]
- [[Optimization and Training Stability]]
- [[Muon Optimizer]]

## Connections to papers
- [[2014 Adam]]
- [[2017 Decoupled Weight Decay Regularization]]
- [[2024 Muon Optimizer]]

## Questions
- How should Shampoo be compared with AdamW when the parameter has strong matrix structure?
- Which practical costs matter most: storing preconditioners, computing inverse powers, or applying the preconditioned update?
- How should Shampoo's tensor-aware update geometry be compared with Muon's orthogonalized update geometry?

## Follow-up reading
- [[2024 Muon Optimizer]]
- SOAP and distributed Shampoo sources, later.
