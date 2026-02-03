# Changeup_Movement_Ranking


Changeup (CH) Pure Movement Ranking — v3.5.2+
Purpose

Estimate optimal horizontal and vertical movement weights for changeups and produce slot-invariant, bias-adjusted pitcher rankings.

The goal is to isolate pure movement quality by removing release/velocity effects and aligning movement direction with real outcomes.

Modeling Strategy

Pitch quality is separated into two independent components:

W — Whiff Model

Binomial ridge regression
→ effect of movement on swinging-strike probability

Q — Soft Contact Model

Gaussian ridge regression
→ effect of movement on contact quality (exit velocity)

Movement importance is measured using 1-SD marginal effect sizes from each ridge model.

Final weights:

w_x = λ·w_x_W + (1−λ)·w_x_Q
w_z = 1 − w_x

λ = trade-off between whiff and weak contact importance  
w_x = weight for horizontal movement  
w_z = weight for vertical movement (1 − w_x)  
w_x_W = horizontal weight from the Whiff model  
w_x_Q = horizontal weight from the Soft Contact model


Bias Removal (Key Idea)

Expected movement is predicted from:

- velocity

- arm slot

Pure movement = observed − expected (residual)

This removes:

- arm slot bias

- velocity bias


Validation

Cluster-fold CV by pitcher (leakage prevention)

Cluster bootstrap for confidence intervals

Outputs

Interactive dashboards:

CH movement grades (20–80 scale)

Pitcher rankings

Bias-adjusted residual movement metrics

Notes

This repository shares methodology and results only.
Full training code is available upon request.
