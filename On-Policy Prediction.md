# On-Policy Prediction
Want to find some weights for a given  that accurately approximate the true value function.

## Mean-Squared Value Error Objective
- Difference between prediction and true value through Mean Squared Error
$$\overline{VE}=\sum_s \mu(s)[v_\pi(s)-\hat{v}(s,w)]^2$$
### State Distribution
- Used to weigh the individual contribution to the MSE from each state.

## Gradient descent
Want to minimize the MSE for a set of weights.
- Modifying the weights will change the value for many states.

**Gradient of linear value approximation**
$$\nabla \hat{v}(s)=\nabla\left[w \cdot x(s)\right] = x(s)$$

## Gradient Monte Carlo Algorithm
Goal: minimize the value error
$$\overline{VE}=\sum_s \mu(s)[v_\pi(s)-\hat{v}(s,w)]^2$$
$$\nabla\overline{VE}=-\sum_s \mu(s)2[v_\pi(s)-\hat{v}(s,w)]\nabla\hat{v}(s,w)$$
- Requires summing over all states.
- Assumes we know $\mu$.
- Instead: sample from our policy.

Algorithm:
	Input: $\pi$ to be evaluated
	Input: a differentiable function $\hat{V}:\mathcal{S} \times R^d\rightarrow R$
	Parameter: step size $\alpha>0$
	Initial weights $w \in R^d$ arbitrarily
	
loop forever
	Generate an episode $S_0,A_0,R_1,S_1,A_1,...,R_T,S_T$ using $\pi$
		$w\leftarrow w + \alpha\left[G_t - \hat{v}(S_t,w)\right]\nabla\hat{v}(S_t,w)$

## State Aggregation for Value Estimation
State aggregation can be used to approximate the value function.
- Treat certain states as "the same".
- Update values for groups of states.
	- One feature for each group of states.
		- State has feature vector with unit vector corresponding to the group it belongs to.

![[StateAggregation.png]]