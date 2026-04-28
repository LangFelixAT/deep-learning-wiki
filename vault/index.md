# Index

## Core pages

- [[Home]] - entry point to the wiki (type: index)

## Mathematical foundations

- [[Probability Theory]] - probability tools used throughout deep learning (type: math, status: stub)
- [[Bayesian Inference]] - posterior inference framing for parameters and latent variables (type: math, status: stub)
- [[Maximum Likelihood Estimation]] - likelihood-based parameter estimation (type: math, status: stub)
- [[KL Divergence]] - divergence used to express posterior approximation error and ELBO tightness (type: math, status: partially verified)
- [[ELBO]] - general variational inference objective used as a lower bound on marginal log likelihood (type: math, status: partially verified)
- [[Variational Inference]] - approximate posterior inference as optimization over a tractable distribution family (type: math, status: partially verified)
- [[Reparameterization Trick]] - change-of-variables method for differentiating stochastic ELBO estimators in VAEs (type: math, status: partially verified)
- [[Diffusion Forward Process]] - fixed Gaussian noising Markov chain used by DDPMs (type: math, status: partially verified)
- [[Diffusion Reverse Process]] - learned Gaussian denoising Markov chain used for DDPM sampling (type: math, status: partially verified)
- [[Diffusion ELBO]] - variational bound and simplified denoising objective used in DDPM training (type: math, status: partially verified)
- [[Score Matching]] - objectives for learning score functions, including DDPM's denoising-score-matching connection (type: math, status: developing)
- [[Langevin Dynamics]] - score-based stochastic sampling procedure (type: math, status: partially verified)
- [[Annealed Langevin Dynamics]] - multi-noise-level Langevin sampler used by NCSNs (type: math, status: partially verified)
- [[Forward SDE]] - continuous-time noising process from data to prior noise (type: math, status: partially verified)
- [[Reverse-Time SDE]] - score-dependent reverse stochastic process for generation (type: math, status: partially verified)
- [[Probability Flow ODE]] - deterministic process sharing SDE marginal distributions (type: math, status: partially verified)
- [[Regularization]] - constraints and penalties for generalization and training behavior (type: math, status: stub)

## Generative models

- [[Variational Autoencoders]] - latent-variable generative models with probabilistic encoders and decoders trained using the ELBO (type: concept, status: developing)
- [[Amortized Variational Inference]] - concept page for shared inference models that avoid per-datapoint variational optimization (type: concept, status: developing)
- [[Diffusion Models]] - generative models that learn to reverse a gradual noising process (type: concept, status: developing)
- [[Score-Based Generative Models]] - generative models that estimate score fields and sample with score-based dynamics (type: concept, status: developing)
- [[Noise Conditional Score Networks]] - score networks conditioned on Gaussian noise level (type: concept, status: developing)
- [[Denoising]] - recovering clean signal from noisy observations, central to DDPM reverse processes (type: concept, status: stub)
- [[Energy-Based Models]] - generative modeling with energy functions (type: concept, status: stub)
- [[Normalizing Flows]] - invertible-transform generative models (type: concept, status: stub)
- [[GANs]] - adversarially trained generative models (type: concept, status: stub)

## Transformers and sequence models

- [[Transformers]] - attention-based neural architecture family (type: concept, status: stub)
- [[Attention]] - relevance-weighted information aggregation (type: concept, status: stub)
- [[Self-Attention]] - attention among elements of the same sequence or set (type: concept, status: stub)
- [[Positional Encoding]] - position information for sequence models (type: concept, status: stub)
- [[Large Language Models]] - large neural language models trained on broad text distributions (type: concept, status: stub)

## Optimization and training

- [[Gradient Descent]] - gradient-based iterative optimization (type: math, status: stub)
- [[Adam]] - adaptive gradient optimizer (type: math, status: stub)
- [[Weight Decay]] - parameter decay and related regularization (type: math, status: stub)
- [[Normalization]] - rescaling and standardization techniques used in neural networks (type: concept, status: stub)
- [[Scaling Laws]] - relationships between performance and scale (type: concept, status: stub)

## Research history

- [[Deep Learning Timeline]] - timeline for major deep learning developments (type: concept, status: stub)
- [[Generative Modeling Timeline]] - timeline for generative modeling developments (type: concept, status: stub)

## Source collections

- [[2013 Auto-Encoding Variational Bayes]] - Kingma and Welling paper introducing SGVB, AEVB, and the VAE example (type: paper, status: studied)
- [[2019 Introduction to Variational Autoencoders]] - Kingma and Welling tutorial covering VAE foundations, latent-variable models, inference, and ELBO interpretation (type: paper, status: studied)
- [[2019 Generative Modeling by Estimating Gradients of the Data Distribution]] - Song and Ermon paper introducing NCSNs and annealed Langevin sampling (type: paper, status: studied)
- [[2020 Denoising Diffusion Probabilistic Models]] - Ho, Jain, and Abbeel paper introducing DDPM training and sampling foundations (type: paper, status: studied)
- [[2021 Score-Based Generative Modeling through SDEs]] - Song et al. paper unifying score-based and diffusion models through SDEs (type: paper, status: studied)
- [[Important Papers]] - catalog of anchor papers for the wiki (type: index, status: stub)
- [[Important Videos]] - catalog of anchor lectures, talks, and videos (type: index, status: stub)
- [[Open Questions]] - unresolved questions guiding future ingestion (type: concept, status: stub)

## Notes

This file is maintained by the LLM.
