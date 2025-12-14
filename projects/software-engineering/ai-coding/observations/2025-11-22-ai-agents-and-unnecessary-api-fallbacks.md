---
title: AI agents and unnecessary API fallbacks
created: 2025-11-22
updated: 2025-11-22
tags: [observation, ai, agents, api-design]
status: draft
summary: AI coding agents often add backward-compatibility fallbacks for API changes that were not requested, which increases complexity and risk for inexperienced developers.
---

# Context
After several sessions using AI coding agents to change API contracts in different projects, I noticed a recurring behaviour.

# Content
- When I request an API contract change, agents often assume I want to preserve all existing call sites and avoid any breaking changes, even if I do not say this.
- They introduce compatibility layers, optional parameters, or branching logic to keep old usage patterns working alongside the new API.
- These backward-compatibility paths are usually not requested explicitly and add extra complexity, code paths, and maintenance overhead.
- Across multiple changes, the fallbacks accumulate into a growing layer that makes it harder to understand the real API surface.
- This is especially risky when a less experienced developer works on the project, because it becomes difficult to see which paths are current, temporary, or safe to remove.
- I prefer agents to treat API contract changes as explicit design decisions: either accept a breaking change with a clear migration path, or add compatibility layers only when I ask for them.
 - Asking agents to write an implementation plan first often reveals early that they silently assumed backward compatibility and no breaking changes, because this assumption shows up in the plan steps.
 - Even if I ask one agent to remove that requirement from the plan, passing the same plan to a different agent can still lead to the same compatibility-preserving behaviour unless the plan explicitly states that breaking changes are expected.

# Next Steps
- Be explicit in prompts about whether breaking changes are acceptable and when they are preferred.
- Tell agents not to add backward-compatibility shims or fallbacks unless they are explicitly requested.
- Ask agents to propose a migration plan when a breaking change is desirable, instead of silently preserving old behaviour.
- Periodically review the codebase for unnecessary compatibility layers introduced by AI assistance and remove ones that are no longer needed.
 - When asking for a plan, explicitly include a line that breaking API changes are expected for this task and that the agent should update all relevant call sites instead of preserving old usage patterns through shims.
