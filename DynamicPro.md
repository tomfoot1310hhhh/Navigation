
                                                 Chapter 2 Dynamic Programmings
                                                 
Reinforcement Learning can generally be divided into two categories: model-based methods and model-free methods. 

Model-based methods assume that the environment dynamics are known, such as the transition probability function in a Markov Decision Process (MDP), denoted by $P(s' \mid s,a)$. In contrast, model-free methods learn optimal behaviors directly from sampled interactions with the environment without explicitly knowing the transition model.

Dynamic Programming (DP) refers to a class of methods that solve sequential decision-making problems through recursive decomposition into future subproblems, as characterized by the Bellman equations.

In this chapter, we focus on three representative DP-based methods: Value Iteration (VI), Real-Time Dynamic Programming (RTDP), and Policy Iteration (PI). All of these methods are model-based and rely on knowledge of the transition dynamics $P(s' \mid s,a)$.

                                                       Value  Iteration    

We begin with Value Iteration. Value Iteration iteratively updates the value function using the Bellman optimality operator, while implicitly deriving a greedy deterministic policy with respect to the current value estimate. The beauty of VI is that it finds the optimal policy via looking for the optimal value function. Just to recap, the definition of V* is that it gives largest value for all states among all policy induced value functions(not all other value functions). This means that some value function(not induced by any policy) might provide larger value for some states comparing with offer from optimal value function. With $V_0$ beinging the initial value function estimate, iterations of updating value function(Bellman backup) are as follows:

```math
V_{k+1}(s) = \max_a \left[R(s,a) + \gamma \sum_{s'} p(s' \mid s,a)V_k(s')\right]
```

The book just stated that we can verify contraction for the Bellman backup, which is shown as follows(important for value iteration and comming Q-learning):

```math
\max_s \left| V_{k+1}(s)-V^*(s) \right|
\leq
\gamma \max_s \left| V_k(s)-V^*(s) \right|
```

Here is the  proofing to this statement:

Denote the Bellman Backup notation by $\mathcal{T}$. We will solve the statement start by proofing：

```math
\left| V_{k+1}(s)-V^*(s) \right|
\leq
\gamma \max_s \left| V_k(s)-V^*(s) \right|
\qquad (1)
```
for any state $s$.

Without loss of generality, set $k$ to be a contant natural number , $s$ to be a specific state, and define $a$ to be

```math
a = \arg\max_{a} \left| \gamma \sum_{s'}p(s'\mid s,a)V_{k}(s')- \gamma \sum_{s'}p(s'\mid s,a)V^{*}(s')\right|
\qquad(2)
```
Hence, we could have:

```math
\begin{aligned}
\left|\mathcal{T}V_k(s)-\mathcal{T}V^*(s)\right|
&= \left|\max_{a1}(R(s,a1) + \gamma \sum_{s^{1}}p(s^{1}\mid s,a1)V_{k}(s^{1}))-\max_{a2}(R(s,a2) + \gamma \sum_{s^{2}}p(s^{2}\mid s,a2)V^{*}(s^{2}))\right|\\
&\leq \left|\gamma \sum_{s'}p(s'\mid s,a) (V_{k}(s')-V^{*}(s'))\right|\\
&= \gamma \left| \sum_{s'}p(s'\mid s,a) (V_{k}(s')-V^{*}(s'))\right|\\
&\leq \gamma \left| \sum_{s'}p(s'\mid s,a) \max_s \left| V_k(s)-V^*(s) \right| \right|\\
&= \gamma \max_s \left| V_k(s)-V^*(s) \right| \left| \sum_{s'}p(s'\mid s,a)\right|\\
&= \gamma \max_s \left| V_k(s)-V^*(s) \right|
\end{aligned}
```
Finished proofing $(1)$. Since the statement works for all states, we have that:
```math
\begin{aligned}
\max_s \left| V_{k+1}(s)-V^*(s) \right|
\leq
\gamma \max_s \left| V_k(s)-V^*(s) \right|
\end{aligned}
```
With linear contraction, each iteration will reduce the maximum value function error. When optimal value function is obtained, we can obatin a greedy policy using:

```math
\begin{aligned}
\pi^{*}(s) = \arg\max_{a}\left[R(s,a)+ \gamma E_{p_{S}(s'\mid s,a)}[V^{*}(s')]\right]
\end{aligned}
```

We can see that the greedy policy is one of the policies that induced the optimal value function. I think that one beauty is that for VI is that it searches policy via finding a fix point for Bellman equation.

                                                 Real Time Dynamic Programming
                                                 
RTDP is a trajectory-focused asynchronous variant of Value Iteration that concentrates computation on reachable states. For VI, we need update the value of all states every iteration which requires a lot computation. In order to counter this, RTDP is a method focused on updating the value along a trajectory. RTDP is operating under a episodic MDP. Here is an introduction about episodic MDPs: An episodic MDP is an MDP in which interactions terminate after a finite trajectory. Take a short path problem for example, the interaction is that when the agent reaches a goal state $s*$, then the MDP will set:
```math
\begin{aligned}
  P(s*\mid s*, a)= 1
\end{aligned}
```
for all actions $a$s. Meaning that it reaches absorbing state. There could be other forms of interaction like reaching $T$ iteraion. When it reaches a state $s$, it performs Bellman backup to that specific state: $V(s)\leftarrow \max_{a}E_{p_{S}(s'\mid s,a)}[R(s,a)+\gamma V(s')]$ , then it pick an action $a$(could be with some exploration like epsilon-greedy action) to real next state and the iteration carries on. In summary, RTDP is like a more general version of VI(e.g. asynchronous value iteration). It is more suitable for sparse reachable region(will look on this later). However, unlike standard Value Iteration, RTDP does not always inherit the straightforward global contraction guarantee due to its partial state updates.

                                                        Policy Iteration

Policy Iteration (PI) is an iterative dynamic programming method that often converges in fewer iterations than Value Iteration (VI). It consists of two parts: policy evaluationa and policy improvement. 
For policy evaluation, we evaluate current policy by calculating its value function. The policy assumption here says that we are only considering deterministic policies which aligns with VI. By recalling Bellman's equation:

```math
\begin{aligned}
  V(s) = E_{\pi(a\mid s)} \left( R(s,a)+\gamma E_{p_{S}(s'\mid s,a)}\left[V(s')\right] \right)
\end{aligned}
```
We could represent this with:
```math
\begin{aligned}
  \mathbf{v} = \mathbf{r}+ \gamma \mathbf{T}\mathbf{v} 
\end{aligned}
```
for all states with $\mathbf{v(s)}:= V_{\pi}(s)$, $\mathbf{r}(s)=\sum_{a}\pi(a\mid s)R(s,a)$(reward vector) and $\mathbf{T}(s'\mid s)= \sum_{a}\pi(a\mid s)p(s'\mid s,a)$(state transition matrix). Here are details why it could be shown in this way. Without loss of generality, we pick arbitrary state $s$, we have:
```math
\begin{aligned}
\mathbf{v}(s)&=V_{\pi}(s)\\
&= E_{\pi(a\mid s)} \left( R(s,a)+\gamma E_{p_{S}(s'\mid s,a)}\left[V^{*}(s')\right] \right)\\
&= \mathbf{r}(s) + \gamma E_{\pi(a\mid s)}\left(E_{T(s'\mid s,a)}[V(s')]\right)\\
&= \mathbf{r}(s) + \gamma \sum_{a}\sum_{s'} \pi(a\mid s)p(s'\mid s,a)v(s')\\
&= \mathbf{r}(s) + \gamma \sum_{s'}\left(\sum_{a}\sum_{s'} \left(\pi(a\mid s)p(s'\mid s,a)\right)v(s')\right)\\
&= \mathbf{r}(s) + \gamma \mathbf{T}(s,:)\mathbf{v}(s)
\end{aligned}
```
Since the transition probabilities and rewards are known in a model-based MDP, policy evaluation reduces to solving a linear system with |S| unknown variables. For each policy, we could either solve this linear system of equations by $\mathbf{v}=(\mathbf{I}-\gamma \mathbf{T})^{-1}\mathbf{r}$ or via value update each iteration $\mathbf{v}_{t+1} = \mathbf{r} + \gamma \mathbf{T}\mathbf{v}_t$ or using asynchronous variant. So choosing one of these involve the tradeoff between three philosophy: exact solution vs iterative global approximation vs local asynchronous approximation. We will go back and talk about this during comparison in experiments.

After evaluation is completed, we then move on to Policy Improvement. We derive better policy $\pi'$ that acts greedyily with respect to $V_{\pi}$ for any state. The deterministic policy $\pi'$ is defined as:
```math
\begin{aligned}
\pi'(s) = \arg\max_{a}{R(s,a)+ \gamma E[V_{\pi}(s')]}
\end{aligned}
```
By denoting $a'= \pi(s)$ for arbitrary picked state $s$, we can have that:
```math
\begin{aligned}
V_{\pi'}(s) = \arg\max_{a}{R(s,a)+\gamma E[V_{\pi}(s')]} \geq R(s,a') +\gamma E[V_{\pi}(s')]
\end{aligned}
```
Hence, we have that $V_{\pi'}\geq V_{\pi}$. The intuition for Policy Improvement is that the inducing policy just satisfies the Bellman equation, not the Bellman optimal equations. It means that there could be better policies for the induced value function comparing with the inducing policy.  

