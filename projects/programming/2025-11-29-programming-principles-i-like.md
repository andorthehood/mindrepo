---
title: Programming principles I like
created: 2025-11-29
updated: 2025-11-29
tags: [programming, principles, favorites]
status: draft
summary: Collection of programming principles I find useful, starting with Locality of Behaviour.
---

# Context
This note collects programming principles that I find clear, practical, and worth reusing in my own work.
It starts with Locality of Behaviour (LoB) and can grow over time as I add more principles.

# Content

## Locality of Behaviour (LoB)
Locality of Behaviour means grouping code so that everything needed to understand or change a specific behaviour is in one small, nearby place.
When this property holds, I can answer questions about a feature by looking at one file, one function, or one module instead of chasing references across the codebase.

- The goal is to reduce the number of places I must open to understand or change a behaviour.
- It applies at many scales: within a function, within a module, within a service, or within a system.
- It often pairs well with clear naming and small, single-purpose modules.

### Why I like it
- It reduces cognitive load when reading or debugging code.
- It makes changes safer because fewer unrelated parts are touched.
- It encourages designs where tests, configuration, and implementation for a feature live close together.
