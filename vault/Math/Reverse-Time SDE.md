# Reverse-Time SDE

## Metadata
- Type: math
- Status: partially verified

## Goal
Define the reverse stochastic process used to generate samples from noise.

## Definitions
- Source: [[2021 Score-Based Generative Modeling through SDEs]].
- The reverse-time SDE runs backward from $T$ to $0$.
- It is simulated from $t = T$ to $t = 0$, so time is reversed relative to the forward SDE.
- For forward SDE $dx = f(x,t) dt + g(t) dw$, the reverse-time SDE is:

$$
dx = [f(x,t) - g(t)^2 \nabla_x \log p_t(x)] dt + g(t) d \bar{w}
$$
- $\bar{w}$ is a Wiener process when time flows backward.
- The score $\nabla_x \log p_t(x)$ is approximated by $s_{\theta}(x,t)$.
- The reverse drift depends on the score of the forward marginals $p_t(x)$.

## Assumptions
- The score of each marginal distribution is available or accurately estimated.
- The reverse-time result relies on conditions from stochastic process theory. Needs verification: formal theorem assumptions are not expanded here.
- Numerical sampling discretizes this reverse process.

## Derivation
- Start from the forward SDE that maps data to a prior.
- Use the reverse-time SDE formula, which modifies the drift by a score-dependent term.
- Replace the unknown score $\nabla_x \log p_t(x)$ with the learned score network $s_{\theta}(x,t)$.
- Simulate the reverse-time SDE from $x(T) ~ p_T$ to produce $x(0)$.
- Skipped steps: proof of the reverse-time SDE formula.

## Interpretation
- The score tells the reverse process how to remove noise in a distribution-aware way.
- This is the continuous-time counterpart of learned reverse denoising transitions.

## Common mistakes
- Omitting the score term from the reverse drift.
- Treating the reverse-time SDE as deterministic.
- Confusing the reverse-time SDE with the probability flow ODE.

## Related concepts
- [[Forward SDE]]
- [[Probability Flow ODE]]
- [[Score Matching]]
- [[Diffusion Models]]
- [[2021 Score-Based Generative Modeling through SDEs]]
