# Multi-Objective TSC

### Multi-Objective Reinforcement Learning for Traffic Signal Control in Face of Unknown Pareto Fronts

### Possible solutions:  
- Simplifying the scenario until it is feasible to solve it exactly
	- apply tabular methods
	- reduce the number of model parameters drastically

- Find a systematic way of (approximately) solving the large scale problem directly
	- Deep Learning


#### Few Policy Parameters
- Easy to cover large parts of the policy space
	- Good approximation of the [[Optimization#Pareto Optimality|Pareto]] front
	- Choosing a policy that is close to the Pareto front/lies on the Pareto front
	- Policy might be "too simple" to solve the problem

#### Deep Policies (a lot of parameters)
- Grid Search of the policy space is not possible --> Deep Learning to obtain "good" candidates
- sparse exploration of the policy space
- Policies can be better than "simple" policies but obtaining the right set for the MOO problem is harder

#### Q1: How many parameters are enough to solve the problem "good engough"
#### Q2: How many parameters are too much to obtain "good" approximations of the pareto front


#### Hierarchical models
e.g.  Module estimates Time T and Reward R 
- meta policy selects the policy
- Exact Solution to a "game" $\neq$  reality we can not find the exact solution
	- Strategies to search for solutions --> Deep Learning / good enough solutions
	- Robustness: "weak learners"

#### Why do we need exact solutions?
- Robustness? --> Risk?



