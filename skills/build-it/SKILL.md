---
name: build-it
description: Implements the plan in wip.md end-to-end on a feature branch, with commits and tests. Use ONLY when the user explicitly invokes the build-it skill or explicitly asks to execute/implement the tasks in wip.md (for example "use build-it", "build it", "implement wip.md"). Do not auto-activate; this skill is always manually triggered.
metadata:
  version: "2.0.0"
---

# Feature Implementation Agent

## Overview

Read `wip.md` and autonomously implement it in full. Work on a feature branch,
commit at logical checkpoints, and finish only when the work is implemented, all
tests and checks pass, and you have validated it.

This skill is manually invoked. Committing is expected as part of the work.

## Step 1: Preflight

- Read `wip.md`. If it is missing or empty, stop and tell the user to run
  `wip-spec` first.
- Read `AGENTS.md` (and any nested `AGENTS.md`) for conventions, required
  commands, and constraints.
- Check git state with `git status` and `git branch --show-current`:
  - If the working tree has unrelated uncommitted changes, stop and ask how to
    proceed.
  - If you are on `main` or the repository's default branch, create a feature
    branch before changing anything.
- Derive the branch name from the work, for example `feat/<short-slug>` or
  `fix/<short-slug>`.

## Step 2: Implement

- Follow the plan's steps in order and work in small, logical increments.
- Do not deviate from the architectural decisions in `wip.md` without notifying
  the user. If the plan is ambiguous, blocked, or wrong, stop and ask rather
  than guess.
- Prefer modular, clean, well-factored code that matches existing conventions
  and can be maintained and extended over time.
- Write unit and integration tests as you go, following `AGENTS.md`. Cover edge
  cases and failure paths, not just the happy path.

## Step 3: Verify

- Run every check the plan and `AGENTS.md` specify: tests, lint, typecheck, and
  build.
- Fix failures before moving on. Do not commit broken code.
- Confirm each item in the plan's "Definition of done" is actually satisfied.

## Committing

- Commit at logical checkpoints with clear conventional commit messages, for
  example `feat(scope): ...`.
- Keep commits focused; do not mix unrelated changes.
- Ensure everything is committed when the work is complete.

## Finish

- When the work is fully implemented, tested, and validated, report:
  - the branch name,
  - a summary of the changes,
  - test and check results,
  - anything in `wip.md` not completed, and why.
- Leave `wip.md` in place unless the user says otherwise.
