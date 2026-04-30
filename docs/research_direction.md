# Research Direction

This document captures the durable direction of the wiki. It is not a fixed syllabus and not a near-term task list.

The project goal is to build a connected mental model of deep learning research: the mathematical foundations, the historical source trail, and the recent frontier ideas that matter for understanding modern systems.

## Core interest

The wiki should connect foundations from the last 10-15 years to current deep learning systems.

Important tracks include:
- generative modeling: VAEs, GANs, normalizing flows, energy-based models, score-based models, diffusion models, and modern image generation
- transformer architecture: attention, residual pathways, normalization, feed-forward blocks, MoE, routing, and positional structure
- efficient attention and inference: KV cache, MQA, GQA, MLA, FlashAttention, sparse attention, XSA, and serving bottlenecks
- optimization and training stability: SGD, Adam, AdamW, Shampoo, Muon, matrix-aware updates, normalization, residual scaling, and stability mechanisms
- representation learning and multimodality: embeddings, CLIP-like models, conditioning, multimodal models, latent representations, JEPA-style models, and world models
- energy-based thinking: energy-based models, score matching, energy-based transformers, and connections to representation learning and generative modeling

## Frontier topics

Recent developments are in scope, including:
- exclusive self-attention and other modern attention variants
- attention residuals and gating residuals
- modern multimodal and image-generation systems
- energy-based transformers
- I-JEPA, V-JEPA, world models, and predictive latent representations
- new optimizers and optimizer-geometry ideas

These topics should not be ingested as isolated trend notes. They should be connected back to:
- the source papers that introduced the mechanism
- the mathematical objective or operation involved
- the architectural role of the mechanism
- the system or scaling bottleneck it addresses
- older ideas it reuses, simplifies, or reinterprets

## Cross-cutting questions

When evaluating a new topic, ask:
- What representation is being learned or manipulated?
- What objective is optimized?
- What architecture implements the idea?
- What inference, decoding, or sampling procedure is used?
- What mathematical structure explains the mechanism?
- What training or systems bottleneck shaped the design?
- Which previous source-grounded concepts does it connect to?

## Grounding rule

The wiki should include recent frontier developments, but source-grounded foundations come first.

If a new topic is important but the foundation is thin:
- create a short stub only if needed for navigation
- mark uncertain claims as `Needs verification`
- add the topic to the roadmap or open questions
- ingest grounding sources before adding detailed explanations

## Candidate future synthesis hubs

Possible synthesis pages once enough sources are grounded:
- Representation Learning and World Models
- Multimodal Generative Models
- Attention and KV Cache Design Space
- Optimizer Geometry
- Energy-Based Modeling

Do not create these pages too early unless they help navigation after several related notes exist.
