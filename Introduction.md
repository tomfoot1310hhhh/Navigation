
                                                     Introduction

RL means a class of methods for solving various kinds of sequential decision making tasks. In such tasks, (want to go back to this part when I finish all the parts for better accuracy)

Just decribe it in short for now, we have agent, environment, policy $\pi$, observation $o_{t}$, internal state $z_{t}$. The relationship between these terms is that internal state $z_{t}$ is like understanding of the agent based on knowledge of observation obtained from environment , agent's long term of understanding of the past process:$z_t$ and agent's current action $a_{t}=\pi(z_t)$. The state-update function could be expressed in this ways:$z_{t+1}= SU(z_t, a_t, o_{t+1})$.
