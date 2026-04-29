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
