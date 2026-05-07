                                                      Chapter 1 Bellman Equartion
Starting with Value Functions, we first need metrices to compare policies. State-value functions and state-action functions given under policy \pi 
map state and action to metric space defined as reward. The functions mean the expected return obtained if we start in state s and follow \pi to choose
actions in continuing task and expected return obtained if we start by taking action a in state s, and then follow \pi to choose actions thereafter.
The introduction of the two functions brought advantage function,meaning the benefits of taking action a at state s and then follow policy \pi, relative
to follow \pi to choose actions thereafter.

Recall that we are working under the framework of a Markov Decision Process (MDP). It is important to emphasize that an MDP itself is not a method for finding 
the optimal policy. Instead, it provides the mathematical framework and environment in which policy optimization is performed. An MDP consists of states, actions, 
transition dynamics, rewards, a discount factor, and the Markov assumption. Under this framework, reinforcement learning algorithms aim to find an optimal policy that maximizes the expected return. 

With value functions defined, we can now move on to improving the policy. With 

