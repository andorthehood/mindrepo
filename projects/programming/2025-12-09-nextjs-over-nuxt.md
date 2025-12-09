---
title: Why I prefer Next.js over Nuxt
created: 2025-12-09
updated: 2025-12-09
tags: [nextjs, nuxt, javascript]
status: draft
summary: Next.js keeps server and client responsibilities explicit, while Nuxt hides compile-time transformations that violate normal JavaScript expectations.
---

# Context
Personal reasoning for choosing Next.js instead of Nuxt.

# Content
Nuxt hides critical behavior inside compile-time macros that impersonate normal JavaScript. Functions such as the callback passed to `useAsyncData` look like regular closures:

```js
const userId = useState('userId')

const { data } = await useAsyncData(() => {
  return $fetch(`/api/users/${userId.value}`)
})
```

Nuxt extracts that callback, runs it on the server, and strips away access to the lexical scope, so variables like `userId` disappear or act differently. The experience is literally “the framework removed my function from its lexical scope without telling me.” That is not JavaScript behavior, and it breaks the normal mental model for closures.

Nuxt also obscures the server–client boundary. Anything returned from those server-run callbacks gets serialized and inlined into the HTML document. When developers forget to filter responses, Nuxt embeds unnecessary or sensitive data into the page. The framework offers no visible indicator that the boundary even exists.

Next.js approaches this problem directly. In the App Router every file is a Server Component unless it begins with `'use client'`:

```js
'use client'
```

The presence or absence of that directive makes the execution environment obvious. Server files cannot access browser-only APIs, and client files cannot consume non-serializable data. If you try to write server code that touches client-only values such as `window.location`, Next.js fails immediately instead of serializing anything silently.

Because Next.js enforces explicit boundaries—no closures crossing layers, no functions passed from server to client, no automatic serialization of arbitrary values—the framework keeps the JavaScript model trustworthy. Nuxt does the opposite by pretending its transformations are normal JavaScript, encouraging subtle bugs and confusing teams. I prefer Next.js because it makes every “magic” behavior visible and predictable.

# Next Steps
- Keep documenting concrete Next.js patterns that prevent accidental data leaks.
- Review Nuxt code for hidden compile-time behavior that would violate these expectations.
