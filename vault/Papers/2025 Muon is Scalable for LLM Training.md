# Muon is Scalable for LLM Training

## Metadata
- Authors: Jingyuan Liu; Jianlin Su; Xingcheng Yao; Zhejun Jiang; Guokun Lai; Yulun Du; Yidao Qin; Weixin Xu; Enzhe Lu; Junjie Yan; Yanru Chen; Huabin Zheng; Yibo Liu; Shaowei Liu; Bohong Yin; Weiran He; Han Zhu; Yuzhi Wang; Jianzhou Wang; Mengnan Dong; Zheng Zhang; Yongsheng Kang; Hao Zhang; Xinran Xu; Yutao Zhang; Yuxin Wu; Xinyu Zhou; Zhilin Yang
- Year: 2025
- Venue: arXiv technical report
- Link: https://arxiv.org/abs/2502.16982
- arXiv: 2502.16982
- Source type: paper
- Status: studied
- Reliability: medium
- Added: 2026-04-30

## Scope
This note focuses on Muon as applied to large-scale LLM training: which parameters use Muon versus AdamW, why matrix parameters are treated differently, what scaling evidence the source gives, training stability observations, and how the source strengthens or limits claims from [[2024 Muon Optimizer]].

Excluded: full benchmark tables, implementation details, infrastructure details beyond optimizer-scaling constraints, unsupported general superiority claims, deep Newton-Schulz derivation, unrelated Kimi/Moonlight architecture details, and marketing or economic claims.

## One-sentence summary
Moonshot AI reports that Muon can scale to LLM pretraining when paired with weight decay, per-parameter update RMS adjustment, and AdamW for non-matrix parameters.

## Why this paper matters
[[2024 Muon Optimizer]] introduced Muon mostly through small-scale experiments and implementation guidance. This technical report is the first source in the wiki that directly tests Muon-style optimization in larger LLM training settings.

## Problem
The source starts from the gap between Muon's small-scale promise and unresolved large-scale questions:
- whether matrix-orthogonalization optimizers scale to billions of parameters and trillions of tokens
- whether approximate orthogonalization can be implemented in distributed training
- whether Muon remains useful beyond pretraining, including supervised finetuning

## Background needed
- [[Muon Optimizer]]
- [[Muon Optimizer (Math)]]
- [[AdamW]]
- [[Weight Decay]]
- [[Matrix-Aware Optimizers]]
- [[Newton-Schulz Iteration]]
- [[Steepest Descent]]

## Core idea
The paper argues that scaling Muon requires practical adjustments beyond the original Muon source:
- add weight decay to Muon
- scale matrix updates so update RMS is more consistent across parameter shapes
- keep AdamW for non-matrix parameter classes
- compare Muon against tuned AdamW baselines in scaling-law experiments

## Method
The source uses Muon for matrix-shaped parameters and AdamW for non-matrix parameters such as RMSNorm parameters, LM head, and embeddings.

The base Muon update is described as:


$$
M_t = \mu M_{t-1} + \nabla L_t(W_{t-1})
O_t = Newton-Schulz(M_t)
W_t = W_{t-1} - \eta_t O_t
$$

The scaled version adds weight decay and update RMS adjustment:


$$
W_t = W_{t-1} - \eta_t \left(0.2\, O_t \sqrt{\max(A, B)} + \lambda W_{t-1}\right)
$$

where $[A, B]$ is the matrix shape.

## Important equations
Source claim for theoretical Muon update RMS:


$$
\operatorname{update\ RMS} \approx \sqrt{\frac{1}{\max(A, B)}}
$$

for a full-rank matrix of shape $[A, B]$.

The paper uses this to motivate shape-dependent scaling by $\sqrt{\max(A, B)}$, then matches the resulting update RMS to an empirical AdamW-like range.

## Results
Claim from source:
- Muon with weight decay outperforms vanilla Muon and AdamW in the reported over-training experiment.
- In scaling-law experiments, Muon requires about 52% of the training FLOPs to match AdamW under the paper's compute-optimal setup.
- The source trains a 3B activated / 16B total-parameter MoE model, Moonlight, with 5.7T tokens using Muon.
- Moonlight is reported to improve the performance-versus-training-FLOPs Pareto frontier in the comparisons shown by the paper.
- The source reports that Muon-pretrained and Muon-finetuned models perform best in its SFT ablation, but Muon applied only at SFT time to an AdamW-pretrained public model does not show a clear advantage over AdamW.

This note does not ingest full benchmark tables.

## Limitations
- The source is a technical report from the model team, so independent replication remains important.
- The paper's strongest results depend on specific Muon modifications, not the unmodified original Muon update.
- The source does not show that Muon is universally better than AdamW across all model families, scales, or training regimes.
- SFT results suggest optimizer mismatch remains an open problem.
- Detailed distributed implementation is outside this note's scope.

## Claim from source
- Muon is designed for matrix-shaped parameters, while AdamW is used with it for non-matrix parameters such as RMSNorm, LM head, and embeddings.
- Adding weight decay is important for scaling Muon.
- Without weight decay, some weights and layer output RMS values can grow too large during longer training.
- Muon's update RMS varies with parameter shape.
- The source proposes scaling Muon updates by $\sqrt{\max(A, B)}$ and matching update RMS to an empirical AdamW-like range.
- The source reports no loss spike or gradient norm spike in Moonlight training.
- The source reports sparse large-attention-logit events early in training and says they decrease as training progresses.
- The source reports that applying weight decay to RMSNorm gamma is important for stability.
- The source reports higher SVD entropy for Muon-trained weight matrices than AdamW-trained ones in its comparison, supporting the interpretation that Muon explores more diverse matrix directions.

## My interpretation
This source strengthens Muon from "interesting small-scale optimizer" to "credible large-scale optimizer candidate," but only with important caveats. The practical recipe is hybrid: Muon for matrix parameters, AdamW for non-matrix parameters, plus weight decay and update RMS scaling.

The most important correction to a naive Muon story is that orthogonalization alone was not enough in this source. Scaling required controlling weight growth and update scale.

## Unclear / Needs verification
- Needs verification: independent replications are needed before treating the reported FLOP efficiency as settled.
- Needs verification: whether update RMS scaling transfers cleanly across architectures beyond the source's settings.
- Needs verification: how to resolve the pretraining/SFT optimizer mismatch.
- Needs verification: whether RMSNorm gamma weight decay is generally required with Muon or specific to this training setup.

## Connections to concepts
- [[Muon Optimizer]]
- [[Muon Optimizer (Math)]]
- [[AdamW]]
- [[Weight Decay]]
- [[Matrix-Aware Optimizers]]
- [[Optimization and Training Stability]]
- [[LLM Training Systems]]
- [[Mixture of Experts]]

## Connections to papers
- [[2024 Muon Optimizer]]
- [[2024 Old Optimizer New Norm]]
- [[2017 Decoupled Weight Decay Regularization]]
- [[2024 DeepSeek-V3 Technical Report]]

## Questions
- Can independent groups reproduce the scaling-law advantage?
- Which parameter groups should remain on AdamW in future Muon variants?
- Is update RMS matching a general principle for matrix-aware optimizers?
- How should Muon interact with SFT and post-training?

## Follow-up reading
- Independent Muon scaling reports.
- Sources on optimizer mismatch between pretraining and finetuning.
- Sources on update RMS / parameterization-aware optimizer scaling.
