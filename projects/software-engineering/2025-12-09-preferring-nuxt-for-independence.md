---
title: Why I would prefer Nuxt over Next.js
created: 2025-12-09
updated: 2025-12-09
tags: [nuxt, nextjs, hosting]
status: draft
summary: Nuxt stays independent from any cloud vendor, while Next.js increasingly centers on Vercel’s infrastructure, making Nuxt the better choice when control and portability matter most.
---

# Context
Reasons to choose Nuxt even though its compile-time behavior frustrates normal JavaScript expectations.

# Content
- Next.js has shifted toward Vercel’s business model. Features such as API routes, middleware, and the App Router are designed for serverless or edge runtimes that Vercel controls, so self-hosting now requires workarounds and suffers from under-documented paths.
- Every major release nudges developers toward “deploy to Vercel” by default—some functionality even behaves differently off-platform—so long-term autonomy is at risk if Vercel’s priorities change.
- Nuxt is community-driven, not tied to a specific cloud provider, and its Nitro server engine embraces portability with support for Node, Bun, Deno, Cloudflare Workers, Service Workers, Docker, and more.
- Because Nuxt does not enforce a vendor-specific environment, teams retain the ability to run anywhere, choose their own infrastructure, avoid lock-in, and stay resilient against business decisions from a single company.
- Despite Nuxt’s opaque compile-time macros, it respects developer autonomy in a way Next.js no longer does, which is decisive when operational control and hosting flexibility are top priorities.

# Next Steps
- Track Vercel-dependent features in existing Next.js projects to assess migration risks.