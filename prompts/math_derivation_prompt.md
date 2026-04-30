# Math Derivation Prompt

Use this prompt when extracting or checking a derivation for a math note.

## Required context

Read:
- `AGENTS.md`
- `docs/ingestion_workflow.md`
- `docs/lint_workflow.md`
- `vault/Math/Notation Conventions.md`
- the relevant source note or raw source

## Output format

```text
Target math note:

Source:

Goal:

Canonical notation:
- ...

Source-specific notation:
- ...

Assumptions:
- ...

Derivation:
1. ...
2. ...
3. ...

Skipped steps:
- ...

Interpretation:
- ...

Common mistakes:
- ...

Connections:
- Related math:
- Related concepts:
- Related papers:

Needs verification:
- ...
```

## Rules

- Do not silently normalize notation across sources.
- If notation differs, state the mapping and mark uncertain mappings as `Needs verification`.
- Do not skip algebra unless the skipped step is explicitly named.
- Keep source-specific derivations in paper notes when they are not generally useful.
- Put reusable definitions, assumptions, and derivation structure in math notes.
- Format math for Obsidian/MathJax: `$...$` for inline math and `$$...$$` for display equations.
- Use braces for grouped superscripts and multi-character subscripts, for example `$x^{(t)}$`, `$\sqrt{d_k}$`, and `$c_{skip}$`.
- Use `\frac{...}{...}` for mathematical fractions in equations.
- Use `$\mathbb{E}_{q}[\cdot]$` for expectations, `$\sim$` for distribution notation, and `$D_{KL}(q \| p)$` for KL arguments.
- Avoid raw ASCII math operators in equations, such as `*`, `||`, `<=`, `>=`, and `~`; use MathJax equivalents.
- Use backticks only for literal code, paths, commands, or pseudocode, not for mathematical formulas.
