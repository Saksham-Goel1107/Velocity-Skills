---
name: velocity-cloud-sandboxes
description: Comprehensive workflow protocols, API specifications, discrete hardware allocations, state transitions, and lifecycle management for Velocity Cloud Sandboxes.
---

# Velocity Cloud Sandboxes Skill

Provides AI agents and developers with exact operational decision trees, full request/response schemas, state transition rules, and hardware allocations for Velocity Cloud Sandboxes.

- **Live Documentation**: https://velocity-docs.fairarena.app/#api-auth-docs
- **Machine-Readable Spec**: https://velocity-docs.fairarena.app/llms.txt

---

## 1. Decision Matrix & Lifecycle Rules

`mermaid
flowchart TD
    Start[User requests development environment] --> List[Call GET /api/workspaces]
    List --> CheckActive{Existing RUNNING workspace available?}
    CheckActive -- Yes --> Reuse[Reuse workspace unless isolation requested]
    CheckActive -- No --> CheckStopped{Existing STOPPED workspace matches specs?}
    CheckStopped -- Yes --> StartWs[Call PATCH /api/workspaces/id with action: start]
    CheckStopped -- No --> CreateWs[Call POST /api/workspaces with discrete specs]
`

### Protocol Rules
1. Reuse Over Recreate: Always call GET /api/workspaces first. If a container matching project needs exists in RUNNING or STOPPED state, reuse or resume it via PATCH /api/workspaces/id with action: start.
2. State Hygiene: Prefer pausing containers (PATCH /api/workspaces/id with action: stop) over deletion. Never invoke DELETE /api/workspaces/id unless container destruction is explicitly requested.
3. State Transitions:
   - STOPPED -> Send PATCH /api/workspaces/id with action: start.
   - CREATING / PROVISIONING -> Wait 5-10s and re-check via GET /api/workspaces/id.
   - FAILED -> Inspect GET /api/activity-logs. Create a fresh container if unrecoverable.

---

## 2. Comprehensive API Specs

### A. List Sandboxes (GET /api/workspaces)
- Headers: Authorization: Bearer ak_live_...
- Response: Array of workspace objects containing id, sandboxId, status, editor, isShared, shareToken.

### B. Create Sandbox (POST /api/workspaces)
- Request Body:
`json
{
  repo: github.com/Saksham-Goel1107/Velocity,
  cpu: 4,
  memory: 8,
  disk: 10,
  gpu: rtx5090,
  gpuCount: 1,
  customName: AI Dev Sandbox,
  autoStop: 15,
  autoDelete: 0,
  editor: code-server
}
`
- Allowed Hardware Specifications:
  - cpu: 1, 2, 4 vCPUs.
  - memory: 1, 2, 4, 8 GB RAM.
  - disk: 5, 10 GB SSD.
  - gpu: none, rtx4090, rtx5090, rtx6000, h100, h200.
  - gpuCount: 0 (for GPU none), or 1, 2, 3 GPUs.
  - editor: code-server or jupyter.

### C. Update & Control (PATCH /api/workspaces/id)
- Request Body: { action: start | stop | unarchive, customName: ..., autoStop: 15, autoDelete: 0 }

### D. Delete (DELETE /api/workspaces/id)
- Permanently purges container.

---

## 3. Web Dashboard Link Protocol
Never output internal preview hostnames directly. Direct developers to the live dashboard:
https://velocity.fairarena.app/all-workflows
