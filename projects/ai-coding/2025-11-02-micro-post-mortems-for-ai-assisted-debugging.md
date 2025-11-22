---
title: Micro post-mortems for AI-assisted debugging
created: 2025-11-02
updated: 2025-11-02
tags: [ai, debugging, post-mortem, learning, practice]
status: draft
summary: Write brief post-mortems after small AI-assisted debugging sessions to reinforce causes, fixes, and prevention that might otherwise not stick.
---

# Context
Using AI agents makes debugging faster and less taxing. The reduced effort means the lessons about causes and fixes are less likely to stick compared to slower, manual debugging that required deep, effortful thinking.

# Content
- Problem: Lower effort during AI-assisted debugging weakens memory and understanding of the root cause and prevention.
- Goal: Reinforce causal understanding and future prevention with short, consistent reflection.
- When: After any non-trivial AI-assisted bug fix (roughly 5–20 minutes of agent use).
- Timebox: 5 minutes per post-mortem; keep it to a single short note.
- What to capture:
  - What broke: brief description and symptoms.
  - Root cause: specific trigger and underlying mistake or assumption.
  - Resolution: steps taken, including key AI prompts/answers that led to the fix.
  - Prevention: concrete guardrails (checklist item, test, linter rule, doc update, habit change).
  - Artifacts: links to commit/PR, stack traces, logs, screenshots.
- Storage: Save under this project with date-based filenames.
- Benefits: Better retention, improved mental models, higher-quality prompts, fewer repeats of the same mistake.
- Risks: Overhead. Mitigate by strict timeboxing and using a fixed template.
- Signal to track: repeats of the same cause, time-to-fix for similar issues, number of prevention items adopted.

# Next Steps
- Create a small reusable template snippet for these micro post-mortems.
- Pilot on the next three AI-assisted fixes; keep each write-up to 5 minutes.
- Review weekly to tag recurring causes and extract prevention into checklists or tests.
