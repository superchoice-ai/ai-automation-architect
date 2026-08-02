# SC-MCP-04 Installation Gate

1. Import SC-MCP-04_Inspect_n8n_System_Impact_READ_ONLY.json as inactive.
2. Create or select HTTP Header Auth credential N8N_API_WORKFLOWS_READONLY with header X-N8N-API-KEY.
3. Confirm the API key is dedicated to inspection and has the minimum available read scope.
4. Test SC-MCP-04 manually with save-success/save-error execution data disabled.
5. Verify output contains no credential values, node parameters, webhook paths, payloads, or customer data.
6. Copy the imported SC-MCP-04 workflow ID into the ADD-ON tool workflow.
7. Import the ADD-ON as inactive and verify inspect_n8n_impact schema.
8. A new explicit approval is required before activating/publishing either workflow.

Rollback: delete only the two newly imported inactive workflows. Do not alter continue_module, SC-MCP-01, SC-MCP-02/02A, SC-MCP-03, provider adapters, or Content-MKT workflows.
