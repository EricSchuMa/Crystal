# On the Generalization of Representations in [[Reinforcement Learning|Reinforcement Learning]]
Establishes a bound on the generalization error arising from specific state representations.

> Generalization behavior of learned representations is well-explained by their effective dimension

## State Representations
Learn simplifications of a state, i.e. *representations*.
- Deal with large problem spaces
- Approximate the value function with few parameters
- Generalize to newly encountered states

## DQN
Use **multiple** layers of **nonlinear transformations** to map inputs to a final layer which is **linearly transformed** into a **value function**.
- Final layer is time-varying state representation

## Effective Dimension
> How many samples are needed to obtain a good generalization of the value function.

## Deep Reinforcement Learning
> How does the effective dimension explain the relative performance of deep RL agents?

- Use effective dimension to measure overfitting
- Reducing the effective dimension might lead to better generalization

## Conclusion
- Left-singular vectors of SRs provide good generalization
- Effective dimension of representations is sensitive to the transition structure
**Question** : Can we explain this in terms of correlations between states? In other words, how do correlations in the state space help to predict the theoretical "generalizability" of a given approach?
- Correlation between effective dimension and performance in Deep-RL
- Generalization is key to explain many performance improvements, 
	- e.g., auxiliary tasks (aux. loss)
	- shape the learned representation of the agent
	
> "Our results also suggest that it may be possible to derive theoretical guarantees regarding transfer between policies or MDPs (Taylor and Stone, 2009)" - Transfer learning for reinforcement learning domains: A survey.