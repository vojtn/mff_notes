[Back to overveiw](Readme.md)


# Adversarial search and games

## Zero-sum game
games in which the sum of the payoffs is always zero
- Morra

## Adversarial search
Game can be formally defined as a kind of search in a game tree representing all possible moves

## Strategy
Game theory call policy a strategy

### Optimal strategy
Optimal strategy leads to outcomes at least as good as any other strategy when playing with infallible opponent.

## Minimax
Optimal strategy can be determined from the minimax value – utility of being in the corresponding state, assuming that both players play optimally.

The minimax decision – action in the root – calculated using the minimax algorithm
Minimax is based on the idea that:
- The **maximizing player** chooses the move with the highest utility.
- The **minimizing player** (opponent) chooses the move with the lowest utility.

Not practical for real games but serves as basis for more practical algorithms (with cutoff depths and evaluation functions)

## AlphaBeta prunning
Optimization of the minimax algorithm
It is not necessary to look at every node of the game tree to calculate the correct minimax decision, there's no need to explore alternatives that are worse.
Some sub-trees can be pruned as they will never be reached in actual play – a better move is available that will not lead to the sub-tree
Alpha-beta can solve a tree roughly twice as deep as minimax in the same amount of time.

## Evaluation funciton
Returns an estimate of the expected utility of the game from a given position (just as the heuristic function), needed when its not possible to search all the terminal states
Most evaluation functions work by calculating various features of the state.
### Examples (Chess)
Typical features include:
- Material balance (e.g., total value of pieces on the board).
- Positional factors (e.g., control of the center, king safety).

A common approach in chess:
- Assign point values to pieces:
  - Pawn: 1 point
  - Knight/Bishop: 3 points
  - Rook: 5 points
  - Queen: 9 points
- Combine these values to produce an overall score for the board.

### Limitations
- They can suffer from the **horizon effect**: missing consequences of actions that occur just beyond the search depth.

## Stochastic games
IRL can happen some unpredictable events -> random
We add chance nodes to a game tree and calculate expected minimax value
The value of a chance node is calculated as the **expected utility** over all possible outcomes, weighted by their probabilities.

## Single-move games
In **single-move games**, all players choose their actions **simultaneously**, without knowing what the others will do. The outcome of the game depends on the **combination** of all players’ actions.

### Example
**Two-finger Morra**: Both players simultaneously reveal 1 or 2 fingers. The winner is determined based on the sum and declared guesses.


### Notions of strategy
- pure strategy = deterministic policy (single action) - the player always chooses the same action
- mixed strategy = randomized policy that selects actions
according to a probability distribution

### Nash equilibrium
No player benefits by switching strategy, given that every other player sticks with the same strategy

### Pareto dominance
Outcome is Pareto dominated by another outcome if all players would prefer
the other outcome. 

### Pareto optimal
Outcome is Pareto dominated by another outcome if all players would prefer
the other outcome. 

### Prisoners dillemma
two prisoners
has a dominant strategy equilibrium (testify, testify) -> Pareto dominated by outcome (refuse, refuse)

![](/img/prisonersDilemma.png)

### Maximin technique
The **maximin strategy** is a conservative approach:
- Each player chooses the strategy that **maximizes their minimum payoff**.
- Useful when players are highly risk-averse or expect the worst-case scenario.

## Repeated game

A **repeated game** is a game that is played **multiple times** by the same players. Each repetition is called a **round**, and players may adjust their strategies based on the **history** of previous rounds.

### Strategy
#### Perpetual punishment
- Cooperate until the opponent defects once
- Then defect forever as punishment
- Ensures that defectors are punished in future rounds, discouraging selfish behavior

#### Tit-for-tat
- Cooperate on the first move.
- Then repeat the opponent’s previous move.
- Encourages cooperation but punishes defection.
- Simple and surprisingly effective in iterated Prisoner's Dilemma.

## Mechanism design (Inverse game theory)
**Mechanism design** is a field of game theory where the goal is to **design the rules of a game** (the "mechanism") so that when self-interested agents follow their optimal strategies, the **overall outcome is desirable** — often maximizing social welfare or efficiency.

In contrast to traditional game theory (which analyzes given games), mechanism design works **backward**: it starts with a desired outcome and constructs a game that leads to it.

### Auctions
Auction is a mechanism for selling some goods to members of a pool of bidders
- private value
- common value
- bid

#### English auction (ascending-bid)
- start with minimum (reserve) bid bmin
- if some bidder is willing to pay that amount, then ask for bmin + d
- continue until nobody is willing to bid anymore, then the last bidder wins the item, paying the price he bid
It has a simple dominant strategy (bid if price is not greater than vi).
But it can discourage competition, if there is a known strong (rich) bidder.
It has also high communication cost (bidders need to meet or have high-speed secure connection to an auctioneer).

#### Dutch auction (descending-bid)
- start with high price and decrease it until somebody accepts the price
It is fast, hence used to sell fruits, flowers etc.
- Strategy: Bid when price first drops below your valuation.


#### Sealed bid auction
- Each bidder submits one bid privately.
- Highest bidder wins and pays their bid.
- No dominant strategy: requires estimating others' bids.

##### Sealed-bid second-price (Vickrey auction)
- each bidder makes a single bid and communicates it to the auctioneer
- the highest bid wins and pays the price of the second highest bid
The dominant strategy is now simply to bid your **true valuation**.

## Tragedy of commons
The **Tragedy of the Commons** describes a situation in which individuals, acting in their own self-interest, **overuse a shared resource**, ultimately reducing its availability and utility for everyone.

### Real-World Examples
- Overfishing
- Air and water pollution
- Traffic congestion

### Solution
Change the machanism/rules

[Back to overveiw](Readme.md)