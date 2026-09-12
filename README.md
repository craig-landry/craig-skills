# craig-skills

AI agent skills for convenience.

This repo contains two complementary skills that form a small spec-then-build
workflow. They are designed to be used together: one turns a working session
into a written plan, the other executes that plan.

## The workflow

The intended flow assumes the user and agent have already done a `grilling`
session — interrogating requirements, edge cases, and constraints — using the
Matt Pocock skills. Once the discussion is settled, these skills pick up:

1. **`wip-spec`** — the "to wip" step. Takes everything discussed and known
   about the work and writes a detailed implementation plan to `wip.md`,
   overwriting any existing file.
2. **`build-it`** — reads `wip.md` and autonomously implements it in full,
   working on a feature branch and committing as it goes.

Matt Pocock's skills also offer a `to-spec` step. This repo deliberately does
not use it; `wip-spec` is the preferred way to produce the spec here.

## Skills

| Skill       | Triggers when the request is to...                          |
| ----------- | ----------------------------------------------------------- |
| `wip-spec`  | draft, write, or overwrite a technical spec in `wip.md`     |
| `build-it`  | execute, build, or implement the tasks defined in `wip.md`  |

## Layout

```text
craig-skills/
├── README.md
└── skills/
    ├── wip-spec/
    │   └── SKILL.md
    └── build-it/
        └── SKILL.md
```

## Installation

The recommended way to install is the
[`vercel-labs/skills`](https://github.com/vercel-labs/skills) CLI (`npx skills`),
which supports opencode and many other agents:

```bash
npx skills add craig-landry/craig-skills
```

The CLI discovers the `skills/` layout in this repo automatically. Use
`--list` to preview, `-s` to select specific skills, and `-g` for a global
install:

```bash
npx skills add craig-landry/craig-skills --list
npx skills add craig-landry/craig-skills --skill wip-spec --skill build-it
npx skills add craig-landry/craig-skills -g
```
