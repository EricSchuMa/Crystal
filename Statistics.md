# Statistics
Record variations, interactions and dependencies of real-world objects of interest and make "sense" of the data via statistics. Statistics can help to quantify potential relationships, patterns, or  answer hypothesis about the data.

# Statistical Models
- Focus on rejecting null hypothesis instead of research hypotheses.
- Relationship between hypothesis and test not clear.
- Industrial framework.

## Hypotheses
## Process models?
## Statistical models
- procedure / Golem
- justified by implications of process model
- question
## Null Models?

## Golems
Golem of Prague analogy
- Clay robots
- Powerful
- No wisdom or foresight
- Dangerous

## Owls
**Bayesian approach to drawing an Owl**
- Permissive
- Flexible
- Express uncertainty at all levels
- Direct solutions for measurement error, missing data
- Focus on scientific modeling

**Drawing the Bayesian Owl**
- Understand what you are doing
- Document your work
- Reduce Error
- Respectable scientific workflow
- Result: Statistical model

### Outline - Drawing the Bayesian Owl
1. Theoretical estimand (*What are you trying to do?*)
2. Scientific (causal) model(s) (*Produce data*)
3. Use 1 & 2 to build statistical model(s)
4. Simulate from 2 to validate 3 yields 1
5. Analyze real data

## DAGs
- Which control variables do we need?
- Different queries, different models.
- Not safe to add everything -> bad control
- How to test the causal model?

![[DAG.png]] 

Variables are nodes and directed edges are causes.
- Directed Acyclic Graphs
- Heuristic causal models
- Clarify Scientific thinking
- Analyze to deduce appropriate statistical models

### Causal Inference
Correlation is **not** causation.
- Associations between variables
- Prediction of intervention: knowing the cause means to be able to predict the consequences of an intervention
 >What if I do this?
- Imputation of missing observations: counterfactual imagination of what could have happened
> What if I had done something else?

**Science Before Statistics**
-  For **statistical models** to produce scientific insight, they require **scientific (causal) models**
- **Reasons** for statistical analysis are not found in the data
- Even descriptions need causal model: How the **sample** differs from the **population**

## Summary
Golems: Brainless, powerful statistical models
Owls: Documented, objective procedures
DAGs: Transparent scientific assumptions to
 - **justify** scientific effort
 - **expose** it to useful critique
 - **connect** theories to Golems

 ## Bayesian Data Analysis
 For each possible explanation of the data
- Record relative frequencies for all the ways data can happen.
- Explanations with more ways to produce the data are more plausible.
![[BayesianProbEst.png]]
Answer: (2) = 3, (3) = 8, (4) = 9

### Bayes Rule
![[BayesRule.png]]

#### Updating priors

![[UpdatingPriors.png]]

#### Intervals

![[ConfidIntervals.png]]

### From Posterior to Prediction
- Implications depend upon **entire** posterior
- **Must** average any inference over entire posterior 
	--> Integral calculus or sampling



