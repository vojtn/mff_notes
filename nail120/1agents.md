[Back to overveiw](Readme.md)

# Agents
## Agent
An **agent** is anything that can:
- **Perceive** its environment through sensors.
- **Act** upon that environment through actuators.

### Examples:
- A robot perceives its surroundings with cameras (sensors) and moves using motors (actuators).
- A software agent observes data (e.g., stock prices) and executes trades (actions).
![](/img/agent.png)

## Rational agent
A **rational agent** selects actions that are expected to **maximize its performance measure**, based on:
- Its percept history
- Its knowledge of the environment
- The actions available
![](/img/rationalAgent.png)

## Environment
### Partially/Partially Observable
**Fully Observable**: The agent's sensors have access to the **entire state** of the environment at each point in time.
  - Example: A chessboard, if all pieces are visible.
- **Partially Observable**: The agent can only see part of the state.
  - Example: A self-driving car cannot fully observe what’s behind buildings.


### Deterministic/Stochastic
- **Deterministic**: The **next state** of the environment is completely determined by the current state and the agent’s action.
  - Example: A mathematical puzzle or tic-tac-toe.
- **Stochastic**: The next state includes **randomness** or uncertainty.
  - Example: Rolling dice in a game or dealing cards.

### Episodic/Sequential
- **Episodic**: The agent’s experience is divided into **discrete episodes**, and decisions in one episode do **not affect future ones**.
  - Example: Image classification tasks.
- **Sequential**: The current decision can **affect all future decisions**.
  - Example: Playing chess or driving a taxi — earlier actions influence future possibilities.

Sequential environments require **planning** and **memory**; episodic ones do not.

### Static/Dynamic
- A **static environment** does **not change** while the agent is deliberating.
- A **dynamic environment** can **change** during the agent's thinking or decision-making process.
- A **semidynamic environment** doesn’t change itself, but the agent’s **performance measure may degrade** over time (e.g., time pressure).

#### Examples:
- **Taxi driving** → Dynamic: other cars, pedestrians, and traffic lights keep changing.
- **Chess with a clock** → Semidynamic: the board doesn't change, but the clock is ticking.
- **Crossword puzzle** → Static: the puzzle stays the same while you think.

### Discrete/Continuos
This distinction can apply to:
- The **state** of the environment
- The **time** model (discrete steps vs. continuous flow)
- The **agent's percepts** and **actions**

| Property        | Discrete Example   | Continuous Example        |
|----------------|--------------------|---------------------------|
| State Space     | Chess board        | Taxi location/speed       |
| Time            | Turn-based games   | Real-time driving         |
| Actions         | Chess moves        | Steering, acceleration    |
| Percepts        | Symbolic input     | Camera input (treated as continuous) |

- **Chess**: Discrete states, time, actions, and percepts.
- **Taxi driving**: Continuous across all aspects — real-world physical processes.


### Single-Agent/Multi-Agent

- **Single-agent environment**: The agent is the **only decision-maker**; the environment may be passive.
  - Example: Solving a puzzle, vacuum cleaning.

- **Multi-agent environment**: Multiple agents interact; outcomes depend on **inter-agent dynamics**.
  - Can be **competitive**, **cooperative**, or a mix.

#### Types of Multi-Agent Scenarios
- **Competitive**: One agent’s gain is another’s loss (zero-sum).
  - Example: Chess, poker, bidding in auctions.
- **Cooperative**: Agents work together toward a shared goal.
  - Example: Team-based robotics, distributed problem solving.


## Structure of agents
### Reflex agent
- Selects actions based solely on the **current percept**.
- Does **not** consider the history or future consequences.
- Simple but often short-sighted.

**Example:** A basic thermostat that turns on heat when temperature < 20°C.

### Goal-based agent
Agents can be more flexible if they assume goal (desirable states) in addition to the current state
- Considers desirable future states (goals) in addition to the current percept.
- Can evaluate and choose actions that help achieve goals.
- More flexible and capable than reflex agents.


![](/img/StructureOfAgents.png)

## Representations of states
### Atomic
- state is indivisible (no internal structure, blackbox)
- used in search
### Factored
- state is a vector of values (properties ofthe world)
- used in constraint satisfaction, propositional logic, planning
### Structured
- state is a set of objects (with own attributes) connected via various relations
- used in first-order logic

![](/img/RepresentationOfStates.png)


[Back to overveiw](Readme.md)
