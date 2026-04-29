# Normalization

## Metadata
- Type: concept
- Status: developing

## Short definition
Techniques that rescale or standardize activations, weights, inputs, or gradients.

## Intuition
Normalization methods modify neural network computations so that some quantity, such as activations or summed inputs, has controlled scale and location. This can make optimization more stable or faster.

## Mathematical formulation
- Related math: [[Layer Normalization (Math)]]
- [[2016 Layer Normalization]] contrasts batch normalization and layer normalization:
  - batch normalization computes statistics across training cases in a mini-batch;
  - layer normalization computes statistics across features within one layer for a single training case.

## Historical development
[[2016 Layer Normalization]] introduces layer normalization as a normalization method that does not depend on mini-batch statistics and is straightforward to apply to recurrent networks.

## Related concepts
- [[Gradient Descent]]
- [[Transformers]]
- [[Layer Normalization]]
- [[Layer Normalization (Math)]]

## Open questions
- Needs verification: add batch normalization, weight normalization, RMSNorm, and optimizer-related normalization sources later.

## Source notes
- [[2016 Layer Normalization]]
