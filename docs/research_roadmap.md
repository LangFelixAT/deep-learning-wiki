# Research Roadmap

This is a living map for the deep learning wiki. It is not a fixed syllabus.

The goal is to build a connected mental model of modern deep learning research, grounded in source notes and strengthened through concept and math pages.

## Generative modeling

Current status: developing.

Covered foundations:
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
- [[Transformers]]
- [[Attention]]
- [[Self-Attention]]
- [[Multi-Head Attention]]
- [[Scaled Dot-Product Attention]]
- [[Transformer Feed-Forward Networks]]
- [[Image Tokenization]]
- [[Diffusion with Transformers]]

Needed backbone:
- Multi-Query Attention
- Grouped-Query Attention
- Multi-Head Latent Attention
- sparse attention
- FlashAttention
- XSA
- positional encodings and RoPE
- residual stream view
- normalization layers

## Efficient attention and inference systems

Current status: mostly missing.

Needed backbone:
- KV cache
- prefill and decode
- memory bandwidth versus compute
- attention complexity
- paged attention
- long-context attention
- inference-time batching

## Optimization and training

Current status: mostly stubbed.

Seed pages:
- [[Gradient Descent]]
- [[Adam]]
- [[Weight Decay]]
- [[Normalization]]
- [[Scaling Laws]]

Needed backbone:
- AdamW
- Muon optimizer
- Shampoo-style matrix-aware optimizers
- learning-rate schedules
- gradient clipping
- residual scaling
- initialization
- training stability

## Mixture of experts and scaling

Current status: missing.

Needed backbone:
- Mixture of Experts
- routing
- expert parallelism
- load balancing
- sparse activation
- scaling laws for dense versus sparse models

## Mathematical foundations

Current status: uneven.

Developing areas:
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
- Use math pages for definitions, assumptions, derivations, and notation.
- Mark weak or uncertain material as `Needs verification`.
- Prefer source-grounded growth over invented completeness.
- Periodically lint for missing links, duplicate explanations, and thin foundations.
