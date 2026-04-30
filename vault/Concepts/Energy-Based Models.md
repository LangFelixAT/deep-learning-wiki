# Energy-Based Models

## Metadata
- Type: concept
- Status: stub

## Short definition
Model family that represents preferences with an energy function.

## Intuition
Energy-based models assign unnormalized scores or energies to data configurations. Low energy corresponds to more preferred or more compatible configurations.

This page is still a stub because the wiki has not yet ingested a dedicated EBM anchor source.

## Mathematical formulation
- Related math: [[Score Matching]]
- For an energy-based model `p(x) = exp(-E(x)) / Z`, the score is `grad_x log p(x) = -grad_x E(x)` because the normalization constant `Z` does not depend on `x`.

## Score-based connection
[[2019 Generative Modeling by Estimating Gradients of the Data Distribution]] notes that score matching was originally proposed for learning energy-based models and that their approach can train EBMs by using the gradient of an energy-based model as the score model.

Learning the score of an EBM corresponds to learning the gradient field of the energy function, up to sign.

## Historical development
Needs verification from dedicated source notes. The current grounded connection comes through [[2019 Generative Modeling by Estimating Gradients of the Data Distribution]], which links score matching to energy-based modeling.

## Related concepts
- [[Generative Modeling]]
- [[Diffusion Models]]
- [[Score Matching]]
- [[Score-Based Generative Models]]
- [[Denoising]]

## Related papers
- [[2019 Generative Modeling by Estimating Gradients of the Data Distribution]]

## Open questions
- Which source should anchor this page?
- Needs verification: energy-based transformers and JEPA/world-model connections should not be added here until grounded by dedicated sources.
