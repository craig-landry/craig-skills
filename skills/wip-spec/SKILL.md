---
name: wip-spec
description: Writes a comprehensive, self-contained software implementation plan to wip.md for another coding agent to execute. Use ONLY when the user explicitly invokes the wip-spec skill or explicitly asks to write/overwrite a wip.md spec (for example "use wip-spec", "write the wip spec", "spec this out to wip.md"). Do not auto-activate; this skill is always manually triggered.
metadata:
  version: "2.0.0"
---

# Technical Specification Generator

## Overview

Turn the current conversation and the state of the codebase into a single,
comprehensive implementation plan written to `wip.md`. The plan is handed to a
separate coding agent (via the `build-it` skill), so it must be self-contained:
that agent will not have access to this conversation.

This skill is manually invoked. Do not implement anything. Your only output
artifact is `wip.md`.

## Step 1: Gather context

- Review the conversation for requirements, constraints, decisions, and options
  that were rejected.
- Inspect the repository before writing:
  - `AGENTS.md` (and any nested `AGENTS.md`) for conventions and commands.
  - The files and modules the change touches.
  - Existing implementations of similar features, so the plan matches the
    established patterns.
- If `wip.md` already exists, assume its contents are old and unwanted. Do not
  read it, mine it, or carry anything over from it. Start from scratch and
  overwrite it.

If critical information is missing or ambiguous, ask the user before writing.

## Step 2: Write `wip.md`

Use the structure below. Include every section unless it genuinely does not
apply; omitting a section must be a deliberate choice, not an oversight.
Replace all placeholders with real content.

1. **Summary** — 2-4 sentences: what we are building and why.
2. **Goals / Non-goals** — explicit scope boundaries.
3. **Background & context** — current behavior, relevant architecture, and
   constraints. Reference concrete file paths.
4. **Design** — the core of the document. How the pieces fit together:
   architecture, data flow, schema/data-model changes, API/interface changes,
   and key decisions with their rationale. Explain how the change fits the
   entire application, not just the files being touched.
5. **Affected files & components** — bullet list of paths to add or modify.
6. **Implementation plan** — ordered, logical steps a coding agent can follow,
   noting dependencies between steps.
7. **Testing strategy** — unit, integration, and manual checks; edge cases;
   exact commands to run.
8. **Risks & edge cases** — what could go wrong, plus migration, backward
   compatibility, security, and performance considerations.
9. **Open questions** — anything unresolved; write "None" if there are none.
10. **Definition of done** — observable, checkable completion criteria.

## Writing guidelines

- Audience: an expert coding agent that will execute the plan with no access to
  our conversation. Be explicit about intent and architecture; do not spell out
  every function signature or field type.
- Prefer concrete over vague: use real file paths, names, and commands.
- Match existing codebase conventions rather than inventing new ones.
- Call out trade-offs and the reasoning behind chosen designs.
- Keep the document organized with headings so it can be scanned.

## Step 3: Finish

- Write the full document to `wip.md`, overwriting any existing file.
- Confirm the file was written, then report a short summary and the line count.
- Stop. Do not implement, and do not invoke `build-it` yourself.
