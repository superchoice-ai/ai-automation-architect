# M2 Validation MCP Tools — Installation and Control Record

## Purpose

Add two bounded SuperChoice MCP capabilities without modifying the established
M0–M4 framework or the production LINE → Cloudflare → `04_RAG_Chat` topology:

1. `run_m2_validation_suite`
2. `get_n8n_execution_evidence`

## Exact change map

| System | Project | Workflow | Node or setting | Change |
|---|---|---|---|---|
| n8n | SuperChoiceAI | `SC-MCP-02 Run M2 Validation Suite` | Entire new subworkflow | Run allowlisted M2 fixture requests; dry-run required first |
| n8n | SuperChoiceAI | `SC-MCP-03 Get n8n Execution Evidence` | `n8n API - Get Execution` | Read one execution and return sanitized metadata/node summary |
| n8n | SuperChoiceAI | `SuperChoice MCP - M2 Validation` | MCP Trigger + two Tool Workflow nodes | Expose both tools to ChatGPT/Claude MCP |
| GitHub | `superchoice-ai/ai-automation-architect` | n/a | Three workflow JSON files and this record | Store source, contract, decision, and rollback evidence |

No change is made to:

- Cloudflare Worker `sc-line-signature-proxy`;
- LINE Developers Webhook URL;
- n8n workflow `04_RAG_Chat`;
- node `LINE Webhook`;
- existing MCP workflow `SuperChoice MCP - continue_module`;
- existing provider/channel credentials.

## Import order

Import into n8n project `SuperChoiceAI` in this order:

1. `n8n/SC-MCP-02 Run M2 Validation Suite.json`
2. `n8n/SC-MCP-03 Get n8n Execution Evidence.json`
3. `n8n/SuperChoice MCP - M2 Validation.json`

Keep all three workflows inactive during configuration.

## Required configuration

### SC-MCP-03

At node `n8n API - Get Execution`:

1. Create or select an **HTTP Header Auth** credential.
2. Credential name recommendation: `N8N_API_EXECUTIONS_READONLY`.
3. Header name: `X-N8N-API-KEY`.
4. Enter the n8n API key directly in n8n Credentials. Never paste it into chat,
   workflow JSON, GitHub, fixtures, or execution evidence.
5. Restrict the key/account to execution reads where the n8n plan and access
   model permit.

### SuperChoice MCP - M2 Validation

At node `run_m2_validation_suite`, select:

`SC-MCP-02 Run M2 Validation Suite`

At node `get_n8n_execution_evidence`, select:

`SC-MCP-03 Get n8n Execution Evidence`

This replaces the two `REPLACE_WITH_...` placeholders with the IDs assigned by
n8n after import.

## Safety controls

### Runner

- Requires explicit boolean `dry_run`.
- Requires a non-empty exact-host allowlist.
- Allows HTTPS only.
- Maximum 100 cases per call.
- Blocks credential-capable headers:
  `Authorization`, `Cookie`, `X-API-Key`, `X-N8N-API-KEY`,
  `X-SC-Proxy-Token`, and `X-Line-Signature`.
- Does not activate, update, or delete workflows.
- Does not call LINE or Cloudflare unless their hostname is explicitly added;
  those production hosts must not be allowlisted for the M2 fixture run.

### Evidence reader

- Reads a single numeric execution ID.
- Returns execution/workflow identity, timestamps, status, and sanitized node
  summaries only.
- Omits credentials, headers, tokens, signatures, node payloads, binary data,
  and customer content.
- Does not retry, stop, delete, or mutate executions.

## Activation sequence

1. Import all three workflows.
2. Configure the two Tool Workflow references.
3. Configure `N8N_API_EXECUTIONS_READONLY`.
4. Manually test `SC-MCP-03` with execution `299`; verify that no payload,
   credential, token, LINE content, or binary data is returned.
5. Manually test `SC-MCP-02` with one harmless fixture case and
   `dry_run=true`.
6. Run the same harmless fixture with `dry_run=false`.
7. Activate only `SuperChoice MCP - M2 Validation`.
8. Reconnect/refresh the SuperChoice MCP plugin so both tools appear.
9. Run the 8 approved suites / 23 cases with dry-run first.

## Rollback

1. Deactivate `SuperChoice MCP - M2 Validation`.
2. Remove or disconnect its MCP endpoint.
3. Delete the three newly imported workflows only after confirming that no
   other workflow calls `SC-MCP-02` or `SC-MCP-03`.
4. Revoke the `N8N_API_EXECUTIONS_READONLY` API key.

The production LINE/Cloudflare/n8n path remains unchanged throughout rollback.

## Gate rule

M2 can close only after all 23 approved cases have:

- case ID and suite ID;
- expected and actual result;
- sanitized execution evidence;
- PASS/FAIL decision;
- no exposed secret or customer payload;
- reconciliation in the M2 Gate evidence record.
