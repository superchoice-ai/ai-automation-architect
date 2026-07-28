# PROJECT_MANIFEST

## Purpose

Define authoritative artifact groups, dependencies, controls, and completion rules while preserving M0–M4.

| Area | Responsibility | Outcome |
|---|---|---|
| `00_PROJECT_CONTROL` | State, roadmap, governance, risks, decisions, changes, releases | Project source of truth |
| M0 | Foundation/governance | Approved scope, controls, standards |
| M1 | Architecture | Traceable boundaries, interfaces, flows, decisions |
| M2 | Implementation | Workflows, schemas, prompts, configurations, components |
| M3 | Validation/operations | Tests, monitoring, security, recovery, runbooks |
| M4 | Production/improvement | Acceptance, handover, KPIs, maintenance |

## Cross-Cutting Controls

Governance and ownership; security, privacy, PDPA, and secrets; data and knowledge architecture; workflow and integration architecture; controlled retrieval; guardrails; human escalation; error handling, retry, recovery, backup; monitoring and evidence; AI quota/cost; portability; versioning and change control.

Each artifact has one purpose/path, defines responsibility, dependencies and acceptance criteria where applicable, avoids duplicated authority, preserves compatibility unless approved otherwise, and contains no production secrets.

Project controls govern M0–M4. M0 constrains M1–M4. M1 contracts guide M2–M4. M2 supplies M3. M3 supplies M4 readiness. M4 feedback enters change control.

Missing-file batches skip existing paths, create one Git tree and commit, and update the branch once per attempt.
