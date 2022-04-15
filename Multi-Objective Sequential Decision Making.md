# Multiple-Objective Sequential Decision Making
## Motivation
- Can not reduce multiple objectives to a single objective

> All research on MOMDPs rests on the premise that there exist tasks for which the conversion to a single-objective task is impossible, infeasible, or undesirable.
 
# Multi-Objective Markov Decision Process
A Multi-Objective [[Sequential Decision Making#Markov Decision Process|Markov Decision Process]] **(MOMDP)** is a formalization used for [[Multi-Objective Sequential Decision Making#Multiple-Objective Sequential Decision Making|Multiple-Objective Sequential Decision Making]].
## MOMDP
A *multi-objective* MDP is an MDP in which the reward function $R:S \times A \times S \rightarrow R^n$  describes a vector of $n$ rewards (one for each objective).

## Multi-Objective value function
Using the definition of a *MOMDP* we can define a (multiobjective-) value vector:
$$V^\pi(s)=E[\sum_{k=0}^\inf \gamma^kr_{t+k+1}|\pi,s_t=s]$$
**Ordering:** for multi-objective value functions there only exists partial ordering. Therefore, an optimal state value can not be determined without additional information. Hence, we can not determine an optimal stationary policy anymore -> This additional information can be provided by a [[Scalarization]] function.

## Scenarios for MOMDPs
![[ScenariosForMOMDPs.png]]

**Why do we need a set of policies?**
- Expressing trade-offs in weights $w$ might be unnatural to the user: rather choose from a set of alternatives (*decision analysis*)
- Trade-offs might change
- Trade-offs might not be known beforehand

> Rather than specifying $w$, "prune" solutions that would not be optimal w.r.t. any $w$. Then offer the user a range of alternatives from which they can select according to their preferences.

### Unknown weight scenario
- Weights for the scalarization function are unknown at planning or learning time.
Example:
 - Public transport system that aims to minimize both latency and pollution costs
 - MOMDP can be scalarized by converting each objective into monetary cost
	 - Economists can compute the cost of lost productivity due to commuting 
	 - Pollution incurs a tax that must be paid in pollution credits purchased at a given price
	 - Assume that credits are traded on an open market and therefore the price constantly fluctuates
	 - If the transport system is complex, it may be infeasible to compute a new plan every day given the latest prices 
-> In such a scenario, it can be preferable to use a multi-objective planning method that computes a set of policies such that, for any price, one of those policies is optimal.

Computing a set of policies needs to be done only once, followed by a *selection phase* and finally an *execution phase*, i.e., deployment.

### Decision Support Scenario
Scalarization is infeasible throughout the entire decision process.
- The user may have "fuzzy" preferences, e.g., a designer can't quantify the loss w.r.t to an obstructed view.
- MOMDP method can help to calculate an optimal solution set w.r.t. the known constraints $f$ and weights $w$.

### Interactive Decision Support Scenario
- Agent has to learn about the preferences of the user and the environment.
- Learns about the user's utility function.
- Parts of the utility might be known.

Example: A user is presented with solutions and ranks them and gives feedback. Thereafter, the agent incorporates this feedback into its representation of the users preferences.

### Dynamic Weights Scenario
- Weights change over time
	- Choose from solution set.
	- Retrain the Agent.

Example: Restaurant choice with and without time limitations (see Time Adaptive RL paper).

### Known Weights Scenario
Weights are known beforehand but scalarization is difficult or the scalarized problem is difficult to solve.
- if $f$ is nonlinear, the resulting single-objective MDP has non additive returns
	- Non-stationary MDP.
	- Stochastic MDP.
	- Converting to MDP with additive returns might blow up state space -> intractable problem

Therefore, if the scalarization is possible but may not be preferable, use methods designed for MOMDPs.

### On-Line vs. Off-line
- Dynamic weights
	- Agent must have seen the weights beforehand to do well.

## Taxonomy
Group approaches according to **underlying assumptions** and **resulting solutions**.
Q: What constitutes an optimal solution? -> Depends on problem taxonomy.

![[taxonomyMOO.png]]

### Utility-based approach
Before the execution process, collapse the value vector to a scalar *utility*
- Using a scalarization function
- Scalarization can be implicit or hidden, e.g. if a user's thought-process is involved
- Find optimal solution to each possible weight setting of the scalarization function
-> MOMDP is solved
- Optimal solution from a set of solutions by 
	- Assumptions about the scalarization function
	- Allowed policies (defined by user)
	- One or multiple policies?

	**In contrast:** Axiomatic approach - optimal solution is the [[Optimization#Pareto Optimality|Pareto front]].

## Optimal Solutions
### Solution Sets
1) Undominated set $U(\Pi)$: the set of policies for which there exist no policy that dominates it
2) Coverage set $CS(\Pi)$: for every possible scal. function there exists an optimal policy in the set. 
3) Pareto front $PF(\Pi)$: if the utility function can be any monotonically increasing function, then the Pareto Front is the undominated set. 

One can also define a *Pareto Coverage Set* (PCS), only retaining one of multiple policies with the same  value vector.

**Convex Hull** for linear utility functions
![[ConvexHull.png]]


## Methods
### Multi-objective planning
- Extend value iteration (Bellman) to convex hull of solutions
- Minimize distance of reward vector and reference point in objective space

### [[Multi-Armed Bandits|Bandit algorithms]]
- Multi-Objective regret
- Extensions to UCB1 
	- Chebyshev scalarization
	- Version based on Pareto dominance
- Extending the contextual bandit to MORL

### Single-Policy
- Extend model-free value-based methods to multiple objectives
- Store values as vectors
- **[[Scalarization||Scalarization]]** / utility function to determine $\epsilon$-greedy action to perform
- Linear scalarization transforms MOMDP to MDP and convergence theorems do apply
- Nonlinear scalarization: utility might be non-linear. 
	- Violates Bellman equation because of non-additive returns -> condition Q-values with *augmented state* (concatenating state with summed previous rewards)

#### Policy-Search
- Can directly optimize with regards to any (non-linear) utility function 
	- ESR criterion must be optimized efficiently
		- Mone Carlo (EUPG) ; see Roijers et al. 2018
		- Distributional Monte Carlo Tree Search (DMCTS) Hayes et al. 2021
- Can produce stochastic policies

### Multi-Policy
- Outer loop: operate on series of single-objective problems
	- Iterate through series of different parameter settings for a utility function
		- re-run a single-policy MORL method for each setting
	- Improve efficiency by: (1) using information from earlier runs; (2) adaptive search methods through the parameter space to reduce iterations of the outer loop.
- Inner loop: directly produce multiple policies
	- Pareto-Q-Learning: modify Q-learning to store multiple Pareto-optimal values for each state-action pair
		- pruning of dominated policies
	- Multi-Objective Fitted Q-Iteration (MOFQI)
		- learns an approximation of the optimal Q-function for all combinations of the scalarization weights
	- Monte Carlo Tree Search

#### Model-based
- once env. has been learned -> derive optimal policy for any utility without further interaction

### Scaling up to high-dimensional states
- Use Deep RL methods to scale (similarly to single-objective RL)
	- SARSA
	- DQN: output layer has $|\mathcal{A}|\times n$ nodes, with $\mathcal{A}$ action space and $n$ objectives.
		- reuse network weights from previous runs for similar policies ($w' \sim w$)
	- Use single-policy that generalizes across user preferences
		- Use diverse experience replay to reduce bias from previous preferences

### Multi-agent algorithms
Each agent can represent one or more distinct users, i.e., each agent can have a different utility function.
![[MOMADM-Taxonomy.png]]

- Agent's strategies are interrelated
- *solution concepts* - whether the agents in the system reach outcomes that are of interest - can be used to evaluate the algorithm's performance

#### Coverage sets
- fully cooperative scenario: team reward / team utility: e.g., through Multi-objective coordination graphs
	- multi-agent systems reward can be factorized into smaller components
- Cooperative multi-objective stochastic game to derive approximate coverage sets
