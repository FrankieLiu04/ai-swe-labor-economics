# Empirical Research Designs

## Design A — Junior hiring and AI exposure

Question: Did entry-level software hiring fall disproportionately in occupations/firms more exposed to coding-agent automation?

Illustrative specification:

\[
JuniorShare_{irt}
=
\alpha
+\beta(Exposure_i \times Post_t)
+\gamma_i+\delta_t
+X_{irt}\theta+\epsilon_{irt}.
\]

Key requirements:

- credible pre-trends;
- occupational and firm fixed effects;
- controls for interest rates, post-2022 tech correction, remote-work intensity, layoffs, and local labor-market conditions;
- separate entry-level, mid-level, and senior postings.

The coefficient \(\beta\) is meaningful only if the treatment and identifying assumptions are defensible.

## Design B — Same-firm regional comparison

Potential quasi-experiment: compare offices of the same multinational across regions with different effective access to frontier models.

Examples of possible units:

- Hong Kong vs Singapore offices;
- Hong Kong vs Tokyo offices;
- within global banking/technology firms.

Illustrative panel:

\[
Hiring_{frt}
=
\beta Access_{rt}
+\alpha_f
+\gamma_t
+X_{rt}\theta
+\epsilon_{frt}.
\]

Major challenge: model access is endogenous to geography, regulation, business mix, and firm policy.

## Design C — Event study around coding-agent capability shocks

Candidate events should be selected before looking at outcomes where possible. Avoid treating generic ChatGPT availability as identical to autonomous coding-agent capability.

Possible treatment variables:

- release of materially stronger coding-agent models;
- enterprise enablement of coding agents;
- changes in approved internal AI tooling;
- large drops in effective inference cost.

## Design D — Structural calibration

Estimate/calibrate:

\[
\Theta =
\{w_J,w_S,p,v,L,c_{inf},c_{tool},c_{comp},\lambda(M),\eta\}.
\]

Then simulate optimal junior, senior, and agent inputs under different model generations, wages, regions, and firm demand elasticities.

This is the most ambitious path and requires novel measurements of supervision time and accepted agent output.
