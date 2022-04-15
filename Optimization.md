#  Optimization
Is the selection of a best element with regard to some criterion

## Minimization or Maximization of a function
e.g. local minimizer $x^*$ of a function $f:R^n->R$  
- $\exists r \in R$ s.t. $\forall x \in B_r(x^*) f(x)<=f(x^*)$ 
- strict min. for inequ. 
- global optim. for whole feasible set
	- easy for convex problems but hard for non-conv. problems

### Methods
- Newton's method $f \in C^2(R^n,R)$  and $\nabla^2f$ is invert.
- Gradient descent
- Generalized steepest descent
- Conjugate Gradient

## Constrained Optimization
Define a feasible set of points and choose optimum from feasible set

### Methods
- Method of Lagrange Multipliers
- Active Set Method

## Multi-Objective Optimization (MOO)
Minimizing several (conflicting) objective functions
- improving one objective may deteriorate several others, i.e.  **tradeoffs**
- optimizing a vector of objectives **vector optimization $$min_x F(x) = (f_1(x) ... f_p(x))^T$$
### Dominance
Consider $x_1, x_2 \in R^n$, then $x_1$ dominates $x_2$ if
- $x_1$ is no worse in any objective
$$\forall i \in {1,...,p}, f_i(x_1)\leq f_i(x_2)$$
- $x_1$ is strictly better in at least one objective 
$$\exists i \in {1,...,p}, f_i(x_1)< f_i(x_2)$$
*Notation:* $F(x_1) \prec F(x_2)$

 ### Pareto Optimality
 Is the concept of Optimality in *MOO* 
 
 The vector $x^*\in \Omega$  is Pareto optimal if it is not dominated by any feasible solution:$$\nexists x \in \Omega \quad s.t. \quad F(x) \prec F(x^*)$$
 **Intuition** 
 > x is Pareto optimal if no objective can be improved without degrading at least one of the others

 ### Weak Pareto Optimality
 The vector $x^* \in \Omega$ is weakly Pareto optimal if there is no $x \in \Omega$ s.t.
 $\forall i=1,...,p$ 
 $$f_i(x)<f_i(x^*)$$
 **Notation**:
 - $P^*$ : set of Pareto optimal solutions
 - $WP^*$: set of weakly Pareto optimal Solutions

## Pareto frontier
Pareto Optimal Set
$$P^* = \{x^* \in \Omega |\nexists x \in \Omega : F(x) \prec F(x^*)\}$$
Pareto frontier $$PF^*=\{F(x^*)|x \in P^* \}$$
## Methods
- Transformation into single-objective ([[Scalarization|scalarized]] MOO)