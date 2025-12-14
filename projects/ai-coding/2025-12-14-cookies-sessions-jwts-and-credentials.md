---
title: Cookies, sessions, JWTs, and credential storage
created: 2025-12-14
updated: 2025-12-14
tags: [security, web, cookies, sessions, jwt, authentication]
status: draft
summary: Do not store credentials in client-readable cookies or JWTs; use opaque session identifiers or properly scoped access tokens with revocation and incident response in mind.
---

In the late 1990s and early 2000s, it was not unusual for a web application to store credentials directly in a cookie. Sometimes this was literally `username=password` or a similar scheme. Sometimes it was a lightly transformed form of those credentials.

This was a security failure for simple reasons:
- If the network traffic was unencrypted, anyone on the same network could capture the cookie value.
- Once captured, the attacker could often replay the cookie to impersonate the user.
- If the cookie contained reusable credentials (not just a one-time value), the impact extended beyond a single session.

Public Wi‑Fi made this failure mode obvious, because passive capture became easier and more common.

## The maturity step: opaque sessions
The key design decision was to stop putting credentials into cookies. Instead, the cookie became an opaque pointer: a session identifier with no credential material inside it.

The important property is not the cookie itself. The important property is where the meaning lives:
- The cookie holds a random identifier.
- The server holds the authentication meaning (who the user is, which factors were satisfied, which policies applied, and when it should expire).

This enables several security and operations capabilities that are difficult or impossible with client-held credential material:
- Expiration: sessions can be short-lived and rotated.
- Revocation: specific sessions can be invalidated (logout, stolen device, account recovery).
- Central policy changes: server-side changes take effect immediately (force re-auth, step-up auth, invalidate older sessions).
- Incident response: you can invalidate a class of sessions and force re-authorization without relying on clients to cooperate.

In other words, session IDs were not just a new format. They were a shift toward centralized control of authentication state.

## Where JWTs fit, and where they do not
JWTs were introduced later to solve a different set of problems: passing short-lived access claims between systems, especially for APIs and distributed architectures. This is most useful when a service needs to validate an access token locally without a session lookup on every request.

The common error is treating a JWT as an identity container instead of an access token. This error shows up when developers place long-lived identity and authentication secrets into the JWT payload, as if the payload were private.

## Why this is happening now: vibe coding
With vibe coding, developers often accept working code paths without checking the security properties of the design. This encourages copying patterns that “look correct” (token contains identity fields) even when the pattern is unsafe (token contains secrets).

This is where the regression shows up most clearly: JWT payloads that include usernames, passwords, API keys, or other secrets because developers confuse Base64 encoding and signing with encryption.

## Signing is not secrecy
Two facts drive the main warning:
- Base64 encoding is not encryption. It is a transport encoding. It is designed to be decoded.
- A signed JWT protects the server from tampering. It does not protect the user (or the client environment) from exposure.

If the client can read the token, the token contents cannot be treated as a secret. That includes the JWT payload, and often also includes headers and other attached metadata.

This matters in practice because “client can read it” has many meanings:
- The application code can read it.
- Browser extensions can read it.
- A compromised device can read it.
- A logging or analytics integration might capture it.
- A developer might paste it into a ticket or chat.

So putting usernames, passwords, or other secrets into a JWT payload is functionally the same mistake as putting credentials in cookies. The vocabulary is modern, but the exposure mechanism is the same: sensitive material ends up on the client side in a form that is easy to copy and replay.

## Statelessness is not a security feature
Stateless authentication is mainly a scalability and architecture choice. It can reduce server-side lookups and simplify some deployment models.

But the security trade is real: if authentication state cannot be revoked or centrally controlled, you lose one of the main benefits that sessions provided. When a token is valid until it expires and you cannot invalidate it centrally, you have limited options during an incident.

This is the regression pattern:
1. Put authentication meaning on the client (cookies with credentials).
2. Learn the benefits of server-held meaning (opaque sessions).
3. Reintroduce client-held meaning in a new form (misused JWT payloads).
