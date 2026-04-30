# Muon source capture - KellerJordan/Muon README

## Metadata
- Repository: KellerJordan/Muon
- URL: https://github.com/KellerJordan/Muon
- Raw README URL: https://raw.githubusercontent.com/KellerJordan/Muon/master/README.md
- Source type: repository README
- Accessed: 2026-04-30
- License shown by repository: MIT
- Reliability for wiki use: medium
- Reason: primary implementation README for an emerging optimizer; useful for intended usage and parameter grouping, not a peer-reviewed source.

## Copyright note
This is a source capture, not a verbatim mirror. It records provenance, short excerpts, and detailed paraphrase of the README.

## Short exact excerpts
- "hidden weights"
- "standard AdamW"
- "ns_steps"

## Source overview
The README presents the repository as an implementation of Muon, with links to the original thread and Keller Jordan writeup. It gives installation instructions, a parameter-grouping usage pattern, example links, basic hyperparameter guidance, benchmark pointers, accomplishments, additional learning resources, and a citation.

## Detailed paraphrase

### Intended use
The README says Muon is for hidden weights in neural networks. It recommends using AdamW for other parameter classes, including embeddings, output/classifier heads, and gains/biases.

For convolutional networks, the README suggests using Muon for most convolutional filters except the first, while leaving other parameters to AdamW.

### Parameter grouping pattern
The README's usage pattern separates:
- hidden matrix-like weights that use Muon
- hidden gains and biases that use AdamW
- non-hidden parameters such as head and embedding parameters that use AdamW

This is important for the wiki because Muon is not positioned as a universal optimizer for all parameters.

### Hyperparameters
The README says defaults for momentum, Nesterov behavior, and Newton-Schulz step count often work. It says learning rate and weight decay still need tuning. It also mentions a learning-rate scaling expectation related to muP.

Any muP discussion should be treated as a future connection unless a source on muP is ingested.

### Benchmarks and accomplishments
The README links to benchmark comparisons and speedrun claims. These should be treated as source claims and not generalized without later corroborating sources.

### Citation
The README provides a `@misc` citation for the Muon writeup with authors Keller Jordan, Yuchen Jin, Vlado Boza, Jiacheng You, Franz Cesista, Laker Newhouse, and Jeremy Bernstein.

## Key claims to preserve as source claims
- Muon is intended for hidden weights.
- AdamW remains recommended for non-hidden and non-matrix-like parameters.
- Parameter grouping is part of practical Muon usage.
- Benchmark and adoption claims are linked but should be labeled as source claims.

## Links captured from README
- Main writeup: https://kellerjordan.github.io/posts/muon/
- Original X thread: https://x.com/kellerjordan0/status/1842300916864844014
- NanoGPT example: https://github.com/KellerJordan/modded-nanogpt
- CIFAR-10 example: https://github.com/KellerJordan/cifar10-airbench
- Optimizer benchmark records: https://github.com/KellerJordan/modded-nanogpt/tree/master/records/102924_Optimizers
- Kimi/Moonshot scaling report: https://arxiv.org/abs/2502.16982

## Ingestion cautions
- Keep README claims separate from blog claims.
- Do not ingest usage code in detail unless the user asks for implementation notes.
- Do not treat the README's benchmark list as peer-reviewed evidence.

