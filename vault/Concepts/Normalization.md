# Normalization

## Metadata
- Type: concept
- Status: developing

## Short definition
Techniques that rescale or standardize activations, weights, inputs, or gradients.

## Intuition
Normalization methods modify neural network computations so that some quantity, such as activations or summed inputs, has controlled scale and location. This can make optimization more stable or faster.

## Mathematical formulation
- Related math: [[Layer Normalization (Math)]], [[RMSNorm (Math)]]
- [[2016 Layer Normalization]] contrasts batch normalization and layer normalization:
  - batch normalization computes statistics across training cases in a mini-batch;
  - layer normalization computes statistics across features within one layer for a single training case.
- [[2019 Root Mean Square Layer Normalization]] introduces [[RMSNorm]], which removes LayerNorm's mean-centering step and normalizes by root mean square.

## Historical development
[[2016 Layer Normalization]] introduces layer normalization as a normalization method that does not depend on mini-batch statistics and is straightforward to apply to recurrent networks.

[[2019 Root Mean Square Layer Normalization]] proposes RMSNorm as a simpler normalization method that preserves re-scaling invariance while dropping re-centering invariance.

## Related concepts
- [[Gradient Descent]]
- [[Transformers]]
- [[Layer Normalization]]
- [[Layer Normalization (Math)]]
- [[RMSNorm]]
- [[RMSNorm (Math)]]
- [[Optimization and Training Stability]]

## Open questions
- Needs verification: add batch normalization, weight normalization, and optimizer-related normalization sources later.

## Source notes
- [[2016 Layer Normalization]]
- [[2019 Root Mean Square Layer Normalization]]
