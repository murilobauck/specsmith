# Specsmith

> 🇧🇷 [Versão em português](./README.pt-br.md)

**A spec-driven development kit for [Claude Code](https://code.claude.com).**

AI coding tools give inconsistent results when you drive them ad hoc. Specsmith
packages a method that works in practice: interrogate the request until it's
unambiguous, write a `spec.md`, then `plan.md`, then `tasks.md`, then execute
with disciplined git hygiene. It ships as an installable Claude Code plugin —
two skills plus a `specs/` scaffold that ties them together.

## Who it's for

Developers already comfortable with Claude Code who want a proven path from a
vague request to shipped, reviewed code without losing rigor along the way.

## The method

```
spec.md (approved)  →  plan.md (approved, declares the branch)  →  tasks.md  →
kickoff (branch)  →  code (1 commit per task)  →  close (tests/CI → push → PR draft, pause)
```

Never jump straight to implementation. Each stage advances only once the
previous one is approved.

## What's in the box

| Skill | What it does |
|---|---|
| `prompt-grill` | Interrogates a vague request one question at a time until it can be written as an assertive spec, then generates `specs/<feature>/spec.md`. |
| `dev-lifecycle` | The single source of git mechanics: branch off `develop`, Conventional Commits, one commit per task, green gates, and a PR that pauses for your approval. |
| `specsmith-init` | Copies the `specs/` scaffold (README + blank templates) into your project so the spec-driven flow has a local home. Optional — `prompt-grill` works without it. |

## Installation

In Claude Code:

```
/plugin marketplace add murilobauck/specsmith
/plugin install specsmith@specsmith
```

After install, the skills are available globally in any project — no
per-project copying or generation step.

## Recommended: scaffold the specs/ folder

Specsmith works out of the box (`prompt-grill` carries the spec structure
itself). For the best results, though, drop the `specs/` scaffold into your
project so the README and the `plan.md` / `tasks.md` templates live in your repo
and your whole team sees the method:

```
/specsmith-init
```

This copies `specs/README.md` and `specs/_template/` into your project root
without overwriting anything that already exists. You can also copy the `specs/`
folder from this repo manually if you prefer.

## Quick start

1. (Optional but recommended) Run `/specsmith-init` to scaffold `specs/`.
2. Run `prompt-grill` (or just say "interview me about X"). It conducts the
   interview and writes `specs/<feature>/spec.md`.
3. With the spec approved, write `plan.md` (copy from `specs/_template/plan.md`).
4. With the plan approved, break it into `tasks.md` (copy from
   `specs/_template/tasks.md`).
5. Implement task by task. `dev-lifecycle` handles the branch, commits, and PR.

## A note on git flow

`dev-lifecycle` ships as one opinionated reference flow (`develop`-based
branches, Conventional Commits, PR paused for approval). Teams using a
different git model should adapt the kickoff and close phases accordingly —
there is no automatic parametrization in v1.

## Status & roadmap

**v0.1 — initial MVP.** This first release is deliberately minimal: it ships
the method (the two core skills + the scaffold) so it can be validated and
refined in real use before growing. Expect the surface to evolve based on
feedback.

On the roadmap:

- **Antigravity support** — a future release will make Specsmith available for
  Antigravity as well, not just Claude Code.

## License

[MIT](./LICENSE)
