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