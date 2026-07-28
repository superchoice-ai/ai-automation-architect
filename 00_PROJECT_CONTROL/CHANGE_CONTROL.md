# CHANGE_CONTROL

| Class | Example | Approval |
|---|---|---|
| Standard | Missing artifact following contracts | Project/Delivery Owner |
| Normal | Non-breaking workflow/schema change | Project Owner plus technical owner |
| Major | Scope, framework, security boundary, breaking interface | Sponsor and control owners |
| Emergency | Restore service or contain risk | Emergency authority plus retrospective |

`Requested → Assessed → Approved → Implemented → Validated → Released → Closed`

Record reason, affected assets, security/privacy/cost/quota/quality/operations impact, dependencies, rollback, criteria, evidence, approvers, commits, and release references.

Controls: skip existing paths; use one tree, commit, and ref update per attempt; do not overwrite without authorization; rebuild from latest HEAD with bounded retry; never force-update production; never report failed atomic work as partial success.
