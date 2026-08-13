# Infrastructure / Core Dependency Change Governance

This repository must treat shared infrastructure changes as gated production changes.

## Mandatory sequence
1. Perform repository-wide System Impact Review before modifying shared infrastructure.
2. Identify direct/indirect consumers: workflows, provider adapters, credentials, webhooks, Supabase/DB access, auth, shared clients, routers, queues, monitoring, approval gates and rollback dependencies.
3. Disclose confirmed and possible impact before implementation.
4. Present alternatives and prefer the lowest blast radius.
5. Obtain explicit approval before implementing a change that can affect multiple workflows or production data paths.
6. Keep changes atomic, reversible and separate from unrelated refactors.
7. Regression-test all identified consumers and document what remains unverified.
8. Define rollback boundary before cutover when practical.

## Supabase / DB core rule
Supabase and equivalent data-layer services are high-risk shared dependencies. Changes to clients, project refs, env selection, RLS, RPC, SECURITY DEFINER functions, migrations, service role, secrets or shared config access require impact analysis before implementation.

## Required pre-change summary
- Change
- Reason
- Confirmed consumers
- Possible impact
- Options
- Recommended lowest-risk option
- Approval required: Yes/No

Read-only impact analysis is allowed without approval. Production/shared infrastructure implementation requires approval when blast radius can cross module/workflow boundaries.
