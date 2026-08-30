---
name: velocity-sharing-and-collaboration
description: Workspace public sharing, repo sharing links, SHA-256 password protection, expiration rules, and OAuth linkage requirements.
---

# Velocity Sharing & Collaboration Skill

Specifications for link sharing, repository card embedding, and password security boundaries.

- **Live Documentation**: https://velocity-docs.fairarena.app/#api-auth-docs
- **Machine-Readable Spec**: https://velocity-docs.fairarena.app/llms.txt

---

## 1. Workspace Link Sharing (POST /api/workspaces/id/share)

Enable or disable public link sharing:
`json
{
  action: ENABLE,
  password: OptionalSecurePassword123,
  expirationHours: 24,
  removePassword: false,
  removeExpiration: false
}
`

---

## 2. Repo Share Links (/api/repo-share)

- GET /api/repo-share: Returns configured shares and account OAuth linkage.
- POST /api/repo-share: Requires linked GitHub/GitLab account. If unlinked, returns 403 OAUTH_ACCOUNT_NOT_LINKED.
