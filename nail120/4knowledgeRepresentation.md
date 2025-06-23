[Back to overveiw](Readme.md)

# Knowledge representation

## Knowledge based agent
A **knowledge-based agent** is an agent that reasons and acts by manipulating **explicit knowledge** stored in a **knowledge base (KB)**.  
It uses two main operations:
- **TELL**: Adds new information to the KB.
- **ASK**: Queries the KB to derive conclusions using logical inference.

## Formula
A **formula** (or sentence) in propositional logic is built from:
- **Propositional symbols**: P, Q, R, ...
- **Logical connectives**:  
  - ¬ (negation)  
  - ∧ (conjunction)  
  - ∨ (disjunction)  
  - → (implication)  
  - ↔ (biconditional)

Formulas are constructed recursively from atomic propositions using these connectives.


### CNF (Conjunctive Normal Form)
A formula is in CNF if it is a conjunction of clauses, where a **clause** is a disjunction of **literals** (atomic variables or their negation).

To convert a formula to CNF:
1. Eliminate ↔ and →
2. Move ¬ inward (De Morgan’s laws)
3. Distribute ∨ over ∧

### DNF (Disjunctive Normal Form)
A formula is in DNF if it is a disjunction of conjunctions of literals.

## Horn clauses
A **Horn clause** is a disjunction of literals with at most **one positive literal**.

Example:  
¬A ∨ ¬B ∨ C ≡ (A ∧ B → C)

Horn clauses are commonly used in rule-based systems and are suitable for efficient inference via forward/backward chaining.

## DPLL algorithm
A complete backtracking search algorithm for deciding **satisfiability** of propositional logic formulas in CNF.

Key techniques:
- **Pure Symbol Heuristic**: If a symbol always appears with the same polarity (only positive or only negative), assign it accordingly to satisfy all clauses it appears in.
- **Unit Clause Heuristic**: If a clause has only one literal (unit clause), assign the value that satisfies it.

DPLL improves upon naive truth-table checking and is the basis of modern SAT solvers.

### Pure symbol 
Always appears with the same “sign” in all clauses

### Unit clause
A clause with just one literal

### Model, Satisfiability and Entailment
 **Model**: A truth assignment to all propositional variables.
- **Satisfiability**: A formula is satisfiable if there exists **at least one model** in which it is true.
- **Entailment**: A KB entails a sentence α (written `KB ⊨ α`) if α is **true in every model where KB is true**.


### Resolution Algorithm
A **complete inference procedure** for propositional logic (in CNF).  
It derives new clauses by resolving pairs with complementary literals.

#### Resolution Rule
From (A ∨ B), (¬B ∨ C) infer (A ∨ C)

If resolution derives the **empty clause (⊥)**, the original formula is **unsatisfiable**, meaning the query is entailed.

### Empty Clause
Denotes a contradiction. If derived, it proves entailment by contradiction.

### Forward Chaining
- **Data-driven** inference
- Start from known facts; apply rules to infer new facts
- Continues until the goal is derived (or no new facts)

Efficient for Horn clauses and works in linear time.

### Backward Chaining
- **Goal-driven** reasoning
- Start from the query (goal) and recursively prove its subgoals
- Efficient for situations with specific goals

Commonly used in logic programming (e.g., Prolog).

[Back to overveiw](Readme.md)