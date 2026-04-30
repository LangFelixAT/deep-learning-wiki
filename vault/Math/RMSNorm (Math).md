# RMSNorm (Math)

## Metadata
- Type: math
- Status: partially verified
- Last reviewed: 2026-04-30

## Goal
Define the RMSNorm operation from [[2019 Root Mean Square Layer Normalization]] and contrast it with [[Layer Normalization (Math)]].

## Canonical notation
- $a_i$: summed input or activation component for feature $i$
- $n$: number of features in the normalized vector
- $a$: vector of summed inputs
- $\operatorname{RMS}(a)$: root mean square of $a$
- $g_i$: learned gain for feature $i$
- $bar_a_i$: normalized value for feature $i$
- $p$: partial ratio used by pRMSNorm, written as a fraction
- $k$: number of features used for partial RMS estimation

## Definitions
- Source: [[2019 Root Mean Square Layer Normalization]].
- RMSNorm normalizes by the root mean square of activations.
- Unlike LayerNorm, RMSNorm does not subtract the mean.
- The source argues that this preserves re-scaling invariance while dropping re-centering invariance.
- pRMSNorm estimates RMS from a subset of features.

## Assumptions
- The normalization is applied across features within one training case.
- This note follows the paper's feed-forward notation and does not claim a specific modern LLM implementation.
- For pRMSNorm, the source assumes an approximately independent identically distributed structure among neurons when motivating subset estimation.

## Main result
RMS statistic:

$$
\operatorname{RMS}(a) = \sqrt((1/n) \sum_{i=1}^n a_i^2)
$$
RMSNorm:

$$
bar_a_i = a_i / \operatorname{RMS}(a) * g_i
$$
pRMSNorm:

$$
RMS_p(a) = \sqrt{(1/k) \sum_{i=1}^k a_i^2}, \quad k = \lceil n p \rceil
$$
## Derivation
- Start with a vector of summed inputs $a = (a_1, ..., a_n)$.
- LayerNorm computes a mean $\mu$ and standard deviation $\sigma$.
- RMSNorm removes the mean computation.
- Compute the root mean square of the vector.
- Divide each component by the RMS.
- Apply learned gain $g_i$.

For positive scale $\alpha$, re-scaling invariance follows from RMS linearity:

$$
\operatorname{RMS}(\alpha a) = \alpha \operatorname{RMS}(a)
$$
Then:

$$
\alpha a_i / \operatorname{RMS}(\alpha a) = \alpha a_i / (\alpha \operatorname{RMS}(a)) = a_i / \operatorname{RMS}(a)
$$
Skipped steps:
- Full gradient derivation from the paper.
- Full invariance table comparison across BatchNorm, WeightNorm, LayerNorm, RMSNorm, and pRMSNorm.
- Formal analysis of pRMSNorm estimator accuracy.

## Interpretation
RMSNorm controls activation scale without forcing zero mean. The key simplification is removing mean-centering, which reduces computation and changes the invariance properties compared with LayerNorm.

The source interprets RMSNorm's behavior as preserving re-scaling invariance and providing implicit learning-rate adaptation through gradient behavior. This note does not fully verify the gradient analysis.

## Alternative formulations
- [[Layer Normalization (Math)]] subtracts the mean and divides by standard deviation.
- pRMSNorm estimates the RMS from a subset of features.
- Batch normalization and weight normalization normalize different quantities and have different dependency structures.

## Common mistakes
- Treating RMSNorm as LayerNorm with a different name.
- Forgetting that RMSNorm does not re-center activations.
- Assuming RMSNorm preserves all LayerNorm invariance properties.
- Treating pRMSNorm as always faster; the source says empirical speed improvements were not consistent.
- Using modern LLM RMSNorm claims as if they were claims from the 2019 paper.

## Related concepts
- [[RMSNorm]]
- [[Normalization]]
- [[Layer Normalization]]
- [[Layer Normalization (Math)]]
- [[Optimization and Training Stability]]
- [[Transformer Architecture]]

## Related papers
- [[2019 Root Mean Square Layer Normalization]]
- [[2016 Layer Normalization]]

## Source references
- [[2019 Root Mean Square Layer Normalization]]

## Verification status
- Status: partially verified
- Needs verification: full gradient analysis and implicit learning-rate adaptation claim.
- Needs verification: exact conventions used by later LLM implementations.
