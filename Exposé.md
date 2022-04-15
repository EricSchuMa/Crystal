# Title: Utility-Based Multi-Objective RL for changing user preferences under Unknown Pareto fronts applied to TSC
Insight & Assumption: tackling from MORL allows for adaptive system (to changing user preferences)
## I. Introduction



- Sequential Decision Making with multiple goals:
	- The goal of an agent is to maximize expected return.
	- Possibly conflicting objectives, e.g., TSC to minimize latency at intersections while maximizing throughput, autonomous vehicle minimize travel time and fuel cost
- Assumption for multi-objective problem formulation
	- The Problem can not be reduced to a single objective
	- Multiple solutions (trade-offs) are desired, e.g., set of (optimal) trade-offs should be presented to stakeholders

### Context 
- Rising CO2 emissions despite having more efficient cars.
- CO2 and traffic flow are correlated. 
	- Need to optimize multiple (conflicting) metrics at once.
- Fluctuating oil prices through global markets.
- Adopt to changing preferences: e.g., oil prices, ratio of electric vehicles on the road, politics (climate change).
- Decision from trade-off from developer to stake holders (e.g., Policy makers):
	- Present a set of optimal solutions w.r.t. possible trade-offs.

Concerns: Describe challenges, difficulties, ..., changing preferences context, Unknown Pareto front, ..., don't need to explain changing preferences here

### Problem
## Multi-objective is given / Multi-policy is not problem
- MORL efficient / Unknown Pareto front / RL complex
- challenges: how to define the coverage set; how to adapt to plausible changing preferences
- insight: diminishing returns 
 
- Problem Setting (How does the motivated problem fit into the taxonomy of MORL?)
	- Initial decision support & dynamic utility function.
	- Complexity of the modeling approach and policy search:
		- How to produce a convex coverage set (CCS)?
	- How to validate the obtained solution set even if the PF/CCS is unknown?
	
### State-Of-The-Art
- Deep RL scales
- Single & Multi-Policy approaches, i.e., produce sets of solutions
-  
TSC
- Mostly single-objective optimization.
	- (Deep-)RL, Robust Optimization, ...

GAP
- Peel the onion
	- Competing approaches

### Aimed Contributions
- Optimize TSC on CO2 emission and traffic metrics given a set of linear utilities (grid).
	- Produce solution sets.
- Zero-Shot adaptation to dynamically changing objectives.
- Derive a realistic utility-scenario (fair testing).
	- Set of utilities for performance evaluation of the obtained solution sets.
- Identify trade-offs in most widely used traffic metrics and vehicular emission.

**Optionally** 
- Benchmark: *OpenAI* Gym for Multi-Objective TSC.
- Apply approach to MOO benchmark problem.

### Approach
- Linear scalarization: metrics can be converted into monetary cost.
	- (non-linear scalarization introduces additional complexity)
- Multiple-policy approach
	- Allows for zero-shot adaptation to changing user preferences.
- Q-Learning/DQN
	- DQN can handle complex control problems: TSC problem formulated with huge state space.
	- Q & DQN can be adapted to solve MORL problem.
		- **Open Questions**: Which level of complexity is needed to solve the problem? Which level of complexity is optimal w.r.t. obtained (approximate) solution and computational cost?
		- *Hints*: resolution of the state space & spatio-temporal problem -> increased state size
- Evaluation
	- Unknown PF 
		- Utility driven evaluation.
	- Realistic utilities to quantify the "optimality" of obtained solutions.
- Objective Estimation in order to dynamically add and/or remove objectives.

## II. Literature Review
- TSC
	- History
	- Single objective
		- Scalarization techniques
	- Multi-objective
	
- MOO
	- MO-Planning
	- MO-RL

## III. Background
- Traffic Signal Control
- Multi-objective Sequential Decision Making
	- MOMDPs
	- Scenarios
	- Taxonomy
	- Methods
		- Planning
		- Single policy
		- Policy-search
		- Multi-policy
		- Deep-Learning
		- Multi-Agent
	- Evaluation of solution sets
		- Axiomatic evaluation
			- Hypervolume
			- Sparsity
			- Epsilon-Metric
			- Coverage Ratio
		- Utility-based evaluation
			- Expected Utility Metric
			- Maximum Utility Loss

## IV. Plan
- Tasks
- Organization and Schedule (2 week interv