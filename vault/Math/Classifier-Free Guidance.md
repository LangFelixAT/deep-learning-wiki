# Classifier-Free Guidance

## Metadata
- Type: math
- Status: partially verified

## Goal
Define classifier-free guidance as a way to condition diffusion sampling without an external classifier.

## Definitions
- Source: [[2022 Classifier-Free Diffusion Guidance]].
- Conditional prediction: a model prediction that receives conditioning information `c`, written as `s_theta(x_t,t,c)` or `epsilon_theta(x_t,t,c)`.
- Unconditional prediction: a model prediction without conditioning, written as `s_theta(x_t,t)` or by passing a null condition.
- `w` is the guidance strength used at sampling time.

## Conditional vs unconditional
- Conditional diffusion models learn a reverse process for samples associated with condition `c`.
- Unconditional diffusion models learn the marginal reverse process without condition information.
- Classifier-free guidance trains both behaviors in one model by sometimes replacing `c` with a null condition.

## Training procedure
- Sample a training pair `(x,c)`.
- Corrupt `x` to a noisy state `x_t`.
- With probability `p_uncond`, replace `c` by a null condition.
- Train the denoising or noise-prediction objective as usual.

## Guidance formula
In score form:

`s_guided(x_t,t,c) = (1 + w) s_theta(x_t,t,c) - w s_theta(x_t,t)`.

In noise-prediction form:

`epsilon_guided(x_t,t,c) = (1 + w) epsilon_theta(x_t,t,c) - w epsilon_theta(x_t,t)`.

Needs verification: signs and coefficients must be checked against the model parameterization used by a specific sampler.

## Role of w
- `w = 0` gives the model's learned conditional prediction without additional guidance amplification.
- Larger `w` amplifies the difference between conditional and unconditional predictions.
- Increasing `w` tends to improve condition adherence or sample fidelity while reducing diversity.
- The useful range of `w` is model and task dependent.

## Interpretation
The conditional prediction says where to denoise under condition `c`; the unconditional prediction says where to denoise on average. Their difference acts like a direction that emphasizes the condition during sampling.

If the score estimates were exact, the difference between conditional and unconditional scores would correspond to an implicit classifier gradient:

`s_theta(x_t,t,c) - s_theta(x_t,t) approx grad_x log p_t(c|x_t)`.

This makes classifier-free guidance analogous to classifier guidance, but without training a separate classifier.

## Common mistakes
- Thinking classifier-free guidance uses a separate classifier.
- Confusing condition dropout during training with dropout in the neural network architecture.
- Assuming larger `w` is always better.
- Forgetting that guided sampling can require two model predictions per step.
- Applying the score-form equation directly to noise prediction without checking signs and scaling.

## Related concepts
- [[Diffusion Models]]
- [[Score Matching]]
- [[Diffusion ODE Solvers]]
- [[2022 Classifier-Free Diffusion Guidance]]
