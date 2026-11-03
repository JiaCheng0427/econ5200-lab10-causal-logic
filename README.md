# Causal Logic and DAGs: Diagnosing Bad Controls

## Objective

In this lab, I learned how different control variables can affect causal estimates. I also used DAGs to understand why adding more controls does not always make a regression better.

## Methodology

- Used Python and OLS regressions to compare different models.
- Tested how controlling for a collider can create bias.
- Checked whether a variable measured before treatment is always safe to control for.
- Compared total effects and direct effects using a mediator.
- Used the LaLonde job-training data to compare experimental and observational estimates.
- Used `dag_utils.py` to check adjustment sets in DAGs.
- Compared AI-suggested controls with the results from the DAG.

## Key Findings

**1. Collider Bias**

The first regression gave an estimate of -0.007. After controlling for C, the estimate changed to -0.585, and R-squared increased to 0.586. The true effect was zero. This showed me that adding a control can actually make the result worse.

**2. Pre-treatment Controls**

Without W, the estimate was 0.008. After adding W, it became -0.193, even though the true effect was zero. I learned that a variable measured before treatment is not always a good control.

**3. Total Effect vs. Direct Effect**

The total effect estimate was 3.989, close to the true value of 4.0. After controlling for skill, the direct effect estimate was 0.974, close to 1.0. Both results make sense because they measure different effects.

**4. LaLonde Experiment**

The experimental benchmark was $1,794. The observational estimate without adjustment was -$8,498. After adding controls, it changed to $699. The adjustment helped, but it still did not match the experimental result.

**5. AI and DAG Checking**

The AI first suggested controlling for `prior_earnings` and `risk_score`. This gave an estimate of 3.622, but the adjustment set was not valid.

After checking the DAG, I removed `risk_score` because it was a collider. The new estimate was 4.047, close to the true effect of 4.0.

## Conclusion

This lab helped me understand that more controls do not always mean better results. I think checking the relationships between variables is important before running a regression. AI can give useful suggestions, but I still need to check whether those suggestions make sense.
