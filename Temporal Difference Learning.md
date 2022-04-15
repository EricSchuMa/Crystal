# TD-Update for Function Approximation
Recall Gradient Monte Carlo Update:
$$w \leftarrow w + \alpha\left[G_t - \hat{v}(S_t,w)\right]\nabla\hat{v}(S_t,w)$$
Instead use any unbiased estimate of the value $U_t$
$$w \leftarrow w + \alpha\left[U_t - \hat{v}(S_t,w)\right]\nabla\hat{v}(S_t,w)$$
- E.g., TD target

## TD compared to Monte Carlo
Compared to MC:
- TD target has lower variance.
- TD converges to a biased estimate.
- TD is a *semi-gradient* method.
- TD might converge fast (useful when working with limited amount of samples).

**Example**

![[LongRunPerformanceTDvsMC.png]]

![[TDConvergence.png]]
## Semi-Gradient TD(0)
Algorithm:


## Biased Value Estimation
## Convergence Speed

# Linear TD
- Simple to understand and analyze mathematically.
- With good features, linear methods can learn quickly and achieve good prediction accuracy.

## TD-update with linear Function Approximation

## Linear vs. Non-Linear Function Approximation

## Fixed Point of Linear TD Learning


### Theoretical Guarantee of Mean Squared Error