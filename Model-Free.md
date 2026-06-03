
                                                        Chapter 3: Model-free Methods

From last chapter, we do analysis about model-based methods: Value iteration, Real-time dyamic Programming and Policy iteration. They do analysis relying 
on explicit world models since we know the value of \(p(s', r \mid s,a)\) from assumption. But lacking explicit world model is often the real case. For this 
chapter, we assume that we only have access to samples from the environment. We will analysis two model-free methods and modifcation for them: Monto Carlo estimation, Temporal 
difference(TD) learning, the combination of former two methods using TD(\(\lambda\)) and Eligibility traces.
