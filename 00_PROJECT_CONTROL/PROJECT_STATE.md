# PROJECT_STATE

## Metadata

- Project: SuperChoice AI Automation Architect
- Framework: M0–M4
- Environment: Production
- Status: Active
- Source of truth: GitHub

## State

The project follows M0–M4. Continuation completes missing artifacts without renaming modules, changing framework boundaries, or replacing existing files.

| Area | State | Responsibility |
|---|---|---|
| `00_PROJECT_CONTROL` | Active | State, manifest, roadmap, governance, risks, decisions, changes, releases |
| M0 | Active | Foundation, scope, standards, governance, controls |
| M1 | Active | Architecture, interfaces, dependencies, handbooks |
| M2 | Planned/Active | Workflows, schemas, templates, components |
| M3 | Planned/Active | Quality, security, observability, operations, recovery |
| M4 | Planned | Acceptance, handover, measurement, improvement |

`Missing → Draft → Review → Approved → Implemented → Validated → Released → Maintained`

## Priorities

1. Complete `00_PROJECT_CONTROL`.
2. Align state, manifest, and roadmap.
3. Continue M0–M4 in dependency order.
4. Resolve blockers before downstream work.
5. Measure validated deliverables, not file count.

## Rules

Preserve M0–M4; skip existing files; commit production batches atomically; maintain governance, security, privacy, observability, quota, cost, fallback, recovery, and human escalation; record material changes; support ChatGPT and Claude-compatible workflows where applicable.

`Progress % = validated required deliverables ÷ total required deliverables × 100`
