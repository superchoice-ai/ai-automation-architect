# n8n backup snapshot — 2026-09-05

This branch contains a read-only snapshot from `https://superchoiceai.app.n8n.cloud`.

## Coverage

- Total inventory: 58
- Full sanitized workflow definitions: 31
- Metadata-only because `Available in MCP` was disabled: 27
- Team project workflows: 51
- Personal project workflows: 7
- Separate published-version snapshots where different from draft: 1
- Credential bindings redacted: 62
- Secret values included: **No**

Directory layout preserves n8n ownership and folders:

- `team/<n8n folder or _root>/...`
- `personal/_root/...`

Each full JSON preserves nodes, connections, workflow settings, active state, node groups, IDs, and workflow/sub-workflow references. Credential IDs/names and recognized inline secret fields are replaced with `__REDACTED__`; credentials must be rebound manually after restore.

`manifest.json` is the authoritative inventory and relationship map. Entries marked `metadata-only-blocked` are **not restorable workflow definitions**. Their graph could not be read because n8n returned `INVALID_ARGUMENT` while `Available in MCP` was disabled. No n8n setting was changed to bypass this boundary.

## Restore outline

1. Review `manifest.json` and import required full JSON files into the correct n8n project/folder.
2. Rebind credentials manually in the target environment.
3. Resolve sub-workflow IDs using the relation map if n8n assigns new IDs.
4. Keep imported workflows inactive until credentials, callers, webhooks, error workflows, and permissions are verified.
5. Validate with pin data or another approved non-production test path before publishing.

This is a backup-only branch. It does not modify n8n, Lovable, databases, credentials, production runtime, or `main`.
