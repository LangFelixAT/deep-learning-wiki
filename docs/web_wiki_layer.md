# Web Wiki Layer

## Purpose

The web wiki layer renders the canonical Obsidian vault as a local Quartz site.

`vault/` remains the source of truth. Quartz should be treated as a publishing and browsing layer, not as a second editing location for notes.

## Local commands

From `quartz/`:

```powershell
npm run build:vault
npm run serve:vault
```

The preview server uses:

```text
http://localhost:8080
```

## Content model

- Source Markdown lives in `vault/`.
- Quartz reads `../vault` directly.
- Generated output goes to `quartz/public/`.
- Installed dependencies and plugin cache stay under `quartz/node_modules/` and `quartz/.quartz/`.

## Notes

- `quartz/content/` is ignored so the web layer does not duplicate the vault.
- `vault/Templates/` and `.obsidian/` are ignored by Quartz.
- The first prototype uses Quartz's Obsidian template with wikilinks, backlinks, graph view, search, and LaTeX enabled.
