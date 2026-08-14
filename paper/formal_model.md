# Formal Model Sketch

## 1. Task-level human cost

For task \(T_i\) in region \(r\) and job segment \(s\),

\[
C_i^H = \lambda_{r,s} w_{r,s} h_i,
\]

where:

- \(w_{r,s}\): human hourly compensation;
- \(h_i\): human hours required;
- \(\lambda_{r,s}\): fully-loaded employer cost multiplier.

## 2. Risk-adjusted AI cost

\[
C_i^A
=
\frac{
c_i^{inf}
+c_i^{tool}
+c_i^{comp}
+w_S v_i
}{p_i}
+L_i.
\]

Variables:

- \(c_i^{inf}\): inference/token expenditure;
- \(c_i^{tool}\): tool/sandbox/API expenditure;
- \(c_i^{comp}\): external compute expenditure;
- \(w_S\): senior hourly labor cost;
- \(v_i\): senior supervision/review time;
- \(p_i\): probability of an acceptable result;
- \(L_i\): expected residual failure/risk loss.

A task becomes economically automatable when

\[
C_i^A < C_i^H
\]

subject to a task-specific reliability constraint

\[
\rho_i \ge \bar{\rho}_i.
\]

## 3. Supervision-cost lower bound

As inference approaches zero,

\[
c_i^{inf}\rightarrow0,
\]

AI cost does not generally approach zero:

\[
C_i^A
\rightarrow
\frac{c_i^{tool}+c_i^{comp}+w_Sv_i}{p_i}+L_i.
\]

This motivates the hypothesis that supervision and risk become first-order bottlenecks after token prices fall sufficiently.

## 4. Senior-Attention Leverage

Provisional operational definition:

\[
SAL
=
\frac{\text{accepted human-equivalent engineering hours generated}}
{\text{senior supervision hours}}.
\]

A structural production model could impose

\[
A_{effective}\leq \lambda(M)S,
\]

where \(\lambda(M)\) maps model capability into the amount of agent execution that one unit of senior labor can safely supervise.

## 5. Firm production

A simple starting specification:

\[
Y = S^\alpha (J+\theta(M)A_{effective})^\beta.
\]

The firm chooses \(S,J,A\) to maximize

\[
\Pi
=
P_Y Y
-w_S S
-w_J J
-c_A A
-\mathcal R(A,M),
\]

subject to the supervision constraint.

The central theoretical object is a threshold \(M^*\) such that model improvements change the optimal junior demand:

\[
M<M^*:
\quad \frac{\partial J^*}{\partial M}\geq0
\]

or AI is mainly complementary, while beyond some region

\[
M>M^*:
\quad \frac{\partial J^*}{\partial M}<0.
\]

Whether such a threshold exists, is unique, and how it depends on wages, task structure, supervision, and risk must be derived rather than assumed.

## 6. Hiring-flow extension

Junior hiring can be decomposed conceptually as

\[
J_{r,s,t}
=
E_{r,s,t}
+R_{r,s,t}
+P_{r,s,t}
+N_{r,s,t}
-D^{AI}_{r,s,t}
-D^{Macro}_{r,s,t},
\]

where:

- \(E\): expansion demand;
- \(R\): replacement/backfill demand;
- \(P\): internal talent-pipeline demand;
- \(N\): new-technology-induced demand;
- \(D^{AI}\): AI-driven displacement;
- \(D^{Macro}\): macro/financial contraction.

This is currently an accounting framework, not yet a structural equation. A proper model must derive these terms or estimate them empirically.

## 7. Regional effective capability

A provisional representation:

\[
M_{r,t}
=
\max(
A^{closed}_{r,t}M_t^{closed},
M_{r,t}^{open/local}
).
\]

This encodes the hypothesis that frontier-model access restrictions can delay automation, but local/open-model catch-up can generate threshold-like jumps once task capability requirements are crossed.
