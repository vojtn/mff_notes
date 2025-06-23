[Back to overveiw](Readme.md)

# Automated planning
Automated planning is concerned with generating a **sequence of actions** (a **plan**) that leads from an initial state to a goal state, given a model of the environment.

## Planning domain
A **planning domain** defines the **types of actions** (called **operators**) that can be performed in an environment. It includes:
- **States** (usually sets of ground atoms)
- **Action schemas** (abstract representations of actions)
- **Transition model** (how actions affect the state)

### Planning problem
Triple (O,s0,g)
- O = planning domain (set of operators/action schemas)
- s0 = initial state (a set of ground atoms)
- g = goal condition (a set of literals to be made true)

## Plan
Sequence of actions <a1,a2,...,ak>
That transforms the **initial state** `s₀` into a **state that satisfies the goal** `g`.

## Representation of states
### State 
A finite set of **ground atoms** (fully instantiated predicates)

### Goal g
A set of **literals** (atoms or their negations)

#### Action schema (operator)
Desribes the action without specifying the particular objects to which the action applies

**Operator** 
triple (name, precondition, effects)
- name = Action name with parameters (e.g., `Move(x, y)`)
- precond = literals that must hold in the state
- effects = literals that will become true after operation application

### Planning operation/action


### Applicability and relevance of action
- **Applicable**: An action `a` is applicable in state `s` **iff** all `preconditions(a)` are satisfied in `s`.
- **Relevant**: An action is relevant to a goal `g` **iff** it has an effect that satisfies at least one literal in `g`.

### Transition function
The **transition function** defines how the world state changes when an action is applied.

Result(s, a) = (s - del(a)) ∪ add(a)
Where:
- `add(a)` = positive effects (literals added to the state)
- `del(a)` = negative effects (literals removed from the state)

This models how an action modifies the current state by removing and adding facts.

### Regression set

In **regression planning**, we reason **backwards** from a goal.
The **regression** of a goal `g` over an action `a`:

y-1(g,a) = (g - effects(a)) U precond(a)

Regress(g, a) = (g \ add(a)) ∪ precond(a)


This produces a new sub-goal that must be achieved before `a` is applied.


## progression planning

## Forward (progression) planning
From initial state to a goal state
nondeterminism implemented by a search algorithm

- Start from **initial state** `s₀`
- Apply applicable actions to reach new states
- Repeat until a state satisfies **goal `g`**

**Characteristics:**
- Simple and intuitive
- May explore many irrelevant paths
- Implemented as a search algorithm
---

## Backward(Regression) planning
starts with the goal and applies the
actions backward until it reaches the initial state.
only relevan actions are explored -> smaller branching factor

- Start from the **goal**
- Apply actions **in reverse** (via regression) to reduce the goal to something true in `s₀`

**Advantages:**
- Explores only relevant actions
- Smaller branching factor than progression


## Planning by logical reasoning (situation calculus)

uses special terms to describe situations (give names to states)

A logical language for representing and reasoning about **dynamic worlds** and **actions**.

### Key Elements:

- **Situations**: History of actions (e.g., `do(a, s)`)
- **Actions**: Change the world from one situation to another
- **Fluents**: Properties that can change between situations (e.g., `At(x, s)`)

## Plan-space planning (partial order planning)
- Plans are **partially ordered**, not linear sequences
- Only impose orderings where necessary (e.g., for causal links)
- Greater flexibility and reusability


## Hiearchical planning
Decomposing tasks to subtasks until primitive asks are obtained

- **Decompose** high-level tasks into **subtasks**
- Continue decomposing until **primitive actions** are reached
- Reflects human-like planning strategies

[Back to overveiw](Readme.md)