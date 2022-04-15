# Value Function Estimation
Tabular methods become intractable for large (continuous) state spaces. Therefore, we try to generalize the value estimation over the state space.

## Parameterized Function Approximation
Use a set of real-valued weights to approximate the value function with a **parameterized function**.
- Linear function
- Neural Network

### Linear Value Function Approximation
$$\hat{v}(s,w)=\sum w_i\cdot x_i(s)$$
- Relies on having good features $x_i(s)$.
- Use unit vectors to obtain tabular value function.

### Generalization and Discrimination
Generalization means that we can use information from one situation (state) and apply it to another situation (state).
- Faster learning by using the information we already have.

Discrimination is the ability to make the value of two states different.
- How is the state information influence the value compared to another state.

![[Discrimination&Generalization.png]]