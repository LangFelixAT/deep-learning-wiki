# Decoupled Weight Decay Regularization

## Metadata
- Authors: Ilya Loshchilov; Frank Hutter
- Year: 2017 preprint; published at ICLR 2019
- Venue: ICLR 2019
- Link: https://arxiv.org/abs/1711.05101
- arXiv: 1711.05101
- Source type: paper
- Status: studied
- Reliability: high
- Added: 2026-04-30

## Scope
This note focuses on the distinction between L2 regularization and weight decay, why they are equivalent for vanilla SGD but not for adaptive optimizers, and the AdamW decoupled weight decay update.

Excluded: benchmark tables, detailed experimental setup, SGDW beyond brief comparison, schedule tuning details, later optimizer variants, and modern claims not grounded in the paper.

## One-sentence summary
The paper argues that L2 regularization and weight decay are equivalent for standard SGD but not for adaptive optimizers such as Adam, and proposes AdamW by decoupling weight decay from Adam's adaptive gradient update.

## Why this paper matters
This paper grounds [[AdamW]] as a correction to how weight decay is applied with adaptive optimizers, clarifying an important distinction for modern optimizer practice.

## Problem
Common adaptive-optimizer implementations used L2 regularization while calling it weight decay, but the paper shows that these are not equivalent for adaptive gradient methods such as [[Adam]].

## Background needed
- [[Gradient Descent]]
- [[Adam]]
- [[Weight Decay]]

## Core idea
For standard SGD, adding an L2 penalty to the loss can produce the same update as multiplicative weight decay after rescaling the regularization coefficient by the learning rate.

For adaptive optimizers, the adaptive preconditioner also scales the L2 penalty gradient. Decoupled weight decay keeps the shrinkage term separate from the adaptive loss-gradient step.

## Method
The paper proposes decoupling weight decay from the gradient-based update. For AdamW, the adaptive Adam step is computed from the loss gradient, while weight decay is applied as a separate shrinkage term on parameters.

## Important equations
Standard SGD with decoupled weight decay:

```text
theta_{t+1} = (1 - lambda) theta_t - alpha grad f_t(theta_t)
```

SGD with L2-regularized loss:

```text
f_t^reg(theta) = f_t(theta) + (lambda' / 2) ||theta||_2^2
theta_{t+1} = theta_t - alpha grad f_t(theta_t) - alpha lambda' theta_t
```

These are equivalent for standard SGD when:

```text
lambda' = lambda / alpha
```

Adaptive optimizer with preconditioner `M_t` and L2 regularization:

```text
theta_{t+1} = theta_t - alpha M_t (grad f_t(theta_t) + lambda' theta_t)
```

Decoupled weight decay with adaptive optimizer:

```text
theta_{t+1} = (1 - lambda) theta_t - alpha M_t grad f_t(theta_t)
```

High-level AdamW update:

```text
theta_t = theta_{t-1} - eta_t * (alpha * hat_m_t / (sqrt(hat_v_t) + epsilon) + lambda theta_{t-1})
```

where the Adam moment estimates are computed from the loss gradient, not from the L2-augmented gradient.

## Results
The paper reports that Adam with decoupled weight decay generalizes better than Adam with L2 regularization in the studied image classification experiments.

This note does not ingest the benchmark tables or detailed experimental setup.

## Limitations
- The empirical analysis is focused on image classification settings.
- Schedule and normalized-weight-decay details are outside this ingest scope.
- The paper includes broader discussion and appendices that are not expanded here.

## Claim from source
- L2 regularization and weight decay are equivalent for standard stochastic gradient descent after rescaling by the learning rate.
- This equivalence does not hold for adaptive gradient algorithms such as Adam.
- With adaptive gradients, L2 regularization causes the regularization term to be scaled by the adaptive gradient mechanism.
- Decoupled weight decay separates parameter shrinkage from the loss-gradient update.
- The paper proposes AdamW as Adam with decoupled weight decay.

## My interpretation
AdamW is not just "Adam plus regularization." It changes where weight decay enters the computation: the decay term is kept outside Adam's coordinatewise adaptive scaling.

This matters for the wiki's optimizer track because it separates two ideas that are easy to conflate: optimizing a regularized loss and explicitly shrinking weights during an optimizer step.

## Unclear / Needs verification
- Needs verification: how AdamW interacts with later large-language-model training recipes should be grounded in separate sources.
- Needs verification: normalized weight decay and warm restarts are in the paper but intentionally not ingested here.

## Connections to concepts
- [[AdamW]]
- [[Adam]]
- [[Weight Decay]]
- [[Gradient Descent]]
- [[Optimization and Training Stability]]

## Connections to papers
- [[2014 Adam]]

## Questions
- Which later optimizer sources best explain why AdamW became the default Adam-style optimizer in many large-model recipes?
- How should AdamW be compared with Muon and matrix-aware optimizers once those sources are ingested?

## Follow-up reading
- Muon optimizer source material.
- Matrix-aware optimizer sources such as Shampoo-style methods.
