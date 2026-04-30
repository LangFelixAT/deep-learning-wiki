# Multi-Head Latent Attention (Math)

## Metadata
- Type: math
- Status: partially verified
- Last reviewed: 2026-04-29

## Goal
Define the MLA attention computation from [[2024 DeepSeek-V2 Technical Report]] and explain how it reduces [[KV Cache]] size during autoregressive inference.

## Canonical notation
- $h_t$: attention input for token $t$
- $n_h$: number of attention heads
- $d_h$: per-head dimension for the content part
- $d_h^R$: per-head dimension for decoupled RoPE query/key components
- $d_c$: KV compression dimension
- $d_c'$: query compression dimension
- $c_t^{KV}$: compressed latent vector for keys and values
- $c_t^Q$: compressed latent vector for queries
- $q_{t,i}$: query for head $i$
- $k_{t,i}$: key for head $i$
- $v_{t,i}^C$: value for head $i$
- $l$: number of layers

## Definitions
- Source: [[2024 DeepSeek-V2 Technical Report]].
- Standard MHA projects $h_t$ into full query, key, and value vectors, slices them into heads, and caches all keys and values during generation.
- MLA applies low-rank joint compression to keys and values before reconstructing head-specific key/value components.
- MLA also uses decoupled [[Rotary Position Embedding]] components because applying RoPE directly to compressed keys would interfere with inference-time projection absorption.

## Assumptions
- The setting is autoregressive generation, where previous attention keys and values are cached.
- The source counts KV cache per token by number of elements, independent of storage precision.
- $d_c << d_h n_h$ and $d_c' << d_h n_h$.
- This note follows the source notation but uses ASCII approximations for superscripts.

## Main result
In standard MHA, the source states that the KV cache per token is:

$$
2 n_h d_h l
$$

In MLA with decoupled RoPE, the source states that the cache per token is:

$$
(d_c + d_h^R) l
$$

The cache is smaller because generation stores the compressed KV latent $c_t^{KV}$ plus a decoupled RoPE key, rather than full per-head key and value tensors.

## Derivation
Standard MHA baseline:

$$
q_t = W^Q h_t
$$

$$
k_t = W^K h_t
$$

$$
v_t = W^V h_t
$$

These are sliced into $n_h$ heads, then each head computes:

$$
o_{t,i} = \sum_{j=1}^t softmax_j(q_{t,i}^T k_{j,i} / \sqrt(d_h)) v_{j,i}
$$

$$
u_t = W^O [o_{t,1}; ...; o_{t,n_h}]
$$

During generation, MHA caches all previous $k_{j,i}$ and $v_{j,i}$ values, giving $2 n_h d_h l$ elements per token.

MLA KV compression:

$$
c_t^{KV} = W^{DKV} h_t
$$

$$
k_t^C = W^{UK} c_t^{KV}
$$

$$
v_t^C = W^{UV} c_t^{KV}
$$

The compressed vector $c_t^{KV}$ is the object cached for the content key/value path.

MLA query compression:

$$
c_t^Q = W^{DQ} h_t
$$

$$
q_t^C = W^{UQ} c_t^Q
$$

Query compression is used by the source to reduce activation memory during training, not to reduce KV cache.

Decoupled RoPE:

$$
q_t^R = RoPE(W^{QR} c_t^Q)
$$

$$
k_t^R = RoPE(W^{KR} h_t)
$$

The final head query and key concatenate content and RoPE components:

$$
q_{t,i} = [q_{t,i}^C; q_{t,i}^R]
$$

$$
k_{t,i} = [k_{t,i}^C; k_t^R]
$$

The attention computation becomes:

$$
o_{t,i} = \sum_{j=1}^t softmax_j(q_{t,i}^T k_{j,i} / \sqrt(d_h + d_h^R)) v_{j,i}^C
$$

$$
u_t = W^O [o_{t,1}; ...; o_{t,n_h}]
$$

Skipped steps:
- Full matrix-shape verification of the source's projection absorption statement.
- Full Appendix C derivation in original tensor notation.

## Interpretation
MLA changes what is stored for later decoding. Standard MHA stores full keys and values for every head. MLA stores a compressed latent vector that can produce the key/value content components, plus a separate RoPE key needed for positional information.

The decoupled RoPE component is not decorative. It is needed because RoPE is position-sensitive; applying RoPE directly to compressed keys would block the source's inference-time absorption of projection matrices.

## Alternative formulations
- [[Multi-Head Attention]] caches full per-head keys and values.
- [[Multi-Query Attention]] shares one key/value set across query heads.
- [[Grouped-Query Attention]] keeps an intermediate number of key/value groups.
- MLA reduces cache through latent key/value compression rather than only through key/value head sharing.

## Common mistakes
- Treating MLA as just another name for MQA or GQA.
- Forgetting that query compression reduces training activation memory, not KV cache.
- Ignoring the decoupled RoPE key when counting the MLA cache.
- Assuming the cache-size formulas include storage precision; the source counts elements.
- Treating the source's performance comparison as a universal result independent of model and training setup.

## Related concepts
- [[Multi-Head Latent Attention]]
- [[KV Cache]]
- [[Multi-Head Attention]]
- [[Multi-Query Attention]]
- [[Grouped-Query Attention]]
- [[Rotary Position Embedding]]
- [[Large Language Models]]

## Related papers
- [[2024 DeepSeek-V2 Technical Report]]
- [[2024 DeepSeek-V3 Technical Report]]

## Source references
- [[2024 DeepSeek-V2 Technical Report]]

## Verification status
- Status: partially verified
- Needs verification: full projection-absorption algebra and matrix shapes.
- Needs verification: independent comparison of MLA, MHA, MQA, and GQA outside the DeepSeek-V2 source.
