# Steepest Descent

## Metadata
- Type: math
- Status: partially verified
- Last reviewed: 2026-04-30

## Goal
Define steepest descent as an optimization step whose direction depends on the norm used to measure updates.

## Canonical notation
- $g$: gradient vector or flattened gradient.
- $G$: matrix gradient.
- `delta`: proposed update vector.
- `Delta W`: proposed matrix update.
- $\lambda$: sharpness or quadratic-penalty scale in the local model.
- $\|\cdot\|$: chosen update norm.
- $\|\cdot\|_*$: dual norm.

## Definitions
- Steepest descent: choose the update that minimizes a linearized loss plus a quadratic penalty on the update norm.
- Update norm: the norm used to measure how large a proposed update is.
- Dual norm: the norm that appears when maximizing gradient alignment under a unit update-norm constraint.
- Induced operator norm: a matrix norm induced by input and output vector norms.

## Assumptions
- The loss is locally approximated by a first-order linear term.
- The norm and $\lambda$ are chosen before the update.
- This page follows the high-level structure from [[2024 Old Optimizer New Norm]] and skips proof details.

## Main result
The generic steepest descent step solves:


$$
\arg\min_{\delta}\left[g^T \delta + \frac{\lambda}{2}\|\delta\|^2\right]
$$

The choice of norm affects the update direction. The solution can be viewed as:


- step size: proportional to $\frac{\|g\|_*}{\lambda}$
- step direction: the unit-norm direction most aligned with $g$

## Derivation
- Start from a first-order local model of the loss:


$$
L(\theta + \delta) \approx L(\theta) + g^T \delta
$$

- Penalize update size using a chosen norm:


$$
g^T \delta + \frac{\lambda}{2}\|\delta\|^2
$$

- Write `delta` as a magnitude times a unit-norm direction.
- The best direction is the unit-norm vector that maximizes alignment with the gradient.
- The best magnitude is controlled by the dual norm of the gradient and by $\lambda$.
- Skipped steps: proof of the dual-norm formula and modular norm propositions.

## Interpretation
Steepest descent is not one optimizer. It is a family of optimizers indexed by the norm used to measure updates.

Under Euclidean or Frobenius norms, the update resembles vanilla [[Gradient Descent]]. Under infinity-norm-like geometry, the update can become sign-descent-like. Under matrix spectral-norm geometry, the update can become semi-orthogonal, which connects to the Shampoo/Muon branch of [[Matrix-Aware Optimizers]].

## Alternative formulations
- For matrix parameters, the norm may be an induced operator norm rather than a norm on a flattened vector.
- A modular norm can assign different norms to different layers or tensors.
- Needs verification: practical optimizers add momentum, EMA, weight decay, and numerical stabilization, so the clean steepest descent step is only part of the full training algorithm.

## Common mistakes
- Assuming steepest descent always means Euclidean gradient descent.
- Treating the learning rate as the only design choice while ignoring the update norm.
- Flattening every matrix parameter without asking whether the layer role suggests a different norm.
- Treating no-EMA theoretical equivalences as exact descriptions of practical Adam, Shampoo, or Muon.

## Related concepts
- [[Gradient Descent]]
- [[Preconditioning]]
- [[Shampoo]]
- [[Muon Optimizer]]
- [[Matrix-Aware Optimizers]]
- [[Adam]]
- [[AdamW]]
- [[Optimization and Training Stability]]

## Related papers
- [[2024 Old Optimizer New Norm]]
- [[2018 Shampoo]]
- [[2014 Adam]]

## Source references
- [[2024 Old Optimizer New Norm]]

## Verification status
- Status: partially verified
- Needs verification: detailed proof steps and broader links to mirror descent, natural gradient, and second-order methods require separate sources.
