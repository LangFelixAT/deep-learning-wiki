# Lint Workflow

This document defines what a wiki lint pass means for this project.

The lint pass keeps the wiki aligned with the LLM Wiki pattern: persistent, interlinked, Obsidian-compatible Markdown that accumulates structure instead of forcing the LLM to rediscover knowledge from raw sources each time.

Lint passes should also check alignment with `docs/research_direction.md`, especially when recent frontier topics have been added.

## Purpose

A lint pass should improve:
- structure
- links and backlinks
- notation consistency
- source separation
- abstraction levels
- navigation through `Home`, `index`, timelines, and synthesis hubs

It should not become a new ingest.

## Obsidian compliance

All lint work must preserve Obsidian-compatible Markdown.

Check:
- Use Obsidian links such as `[[ELBO]]` for real note relationships.
- Prefer simple note-title links such as `[[ELBO]]`.
- Avoid folder-qualified link targets such as `Math/ELBO|ELBO` unless there is a deliberate reason.
- Keep filenames unique across the vault so links stay unambiguous.
- If a planned concept is important enough to link, create a short stub rather than leaving a dangling link.
- Do not create excessive links; link relationships that are meaningful for navigation or synthesis.

## Structure checks

Check whether pages match their type.

Paper notes should:
- preserve source claims
- include metadata, reliability, and source type
- separate claims from interpretation
- avoid importing later work into older source notes except as clearly labeled connections

Math notes should:
- include goal, definitions, assumptions, derivation, interpretation, common mistakes, and related concepts
- state canonical notation
- mark skipped derivation steps explicitly
- avoid verified status unless derivations were checked carefully

Concept notes should:
- include short definition, intuition, mathematical formulation, historical development, related papers, related concepts, open questions, and source notes when useful
- synthesize across sources without pretending weak connections are settled

Synthesis pages should:
- organize a track or design space
- connect source notes, math notes, and concept notes
- identify open gaps
- avoid unsupported claims
- connect recent frontier topics back to source-grounded foundations where possible

Index and timeline pages may be lighter than normal concept pages, but they should still have metadata, purpose or short definition, orientation, and related links.

## Linking checks

Check:
- unresolved wiki links
- folder-qualified wiki links
- duplicate note basenames
- orphan or low-backlink pages
- important source notes not linked from relevant concept pages
- important concept/math notes not listed in `vault/index.md`
- missing links from `vault/Home.md` for major hubs
- missing roadmap entries for new research tracks
- missing cross-track links where a topic connects architecture, math, systems, optimization, representation learning, or generative modeling

Low-backlink pages are not automatically wrong. Stubs, templates, and future placeholders may be acceptable if they are intentional.

## Notation checks

Use [[Notation Conventions]] as the canonical reference.

Pay special attention to:
- `q_phi(z|x)`
- `p_theta(x,z)`
- `p_theta(z|x)`
- `ELBO`
- `epsilon_theta`
- `s_theta`
- `sigma`
- `alpha_bar_t`
- `x_0`, `x_t`, `x_T`
- `z_t`
- `Q`, `K`, `V`, `d_k`
- `n_h`, `d_h`, `d_c`

If notation differs across sources, do not silently normalize equations. Mention the source-specific notation and mark uncertain mappings as `Needs verification`.

## Duplication checks

Distinguish useful overlap from bad duplication.

Useful overlap:
- `[[Transformers]]` as a base concept and `[[Transformer Architecture]]` as a synthesis hub.
- `[[Diffusion Models]]` as a concept and `[[Diffusion Design Space]]` as a design-space synthesis.
- `[[Efficient LLM Architecture]]` as an architecture synthesis and `[[LLM Inference Systems]]` as a future serving-systems hub.

Bad duplication:
- two pages with the same title
- the same mathematical derivation copied into multiple pages
- source claims repeated as interpretation without attribution
- concept pages and paper notes both trying to serve as the same synthesis hub

## Abstraction-level checks

Make sure each page has a clear job:
- Paper: historical source and claims.
- Math: formal definitions and derivations.
- Concept: intuition and connections.
- Synthesis: cross-page map of a track or design space.
- Index/timeline: navigation.

If a page mixes jobs, prefer a small correction:
- move detailed equations toward math notes
- move broad interpretation toward concept or synthesis pages
- keep source-specific claims in paper notes

## Safe fixes

Apply small safe fixes when clear:
- broken links
- missing backlinks
- missing index entries
- missing `Home` entries for major hubs
- section headers needed for consistency
- minor notation wording
- explicit `Needs verification` labels
- short stubs for important planned linked pages

Avoid:
- rewriting whole pages
- adding new source material
- expanding advanced topics without a source
- renaming files unless the user asks or ambiguity is severe
- deleting pages

## Expected output

When reporting a lint pass, group issues by:
- Structure
- Linking
- Notation
- Duplication
- Abstraction level

Then list concrete fixes.

If fixes were applied, list every created or modified file and briefly explain why.
