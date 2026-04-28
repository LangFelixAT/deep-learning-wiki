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

## Linking convention

Use Obsidian links:

- `[[ELBO]]`
- `[[KL Divergence]]`
- `[[Variational Autoencoders]]`

Prefer meaningful links over excessive linking.

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

```markdown
## [YYYY-MM-DD] ingest | Source title

- Source:
- Pages created:
- Pages updated:
- Key concepts:
- Notes: