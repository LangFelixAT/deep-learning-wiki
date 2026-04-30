# Paper Ingestion Prompt

Use this prompt when ingesting one paper into the deep learning wiki.

## Required user input

The user should provide:
- raw PDF path
- paper title
- authors and year, if known
- scope or focus, if there is a specific goal

Short example:

```text
Ingest:
data/raw/papers/sohl_dickstein_nonequilibrium_thermodynamics_2015.pdf

Source:
Deep Unsupervised Learning using Nonequilibrium Thermodynamics
Sohl-Dickstein et al., 2015

Scope:
Focus on forward diffusion, learned reverse process, tractability motivation, likelihood/evaluation idea, and relationship to DDPM.
```

## Required setup

Before editing, read:
- `AGENTS.md`
- `docs/ingestion_workflow.md`
- `docs/research_direction.md`
- `docs/research_roadmap.md`
- the relevant templates in `vault/Templates/`
- the existing related wiki pages found through `vault/index.md` and search

Use the raw PDF as the source of truth. Do not modify raw sources.

## Default ingest behavior

Create or update the paper note in `vault/Papers/` using the paper template.

Fill only source-grounded sections:
- metadata
- one-sentence summary
- why this paper matters
- problem
- background needed
- core idea
- method
- important equations
- results, if relevant to the requested scope
- limitations
- claims from source
- my interpretation
- unclear / needs verification
- connections to concepts
- connections to papers
- questions
- follow-up reading

Keep the paper note faithful to the source. Do not invent claims or import later literature into the source note except as clearly marked connection context.

## Concept and math updates

Update existing concept and math notes only where the paper genuinely strengthens them.

Create new notes only when useful. Use:
- `vault/Templates/Concept.md` for concept pages
- `vault/Templates/Math.md` for math pages

For math notes:
- state the goal
- define canonical notation
- list assumptions
- include derivation structure
- mark skipped algebra explicitly
- mark uncertain steps as `Needs verification`

For concept notes:
- keep intuition separate from source claims
- connect to historical development
- link related papers and math pages
- avoid turning concept pages into paper summaries

## Scope control

Respect the user's requested scope.

For frontier or recent sources, first identify what foundation the paper strengthens:
- representation
- objective
- architecture
- inference, decoding, or sampling
- optimization and training stability
- systems bottleneck
- multimodal or energy-based modeling connection

Do not ingest recent topics as isolated trend notes. Connect them back to existing source notes, math notes, concept notes, and synthesis pages where the source supports the connection.

If the paper contains advanced sections outside scope:
- do not ingest them
- optionally list them under follow-up reading or questions
- record the scope in the paper note or log entry

If no scope is provided, choose a conservative foundational scope based on the current research roadmap and existing wiki gaps. State that scope before editing.

## Synthesis checkpoint

After source-specific edits, check whether the paper changes the existing mental model.

Ask:
- Does it update an overview page?
- Does it add a historical step?
- Does it introduce a new design axis?
- Does it clarify a mathematical foundation?
- Does it reveal a missing prerequisite page?
- Does it affect `docs/research_roadmap.md`?
- Does it affect an active synthesis page such as `[[Transformer Architecture]]`, `[[Efficient LLM Architecture]]`, `[[Optimization and Training Stability]]`, or `[[Diffusion Design Space]]`?

Apply only small synthesis edits unless the user requested a larger refactor.

## Required bookkeeping

After every meaningful ingest:
- update `vault/index.md`
- append to `vault/log.md`

Use this log format:

```text
## [YYYY-MM-DD] ingest | Source title

- Source:
- Pages created:
- Pages updated:
- Key concepts:
- Notes:
```

The log notes should include the ingest scope and any excluded topics.

## Before editing

Summarize:
- intended paper note path
- intended scope
- likely concept/math pages to update or create
- risky or uncertain changes, if any

## After editing

List:
- files created
- files modified
- what changed in each
- any claims or derivations marked `Needs verification`
