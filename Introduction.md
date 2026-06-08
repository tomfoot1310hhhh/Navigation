
                                                     Introduction

Reinforcement Learning (RL) is a class of methods for solving sequential decision-making problems. In such settings, an agent interacts with an environment over time and aims to learn a policy that maximizes long-term cumulative rewards.

To describe the RL framework, we introduce several key components: the **agent**， the **environment**, a policy $\mathbf{\pi}$, observations $o_{t}$ and an internal state $z_{t}$.

At each time step, the environment provides an observation $o_{t}$ to the agent. Based on the sequence of past observations and interactions, the agent maintains an internal state $z_{t}$, which serves as its representation or belief about the environment. The policy then maps this internal state to an action:


