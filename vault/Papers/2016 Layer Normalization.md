# Layer Normalization

## Metadata
- Authors: Jimmy Lei Ba, Jamie Ryan Kiros, Geoffrey E. Hinton
- Year: 2016
- Venue: arXiv
- Link: https://arxiv.org/abs/1607.06450
- arXiv: 1607.06450
- Source type: paper
- Status: studied
- Reliability: high
- Added: 2026-04-29

## Scope
This ingest covers the foundational normalization idea: motivation for normalization, high-level contrast with batch normalization, layer-wise statistics within a single training case, mean/variance computation over summed inputs, learned gain and bias, suitability for recurrent/sequence models, and relationship to Transformer sublayer normalization.

Excluded: detailed RNN experiment results, benchmark tables, implementation tricks, modern transformer variants such as pre-norm versus post-norm, RMSNorm and later normalization methods except as future connections, and optimizer-specific discussion.

## One-sentence summary
Ba, Kiros, and Hinton introduce layer normalization, which normalizes summed inputs across features within a layer for each individual training case.

## Why this paper matters
Layer normalization became a core architectural component in sequence models and Transformers because it does not depend on mini-batch statistics and is straightforward to apply at each sequence timestep.

## Problem
Normalization can make neural network training easier, but batch normalization depends on mini-batch statistics and is awkward for recurrent neural networks, online learning, and very small mini-batches.

## Background needed
- [[Normalization]]
- [[Transformers]]
- [[Residual Connections]]
- [[Layer Normalization (Math)]]

## Core idea
Instead of computing normalization statistics across a mini-batch for each neuron, compute the mean and variance across the summed inputs of all neurons in a layer for a single training case.

Each training case gets its own normalization statistics, and learned gain and bias parameters are applied after normalization.

## Method
- For a layer with summed inputs $a_i$, compute the layer mean over hidden units.
- Compute the layer standard deviation over hidden units.
- Normalize each summed input using that mean and standard deviation.
- Apply learned per-unit gain $g_i$ and bias $b_i$.
- In recurrent networks, compute these statistics separately at each time step.

## Important equations
Layer mean:

$$
\mu = (1/H) \sum_{i=1}^H a_i
$$
Layer standard deviation:

$$
\sigma^2 = (1/H) \sum_{i=1}^H (a_i - \mu)^2
$$
$$
\sigma = \sqrt((1/H) \sum_{i=1}^H (a_i - \mu)^2)
$$
Layer-normalized activation form:

$$
h_i = f((g_i / \sigma)(a_i - \mu) + b_i)
$$
For an RNN timestep:

$$
h_t = f[(g / \sigma_t) odot (a_t - \mu_t) + b]
$$
## Results
- Claim from source: layer normalization performs the same computation at training and test time.
- Claim from source: layer normalization can be applied to recurrent neural networks by computing normalization statistics separately at each time step.
- Claim from source: the paper reports that recurrent neural networks benefit most, especially for long sequences and small mini-batches.

Detailed experiment results are outside this ingest scope.

## Limitations
- The paper reports preliminary convolutional-network experiments where batch normalization outperforms layer normalization.
- The paper predates Transformer-specific pre-norm/post-norm analysis and later normalization variants such as RMSNorm.
- The source focuses heavily on recurrent networks rather than Transformers.

## Claim from source
- Claim from source: batch normalization uses the distribution of summed inputs over a mini-batch to compute mean and variance.
- Claim from source: layer normalization computes mean and variance from all summed inputs to neurons in a layer for a single training case.
- Claim from source: unlike batch normalization, layer normalization introduces no dependency between training cases.
- Claim from source: unlike batch normalization, layer normalization performs the same computation at training and test time.
- Claim from source: layer normalization is straightforward to apply to recurrent neural networks by computing statistics separately at each time step.
- Claim from source: layer normalization provides each neuron its own adaptive bias and gain after normalization.

## My interpretation
Layer normalization is a normalization choice whose unit of normalization is the feature set inside one example, not the batch. That makes it naturally compatible with variable-length sequence models and later Transformer blocks.

## Unclear / Needs verification
- Needs verification: how the paper's recurrent-network motivation maps onto modern Transformer stability explanations.
- Needs verification: exact comparison between layer normalization and later RMSNorm should wait for a dedicated RMSNorm source.

## Connections to concepts
- [[Layer Normalization]]
- [[Layer Normalization (Math)]]
- [[Normalization]]
- [[Transformers]]
- [[Residual Connections]]

## Connections to papers
- [[2017 Attention Is All You Need]]

## Questions
- Which source should anchor pre-norm versus post-norm Transformer blocks?
- Which source should anchor RMSNorm?

## Follow-up reading
- [[2017 Attention Is All You Need]]
- RMSNorm
- modern Transformer normalization analyses
