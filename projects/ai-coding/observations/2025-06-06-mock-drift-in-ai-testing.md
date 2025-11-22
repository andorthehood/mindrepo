---
title: Mock drift in AI-driven testing
created: 2025-06-06
updated: 2025-11-12
tags: [observation, testing, mocks, ai, vibe-coding]
status: draft
summary: AI agents keep expanding test mocks until the mocks effectively implement the real system, unless someone intervenes with boundaries and policy.
---

# Context
Observed "mock drifting" in AI-assisted development where agents iteratively edit tests and supporting scaffolding to achieve green runs.

# Content
- Definition: "Mock drift" is when test mocks accumulate behavior with each iteration until they replicate the real implementation. This happens because the agent optimizes for passing tests, not for maintaining strict mock boundaries.
- Causes:
  - No stated scope for what a mock may do; the agent treats the mock as an open-ended place to fix failures.
  - Tests overspecify interactions, forcing mocks to learn business logic.
  - Lack of contract tests against real components or interfaces, so the drift goes unnoticed.
  - Reward function is “tests pass now,” not “architecture stays healthy.”
- Risks:
  - False confidence: tests pass while real integration paths remain untested.
  - Duplicated business logic in mocks, increasing maintenance and masking regressions.