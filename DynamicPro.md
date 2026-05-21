
                                                 Chapter 2 Dynamic Programmings
                                                 
Renforcement Learning could mainly consist of two forms, model-based ones and model-free ones. Model-based means that the enivronment of the problem is known(e.g. the transition probability for MDP for the problem). The definition of Dynamic Programmings is to solve the problem by referring to future subproblems(e.g. Bellman recursive equation). For this chapter, we will focus on three representative methods: Value Iteration method, Real-time Value Iteration and Policy Iteration. All of these methods are model-based, depending on $P(s'|s, a)$.
Starting with Value Iteration. It is a method consisting of iterations of evaluation on states and a greedy deterministic policy to maximize value for all states.
