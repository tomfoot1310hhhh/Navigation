
                                                 Chapter 2 Dynamic Programmings
                                                 
Reinforcement Learning can generally be divided into two categories: model-based methods and model-free methods. 

Model-based methods assume that the environment dynamics are known, such as the transition probability function in a Markov Decision Process (MDP), denoted by $P(s' \mid s,a)$. In contrast, model-free methods learn optimal behaviors directly from sampled interactions with the environment without explicitly knowing the transition model.

Dynamic Programming (DP) refers to a class of methods that solve sequential decision-making problems through recursive decomposition into future subproblems, as characterized by the Bellman equations.

In this chapter, we focus on three representative DP-based methods: Value Iteration (VI), Real-Time Dynamic Programming (RTDP), and Policy Iteration (PI). All of these methods are model-based and rely on knowledge of the transition dynamics $P(s' \mid s,a)$.

We begin with Value Iteration. Value Iteration iteratively updates the value function using the Bellman optimality operator, while implicitly deriving a greedy deterministic policy with respect to the current value estimate. With $V_0$ beinging the initial value function estimate, iterations of updating value function(Bellman backup) are as follows:

$V_{k+1}(s)=max_{a}[R(s,a)+\gamma \sum_{s'}p(s'\mid s,a)V_k(s')]$
