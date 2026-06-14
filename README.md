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

The plugin also ships the `specs/` scaffold (a README explaining the cycle and
a blank `_template/`) so any project gets the method's structure for free.

## Installation

In Claude Code:

```
/plugin marketplace add murilobauck/specsmith
/plugin install specsmith@specsmith
```

After install, both skills are available globally in any project — no
per-project copying or generation step.

## Quick start

1. Run `prompt-grill` (or just say "interview me about X"). It conducts the
   interview and writes `specs/<feature>/spec.md`.
2. With the spec approved, write `plan.md` (copy from `specs/_template/plan.md`).
3. With the plan approved, break it into `tasks.md` (copy from
   `specs/_template/tasks.md`).
4. Implement task by task. `dev-lifecycle` handles the branch, commits, and PR.

## A note on git flow

`dev-lifecycle` ships as one opinionated reference flow (`develop`-based
branches, Conventional Commits, PR paused for approval). Teams using a
different git model should adapt the kickoff and close phases accordingly —
there is no automatic parametrization in v1.

## License

[MIT](./LICENSE)
