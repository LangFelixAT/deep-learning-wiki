# LLM Training Systems

## Metadata
- Type: concept
- Status: developing
- Last reviewed: 2026-04-29

## Short definition
LLM training systems are the infrastructure and numerical methods used to train large language models efficiently at scale.

## Intuition
Large-model capability is not only a model-architecture question. Training depends on memory, communication, parallelism, numerical precision, and hardware utilization.

## Mathematical formulation
- Related math: [[Expert Routing]], [[AdamW]], [[Muon Optimizer (Math)]], [[Weight Decay]]
- Needs verification: add formal notes for parallelism, precision, and communication cost after source-grounded ingests.
- [[2024 DeepSeek-V3 Technical Report]] treats FP8 mixed precision, communication overlap, and MoE training constraints as part of the same efficiency problem.

## Historical development
[[2024 DeepSeek-V3 Technical Report]] frames DeepSeek-V3 as a co-design of algorithms, training framework, and hardware use, including FP8 mixed precision and communication-overlap strategies.

The same source reports that some components remain in higher precision for stability while compute-heavy linear operations use FP8.

[[2025 Muon is Scalable for LLM Training]] adds optimizer choice as a training-system constraint: matrix-aware optimizers may require distributed update computation and parameter-group handling, even when the architecture is otherwise fixed.

## Related papers
- [[2024 DeepSeek-V3 Technical Report]]
- [[2025 Muon is Scalable for LLM Training]]

## Related concepts
- [[Large Language Models]]
- [[Transformers]]
- [[Mixture of Experts]]
- [[Expert Routing]]
- [[KV Cache]]
- [[Muon Optimizer]]
- [[Optimization and Training Stability]]

## Open questions
- Needs verification: separate notes are needed for FP8 training, pipeline parallelism, expert parallelism, communication overlap, and distributed optimizer state.
- Needs verification: multi-token prediction should be separated from systems topics if it becomes a training-objective note.

## My understanding
Training systems are where model design choices become resource constraints. Sparse experts, low precision, and parallelism have to fit together for a large model to be trainable.

## Source notes
- [[2024 DeepSeek-V3 Technical Report]]
- [[2025 Muon is Scalable for LLM Training]]

## Revision notes
