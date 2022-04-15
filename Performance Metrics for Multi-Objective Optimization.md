# Evaluation of [[Multi-Objective Sequential Decision Making]]
Generally, there is more than one optimal solution. MORL algorithms produce *solution sets*. 
- When is one solution set better than the other?
- What properties should a solution set have, and how do we measure those?

# Axiomatic-Based Evaluation Metrics
Assume that the optimal solution is the true Pareto front (or convex hull).
Compare sets in terms of:
- Spread 
- Coverage 
- Distance

Con: Difficult to interpret for a user -> Motivates the utility-based evaluation

### Hypervolume Metric
Measure the volume in value-space that is Pareto-dominated by the policies in an approximate coverage set. 

![[HypervolumeMetric.png]]

$$HyperVolume(CS,V_{ref})=\cup_{\pi \in CS} Volume(V_{ref},V^\pi).$$
where $Volume(V_{ref}, V^\pi)$ is the hypercube spanned by the reference vector, $V_{ref}$, and the vector in the $CS$, $V^\pi$.

- Correlates with the [[Spread of a Set]].
- Performance of a solution can be obtained by comparing the hypervolume of the solution to the hypervolume of the non-dominated set (or with true Pareto front).
- Difficult to interpret, because hypervolumes do not map to real-world value or utility.
	- What does a difference of hypervolume mean to an end-user?
	- Adding just one solution to an extreme end of the solution range could drastically change the hypervolume.
	- True set (Pareto front) is unlikely to be known for complex problems.

## Sparsity of Coverage Sets
If we have two approximate solution sets with similar hypervolume, we should prefer the set which has more spread over the value space. In other words, the user has a large variety to choose from.
- Look for diverse solutions: solution sets that are evenly spread over the solution space
- Look for sets with high resolution - dense coverage of the whole Pareto front.

Sparsity: 
- Pareto fronts approximations with lower sparsity are better.
	$$Sp(S)=\frac{1}{|S| - 1}\sum_{j=1}^m \sum_{i=1}^{|S|-1} (\tilde{S}_j(i) - \tilde{S}_j(i+1))^2$$
with Pareto front, $S$, $m$ objectives, and $\tilde{S}_j(i)$ is the $i-th$ value in the sorted list for the $j-th$ objective value in $S$.

## The Epsilon-Metric
Measures how closely a solution set $S$ approximates the Pareto front $PF$.
- Gives an indication of the factor by which the approximate solution is worse than the Pareto front.
- Can be used to derive a gain in utility for the user.

**Additive epsilon-indicator**:
A solution set $S$ is an $\epsilon$-approximate Pareto front according to this metric if *for each* value vector $V^\pi$ on the Pareto front, there *exists at least one* value vector $V^{\pi'}$ in the solution set $S$ , s.t. for each objective $d$, the value in $V^{\pi'}$ is at most $\epsilon$ smaller than the values in $V^\pi$.
$$I_{\epsilon^+}=inf_{\epsilon \in R}\{\forall V^\pi \in PF, \exists V^{\pi'} \in S: V_i^\pi \leq V_i^{\pi'} + \epsilon, \forall i \in \{1,...,n\}\}$$
with $n$ objectives, $V^\pi$ being the $d-$dimensional value of policy $\pi$. 

**Multiplicative epsilon-indicator:**
$$I_{\epsilon^*}=inf_{\epsilon \in R}\{\forall V^\pi \in PF, \exists V^{\pi'} \in S: V_i^\pi \leq V_i^{\pi'} (1+ \epsilon), \forall i \in \{1,...,n\}\}$$
Each objective can at most be worse by a multiplicative factor of $1+\epsilon$. This scales with the magnitudes of the individual values (obj. with larger values allow for a larger deviation).

## Metrics from Information Retrieval
Coverage Ratio (CR): measures the count of policies recovered from a finite Coverage Set.

![[CoverageRatio.png]]

**Issues**
- Implies that precision and recall are equally important.
- Solutions are treated equally regardless of how big the utility is to the user.
- Not correlated with the spread of the solution.
- $\epsilon$ needs to be defined (arbitrary choice) 
	- Consider too many or too little solutions to "be" in the CS.
	- Choice of $\epsilon$ can influence ordering of obtained solutions
- Policies can be counted twice.

# Utility-Based Evaluation Metrics
If it is possible to assess the utility of the user at the time of deployment, the solution sets can be compared based on the user's utility.
- Compare agent's ability to maximize user utility.

**Expected Utility Metric (EUM)**
For a given solution set, the EUM is defined as the expected utility given a prior distribution over user utility. Under SER optimality criterion, this can be written as:
$$EUM=E_{P_u}\left[max_{\pi \in S} u(V^\pi) \right]$$
with solution set $S$ , utility function $u$ and value vector $V^\pi$.
- Useful in situations where we care about the agent's ability to do well across many different utility functions. E.g., many solutions from the set will be used.
- Requires a good prior over utility (scalarization) functions in order for EUM to be meaningful.

**Maximal Utility Loss (MUL)**

Maximal loss in utility when taking a single policy from a given solution set instead of the full set of possible optimal solutions. In terms of SER optimality:
$$MUL=max_{u \in U}\left(max_{\pi \in S^*} u(V^{\pi^*}) - max_{\pi \in S} u(V^\pi)\right)$$
where $S^*$ is the true optimal solution set (PF or CH), $S$ the solution set outputted by the algorithm, $V^\pi$ the vector-value of said policy, and $u$ the utility function of the user over which we maximize.

## Note on evaluation
- Values are mostly approximations and will translate this into evaluation.
	- May have high variance or systematic biases.
	- If the value of the best policy is off we might not select it.
	- Misleading utility estimate.
**Therefore, value estimates in the selection phase should not directly rely on the value vector estimates from the MORL algorithms.**
-> Instead run a separate run of policy evaluation before selection.

### Benchmarks
![[MORLBenchmarks.png]]