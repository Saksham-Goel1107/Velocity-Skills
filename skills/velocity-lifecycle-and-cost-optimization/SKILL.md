---
name: velocity-lifecycle-and-cost-optimization
description: Operating policy and rules for stopping, deleting, and optimizing compute costs for Velocity workspaces.
---

# Velocity Lifecycle & Cost Optimization Skill

This skill defines rules for managing container lifecycles to minimize unnecessary user billing.

## Power Management Decision Rules

`mermaid
flowchart TD
    Finish[Agent completes active user task] --> CheckGPU{Is container a GPU instance?}
    CheckGPU -- Yes --> StopGPU[Stop immediately via stop_workspace]
    CheckGPU -- No --> CheckPersist{User requested persistent state?}
    CheckPersist -- Yes --> Stop[Call stop_workspace to halt compute billing]
    CheckPersist -- No --> CheckDisposable{Disposable one-off test sandbox?}
    CheckDisposable -- Yes --> Delete[Call delete_workspace]
    CheckDisposable -- No --> Stop
`

### Policy Rules:
1. **GPU Power Hygiene**: Never leave expensive GPU containers (tx4090, h100, etc.) running idle after a task is finished. Always call stop_workspace when GPU work completes.
2. **STOP vs DELETE**:
   - Use stop_workspace when the user wants to preserve installed dependencies, project files, or disk state for later use.
   - Use delete_workspace ONLY when the user explicitly requests container destruction or permanent cleanup.
3. **GPU Ephemerality**: GPU containers auto-delete on stop (utoDelete: 0). Explain this to the user before stopping a GPU instance.
