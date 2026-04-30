# Ingestion Workflow

This document describes how new knowledge enters the wiki.

Before ingesting, check `docs/research_direction.md` and `docs/research_roadmap.md` so the source is placed into the right research track.

## Step 1: Identify the source

Classify the source as one of:

- paper
- video
- lecture
- book chapter
- blog post
- documentation
- personal note

For paper ingestion, use `prompts/ingest_paper.md` as the reusable prompt pattern. The user can then provide only the PDF path, source title, and source-specific scope.

For frontier or recent sources, identify the foundation they are meant to strengthen:
- representation
- objective
- architecture
- inference, decoding, or sampling
- optimization and training stability
- systems bottleneck

Do not ingest a frontier source as an isolated trend note. Connect it to existing source notes, math notes, concept notes, and synthesis pages where grounded.

## Step 2: Create a source note

Use the appropriate template:

- `vault/Templates/Paper.md`
- `vault/Templates/Video.md`

The source note should stay faithful to the original source.

## Step 3: Extract concepts

Identify important concepts mentioned in the source.

Examples:
- ELBO
- KL divergence
- attention
- score matching
- denoising objective
- Bayesian posterior
- variational approximation

For each concept:
- link existing concept/math pages
- create missing stubs only when useful

## Step 4: Update math notes

If the source contains an important derivation:
- add it to the relevant math page
- include assumptions
- preserve notation
- mention source-specific notation if needed
- format equations for Obsidian/MathJax: inline math as `$...$`, display equations as `$$...$$`
- use braces for grouped superscripts and function arguments, for example `$x^{(t)}$` and `$\sqrt{d_k}$`
- use braces for multi-character subscripts, for example `$c_{skip}$`, `$L_{LDM}$`, and `$D_{KL}$`
- use proper LaTeX operators and delimiters, for example `$\arg\max_i$`, `$\arg\min_{\delta}$`, and `$\|\delta\|^2$`
- reserve backticks for literal code, filenames, commands, or pseudocode, not mathematical variables or formulas

## Step 5: Update concept notes

Update higher-level concept pages with:
- intuition
- historical role
- relation to other ideas
- links to the source note

## Step 6: Add personal understanding

Use a clearly separated section:

## My understanding

This section may contain:
- personal interpretation
- questions
- confusion
- partial understanding

## Step 7: Mark status

Every source note should have a status:

- unread
- skimmed
- studied
- verified

Only use "verified" after manually checking important claims.

Concept and math notes may also use the vault status vocabulary:

- stub
- developing
- partially verified
- verified

## Step 8: Update index and log

After ingestion:
- update `vault/index.md`
- append an entry to `vault/log.md`

Follow the format defined in `AGENTS.md`.

## Step 9: Synthesis checkpoint

After ingesting a source, ask whether it changes the existing mental model.

Check:
- Does this source update an overview page?
- Does it add a new design axis, historical step, or mathematical framing?
- Does it contradict or refine an earlier source?
- Does it reveal a missing prerequisite concept or math note?
- Should a timeline, roadmap, or synthesis page be updated?
- If the source belongs to an active track, should the relevant track hub be updated?

For isolated sources, keep this short. After several related ingests, perform a larger synthesis pass that connects the sources and identifies gaps.
If no synthesis page is updated, briefly note why in the log when useful.

## Step 10: Track context

Record the relevant research track when useful:
- generative modeling
- transformer architecture
- efficient attention
- LLM training and inference systems
- optimization
- representation learning
- multimodality
- energy-based modeling
- world models and predictive representations
- mathematical foundations

The goal is to prevent the wiki from becoming a sequence of paper summaries. Each ingest should strengthen the persistent map of the field.
