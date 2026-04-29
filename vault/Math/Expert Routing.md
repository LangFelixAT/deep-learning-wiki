# Expert Routing

## Metadata
- Type: math
- Status: partially verified
- Last reviewed: 2026-04-29

## Goal
Define the routing mechanism used to assign token representations to experts in Switch-style [[Mixture of Experts]] layers.

## Canonical notation
- `x`: token representation
- `N`: number of experts
- `E_i(x)`: output of expert `i` on token `x`
- `W_r`: router weight matrix
- `h(x)`: router logits
- `p_i(x)`: router probability for expert `i`
- `T`: selected expert index set
- `f_i`: fraction of tokens dispatched to expert `i`
- `P_i`: fraction of router probability allocated to expert `i`
- `alpha`: load-balancing loss coefficient

## Definitions
- Source: [[2021 Switch Transformers]]
- Router logits: `h(x) = W_r x`.
- Router probability:

`p_i(x) = exp(h_i(x)) / sum_j exp(h_j(x))`

- Top-1 routing selects `argmax_i p_i(x)`.
- Expert capacity is the maximum number of tokens an expert processes in a batch.

## Assumptions
- The layer has a fixed number of experts.
- Each token is routed independently.
- In Switch routing, each token is routed to one expert.
- Expert capacity may be smaller than the number of tokens assigned to an expert.
- Dropped tokens skip the expert computation and continue through the residual path in the source's implementation.

## Main result
Switch routing is top-1 MoE routing: each token activates one expert, enabling parameter count to scale with the number of experts while per-token expert computation remains roughly fixed.

For selected expert `i* = argmax_i p_i(x)`, the Switch layer output for the token is:

`y = p_{i*}(x) E_{i*}(x)`

## Derivation
- Compute router logits `h(x) = W_r x`.
- Convert logits to router probabilities with softmax.
- Choose the top-probability expert for each token.
- Apply only the selected expert to the token.
- Multiply the selected expert output by the router gate value.
- Apply the capacity constraint. If too many tokens select the same expert, overflow tokens are dropped from expert computation.
- Add a load-balancing loss during training:

`loss = alpha * N * sum_i f_i * P_i`

where `f_i` is based on hard assignments and `P_i` is based on router probability mass.

- Skipped steps: full gradient analysis of the auxiliary loss.

## Interpretation
Routing makes the feed-forward layer conditional on the token. The model can contain many experts, but each token only pays for the expert it selects.

The load-balancing loss is needed because a router that sends most tokens to the same expert wastes available capacity and increases token overflow.

## Alternative formulations
- Top-k MoE routes each token to more than one expert and combines outputs.
- Switch routing is the top-1 simplification studied in [[2021 Switch Transformers]].
- [[2024 DeepSeekMoE]] uses fine-grained routed experts plus shared expert isolation: shared experts are always active, while routed experts are selected by top-k affinity scores.
- [[2024 DeepSeek-V2 Technical Report]] describes DeepSeekMoE with top-k routed experts plus shared experts, device-limited routing, and auxiliary losses for expert/device/communication balance.
- [[2024 DeepSeek-V3 Technical Report]] uses top-k routed experts plus shared experts, and describes an auxiliary-loss-free load-balancing strategy.
- Needs verification: later MoE variants may use different routing rules, expert-choice routing, or dropless capacity handling.

## Common mistakes
- Thinking every token uses all experts.
- Confusing number of experts with per-token compute.
- Treating the router as a separate language model; in this source it is a learned assignment function inside a transformer layer.
- Ignoring expert capacity and assuming all assignments are always processed.

## Related concepts
- [[Mixture of Experts]]
- [[DeepSeekMoE]]
- [[Transformer Feed-Forward Networks]]
- [[Transformers]]
- [[Large Language Models]]
- [[Scaling Laws]]

## Related papers
- [[2021 Switch Transformers]]
- [[2024 DeepSeekMoE]]
- [[2024 DeepSeek-V2 Technical Report]]
- [[2024 DeepSeek-V3 Technical Report]]

## Source references
- [[2021 Switch Transformers]]
- [[2024 DeepSeekMoE]]
- [[2024 DeepSeek-V2 Technical Report]]
- [[2024 DeepSeek-V3 Technical Report]]

## Verification status
- Status: partially verified
- Needs verification: exact behavior of dropped tokens in later MoE systems.
- Needs verification: derive DeepSeekMoE balance losses in full if routing math becomes a priority.
