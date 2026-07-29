# Production Cutover Guardrails

**Document ID:** SC-PCG-001  
**Status:** Mandatory  
**Effective date:** 2026-07-29  
**Scope:** M0-M4 production changes, integrations, channels, providers, webhooks, credentials, routing, and cutovers

## Purpose

Prevent production outages, duplicate routes, disconnected dependencies, and ambiguous implementation instructions during any production change.

## Iron Rule 1 — Inspect Existing Production Topology and Dependencies Before Proposing Cutover

Before recommending, approving, or executing any cutover, the operator or AI must:

1. Inspect the current production topology and identify the active ingress, processing workflow, outbound channel, secrets, credentials, routes, and fallback paths.
2. Identify upstream and downstream dependencies, including shared webhook URLs, LINE reply/push flows, active n8n workflows, Cloudflare Workers, provider adapters, monitoring, and rollback paths.
3. Confirm whether the target platform supports one endpoint or multiple endpoints. A single-endpoint constraint must be treated as a critical dependency.
4. Compare the proposed topology with the current topology and document what remains unchanged, what is inserted, what is replaced, and what is removed.
5. Define a rollback point and a no-downtime cutover order before changing production.
6. Do not create a replacement receiver, workflow, route, or credential until the existing production dependency has been verified.
7. Stop the cutover when any production URL, workflow, node, credential reference, activation state, or dependency remains unknown.

### Mandatory topology evidence

Every production cutover must record:

- Current ingress URL and owner system
- Current active workflow and trigger node
- Downstream workflows/nodes
- Reply, push, notification, and escalation dependencies
- Secret and credential names without secret values
- Proposed route
- Expected HTTP status and validation evidence
- Rollback route

## Iron Rule 2 — State Exactly What Is Being Changed and Its Impact

Before giving change instructions or applying a change, always state:

- **System:** The platform being changed, such as Cloudflare, n8n, LINE Developers, GitHub, or Google Drive
- **Project/Environment:** The exact project, account, environment, or folder
- **Workflow/Service:** The exact workflow, Worker, service, or component name
- **Node/Setting/File:** The exact node, setting, secret name, route, function, or file path
- **Current value/state:** The existing value or status when safely observable
- **New value/state:** The intended value or status
- **Dependencies affected:** Upstream and downstream components
- **Expected impact:** What changes and what must remain unchanged
- **Validation:** The exact test and expected result
- **Rollback:** The exact restoration step

No instruction may use ambiguous phrases such as “แก้โค้ด”, “เปลี่ยน webhook”, “ตั้งค่า secret”, or “deploy ใหม่” without the fields above.

## Mandatory Change Declaration Template

```text
System:
Project/Environment:
Workflow/Service:
Node/Setting/File:
Current value/state:
New value/state:
Dependencies affected:
Expected impact:
Validation:
Rollback:
Cutover status: HOLD / READY / EXECUTING / VERIFIED / ROLLED BACK
```

## Incident Record — LINE Signed Webhook Proxy

### Observed risk

A new n8n workflow named `SC LINE Signed Webhook Receiver` was created and initially proposed as the upstream destination for `sc-line-signature-proxy` without first validating the existing production topology of `04_RAG_Chat`.

This could have disconnected LINE events from the established processing chain and affected LINE Reply/Push behavior.

### Verified production topology

```text
LINE Developers Webhook
→ LINE Webhook node in n8n workflow 04_RAG_Chat
→ Normalize Input
→ FAQ / RAG / Internet / Admin escalation
→ Split For LINE
→ LINE Reply and LINE Push/Notify paths
```

### Verified components

- **System:** n8n Cloud
- **Project:** `SuperChoiceAI`
- **Production workflow:** `04_RAG_Chat`
- **Ingress node:** `LINE Webhook`
- **Production n8n endpoint:** `https://superchoiceai.app.n8n.cloud/webhook/line-webhook`
- **Proxy system:** Cloudflare Workers
- **Worker:** `sc-line-signature-proxy`
- **Worker URL:** `https://sc-line-signature-proxy.auichai-s2.workers.dev`
- **Cloudflare upstream secret name:** `N8N_WEBHOOK_URL`
- **Required upstream value:** `https://superchoiceai.app.n8n.cloud/webhook/line-webhook`

### Corrective action

- The redundant workflow `SC LINE Signed Webhook Receiver` was archived and removed from the active `ai-automation-architect` folder.
- The active production workflow `04_RAG_Chat` remains the sole LINE event processing workflow.
- Cutover remains controlled until the Worker forwards successfully to the existing `LINE Webhook` node and LINE Developers verification returns HTTP 200.

## Current 502 Diagnostic Change Declaration

```text
System: Cloudflare Workers
Project/Environment: Production
Workflow/Service: sc-line-signature-proxy
Node/Setting/File: Worker code, fetch() handler, outbound fetch block to n8n
Current value/state: LINE Verify reaches Worker but Worker returns HTTP 502 during upstream forwarding
New value/state: Normalize N8N_WEBHOOK_URL and N8N_PROXY_TOKEN with trim(); remove redirect: "error" from outbound fetch; retain the original raw body and x-line-signature
Dependencies affected: LINE Developers webhook verification and n8n workflow 04_RAG_Chat / LINE Webhook node
Expected impact: Worker forwards verified LINE requests to the existing production n8n webhook; Reply/Push topology remains unchanged
Validation: /health returns HTTP 200; direct n8n POST returns HTTP 200; LINE Developers Verify returns HTTP 200; 04_RAG_Chat records a production execution
Rollback: Restore the previous Worker version and keep LINE Developers pointed at the previously verified webhook until the proxy path is corrected
Cutover status: HOLD
```

## Enforcement

These rules are mandatory for humans and AI systems working on this repository. Any production-changing action that lacks topology evidence or an exact change declaration must stop at `HOLD` and must not be executed.
