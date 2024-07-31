# Reinforcement Learning

- *Reinforcement learning* is a technique to teach an algorithm how to perform a task by rewarding it when it does well and penalizing it when it does badly.
- Some applications include controlling robots, stock trading, and video games.

## Mars Rover Example

- State: Position of the rover.
- Terminal State: Nothing happens after reaching this state.
- We can assign rewards to the state that we would like to rover to be at.

### Notation

- $S$ - The current state.
- $a$ - The action to be taken.
- $R(S)$ - The reward associated with the current state.
- $S'$ - The new state after action is taken.

## The Return in Reinforcement Learning

- The *return* allows the algorithm to understand which rewards are better to go for - it weighs between short term and less valuable rewards vs long term but more valuable rewards.
- The return therefore calculates the sum of rewards for each state up until the terminal state, weighted by the *discount factor* $\gamma$, where:

    $\text{return} = R_1 + \gamma R_2 + \gamma^2 R_3 + ...$.

- This also encourages reinforcement learning algorithms to push negative rewards as far in the future as possible, because $\gamma^n$ makes a negative number small as $n$ becomes large.

## Making Decisions: Policies in Reinforcement Learning

- A policy $\pi(s)$, is a function which maps the current state $s$ to the action $a$ to take.
- Thus, the goal of reinforcement learning is to find a policy which maximizes the return (i.e. the reward).
- The *Markov Decision Process (MDP)* is the process of reinforcement learning previously described - the iterative cycle of making an action based on the current state, $\pi(s) = a$, and observing the reward $R$ and the new state $S'$.
  - *Markov* means that only the current state matters, and how we got to the current state is irrelevant.

## State-Value Action Function

- The *state-value action function* $Q(s, a)$, defines the best return value you can get after making action $a$ at state $s$.
- Thus, the best possible action from any state $s$ is the one that maximizes the state-value action function, $\text{max}_{a}Q(S, a)$
- If we can compute $Q(S, a)$ for every state, we have a good way of determining the policy $\pi(s)$ because we will know what is the best action to take.

## Bellman Equation

- The *Bellman Equation* defines a recursive relation to calculate the optimal return at state $s$ and taking action $a$.

$$Q(s, a) = R(s) + \gamma \text{ max}_{a'} Q(s', a')$$

### Bellman Equation Notation

- $s$ - Current state.
- $a$ - Current action.
- $s'$ - State after taking action $a$.
- $a'$ - Action taken in state $s'$.
- $R(s)$ - Reward at state $s$.
- $Q(s, a)$ - The return value if you take action $a$ at state $s$ and continue optimally after that.

## Random (Stochastic) Environment

- **Context**: In a *stochastic environment*, due to randomness, there is a chance that our algorithm doesn't perform the action we want it to take.
- Because of this, the return is now probabilistic, which means we would be trying to maximize the *average* or *expected value* of the return.
  - E.g. Given that we are in state `3` (table below) and we want to move left, in a stochastic environment, there could be a `0.9` chance of moving left and a `0.1` chance of moving right.
  - If our algorithm is trying to move to state `0`, one path it could take is: 3 → 2 → 1 → 2 → 1 → 0.
  - Another path could be: 3 → 2 → 1 → 0.
  - As a result, the return would be different for different paths, which is why our return value is now probabilistic.

  | Reward | 100 | 0 | 0 | 0 | 0 | 40 |
  |--------|-----|---|---|---|---|----|
  | State  | 0   | 1 | 2 | 3 | 4 | 5  |

- Hence, our $\text{Expected Return} = \text{Average}(R_1 + \gamma R_2 + \gamma^2 + R_3 + ...)$.
- The revised goal of reinforcement learning in a stochastic environment would be to choose a *policy* $\pi$ which maximizes the *expected* return.
- The Bellman Equation revised has the current reward $R(s)$ plus the expected value of the future return:

$$Q(s, a) = R(s) + \gamma E[\text{max}_{a'} Q(s', a')]$$

## Continuous State Spaces

- Typically, state is not just a set of discrete values, but a *continuous* state of values.
  - E.g. If the mars rover can move between states 1 to 6, a continuous state would mean it could take on non-discrete values like 2.7, etc.
- Therefore, it is useful to represent state as a vector.
  - E.g. The state of a moving truck can be represented as a vector containing information about its x-position, y-position, orientation, x-velocity, y-velocity, and angular velocity: $<x, y, \theta, \dot{x}, \dot{y}, \dot{\theta}>$

## Reinforcement Learning Problem Example: Lunar Lander

- In this problem, the goal of reinforcement learning is to simulate the landing of a lunar lander. This is done by taking actions over time.

### Lunar Lander Actions

- Do Nothing
- Fire Left Thruster
- Fire Right Thruster
- Fire Main Thruster

### Lunar Lander State Space

$<x, y, \dot{x}, \dot{y}, \theta, \dot{\theta}, l, r>$

- $x$ - Horizontal Position
- $y$ - Vertical Position
- $\dot{x}$ - Horizontal Velocity
- $\dot{y}$ - Vertical Velocity
- $\theta$ - Angle of Tilt
- $\dot{\theta}$ - Angular Velocity
- $l$ - Left Leg Touching Ground? (0 or 1)
- $r$ - Right Leg Touching Ground? (0 or 1)

### Lunar Lander Reward Function

- Getting to landing pad: 100 to 140
- Additional reward for moving toward / away from pad.
- Crash: -100
- Soft landing: +100
- Leg grounded: +10
- Fire main engine: -0.3
- Fire side thruster: -0.03
