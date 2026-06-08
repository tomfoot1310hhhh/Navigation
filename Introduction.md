
                                                     Introduction

Reinforcement Learning (RL) is a class of methods for solving sequential decision-making problems. In such settings, an agent interacts with an environment over time and aims to learn a policy that maximizes long-term cumulative rewards.

To describe the RL framework, we introduce several key components: the **agent**，the **environment**, a policy $\mathbf{\pi}$, observations $o_{t}$ and an internal state $z_{t}$.

At each time step, the environment provides an observation $o_{t}$ to the agent. Based on the sequence of past observations and interactions, the agent maintains an internal state $z_{t}$, which serves as its representation or belief about the environment. The policy then maps this internal state to an action:

```math
a_{t}=\pi(z_{t})
```
After executing the action, the agent receives a new observation $o_{t+1}$ and updates its internal state according to a state-update function:

```math
z_{t+1}=\mathbf{SU}(z_{t}, a_{t}, o_{t+1})
```
Intuitively, the internal state $z_{t}$ summarizes the information gathered from previous interactions and provides the agent with a compact representation of its current understanding of the environment. In fully observable settings (MDPs), the internal state often coincides with the environment state itself. In partially observable settings (POMDPs), however, the internal state acts as the agent's best estimate of the hidden environment state.
