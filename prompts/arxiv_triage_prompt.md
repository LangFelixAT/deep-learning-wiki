# Manual Source Triage Prompt

Use this prompt for manually evaluating a candidate paper or source before ingestion.

Do not implement automated arXiv scanning. This prompt is for user-provided sources or explicit manual lookup tasks.

## Required context

Read:
- `AGENTS.md`
- `docs/research_direction.md`
- `docs/research_roadmap.md`
- `docs/ingestion_workflow.md`

## Triage questions

Evaluate:
- What research track does this source belong to?
- Which foundation does it strengthen: representation, objective, architecture, inference/sampling, optimization, systems, multimodality, or energy-based modeling?
- Is it an anchor source, a refinement source, or a frontier update?
- Which existing pages would it connect to?
- Which math notes would need updating or creation?
- Which concept or synthesis pages would it affect?
- Is the source likely to create duplicate explanations?
- What should be explicitly out of scope during ingestion?

## Output format

```text
Recommended filename:

Recommended note title:

Research track:

Why ingest:

Suggested scope:
- ...

Do not include:
- ...

Likely pages to update:
- ...

Possible new pages:
- ...

Risks / Needs verification:
- ...
```

## Grounding rule

Recent frontier sources are allowed, but only if they are connected back to source-grounded foundations and the user's current research direction.
