# Old Optimizer, New Norm

## Metadata
- Authors: Jeremy Bernstein; Laker Newhouse
- Year: 2024
- Venue: OPT2024 workshop; arXiv preprint
- Link: https://arxiv.org/abs/2409.20325
- arXiv: 2409.20325
- Source type: paper
- Status: studied
- Reliability: high
- Added: 2026-04-30

## Scope
This note focuses on optimizer update geometry: why the norm used to measure updates matters, how steepest descent depends on the chosen norm, how matrix-valued parameters differ from flattened coordinatewise parameters, and how Shampoo-like and Muon-like methods fit into a broader optimizer-geometry view.

Excluded: full proof details, long derivations, implementation details, benchmark details, unsupported claims about LLM-scale superiority, and treating Muon as settled consensus.

## One-sentence summary
The paper argues that several optimizers can be understood as first-order steepest descent methods under different norms, making optimizer design partly a problem of choosing the right geometry for each parameter type.

## Why this paper matters
This source gives the wiki a conceptual bridge between [[Adam]], [[Shampoo]], [[Preconditioning]], [[Matrix-Aware Optimizers]], and [[Muon Optimizer]] by explaining optimizer behavior through update norms rather than only through second-order or convex-analysis stories.

## Problem
Deep learning optimizers are often explained through convex optimization or approximate second-order intuition. The paper asks whether some optimizer behavior can instead be explained as first-order steepest descent under carefully chosen norms.

## Background needed
- [[Gradient Descent]]
- [[Steepest Descent]]
- [[Preconditioning]]
- [[Adam]]
- [[Shampoo]]
- [[Matrix-Aware Optimizers]]

## Core idea
Steepest descent chooses an update by minimizing a local linear model of the loss plus a quadratic penalty on the update norm. Changing the norm can change the update direction, not just its magnitude.

The paper uses this lens to reinterpret Adam, Shampoo, and Prodigy after disabling exponential moving averages.

## Method
The source starts from the steepest descent objective:


$$
arg min_delta [ g^T delta + (\lambda / 2) ||delta||^2 ]
$$

It then studies which update direction is produced by different choices of norm:
- Euclidean/Frobenius norms lead to gradient-descent-like updates.
- Infinity-norm and related max-of-max norms lead to sign-descent-like updates, connecting to Adam without exponential moving averages.
- Spectral-norm geometry for matrices leads to semi-orthogonal update directions, connecting to Shampoo without accumulation.

## Important equations
Generic steepest descent objective:


$$
arg min_delta [ g^T delta + (\lambda / 2) ||delta||^2 ]
$$

The source separates the solution into:
- a step size depending on the dual norm of the gradient
- a direction that maximizes alignment with the gradient under a unit-norm constraint

For Shampoo without accumulation, the source writes the matrix update as:


$$
(G G^T)^(-1/4) G (G^T G)^(-1/4) = U V^T
$$

where:


$$
G = U S V^T
$$

This connects Shampoo-style updates to semi-orthogonal matrix directions.

## Results
This paper is primarily conceptual and theoretical. It presents optimizer reinterpretations and proofs, not benchmark-focused empirical claims.

## Limitations
- The main arguments analyze optimizers after disabling exponential moving averages or accumulation, so the full practical optimizer is only partly explained by the clean steepest descent view.
- The source does not settle which norms are best for modern LLM training.
- The paper's Muon relevance is a later wiki connection, not a central source claim in this note.

## Claim from source
- Adam, Shampoo, and Prodigy can be interpreted as steepest descent methods under particular norms after switching off exponential moving averages or accumulation.
- Steepest descent separates optimizer design into choosing a norm and choosing a step size.
- Adam without exponential moving averages reduces to sign gradient descent.
- Shampoo without accumulation produces semi-orthogonal matrix updates.
- Shampoo without accumulation can be interpreted as steepest descent under a spectral norm over layers.
- Linear layers and embedding layers can have the same matrix weight space while playing different roles, so they may deserve different norms.
- The paper argues for choosing norms based on the role each tensor plays in the network.

## My interpretation
This paper sharpens the wiki's optimizer map: [[AdamW]] is not only "adaptive learning rates", [[Shampoo]] is not only "matrix preconditioning", and [[Muon Optimizer]] is not only "Newton-Schulz". These methods can be compared by asking what geometry their updates impose on vectors, matrices, or tensors.

The most useful bridge for this wiki is that Shampoo's no-accumulation update and Muon's idealized orthogonalized update both point toward semi-orthogonal matrix update geometry. Needs verification: this is a conceptual bridge, not a formal equivalence between practical Shampoo and practical Muon.

## Unclear / Needs verification
- Needs verification: how much of the no-EMA/no-accumulation analysis predicts behavior of practical optimizers with momentum, EMA, accumulation, and weight decay.
- Needs verification: which norm choices are best for transformer layers, embeddings, attention projections, and feed-forward matrices.
- Needs verification: Muon comparisons should be grounded by Muon-specific and independent empirical sources.

## Connections to concepts
- [[Steepest Descent]]
- [[Preconditioning]]
- [[Shampoo]]
- [[Muon Optimizer]]
- [[Matrix-Aware Optimizers]]
- [[Optimization and Training Stability]]
- [[Adam]]
- [[AdamW]]

## Connections to papers
- [[2014 Adam]]
- [[2018 Shampoo]]
- [[2024 Muon Optimizer]]

## Questions
- Which layer roles in transformers should receive different update norms?
- Is Muon best understood as a practical way to approximate the semi-orthogonal update direction emphasized by the Shampoo geometry story?
- How should EMA, momentum, accumulation, and weight decay be added back into the clean steepest descent picture?

## Follow-up reading
- [[2018 Shampoo]]
- [[2024 Muon Optimizer]]
- Later Muon scaling and independent optimizer comparison sources.
