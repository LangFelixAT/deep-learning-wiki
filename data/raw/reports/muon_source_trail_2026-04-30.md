# Muon source trail

## Metadata
- Topic: Muon optimizer source provenance
- Created: 2026-04-30
- Source type: source-trail capture
- Purpose: identify what should be ingested before creating a wiki note for Muon Optimizer

## Core primary sources

### Keller Jordan writeup
- Title: Muon: An optimizer for hidden layers in neural networks
- URL: https://kellerjordan.github.io/posts/muon/
- Date: 2024-12-08
- Role: primary explanatory writeup
- Best use: definition, design, Newton-Schulz orthogonalization, relationship to Shampoo, empirical cautions, open questions
- Suggested local capture: `data/raw/blogs/muon_keller_jordan_2024.md`

### KellerJordan/Muon repository
- URL: https://github.com/KellerJordan/Muon
- Role: primary implementation
- Best use: parameter grouping, implementation-level confirmation, README usage guidance
- Suggested local captures:
  - `data/raw/repos/muon_keller_jordan_readme_2024.md`
  - `data/raw/repos/muon_keller_jordan_muon_py_2024.md`

### Original X thread
- URL: https://x.com/kellerjordan0/status/1842300916864844014
- Archived snapshot referenced by writeup: https://archive.is/RZYBG
- Role: historical origin of the optimizer announcement
- Best use: provenance only unless user specifically wants social-thread ingestion
- Caution: X content may be hard to access reliably; use only as provenance unless archived content is available and relevant.

## Theory bridge sources

### Shampoo
- Title: Shampoo: Preconditioned Stochastic Tensor Optimization
- Authors: Vineet Gupta; Tomer Koren; Yoram Singer
- Year: 2018
- URL: https://arxiv.org/abs/1802.09568
- Role: matrix/tensor-aware preconditioning predecessor
- Best use: bridge from AdamW to matrix-aware optimizers before Muon

### Old Optimizer, New Norm
- Title: Old Optimizer, New Norm: An Anthology
- Authors: Jeremy Bernstein; Laker Newhouse
- Year: 2024
- URL: https://arxiv.org/abs/2409.20325
- Role: norm/steepest-descent framing referenced by the Muon writeup
- Best use: theory bridge for why tensor roles may call for different update norms

## Scaling / later adoption sources

### Muon is Scalable for LLM Training
- Authors: Jingyuan Liu, Jianlin Su, Xingcheng Yao, and others
- Year: 2025
- URL: https://arxiv.org/abs/2502.16982
- Role: later scaling report from Moonshot/Kimi context
- Best use: separate ingest after base Muon, not part of first Muon concept note
- Caution: contains large-scale empirical claims; keep clearly labeled as source claims.

### Practical Efficiency of Muon for Pretraining
- URL: https://arxiv.org/abs/2505.02222
- Role: later empirical/practical efficiency source
- Best use: later comparison source, not needed for first Muon ingest

## Recommended ingestion order
1. Ingest Shampoo first if the goal is a clean math bridge from coordinatewise adaptivity to matrix-aware optimization.
2. Ingest Muon from the Keller Jordan writeup plus repository captures.
3. Ingest Bernstein-Newhouse if we want the norm-based theory framing.
4. Ingest Moonshot/Kimi scaling only after base Muon is established.

## Recommended first Muon ingest scope
- Muon as an optimizer for hidden-layer 2D parameters.
- Momentum update followed by approximate orthogonalization.
- Newton-Schulz iteration as practical approximate orthogonalization.
- Relationship to AdamW: AdamW remains used for embeddings, heads, scalar/vector parameters, gains, and biases.
- Relationship to Shampoo: matrix-aware/orthogonalized update connection, marked `Needs verification` until Shampoo is ingested.
- Current empirical claims as source claims only.
- Open questions around scale, distributed training, finetuning, and reinforcement learning.

## Do not include in first Muon ingest
- Full code implementation.
- Detailed benchmark tables.
- Long social-thread content.
- Large-scale Moonshot/Kimi claims except as future connections.
- Deep Newton-Schulz convergence proof.
- Full Shampoo derivation unless Shampoo has been ingested.
