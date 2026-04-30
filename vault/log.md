# Log

This is an append-only chronological record of wiki operations.

Entries include:
- ingest
- query
- lint
- refactor
- manual

Format:

## [YYYY-MM-DD] type | description

- Source:
- Pages created:
- Pages updated:
- Key concepts:
- Notes:

## [2026-04-28] manual | Vault backbone foundation pass

- Source: AGENTS.md; docs/ingestion_workflow.md; Karpathy LLM Wiki gist
- Pages created: [[Probability Theory]], [[Bayesian Inference]], [[Maximum Likelihood Estimation]], [[Variational Inference]], [[Score Matching]], [[Regularization]], [[Energy-Based Models]], [[Normalizing Flows]], [[GANs]], [[Transformers]], [[Attention]], [[Self-Attention]], [[Positional Encoding]], [[Large Language Models]], [[Gradient Descent]], [[Adam]], [[Weight Decay]], [[Normalization]], [[Scaling Laws]]
- Pages updated: [[Home]], [[index]], [[log]], [[ELBO]], [[KL Divergence]], [[Diffusion Models]], [[Variational Autoencoders]], [[Important Papers]], [[Important Videos]], [[Open Questions]], [[Concept]], [[Math]], [[Paper]], [[Video]]
- Key concepts: wiki backbone, templates, concept stubs, math stubs
- Notes: Added short structured stubs only; no arXiv scanning or automation added.

## [2026-04-28] manual | Normalize note filenames

- Source: user request
- Pages created:
- Pages updated: [[Home]], [[index]], [[log]], [[ELBO]], [[KL Divergence]], [[Score Matching]], [[Variational Inference]], [[Diffusion Models]], [[Variational Autoencoders]], [[GANs]], [[Energy-Based Models]], [[Normalizing Flows]]
- Key concepts: Obsidian links, note filenames
- Notes: Renamed underscore-based note filenames to space-based filenames and updated references.

## [2026-04-28] ingest | Auto-Encoding Variational Bayes

- Source: data/raw/papers/vae_kingma_welling_2013.pdf
- Pages created:
- Pages updated: [[2013 Auto-Encoding Variational Bayes]], [[ELBO]], [[KL Divergence]], [[Variational Autoencoders]], [[index]], [[log]]
- Key concepts: [[ELBO]], [[KL Divergence]], [[Variational Inference]], [[Variational Autoencoders]]
- Notes: First paper ingestion. Added source-faithful summary, problem framing, method, key equations, source claims, and short math/concept updates. Unverified regularity details are marked as needing verification.

## [2026-04-28] ingest | An Introduction to Variational Autoencoders

- Source: data/raw/papers/vae_intro_kingma_welling_2019.pdf
- Pages created: [[Amortized Variational Inference]]
- Pages updated: [[2019 Introduction to Variational Autoencoders]], [[ELBO]], [[KL Divergence]], [[Variational Inference]], [[Variational Autoencoders]], [[index]], [[log]]
- Key concepts: [[ELBO]], [[KL Divergence]], [[Variational Inference]], [[Amortized Variational Inference]], [[Variational Autoencoders]]
- Notes: Ingested only foundational sections on latent-variable models, probabilistic setup, inference, variational approximation, and ELBO/KL interpretation. Advanced sections and model extensions were not ingested.

## [2026-04-28] manual | Normalize variational inference links

- Source: user request
- Pages created:
- Pages updated: [[Home]], [[index]], [[log]], [[2013 Auto-Encoding Variational Bayes]], [[2019 Introduction to Variational Autoencoders]], [[Bayesian Inference]], [[ELBO]], [[KL Divergence]], [[Variational Inference]], [[Variational Autoencoders]], [[Amortized Variational Inference]]
- Key concepts: [[Variational Inference]], [[Amortized Variational Inference]]
- Notes: Removed active path-qualified variational inference links by keeping [[Variational Inference]] as the canonical math note and renaming the VAE-specific concept note to [[Amortized Variational Inference]].

## [2026-04-28] manual | Clarify variational inference identity

- Source: user review
- Pages created:
- Pages updated: [[Variational Inference]], [[ELBO]], [[index]], [[log]]
- Key concepts: [[Variational Inference]], [[ELBO]], [[KL Divergence]]
- Notes: Added the central ELBO/KL identity and made the optimization-over-distributions perspective explicit.

## [2026-04-28] manual | Update repository instructions

- Source: user request
- Pages created:
- Pages updated: AGENTS.md, [[log]]
- Key concepts: Obsidian links, note naming, scoped ingestion
- Notes: Added small rules for unique note titles, simple wikilinks, disambiguated concept/math naming, and respecting user-limited ingest scope.

## [2026-04-28] ingest | Reparameterization Trick

- Source: data/raw/papers/vae_intro_kingma_welling_2019.pdf
- Pages created: [[Reparameterization Trick]]
- Pages updated: [[ELBO]], [[Variational Autoencoders]], [[Variational Inference]], [[index]], [[log]]
- Key concepts: [[Reparameterization Trick]], [[ELBO]], [[Variational Autoencoders]], [[Variational Inference]]
- Notes: Ingested only the focused 2019 tutorial material on stochastic ELBO gradients, differentiating expectations over `q_phi(z|x)`, `z = g_phi(epsilon, x)`, the Gaussian example, and backpropagation. Advanced variants, unrelated training tricks, and implementation details were not ingested.

## [2026-04-28] manual | Refine reparameterization trick note

- Source: user review
- Pages created:
- Pages updated: [[Reparameterization Trick]], [[log]]
- Key concepts: [[Reparameterization Trick]], [[ELBO]]
- Notes: Added the central expectation-rewrite identity, clarified gradient wording, added the distribution-family caveat, and marked the score-function estimator contrast as needing verification.

## [2026-04-28] ingest | Denoising Diffusion Probabilistic Models

- Source: data/raw/papers/ddpm_ho_jain_abbeel_2020.pdf
- Pages created: [[Diffusion Forward Process]], [[Diffusion Reverse Process]], [[Diffusion ELBO]], [[Denoising]]
- Pages updated: [[2020 Denoising Diffusion Probabilistic Models]], [[Diffusion Models]], [[Score Matching]], [[ELBO]], [[Variational Inference]], [[index]], [[log]]
- Key concepts: [[Diffusion Models]], [[Diffusion Forward Process]], [[Diffusion Reverse Process]], [[Diffusion ELBO]], [[Denoising]], [[Score Matching]]
- Notes: First diffusion-model ingest. Covered only forward noising, reverse denoising, variational/ELBO objective, denoising score-matching connection, and basic sampling. Did not ingest detailed implementation settings, detailed experimental tables, or later diffusion extensions.

## [2026-04-28] manual | Clarify diffusion ELBO equation

- Source: user review
- Pages created:
- Pages updated: [[Diffusion ELBO]], [[2020 Denoising Diffusion Probabilistic Models]], [[log]]
- Key concepts: [[Diffusion ELBO]]
- Notes: Rewrote the DDPM variational-bound expression to avoid ambiguous log/ratio formatting.

## [2026-04-28] ingest | Generative Modeling by Estimating Gradients of the Data Distribution

- Source: data/raw/papers/score_matching_song_ermon_2019.pdf
- Pages created: [[Langevin Dynamics]], [[Annealed Langevin Dynamics]], [[Score-Based Generative Models]], [[Noise Conditional Score Networks]]
- Pages updated: [[2019 Generative Modeling by Estimating Gradients of the Data Distribution]], [[Score Matching]], [[Diffusion Models]], [[Energy-Based Models]], [[index]], [[log]]
- Key concepts: [[Score Matching]], [[Score-Based Generative Models]], [[Noise Conditional Score Networks]], [[Langevin Dynamics]], [[Annealed Langevin Dynamics]]
- Notes: Ingested only foundational score-based modeling material: score definition, score matching, manifold and low-density issues, Gaussian perturbations, NCSNs, annealed Langevin dynamics, and high-level DDPM relation. Did not ingest detailed experimental tables, implementation settings, or later extensions.

## [2026-04-28] manual | Refine score-based foundations

- Source: user review
- Pages created:
- Pages updated: [[Score Matching]], [[Langevin Dynamics]], [[Diffusion Models]], [[Energy-Based Models]], [[log]]
- Key concepts: [[Score Matching]], [[Langevin Dynamics]], [[Diffusion Models]], [[Energy-Based Models]]
- Notes: Clarified practical score matching objective, score normalization invariance, Langevin target distribution, DDPM noise prediction as score estimation, and the EBM score-energy relationship.

## [2026-04-28] lint | Wiki consistency pass

- Source: AGENTS.md; docs/ingestion_workflow.md; current vault
- Pages created:
- Pages updated: [[Concept]], [[Math]], [[log]]
- Key concepts: Obsidian links, note naming, status vocabulary, index coverage
- Notes: Checked for broken simple wikilinks, folder-qualified links, duplicate note basenames, index coverage, and status consistency. No renames needed. Updated template status vocabularies to include `partially verified`.

## [2026-04-28] ingest | Score-Based Generative Modeling through Stochastic Differential Equations

- Source: data/raw/papers/sde_song_2021.pdf
- Pages created: [[Forward SDE]], [[Reverse-Time SDE]], [[Probability Flow ODE]]
- Pages updated: [[2021 Score-Based Generative Modeling through SDEs]], [[Score Matching]], [[Diffusion Models]], [[Langevin Dynamics]], [[index]], [[log]]
- Key concepts: [[Forward SDE]], [[Reverse-Time SDE]], [[Probability Flow ODE]], [[Score Matching]], [[Diffusion Models]]
- Notes: Ingested only foundational SDE concepts: forward SDE, reverse-time SDE, time-dependent scores, probability flow ODE, predictor-corrector sampling, and conceptual relations to DDPM and score matching. Did not ingest inverse problems, application sections, architecture details, experimental results, or detailed likelihood machinery.

## [2026-04-28] manual | Refine SDE foundation notes

- Source: user review
- Pages created:
- Pages updated: [[Forward SDE]], [[Reverse-Time SDE]], [[Probability Flow ODE]], [[Score Matching]], [[log]]
- Key concepts: [[Forward SDE]], [[Reverse-Time SDE]], [[Probability Flow ODE]], [[Score Matching]]
- Notes: Clarified reverse-time simulation direction, dependence on forward marginals, probability-flow marginal equivalence, and time-dependent score notation. Deferred SDE note renames because current titles are unique and clear.

## [2026-04-28] ingest | Denoising Diffusion Implicit Models

- Source: data/raw/papers/ddim_song_meng_ermon_2020.pdf.pdf
- Pages created: [[DDIM Sampling]]
- Pages updated: [[2020 Denoising Diffusion Implicit Models]], [[Diffusion Models]], [[Diffusion Reverse Process]], [[index]], [[log]]
- Key concepts: [[DDIM Sampling]], [[Diffusion Models]], [[Diffusion Reverse Process]]
- Notes: Ingested only foundational DDIM material: relation to DDPM, shared noise-prediction training objective, non-Markovian generative process, deterministic sampling when `eta = 0`, faster sampling with fewer steps, and role of `epsilon_theta(x_t,t)`. Did not ingest classifier guidance, later diffusion variants, latent diffusion, detailed implementation settings, or unrelated modern sampling methods.

## [2026-04-28] manual | Refine DDIM sampling note

- Source: user review
- Pages created:
- Pages updated: [[DDIM Sampling]], [[Diffusion Models]], [[log]]
- Key concepts: [[DDIM Sampling]], [[Diffusion Models]], [[Probability Flow ODE]]
- Notes: Replaced an over-specific deterministic DDIM update with a safer prose statement, added a cautious ODE-connection note, and clarified DDIM as a deterministic trajectory through diffusion marginals.

## [2026-04-28] ingest | Elucidating the Design Space of Diffusion-Based Generative Models

- Source: data/raw/papers/edm_karras_2022.pdf.pdf
- Pages created: [[Diffusion Parameterization]], [[Diffusion Design Space]]
- Pages updated: [[2022 Elucidating the Design Space of Diffusion-Based Generative Models]], [[Diffusion Models]], [[Probability Flow ODE]], [[index]], [[log]]
- Key concepts: [[Diffusion Design Space]], [[Diffusion Parameterization]], [[Probability Flow ODE]], [[Diffusion Models]]
- Notes: Ingested only conceptual EDM structure: decomposition of design choices, sigma-space parameterization, denoiser preconditioning, ODE sampling as numerical integration, relation to probability-flow ODEs, and equivalence under reparameterization. Did not ingest architecture details, dataset results, hyperparameters, code-level implementation, or detailed training tricks.

## [2026-04-28] manual | Refine EDM design-space notes

- Source: user review
- Pages created:
- Pages updated: [[Diffusion Parameterization]], [[Diffusion Design Space]], [[Diffusion Models]], [[2022 Elucidating the Design Space of Diffusion-Based Generative Models]], [[log]]
- Key concepts: [[Diffusion Parameterization]], [[Diffusion Design Space]], [[Diffusion Models]]
- Notes: Clarified that the score-denoiser identity is conditional on Gaussian corruption, framed `sigma(t) = t` as a non-unique parameterization choice, and added EDM's reparameterization and numerical-discretization insights.

## [2026-04-28] ingest | DPM-Solver

- Source: data/raw/papers/dpm_solver_lu_2022.pdf
- Pages created: [[Diffusion ODE Solvers]]
- Pages updated: [[2022 DPM-Solver]], [[Probability Flow ODE]], [[Diffusion Design Space]], [[index]], [[log]]
- Key concepts: [[Diffusion ODE Solvers]], [[Probability Flow ODE]], [[Diffusion Design Space]]
- Notes: Ingested only conceptual and mathematical solver structure: sampling as probability-flow ODE integration, limits of simple solvers, high-order solver idea, exponential-integrator intuition, reduced step counts, and dependence on parameterization / noise schedule. Did not ingest implementation details, hyperparameters, extensive derivations, later solver variants, or benchmark tables beyond a brief source claim.

## [2026-04-28] manual | Refine DPM-Solver notes

- Source: user review
- Pages created:
- Pages updated: [[Diffusion ODE Solvers]], [[Diffusion Design Space]], [[log]]
- Key concepts: [[Diffusion ODE Solvers]], [[Diffusion Design Space]]
- Notes: Added a local caution that diffusion ODE signs and scalings are parameterization-dependent, and moved [[2022 DPM-Solver]] into related papers for the design-space page.

## [2026-04-28] ingest | Classifier-Free Diffusion Guidance

- Source: data/raw/papers/cfg_ho_salimans_2022.pdf
- Pages created: [[Classifier-Free Guidance]]
- Pages updated: [[2022 Classifier-Free Diffusion Guidance]], [[Diffusion Models]], [[Score Matching]], [[index]], [[log]]
- Key concepts: [[Classifier-Free Guidance]], [[Diffusion Models]], [[Score Matching]]
- Notes: Ingested only core classifier-free guidance ideas: conditional vs unconditional diffusion models, condition dropout during training, guidance formula, role of guidance scale `w`, and intuition for steering samples toward a condition. Did not ingest architecture details, CLIP/text encoders, implementation tricks, or large-system details.

## [2026-04-28] manual | Refine classifier-free guidance note

- Source: user review
- Pages created:
- Pages updated: [[Classifier-Free Guidance]], [[log]]
- Key concepts: [[Classifier-Free Guidance]]
- Notes: Clarified `w = 0` wording and added the implicit-classifier interpretation of the conditional-minus-unconditional score difference. Deferred a conditioning concept link until that page exists.

## [2026-04-28] ingest | High-Resolution Image Synthesis with Latent Diffusion Models

- Source: data/raw/papers/ldm_rombachetal_2022.pdf
- Pages created: [[Latent Diffusion Models]], [[Latent Diffusion]]
- Pages updated: [[2022 Latent Diffusion Models]], [[Diffusion Models]], [[index]], [[log]]
- Key concepts: [[Latent Diffusion Models]], [[Latent Diffusion]], [[Diffusion Models]], [[Classifier-Free Guidance]]
- Notes: Ingested only core conceptual ideas: latent-space diffusion, encoder/decoder roles, efficiency motivation, high-level cross-attention conditioning, and the overall generation pipeline. Did not ingest UNet architecture details, attention block internals, training tricks, dataset specifics, or implementation details.

## [2026-04-29] ingest | Learning Transferable Visual Models From Natural Language Supervision

- Source: data/raw/papers/clip_radford_2021.pdf
- Pages created: [[CLIP]], [[Contrastive Learning]]
- Pages updated: [[2021 CLIP]], [[Latent Diffusion Models]], [[Diffusion Models]], [[index]], [[log]]
- Key concepts: [[CLIP]], [[Contrastive Learning]], [[Latent Diffusion Models]], [[Diffusion Models]]
- Notes: Ingested only core CLIP ideas: joint image-text embedding space, contrastive matching of correct pairs against incorrect pairs, cosine/dot-product alignment, semantic embeddings, and why embeddings can be used as conditioning inputs in generative models. Did not ingest architecture details, implementation tricks, dataset scale details, or training infrastructure.

## [2026-04-29] manual | Refine CLIP conditioning note

- Source: user review
- Pages created:
- Pages updated: [[CLIP]], [[log]]
- Key concepts: [[CLIP]], conditioning
- Notes: Clarified that CLIP-like embeddings enter diffusion models as additional inputs to the denoising network while keeping the description architecture-level only.

## [2026-04-29] ingest | Scalable Diffusion Models with Transformers

- Source: data/raw/papers/dit_peebles_xie_2022.pdf
- Pages created: [[2022 Scalable Diffusion Models with Transformers]], [[Diffusion with Transformers]], [[Image Tokenization]]
- Pages updated: [[Diffusion Models]], [[Latent Diffusion Models]], [[Diffusion Design Space]], [[Transformers]], [[index]], [[log]]
- Key concepts: [[Diffusion with Transformers]], [[Image Tokenization]], [[Latent Diffusion Models]], [[Transformers]]
- Notes: Ingested only DiT as an architectural bridge: replacing U-Net backbones with transformers, latent patch tokens, high-level conditioning, relation to latent diffusion, and scaling behavior with depth/width, token count, and Gflops. Did not ingest benchmark tables, dataset details, implementation details, training hyperparameters, detailed transformer internals, attention explanations, or later DiT variants.

## [2026-04-29] manual | Refine DiT notes

- Source: user review
- Pages created:
- Pages updated: [[Diffusion with Transformers]], [[Image Tokenization]], [[2022 Scalable Diffusion Models with Transformers]], [[log]]
- Key concepts: [[Diffusion with Transformers]], [[Image Tokenization]]
- Notes: Clarified backbone choice as a design-space axis, added a caveat that tokenization changes representation rather than the diffusion process itself, and scoped the U-Net inductive-bias claim to the studied setting.

## [2026-04-29] manual | Review latent diffusion ingest caveats

- Source: user review; data/raw/papers/ldm_rombachetal_2022.pdf
- Pages created:
- Pages updated: [[Latent Diffusion]], [[index]], [[log]]
- Key concepts: [[Latent Diffusion]], [[Latent Diffusion Models]]
- Notes: Added an explicit assumption that latent compression must be perceptually meaningful. Checked the autoencoder reuse statement against the source and left it unchanged because the paper directly states that the autoencoding stage can be trained once and reused for multiple diffusion trainings or different tasks. Deferred creating a broader modern diffusion systems page until there is a concrete refactor scope.

## [2026-04-29] lint | Wiki structure and notation consistency

- Source: manual lint pass
- Pages created:
- Pages updated: Math template, [[CLIP]], [[Diffusion with Transformers]], [[Latent Diffusion Models]], [[Image Tokenization]], [[Transformers]], [[Langevin Dynamics]], [[Diffusion Models]], [[index]], [[log]]
- Key concepts: structure consistency, notation consistency, Obsidian linking
- Notes: Normalized the math template status vocabulary, added missing lightweight concept sections, linked image tokenization to the DiT paper, clarified `z_t` versus Gaussian-noise notation, added diffusion notation conventions, and updated the Transformers status to developing.

## [2026-04-29] manual | Expand project schema and roadmap

- Source: user project direction and Karpathy LLM Wiki pattern
- Pages created:
- Pages updated: AGENTS.md, docs/ingestion_workflow.md, docs/research_roadmap.md, [[log]]
- Key concepts: project schema, ingestion workflow, research roadmap
- Notes: Added the broader research trajectory beyond diffusion, added synthesis checkpoint behavior to the ingestion workflow, and created a living roadmap for generative modeling, transformer architecture, efficient attention, optimization, mixture of experts, and mathematical foundations. The roadmap emphasizes source-grounded growth rather than filling math pages with unsupported explanations.

## [2026-04-29] manual | Add reusable paper ingestion prompt

- Source: user workflow refinement
- Pages created: prompts/ingest_paper.md
- Pages updated: docs/ingestion_workflow.md, [[log]]
- Key concepts: paper ingestion, scope control, synthesis checkpoint
- Notes: Added a reusable prompt so future paper ingests can be requested with only the PDF path, source identity, and paper-specific scope while preserving the existing source-grounded workflow.

## [2026-04-29] ingest | Deep Unsupervised Learning using Nonequilibrium Thermodynamics

- Source: data/raw/papers/nonequilibrium_thermodynamics_sohl_dickstein_2015.pdf.pdf
- Pages created: [[2015 Deep Unsupervised Learning using Nonequilibrium Thermodynamics]]
- Pages updated: [[Diffusion Models]], [[Diffusion Forward Process]], [[Diffusion Reverse Process]], [[Diffusion ELBO]], [[Generative Modeling Timeline]], [[index]], [[log]]
- Key concepts: [[Diffusion Models]], [[Diffusion Forward Process]], [[Diffusion Reverse Process]], [[Diffusion ELBO]]
- Notes: Ingested only foundational diffusion-model ideas: forward noising as gradual destruction of data structure, learned reverse generative Markov chains, small-step tractability, high-level variational lower bound, probability-evaluation motivation, nonequilibrium-thermodynamics intuition, and historical relationship to DDPM. Excluded detailed thermodynamic derivations, implementation details, benchmark details beyond short source claims, modern diffusion extensions, and SDE/score reinterpretations beyond brief later connections.

## [2026-04-29] manual | Refine nonequilibrium diffusion ingest

- Source: cross-check against [[2015 Deep Unsupervised Learning using Nonequilibrium Thermodynamics]]
- Pages created:
- Pages updated: [[2015 Deep Unsupervised Learning using Nonequilibrium Thermodynamics]], [[Diffusion ELBO]], [[Diffusion Forward Process]], [[Diffusion Models]], [[log]]
- Key concepts: [[Diffusion ELBO]], [[Diffusion Forward Process]], [[Diffusion Models]]
- Notes: Clarified the sign convention difference between the 2015 lower bound on log likelihood and DDPM's upper bound on negative log likelihood, noted entropy terms in the 2015 bound, distinguished the 2015 diffusion-schedule treatment from fixed DDPM schedules, and reordered the diffusion historical development section chronologically.

## [2026-04-29] ingest | Attention Is All You Need

- Source: data/raw/papers/attention_is_all_you_need_vaswani_2017.pdf
- Pages created: [[2017 Attention Is All You Need]], [[Scaled Dot-Product Attention]], [[Multi-Head Attention]], [[Transformer Feed-Forward Networks]], [[Residual Connections]], [[Layer Normalization]]
- Pages updated: [[Transformers]], [[Attention]], [[Self-Attention]], [[Positional Encoding]], [[Deep Learning Timeline]], [[Home]], docs/research_roadmap.md, [[index]], [[log]]
- Key concepts: [[Transformers]], [[Self-Attention]], [[Scaled Dot-Product Attention]], [[Multi-Head Attention]], [[Positional Encoding]]
- Notes: Ingested only foundational transformer architecture ideas: self-attention, scaled dot-product attention, query/key/value projections, multi-head attention, positional encodings, encoder-decoder structure, feed-forward blocks, residual connections, layer normalization, and parallelism compared with recurrence. Excluded detailed benchmark tables, machine-translation dataset details, optimizer/training hyperparameters beyond brief context, label smoothing, byte-pair encoding, implementation details, later transformer variants, and modern attention optimizations beyond brief future connections.

## [2026-04-29] ingest | Layer Normalization

- Source: data/raw/papers/layer_normalization_ba_2016.pdf
- Pages created: [[2016 Layer Normalization]], [[Layer Normalization (Math)]]
- Pages updated: [[Layer Normalization]], [[Normalization]], [[Transformers]], [[Deep Learning Timeline]], [[Home]], docs/research_roadmap.md, [[index]], [[log]]
- Key concepts: [[Layer Normalization]], [[Layer Normalization (Math)]], [[Normalization]], [[Transformers]]
- Notes: Ingested only foundational normalization ideas: motivation for normalization, high-level contrast with batch normalization, per-training-case feature statistics, mean/variance over summed inputs, learned gain and bias, suitability for recurrent/sequence models, and relationship to Transformer sublayer normalization. Excluded detailed RNN experiment results, benchmark tables, implementation tricks, pre-norm versus post-norm, RMSNorm and later normalization methods except as future connections, and optimizer-specific discussion.

## [2026-04-29] ingest | RoFormer

- Source: data/raw/papers/roformer_rotary_position_embedding_su_2021.pdf
- Pages created: [[2021 RoFormer]], [[Rotary Position Embedding]], [[Rotary Position Embedding (Math)]]
- Pages updated: [[Positional Encoding]], [[Transformers]], [[Scaled Dot-Product Attention]], [[Deep Learning Timeline]], [[Home]], docs/research_roadmap.md, [[index]], [[log]]
- Key concepts: [[Rotary Position Embedding]], [[Rotary Position Embedding (Math)]], [[Positional Encoding]], [[Scaled Dot-Product Attention]]
- Notes: Ingested only foundational RoPE ideas: limits of absolute positional encoding, rotary query/key rotations, relative position through dot-product attention, high-level extrapolation and long-range dependency claims, connection to Transformer positional encodings, and importance for later LLM architecture. Excluded detailed benchmark tables, full RoFormer architecture details, implementation tricks, downstream task specifics, later RoPE variants, and modern long-context methods beyond future connections.

## [2026-04-29] manual | Refine RoFormer ingest

- Source: cross-check against [[2021 RoFormer]]
- Pages created:
- Pages updated: [[2021 RoFormer]], [[Rotary Position Embedding]], [[Rotary Position Embedding (Math)]], [[log]]
- Key concepts: [[Rotary Position Embedding]], [[Rotary Position Embedding (Math)]]
- Notes: Recorded the arXiv version read, added the paper's RoPE frequency choice, and clarified that absolute positions determine rotations while attention scores expose relative position.

## [2026-04-29] lint | Wiki consistency pass

- Source: AGENTS.md; docs/ingestion_workflow.md; current vault
- Pages created:
- Pages updated: docs/ingestion_workflow.md, [[Classifier-Free Guidance]], [[DDIM Sampling]], [[Diffusion ODE Solvers]], [[Diffusion Parameterization]], [[Energy-Based Models]], [[Image Tokenization]], [[index]], [[log]]
- Key concepts: Obsidian links, status vocabulary, math-note structure, notation consistency
- Notes: Confirmed no unresolved wikilinks, no folder-qualified wikilinks, and no duplicate note basenames. Added missing math-note scaffold sections, aligned the Normalization index status with the page, clarified EBM score notation, normalized the Image Tokenization concept structure, and kept catalog/timeline pages as intentional template exceptions.

## [2026-04-29] manual | Refresh home and deep learning timeline

- Source: current vault index and ingested paper notes
- Pages created:
- Pages updated: [[Deep Learning Timeline]], [[Home]], [[log]]
- Key concepts: research timeline, wiki navigation
- Notes: Updated the deep learning timeline to reflect already-ingested source notes across VAEs, diffusion, CLIP, transformers, RoPE, normalization, and DiT. Added active map and representation-learning links to Home.

## [2026-04-29] ingest | Fast Transformer Decoding: One Write-Head is All You Need

- Source: data/raw/papers/fast_transformer_decoding_one_write_head_shazeer_2019.pdf
- Pages created: [[2019 Fast Transformer Decoding One Write-Head is All You Need]], [[Multi-Query Attention]], [[KV Cache]]
- Pages updated: [[Multi-Head Attention]], [[Attention]], [[Self-Attention]], [[Transformers]], [[Large Language Models]], [[Home]], docs/research_roadmap.md, [[Deep Learning Timeline]], [[index]], [[log]]
- Key concepts: [[Multi-Query Attention]], [[KV Cache]], [[Multi-Head Attention]], [[Large Language Models]]
- Notes: Ingested only decoding-time bottlenecks, key/value memory bandwidth, multi-query attention, shared key/value heads, KV-cache effects, high-level speed/quality tradeoff, and relation to later efficient LLM inference. Excluded detailed benchmark tables, TPU/kernel details, full machine-translation setup, training hyperparameters, unrelated architecture changes, and modern GQA/MLA/FlashAttention details except as future connections.

## [2026-04-29] manual | Refine multi-query attention ingest

- Source: cross-check against [[2019 Fast Transformer Decoding One Write-Head is All You Need]]
- Pages created:
- Pages updated: [[2019 Fast Transformer Decoding One Write-Head is All You Need]], [[Multi-Query Attention]], [[log]]
- Key concepts: [[Multi-Query Attention]], [[KV Cache]]
- Notes: Added the source's memory-access ratio comparison and clarified that "one write-head" refers to one shared key/value set rather than one query head.

## [2026-04-29] lint | Cross-layer reference maintenance

- Source: current vault concepts, math notes, paper notes, and index
- Pages created:
- Pages updated: [[Scaled Dot-Product Attention]], [[Attention]], [[Important Papers]], [[index]], [[log]]
- Key concepts: [[Attention]], [[Multi-Query Attention]], [[KV Cache]], source catalogs
- Notes: Added multi-query attention and KV-cache references to the core attention math page, completed the 2019 source backlink on the Attention concept page, and populated the Important Papers catalog with already-ingested anchor papers.

## [2026-04-29] ingest | GQA: Training Generalized Multi-Query Transformer Models from Multi-Head Checkpoints

- Source: data/raw/papers/grouped_query_attention_ainslie_2023.pdf
- Pages created: [[2023 GQA]], [[Grouped-Query Attention]]
- Pages updated: [[Attention]], [[Self-Attention]], [[Scaled Dot-Product Attention]], [[Multi-Head Attention]], [[Multi-Query Attention]], [[KV Cache]], [[Transformers]], [[Large Language Models]], [[Home]], docs/research_roadmap.md, [[Deep Learning Timeline]], [[Important Papers]], [[index]], [[log]]
- Key concepts: [[Grouped-Query Attention]], [[Multi-Query Attention]], [[Multi-Head Attention]], [[KV Cache]]
- Notes: Ingested only GQA as a middle point between MHA and MQA, sharing key/value heads across query-head groups, the query-head/key-value-head relationship, high-level checkpoint uptraining, KV-cache and memory-bandwidth effects, and relevance for efficient LLM inference. Excluded detailed benchmark tables, full T5 setup, implementation details, hyperparameters, tokenizer/data details, and modern MLA/FlashAttention/paged-attention details except as future connections.

## [2026-04-29] manual | Refine GQA ingest

- Source: cross-check against [[2023 GQA]]
- Pages created:
- Pages updated: [[2023 GQA]], [[Grouped-Query Attention]], [[log]]
- Key concepts: [[Grouped-Query Attention]]
- Notes: Added the paper's `GQA-G` naming convention and clarified that the source applies GQA to decoder attention, not encoder self-attention.

## [2026-04-29] ingest | FlashAttention

- Source: data/raw/papers/flashattention_dao_2022.pdf
- Pages created: [[2022 FlashAttention]], [[FlashAttention]]
- Pages updated: [[Scaled Dot-Product Attention]], [[Attention]], [[Multi-Head Attention]], [[KV Cache]], [[Transformers]], [[Large Language Models]], [[Home]], docs/research_roadmap.md, [[Deep Learning Timeline]], [[Important Papers]], [[index]], [[log]]
- Key concepts: [[FlashAttention]], [[Scaled Dot-Product Attention]], [[Attention]], [[KV Cache]]
- Notes: Ingested only the IO-aware exact-attention core: standard attention as memory/IO limited, attention matrix materialization, tiling/blocking, online softmax at a conceptual level, exact versus approximate attention, long-sequence relevance, and relation to existing attention/KV-cache notes. Excluded CUDA kernel details, detailed backward derivation, benchmark tables, FlashAttention-2 and later variants, paged attention, MLA/GQA details beyond future connections, and hardware-specific tuning.

## [2026-04-29] manual | Refine FlashAttention ingest

- Source: cross-check against [[2022 FlashAttention]]
- Pages created:
- Pages updated: [[FlashAttention]], [[Scaled Dot-Product Attention]], [[log]]
- Key concepts: [[FlashAttention]], [[Scaled Dot-Product Attention]]
- Notes: Added the standard `S/P/O` attention formulation to the concept page and clarified that FlashAttention changes memory access for exact attention rather than changing the attention function or making exact attention linear-time.

## [2026-04-29] ingest | Switch Transformers

- Source: data/raw/papers/switch_transformers_fedus_2021.pdf
- Pages created: [[2021 Switch Transformers]], [[Mixture of Experts]], [[Expert Routing]]
- Pages updated: [[Transformers]], [[Transformer Feed-Forward Networks]], [[Large Language Models]], [[Home]], docs/research_roadmap.md, [[Deep Learning Timeline]], [[Important Papers]], [[index]], [[log]]
- Key concepts: [[Mixture of Experts]], [[Expert Routing]], [[Transformer Feed-Forward Networks]], [[Large Language Models]]
- Notes: Ingested only sparse expert routing, dense versus expert feed-forward layers, top-1 Switch routing, token-to-expert assignment, expert capacity and dropped tokens, load balancing, compute-efficient parameter scaling, relation to transformer feed-forward blocks, and relevance to modern LLM scaling/inference. Excluded detailed benchmark tables, full T5 setup, dataset details, TPU/system implementation details, training hyperparameters beyond brief context, detailed routing-loss derivations, and modern MoE variants except as future connections.

## [2026-04-29] manual | Refine Switch Transformers ingest

- Source: cross-check against [[2021 Switch Transformers]]
- Pages created:
- Pages updated: [[2021 Switch Transformers]], [[Expert Routing]], [[log]]
- Key concepts: [[Expert Routing]], [[Mixture of Experts]]
- Notes: Added the arXiv source link and made the top-1 Switch output equation explicit in both the source note and routing math note.

## [2026-04-29] ingest | DeepSeek-V3 Technical Report

- Source: data/raw/papers/deepseek_v3_technical_report_deepseek_ai_2024.pdf
- Pages created: [[2024 DeepSeek-V3 Technical Report]], [[Multi-Head Latent Attention]], [[LLM Training Systems]]
- Pages updated: [[Mixture of Experts]], [[Expert Routing]], [[KV Cache]], [[Large Language Models]], [[Transformers]], [[Home]], docs/research_roadmap.md, [[Deep Learning Timeline]], [[Important Papers]], [[index]], [[log]]
- Key concepts: [[Mixture of Experts]], [[Expert Routing]], [[Multi-Head Latent Attention]], [[KV Cache]], [[LLM Training Systems]]
- Notes: Map-building ingest only. Covered DeepSeek-V3 as sparse MoE LLM, total versus activated parameters, high-level DeepSeekMoE, high-level MLA as KV-cache compression, auxiliary-loss-free load balancing, multi-token prediction, and FP8/systems co-design as brief context. Excluded benchmark-table detail, full training data, post-training/RL, DualPipe implementation, hardware kernels, full FP8 recipe, full MLA/DeepSeekMoE derivations, long-context methods, DeepSeek-R1 reasoning content, and later DeepSeek versions.

## [2026-04-29] manual | Refine DeepSeek-V3 map ingest

- Source: cross-check against [[2024 DeepSeek-V3 Technical Report]]
- Pages created:
- Pages updated: [[Multi-Head Latent Attention]], [[log]]
- Key concepts: [[Multi-Head Latent Attention]], [[KV Cache]]
- Notes: Softened the MLA interpretation so it does not imply full equivalence to standard multi-head attention before a focused MLA source pass.

## [2026-04-29] ingest | DeepSeek-V2 Technical Report

- Source: data/raw/papers/deepseek_v2_technical_report_deepseek_ai_2024.pdf
- Pages created: [[2024 DeepSeek-V2 Technical Report]], [[DeepSeekMoE]]
- Pages updated: [[Multi-Head Latent Attention]], [[KV Cache]], [[Mixture of Experts]], [[Expert Routing]], [[Large Language Models]], [[Transformers]], [[Home]], docs/research_roadmap.md, [[Deep Learning Timeline]], [[Important Papers]], [[index]], [[log]]
- Key concepts: [[Multi-Head Latent Attention]], [[KV Cache]], [[DeepSeekMoE]], [[Mixture of Experts]], [[Expert Routing]]
- Notes: Ingested only DeepSeek-V2 as source context for MLA and high-level DeepSeekMoE: KV-cache motivation, low-rank key-value joint compression, cached latent representation, decoupled RoPE key, relationship to MHA, limited comparison to MQA/GQA, shared and routed experts, fine-grained expert segmentation, total versus activated parameters, and how V2 prepares the architecture reused by DeepSeek-V3. Excluded benchmark-table detail, full data and alignment details, hardware/system implementation, complete MLA derivation, long-context details, DeepSeek-V3 changes, DeepSeek-R1 reasoning, and political/economic discussion.

## [2026-04-29] manual | Refine DeepSeek-V2 ingest

- Source: cross-check against [[2024 DeepSeek-V2 Technical Report]]
- Pages created:
- Pages updated: [[2024 DeepSeek-V2 Technical Report]], [[Multi-Head Latent Attention]], [[log]]
- Key concepts: [[Multi-Head Latent Attention]], [[2024 DeepSeek-V3 Technical Report]]
- Notes: Clarified that V2 grounds mechanisms later reused by V3, and removed the stale MLA question about whether V2 should be the primary MLA source.

## [2026-04-29] ingest | DeepSeekMoE

- Source: data/raw/papers/deepseekmoe_dai_2024.pdf
- Pages created: [[2024 DeepSeekMoE]]
- Pages updated: [[DeepSeekMoE]], [[Mixture of Experts]], [[Expert Routing]], [[Transformer Feed-Forward Networks]], [[Large Language Models]], [[Transformers]], docs/research_roadmap.md, [[Deep Learning Timeline]], [[Important Papers]], [[index]], [[log]]
- Key concepts: [[DeepSeekMoE]], [[Mixture of Experts]], [[Expert Routing]], [[Transformer Feed-Forward Networks]]
- Notes: Ingested only DeepSeekMoE as the source for the MoE mechanism reused by DeepSeek-V2 and DeepSeek-V3: motivation for improving conventional MoE, knowledge hybridity and redundancy, fine-grained expert segmentation, shared expert isolation, routed versus shared experts, high-level top-k routed expert selection, relation to Switch Transformers, and preparation for V2/V3. Excluded full benchmark tables, full training setup, datasets, hardware/system details, hyperparameter sweeps, V2/V3-specific detail except later connections, and unrelated MoE variants beyond brief comparison.

## [2026-04-29] manual | Refine DeepSeekMoE ingest

- Source: cross-check against [[2024 DeepSeekMoE]]
- Pages created:
- Pages updated: [[2024 DeepSeekMoE]], [[DeepSeekMoE]], [[log]]
- Key concepts: [[DeepSeekMoE]], [[Expert Routing]]
- Notes: Clarified that shared expert isolation reduces the activated routed expert count to keep compute comparable, and made the Switch comparison question point to the source note.

## [2026-04-29] refactor | DeepSeek-V2 MLA math repass

- Source: [[2024 DeepSeek-V2 Technical Report]]
- Pages created: [[Multi-Head Latent Attention (Math)]]
- Pages updated: [[Multi-Head Latent Attention]], [[KV Cache]], [[Scaled Dot-Product Attention]], [[2024 DeepSeek-V2 Technical Report]], [[index]], [[log]]
- Key concepts: [[Multi-Head Latent Attention]], [[Multi-Head Latent Attention (Math)]], [[KV Cache]], [[Rotary Position Embedding]]
- Notes: Added a focused math note for MLA covering MHA baseline equations, low-rank key-value compression, query compression, decoupled RoPE, MLA attention computation, and cache-size comparison. Marked projection-absorption algebra and independent MLA/MHA/MQA/GQA comparisons as needing verification.

## [2026-04-29] refactor | DeepSeek-V3 hub refinement

- Source: [[2024 DeepSeek-V3 Technical Report]], [[2024 DeepSeek-V2 Technical Report]], [[2024 DeepSeekMoE]]
- Pages created:
- Pages updated: [[2024 DeepSeek-V3 Technical Report]], [[Expert Routing]], [[LLM Training Systems]], [[Large Language Models]], [[index]], [[log]]
- Key concepts: [[DeepSeekMoE]], [[Multi-Head Latent Attention]], [[Multi-Head Latent Attention (Math)]], [[Expert Routing]], [[LLM Training Systems]]
- Notes: Refined the V3 paper note into a hub that separates inherited architecture from V3-specific additions. Added concise notes on auxiliary-loss-free balancing, MTP, FP8/systems co-design, and clarified that MLA and DeepSeekMoE are grounded by V2 and the DeepSeekMoE paper.

## [2026-04-29] manual | Add synthesis workflow and efficient LLM hub

- Source: project guidance and accumulated wiki notes
- Pages created: [[Efficient LLM Architecture]], docs/synthesis_workflow.md
- Pages updated: [[Home]], docs/research_roadmap.md, docs/ingestion_workflow.md, AGENTS.md, [[index]], [[log]]
- Key concepts: [[Efficient LLM Architecture]], [[KV Cache]], [[FlashAttention]], [[Multi-Head Latent Attention]], [[DeepSeekMoE]], [[Expert Routing]]
- Notes: Added durable guidance for synthesis pages and created the first efficient-architecture hub to connect attention efficiency, KV-cache reduction, sparse MoE capacity, and LLM systems constraints without adding new source material.

## [2026-04-29] lint | Structure, connections, and notation pass

- Source: current vault
- Pages created: [[Notation Conventions]], [[Transformer Architecture]], [[Optimization and Training Stability]], [[Generative Modeling]], [[LLM Inference Systems]]
- Pages updated: [[Attention]], [[Multi-Head Attention]], [[KV Cache]], [[Mixture of Experts]], [[Large Language Models]], [[Transformers]], [[Diffusion Models]], [[Diffusion Design Space]], [[Deep Learning Timeline]], [[Generative Modeling Timeline]], [[Important Papers]], [[Important Videos]], [[Open Questions]], [[Scaled Dot-Product Attention]], [[Diffusion Parameterization]], [[ELBO]], [[Expert Routing]], [[Efficient LLM Architecture]], [[Home]], docs/research_roadmap.md, docs/synthesis_workflow.md, AGENTS.md, [[index]], [[log]]
- Key concepts: [[Notation Conventions]], [[Efficient LLM Architecture]], [[Transformer Architecture]], [[Optimization and Training Stability]], [[Generative Modeling]], [[LLM Inference Systems]], [[Diffusion Design Space]], [[KV Cache]], [[Multi-Head Latent Attention]], [[Expert Routing]]
- Notes: Added a central notation convention page, separated diffusion paper links from concept links, strengthened backlinks between efficient-LLM synthesis, attention variants, KV cache, MoE, and systems pages, added small orientation sections to timeline/index pages, and created short stubs for planned synthesis hubs so guidance links remain Obsidian-consistent.

## [2026-04-29] manual | Add lint workflow guidance

- Source: project guidance and Karpathy LLM Wiki pattern
- Pages created: docs/lint_workflow.md
- Pages updated: docs/design_principles.md, AGENTS.md, [[log]]
- Key concepts: [[Notation Conventions]], [[Efficient LLM Architecture]]
- Notes: Anchored the operational workflow document structure and added a dedicated lint workflow covering Obsidian compliance, structure, links, notation, duplication, abstraction levels, safe fixes, and expected lint output.

## [2026-04-30] manual | Expand Transformer Architecture synthesis

- Source: accumulated transformer architecture notes
- Pages created:
- Pages updated: [[Transformer Architecture]], docs/synthesis_workflow.md, [[index]], [[log]]
- Key concepts: [[Transformers]], [[Attention]], [[Multi-Head Attention]], [[Transformer Feed-Forward Networks]], [[Layer Normalization]], [[Residual Connections]], [[Rotary Position Embedding]], [[Efficient LLM Architecture]]
- Notes: Expanded the transformer synthesis hub to connect attention, feed-forward layers, positional encodings, normalization, residual scaffolding, MoE, KV-cache-related variants, and systems-aware architecture choices without adding new source material.

## [2026-04-30] ingest | Root Mean Square Layer Normalization

- Source: data/raw/papers/rmsnorm_zhang_sennrich_2019.pdf
- Pages created: [[2019 Root Mean Square Layer Normalization]], [[RMSNorm]], [[RMSNorm (Math)]]
- Pages updated: [[Normalization]], [[Layer Normalization]], [[Optimization and Training Stability]], [[Transformer Architecture]], [[Large Language Models]], [[Transformers]], [[Layer Normalization (Math)]], [[Notation Conventions]], [[Deep Learning Timeline]], [[Important Papers]], docs/research_roadmap.md, [[Home]], [[index]], [[log]]
- Key concepts: [[RMSNorm]], [[RMSNorm (Math)]], [[Layer Normalization]], [[Normalization]], [[Optimization and Training Stability]]
- Notes: Ingested RMSNorm with focus on simplifying LayerNorm, root-mean-square normalization without mean-centering, learned gain, relationship to LayerNorm, computational simplicity, sequence/transformer relevance, and later LLM relevance as a connection. Excluded detailed benchmarks, full RNN experiment details, modern LLM claims not in the paper, and optimizer discussion beyond training-stability context.

## [2026-04-30] ingest | Adam

- Source: data/raw/papers/adam_kingma_ba_2014.pdf
- Pages created: [[2014 Adam]], [[AdamW]]
- Pages updated: [[Adam]], [[Gradient Descent]], [[Weight Decay]], [[Optimization and Training Stability]], [[Notation Conventions]], docs/research_roadmap.md, [[Home]], [[Deep Learning Timeline]], [[Important Papers]], [[index]], [[log]]
- Key concepts: [[Adam]], [[Gradient Descent]], [[Weight Decay]], [[AdamW]], [[Optimization and Training Stability]]
- Notes: Ingested Adam with focus on stochastic gradient descent context, first and second moment estimates, bias correction, elementwise adaptive learning rates, the Adam update rule, and hyperparameter roles for `alpha`, `beta_1`, `beta_2`, and `epsilon`. Excluded convergence proof details, regret-bound derivation, extensive benchmark tables, AdaMax derivation, AdamW details, and modern optimizer claims not in the paper.

## [2026-04-30] ingest | Decoupled Weight Decay Regularization

- Source: data/raw/papers/adamw_loshchilov_hutter_2017.pdf
- Pages created: [[2017 Decoupled Weight Decay Regularization]]
- Pages updated: [[AdamW]], [[Adam]], [[Weight Decay]], [[Regularization]], [[Optimization and Training Stability]], [[Notation Conventions]], docs/research_roadmap.md, [[Deep Learning Timeline]], [[Important Papers]], [[index]], [[log]]
- Key concepts: [[AdamW]], [[Adam]], [[Weight Decay]], [[Regularization]], [[Gradient Descent]], [[Optimization and Training Stability]]
- Notes: Ingested AdamW with focus on the difference between L2 regularization and weight decay, why they are equivalent for vanilla SGD after coefficient rescaling, why the equivalence fails for adaptive optimizers, how Adam with L2 regularization couples the penalty to adaptive learning rates, and the high-level AdamW decoupled update. Excluded benchmark tables, SGDW details beyond brief comparison, schedule tuning, extensive experimental setup, later optimizer variants, and modern claims not grounded in the paper.

## [2026-04-30] manual | Capture Muon source trail

- Source: Keller Jordan Muon writeup, KellerJordan/Muon repository, original X-thread reference, Shampoo, Bernstein-Newhouse, and later Muon scaling sources
- Pages created:
- Pages updated: [[log]]
- Key concepts: Muon optimizer, matrix-aware optimization, Shampoo, AdamW
- Notes: Created local source-capture Markdown files under data/raw/blogs, data/raw/repos, and data/raw/reports for future Muon ingestion. These captures store provenance, links, short compliant excerpts, detailed paraphrases, and ingestion cautions rather than verbatim mirrors.

## [2026-04-30] ingest | Muon Optimizer

- Source: data/raw/blogs/muon_keller_jordan_2024.md; data/raw/repos/muon_keller_jordan_readme_2024.md; data/raw/repos/muon_keller_jordan_muon_py_2024.md; data/raw/reports/muon_source_trail_2026-04-30.md
- Pages created: [[2024 Muon Optimizer]], [[Muon Optimizer]], [[Muon Optimizer (Math)]], [[Newton-Schulz Iteration]], [[Matrix-Aware Optimizers]], [[Shampoo]]
- Pages updated: [[AdamW]], [[Optimization and Training Stability]], [[Notation Conventions]], docs/research_roadmap.md, [[Home]], [[Deep Learning Timeline]], [[Important Papers]], [[index]], [[log]]
- Key concepts: [[Muon Optimizer]], [[Muon Optimizer (Math)]], [[Newton-Schulz Iteration]], [[Matrix-Aware Optimizers]], [[Shampoo]], [[AdamW]]
- Notes: Ingested the Muon source bundle as a blog/repository source, not as a peer-reviewed paper. Focused on Muon as an optimizer for hidden-layer 2D parameters, momentum followed by approximate orthogonalization, Newton-Schulz iteration as the practical method, AdamW as the companion optimizer for incompatible parameter classes, and the Shampoo relationship as a future bridge. Kept empirical speedrun and scaling claims labeled as source claims or future connections.

## [2026-04-30] ingest | Shampoo

- Source: data/raw/papers/shampoo_preconditioned_tensor_optimization_gupta_2018.pdf
- Pages created: [[2018 Shampoo]], [[Preconditioning]]
- Pages updated: [[Shampoo]], [[Matrix-Aware Optimizers]], [[Optimization and Training Stability]], [[Muon Optimizer]], [[Muon Optimizer (Math)]], [[2024 Muon Optimizer]], [[Notation Conventions]], docs/research_roadmap.md, [[Home]], [[Deep Learning Timeline]], [[Important Papers]], [[index]], [[log]]
- Key concepts: [[Shampoo]], [[Preconditioning]], [[Matrix-Aware Optimizers]], [[Adam]], [[AdamW]], [[Muon Optimizer]]
- Notes: Ingested Shampoo with focus on why preconditioning helps, why full-matrix preconditioning is expensive, matrix/tensor-aware per-dimension preconditioners, the high-level matrix update, and the bridge from coordinatewise adaptive optimizers toward matrix-aware methods. Excluded convergence proof, trace inequality derivations, benchmark tables, implementation details, distributed Shampoo variants, SOAP, Muon derivation, and large-scale LLM claims.

## [2026-04-30] ingest | Old Optimizer, New Norm

- Source: data/raw/papers/old_optimizer_new_norm_bernstein_newhouse_2024.pdf
- Pages created: [[2024 Old Optimizer New Norm]], [[Steepest Descent]]
- Pages updated: [[Preconditioning]], [[Shampoo]], [[Muon Optimizer]], [[Muon Optimizer (Math)]], [[2024 Muon Optimizer]], [[Matrix-Aware Optimizers]], [[Optimization and Training Stability]], [[Notation Conventions]], docs/research_roadmap.md, [[Home]], [[Deep Learning Timeline]], [[Important Papers]], [[index]], [[log]]
- Key concepts: [[Steepest Descent]], [[Preconditioning]], [[Shampoo]], [[Muon Optimizer]], [[Matrix-Aware Optimizers]], [[Adam]], [[AdamW]]
- Notes: Ingested Old Optimizer, New Norm with focus on optimizer update geometry, steepest descent under different norms, matrix-valued versus coordinatewise parameter views, Shampoo-like spectral update geometry, and conceptual bridges to Muon-like semi-orthogonal updates. Excluded proof details, long derivations, implementation details, benchmarks, unsupported LLM-scale claims, and any treatment of Muon as settled consensus.

## [2026-04-30] ingest | Muon is Scalable for LLM Training

- Source: data/raw/papers/muon_is_scalable_for_llm_training_moonshot_ai_2025.pdf
- Pages created: [[2025 Muon is Scalable for LLM Training]]
- Pages updated: [[Muon Optimizer]], [[Muon Optimizer (Math)]], [[Matrix-Aware Optimizers]], [[Optimization and Training Stability]], [[LLM Training Systems]], [[Notation Conventions]], docs/research_roadmap.md, [[Deep Learning Timeline]], [[Important Papers]], [[index]], [[log]]
- Key concepts: [[Muon Optimizer]], [[Muon Optimizer (Math)]], [[AdamW]], [[Weight Decay]], [[Matrix-Aware Optimizers]], [[LLM Training Systems]]
- Notes: Ingested the Moonshot AI Muon scaling report with focus on large-scale LLM training, Muon versus AdamW parameter groups, weight decay, update RMS scaling, scaling-law evidence, training-stability observations, and how the source strengthens or limits claims from [[2024 Muon Optimizer]]. Excluded full benchmark tables, implementation details, infrastructure details beyond optimizer-scaling constraints, unrelated architecture details, deep Newton-Schulz derivation, unsupported general superiority claims, and marketing/economic claims.
