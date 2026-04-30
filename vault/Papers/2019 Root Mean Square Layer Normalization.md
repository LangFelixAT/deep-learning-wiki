# Root Mean Square Layer Normalization

## Metadata
- Authors: Biao Zhang; Rico Sennrich
- Year: 2019
- Venue: NeurIPS 2019
- Link: https://arxiv.org/abs/1910.07467
- arXiv: 1910.07467
- Source type: paper
- Status: studied
- Reliability: high
- Added: 2026-04-30

## Scope
This ingest focuses on why [[Layer Normalization]] can be simplified, RMS normalization without mean-centering, learned gain parameters, relationship to LayerNorm, computational simplicity, role in sequence and transformer models, and later relevance to modern LLMs as a connection.

Excluded: detailed benchmark tables, full RNN experiment details, modern LLM claims not made by the paper, and optimizer discussion beyond training-stability context.

## One-sentence summary
Zhang and Sennrich propose [[RMSNorm]], a simplification of [[Layer Normalization]] that normalizes by root mean square without subtracting the mean, aiming to preserve re-scaling invariance while reducing computational overhead.

## Why this paper matters
The paper gives a source-grounded normalization variant that helps connect [[Layer Normalization]] to later transformer and LLM architecture choices without treating all normalization methods as equivalent.

## Problem
LayerNorm can stabilize training and improve convergence, but it adds computation to every normalized layer. The paper asks whether the mean-centering part of LayerNorm is necessary for its benefits.

## Background needed
- [[Normalization]]
- [[Layer Normalization]]
- [[Layer Normalization (Math)]]
- [[Transformers]]
- [[Optimization and Training Stability]]

## Core idea
RMSNorm removes the re-centering operation from LayerNorm and normalizes activations using only their root mean square. The source hypothesizes that re-scaling invariance is the important property and that re-centering invariance is dispensable.

## Method
- Start from LayerNorm's normalization of summed inputs with mean and variance.
- Remove the mean subtraction.
- Compute the RMS of the summed inputs.
- Divide each summed input by the RMS.
- Apply a learned gain parameter.
- Optionally estimate RMS from a subset of inputs in partial RMSNorm, or pRMSNorm.

## Important equations
LayerNorm background:

$$
\mu = (1/n) \sum_i a_i
$$

$$
\sigma = \sqrt((1/n) \sum_i (a_i - \mu)^2)
$$

$$
bar_a_i = (a_i - \mu) / \sigma * g_i
$$

RMSNorm:

$$
\operatorname{RMS}(a) = \sqrt((1/n) \sum_i a_i^2)
$$

$$
bar_a_i = a_i / \operatorname{RMS}(a) * g_i
$$

Linearity property used for re-scaling invariance:

For positive scale $\alpha$:

$$
\operatorname{RMS}(\alpha x) = \alpha \operatorname{RMS}(x)
$$

pRMSNorm estimates RMS from the first $p\%$ of summed inputs. If $p$ is written as a fraction, then:

$$
RMS_p(a) = \sqrt{(1/k) \sum_{i=1}^k a_i^2}, \quad k = \lceil n p \rceil
$$
## Results
- Claim from source: RMSNorm achieves comparable performance to LayerNorm across the paper's evaluated tasks while reducing running time.
- Claim from source: the paper reports speedups of 7% to 64% across different models and implementations.
- Claim from source: pRMSNorm can be competitive with RMSNorm, but the paper does not consistently observe empirical speed improvements for pRMSNorm.
- Claim from source: speed improvements depend on framework, hardware, architecture, and the relative cost of other model components.

## Limitations
- The experiments cover several architectures and tasks, but the paper predates current large decoder-only LLM training practice.
- The paper's modern relevance to LLMs is a later connection, not a claim made by the source.
- The gradient and invariance analyses are not fully re-derived in this wiki ingest.
- pRMSNorm is presented as theoretically faster, but the source says empirical speed improvements are not consistent.

## Claim from source
- LayerNorm handles both re-centering and re-scaling invariance.
- RMSNorm removes the re-centering operation and preserves re-scaling invariance.
- RMSNorm is computationally simpler than LayerNorm.
- RMSNorm gives the model re-scaling invariance and implicit learning-rate adaptation ability according to the source.
- RMSNorm can be used as a drop-in replacement for LayerNorm in the evaluated settings.
- RMSNorm achieves comparable performance to LayerNorm while reducing running time in the paper's experiments.

## My interpretation
RMSNorm is a useful normalization bridge for the wiki: it keeps the scale-control intuition of LayerNorm while removing mean-centering. For the modern transformer path, it is best treated as part of the training-stability and architecture-scaffolding track, not as an optimizer.

## Unclear / Needs verification
- Needs verification: how RMSNorm became standard in later LLM architectures should be grounded in model-specific sources.
- Needs verification: full gradient analysis and implicit learning-rate adaptation should be checked before expanding [[RMSNorm (Math)]].
- Needs verification: pRMSNorm should stay secondary unless later sources use it.

## Connections to concepts
- [[RMSNorm]]
- [[Normalization]]
- [[Layer Normalization]]
- [[Optimization and Training Stability]]
- [[Transformer Architecture]]
- [[Large Language Models]]

## Connections to papers
- [[2016 Layer Normalization]]
- [[2017 Attention Is All You Need]]

## Questions
- Which later LLM architecture source should ground widespread RMSNorm usage?
- Should pRMSNorm get its own note, or stay as a subsection of [[RMSNorm (Math)]]?

## Follow-up reading
- [[2016 Layer Normalization]]
- Future RMSNorm usage in modern LLM architecture papers.
