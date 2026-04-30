# Project Plan

This file captures near-term execution priorities. It should stay more concrete than `docs/research_direction.md` and more temporary than `docs/research_roadmap.md`.

## Current phase

The wiki is in a foundation-building and synthesis-building phase.

The goal is to keep expanding into recent deep learning research while preserving the source-grounded structure:
- source notes for faithful claims
- math notes for definitions and derivations
- concept notes for intuition and links
- synthesis pages for design spaces and historical maps

## Current priorities

1. Keep existing synthesis hubs healthy:
   - [[Transformer Architecture]]
   - [[Efficient LLM Architecture]]
   - [[Optimization and Training Stability]]
   - [[Diffusion Design Space]]

2. Strengthen weak foundations before deep specialization:
   - [[Energy-Based Models]]
   - [[GANs]]
   - [[Normalizing Flows]]
   - representation learning beyond [[CLIP]]
   - multimodal model structure

3. Continue the modern architecture track:
   - attention variants such as XSA and sparse attention
   - attention residuals and gating residuals
   - residual stream and normalization variants
   - efficient inference and KV-cache systems

4. Continue the optimization and training-stability track:
   - optimizer geometry
   - matrix-aware optimizers
   - Muon validation and comparison sources
   - learning-rate schedules, clipping, initialization, and residual scaling

5. Build toward representation and world-model tracks:
   - multimodal embeddings and conditioning
   - JEPA-style predictive representations
   - latent world models
   - links between energy-based thinking and representation learning

## Operating reminders

- Do not chase recent papers as isolated summaries.
- For frontier topics, first identify the foundational question: representation, objective, architecture, inference/sampling, optimization, or systems bottleneck.
- Prefer one grounded source ingest at a time unless a batch is explicitly useful.
- After several related ingests, update or create a synthesis page only if it improves navigation.
- Keep candidate synthesis hubs as plain text until enough source-grounded pages exist to justify real notes.
