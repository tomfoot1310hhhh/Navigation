
                                                        Chapter 3: Model-free Methods

In the previous chapter, we studied several model-based reinforcement learning methods, including Value Iteration, Real-Time Dynamic Programming (RTDP), and Policy Iteration. These methods rely on an explicit world model, since the transition dynamics $p(s',r\mid s,a)$ are assumed to be known.

In practice, however, such a model is often unavailable. Therefore, in this chapter, we assume that the agent only has access to samples collected from the environment. We introduce two model-free methods for value estimation and control: Monte Carlo (MC) estimation and Temporal Difference (TD) learning. We then discuss TD($\lambda$), which combines ideas from both MC and TD, as well as Eligibility Traces, an efficient online implementation of TD(λ).

Starting with Monte Carlo estimation. It modifies the value evaluation of Policy iteration. Instead of solving Bellman equation:
```math
\begin{aligned}
  V(s) = E_{\pi(a\mid s)} \left( R(s,a)+\gamma E_{p_{S}(s'\mid s,a)}\left[V(s')\right] \right)
\end{aligned}
```
where we require explicit value for $p_{S}(s'\mid s,a)$. Monte Carlo approximation uses rounds of trajectories to approximate V_\pi(s). Recall definition of Cumulative discounted reward:
```math
\begin{aligned}
 G_{t}= \sum_{t'=t}^{\infty} \gamma^{t'-t}r_{t'} 
\end{aligned}
```
Monte Carlo is using samples to approximate $V_{\pi}(s)$, it updates the $V(s_t)$ whenever the current trajectory sample walks past $s_t$. 
```math
\begin{aligned}
V(s_t)\leftarrow V(s_t)+\eta [G_t-V(s_t)]
\end{aligned}
```
where s_t denotes the state visited at time step t in the current trajectory. The $\eta$ here could have many choices. We are We could set $\eta$ to be $\dfrac{1}{N(s)}$ where N(s) denotes the total number of visits to state s. We could prove that under such setting is equal to averaging $G_t$. Before that, one important thing about Monte Carlo approximation is that each update must wait for the whole trajectory to be finished since the value of $G_t$ consists of rewards after $t$. 

To show that choosing $\eta_t=\dfrac{1}{t}$ is equivalent to averaging returns, consider an arbitrary state s. Let $G^1,G^2,\ldots,G^{t^\ast}$

denote all observed returns following visits to s. Starting from the last update and recursively expanding the update rule, we obtain:
```math
\begin{aligned}
  V(s)&= \eta G^{t^{*}}+ (1-\eta) V(s)\\
  &= \dfrac{1}{t^{*}}G^{t^{*}}+\dfrac{t^{*}-1}{t^{*}}V(s)\\
  &= \dfrac{1}{t^{*}}G^{t^{*}}+\dfrac{t^{*}-1}{t^{*}}(\dfrac{1}{t^{*}-1}G^{t^{*}-1}+\dfrac{t^{*}-2}{t^{*}-1}V(s))\\
  &= \dfrac{1}{t^{*}}G^{t^{*}}+\dfrac{1}{t^{*}}G^{t^{*}-1}+\dfrac{t^{*}-2}{t^{*}}V(s)\\
  &= \dfrac{1}{t^{*}}\sum_{i=1}^{t^{*}}G^i
\end{aligned}
```



