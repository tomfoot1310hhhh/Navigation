
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
where we require explicit value for $p_{S}(s'\mid s,a)$. Monto Carlo approximation uses rounds of 

