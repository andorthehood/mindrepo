---
created: 2025-10-10
updated: 2025-10-16
model: GPT-5
topic: codex auto-verification loop
tags: [codex, tooling, feedback]
---

# TODO: Codex Auto-Verification Feedback

## Issue
OpenAI Codex v0.46.0 keeps re-verifying files it has edited during a session. When I make manual adjustments afterward, Codex assumes they are mistakes, restores its previous edits, and removes my changes. This persistent re-checking happens even across follow-up prompts, which interrupts iteration and feels overly defensive.

## Next Step
- [ ] Check whether the OpenAI Codex repository already has an issue tracking this auto-verification behavior so I can follow or contribute to it.
