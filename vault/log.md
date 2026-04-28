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
