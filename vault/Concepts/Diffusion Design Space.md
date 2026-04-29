# Diffusion Design Space

## Metadata
- Type: concept
- Status: developing

## Short definition
The diffusion design space is the set of separable choices involved in building a diffusion model, including parameterization, denoiser preconditioning, sampler, noise schedule, and training objective.

## Intuition
EDM argues that diffusion methods are often presented as monolithic systems, even though many parts can be changed independently. A model family may look different because it uses different coordinates, not because it is solving a fundamentally different problem.

Many diffusion formulations differ only by reparameterization of variables, not by fundamentally different objectives.

## Mathematical formulation
- Related math: [[Diffusion Parameterization]], [[Probability Flow ODE]], [[Score Matching]], [[Notation Conventions]].
- Model choice: what denoiser or score network is trained.
- Backbone choice: whether the denoiser is implemented with a U-Net, transformer, or another architecture.
- Parameterization choice: whether the network predicts clean data, noise, score, or a preconditioned output.
- Sampler choice: how the denoiser is used to move from high noise to low noise.
- Solver choice: which numerical method integrates the ODE or reverse process.
- Schedule choice: how noise levels such as `sigma` are traversed.

## Historical development
[[2020 Denoising Diffusion Probabilistic Models]] and [[2020 Denoising Diffusion Implicit Models]] introduced influential discrete-time training and sampling views.

[[2021 Score-Based Generative Modeling through SDEs]] unified score-based and diffusion models using SDEs and probability-flow ODEs.

[[2022 Elucidating the Design Space of Diffusion-Based Generative Models]] reorganizes these ideas into a practical design-space view, emphasizing modular choices and reparameterizations.

[[2022 DPM-Solver]] sharpens the sampler axis by treating the choice of ODE solver as an independent design choice that can improve sampling without retraining the denoiser.

[[2022 Scalable Diffusion Models with Transformers]] sharpens the backbone axis by showing that a transformer can replace the common U-Net denoising backbone in latent diffusion.

## Related papers
- [[2020 Denoising Diffusion Probabilistic Models]]
- [[2020 Denoising Diffusion Implicit Models]]
- [[2021 Score-Based Generative Modeling through SDEs]]
- [[2022 Elucidating the Design Space of Diffusion-Based Generative Models]]
- [[2022 DPM-Solver]]
- [[2022 Scalable Diffusion Models with Transformers]]

## Related concepts
- [[Diffusion Models]]
- [[Diffusion Parameterization]]
- [[Diffusion ODE Solvers]]
- [[Probability Flow ODE]]
- [[Score Matching]]
- [[DDIM Sampling]]
- [[Diffusion with Transformers]]
- [[Notation Conventions]]

## Open questions
- Needs verification: exact equivalences among VP, VE, iDDPM, DDIM, and EDM require careful notation mapping.
- Needs verification: which design choices are truly independent in large-scale modern systems may depend on architecture, conditioning, and training setup.
