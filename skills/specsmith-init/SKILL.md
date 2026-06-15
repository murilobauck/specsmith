---
name: specsmith-init
description: Scaffolds the Specsmith specs/ structure into the current project — copies the specs/ README and the spec/plan/tasks templates from the installed plugin into the project root so prompt-grill and the spec-driven flow have a local home. Use when the user installs Specsmith and wants the specs/ scaffold in their project, says "init specsmith", "set up specs", "add the spec template", or before starting the spec-driven flow in a project that has no specs/ folder yet.
---

# Specsmith Init

Goal: drop the Specsmith `specs/` scaffold into the user's project so the
spec-driven flow has a local home (a README explaining the cycle and a
`_template/` with validated `spec.md`, `plan.md`, `tasks.md` templates).

## What to do

1. Locate the plugin's bundled scaffold. It lives at `specs/` inside the
   installed Specsmith plugin. Resolve the plugin root via the
   `${CLAUDE_PLUGIN_ROOT}` environment variable. If it is not set in the shell,
   find the plugin under `~/.claude/plugins/cache/` (look for the `specsmith`
   plugin directory containing `specs/README.md` and `specs/_template/`).
2. Copy into the user's project root:
   - `specs/README.md`
   - `specs/_template/spec.md`
   - `specs/_template/plan.md`
   - `specs/_template/tasks.md`
3. **Never overwrite existing files.** If a target already exists, leave it
   untouched and report which files were skipped. Create directories as needed.
4. Report what was created vs. skipped, then point the user at the next step:
   run `prompt-grill` to produce `specs/<feature>/spec.md`.

## Notes

- This is a one-time, opt-in scaffold — not a wizard and not per-project
  generated config. It only copies static files.
- The scaffold is optional: `prompt-grill` works without it (it carries the
  spec structure itself). The local scaffold is for teams who want the README
  and the `plan.md` / `tasks.md` templates checked into their repo.
