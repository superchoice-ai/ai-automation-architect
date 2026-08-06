# PROJECT_GOVERNANCE

## Authority and mandatory read-first protocol

GitHub is the source of truth and the center for both human and AI readers. Before inspecting, planning, changing, validating, or operating any project asset, every human or AI actor must read `00_PROJECT_CONTROL/README.md`, this file, `PROJECT_STATE.md`, `PROJECT_MANIFEST.md`, `PROJECT_ROADMAP.md`, `DECISION_LOG.md`, and `CHANGE_CONTROL.md`. Instructions already recorded in these canonical files are binding and must not be replaced by assumptions, chat memory, scratch files, or newly created duplicate governance documents.

If a canonical instruction appears incomplete, the actor must verify the existing GitHub Markdown first and update the existing authoritative file through change control. A scratch or Library copy is not an authoritative project update.

## Principles

GitHub is the source of truth. Decisions are evidence-based. Security, privacy, quality, cost, and operations are shared responsibilities. Material scope, security, architecture, production, permission, publication, activation, deletion, or destructive changes require specific human approval. Gates require evidence.

## Iron rules

### IR-01 — MCP First; Cloud Browser requires prior approval

If an appropriate MCP capability exists, all inspection, creation, editing, validation, and operational actions must use MCP first.

Cloud Browser is a worst-case fallback only when the required MCP capability is unavailable or demonstrably cannot complete the specific action. Before using Cloud Browser, the actor must state the exact MCP limitation, the intended browser actions, affected systems, and risks, then obtain explicit human approval for that browser use. A previous `Continue` or approval for another action does not authorize Cloud Browser.

### IR-02 — Absolute prohibition on AI-to-AI communication

An AI must never send AI-generated output to another AI for review, critique, validation, rewriting, continuation, decision-making, delegation, orchestration, debate, judging, or conversation. Sub-agent, planner-executor, reviewer-judge, multi-model debate, and equivalent AI handoffs are prohibited unless this rule is explicitly amended by the Project Owner in GitHub.

Every AI invocation must be attributable to one user request and one defined purpose. Duplicate AI calls, speculative calls, parallel model calls, and unapproved retry loops are prohibited because they reduce auditability and consume credit/cost repeatedly.

Provider fallback is permitted only as sequential failure handling: call one provider at a time, call the next provider only when the current provider fails or has no usable quota, never pass one provider's generated answer to another provider, and stop immediately when one provider succeeds. The approved order remains `OpenAI → Claude → Future low-cost AI → Gemini → Admin escalation`. Gemini-pinned embedding/vector operations remain a separate non-conversational system responsibility.

### IR-03 — Approval is action-specific

`Approve`, `อนุมัติ`, or `Continue` authorizes only the latest clearly described action and its stated scope. It does not implicitly authorize Cloud Browser, AI-to-AI work, additional permissions, publishing, activation, deletion, destructive actions, production review submission, or scope expansion. When the action, method, permission, target, or risk changes, obtain new explicit approval.

## Roles

| Role | Accountability |
|---|---|
| Sponsor | Business outcome, funding, escalation |
| Project Owner | Scope, priorities, acceptance, roadmap |
| Architecture Owner | Architecture integrity and contracts |
| Security/Privacy Owner | Security, PDPA, access, risk acceptance |
| Delivery Owner | Implementation quality and dependencies |
| Operations Owner | Monitoring, recovery, quota, cost, readiness |
| Quality Owner | Tests, evidence, defects, release recommendation |

## Review cadence

| Cadence | Review |
|---|---|
| Before every project action | Mandatory read-first check; MCP availability; approval scope; AI-call count |
| Per batch | Scope, paths, validation, atomic commit |
| Delivery cycle | Progress, RAID, dependencies, decisions |
| Module gate | Artifacts, evidence, risks, approval |
| Release | Security, quality, operations, rollback |
| Post-release | KPIs, incidents, cost, quota, improvement |
