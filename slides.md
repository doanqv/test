<script type="text/javascript" async
  src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-MML-AM_CHTML">
</script>

Does Regression Produce Representative Estimates of Causal Effects? Discussing Aronow & Samii (2016)
========================================================
author: Quantitative Methods Workshop
date: October 4th, 2016
autosize: true

Why this Paper?
========================================================

Multiple regression (MR) is probably the most common empirical technique we work with, a “workhorse approach for estimating causal effects” (p.251) 

**Key Takeaways**

1. Covariate selection influences both internal and external validity.
2. All effects are local in some way or another. Don’t despair, be detailed.
3. Be considerate (1) in general, but also, (2) of your sources of identifying variation.

External and Internal Validity Trade-Offs
========================================================

From Campbell (1957):

External validity: "To what population, settings, and variables can this effect be generalized?"

Internal Validity: "Did in fact the experimental stimulus make some significant difference in this specific instance?"

External and Internal Validity Trade-Offs
========================================================

**RCTs and Quasi-experimental designs: Internal > External**

- RCTs: small, unrepresentative experimental sample
- RDs: treatment effect “local” only to those within bandwidth
- Instrumental Variables: treatment effect “local” only to “compliers”
- Fixed Effects: identifying variation limited to “switchers”

**Multiple Regression: External > Internal** 

- With large data set, can be used to draw identifying variation from representative sample
- Increased risk of OVB but use of “rich” covariates can help mitigate (e.g., NCES data sets)

A & S: The “perceived trade-off...is an illusion”
========================================================

(i.e., everything is terrible)

A & S identify how the use of covariates effectively weights units differently. 

They lay out a method to calculate “multiple regression weights” that identifies the “[contribution] of sample members” to the treatment effect.

**Broader Implication: You can start off with a (nominally) representative sample that, by your covariate selection, non-representatively contributes to your estimates.**

A Heuristic, Math-Minimal Explanation
========================================================

Consider estimating a treatment effect in the following fashion:

$Y_i = \beta_0 + \beta_1D_i + \mathbf{X_i}\beta_2 + \varepsilon_i$

We want to estimate the average treatment effect of some binary treatment ($D_i$) on an outcome ($Y_i$). We are concerned about selection bias, so we control for a set of covariates ($\mathbf{X_i}$). 

Let’s think about the effect of these covariates by breaking out a separate “selection” model, where we're trying to explain someone's selection into treatment (whether $D_i = 0,1$) with a set of observable characteristics:

$D_i = \delta_0 + \mathbf{X_i}\delta_1 + \eta_i$

The Cost of Covariates
========================================================

Why did we add $\mathbf{X_i}$? Because we’re concerned that those factors that explain selection into treatment also explain variation in the outcome, i.e., $cov(\varepsilon_i, \eta_i) \neq 0$.

The hope is that, conditional on covariates $\mathbf{X_i}$, the two errors are independent, i.e., $cov(\varepsilon_i, \eta_i|\mathbf{X_i}) = 0$ 

If conditional independence holds, we’ve broken the link between unobservables in the selection model and structural models; that’s good. 

The Cost of Covariates
========================================================

But covariate inclusion isn't without consequences.

$Y_i = \beta_0 + \beta_1D_i + \mathbf{X_i}\beta_2 + \varepsilon_i$

$D_i = \delta_0 + \mathbf{X_i}\delta_1 + \eta_i$

Recall the “partialling out” interpretation of multiple regression. $\beta_1$ is identified using variation in $D_i$ that isn’t explained by, i.e. “partialled out”, by $\mathbf{X_i}$

Therefore, where’s our identifying variation? It's $\eta_i$, whatever component of variation in $D_i$ that is unexplained by your covariates.

Identifying the Effective Sample
========================================================

A & S identify that each unit’s contribution to the effect estimate is weighted according to the conditional variance of the treatment variable.

$D_i = \delta_0 + \mathbf{X_i}\delta_1 + \bbox[5px,border:2px solid red]{\eta_i}$

In other words, the larger your value of $\eta_i$ (i.e., the less the included covariates explain your treatment status/level), the more your individual effect is weighted.

This is a problem if there are hetereogeneous treatment effects.

**Your identifying variation could be unbiased but is it coming from your (full) population of interest?**

Identifying the Effective Sample
========================================================

$D_i = \delta_0 + \mathbf{X_i}\delta_1 + \bbox[5px,border:2px solid red]{\eta_i}$

A & S use the squared residual from the selection model, i.e., $\hat{\eta_i}^2$ as an estimate of each unit’s multiple regression weight ($w_i$). This weight is calculated independent of the outcome variable.

You can calculate the proportion of each unit’s contribution to the treatment effect as $w_i/\sum w_i$. These weights transform the “nominal” sample into the “effective” sample.

This is particular useful when working with nested data. How much does each school/district/college/country contribute to the treatment effect?

Extensions I Find Interesting
========================================================

Non-varying units in a fixed effects model are a special case where $\eta_i = 0$. The treatment status of “non-switchers” is explained entirely by their unit membership, and therefore, contribute no identifying variation.

Scenario: the inclusion of another variable changes your coefficient of interest. Is it OVB or a re-weighting of your "effective sample"?

What about research studying disadvantaged populations who may be more "bound" by demographics (i.e., "demography is destiny") to certain "treatment" statuses?

Coding Demonstration
========================================================


