# Forward SDE

## Metadata
- Type: math
- Status: partially verified

## Goal
Define the continuous-time noising process used in score-based generative modeling through SDEs.

## Definitions
- Source: [[2021 Score-Based Generative Modeling through SDEs]].
- A forward SDE maps data toward a tractable prior distribution by gradually injecting noise.
- General form:

`dx = f(x,t) dt + g(t) dw`.

- `f(x,t)` is the drift coefficient.
- `g(t)` is the diffusion coefficient.
- `w` is a standard Wiener process.
- `p_t(x)` denotes the marginal density of `x(t)`.
- The reverse generative process depends on the score of these forward marginals, `grad_x log p_t(x)`.

## Assumptions
- The process starts at `x(0) ~ p_0`, the data distribution.
- The final distribution `p_T` is chosen to be tractable for sampling.
- The paper assumes conditions under which the SDE has a unique strong solution. Needs verification: formal Lipschitz and regularity conditions are not expanded here.

## Derivation
- Replace a finite sequence of noise perturbations with a continuous-time stochastic process.
- Choose drift and diffusion coefficients so the process evolves from data to noise.
- The score model is later trained on the intermediate marginal distributions `p_t(x)`.
- Skipped steps: deriving particular VE/VP SDEs from discrete SMLD/DDPM limits.

## Interpretation
- The forward SDE is the continuous-time analogue of a noising process.
- It is not the generative direction; generation uses the reverse-time process.

## Common mistakes
- Confusing the forward SDE with the sampling process.
- Forgetting that the forward SDE has no trainable score network.
- Treating all choices of `f` and `g` as equivalent.

## Related concepts
- [[Reverse-Time SDE]]
- [[Probability Flow ODE]]
- [[Diffusion Models]]
- [[Score Matching]]
- [[2021 Score-Based Generative Modeling through SDEs]]
