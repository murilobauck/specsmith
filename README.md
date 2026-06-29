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
previous one is approved. Once they are, the agent codes **autonomously** —
applying **KISS, YAGNI, DRY, and SoC** to the code it writes and refactoring any
violation before each commit, without pausing to ask.

## What's in the box

| Skill | What it does |
|---|---|
| `prompt-grill` | Interrogates a vague request one question at a time until it can be written as an assertive spec, then generates `specs/<feature>/spec.md`. |
| `dev-lifecycle` | The single source of git mechanics: branch off `develop`, Conventional Commits, one commit per task, green gates, and a PR that pauses for your approval. Also carries the coding principles (KISS, YAGNI, DRY, SoC) the agent self-applies while writing each task. |
| `specsmith-init` | Copies the `specs/` scaffold (README + validated templates for spec, plan, and tasks) into your project so the spec-driven flow has a local home. Optional — `prompt-grill` works without it. |

## Installation

**IDEs** (Antigravity, Cursor, Vscode, etc.) — see below ↓

**Claude Code** — via plugin marketplace:

```text
/plugin marketplace add murilobauck/specsmith
/plugin install specsmith@specsmith
```

After install, the skills are available globally in any project — no
per-project copying or generation step. To also scaffold the `specs/` folder
into your project, run `/specsmith-init`.

### Installing in IDEs

Paste the prompt below into your agent. It will fetch both skills from GitHub,
write them into `.specsmith/` in your project, and scaffold the `specs/`
folder — no manual steps needed.

```text
Install Specsmith in this project by following these steps:

1. Fetch https://raw.githubusercontent.com/murilobauck/specsmith/main/skills/dev-lifecycle/SKILL.md
   and write the content to .specsmith/dev-lifecycle.md in the current project root.

2. Fetch https://raw.githubusercontent.com/murilobauck/specsmith/main/skills/prompt-grill/SKILL.md
   and write the content to .specsmith/prompt-grill.md in the current project root.

3. Fetch https://raw.githubusercontent.com/murilobauck/specsmith/main/specs/README.md
   and write it to specs/README.md (skip if the file already exists).

4. Fetch https://raw.githubusercontent.com/murilobauck/specsmith/main/specs/_template/spec.md
   and write it to specs/_template/spec.md (skip if exists).

5. Fetch https://raw.githubusercontent.com/murilobauck/specsmith/main/specs/_template/plan.md
   and write it to specs/_template/plan.md (skip if exists).

6. Fetch https://raw.githubusercontent.com/murilobauck/specsmith/main/specs/_template/tasks.md
   and write it to specs/_template/tasks.md (skip if exists).

After completing all steps, read .specsmith/prompt-grill.md and .specsmith/dev-lifecycle.md
so you are ready to use them. Confirm which files were created.
```

## Quick start

1. (Optional but recommended) Run `/specsmith-init` to scaffold `specs/` (Claude Code only).
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

## License

[MIT](./LICENSE)
