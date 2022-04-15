# Markov Decision Process
A *Markov decision process* *MDP* is given by a five-tuple $(\mathcal{A}, \mathcal{S}, p(\cdot|s,a), \mathcal{R}(s,a,s'), \gamma)$:
- A set of actions $\mathcal{A}$,
- a set of states $\mathcal{S}$,
- a state transition function $p(\cdot|s,a)$,
- a reward function $\mathcal{R}(s,a,s')$,
- and a discount factor for future rewards $\gamma \in [0,1]$.

## Markov Property 
> given the current state $s_t$, the next state $s_{t+1}$ is independent from previous states $(s_0,...,s_{t-1})$.

## Return
Is the immediate reward plus the sum of discounted future rewards
$$R_t = \sum_{k=0}^\inf \gamma^kr_{t+k+1}$$
