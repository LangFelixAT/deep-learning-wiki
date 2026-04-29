# Design Principles

This repository follows the LLM Wiki pattern described by Andrej Karpathy: a persistent, interlinked Markdown wiki maintained by an LLM agent, with raw sources as immutable ground truth and Obsidian as the browsing/editing environment.

The goal is not to create isolated summaries. The goal is to compile knowledge into a durable, Obsidian-compatible graph that grows more useful as sources, questions, and synthesis passes accumulate.

## Operating document structure

- `AGENTS.md`: project constitution for the agent.
- `docs/ingestion_workflow.md`: how new sources enter the wiki.
- `docs/synthesis_workflow.md`: how accumulated notes become higher-level maps.
- `docs/lint_workflow.md`: how the wiki is checked for structure, links, notation, duplication, and abstraction-level drift.
- `docs/research_roadmap.md`: current research tracks and future study direction.

## Core principles

- Raw sources in `data/raw/` are immutable.
- Wiki pages are Obsidian-compatible Markdown.
- The graph matters: important relationships should be represented with Obsidian links such as `[[ELBO]]`.
- Source claims and interpretation must remain separate.
- Concepts, math notes, source notes, and synthesis pages have different jobs.
- Weak or uncertain claims should be marked `Needs verification`.
- Lint passes should improve structure and connectivity without inventing new source material.
