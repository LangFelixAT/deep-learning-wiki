# Rotary Position Embedding (Math)

## Metadata
- Type: math
- Status: partially verified
- Last reviewed: 2026-04-29

## Goal
Define the rotary position embedding operation used in [[2021 RoFormer]].

## Canonical notation
- `x_m`: token representation at position `m`
- `W_q`, `W_k`: query and key projection matrices
- `R^d_{Theta,m}`: block-diagonal rotary matrix for position `m`
- `theta_i`: frequency for coordinate pair `i`
- `q_m`, `k_n`: position-encoded query and key vectors

## Definitions
- Source: [[2021 RoFormer]].
- RoPE applies position-dependent rotations to query and key vectors.
- For even dimension `d`, coordinates are grouped into 2D pairs.
- Each coordinate pair is rotated by an angle depending on position and frequency.
- The paper uses frequencies `theta_i = 10000^{-2(i-1)/d}` for coordinate pair `i`.

## Assumptions
- The hidden dimension used for RoPE is even.
- RoPE is applied to query and key representations.
- The note focuses on standard dot-product attention, not later RoPE scaling variants.

## Main result
RoPE applies:

`q_m = R^d_{Theta,m} W_q x_m`.

`k_n = R^d_{Theta,n} W_k x_n`.

The attention score is:

`q_m^T k_n = (R^d_{Theta,m} W_q x_m)^T (R^d_{Theta,n} W_k x_n)`.

Because:

`(R^d_{Theta,m})^T R^d_{Theta,n} = R^d_{Theta,n-m}`,

the dot product depends on relative position through `n - m`.

The sign of the offset depends on whether the relation is written from query-to-key or key-to-query order; the important property is dependence on relative position rather than absolute positions separately.

## Derivation
- In 2D, represent a query/key vector as a complex number.
- Multiply the projected query at position `m` by `e^{i m theta}`.
- Multiply the projected key at position `n` by `e^{i n theta}`.
- The query-key interaction contains a phase depending on the position difference, so relative position appears in the score.
- For higher even dimension, split the vector into 2D coordinate pairs and apply independent rotations.
- Skipped steps: full complex-number derivation and long-term decay proof from the paper.

## Interpretation
RoPE encodes absolute positions through rotations, but attention scores see relative position because dot products compare two rotated vectors.

## Alternative formulations
- Absolute sinusoidal positional encoding adds a position vector to token embeddings.
- Relative position bias methods add or modify attention-score terms directly.
- RoPE is multiplicative: it rotates query/key representations.

## Common mistakes
- Treating RoPE as simply adding sinusoidal embeddings.
- Assuming RoPE by itself explains all modern long-context behavior.
- Applying the paper's claims about RoPE variants that were introduced later.

## Related concepts
- [[Rotary Position Embedding]]
- [[Positional Encoding]]
- [[Scaled Dot-Product Attention]]
- [[Self-Attention]]
- [[Transformers]]

## Related papers
- [[2021 RoFormer]]
- [[2017 Attention Is All You Need]]

## Source references
- [[2021 RoFormer]]

## Verification status
- Status: partially verified
- Needs verification: full long-term decay derivation and modern RoPE scaling methods require separate checks.
