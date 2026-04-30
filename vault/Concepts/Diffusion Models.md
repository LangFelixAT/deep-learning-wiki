# Diffusion Models

## Metadata
- Type: concept
- Status: developing

## Short definition
Generative models that learn to reverse a gradual noising process.

## Intuition
In [[2015 Deep Unsupervised Learning using Nonequilibrium Thermodynamics]], a diffusion model starts with data, applies a forward process that gradually destroys structure, and learns a reverse process that restores structure from a tractable noise distribution.

In [[2020 Denoising Diffusion Probabilistic Models]], this idea is developed into the DDPM setup: data $x_0$ is gradually noised into $x_T$, and a learned reverse process denoises from $x_T$ back to a sample resembling data.

## Mathematical formulation
- Related math: [[Diffusion Forward Process]], [[Diffusion Reverse Process]], [[Diffusion ELBO]], [[Diffusion Parameterization]], [[Score Matching]], [[ELBO]], [[Notation Conventions]]
- Forward process: $q(x_t|x_{t-1})$ adds Gaussian noise according to a variance schedule.
- Reverse process: $p_{\theta}(x_{t-1}|x_t)$ is a learned Gaussian transition.
- Training uses a variational bound and, in DDPM, a simplified noise-prediction objective.
- In DDPM, predicting the added noise $\epsilon$ is closely related to estimating the score of a Gaussian-perturbed distribution. Needs verification: exact scaling and weighting depend on parameterization.
- [[2020 Denoising Diffusion Implicit Models]] uses the same trained noise-prediction objective as DDPM but changes the sampling process.
- In [[2021 Score-Based Generative Modeling through SDEs]], diffusion models are interpreted in continuous time with a [[Forward SDE]] from data to noise and a [[Reverse-Time SDE]] from noise back to data.
- [[2022 Elucidating the Design Space of Diffusion-Based Generative Models]] frames diffusion models as separable design choices: parameterization, denoiser preconditioning, sampler, schedule, and training objective.
- Conditional diffusion models can use [[Classifier-Free Guidance]] to steer samples toward conditioning information by combining conditional and unconditional predictions during sampling.
- [[Latent Diffusion Models]] move the diffusion process from pixel space to a learned latent space, making high-resolution generation more computationally scalable.
- Conditioning signals in modern diffusion systems often come from learned embedding models such as [[CLIP]], which convert text or other inputs into semantic vectors.
- [[Diffusion with Transformers]] replaces the usual U-Net denoising backbone with a transformer over image or latent tokens.

## Notation conventions
- $x_t$ denotes a noisy data-space state at timestep $t$.
- $z_t$ denotes a noisy latent-space state in latent diffusion notes.
- $\epsilon_{\theta}(x_t,t)$ denotes a learned noise prediction unless a source defines different notation.
- $s_{\theta}(x,t)$ denotes a learned score estimate.
- $\sigma$ or $\sigma_t$ denotes a noise scale; exact meaning is source- and parameterization-dependent.
- $\bar{\alpha}_t$ denotes the cumulative DDPM noise-schedule product.

## Historical development
[[2015 Deep Unsupervised Learning using Nonequilibrium Thermodynamics]] introduces diffusion probabilistic models as learned reversals of gradual noising Markov chains. It emphasizes the flexibility/tractability tradeoff, probability evaluation, and the idea that small diffusion steps make local reverse transitions easier to model.

[[2019 Generative Modeling by Estimating Gradients of the Data Distribution]] develops a score-based framework using multiple Gaussian noise levels and annealed Langevin dynamics. At a high level, DDPM's noise-prediction objective is related to denoising score matching, but the exact correspondence depends on parameterization and weighting. Needs verification.

[[2020 Denoising Diffusion Probabilistic Models]] demonstrates high-quality image synthesis with diffusion probabilistic models and highlights a connection to denoising score matching.

[[2021 Score-Based Generative Modeling through SDEs]] presents SMLD and DDPM as discretizations of different SDEs. In that framing, DDPM is related to a variance-preserving SDE. Needs verification: exact discretization details are not expanded here.

[[2020 Denoising Diffusion Implicit Models]] introduces DDIM sampling, which reuses a DDPM-trained $\epsilon_{\theta}(x_t,t)$ model with a non-Markovian generative process. It can sample deterministically when $\eta = 0$ and can use fewer denoising steps for faster generation.

DDIM can be interpreted as selecting a deterministic trajectory consistent with the diffusion marginals. Needs verification: the precise ODE connection depends on the continuous-time formulation and timestep schedule.

[[2022 Elucidating the Design Space of Diffusion-Based Generative Models]] argues that many diffusion formulations are equivalent or closely related after reparameterization. This separates modeling choices, such as what denoiser is learned, from parameterization and sampler choices, such as how noise levels are traversed.

## Basic sampling idea
Sampling starts from $x_T \sim \mathcal{N}(0, I)$ and repeatedly applies the learned reverse transition until reaching $x_0$.

DDIM changes this basic sampling story by allowing a shorter timestep trajectory and, when $\eta = 0$, a deterministic map from the initial $x_T$ to the final sample.

The EDM design-space view treats deterministic sampling as numerical integration of an ODE driven by a denoiser or score model.

EDM emphasizes that sampling quality depends strongly on numerical discretization choices, not only on the learned model.

Classifier-free guidance is now a standard conditioning mechanism for diffusion models: a single model is trained with condition dropout, then sampling uses a guidance scale `w` to trade off condition strength, fidelity, and diversity.

Latent diffusion keeps the iterative denoising framework but applies it to latent variables `z` produced by an encoder, then decodes the final latent sample back to pixels.

Embedding models can provide the conditioning representation used by conditional diffusion models; the diffusion model then learns how denoising should depend on that representation.

DiT adds an architectural bridge: diffusion supplies the generative objective and denoising process, while transformers supply the scalable backbone over tokenized visual representations.

## Related concepts
- [[ELBO]]
- [[Score Matching]]
- [[Denoising]]
- [[Diffusion Forward Process]]
- [[Diffusion Reverse Process]]
- [[Diffusion ELBO]]
- [[Diffusion Parameterization]]
- [[Diffusion Design Space]]
- [[Latent Diffusion]]
- [[Diffusion with Transformers]]
- [[Image Tokenization]]
- [[DDIM Sampling]]
- [[Classifier-Free Guidance]]
- [[Latent Diffusion Models]]
- [[CLIP]]
- [[Score-Based Generative Models]]
- [[Noise Conditional Score Networks]]
- [[Annealed Langevin Dynamics]]
- [[Forward SDE]]
- [[Reverse-Time SDE]]
- [[Probability Flow ODE]]

## Related papers
- [[2019 Generative Modeling by Estimating Gradients of the Data Distribution]]
- [[2015 Deep Unsupervised Learning using Nonequilibrium Thermodynamics]]
- [[2020 Denoising Diffusion Probabilistic Models]]
- [[2020 Denoising Diffusion Implicit Models]]
- [[2021 Score-Based Generative Modeling through SDEs]]
- [[2022 Elucidating the Design Space of Diffusion-Based Generative Models]]
- [[2022 Classifier-Free Diffusion Guidance]]
- [[2022 Latent Diffusion Models]]
- [[2021 CLIP]]
- [[2022 Scalable Diffusion Models with Transformers]]

## Open questions
- Needs verification: how later diffusion literature generalizes the DDPM setup.
