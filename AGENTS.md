# AGENTS.md

This repository is a personal Obsidian-compatible deep learning wiki.

## Project goal

Build a rigorous, evolving knowledge base for deep learning, including:
- mathematical foundations
- important papers
- lecture/video notes
- conceptual summaries
- historical development of ideas

The wiki should help the user understand topics such as:
- transformers
- VAEs
- ELBO
- Bayesian inference
- regularization
- diffusion models
- score matching
- generative modeling
- optimization
- representation learning

## Research trajectory

The wiki is not only about diffusion models. Diffusion has been an early foundation-building track, but the broader goal is a connected mental model of modern deep learning research.

Current research tracks include:
- generative modeling: VAEs, GANs, normalizing flows, energy-based models, score-based models, diffusion models, and text-guided generation
- transformer architecture: attention, self-attention, multi-head attention, multi-query attention, grouped-query attention, multi-head latent attention, sparse attention, FlashAttention, and related efficient attention variants
- large model systems: KV cache, prefill/decode behavior, inference efficiency, memory bandwidth, mixture of experts, routing, and scaling constraints
- optimization: gradient descent, Adam, Muon, second-order or matrix-aware optimizers, normalization, residual pathways, and training stability
- representation learning: embeddings, contrastive learning, CLIP-like models, conditioning signals, and semantic representation spaces
- frontier topics: exclusive self-attention, attention residuals, gating residuals, multimodal generative systems, energy-based transformers, JEPA-style models, world models, and other recent developments when grounded in sources

When moving into a new track, build the backbone first: seed the core concept and math pages, then ingest source papers that ground the details.

Use `docs/research_direction.md` as the durable north star for the user's research interests and for connecting recent frontier topics back to foundations.

## Core rule

Do not treat this as a blog or generic summary collection.

The wiki has three layers:

1. Source notes
   - papers
   - videos
   - lectures
   - books
   - blog posts

2. Math notes
   - derivations
   - definitions
   - assumptions
   - notation

3. Concept notes
   - synthesis
   - intuition
   - connections
   - historical development

## Folder meanings

- `vault/Papers/`
  Faithful notes for individual papers.

- `vault/Videos/`
  Notes from lectures, talks, and video transcripts.

- `vault/Math/`
  Rigorous mathematical notes and derivations.

- `vault/Concepts/`
  Higher-level conceptual synthesis pages.

- `vault/People/`
  Notes on important researchers, only if useful.

- `vault/Research-Radar/`
  Later: arXiv scans and paper triage.

- `data/raw/`
  Raw source material. Do not modify raw sources.

- `prompts/`
  Reusable prompts for LLM-assisted ingestion.

## Rules for source notes

Source notes must stay close to the source.

They may include:
- summary
- problem statement
- method
- important equations
- results
- limitations
- connections

They must not overclaim beyond the source.

Use labels such as:
- `Claim from source`
- `My interpretation`
- `Unclear`
- `Needs verification`

## Rules for math notes

Math notes must be rigorous.

Always include:
- goal
- definitions
- assumptions
- derivation
- interpretation
- common mistakes
- related concepts

Do not skip algebraic steps unless explicitly marked as skipped.

When notation differs across sources, define canonical notation and mention alternatives.

Format mathematics for Obsidian/MathJax:
- inline math uses `$...$`
- display equations use `$$...$$`
- backticks are only for literal code, commands, filenames, or pseudocode

## Rules for concept notes

Concept notes synthesize multiple sources.

They should include:
- short definition
- intuition
- mathematical formulation
- historical development
- related papers
- related concepts
- open questions

Concept notes may evolve over time.

## Rules for synthesis pages

After several related ingests in one research track, create or update a synthesis page that organizes the accumulated knowledge.

Synthesis pages should:
- explain the design space or historical progression
- connect source notes, math notes, and concept notes
- identify open gaps and weak areas
- avoid introducing unsupported new claims
- mark uncertain connections as `Needs verification`

Examples include:
- `[[Diffusion Design Space]]`
- `[[Efficient LLM Architecture]]`
- `[[Transformer Architecture]]`
- `[[Optimization and Training Stability]]`

## Linking convention

Use Obsidian links:

- `[[ELBO]]`
- `[[KL Divergence]]`
- `[[Variational Autoencoders]]`

Prefer meaningful links over excessive linking.

Prefer simple note-title links such as `[[Variational Inference]]`.
Avoid folder-qualified link targets such as `Math/Variational Inference|Variational Inference` unless there is a deliberate reason.

Filenames should generally be unique across the vault so links stay unambiguous.
If a concept note and math note would otherwise have the same title, choose a more specific title for one of them, for example:
- `[[Variational Inference]]` for the math note
- `[[Amortized Variational Inference]]` for the concept note

## Reliability labels

Every source note should include:

- Reliability: high / medium / low
- Status: unread / skimmed / studied / verified
- Source type: paper / video / book / blog / course

## Important behavior for Codex

When editing the vault:
1. Preserve Obsidian Markdown.
2. Do not rename files unless asked.
3. Do not delete notes unless asked.
4. Prefer small, reviewable changes.
5. If creating a new note, use the correct template.
6. If adding mathematical derivations, be explicit about assumptions.
7. If unsure, mark content as `Needs verification`.
8. Never invent paper claims.
9. Separate source claims from interpretation.
10. Keep raw sources immutable.
11. After meaningful changes, update `vault/index.md` and append an entry to `vault/log.md`.
12. If the user limits an ingest to specific sections or topics, only ingest that scope and record the scope in the source note or log.
13. Do not let one research track dominate the wiki structure. Keep overview pages connected across generative modeling, transformers, optimization, systems, and representation learning.
14. Prefer source-grounded math and concepts. If a needed foundation is thin, create a stub or mark it as `Needs verification`, then strengthen it through later source ingests.
15. Prefer conceptual grounding before deep specialization. Do not expand into full derivations, variants, implementation details, or benchmark minutiae unless the user asks or the detail is necessary for the current mental model.
16. After several related ingests, update the relevant synthesis page or explicitly note why no synthesis update was needed.

## Current phase

We are in the foundation-building phase.

Do not implement arXiv scanning yet.

Focus on:
- strong templates
- seed concept pages
- seed math pages
- manual ingestion workflow
- retroactive ingestion of already-known resources

## Special files

### `docs/design_principles.md`

Project-level principles and the map of operational workflow documents.

### `docs/research_direction.md`

Durable direction of the user's research interests, including how recent frontier topics should connect back to source-grounded foundations.

### `docs/ingestion_workflow.md`

How new sources enter the wiki.

### `docs/synthesis_workflow.md`

How accumulated notes become higher-level maps.

### `docs/lint_workflow.md`

How lint passes should check structure, links, notation, duplication, abstraction levels, and Obsidian compatibility.

### `docs/research_roadmap.md`

Living map of current research tracks, covered foundations, and open backbone gaps.

### `docs/project_plan.md`

Near-term execution priorities and operating reminders.

### `vault/index.md`

Content-oriented catalog of the wiki.

It should list important pages with:
- link
- one-line summary
- type: concept / math / paper / video / index
- status if applicable

The LLM should update `index.md` after every ingest or major wiki edit.

### `vault/log.md`

Chronological append-only record.

Every important operation should add an entry using this format:
[YYYY-MM-DD] ingest | Source title

- Source:
- Pages created:
- Pages updated:
- Key concepts:
- Notes:

Other operation types:

- ingest
- query
- lint
- refactor
- manual

Do not rewrite old log entries except to fix obvious formatting errors.
