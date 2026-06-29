---
name: dev-lifecycle
description: Git mechanics for any code demand — branch creation off develop, conventional commits, CI/tests, push, and a PR that pauses for approval. Use ALWAYS when starting a feature/fix/chore, creating a branch, committing, opening a PR, or when the spec-driven flow (prompt-grill) reaches the kickoff, checkpoint, or close phases. Single source of git mechanics; never reimplement branch/commit/PR outside it.
---

# Dev Lifecycle

Composable git mechanics for any code demand. The spec-driven flow (`prompt-grill`)
calls these phases at the right moments; the `/ship` command runs them in sequence
for small changes without a spec. Either way, the mechanics live here and only here.

All git artifacts — branch names, commit messages, CI config, PR title and
description — must be in **English**, regardless of the language of specs or chat.

> **Reference flow, not a mandate.** This skill ships as one opinionated
> `develop`-based reference flow. Teams using a different git model (trunk-based,
> GitHub Flow, release branches, etc.) should adapt the kickoff and close phases
> accordingly. There is no automatic parametrization.

## Phase: kickoff (start of any demand)

1. Ensure `develop` is up to date (`git fetch` + fast-forward).
2. Create the working branch from `develop`:
   `<type>/<kebab-case-description>` where `<type>` is a Conventional Commits
   type: `feat | fix | chore | refactor | docs | test | perf`.
3. If working spec-driven: the branch name comes from the approved `plan.md`;
   also record it at the top of `tasks.md` so a new session knows where to work.
4. Never work directly on `develop` or `main`.

## Phase: checkpoint (during development)

Make a Conventional Commit: `type(scope): subject` — imperative mood, concise, English.

**Commit-unit ownership (avoids double decomposition):**
- **With a spec** (`tasks.md` exists): the task is the commit unit. One task
  marked `[x]` = one commit referencing what the task delivered. Do not invent
  a different split.
- **Without a spec** (small change via `/ship`): commit in logical units —
  never one giant commit at the end.

**Coding principles (apply autonomously while writing each task — refactor before
the commit; never pause to ask the user):**
- **KISS** — write the simplest code that satisfies the task's acceptance criteria.
  Predictable over clever; if a new reader wouldn't grasp it in ~30s, simplify.
- **YAGNI** — implement only what the approved spec requires *now*. No speculative
  config, hooks, parameters, or abstraction layers with a single caller.
- **DRY** — deduplicate *knowledge*, not look-alike code. Abstract on the third real
  repetition of the same concept; two similar blocks that change for different
  reasons stay separate (premature abstraction is worse than duplication).
- **SoC** — each module/function/layer has one reason to change; respect the layer
  boundaries declared in `plan.md` (no cross-layer leakage). Prefer composition
  over inheritance.

If the code as written violates one of these, refactor it within the same task
before committing — this is autonomous, no approval needed. If honoring a principle
would contradict the approved spec or plan, the spec/plan wins; note it in the
commit body.

Before each checkpoint, the local gates must be green: lint, type-check, tests
(same three gates as CI — see close phase).

## Phase: close (when the work is done)

1. **Detect the stack** from the repo's manifests — never assume:
   - Node/TS (`package.json` + lockfile): eslint · `tsc --noEmit` · vitest/jest,
     using the package manager the lockfile implies.
   - Python (`pyproject.toml` / `requirements*.txt`): ruff · mypy · pytest.
   - React: eslint · `tsc` · vitest/jest · production build.
2. **CI** (GitHub Actions, `.github/workflows/`):
   - If none exists: create one running install → lint → type-check → tests
     for the detected stack. Use Docker / service containers **only if the
     project already uses them** — Docker is never a prerequisite.
   - If CI exists: evolve the tests to cover the changes made; touch the CI
     config only if the change actually requires it.
3. Run the full local gate suite. All green before pushing.
4. **Push** the auxiliary branch to origin — automatic, no confirmation needed.
5. **Draft the PR (base: `develop`) and PAUSE.** Show title and description and
   wait for explicit approval before opening it.
   - Title: clear, objective, Conventional-Commits style.
   - Description: valid Markdown, exactly this template (no leading
     indentation — the `##` headings must start at column 0):

```markdown
## Summary
What changed and why, briefly.

## Notable Decisions
Key choices made, and meaningful alternatives rejected (with the reason).
(Spec-driven? Pull these from spec.md "Decisions taken".)

## Test Plan
How the change was verified / steps to reproduce the verification.
(Spec-driven? Derive from the acceptance criteria checklist.)
```

## Guardrails

- Never commit or push to `develop` or `main` directly.
- Never auto-merge; never force-push a shared branch.
- Never open the PR without explicit approval of title + description.
- If the stack or CI host is ambiguous, ask before generating CI.
- If `plan.md` flagged a PR-split decision, honor it: one branch/PR per slice.
