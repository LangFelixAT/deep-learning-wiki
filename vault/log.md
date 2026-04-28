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
