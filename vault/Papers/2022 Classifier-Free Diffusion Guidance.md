# Classifier-Free Diffusion Guidance

## Metadata
- Authors: Ho, Salimans
- Year: 2022
- Link: https://arxiv.org/abs/2207.12598
- Source type: paper
- Status: studied
- Reliability: high

## Scope
This ingest covers only the core classifier-free guidance mechanism: conditional vs unconditional diffusion models, condition dropout during training, the guidance formula, guidance scale `w`, and intuition for steering samples toward the condition.

## One-sentence summary
Classifier-free guidance trains conditional and unconditional diffusion behavior in one model and combines their predictions at sampling time to steer samples toward a condition without an external classifier.

## Problem
Classifier guidance can improve conditional diffusion sample fidelity, but it requires a separate noisy-data classifier and uses classifier gradients during sampling.

## Core ideas
- A conditional diffusion model predicts a denoising direction using conditioning information `c`.
- An unconditional diffusion model predicts without conditioning.
- Classifier-free guidance trains both behaviors jointly by randomly dropping the condition during training.
- During sampling, conditional and unconditional predictions are linearly combined.
- The guidance strength `w` controls how strongly sampling is pushed toward the condition.

## Important equations
Condition dropout training:

`c <- empty` with probability $p_{\mathrm{uncond}}$.

Classifier-free guided score:

$$
s_{guided}(x_t,t,c) = (1 + w) s_{\theta}(x_t,t,c) - w s_{\theta}(x_t,t)
$$
Equivalent noise-prediction form:

$$
\epsilon_{guided}(x_t,t,c) = (1 + w) \epsilon_{\theta}(x_t,t,c) - w \epsilon_{\theta}(x_t,t)
$$
Needs verification: exact signs and scaling depend on whether the model is written in score, noise, or denoised-data parameterization.

## Claims from source
- Claim from source: classifier-free guidance avoids training a separate classifier.
- Claim from source: conditional and unconditional diffusion models can be jointly trained by randomly replacing the condition with a null conditioning token.
- Claim from source: conditional sampling uses a linear combination of conditional and unconditional score estimates.
- Claim from source: sweeping the guidance strength trades off sample quality and diversity similarly to classifier guidance.
- Claim from source: classifier-free guidance uses only generative model predictions, not classifier gradients.

## Limitations
- Each guided sampling step may require both conditional and unconditional model evaluations.
- Larger guidance can reduce diversity.
- The paper studies guidance behavior empirically; optimal `w` and condition dropout probability are task/model dependent.
- This note does not include architecture details, text encoders, implementation tricks, or large-system details.

## My interpretation
Classifier-free guidance makes conditioning a sampling-time direction: the difference between conditional and unconditional predictions estimates how the condition should steer the reverse process.

## Connections
- [[Diffusion Models]]
- [[Score Matching]]
- [[Classifier-Free Guidance]]
- [[Diffusion ODE Solvers]]
