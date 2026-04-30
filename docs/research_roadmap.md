# Research Roadmap

This is a living map for the deep learning wiki. It is not a fixed syllabus.

The goal is to build a connected mental model of modern deep learning research, grounded in source notes and strengthened through concept and math pages.

## Generative modeling

Current status: developing.

Covered foundations:
- [[Generative Modeling]]
- [[Variational Autoencoders]]
- [[ELBO]]
- [[Score Matching]]
- [[Diffusion Models]]
- [[Latent Diffusion Models]]
- [[Classifier-Free Guidance]]
- [[CLIP]]
- [[Diffusion with Transformers]]

Open backbone gaps:
- [[GANs]]
- [[Normalizing Flows]]
- [[Energy-Based Models]]
- broader comparison of likelihood-based, adversarial, score-based, and diffusion models

## Transformer architecture

Current status: early foundation.

Seed pages:
- [[Transformer Architecture]]
- [[Efficient LLM Architecture]]
- [[Transformers]]
- [[Attention]]
- [[Self-Attention]]
- [[Multi-Head Attention]]
- [[Scaled Dot-Product Attention]]
- [[Transformer Feed-Forward Networks]]
- [[Layer Normalization]]
- [[Layer Normalization (Math)]]
- [[Rotary Position Embedding]]
- [[Rotary Position Embedding (Math)]]
- [[Grouped-Query Attention]]
- [[Multi-Query Attention]]
- [[FlashAttention]]
- [[Multi-Head Latent Attention]]
- [[KV Cache]]
- [[Mixture of Experts]]
- [[DeepSeekMoE]]
- [[Expert Routing]]
- [[Image Tokenization]]
- [[Diffusion with Transformers]]

Needed backbone:
- sparse attention
- XSA
- later positional encoding and RoPE scaling variants
- residual stream view
- later normalization variants beyond [[RMSNorm]]

## Efficient attention and inference systems

Current status: early foundation.

Seed pages:
- [[LLM Inference Systems]]
- [[Efficient LLM Architecture]]
- [[KV Cache]]
- [[Grouped-Query Attention]]
- [[Multi-Query Attention]]
- [[FlashAttention]]
- [[Multi-Head Latent Attention]]
- [[LLM Training Systems]]

Needed backbone:
- prefill and decode
- memory bandwidth versus compute
- attention complexity
- paged attention
- long-context attention
- inference-time batching

## Optimization and training

Current status: early foundation.

Seed pages:
- [[Optimization and Training Stability]]
- [[Gradient Descent]]
- [[Adam]]
- [[AdamW]]
- [[Weight Decay]]
- [[Normalization]]
- [[RMSNorm]]
- [[Scaling Laws]]

Needed backbone:
- Muon optimizer
- Shampoo-style matrix-aware optimizers
- learning-rate schedules
- gradient clipping
- residual scaling
- initialization
- training stability

## Mixture of experts and scaling

Current status: early foundation.

Seed pages:
- [[Mixture of Experts]]
- [[Expert Routing]]
- [[DeepSeekMoE]]
- [[LLM Training Systems]]

Needed backbone:
- expert parallelism
- load balancing
- sparse activation
- scaling laws for dense versus sparse models
- modern MoE variants grounded in separate sources
- expert specialization synthesis after more MoE sources

## Mathematical foundations

Current status: uneven.

Developing areas:
- [[Notation Conventions]]
- [[Probability Theory]]
- [[Bayesian Inference]]
- [[KL Divergence]]
- [[Variational Inference]]
- [[ELBO]]
- [[Score Matching]]

Needed backbone:
- linear algebra for projections and attention
- matrix calculus for backpropagation
- softmax and log-sum-exp
- information theory basics
- optimization geometry
- numerical stability

## Operating principles

- Ingest papers one at a time unless there is a deliberate batch plan.
- Keep paper notes faithful to the source.
- Use concept pages for synthesis.
- After several related ingests, update the relevant synthesis hub.
- Use math pages for definitions, assumptions, derivations, and notation.
- Mark weak or uncertain material as `Needs verification`.
- Prefer source-grounded growth over invented completeness.
- Periodically lint for missing links, duplicate explanations, and thin foundations.
