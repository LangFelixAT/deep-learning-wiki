# Muon source capture - Keller Jordan writeup

## Metadata
- Source title: Muon: An optimizer for hidden layers in neural networks
- Author: Keller Jordan, with listed contributors Yuchen Jin, Vlado Boza, Jiacheng You, Franz Cesista, Laker Newhouse, Jeremy Bernstein
- Date on source: 2024-12-08
- Source type: blog / technical writeup
- URL: https://kellerjordan.github.io/posts/muon/
- Accessed: 2026-04-30
- Reliability for wiki use: medium
- Reason: primary author writeup for an emerging optimizer, not a peer-reviewed archival paper.

## Copyright note
This is a source capture, not a verbatim mirror. It records provenance, section structure, short excerpts, and detailed paraphrase so the wiki can ingest the source while preserving copyright boundaries.

## Short exact excerpts
- "optimizer for 2D parameters"
- "MomentUm Orthogonalized by Newton-Schulz"
- "Remaining open questions"

## Source structure
- Definition
- Results
- The design of Muon
- Why orthogonalize the update?
- Eliminating alternatives to Newton-Schulz iteration
- Proving that Newton-Schulz iteration orthogonalizes the update
- Tuning the coefficients
- Runtime analysis
- Relationship to prior optimizers
- Empirical considerations
- Discussion on competitive training tasks
- Remaining open questions
- Contributors
- References

## Detailed paraphrase

### Definition
The writeup defines Muon as an optimizer intended for hidden-layer matrix parameters. It does not present Muon as a drop-in optimizer for every parameter tensor. Scalar parameters, vector parameters, embeddings, and output layers are treated as better handled by a standard optimizer such as AdamW.

The core algorithm starts from an SGD-momentum-like update for a 2D parameter, then applies a Newton-Schulz matrix iteration to approximately orthogonalize the update before applying it to the weights.

### Newton-Schulz role
The source presents Newton-Schulz iteration as an efficient way to approximately replace an update matrix with a semi-orthogonal version. The writeup contrasts this with using an SVD directly, which is conceptually simple but too slow for the intended training use case.

The source uses a quintic iteration with tuned coefficients and says a small fixed number of Newton-Schulz steps is enough in the reported experiments. It also emphasizes that the implementation can run in bfloat16, which is part of the practical motivation.

### Orthogonalization intuition
The source argues that updates from SGD-momentum and Adam for transformer hidden matrices often appear poorly conditioned, with a few dominant directions. The author speculates that orthogonalizing updates can lift smaller but useful directions.

This should be treated as source interpretation, not settled theory.

### Relationship to Shampoo
The writeup explicitly connects Muon to Shampoo and Bernstein-Newhouse's analysis. The key source idea is that, without preconditioner accumulation, a Shampoo-like expression can reduce to an orthogonalized-gradient update. Muon can therefore be interpreted as related to a cheaper, momentum-before-orthogonalization form of this matrix-aware family.

This relationship should be marked carefully in the wiki until the underlying Shampoo and Bernstein-Newhouse sources are ingested.

### Empirical claims
The source reports improvements on competitive training tasks, including NanoGPT speedrunning and CIFAR-10 speedrunning, and reports experiments at larger model scales. These are source claims and should not be treated as broad consensus without additional sources.

The writeup also states empirical usage guidance:
- use Muon for hidden 2D weight matrices
- use AdamW for embeddings, output layers, scalar parameters, vector parameters, gains, and biases
- for convolutional filters, flattening can make them compatible with the matrix update
- for transformers, applying Muon separately to Q, K, and V parameters was reported to work better than applying it to a fused QKV matrix

### Evidence standard
The writeup argues that competitive training tasks can reduce the undertuned-baseline problem in optimizer research. The source presents Muon's NanoGPT speedrunning record as evidence, while still listing open questions.

### Open questions from the source
The writeup asks whether Muon scales to larger training runs, whether the Newton-Schulz iterations can be distributed properly across large GPU clusters, and whether the method works outside pretraining, such as finetuning or reinforcement-learning workloads.

## Key claims to preserve as source claims
- Muon is designed for hidden-layer 2D parameters.
- Muon applies momentum first and orthogonalizes the update afterward.
- Newton-Schulz is selected for practical orthogonalization efficiency.
- Some parameters should remain on AdamW.
- The source links Muon to Shampoo-style matrix-aware optimization.
- Empirical performance claims should be labeled as claims from the source.

## Ingestion cautions
- Do not present Muon as a fully settled replacement for AdamW.
- Do not ingest benchmark claims without marking them as source claims.
- Do not explain the Shampoo connection in detail before ingesting Shampoo.
- Do not treat Newton-Schulz coefficients as universal theory; the source describes them as selected/tuned for practical behavior.
- Avoid implementation details beyond the conceptual update unless the user asks for code-level notes.

## Related source trail
- GitHub repository: https://github.com/KellerJordan/Muon
- Original X thread referenced by the repo: https://x.com/kellerjordan0/status/1842300916864844014
- Archived X snapshot referenced by the writeup: https://archive.is/RZYBG
- Shampoo paper: https://arxiv.org/abs/1802.09568
- Bernstein-Newhouse paper: https://arxiv.org/abs/2409.20325
- Kimi/Moonshot scaling report: https://arxiv.org/abs/2502.16982
