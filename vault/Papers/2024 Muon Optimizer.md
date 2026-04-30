# Muon Optimizer

## Metadata
- Authors: Keller Jordan; Yuchen Jin; Vlado Boza; Jiacheng You; Franz Cesista; Laker Newhouse; Jeremy Bernstein
- Year: 2024
- Venue:
- Link: https://kellerjordan.github.io/posts/muon/
- arXiv:
- Source type: blog / repository
- Status: studied
- Reliability: medium
- Added: 2026-04-30

## Scope
This note ingests the Keller Jordan Muon writeup plus local captures of the KellerJordan/Muon README and implementation at a conceptual level.

Focus:
- Muon as an optimizer for hidden-layer 2D parameters
- momentum update followed by approximate orthogonalization
- Newton-Schulz iteration as the practical orthogonalization method
- why AdamW remains used for embeddings, heads, scalar/vector parameters, gains, and biases
- relationship to Shampoo and matrix-aware optimization as a high-level bridge
- empirical claims only as source claims

Excluded:
- full code implementation
- benchmark tables
- long social-thread content
- large-scale Moonshot/Kimi scaling claims except as future connections
- deep Newton-Schulz convergence proof
- full Shampoo derivation

## One-sentence summary
Muon is an emerging optimizer for hidden-layer matrix parameters that applies momentum and then approximately orthogonalizes the update using Newton-Schulz iteration before applying it to the weights.

## Why this paper matters
Although this is not a formal paper, it is the primary source for Muon and introduces a modern optimizer direction beyond coordinatewise adaptive methods such as [[AdamW]].

## Problem
The source targets neural network training efficiency and asks whether hidden-layer matrix parameters should use update geometry that reflects their matrix structure rather than only coordinatewise adaptive scaling.

## Background needed
- [[AdamW]]
- [[Gradient Descent]]
- [[Weight Decay]]
- [[Matrix-Aware Optimizers]]
- [[Newton-Schulz Iteration]]
- [[Shampoo]]

## Core idea
Muon starts from an SGD-momentum-like update for a 2D hidden weight matrix, then post-processes that update with a Newton-Schulz iteration to make it approximately semi-orthogonal.

The source positions Muon as a partial optimizer: it is used for compatible hidden matrix parameters, while AdamW remains used for scalar/vector parameters, embeddings, heads, gains, and biases.

## Method
At a high level:
1. Compute a gradient for a hidden weight matrix.
2. Update a momentum buffer.
3. Optionally use a Nesterov-style momentum update.
4. Apply Newton-Schulz-style approximate orthogonalization to the update matrix.
5. Apply decoupled weight decay and the orthogonalized update.

The repository's auxiliary optimizer uses Muon for selected matrix parameters and an Adam-style update with decoupled weight decay for non-Muon parameter groups.

## Important equations
The writeup describes orthogonalization as replacing an update matrix `G` by an approximately nearest semi-orthogonal matrix:


$$
Ortho(G) = argmin_O ||O - G||_F
$$

subject to one of the semi-orthogonality constraints:


$$
O^T O = I
$$

or


$$
O O^T = I
$$

If $G = U S V^T$, the idealized orthogonalized update is:


$$
Ortho(G) = U V^T
$$

The source uses Newton-Schulz iteration as a practical approximate method instead of computing a full SVD.

## Results
Claim from source:
- The writeup reports speedrun and training-efficiency results for NanoGPT and CIFAR-10 settings.
- The README links to benchmark records and later scaling reports.

These are not treated here as settled consensus. They should be re-evaluated with later empirical sources such as the Moonshot/Kimi scaling report and other independent comparisons.

## Limitations
- The main source is a blog/repository source, not a peer-reviewed paper.
- The source itself lists open questions about scale, distributed Newton-Schulz computation, and whether Muon works outside pretraining.
- The relationship to [[Shampoo]] is only sketched here; exact comparisons should use [[2018 Shampoo]] and later sources.
- The relationship to Bernstein-Newhouse's norm framing needs a separate source ingest.

## Claim from source
- Muon is designed for hidden-layer 2D parameters.
- Muon applies momentum before orthogonalizing the update.
- Newton-Schulz iteration is used as a practical approximate orthogonalization method.
- Scalar/vector parameters, embeddings, output heads, gains, and biases should generally remain on AdamW according to the source.
- The implementation applies decoupled weight decay in an AdamW-style way.
- The source links Muon conceptually to Shampoo-style matrix-aware optimization.
- The source reports empirical improvements on competitive training tasks, but those claims should remain source-labeled.

## My interpretation
Muon is best understood as a shift from coordinatewise optimizer thinking toward matrix-structured update geometry. AdamW adapts individual coordinates; Muon tries to shape the update for whole hidden weight matrices.

This makes Muon a natural next step in the wiki after [[Adam]] and [[AdamW]], but it should be treated as emerging and less settled than those older optimizer anchors.

## Unclear / Needs verification
- Needs verification: whether Muon remains robust at much larger training scales.
- Needs verification: whether Muon works well for finetuning or reinforcement-learning workloads.
- Needs verification: how to compare Muon fairly against heavily tuned AdamW and matrix-aware optimizers.
- Needs verification: the precise mathematical relationship between Muon, [[Shampoo]], and norm-based optimizer views.

## Connections to concepts
- [[Muon Optimizer]]
- [[Muon Optimizer (Math)]]
- [[Newton-Schulz Iteration]]
- [[Matrix-Aware Optimizers]]
- [[Shampoo]]
- [[AdamW]]
- [[Optimization and Training Stability]]

## Connections to papers
- [[2014 Adam]]
- [[2017 Decoupled Weight Decay Regularization]]
- [[2018 Shampoo]]

## Questions
- Which later source best validates Muon at LLM scale?
- How should matrix-aware optimizers be organized relative to coordinatewise adaptive optimizers?

## Follow-up reading
- Shampoo: Preconditioned Stochastic Tensor Optimization.
- [[2024 Old Optimizer New Norm]]
- Muon is Scalable for LLM Training.
