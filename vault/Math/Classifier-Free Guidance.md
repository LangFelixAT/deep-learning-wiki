# Classifier-Free Guidance

## Metadata
- Type: math
- Status: partially verified

## Goal
Define classifier-free guidance as a way to condition diffusion sampling without an external classifier.

## Definitions
- Source: [[2022 Classifier-Free Diffusion Guidance]].
- Conditional prediction: a model prediction that receives conditioning information $c$, written as $s_{\theta}(x_t,t,c)$ or $\epsilon_{\theta}(x_t,t,c)$.
- Unconditional prediction: a model prediction without conditioning, written as $s_{\theta}(x_t,t)$ or by passing a null condition.
- $w$ is the guidance strength used at sampling time.

## Assumptions
- The same model can produce conditional and unconditional predictions.
- The unconditional behavior is learned by dropping or nulling the condition during training.
- The formula must match the model parameterization used by the sampler.

## Conditional vs unconditional
- Conditional diffusion models learn a reverse process for samples associated with condition $c$.
- Unconditional diffusion models learn the marginal reverse process without condition information.
- Classifier-free guidance trains both behaviors in one model by sometimes replacing $c$ with a null condition.

## Training procedure
- Sample a training pair $(x,c)$.
- Corrupt $x$ to a noisy state $x_t$.
- With probability $p_{\mathrm{uncond}}$, replace $c$ by a null condition.
- Train the denoising or noise-prediction objective as usual.

## Guidance formula
In score form:

$$
s_{guided}(x_t,t,c) = (1 + w) s_{\theta}(x_t,t,c) - w s_{\theta}(x_t,t)
$$
In noise-prediction form:

$$
\epsilon_{guided}(x_t,t,c) = (1 + w) \epsilon_{\theta}(x_t,t,c) - w \epsilon_{\theta}(x_t,t)
$$
Needs verification: signs and coefficients must be checked against the model parameterization used by a specific sampler.

## Derivation
- Train the model with condition $c$ present for some examples and replaced by a null condition for others.
- At sampling time, evaluate both the conditional and unconditional predictions.
- Form a linear combination that amplifies the difference between the conditional and unconditional directions.
- Skipped steps: derivation from classifier guidance and exact parameterization-specific conversions.

## Role of w
- $w = 0$ gives the model's learned conditional prediction without additional guidance amplification.
- Larger $w$ amplifies the difference between conditional and unconditional predictions.
- Increasing $w$ tends to improve condition adherence or sample fidelity while reducing diversity.
- The useful range of $w$ is model and task dependent.

## Interpretation
The conditional prediction says where to denoise under condition $c$; the unconditional prediction says where to denoise on average. Their difference acts like a direction that emphasizes the condition during sampling.

If the score estimates were exact, the difference between conditional and unconditional scores would correspond to an implicit classifier gradient:

$$
s_{\theta}(x_t,t,c) - s_{\theta}(x_t,t) \approx \nabla_x \log p_t(c|x_t)
$$
This makes classifier-free guidance analogous to classifier guidance, but without training a separate classifier.

## Common mistakes
- Thinking classifier-free guidance uses a separate classifier.
- Confusing condition dropout during training with dropout in the neural network architecture.
- Assuming larger $w$ is always better.
- Forgetting that guided sampling can require two model predictions per step.
- Applying the score-form equation directly to noise prediction without checking signs and scaling.

## Related concepts
- [[Diffusion Models]]
- [[Score Matching]]
- [[Diffusion ODE Solvers]]
- [[2022 Classifier-Free Diffusion Guidance]]
