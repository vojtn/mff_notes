[Back to overveiw](Readme.md)

# Constraint satisfaction

## Constraint Satisfaction Problem (CSP)
A **CSP** is defined by:
- A finite set of **variables**: {X₁, X₂, ..., Xₙ}
- Each variable Xᵢ has a **domain** Dᵢ: a finite set of possible values
- A finite set of **constraints** that restrict allowable combinations of values

A **solution** to a CSP is an assignment of values to variables such that:
- Each variable Xᵢ is assigned a value from its domain Dᵢ
- All constraints are satisfied

## Examples
### N-Queens Problem
- **Variables**: `r₁, r₂, ..., rₙ` (row position of queen in column *i*)
- **Domains**: `{1, ..., N}`
- **Constraints**:
  - No two queens in the same row
  - No two queens on the same diagonal

### Sudoku
- **Variables**: Each cell in a 9x9 grid
- **Domains**: `{1, ..., 9}`
- **Constraints**:
  - All values in each row, column, and 3x3 block must be **all-different**

## Constraint modeling
Formulating a real-world problem as a CSP:
- Define variables
- Define their domains
- Define constraints between them

## Variable ordering
**Fail-first principle**: assign first a variable, which will probably lead to a failure
- **dom heuristic** = variable with the **smallest** domain first
- **deg heuristic** = variable participating in the **largest number** of constraint first

## Value ordering
**Succeed-first principle**:
Try values that are **most likely to lead to a solution**.

- **Least-constraining value**: Choose the value that rules out the fewest choices for neighboring variables.

## Arc consistency

An arc (X → Y) is **arc consistent** if:

> For every `x ∈ Dₓ`, there exists **some** `y ∈ Dᵧ` such that the constraint between `X` and `Y` is satisfied.

A CSP is **arc consistent** if every arc in both directions is arc consistent.


## K-Consistency

A CSP is **k-consistent** if:

> For any consistent assignment to `k − 1` variables, there exists a value for any `kᵗʰ` variable such that all constraints among the `k` variables are satisfied.

- **1-consistency** = node consistency  
- **2-consistency** = arc consistency  
- **3-consistency** = path consistency

### Strong k-consistency
A CSP is **strongly k-consistent** if it is **j-consistent for all j ≤ k**.

## AC-3 algorithm
An algorithm to enforce arc consistency.

### Pseudocode
```
procedure AC-3(csp)
queue ← all arcs in csp
while queue is not empty do
(X, Y) ← queue.pop()
if REVISE(csp, X, Y) then
if Dₓ is empty then return false
for each Z in neighbors(X) - {Y} do
add (Z, X) to queue
return true
```
#### REVISE(X, Y)
Removes values from Dₓ if **no value** in Dᵧ satisfies the constraint with that value in Dₓ.

#### Complexity
- Time: **O(e × d³)**  
  where `e` = number of arcs, `d` = domain size


## Global Constraints

A **global constraint** captures a common pattern in constraints with known efficient algorithms.

### Example
- `all_different({x₁, x₂, ..., xₙ})`: All values must be different (used in Sudoku, scheduling, etc.)

---

## Forward Checking

When a variable is assigned, **remove** inconsistent values from domains of neighboring unassigned variables.

### Example (N-Queens)
When placing a queen in a column, eliminate conflicting rows in other columns from their domains.

---

## Look-Ahead

Goes **further than forward checking** by checking whether **future variables** still have **possible values** after an assignment.

- May include checking arc consistency after each assignment (e.g., MAC - Maintaining Arc Consistency)

---

[Back to overveiw](Readme.md)
