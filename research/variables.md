# Variables and Measurement Plan

| Variable | Meaning | Candidate measurement |
|---|---|---|
| `w_J` | Junior fully-loaded hourly labor cost | payroll / compensation datasets / employer surveys |
| `w_S` | Senior fully-loaded hourly labor cost | same |
| `h_i` | Human hours per task | engineering telemetry / task studies |
| `c_inf` | Agent inference cost | model provider price sheets + token traces |
| `c_tool` | Tool/sandbox/API cost | cloud/tool billing |
| `c_comp` | Experiment/build compute cost | GPU/VM/CI billing |
| `p_i` | Probability of acceptable completion | agent benchmark / production eval |
| `v_i` | Senior supervision time | IDE/agent telemetry + review logs + time study |
| `L_i` | Expected residual failure cost | incident/rollback/security data |
| `SAL` | Human-equivalent accepted output per senior hour | new metric; requires operationalization |
| `JuniorShare` | Entry-level share of hiring | postings datasets |
| `BackfillRate` | Share of departures replaced | firm HR data or surveys |
| `AIExposure` | Task-level coding-agent exposure | task taxonomy + benchmark mapping |
| `Access_rt` | Effective regional frontier-model access | provider support + firm policy + compliance |
| `eta` | Demand elasticity for software output | structural estimation / firm-level proxies |

## Important distinction

API list price is not the same as effective agent cost. Production cost must include:

- repeated trajectories;
- cached vs uncached context;
- build/test/CI compute;
- tool calls;
- human review;
- failures and rollbacks.

Likewise, salary is not employer labor cost. Fully-loaded cost should be used where possible.
