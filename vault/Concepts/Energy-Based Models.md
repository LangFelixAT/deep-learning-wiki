# Energy-Based Models

## Metadata
- Type: concept
- Status: stub

## Short definition
Model family that represents preferences with an energy function.

## Intuition
Energy-based models assign unnormalized scores or energies to data configurations. Needs development from source notes.

## Mathematical formulation
- Related math: [[Score Matching]]
- For an energy-based model `p(x) = exp(-E(x)) / Z`, the score is `grad_x log p(x) = -grad_x E(x)` because the normalization constant `Z` does not depend on `x`.

## Score-based connection
[[2019 Generative Modeling by Estimating Gradients of the Data Distribution]] notes that score matching was originally proposed for learning energy-based models and that their approach can train EBMs by using the gradient of an energy-based model as the score model.

Learning the score of an EBM corresponds to learning the gradient field of the energy function, up to sign.

## Historical development
Needs verification from source notes.

## Related concepts
- [[Diffusion Models]]
- [[Score Matching]]
- [[Score-Based Generative Models]]

## Related papers
- [[2019 Generative Modeling by Estimating Gradients of the Data Distribution]]

## Open questions
- Which source should anchor this page?
