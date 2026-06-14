# Plan — <feature name>

> Only write this after `spec.md` is approved.
> An approved plan triggers the **kickoff** phase of the `dev-lifecycle` skill (branch creation).

## Branch and delivery

- **Branch:** `<type>/<kebab-case-description>` (base: `develop`, in English)
- **PR slicing:** <single PR | N PRs — if >~10 tasks or independent slices across
  layers, split into reviewable PRs and list the slices here>

## Technical approach

<2-4 sentences: the high-level implementation strategy.>

## Affected files (by layer)

> Adapt the layers to your project's architecture (Node/TS, React, Python, etc.).
> The rows below are illustrative — replace them with your stack's structure.

| Layer | File | Change |
|---|---|---|
| <e.g. Router / Controller> | `<path>` | <...> |
| <e.g. Service> | `<path>` | <...> |
| <e.g. Repository / Data> | `<path>` | <...> |
| <e.g. Model / Entity> | `<path>` | <...> |
| <e.g. Migration> | `<path>` | <if there's a schema change> |

## Risks and mitigation

| Risk | Mitigation |
|---|---|
| <...> | <...> |

## Rollback and reversibility

- Migration: `downgrade()` implemented and **tested** (upgrade → downgrade → upgrade green).
- Reversal plan: <e.g. reverting the PR is enough | requires manual step X — describe>.
- <If irreversible (e.g. dropping a column with data), flag as a risk and require explicit approval.>

## Testing strategy

- Unit: <business logic in the service>
- Integration: <I/O — DB, queues, external APIs>
- E2E: <only for critical flows>
- Target coverage: ≥ 90% on core modules; 100% on critical logic.
  Justify exceptions in the PR (Notable Decisions).

## Observability / performance (if any LLM)

- Log tokens, latency, and cost per LLM call. No blind calls.
- Justify the model choice (cheap solves it → small model).
- Independent I/O in parallel; no N+1; pagination on lists.
