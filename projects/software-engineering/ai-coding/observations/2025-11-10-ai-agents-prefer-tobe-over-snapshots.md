---
title: AI agents prefer long expect.toBe lists over snapshots
created: 2025-11-10
updated: 2025-11-22
tags: [observation, ai, testing, agents]
status: draft
summary: AI coding agents often expand objects into many expect.toBe assertions instead of using snapshot tests, due to training bias, environment uncertainty, and simple heuristics about what a “good” test looks like.
---

# Context

I keep seeing AI coding agents generate tests that enumerate every field with `expect(...).toBe(...)` instead of using snapshot-style assertions, even when a snapshot would be clearer and easier to maintain.

# Content

Working hypothesis about why AI agents do this:

- Training data bias: they have seen far more examples of unit tests that use explicit `expect(...).toBe(...)` or `expect(...).toEqual(...)` on scalar fields and small objects than examples that rely on snapshot APIs. They copy the dominant pattern they were trained on.
- Framework uncertainty: snapshot tests depend on specific runners and conventions (for example Jest `toMatchSnapshot`, inline snapshots, serializers, and snapshot files on disk). An agent can rarely be certain which runner or assertion library is active, so it falls back to core expectations that probably exist everywhere.
- Naive coverage heuristic: the agent seems to follow a simple rule that “more assertions means better coverage.” A long sequence of `expect(...).toBe(...)` calls looks thorough, even if a single well-chosen snapshot (or a smaller set of semantic assertions) would be more maintainable and just as precise.