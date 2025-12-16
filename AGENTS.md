Agent guidelines for this repository

## Scope
- This file applies to the entire repository.
- Follow these rules for any file you read or write.

## Repository structure
- Notes and small project starters live under `projects/`.
- Use files named `projects/<topic>/<YYYY-MM-DD-title>.md`.
- Do not create new `projects/<topic>` folders unless the user requests it.
- If no existing project fits a new note, default to `projects/unsorted`.

## Naming conventions
- Use ISO dates `YYYY-MM-DD` at the start of filenames.
- Use lowercase and hyphens. Avoid spaces and underscores.

## Language
Prefer clear, literal language that states what is meant directly.
Avoid narrative or inflated phrasing that adds implied meaning without
increasing clarity.

Examples:
- Bad: I wrote a script to hunt down the shortest available .com domains.
- Good: I wrote a script to find the shortest available .com domains.

- Bad: I finally wrestled the problem into submission.
- Good: I solved the problem.

## Metadata
- Use YAML front matter at the top of new Markdown notes with: `title`, `created`, `updated`, `tags`, `status`, `summary`.
- `created` and `updated` are `YYYY-MM-DD`.

## Provenance
- When adding content based on external material, include a short citation or link in the body. Mark quotations clearly.

## New note template

---
title: Short descriptive title
created: 2025-10-24
updated: 2025-12-14
tags: [tag1, tag2]
status: draft
summary: One or two sentences stating the point of the note.
---

# Context
Brief context in plain language.

# Content
Facts, observations, or ideas in short paragraphs or bullets.

# Next Steps
- Action 1
- Action 2
