---
title: Nuxt compile-time confusion
created: 2025-12-09
updated: 2025-12-09
tags: [nuxt, javascript, frameworks]
status: draft
summary: Nuxt hides server-only macros inside functions that look like normal JavaScript, which blurs the server-client boundary and leads to confusing, unsafe behavior.
---

# Context
Personal note on why Nuxt feels unreliable for predictable JavaScript behavior.

# Content
- Nuxt introduces compile-time macros such as `useAsyncData` that resemble everyday callbacks, but the compiler lifts them out of the lexical scope and runs them on the server, so closures stop behaving like real JavaScript closures.
- Because the execution context changes, variables from the surrounding scope are no longer available, and the code base now contains functions that look normal yet silently run elsewhere.
- The boundary between server and client is hidden. Data that those callbacks return is serialized and embedded directly into the HTML document, so any response that is not filtered or cleaned gets shipped to the browser verbatim.
- Embedding that data leaks unnecessary or sensitive values, bloats the payload, and encourages unsafe patterns because the developer cannot see the boundary while writing the function.
- These hidden transformations and unclear boundaries break the usual JavaScript mental model, confuse teams, and produce subtle bugs that are hard to anticipate or test.
- The official Nuxt documentation never states plainly that these callbacks are lifted and executed elsewhere, leaving developers to discover the behavior only after encountering confusing bugs.
- Related note: `projects/programming/2025-12-09-nextjs-over-nuxt.md` explains how Next.js keeps these boundaries explicit.
