---
name: velocity-sharing-and-collaboration
description: Security policies, sharing state rules, token regeneration, and exposure boundaries for Velocity shared workspaces.
---

# Velocity Sharing & Collaboration Skill

This skill governs workspace link sharing, public access token management, and security boundaries.

## Operational Actions (manage_workspace_sharing)
- **ENABLE**: Activates public link sharing and generates/preserves a shareToken. Sets isShared: true.
- **DISABLE**: Deactivates public access. Sets isShared: false and nullifies public sharePath.
- **REGENERATE**: Generates a new secure UUID shareToken while keeping isShared: true. Invalidates all previously issued share links.

## Security & Privacy Rules
1. **Workspace Access vs App Preview**:
   - shareUrl gives full authenticated workspace privileges in the browser.
   - previewUrl only exposes the running web application on the specified port.
2. **Credential Protection**:
   - **Never share SSH private keys or API tokens** over shared workspaces or chat outputs.
3. **Pro Plan Requirement**:
   - Sharing requires a **Pro subscription plan**. Attempting to share on a Free plan returns an authorization error.
