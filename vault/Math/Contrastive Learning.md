# Contrastive Learning

## Metadata
- Type: math
- Status: partially verified

## Goal
Learn representations by pulling related examples together and pushing unrelated examples apart.

## Definitions
- Source example: [[2021 CLIP]].
- A positive pair contains two views or modalities that should match, such as an image and its caption.
- A negative pair contains examples that should not match, such as an image and another image's caption.
- A similarity function scores whether two embeddings align.

## Positive vs negative pairs
- Positive: `(image_i, text_i)`.
- Negative: `(image_i, text_j)` for `j != i`.
- In a batch of `N` image-text pairs, the correct `N` pairs are positives and the other cross-pairs are negatives.

## Similarity objective
CLIP normalizes image and text embeddings and compares them with dot products, equivalent to cosine similarity after normalization:

`sim(i, t) = normalize(i) dot normalize(t)`.

The objective increases `sim(image_i, text_i)` and decreases `sim(image_i, text_j)` for mismatched `j`.

## InfoNCE-style structure
For one image embedding `i`, a light image-to-text contrastive term has the form:

`-log exp(sim(i, t_pos) / tau) / sum_j exp(sim(i, t_j) / tau)`.

CLIP uses a symmetric version: image-to-text matching and text-to-image matching are both optimized.

## Assumptions
- Positive pairs are meaningful matches.
- Negatives in the batch are treated as mismatches.
- The similarity measure is appropriate for the embedding space.
- Needs verification: exact temperature handling and batching details are source-specific.

## Derivation
- Embed each item.
- Compute pairwise similarities.
- Convert similarities into matching probabilities with a softmax.
- Apply cross-entropy so the correct pair has high probability.
- Skipped steps: gradient derivation and mutual-information interpretation.

## Interpretation
Contrastive learning makes representation geometry carry semantic information: nearby vectors should correspond to related examples, while distant vectors should correspond to unrelated examples.

## Common mistakes
- Thinking contrastive learning only applies to image-text pairs.
- Forgetting that the choice of negatives affects the learned representation.
- Treating cosine similarity as meaningfully calibrated probability by itself.
- Confusing the embedding objective with a generative likelihood.

## Related concepts
- [[CLIP]]
- [[2021 CLIP]]
