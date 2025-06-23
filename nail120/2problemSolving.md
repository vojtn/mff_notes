[Back to overveiw](Readme.md)


# Problem solving

## Well-defined problem
- **Initial state**: The starting point of the problem.
- **Transition model**: A function that describes the result of performing an action in a given state:  
  `(state, action) → new_state`
- **Goal test**: A function that determines whether a given state is a goal state.

## Solution of the problem
Sequence of actions that leads from the initial state to a goal state
- The **quality** of a solution is measured by the **path cost**.
- An **optimal solution** is one that has the **lowest total path cost** among all possible solutions.

## Search
Search is the process of exploring the state space to find a solution.

### General structure of a search algorithm
1. root node to frontier (open list)
2. select node from fontier (using some search strategy)
3. expand the node (add successor states to the frontier)
4. repeat until goal is found or frontier is empty

### Tree search
**Does not remember previously visited states**.
- Can explore redundant paths (repeats a state at
different nodes)

### Graph search
- added data structure (explored set or closed list) to remember expanded node
- Avoids expanding the same state more than once.
- **More efficient** than tree search, especially in large or cyclic state spaces.

## Node selection strategies
The choice of which node to expand next (i.e. node selection strategy) defines the behavior of a search algorithm.

### Uninformed search strategies
#### Breadth-First Search
- Expands the **shallowest unexpanded node** first (FIFO queue).
- Explores all nodes at depth `d` before moving to depth `d+1`.

**Properties:**
- **Complete**: Will always find a solution if one exists.
- **Optimal**: Finds the **shortest path** if all step costs are equal.
- **Time complexity**: `O(b^d)`
- **Space complexity**: `O(b^d)`


#### Depth-First Search (DFS)
- Expands the **deepest unexpanded node** first (LIFO stack).
- May go deep down one path before exploring others.
**Properties:**
- **Complete**:
  - ✅ Yes, for **graph search** (if cycles are avoided).
  - ❌ No, for **tree search** (may get stuck in infinite branches).
- **Not optimal**
- **Time complexity**: `O(b^m)`
- **Space complexity**: `O(bm)`

![](/img/BFS-DFS.png)

#### Uniform-cost search (Dijkstra)
- A cost-aware extension of BFS.
- Expands the node with the **lowest total path cost** `g(n)`.
- Uses a **priority queue** ordered by `g(n)` (path cost so far).

**Properties:**
- **Complete**
- **Optimal**, even when step costs vary
- **Time complexity**: `O(b^{1 + ⌊C*/ε⌋})`

### Informed search
#### Best-first search
Expands the node with the lowest evaluation function f(n)

##### Evaluation function f(n)
- Determines the order of node expansion.
- Represents the estimated cost of the solution through node `n`.
- In Uniform-Cost Search: `f(n) = g(n)`  
- In A*: `f(n) = g(n) + h(n)`

##### Heuristic function h(n)
- Estimates the **cost of the cheapest path** from node `n` to a goal.
- Should be **problem-specific**.
- Used to guide the search more intelligently.

#### Greedy best-first search
- Expands the node that appears **closest to the goal**:
  `f(n) = h(n)`

**Properties:**
- Not complete (may get stuck in loops or dead ends)
- Not optimal
- Typically faster than uninformed methods but less reliable

### Admissible heuristic
- h(n) <= ”the cost of the cheapest path from n to goal”
- an optimistic view (the algorithm assumes a better cost than the real cost)

### Monotonous heuristic
let n‘ be a successor of n via action a and c(n,a,n‘) be the transition cost
- h(n) <= c(n,a,n‘) + h(n‘)
- this is a form of triangle inequality

#### A* search
expands the node with the **lowest total estimated cost**: f(n) = g(n) + h(n)

Where:
- `g(n)` is the cost to reach node `n` from the start node.
- `h(n)` is the heuristic estimate of the cheapest cost from `n` to the goal.
- `f(n)` is the estimated cost of the cheapest solution through node `n`.

**Properties:**
- ✅ **Complete** (if step costs are ≥ some small positive constant ε)
- ✅ **Optimal** (with admissible `h(n)` in tree search, and consistent `h(n)` in graph search)
- ✅ **Efficient**, especially with a good heuristic

### Proves

#### Monotonous heuristic is admissible


#### admissible heuristic h(n) -> A* in Tree Search is optimal

#### monotonous heuristic h(n) -> A* in Graph Search is optimal

[Back to overveiw](Readme.md)
