# Index

## Core pages

- [[Home]] - entry point to the wiki (type: index)

## Mathematical foundations

- [[Probability Theory]] - probability tools used throughout deep learning (type: math, status: stub)
- [[Bayesian Inference]] - posterior inference framing for parameters and latent variables (type: math, status: stub)
- [[Maximum Likelihood Estimation]] - likelihood-based parameter estimation (type: math, status: stub)
- [[KL Divergence]] - divergence used to express posterior approximation error and ELBO tightness (type: math, status: partially verified)
- [[ELBO]] - general variational inference objective used as a lower bound on marginal log likelihood (type: math, status: partially verified)
- [[Notation Conventions]] - central convention page for notation shared across variational inference, diffusion, attention, and MoE notes (type: math, status: developing)
- [[Variational Inference]] - approximate posterior inference as optimization over a tractable distribution family (type: math, status: partially verified)
- [[Reparameterization Trick]] - change-of-variables method for differentiating stochastic ELBO estimators in VAEs (type: math, status: partially verified)
- [[Diffusion Forward Process]] - fixed Gaussian noising Markov chain used by DDPMs (type: math, status: partially verified)
- [[Diffusion Reverse Process]] - learned Gaussian denoising Markov chain used for DDPM sampling (type: math, status: partially verified)
- [[Diffusion ELBO]] - variational bound and simplified denoising objective used in DDPM training (type: math, status: partially verified)
- [[DDIM Sampling]] - non-Markovian diffusion sampling update that can be deterministic and faster than DDPM sampling (type: math, status: partially verified)
- [[Diffusion Parameterization]] - sigma-space and denoiser parameterizations used to compare diffusion formulations (type: math, status: partially verified)
- [[Diffusion ODE Solvers]] - numerical solvers for probability-flow diffusion ODE sampling (type: math, status: partially verified)
- [[Classifier-Free Guidance]] - conditioning mechanism combining conditional and unconditional diffusion predictions (type: math, status: partially verified)
- [[Latent Diffusion]] - diffusion formulation where noising and denoising occur in a perceptually meaningful autoencoder latent space (type: math, status: partially verified)
- [[Contrastive Learning]] - representation learning objective that aligns positive pairs and separates negatives (type: math, status: partially verified)
- [[Scaled Dot-Product Attention]] - core Transformer attention operation using scaled query-key dot products and value weighting (type: math, status: partially verified)
- [[Layer Normalization (Math)]] - feature-wise normalization operation computed within one layer and one training case (type: math, status: partially verified)
- [[RMSNorm (Math)]] - root-mean-square normalization operation that removes LayerNorm mean-centering (type: math, status: partially verified)
- [[Rotary Position Embedding (Math)]] - rotary query/key positional encoding that makes attention scores depend on relative position (type: math, status: partially verified)
- [[Multi-Head Latent Attention (Math)]] - MLA equations and cache-size comparison for latent key/value compression (type: math, status: partially verified)
- [[Expert Routing]] - router probabilities, top-1 assignment, expert capacity, and load balancing for Switch-style MoE layers (type: math, status: partially verified)
- [[Score Matching]] - objectives for learning score functions, including DDPM's denoising-score-matching connection (type: math, status: developing)
- [[Langevin Dynamics]] - score-based stochastic sampling procedure (type: math, status: partially verified)
- [[Annealed Langevin Dynamics]] - multi-noise-level Langevin sampler used by NCSNs (type: math, status: partially verified)
- [[Forward SDE]] - continuous-time noising process from data to prior noise (type: math, status: partially verified)
- [[Reverse-Time SDE]] - score-dependent reverse stochastic process for generation (type: math, status: partially verified)
- [[Probability Flow ODE]] - deterministic process sharing SDE marginal distributions (type: math, status: partially verified)
- [[Regularization]] - constraints and penalties for generalization and training behavior (type: math, status: stub)

## Generative models

- [[Generative Modeling]] - synthesis stub for the broader generative-modeling track beyond diffusion (type: concept, status: stub)
- [[Variational Autoencoders]] - latent-variable generative models with probabilistic encoders and decoders trained using the ELBO (type: concept, status: developing)
- [[Amortized Variational Inference]] - concept page for shared inference models that avoid per-datapoint variational optimization (type: concept, status: developing)
- [[Diffusion Models]] - generative models that learn to reverse a gradual noising process (type: concept, status: developing)
- [[Latent Diffusion Models]] - diffusion models that generate in learned latent space for more efficient high-resolution synthesis (type: concept, status: developing)
- [[CLIP]] - vision-language joint embedding model trained with image-text contrastive learning (type: concept, status: developing)
- [[Diffusion with Transformers]] - diffusion models using transformer denoising backbones over image or latent tokens (type: concept, status: developing)
- [[Image Tokenization]] - representing images or latents as patch tokens for transformer processing (type: concept, status: stub)
- [[Diffusion Design Space]] - modular view of diffusion model design choices and equivalent parameterizations (type: concept, status: developing)
- [[Score-Based Generative Models]] - generative models that estimate score fields and sample with score-based dynamics (type: concept, status: developing)
- [[Noise Conditional Score Networks]] - score networks conditioned on Gaussian noise level (type: concept, status: developing)
- [[Denoising]] - recovering clean signal from noisy observations, central to DDPM reverse processes (type: concept, status: stub)
- [[Energy-Based Models]] - generative modeling with energy functions (type: concept, status: stub)
- [[Normalizing Flows]] - invertible-transform generative models (type: concept, status: stub)
- [[GANs]] - adversarially trained generative models (type: concept, status: stub)

## Transformers and sequence models

- [[Efficient LLM Architecture]] - synthesis hub for attention efficiency, KV-cache reduction, sparse MoE capacity, and LLM systems constraints (type: concept, status: developing)
- [[Transformer Architecture]] - synthesis hub for transformer internals, including attention, feed-forward blocks, positional encodings, normalization, residuals, and efficient variants (type: concept, status: developing)
- [[Transformers]] - attention-based neural architecture family (type: concept, status: developing)
- [[Attention]] - query/key/value mechanism for weighting information by relevance (type: concept, status: developing)
- [[Self-Attention]] - attention among elements of the same sequence or set (type: concept, status: developing)
- [[Multi-Head Attention]] - parallel attention heads over learned query/key/value projections (type: concept, status: developing)
- [[Grouped-Query Attention]] - attention variant sharing key/value heads across groups of query heads (type: concept, status: developing)
- [[Multi-Query Attention]] - attention variant with multiple query heads but shared key/value heads for faster incremental decoding (type: concept, status: developing)
- [[FlashAttention]] - IO-aware exact attention algorithm that avoids materializing the full attention matrix in slow memory (type: concept, status: developing)
- [[Multi-Head Latent Attention]] - attention-state compression idea used to reduce KV-cache cost during inference (type: concept, status: developing)
- [[KV Cache]] - cached attention keys and values reused during autoregressive decoding (type: concept, status: developing)
- [[Positional Encoding]] - position information for sequence models (type: concept, status: developing)
- [[Rotary Position Embedding]] - positional encoding method that rotates query and key vectors by position-dependent angles (type: concept, status: developing)
- [[Transformer Feed-Forward Networks]] - position-wise MLP sublayers inside transformer blocks (type: concept, status: developing)
- [[Mixture of Experts]] - sparse expert layers that route inputs through selected subnetworks to scale capacity (type: concept, status: developing)
- [[DeepSeekMoE]] - MoE feed-forward design with shared experts and fine-grained routed experts (type: concept, status: developing)
- [[LLM Training Systems]] - infrastructure, precision, and parallelism constraints for training large language models (type: concept, status: developing)
- [[LLM Inference Systems]] - synthesis stub for serving and inference constraints in large language models (type: concept, status: stub)
- [[Residual Connections]] - sublayer skip connections used in transformer blocks (type: concept, status: stub)
- [[Layer Normalization]] - normalization method computed across features within a single training case (type: concept, status: developing)
- [[RMSNorm]] - normalization method that rescales by root mean square without mean-centering (type: concept, status: developing)
- [[Large Language Models]] - large neural language models trained on broad text distributions (type: concept, status: developing)

## Optimization and training

- [[Optimization and Training Stability]] - synthesis stub for optimization and training-stability mechanisms (type: concept, status: stub)
- [[Gradient Descent]] - gradient-based iterative optimization (type: math, status: stub)
- [[Adam]] - adaptive gradient optimizer (type: math, status: stub)
- [[Weight Decay]] - parameter decay and related regularization (type: math, status: stub)
- [[Normalization]] - rescaling and standardization techniques used in neural networks (type: concept, status: developing)
- [[Scaling Laws]] - relationships between performance and scale (type: concept, status: stub)

## Research history

- [[Deep Learning Timeline]] - timeline for major deep learning developments (type: concept, status: developing)
- [[Generative Modeling Timeline]] - timeline for generative modeling developments (type: concept, status: developing)

## Source collections

- [[2013 Auto-Encoding Variational Bayes]] - Kingma and Welling paper introducing SGVB, AEVB, and the VAE example (type: paper, status: studied)
- [[2015 Deep Unsupervised Learning using Nonequilibrium Thermodynamics]] - Sohl-Dickstein et al. paper introducing diffusion probabilistic models as learned reversals of gradual noising processes (type: paper, status: studied)
- [[2016 Layer Normalization]] - Ba, Kiros, and Hinton paper introducing layer normalization for neural networks and recurrent sequence models (type: paper, status: studied)
- [[2017 Attention Is All You Need]] - Vaswani et al. paper introducing the Transformer architecture based on self-attention and multi-head attention (type: paper, status: studied)
- [[2019 Introduction to Variational Autoencoders]] - Kingma and Welling tutorial covering VAE foundations, latent-variable models, inference, and ELBO interpretation (type: paper, status: studied)
- [[2019 Root Mean Square Layer Normalization]] - Zhang and Sennrich paper introducing RMSNorm as a simpler alternative to LayerNorm (type: paper, status: studied)
- [[2019 Fast Transformer Decoding One Write-Head is All You Need]] - Shazeer paper introducing multi-query attention to reduce key/value memory bandwidth during incremental Transformer decoding (type: paper, status: studied)
- [[2019 Generative Modeling by Estimating Gradients of the Data Distribution]] - Song and Ermon paper introducing NCSNs and annealed Langevin sampling (type: paper, status: studied)
- [[2020 Denoising Diffusion Probabilistic Models]] - Ho, Jain, and Abbeel paper introducing DDPM training and sampling foundations (type: paper, status: studied)
- [[2020 Denoising Diffusion Implicit Models]] - Song, Meng, and Ermon paper introducing DDIM sampling with the DDPM training objective (type: paper, status: studied)
- [[2021 CLIP]] - Radford et al. paper introducing contrastive image-text pretraining for transferable visual representations (type: paper, status: studied)
- [[2021 RoFormer]] - Su et al. paper introducing rotary position embedding for Transformer self-attention (type: paper, status: studied)
- [[2021 Score-Based Generative Modeling through SDEs]] - Song et al. paper unifying score-based and diffusion models through SDEs (type: paper, status: studied)
- [[2021 Switch Transformers]] - Fedus, Zoph, and Shazeer paper introducing simplified sparse expert routing in transformer language models (type: paper, status: studied)
- [[2022 Elucidating the Design Space of Diffusion-Based Generative Models]] - Karras et al. paper organizing diffusion methods into a modular design space (type: paper, status: studied)
- [[2022 DPM-Solver]] - Lu et al. paper introducing a high-order ODE solver for fast diffusion sampling (type: paper, status: studied)
- [[2022 Classifier-Free Diffusion Guidance]] - Ho and Salimans paper introducing classifier-free guidance for conditional diffusion sampling (type: paper, status: studied)
- [[2022 FlashAttention]] - Dao et al. paper introducing IO-aware exact attention for faster and more memory-efficient Transformers (type: paper, status: studied)
- [[2022 Latent Diffusion Models]] - Rombach et al. paper introducing diffusion in autoencoder latent space for efficient high-resolution synthesis (type: paper, status: studied)
- [[2022 Scalable Diffusion Models with Transformers]] - Peebles and Xie paper introducing transformer denoising backbones for latent diffusion (type: paper, status: studied)
- [[2023 GQA]] - Ainslie et al. paper introducing grouped-query attention and uptraining from multi-head checkpoints (type: paper, status: studied)
- [[2024 DeepSeekMoE]] - Dai et al. paper introducing fine-grained expert segmentation and shared expert isolation for MoE specialization (type: paper, status: studied)
- [[2024 DeepSeek-V2 Technical Report]] - DeepSeek-AI report introducing MLA and DeepSeekMoE in an efficient sparse MoE language model (type: paper, status: studied)
- [[2024 DeepSeek-V3 Technical Report]] - DeepSeek-AI report mapping sparse MoE, MLA, multi-token prediction, and systems co-design in a modern LLM (type: paper, status: studied)
- [[Important Papers]] - catalog of anchor papers for the wiki (type: index, status: developing)
- [[Important Videos]] - catalog of anchor lectures, talks, and videos (type: index, status: stub)
- [[Open Questions]] - unresolved questions guiding future ingestion (type: concept, status: stub)

## Notes

This file is maintained by the LLM.
