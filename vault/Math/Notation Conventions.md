# Notation Conventions

## Metadata
- Type: math
- Status: developing
- Last reviewed: 2026-04-29

## Goal
Collect canonical notation used across the wiki so related math and concept notes remain consistent.

## Definitions

### Probability and likelihood
- $p(x)$: probability mass or density of observed variable $x$.
- $p(x,z)$: joint distribution over observed and latent variables.
- $p(z|x)$: posterior or conditional distribution of latent variable $z$ given observation $x$.
- $p(x|z)$: likelihood of observation $x$ given latent variable $z$.
- $E_p[f(x)]$: expectation of $f(x)$ under distribution $p$.
- $\theta$: model parameters.

### Variational inference
- $x$: observed data.
- $z$: latent variable.
- $p_{\theta}(x,z)$: generative joint distribution.
- $p_{\theta}(z|x)$: true posterior under the generative model.
- $q_{\phi}(z|x)$: approximate posterior or inference model.
- $ELBO$: lower bound on $\log p_{\theta}(x)$.

### Diffusion models
- $x_0$: clean data sample in data space.
- $x_t$: noisy data-space state at timestep $t$.
- $x_T$: high-noise terminal state.
- $z_t$: noisy latent-space state in latent diffusion notes.
- $\epsilon$: Gaussian noise sample, usually $\epsilon ~ \mathcal{N}(0,I)$.
- $\epsilon_{\theta}(x_t,t)$: learned DDPM-style noise predictor unless a source defines different notation.
- $s_{\theta}(x,t)$: learned score estimate, usually approximating $\nabla_x \log p_t(x)$.
- $\sigma$ or $\sigma_t$: noise scale; exact meaning depends on parameterization.
- $\bar{\alpha}_t$: cumulative DDPM noise-schedule product.

### Transformer attention
- $Q$: query matrix.
- $K$: key matrix.
- $V$: value matrix.
- $d_k$: query/key dimension used in scaled dot-product attention.
- $d_v$: value dimension.
- $h$ or $n_h$: number of attention heads.
- $d_h$: per-head dimension in several efficient-attention notes.

### Normalization
- $a_i$: activation or summed input component for feature $i$.
- $\mu$: feature mean used by LayerNorm.
- $\sigma$: feature standard deviation used by LayerNorm.
- $\operatorname{RMS}(a)$: root mean square used by RMSNorm.
- $g_i$: learned gain parameter.

### Optimization
- $\theta_t$: parameter vector after timestep $t$.
- $g_t$: stochastic gradient at timestep $t$.
- $\alpha$: learning rate or stepsize.
- $m_t$: Adam first moment estimate.
- $v_t$: Adam second raw moment estimate.
- $\hat{m}_t$: bias-corrected Adam first moment estimate.
- $\hat{v}_t$: bias-corrected Adam second raw moment estimate.
- $\beta_1$: Adam first moment exponential decay rate.
- $\beta_2$: Adam second raw moment exponential decay rate.
- $\epsilon$: small numerical constant used in optimizer denominators.
- $\lambda$: weight decay factor in [[AdamW]] and [[Weight Decay]] notes; sharpness parameter in [[Steepest Descent]] contexts.
- $\lambda'$: L2 regularization coefficient when distinguishing L2 penalties from decoupled weight decay.
- $\beta_t$: schedule multiplier used in [[2017 Decoupled Weight Decay Regularization]].
- $W_t$: matrix-valued weight parameter in matrix-aware optimizer notes.
- $G_t$: gradient or update matrix in matrix-aware optimizer notes.
- $L_t$: left preconditioner in the matrix case of [[Shampoo]].
- $R_t$: right preconditioner in the matrix case of [[Shampoo]].
- $P_t$: generic preconditioner in [[Preconditioning]].
- $M_t$: momentum buffer or generic adaptive preconditioner depending on optimizer context.
- $Ortho(G)$: idealized orthogonalized update matrix in [[Muon Optimizer (Math)]].
- $U S V^T$: singular value decomposition notation used in matrix-aware optimizer notes.
- `A, B`: matrix dimensions used in [[Muon Optimizer (Math)]] update-scaling notes.
- $update RMS$: root mean square magnitude of an optimizer update.
- `delta`: vector update in [[Steepest Descent]] notes.
- `Delta W`: matrix update in optimizer-geometry notes.
- $\|\cdot\|$: chosen update norm; source-specific.
- $\|\cdot\|_*$: dual norm.

### Efficient LLM architecture
- `KV cache`: stored keys and values reused during autoregressive decoding.
- $n_h$: number of query heads in efficient-attention notes unless the source uses a different symbol.
- $d_c$: compressed key/value latent dimension in [[Multi-Head Latent Attention (Math)]].
- $d_h^R$: decoupled RoPE key/query dimension in [[Multi-Head Latent Attention (Math)]].
- $N$: number of experts in MoE routing notes.
- $E_i$: expert $i$.

## Assumptions
- This page records wiki-level conventions, not a universal standard.
- Source-specific notation takes priority inside a source note.
- When mapping between papers, coefficients and dimensions must be checked before transferring equations.

## Interpretation
The same symbols are reused differently across deep learning subfields. A central convention page helps keep concept pages readable while preserving source-specific notation in paper and math notes.

## Common mistakes
- Treating $z_t$ in latent diffusion as the same object as VAE latent variable $z$ without checking context.
- Treating $\sigma$ in EDM-style notes and $\bar{\alpha}_t$ in DDPM-style notes as directly interchangeable without a schedule mapping.
- Assuming $\epsilon_{\theta}$ and $s_{\theta}$ have the same sign and scaling across parameterizations.
- Confusing number of query heads with number of key/value heads in MQA, GQA, and MLA notes.
- Treating $v_t$ in [[Adam]] as a centered variance rather than a second raw moment estimate.
- Treating $\lambda$ and $\lambda'$ as interchangeable without checking whether a note is using weight decay or L2 regularization.
- Treating $\lambda$ in steepest-descent notes as the same object as weight decay without checking context.
- Reusing $M_t$ without checking context: in AdamW notes it may denote a generic preconditioner, while in Muon notes it may denote a momentum buffer.
- Reusing $\epsilon$ without checking context: it can be an optimizer denominator constant, a preconditioner stabilizer, or Gaussian noise in diffusion notes.

## Related concepts
- [[Variational Inference]]
- [[ELBO]]
- [[Diffusion Models]]
- [[Diffusion Parameterization]]
- [[Scaled Dot-Product Attention]]
- [[RMSNorm (Math)]]
- [[Adam]]
- [[AdamW]]
- [[Weight Decay]]
- [[Steepest Descent]]
- [[Preconditioning]]
- [[Shampoo]]
- [[Muon Optimizer (Math)]]
- [[Newton-Schulz Iteration]]
- [[Multi-Head Latent Attention (Math)]]
- [[Expert Routing]]

## Source references
- [[2013 Auto-Encoding Variational Bayes]]
- [[2019 Introduction to Variational Autoencoders]]
- [[2020 Denoising Diffusion Probabilistic Models]]
- [[2022 Elucidating the Design Space of Diffusion-Based Generative Models]]
- [[2017 Attention Is All You Need]]
- [[2014 Adam]]
- [[2017 Decoupled Weight Decay Regularization]]
- [[2018 Shampoo]]
- [[2024 Old Optimizer New Norm]]
- [[2024 Muon Optimizer]]
- [[2025 Muon is Scalable for LLM Training]]
- [[2024 DeepSeek-V2 Technical Report]]
- [[2021 Switch Transformers]]

## Verification status
- Status: developing
- Needs verification: source-specific notation mappings should be checked before adding exact conversion formulas.
