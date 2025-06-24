[Back to overveiw](Readme.md)

# Decision making
Decision making under uncertainty is based on selecting actions that **maximize expected utility**.

## Utility function
- `U(s)`: A real number representing the **desirability** (or preference) of being in state `s`.
- Captures agent’s preferences over states.
- Higher utility = more preferred state.

## Expected utility
The **expected utility** of an action `a`, given evidence `e`:
EU(a | e) = ∑ₛ P(Result(a) = s | a, e) × U(s)

- Sum over all possible outcome states `s`
- Weigh each utility by the probability of that outcome
- Captures uncertainty in action outcomes

---

## Maximum Expected Utility (MEU)

A **rational agent** should choose the action that **maximizes expected utility**:
a* = argmaxₐ EU(a | e)
This is the formalization of **rationality**.


## Decision Networks (Influence Diagrams)

A **decision network** is an extension of a Bayesian network that supports decision making.

### Components:
- **Chance nodes**: Represent random variables (ovals)
- **Decision nodes**: Represent possible actions (rectangles)
- **Utility nodes**: Represent utility functions (diamonds)

### Purpose:
- Compute MEU by evaluating the outcomes and their probabilities
- Help choose the optimal action using probabilistic inference and utility maximization

---

## Markov Decision Process (MDP)

An MDP models **sequential decision problems** in a **fully observable**, **stochastic** environment.

### Defined by a 4-tuple (S, A, T, R):

- `S`: Set of states
- `A`: Set of actions
- `T(s, a, s')`: **Transition model** – probability that action `a` in state `s` leads to state `s'`  
  `T(s, a, s') = P(s' | s, a)`
- `R(s)`: **Reward function** – numerical reward received when entering state `s`

---

## Utility in MDPs

The utility of a state is defined as the **expected total (possibly discounted) reward**:
U(s) = expected sum of rewards from s onward
Often discounted to prioritize immediate rewards:
- γ ∈ [0,1] is the **discount factor**

---

## Policy

A **policy** π(s) is a function that maps each state `s` to an action `a`.

- **Optimal policy** π* yields the highest expected utility from every state.

---

## Bellman Equation

Gives a recursive definition of utility:

U(s) = R(s) + γ × maxₐ ∑ₛ' P(s' | s, a) × U(s')

- Forms the basis of **value iteration** and **policy iteration**
- Defines utility of a state as **immediate reward** plus **expected utility of successor states**

---

## Value Iteration

**Value Iteration** is a dynamic programming algorithm that computes the **optimal utility values** for each state using the **Bellman update**.

### Steps:
1. Initialize utility values: `U(s) = 0` for all states `s`
2. Repeat until convergence:
   - For each state `s`, update its utility using the Bellman equation:
U(s) ← R(s) + γ × maxₐ ∑ₛ' P(s' | s, a) × U(s')
3. After convergence, extract the **optimal policy**:
π*(s) = argmaxₐ ∑ₛ' P(s' | s, a) × U(s')

### Notes:
- `γ` is the **discount factor** (0 ≤ γ ≤ 1)
- Guarantees convergence to optimal utilities
- Computationally efficient when the number of states is manageable

---

## Policy Iteration

**Policy Iteration** solves an MDP by:
1. **Policy Evaluation**: Given a policy π, compute utility `U(s)` for each state under π.
2. **Policy Improvement**: Update π by choosing better actions based on current utilities.

### Repeat:
- Evaluate the current policy until utilities converge
- Improve policy using:
π(s) ← argmaxₐ ∑ₛ' P(s' | s, a) × U(s')
-  Stop when policy no longer changes (converged to optimal policy π*)

### Comparison:
- Often converges faster than value iteration
- Especially useful when actions have deterministic or sparse effects

---

## Partially Observable MDP (POMDP)

**POMDP** generalizes MDPs to environments where the agent **cannot fully observe the state**.

### Additional Elements:
- **Observation model**: `P(e | s)` — likelihood of perceiving evidence `e` in state `s`
- **Belief state**: A probability distribution over possible world states
  - Represents the agent’s **uncertainty about the true state**

### Solving POMDPs:
- Maintain and update the **belief state** using Bayesian inference
- Plan over belief states instead of concrete states
- Algorithms: **Value iteration over belief space**, **point-based approximation methods**

---

[Back to overveiw](Readme.md)
