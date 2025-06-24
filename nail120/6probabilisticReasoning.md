[Back to overveiw](Readme.md)

# Probabilistic reasoning over time

## Transition model
- Specifies the **probability distribution over the next state** given the current (or past) states.
- Assumes the **Markov property**: the future is conditionally independent of the past given the present.
  
**Markov Assumption:**
``P(Xₜ | X₀:ₜ₋₁) = P(Xₜ | Xₜ₋₁)``


## Observation model
- Describes how **evidence variables** depend on the state variables.
- Captures the likelihood of receiving observations given the hidden state.

Example:
``P(Eₜ | Xₜ)`` (assuming conditional independence from earlier states and observations)

---

## Basic inference tasks

### Filtering
- Compute the **posterior distribution over the current state**, given all evidence so far.
- Answers: “**Where am I now?**”

``P(Xₜ | e₁:ₜ)``

### Prediction
- Compute the **distribution over future states**, given current evidence.
- Answers: “**Where will I be?**”

``P(Xₜ₊ₖ | e₁:ₜ)``, for `k > 0`

### Smoothing
- Compute the **posterior over a past state**, given all evidence up to the present.
- Answers: “**Where was I?**”

``P(Xₖ | e₁:ₜ)``, for `0 ≤ k < t`

### Most-likely explanation
- Find the **most probable sequence of hidden states** that explains the evidence.
- Answers: “**What path did I go through?**”

``argmaxₓ₁:ₜ P(x₁:ₜ | e₁:ₜ)``

---

## Hidden Markov Model (HMM)
- A special case of a dynamic model where:
  - **State**: Single discrete random variable `Xₜ`
  - **Observation**: Single evidence variable `Eₜ`
- Transitions and emissions are described by matrices.

### HMM Assumptions
- `Xₜ` depends only on `Xₜ₋₁` (Markov assumption)
- `Eₜ` depends only on `Xₜ` (sensor model)

### Localization Example
- A robot moves randomly on a grid and tries to **estimate its position** using noisy sensors and a known movement model.

## Dynamic Bayesian Network (DBN)
- Generalization of HMMs that allow:
  - **Multiple variables per time step**
  - **Structured dependencies** within each time slice and across time slices

- Represented as a pair of Bayesian networks:
  1. One for the initial state (`P(X₀)`)
  2. One for the transition model (`P(Xₜ | Xₜ₋₁)`)

---

## DBN vs HMM

| Feature         | HMM                            | DBN                                   |
|----------------|--------------------------------|----------------------------------------|
| States          | Single variable                | Multiple variables                     |
| Transitions     | Matrix-based                   | Factored (graph-based)                 |
| Observations    | Single observation             | Multiple (structured) observations     |
| Expressiveness  | Less flexible                  | More expressive and general            |

- HMM is a **special case** of a DBN with only one state and one observation variable per time step.

[Back to overveiw](Readme.md)