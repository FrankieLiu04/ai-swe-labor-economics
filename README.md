# AI, Coding Agents, and Junior SWE Labor Demand

A research repository for developing an economics-style framework connecting frontier coding-agent capability, inference expenditure, human supervision, software-engineering task structure, and junior software-engineer hiring.

## Research question

When does improving AI-agent capability translate from a productivity tool into a structural compression of junior software-engineering hiring?

The project explicitly separates four stages:

1. **Capability** — can an agent complete a task?
2. **Economic viability** — is the risk-adjusted agent cost lower than human labor cost?
3. **Organizational adoption** — can firms safely integrate agents into real production workflows?
4. **Hiring response** — do firms use productivity gains to expand output or reduce labor demand?

## Core hypothesis

The most important near-term bottleneck may no longer be token price itself. Once inference is cheap, the relevant constraint becomes the amount of senior attention required to specify, supervise, verify, and recover agent work.

We call the proposed intermediate quantity:

> **Senior-Attention Leverage (SAL)** — reliable human-equivalent engineering output enabled per unit of senior supervision time.

## Repository structure

- `paper/draft.md` — current conceptual paper draft.
- `paper/formal_model.md` — compact formalization of the economic model.
- `research/empirical_design.md` — possible causal and structural empirical strategies.
- `research/variables.md` — variables, operational definitions, and potential data sources.
- `research/falsifiable_predictions.md` — predictions that can be tested or rejected.
- `notes/research_log.md` — evolution of the reasoning and open questions.
- `notes/ideas.md` — additional hypotheses and extensions.
- `sources/README.md` — source inventory and what each source contributes.
- `data/README.md` — proposed datasets; no proprietary/raw copyrighted data are committed.

## Current status

This repository is currently a **research note / conceptual framework**, not yet a completed economics paper. The main gaps are:

- a formally solved production/labor-demand model;
- causal identification;
- calibrated or estimated parameters;
- robust data on junior/senior hiring and agent supervision;
- systematic literature positioning.

## Suggested next milestone

Turn the conceptual framework into a supervision-constrained production model:

\[
Y = F(S, J, A; M)
\]

subject to

\[
A_{effective} \leq \lambda(M)S,
\]

where `S` is senior labor, `J` junior labor, `A` agent compute/execution, `M` model capability, and `λ(M)` is Senior-Attention Leverage.

Then derive the conditions under which:

\[
\frac{\partial J^*}{\partial M} < 0.
\]

## License

No license has been selected yet. Do not assume permission for redistribution of third-party source materials. This repository stores links and research notes rather than mirroring copyrighted papers.
