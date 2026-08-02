# inspect_n8n_impact Contract v1.0

## Purpose
Read-only System Impact Review for Contents-MKT and the existing SuperChoiceAI environment.

## Inputs
- base_url: n8n instance base URL.
- project_tag: optional workflow-tag filter.
- include_inactive: boolean, default true.

## Allowed operations
- GET /api/v1/workflows only.
- Read workflow metadata, active/archive status, node names/types, credential reference names/types, and connection edges.

## Never returned
Credential values, API keys, tokens, node parameters, webhook paths, execution payloads, or customer data.

## Output
Sanitized inventory, dependency edges, category map, duplicate workflow-name risks, and confirmation of prohibited fields removed.

## Production guardrails
The imported workflow must remain inactive until a separate approval. Use a dedicated credential named N8N_API_WORKFLOWS_READONLY. Do not reuse production provider credentials. No POST, PUT, PATCH, or DELETE operation is present.
