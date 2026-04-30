# Synthesis Workflow

This document describes how accumulated notes become higher-level maps.

## Purpose

Synthesis pages prevent the wiki from becoming only a sequence of paper summaries.

They organize already-ingested knowledge into a mental model:
- what problem area the track covers
- which design axes matter
- which concepts and math pages belong together
- which papers grounded the current understanding
- which gaps still need source-grounded work

Synthesis pages should also keep the wiki aligned with `docs/research_direction.md`: recent frontier topics are useful only when they are connected back to foundations, math, source notes, and historical development.

## When to create or update a synthesis page

Create or update a synthesis page after:
- several related papers have been ingested
- a new design axis appears
- an older source changes the interpretation of newer work
- a track becomes hard to navigate from individual notes alone
- the user asks for direction, consolidation, or a next-step plan

## What synthesis pages may include

- short definition of the track or design space
- main design axes
- historical progression
- important concepts
- relevant math pages
- anchor papers
- open gaps
- current mental model
- how recent variants connect to older foundations
- what should not be generalized yet

## What synthesis pages should avoid

- unsupported claims not grounded in notes
- long derivations that belong in math pages
- benchmark details that belong in paper notes
- implementation details unless they are central to the design axis
- pretending weak areas are settled

## Reliability

Synthesis pages may contain interpretation, but the interpretation must be clearly separated from source claims.

Use:
- `Claim from source`
- `My interpretation`
- `Needs verification`
- `Open question`

## Active synthesis pages

- [[Diffusion Design Space]]
- [[Efficient LLM Architecture]]
- [[Transformer Architecture]]
- [[Optimization and Training Stability]]

## Candidate synthesis pages

- [[Generative Modeling]]
- [[LLM Inference Systems]]
- Representation Learning and World Models
- Multimodal Generative Models
- Attention and KV Cache Design Space
- Optimizer Geometry
- Energy-Based Modeling
