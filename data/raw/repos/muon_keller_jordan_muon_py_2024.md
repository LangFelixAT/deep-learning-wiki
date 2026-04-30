# Muon source capture - KellerJordan/Muon implementation

## Metadata
- Repository: KellerJordan/Muon
- File: muon.py
- URL: https://github.com/KellerJordan/Muon/blob/master/muon.py
- Raw URL: https://raw.githubusercontent.com/KellerJordan/Muon/master/muon.py
- Source type: repository implementation
- Accessed: 2026-04-30
- License shown by repository: MIT
- Reliability for wiki use: medium
- Reason: primary implementation; useful for checking algorithmic details, but implementation may change over time.

## Copyright note
This file is not a verbatim copy of the implementation. It captures structure and behavior at a high level for later ingestion.

## Short exact excerpts
- "zeroth power"
- "nearest orthogonal matrix"
- "hidden weight layers"

## Implementation structure
The implementation exposes:
- a Newton-Schulz-based orthogonalization helper
- a Muon update helper
- a distributed Muon optimizer
- a single-device Muon optimizer
- an Adam-style update helper
- a Muon-with-auxiliary-Adam optimizer
- a single-device Muon-with-auxiliary-Adam optimizer

## Detailed paraphrase

### Newton-Schulz helper
The implementation computes an approximate matrix zeroth power / orthogonalized update using a fixed quintic Newton-Schulz-style iteration. It normalizes the input matrix before iterating and handles rectangular matrices by transposing when useful.

The implementation comments indicate that the iteration does not necessarily produce exact `UV^T`; instead it produces an approximation whose singular values are in a useful range for training.

### Muon update
The update begins with momentum. If Nesterov behavior is enabled, the update combines the current gradient with the momentum buffer in the Nesterov style. For 4D convolution filters, the update is reshaped to a 2D matrix before orthogonalization.

After orthogonalization, the update is scaled according to matrix shape before being applied.

### Optimizer step
For Muon parameter groups, the optimizer:
- maintains a momentum buffer
- computes the Muon update
- applies AdamW-style decoupled weight decay
- applies the orthogonalized update with the group learning rate

For non-Muon parameter groups in the auxiliary optimizer, it uses an Adam-style update with decoupled weight decay.

### Practical implication
The implementation reinforces the source guidance that Muon is a partial optimizer: it is used for compatible hidden matrix parameters, while Adam-style updates handle other parameters.

## Key details to preserve as source claims
- The implementation uses Newton-Schulz-style approximate orthogonalization.
- The implementation applies weight decay in an AdamW-style decoupled way.
- MuonWithAuxAdam separates Muon-compatible and Adam-compatible parameter groups.
- The implementation supports distributed and single-device variants.

## Ingestion cautions
- Do not freeze implementation details as mathematical definitions without checking the writeup.
- Do not include code-level distributed details in the wiki unless the user asks.
- If the repo changes, this capture may need a refresh before precise implementation claims.

