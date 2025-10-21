---
created: 2024-03-17
updated: 2025-10-16
topic: co-located tests research
tags: [javascript, typescript, testing]
---

# Research Task: Co-Locating JS/TS Tests

I really like Rust’s in-file `#[cfg(test)]` modules that keep unit tests right next to the code they touch, unlike the JavaScript and TypeScript tendency to place tests in separate `__tests__` folders or sibling `*.test.ts` files. I’d like to understand why the same pattern hasn’t become equally popular in JavaScript and TypeScript projects.

## My hypothesesis for current JS/TS testing conventions

- Shipping source straight to browsers incentivized keeping tests out of the same files to avoid accidental bundling.
- Tooling and scaffolds (Jest, CRA, Next.js, Angular CLI) default to `__tests__` or mirrored directory structures, reinforcing separation.
- TypeScript build setups often emit only `src/` to `dist/`, so colocated tests complicate compiler configs.
- Mocking/DI ecosystems assume a distinct test harness and directory, making same-file patterns feel awkward.
- Guides, tutorials, and OSS examples rarely showcase inline tests, so the convention never shifted.

## Findings

### Vitest In-Source Testing Support

Found that [Vitest supports in-source testing](https://vitest.dev/guide/in-source.html#in-source-testing) similar to Rust's `#[cfg(test)]` modules. Key details:

- Uses `if (import.meta.vitest)` blocks at the end of source files
- Tests share the same closure as implementations, allowing access to private states
- Requires `includeSource: ['src/**/*.{js,ts}']` in vitest config
- Production builds need `define: { 'import.meta.vitest': 'undefined' }` for dead code elimination
- TypeScript support via `"vitest/importMeta"` in tsconfig types
- Recommended for unit testing small functions/utilities and prototyping
- Separate test files still recommended for complex tests like components or E2E

## TODO tasks

- Identify test runners and bundlers that officially support colocated tests.
- Document tree-shaking or build-step patterns to exclude inline tests from production bundles.
- Compare ergonomics with Rust's `#[cfg(test)]` modules, including pros/cons for large codebases.
- Collect real-world examples or case studies (framework docs, OSS repos) using this layout.
- Summarize recommended project structure and naming conventions for colocated tests.
