
                                                        Chapter 3: Model-free Methods

From last chapter, we do analysis about model-based methods: Value iteration, Real-time dyamic Programming and Policy iteration. They do analysis relying 
on explicit world models since we know the value of $p(s', r \mid s,a)$ from assumption. But lacking explicit world model is often the real case. For this 
chapter, we assume that we only have access to samples from the environment. We will analysis two model-free methods and modifcation for them: Monto Carlo estimation, Temporal 
difference(TD) learning, the combination of former two methods using TD(\(\lambda\)) and Eligibility traces. 


Starting with Monto Carlo estimation. It modifies the value evaluation of Policy iteration. Instead of solving Bellman equation:
```math
\begin{aligned}
  V(s) = E_{\pi(a\mid s)} \left( R(s,a)+\gamma E_{p_{S}(s'\mid s,a)}\left[V(s')\right] \right)
\end{aligned}
```
where we require explicit value for $p_{S}(s'\mid s,a)$. Monto Carlo approximation uses rounds of trajectories to approximate $V(S)$. Recall definition of Cumulative discounted reward:
```math
\begin{aligned}
 G_{t}= \sum_{t'=t}^{\infty} \gamma^{t'-t}r_{t'} 
\end{aligned}
```
Monto Carlo is using samples to approximate $V_{\pi}(s)$, it updates the $V(s_t)$ whenever the current trajectory sample walks past $s_t$. 
```math
\begin{aligned}
V(s_t)\leftarrow V(s_t)+\eta [G_t-V(s_t)]
\end{aligned}
```
where $s_t$ means the $t$th state current trajectory passes. The $\eta$ here could have many choices. We are We could set $\eta$ to be $\dfrac{1}{N(s)}$ where $N(s)$ stands for number that existing trajectories pass $s$ in total. We could prove that under such setting is equal to averaging $G_t$. Before that, one important thing about Monto Carlo approximation is that each update must wait for the whole trajectory to be finished since the value of $G_t$ consists of rewards after $t$. 

Here is a brief proof for Monto Carlo approximation when we have $\eta = \dfrac{1}{N(s)}$. Without loss of generality, let us pick $t^{*}$ that makes $\eta^{t}$ small enough and arbitiary picked state $s$. We consider that in  the Using recursion, we have:
```math
\begin{aligned}
  V(s)= 
\end{aligned}
```



