                                                      Chapter 1 Bellman Equartion
Starting with Value Functions, we first need metrices to compare policies. State-value functions and state-action functions given under policy \pi 
map state and action to metric space defined as reward. The functions mean the expected return obtained if we start in state s and follow \pi to choose
actions in continuing task and expected return obtained if we start by taking action a in state s, and then follow \pi to choose actions thereafter.
The introduction of the two functions brought advantage function,meaning the benefits of taking action a at state s and then follow policy \pi, relative
to follow \pi to choose actions thereafter.

Recall that we are working under the framework of a Markov Decision Process (MDP). It is important to emphasize that an MDP itself is not a method for finding 
the optimal policy. Instead, it provides the mathematical framework and environment in which policy optimization is performed. An MDP consists of states, actions, 
transition dynamics, rewards, a discount factor, and the Markov assumption. Under this framework, reinforcement learning algorithms aim to find an optimal policy that maximizes the expected return. (i.e. we could use dynamic programming to find the optimal solution)

With value functions defined, we can now move on to improving the policy. A policy is optimal when it gives greatest state value for all states. Optimal policies are not unique under MDP. The value functions between optimal policies give idential values to same states or states plus actions.
The two functions are called optimal-state functiona (V*) and optimal action-value function(Q*), respectively. The equations could be referred from course book. The way why V*(s) is set up in that form is because under MDP assumption, the futrhest state we could refer to is state next to current state. Here are understanding about Bellman's optimality equations(2.4 & 2.5). Starting from a confusion coming out of (2.5). I beleive that max_{a'}Q*(s',a') could be represented as V*(s'), why don't just use this representation, shouldn't it make it simplier? After some thinking, maybe 
it is because we want to calculate Q* purly via rewards and Q* itself, meaning that Q learning just needs Q*. The second possible reason is that Bellman's optimality equations are to be greedy, maxmizing on Q* aligns with that idea. Third is to align with V*(V learning). The construction of the Bellman's optimality equations refer strictly to MDP, using one step to the future to make it easy to calculate plus using the assumption that Markov just connects one step future with current state.  

