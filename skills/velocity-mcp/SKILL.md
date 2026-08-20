---
name: velocity-mcp
description: Model Context Protocol schema definitions, tool parameters, error codes, and response shapes for Velocity MCP Server.
---

# Velocity MCP Skill

This skill documents the tool interface and error specifications for the Velocity Model Context Protocol endpoint.

## Endpoint & Authentication
- **Transport URL**: https://velocity.fairarena.app/mcp
- **Protocol**: JSON-RPC 2.0 over HTTP POST / SSE

## Standard Error Codes Matrix

| Error Code / Message | HTTP Status | Cause | Mitigation / Recovery |
| :--- | :--- | :--- | :--- |
| Error: User unauthorized or unauthenticated. | 401 | Missing or invalid Clerk Bearer token | Re-authenticate MCP client session |
| PREMIUM_FEATURE_LOCKED | 403 | GPU or sharing requested on Free Plan | Prompt user to upgrade to Pro plan |
| INSUFFICIENT_BALANCE | 403 | Wallet balance depleted (.00) | Prompt user to recharge wallet |
| CAPACITY_EXCEEDED | 403 | Free tier 80% or Org 100% capacity hit | Retry later or upgrade to Pro plan |
| WORKSPACE_NOT_FOUND | 404 | Invalid or non-existent workspace ID | Call list_workspaces to fetch valid IDs |
