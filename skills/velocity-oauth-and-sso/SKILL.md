---
name: velocity-oauth-and-sso
description: OAuth 2.0 Authorization Server, OIDC discovery, token exchange, Clerk integration, and single sign-on (SSO) for 3rd-party apps & Custom GPTs.
---

# Velocity OAuth 2.0 & Single Sign-On (SSO) Skill

Complete operational specifications for authenticating Custom GPTs, external AI agents, and 3rd-party apps with Velocity via OAuth 2.0 and OpenID Connect (OIDC).

- **Live Documentation**: https://velocity-docs.fairarena.app/#oauth-docs
- **Machine-Readable Spec**: https://velocity-docs.fairarena.app/oauth-llms.txt

---

## 1. OIDC Endpoints Reference

- OpenID Configuration: https://clerk.velocity.fairarena.app/.well-known/openid-configuration
- Authorization URL: https://clerk.velocity.fairarena.app/oauth/authorize
- Token Endpoint: https://clerk.velocity.fairarena.app/oauth/token
- Token Info Endpoint: https://clerk.velocity.fairarena.app/oauth/token_info
- User Info Endpoint: https://clerk.velocity.fairarena.app/oauth/userinfo

---

## 2. OAuth App Management Endpoints

### A. List OAuth Apps (GET /api/oauth-apps)
- Returns registered client credentials and redirect URIs.

### B. Create OAuth App (POST /api/oauth-apps)
- Request Body:
`json
{
  name: <App Name>,
  redirectUris: [
    <Redirect URI1>,
    <Redirect URI2>,
  ],
  scopes: profile email
}
`

### C. Update OAuth App (PATCH /api/oauth-apps/id)
- Up to 10 redirect URIs supported per client. Validated for proper URL syntax.

### D. Rotate Secret (POST /api/oauth-apps/id/rotate-secret)
- Rotates clientSecret safely.
