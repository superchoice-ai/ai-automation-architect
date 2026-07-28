# PROJECT_MANIFEST

## Purpose

This manifest defines the authoritative artifact groups, control expectations, and completion rules for the AI Automation Architect repository while preserving the established M0–M4 framework.

## Repository Structure

| Area | Responsibility | Required Outcome |
|---|---|---|
| `00_PROJECT_CONTROL` | Project state, manifest, roadmap, governance, decisions, risks, progress, and release controls | A consistent source of project-level truth |
| M0 | Foundation and governance | Approved standards, scope, controls, and working conventions |
| M1 | Architecture | Traceable architecture definitions, module handbooks, interfaces, and design decisions |
| M2 | Build assets | Implementable workflows, schemas, templates, configurations, and reusable components |
| M3 | Validation and operations | Tests, observability, error handling, security checks, runbooks, and operational readiness |
| M4 | Release and improvement | Production acceptance, handover, maintenance, measurement, and continuous-improvement controls |

## Mandatory Cross-Cutting Controls

Every applicable artifact must account for:

- Governance and ownership
- Security, privacy, and secrets handling
- Data and knowledge architecture
- Workflow and integration architecture
- Controlled retrieval and grounded responses
- Guardrails and threshold control
- Human escalation and fallback behavior
- Error handling, retry, recovery, and backup
- Monitoring, auditability, and operational evidence
- AI quota and cost optimization
- Vendor and model portability
- Versioning, compatibility, and change control

## Artifact Requirements

Each file must:

1. Have one clear purpose and an unambiguous path.
2. Identify its module or project-control responsibility.
3. Define inputs, outputs, dependencies, and acceptance criteria when applicable.
4. Avoid duplicating an existing source of truth.
5. Preserve backward compatibility unless an approved decision states otherwise.
6. Contain no production secrets, tokens, or credentials.
7. Be complete enough for implementation or review without hidden assumptions.

## Completion Rules

An artifact is complete only when:

- It exists at the manifest-approved path.
- Its required sections are populated.
- Dependencies and downstream consumers are identified.
- Acceptance criteria are testable.
- Relevant security and operational controls are addressed.
- Review or validation evidence is available where required.

A module is complete only when all mandatory artifacts are complete and its exit criteria are satisfied. Creating files alone does not constitute module completion.

## Dependency Direction

- Project controls govern M0–M4.
- M0 constrains M1–M4.
- M1 provides architecture contracts for M2–M4.
- M2 provides implementation assets for M3 validation.
- M3 provides readiness evidence for M4 release.
- M4 feedback may create controlled change requests for earlier modules without bypassing governance.

## Change Management

All additions must be committed with a concise message describing the batch. Existing artifacts must be updated only through an explicitly authorized change task. Missing-file continuation tasks must skip existing paths and commit new files together as one atomic batch.

## Manifest Maintenance

When project scope or architecture changes, update this manifest together with `PROJECT_STATE.md` and `PROJECT_ROADMAP.md` so the three project-control views remain consistent.
