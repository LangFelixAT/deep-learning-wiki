# Deep Learning Timeline

## Metadata
- Type: concept
- Status: developing

## Short definition
Timeline of important deep learning developments covered by the wiki.

## Scope
This page tracks source-grounded milestones already represented in the wiki. It is not a complete history of deep learning.

## Timeline
- 2013: [[2013 Auto-Encoding Variational Bayes]] introduces the VAE example and reparameterized stochastic variational training.
- 2015: [[2015 Deep Unsupervised Learning using Nonequilibrium Thermodynamics]] introduces diffusion probabilistic models as learned reversals of gradual noising processes.
- 2016: [[2016 Layer Normalization]] introduces layer normalization as a normalization method suited to recurrent and sequence models.
- 2017: [[2017 Attention Is All You Need]] introduces the Transformer architecture based on self-attention and multi-head attention.
- 2019: [[2019 Introduction to Variational Autoencoders]] consolidates VAE foundations, latent-variable modeling, variational approximation, and ELBO interpretation.
- 2019: [[2019 Generative Modeling by Estimating Gradients of the Data Distribution]] develops score-based generative modeling with noise-conditional score networks and annealed Langevin dynamics.
- 2019: [[2019 Fast Transformer Decoding One Write-Head is All You Need]] introduces multi-query attention for faster incremental Transformer decoding.
- 2020: [[2020 Denoising Diffusion Probabilistic Models]] develops DDPM training and sampling foundations.
- 2020: [[2020 Denoising Diffusion Implicit Models]] introduces DDIM sampling as a faster sampler using the DDPM training objective.
- 2021: [[2021 CLIP]] introduces contrastive image-text pretraining for transferable visual representations and conditioning signals.
- 2021: [[2021 RoFormer]] introduces rotary position embedding for injecting relative position information into self-attention.
- 2021: [[2021 Score-Based Generative Modeling through SDEs]] unifies score-based and diffusion models through SDEs and probability-flow ODEs.
- 2022: [[2022 Classifier-Free Diffusion Guidance]] introduces classifier-free guidance for conditional diffusion sampling.
- 2022: [[2022 Latent Diffusion Models]] moves diffusion into learned latent space for efficient high-resolution synthesis.
- 2022: [[2022 Elucidating the Design Space of Diffusion-Based Generative Models]] organizes diffusion methods into a modular design space.
- 2022: [[2022 DPM-Solver]] frames fast diffusion sampling as high-order ODE solving.
- 2022: [[2022 Scalable Diffusion Models with Transformers]] connects transformer backbones to diffusion models through DiT.
- 2023: [[2023 GQA]] introduces grouped-query attention as a middle point between multi-head and multi-query attention.

## Track links
- Generative modeling: [[Generative Modeling Timeline]], [[Diffusion Models]], [[Diffusion Design Space]]
- Transformer architecture: [[Transformers]], [[Attention]], [[Rotary Position Embedding]]
- Efficient inference systems: [[KV Cache]], [[Multi-Query Attention]], [[Grouped-Query Attention]]
- Representation learning: [[CLIP]], [[Contrastive Learning]]
- Optimization and training: [[Normalization]], [[Layer Normalization]]

## Open questions
- Needs verification: add core CNN, ResNet, GAN, normalizing-flow, optimizer, decoder-only LLM, MoE, and efficient-attention milestones as their anchor sources are ingested.
