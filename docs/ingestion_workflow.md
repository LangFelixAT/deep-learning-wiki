# Ingestion Workflow

This document describes how new knowledge enters the wiki.

## Step 1: Identify the source

Classify the source as one of:

- paper
- video
- lecture
- book chapter
- blog post
- documentation
- personal note

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

Every note should have a status:

- unread
- skimmed
- studied
- verified

Only use "verified" after manually checking important claims.

## Step 8: Update index and log

After ingestion:
- update `vault/index.md`
- append an entry to `vault/log.md`

Follow the format defined in `AGENTS.md`.