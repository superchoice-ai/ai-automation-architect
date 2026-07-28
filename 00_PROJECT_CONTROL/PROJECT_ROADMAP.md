# PROJECT_ROADMAP

Delivery follows M0–M4. Overlap is allowed only when upstream contracts are stable.

| Phase | Objective | Outputs | Exit gate |
|---|---|---|---|
| M0 | Foundation | Scope, governance, standards, roles, security baseline | Foundation approved |
| M1 | Architecture | Handbooks, boundaries, interfaces, flows, decisions | Contracts ready |
| M2 | Build | Workflows, schemas, prompts, templates, integrations | Assets satisfy M1 |
| M3 | Validate | Tests, gates, monitoring, quota, fallback, runbooks | Readiness passes |
| M4 | Release | Acceptance, handover, KPIs, maintenance | Ownership complete |

## Order

1. Complete `00_PROJECT_CONTROL`.
2. Complete M0 controls.
3. Complete M1 contracts.
4. Produce M2 assets.
5. Run M3 validation.
6. Complete M4 acceptance.

## Gates

- Gate 0: Controls, ownership, risks, changes, decisions align.
- Gate 1: Components, interfaces, schemas, dependencies, security, privacy, data, workflow, fallback, escalation are traceable.
- Gate 2: Assets conform; secrets are externalized; errors, quota, retry, fallback, escalation are defined.
- Gate 3: Tests, monitoring, alerts, backup, recovery, runbooks pass.
- Gate 4: Acceptance, documentation, ownership, KPIs, cadence, backlog are active.

Do not change M0–M4, pass gates with placeholder evidence, overwrite existing files, or split a production batch.
