---
title: GitHub Copilot PM meeting notes
created: 2025-12-01
updated: 2025-12-03
tags: [ai-coding, copilot, meeting]
status: draft
summary: My notes and prompts to give structured feedback about GitHub Copilot as an AI coding agent, especially its GitHub UI integration for issues and pull requests.
---

# Context
- **Role:** I am a principal engineer (web developer).
- **Scope:** I mainly use Copilot in my open source projects, not in my primary job codebase.
- **Workflows:** My main Copilot workflows are refactoring existing code, writing tests, and adding new features.
- **Surfaces:** I use Copilot both in my IDE and in the GitHub UI (issues and pull requests).
- **Standout value:** For me, the standout value is that Copilot inside the GitHub UI can manage issues and pull requests, give and receive feedback through review comments, and behaves like another collaborator in the repository.
- **Hypothesis:** My hypothesis is that this collaboration experience is the main advantage of Copilot compared to other AI coding tools.

## Key talking points
- **GitHub UI integration as a teammate**
- **Preferred plan-first workflow with agents**
- **Why I do not plan with GitHub Chat**
- **Usage and cost transparency**
- **Pull request workflows and limitations**

# Content

## What currently works well
- **GitHub UI integration** (what I like):
  - It participates in issues and pull requests with comments and suggestions.
  - It fits into my existing review workflows, similar to working with another human developer.
  - It keeps discussion and code changes in one place, rather than forcing me to switch to external tools.
- **Review agent configuration**:
  - I like that I can give specific instructions to the review agent (for example, what to focus on or how strict to be), rather than only using generic, one-size-fits-all instructions.
- Overall, it feels to me like a teammate embedded directly into the repository rather than a separate generic coding assistant.

## Preferred workflow with Copilot agents
- The current Copilot agent user interface has a **single input field** where I enter a prompt and the agent starts working immediately.
- I prefer to **separate planning from execution**:
  - First, I **brainstorm a detailed plan** with an AI chatbot (Copilot, Claude Code, or Codex) until the plan is clear and low in ambiguity.
  - Then I ask the chatbot to **save the agreed plan as a file** in the repository for archiving and later reference.
  - After the plan is saved in the repository, I ask the GitHub agent to **execute that plan**.
- With this workflow, the GitHub agent usually needs **minimal steering** while it works, because the plan is explicit and stored in the codebase.

## Why I prefer other AI tools over GitHub Chat for planning
- In theory, GitHub Chat would be the obvious tool for planning, because it is **integrated into the experience** and can **delegate to agents**, but in practice I do not use it for this.
- When I try to plan with GitHub Chat, it often feels **difficult to talk to**:
  - It behaves as if it is not willing to **look into files** during planning.
  - It prefers to **assume details**, such as API shapes, instead of reading the actual implementation in the repository.
  - I need to **ask it repeatedly to read the files and the code**, which is exhausting for me.
  - It is also not clear to me **which files it actually read, and when**, so I cannot easily tell how up-to-date or grounded its suggestions are.
- Sometimes GitHub Chat also **struggles to read or write files** at all:
  - It tells me that it was unable to read or edit specific files.
  - Then it gives me detailed instructions on how I should open and edit the files myself, or what to search for in the repository to find relevant files.
  - It often asks me to paste my findings back into the chat, which breaks the feeling that it is an integrated coding agent.
- Other AI tools I use for planning (Claude Code or Codex) tend to **read files in the repository more readily**, with fewer assumptions, which makes planning with them smoother.
- Another reason I avoid GitHub Chat for planning is **usage limits**: I do not want to drain my Copilot usage limits with planning conversations, because I prefer to preserve that usage for agents that execute my saved plans.
- For planning, I prefer AI tools that are more **transparent about their usage and costs**, so I can see how much of my budget I spend during the planning phase.

## Problems and questions to explore in the meeting
- **Usage transparency:**
  - Copilot Chat and Copilot agents are not transparent about **usage metrics**.
  - I would like a **summary at the end of a conversation or agent run** that shows how many tokens or other usage units it consumed (for example, a percentage of a plan or quota).
- **Pull request workflows:**
  - When I manually open a pull request, the Copilot agent **cannot assist directly on that branch**.
  - Instead of committing into the existing branch, it **creates a separate pull request**.
  - This behavior is especially annoying for **smaller changes** where I expect the agent to just help me finish or polish my own PR.
  - I also noticed that the agent **cannot edit the description** of manually created pull requests when I ask it to.
  - In those cases, it opens a **new pull request**, and then realises that it still cannot edit the original description, which feels like wasted work and noise.

## Ideas and potential improvements to discuss
- **Collaboration model:**
  - Make the “team member” behavior in GitHub UI even more explicit, with clear roles (for example, “refactoring specialist”, “test engineer”, or “docs reviewer”).
  - Better memory of the repository’s norms: coding style, review customs, decision records, and previous discussions.
  - Smarter follow-up comments that track conversations across multiple pull requests.

## Model-level limitations (generic, not necessarily Copilot-specific)
- These are **model-level issues** that are not specific to GitHub Copilot, but might still be interesting to discuss if there is time, especially if they can be mitigated at the **agent layer**.
- Examples I might bring up (only if relevant in the conversation):
  - **Superficial tests and mirror assertions:** cases where the model generates tests that are technically correct but not meaningful (for example, creating an object and using `expect(...).toBe(...)` only to check fields that were just set in the same test), or where the test recomputes the expected value by calling the same helpers as production code. I wrote more about this pattern as “mirror assertions” in `projects/ai-coding/observations/2025-05-05-mirror-assertions-in-ai-tests.md`.
  - **Mock drift:** cases where AI-driven editing of tests and mocks gradually expands mock behaviour until mocks start reimplementing real systems, increasing false confidence and masking integration issues. I wrote more about this in `projects/ai-coding/observations/2025-06-06-mock-drift-in-ai-testing.md`.
  - **Preference for long expect.toBe lists over snapshots:** cases where agents generate many explicit `expect(...).toBe(...)` assertions instead of using snapshot-style tests, even when snapshots would be clearer and easier to maintain. I wrote more about this in `projects/ai-coding/observations/2025-11-10-ai-agents-prefer-tobe-over-snapshots.md`.
  - **Unnecessary API fallbacks:** cases where agents add backward-compatibility shims, optional parameters, or branching logic for API changes I did not ask to keep backwards compatible, which increases complexity and is especially confusing for less experienced developers. I wrote more about this in `projects/ai-coding/observations/2025-11-22-ai-agents-and-unnecessary-api-fallbacks.md`.
