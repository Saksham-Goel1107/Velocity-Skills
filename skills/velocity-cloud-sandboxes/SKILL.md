---
name: velocity-cloud-sandboxes
description: Workflow decisions, state management, and lifecycle control for Velocity Cloud Sandboxes via MCP. Use when discovering, inspecting, creating, starting, stopping, restarting, or deleting containers.
---

# Velocity Cloud Sandboxes Skill

This skill guides AI agents through discovering, provisioning, managing, and recycling cloud container workspaces on the Velocity platform.

## Agent Decision Matrix

`mermaid
flowchart TD
    Start[User requests development environment] --> List[Call list_workspaces]
    List --> CheckActive{Existing RUNNING workspace available?}
    CheckActive -- Yes --> Reuse[Reuse workspace unless isolation requested]
    CheckActive -- No --> CheckStopped{Existing STOPPED workspace matches specs?}
    CheckStopped -- Yes --> StartWs[Call start_workspace]
    CheckStopped -- No --> CreateWs[Call create_workspace with discrete specs]
`

### Operational Rules
1. **Reuse over Recreate**: Always call list_workspaces first. If a workspace with matching environment or project exists in RUNNING or STOPPED state, reuse or start it. Do not create duplicate containers.
2. **Preserve State**: Prefer stop_workspace when work is paused. Never call delete_workspace unless the user explicitly requests container destruction or cleanup.
3. **Handle State Transitions**:
   - **STOPPED**: Call start_workspace.
   - **CREATING / PROVISIONING**: Wait 5–15 seconds and re-check list_workspaces or get_connection_info. Do not trigger another create_workspace.
   - **FAILED**: Inspect failure logs in get_notifications. Do not retry indefinitely. Create a clean replacement workspace if the previous container cannot be recovered.

## Available Discrete Specifications

When creating a workspace, supply exact values:
- **cpu**: 1, 2, or 4 vCPUs.
- **memory**: 1, 2, 4, or 8 GB RAM (Daytona limit: max 8 GB per sandbox).
- **disk**: 5 or 10 GB SSD.
- **gpu**: 'none', 'rtx4090', 'rtx5090', 'rtx6000', 'h100', 'h200' (Requires Pro subscription plan).
- **editor**: 'code-server' (VS Code) or 'jupyter' (JupyterLab).

## Workflow Execution Steps

1. **Discover**: Call list_workspaces. Check for active containers.
2. **Provision**: Call create_workspace with exact discrete parameters.
3. **Monitor**: Verify status becomes PROVISIONING ? RUNNING.
4. **Connect**: Call get_connection_info to retrieve preview/terminal/SSH commands.
5. **Clean Up**: Call stop_workspace upon completing the user request to save compute billing.
