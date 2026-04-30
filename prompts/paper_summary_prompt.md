# Paper Summary Prompt

Use this prompt for a faithful, source-grounded summary of one paper before or during ingestion.

This is not a replacement for a full wiki ingest. It is a compact reading aid.

## Required context

Read:
- `AGENTS.md`
- `docs/research_direction.md`
- `docs/research_roadmap.md`

Use the source itself as ground truth. Do not import later claims unless clearly labeled as external context.

## Output format

```text
Title:
Authors / year:
Source type:
Reliability:

One-sentence summary:

Problem:

Core idea:

Method:

Important equations or mechanisms:

Claims from source:
- ...

Limitations from source:
- ...

My interpretation:
- ...

Connections:
- Existing concepts:
- Existing math:
- Existing papers:

Needs verification:
- ...

Suggested ingest scope:
- ...

Exclude:
- ...
```

## Rules

- Separate source claims from interpretation.
- Prefer precise, minimal statements over broad claims.
- Mark uncertainty as `Needs verification`.
- For frontier sources, state which foundation the paper strengthens.
