# Switch Transformers

## Metadata
- Authors: William Fedus, Barret Zoph, Noam Shazeer
- Year: 2021 preprint; 2022 JMLR publication
- Venue: Journal of Machine Learning Research
- Link: https://arxiv.org/abs/2101.03961
- arXiv: 2101.03961
- Source type: paper
- Status: studied
- Reliability: high
- Added: 2026-04-29

## Scope
This ingest covers sparse expert routing, the difference between dense feed-forward layers and expert feed-forward layers, top-1 Switch routing, token-to-expert assignment, expert capacity, dropped tokens, the load-balancing objective, compute-efficient parameter scaling, relation to transformer feed-forward blocks, and relevance to modern LLM scaling and inference.

Excluded: detailed benchmark tables, full T5 training setup, dataset details, TPU/system implementation details, training hyperparameters beyond brief context, detailed routing-loss derivations, and modern MoE variants except as future connections.

## One-sentence summary
Switch Transformers replace some dense transformer feed-forward layers with sparsely activated expert feed-forward layers, routing each token to one expert so parameter count can grow while per-token compute stays roughly fixed.

## Why this paper matters
The paper is a key source for practical [[Mixture of Experts]] in transformer language models. It makes MoE simpler by using top-1 routing and frames sparse activation as a way to scale capacity without activating all parameters for every token.

## Problem
Dense transformer scaling increases parameter count and computation together. The paper asks how to increase model capacity while keeping the floating-point operations per example manageable.

Earlier MoE models had adoption barriers from routing complexity, communication costs, and training instability.

## Background needed
- [[Transformers]]
- [[Transformer Feed-Forward Networks]]
- [[Expert Routing]]
- [[Scaling Laws]]
- [[Large Language Models]]

## Core idea
Replace selected dense feed-forward sublayers in a transformer with a Switch feed-forward layer containing multiple experts. A router assigns each token to a single expert, and only that expert processes the token.

## Method
- Each expert is a feed-forward network.
- For a token representation `x`, a router produces logits over experts.
- The router probabilities are computed with a softmax over experts.
- Switch routing selects the highest-probability expert for each token.
- The selected expert output is multiplied by the corresponding router gate value.
- Each expert has a fixed capacity. Tokens routed to an already-full expert are dropped from that expert computation and pass onward through the residual connection.
- An auxiliary load-balancing loss encourages tokens and router probability mass to spread across experts.

## Important equations
Router probabilities:

$$
p_i(x) = \frac{\exp(h_i(x))}{\sum_j \exp(h_j(x))}
$$

where the paper defines router logits from $h(x) = W_r x$.

General top-k MoE output:

$$
y = \sum_{i in T} p_i(x) E_i(x)
$$

For Switch routing, `T` contains only the top-1 expert.

Switch top-1 output:

$$
i^* = \arg\max_i p_i(x)
$$

$$
y = p_{i^*}(x) E_{i^*}(x)
$$

Expert capacity:

$$
\operatorname{expert\ capacity} = \frac{\operatorname{tokens\ per\ batch}}{\operatorname{number\ of\ experts}} \cdot \operatorname{capacity\ factor}
$$

Auxiliary load-balancing loss:

$$
loss = \alpha * N * \sum_i f_i * P_i
$$

where $f_i$ is the fraction of tokens dispatched to expert $i$, and $P_i$ is the fraction of router probability assigned to expert $i$ across the batch.

## Results
- Claim from source: Switch Transformer simplifies MoE routing by using a single selected expert per token.
- Claim from source: Increasing the number of experts increases sparse model parameters while keeping per-token computation approximately fixed.
- Claim from source: In the studied T5-based setup, Switch models show faster pre-training than dense baselines under comparable compute budgets.
- Claim from source: The paper reports training models up to trillion-parameter scale using sparse expert layers.

## Limitations
- The paper's engineering setting is tied to distributed training infrastructure and T5-style models.
- Expert capacity introduces a tradeoff between dropped tokens and wasted computation.
- Routing imbalance must be managed with an auxiliary loss.
- The paper does not settle later MoE design questions such as expert-choice routing, shared experts, or dropless routing.

## Claim from source
- MoE models select different parameters for different incoming examples, producing sparsely activated models with many parameters but roughly constant computational cost.
- The Switch Transformer routes each token to only one expert.
- The simplified top-1 routing reduces router computation, expert capacity requirements, and communication complexity compared with top-k MoE routing.
- The load-balancing objective is used because uniform expert use is desirable.

## My interpretation
Switch Transformer turns the transformer feed-forward block into a conditional-capacity module. Attention still mixes information across tokens, while the expert layer decides which parameter subset transforms each token.

The important mental model is not "more layers are active"; it is "many more parameters are available, but each token only uses a small subset."

## Unclear / Needs verification
- Needs verification: how the load-balancing loss used here compares algebraically with later MoE routing losses.
- Needs verification: how token dropping is handled in later production MoE systems.
- Needs verification: whether modern decoder-only LLM MoE layers preserve the same top-1 routing assumptions.

## Connections to concepts
- [[Mixture of Experts]]
- [[Expert Routing]]
- [[Transformers]]
- [[Transformer Feed-Forward Networks]]
- [[Large Language Models]]
- [[Scaling Laws]]

## Connections to papers
- [[2017 Attention Is All You Need]]

## Questions
- How much of Switch Transformer's gain comes from sparse capacity versus regularization or training setup?
- Which later paper should anchor modern decoder-only MoE architectures?

## Follow-up reading
- Earlier MoE work by Shazeer et al. should be ingested later for historical grounding.
- Modern MoE architectures should be ingested separately.
