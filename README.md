# econ3916-lab10-causal-logic

# Correlation & Causality: Confounders, Colliders and the Limits of Controls

## Objective
I wanted to show, with simulations and the LaLonde data, that a correlation alone does not reveal the causal structure behind it, and that adding controls can remove bias or create it depending on the graph.

## Methodology
- Simulated three worlds (true causation, pure confounding and pure selection) that all produce a correlation near 0.65, although the true effects are 2.0, 0.0 and 0.0.
- Drew a confounder, a collider and a mediator as directed graphs with networkx.
- Estimated the treatment effect with and without controlling for the confounder, and with and without controlling for the collider, to compare each result against the known truth.
- Built an M-bias structure in which a control measured before treatment still biases the estimate.
- Wrote a small function, `coef_on_d()`, that returns the coefficient on the treatment for any list of controls, and used it to test whether also controlling for one of the hidden causes (u1) closes the biased path.
- Reproduced the LaLonde (1986) contrast by comparing the randomised experiment with a comparison group from the CPS, then measured how much of the gap covariate adjustment closes.

## Key Findings
- The three simulated worlds gave correlations of 0.654, 0.664 and 0.632, even though the true effects are 2.0, 0.0 and 0.0.
- Controlling for the confounder recovered the true effect.
- Controlling for the collider produced a large, highly significant association between two independent variables: the estimate was -0.592, where the truth is 0.
- In the M-bias structure, the estimate was -0.191. It changed to 0.009 once I also controlled for u1, so a control measured before treatment can still bias the result.
- In the LaLonde replication, the experimental estimate was $1,794 and the naive CPS estimate was $-8,498. With controls, the CPS estimate was $699, which closes 89% of the gap.
