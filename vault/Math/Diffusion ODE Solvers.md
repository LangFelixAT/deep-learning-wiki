# Diffusion ODE Solvers

## Metadata
- Type: math
- Status: partially verified

## Goal
Describe how diffusion sampling can be viewed as numerical integration of an ODE, and why solver choice affects sampling speed and quality.

## Definitions
- Source: [[2022 DPM-Solver]].
- Diffusion ODE solvers integrate the [[Probability Flow ODE]] from high noise to low noise.
- A noise-prediction diffusion ODE can be written structurally as:

$$
dx_t / dt = f(t) x_t + g(t)^2 / (2 \sigma_t) \epsilon_{\theta}(x_t,t)
$$
- Needs verification: exact signs and scalings depend on whether the model is parameterized as noise prediction, score prediction, or denoiser prediction, and on the chosen noise schedule.
- $\epsilon_{\theta}(x_t,t)$ is the learned noise-prediction network.
- The noise schedule determines $\alpha_t$, $\sigma_t$, and the time/noise parameterization used by the solver.

## Assumptions
- The learned model is fixed; solver changes do not retrain the network.
- The ODE shares the desired marginals with the corresponding diffusion process under the probability-flow formulation.
- The solver has access to a continuous or interpolated time/noise input for the model.
- Needs verification: formal convergence guarantees require regularity assumptions on the neural network and schedule.

## Connection to probability flow ODE
- [[Probability Flow ODE]] gives a deterministic sampling trajectory associated with a diffusion SDE.
- A finite sampler approximates this continuous trajectory by evaluating the learned score or noise predictor at selected points.
- Solver error comes from replacing the continuous ODE solution with a finite-step numerical approximation.

## Euler method and DDIM perspective
- Euler-style methods approximate the ODE using local first-order information.
- [[DDIM Sampling]] can be understood as a deterministic first-order solver for the diffusion ODE.
- [[2022 DPM-Solver]] states that DDIM is equivalent to DPM-Solver-1, its first-order update.

## High-order solver idea
- Higher-order solvers use additional structure or intermediate evaluations to reduce local truncation error.
- DPM-Solver exploits the semi-linear form of the diffusion ODE: it handles the linear part analytically and approximates the nonlinear neural-network part.
- After a change of variable to half-log-SNR, the remaining term is an exponentially weighted integral of the network output.
- This motivates an exponential-integrator view without requiring a full black-box ODE solve.

## Derivation
- Start from the probability-flow ODE or the equivalent diffusion ODE under the chosen parameterization.
- Separate the analytically tractable linear term from the neural-network-dependent term.
- Change variables to a schedule coordinate such as half-log-SNR.
- Approximate the remaining integral with a first- or higher-order numerical rule.
- Skipped steps: full DPM-Solver order conditions and coefficient derivations.

## Why step count can be reduced
- If each step has lower numerical error, fewer steps may be needed for acceptable sample quality.
- Higher-order methods can improve the error-vs-network-evaluation tradeoff compared with simple first-order updates.
- The practical gain depends on the model, noise schedule, parameterization, and evaluation budget.

## Interpretation
Solver choice is part of the diffusion model's sampling design. A learned denoiser or noise predictor does not fully determine sample quality; the numerical method used to integrate the reverse trajectory also matters.

## Common mistakes
- Treating sampler choice as an implementation detail with no modeling consequences.
- Assuming DDIM and higher-order ODE solvers differ only by timestep count.
- Ignoring that the solver's variables depend on the diffusion parameterization and noise schedule.
- Confusing training-free solver improvements with retraining or distillation.

## Related concepts
- [[Probability Flow ODE]]
- [[DDIM Sampling]]
- [[Diffusion Parameterization]]
- [[Diffusion Design Space]]
- [[Diffusion Models]]
- [[2022 DPM-Solver]]
