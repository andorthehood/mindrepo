Agent guidelines for this repository

Scope
- This file applies to the entire repository.
- Follow these rules for any file you read or write.

Tone and style
- Use direct, literal English. Avoid idioms, metaphors, or figurative phrases. If the user uses figurative language, translate it into straightforward terms before responding.

Repository structure
- Notes and small project starters live under `projects/`.
- Use files named `projects/<topic>/<YYYY-MM-DD-title>.md` or `.txt`.
- Use Markdown (`.md`) for formatted notes. Use `.txt` for plain text.
- Do not create new `projects/<topic>` folders unless the user requests it.
- If no existing project fits a new note, default to `projects/unsorted`.

Naming conventions
- Use ISO dates `YYYY-MM-DD` at the start of filenames.
- Use lowercase and hyphens. Avoid spaces and underscores.
- Do not rename existing files unless the user requests it.

Edit rules
- Do not change the meaning of existing notes.
- Prefer append-only edits.
- Do not delete files without approval.
- Do not merge or reorganize folders without approval.

Metadata
- Use YAML front matter at the top of new Markdown notes with: `title`, `created`, `updated`, `tags`, `status`, `summary`.
- `created` and `updated` are `YYYY-MM-DD`.

Provenance
- When adding content based on external material, include a short citation or link in the body. Mark quotations clearly.

Automation boundaries
- Do not perform destructive actions.
- Ask before any bulk changes.

New note template

---
title: Short descriptive title
created: 2025-10-24
update: 2025-10-24
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
