[Back to overveiw](Readme.md)

# Probabilistic reasoning

## Core notions

### Event
- An **event** is a set of possible worlds (i.e., outcomes) in which the event is true.

### Random Variable
- A **random variable** represents a probabilistic variable with a domain (set of possible values).
- Example: `Weather ∈ {sunny, cloudy, rainy}`

### Conditional Probability
- Defines the probability of an event **given** another event:
  
``P(a | b) = P(a ∧ b) / P(b)``, provided that `P(b) > 0`.

### Full Joint Probability Distribution
- Specifies the probability for **each complete assignment** of values to all variables.
- Example for variables A and B:
  
``P(A, B)``

### Independence
- Two variables X and Y are **independent** if:
  
``P(X, Y) = P(X) * P(Y)``, or equivalently, ``P(X | Y) = P(X)``

- Example: Two dice rolls:
  
``P(Die1 = 5, Die2 = 3) = P(Die1 = 5) * P(Die2 = 3)``

---

## Probabilistic Inference

### Bayes' Rule
- Allows reversing the direction of inference:
  
``P(A | B) = (P(B | A) * P(A)) / P(B)``

### Marginalization
- Summing over unobserved variables:
  
``P(Y) = Σz P(Y, z)``

### Normalization
- Ensures probabilities sum to 1:
  
``P(Y | E = e) = α * P(Y, E = e)``, where
  
``α = 1 / Σy P(Y = y, E = e)``

### Causal vs Diagnostic Reasoning
- **Causal**: From cause to effect, ``P(effect | cause)``
- **Diagnostic**: From effect to cause, ``P(cause | effect)``

---
## Bayesian Network

- A **Bayesian network (BN)** is a directed acyclic graph (DAG) representing:
  - Random variables (nodes)
  - Probabilistic dependencies (edges)
  - Each variable has a **conditional probability table (CPT)**

### Components
- Nodes: Random variables
- Edges: Causal dependencies
- Parents(X): Set of variables that directly influence X
- CPT: ``P(X | Parents(X))``

### Chain Rule in BNs
- The joint distribution over all variables is the product of local conditional distributions:
  
``P(X₁, ..., Xₙ) = Π P(Xᵢ | Parents(Xᵢ))``

---
## Inference in Bayesian Networks

Goal: Compute ``P(Query | Evidence)``

### Enumeration
- **Brute-force** method using the full joint distribution.
- Uses summing and multiplying probabilities via chain rule.
- Inefficient due to repeated subcomputations.

### Variable Elimination
- Improves on enumeration by **reusing intermediate results**.
- Works with **factors** (tables from CPTs) and applies:
  - **Pointwise product** of factors
  - **Summing out** variables
- More efficient, often used in practice.

### Rejection Sampling
- Generate full samples from the network.
- **Reject** those inconsistent with the evidence.
- Estimate: ``P(X | e) ≈ N(X, e) / N(e)``
- Weakness: Can waste many samples (especially with unlikely evidence).

### Likelihood Weighting
- Improves on rejection sampling by:
  - **Fixing evidence variables**
  - **Sampling only non-evidence variables**
  - **Weighting each sample** by the likelihood of the evidence given the sampled values
  
Formula:
``P(X | e) ≈ α Σ Samples w(X, e)``

- Weakness: Weight values can be very small → low accuracy

---

## Summary Table

| Concept                  | Description                                                                 |
|--------------------------|-----------------------------------------------------------------------------|
| Event                    | Set of possible worlds                                                      |
| Random Variable          | Variable with a domain of values                                            |
| Conditional Probability  | Probability of A given B                                                    |
| Full Joint Distribution  | Probability over all combinations of variables                              |
| Independence             | X and Y are independent if ``P(X, Y) = P(X) * P(Y)``                         |
| Bayes’ Rule              | Reverse conditional probabilities                                           |
| Marginalization          | Sum out unobserved variables                                                |
| Normalization            | Ensure valid probability distribution                                       |
| Bayesian Network         | DAG representation of conditional dependencies                             |
| Enumeration              | Simple but inefficient inference method                                     |
| Variable Elimination     | Efficient inference using factor manipulation                              |
| Rejection Sampling       | Keep only samples consistent with evidence                                  |
| Likelihood Weighting     | Use weights for evidence-consistent samples                                |


[Back to overveiw](Readme.md)
