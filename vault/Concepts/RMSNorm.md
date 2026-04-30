# RMSNorm

## Metadata
- Type: concept
- Status: developing
- Last reviewed: 2026-04-30

## Short definition
RMSNorm is a normalization method that rescales a layer's activations by their root mean square without subtracting their mean.

## Intuition
LayerNorm centers and rescales activations. RMSNorm asks whether the centering step is necessary. It keeps scale control by dividing by root mean square, but removes mean subtraction to make the computation simpler.

## Mathematical formulation
- Related math: [[RMSNorm (Math)]]
- RMSNorm normalizes summed inputs $a_i$ using:

$$
\operatorname{RMS}(a) = \sqrt((1/n) \sum_i a_i^2)
$$

- The normalized activation before the next nonlinearity is:

$$
bar_a_i = a_i / \operatorname{RMS}(a) * g_i
$$

- The source uses learned gain parameters $g_i$.

## Historical development
[[2019 Root Mean Square Layer Normalization]] introduces RMSNorm as a simplification of [[Layer Normalization]].

The paper frames RMSNorm around retaining re-scaling invariance while dropping re-centering invariance.

Modern LLM connection: RMSNorm later becomes relevant to transformer language model architecture, but specific adoption claims should be grounded in later model papers.

## Related papers
- [[2019 Root Mean Square Layer Normalization]]
- [[2016 Layer Normalization]]

## Related concepts
- [[Normalization]]
- [[Layer Normalization]]
- [[RMSNorm (Math)]]
- [[Transformer Architecture]]
- [[Optimization and Training Stability]]
- [[Large Language Models]]

## Open questions
- Needs verification: which model papers should anchor RMSNorm's role in modern LLMs.
- Needs verification: relationship between RMSNorm, pre-norm transformer blocks, and residual-stream stability.

## My understanding
RMSNorm is mainly a scale-control mechanism. It simplifies LayerNorm by removing mean-centering while keeping a normalization factor that prevents activation scale from freely drifting.

## Source notes
- [[2019 Root Mean Square Layer Normalization]]

## Revision notes
- 2026-04-30: Created from RMSNorm ingest.
