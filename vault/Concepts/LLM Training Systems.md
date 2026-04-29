# LLM Training Systems

## Metadata
- Type: concept
- Status: stub
- Last reviewed: 2026-04-29

## Short definition
LLM training systems are the infrastructure and numerical methods used to train large language models efficiently at scale.

## Intuition
Large-model capability is not only a model-architecture question. Training depends on memory, communication, parallelism, numerical precision, and hardware utilization.

## Mathematical formulation
- Related math:
- Needs verification: add formal notes for parallelism, precision, and communication cost after source-grounded ingests.

## Historical development
[[2024 DeepSeek-V3 Technical Report]] frames DeepSeek-V3 as a co-design of algorithms, training framework, and hardware use, including FP8 mixed precision and communication-overlap strategies.

## Related papers
- [[2024 DeepSeek-V3 Technical Report]]

## Related concepts
- [[Large Language Models]]
- [[Transformers]]
- [[Mixture of Experts]]
- [[Expert Routing]]
- [[KV Cache]]

## Open questions
- Needs verification: separate notes are needed for FP8 training, pipeline parallelism, expert parallelism, and communication overlap.

## My understanding
Training systems are where model design choices become resource constraints. Sparse experts, low precision, and parallelism have to fit together for a large model to be trainable.

## Source notes
- [[2024 DeepSeek-V3 Technical Report]]

## Revision notes
