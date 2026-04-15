# Architecture Decision: Authentication

## Status: Accepted

## Context
The application needs user authentication for API access.

## Decision
- JWT tokens with RS256 signing
- Access tokens: 15 minute expiry
- Refresh tokens: 7 day expiry, stored in httpOnly cookies
- Token refresh endpoint for seamless session extension

## Consequences
- Stateless auth (no session store needed)
- Key rotation supported via RS256 key pairs
- httpOnly cookies prevent XSS-based token theft
- Requires CORS configuration for cookie-based refresh flow
