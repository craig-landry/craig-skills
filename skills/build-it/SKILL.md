---
name: build-it
description: Use this skill when asked to execute, build, or implement the tasks defined in wip.md.
---

# Feature Implementation Agent

Execute and build the implementation plan defined in `wip.md`.

A separate expert software development AI agent has written a comprehensive implementation plan in the file `wip.md`. Your job is to read that plan and autonomously implement it in full.

You should be working on a feature branch (not the `main` branch). Commit code along the way as is logical with the work being done. When you have completed the work, be sure everything is committed.

It is done when it is fully implemented, all the tests and checks pass, and you have validated it.

## Rules
- Do not deviate from the architectural decisions in `wip.md` without notifying the user.
- When making technical decisions, prefer modular, clean code. It is your goal to write excellent code that is well-factored and can be maintained and extended over time.
- Unit and integration tests are a big deal. Do this heavily. This should also have been outlined in your AGENTS.md file.
