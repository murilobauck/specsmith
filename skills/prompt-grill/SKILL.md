---
name: prompt-grill
description: Interrogates the user about a vague plan, feature, or prompt until reaching complete understanding, resolving every branch of the decision tree before any implementation. Use ALWAYS when the user requests a new feature, describes an ambiguous task, says "grill me", "interview me", "refine this prompt", or when a request has more than one possible interpretation — even if they don't ask for it explicitly.
---

# Prompt Grill

Goal: turn vague requests into assertive specifications BEFORE writing any code.

## Interview rules

1. Ask ONE question at a time via the AskUserQuestion tool. Never dump a questionnaire.
2. Each question offers 2-3 options; the recommended one comes first with "(Recommended)"
   in the label, and each option's `description` states the trade-off in one line.
3. Walk the decision tree in order, advancing only once the current branch is resolved:
   - (a) problem and target user
   - (b) measurable success criteria
   - (c) explicit IN / OUT scope
   - (d) data and contracts (inputs, outputs, schemas)
   - (e) edge cases and failure modes
   - (f) constraints (performance, cost, deadline, privacy/compliance)
   - (g) technical decisions
4. When an answer opens a new branch, pursue it before moving on.
5. Stop when you can write the spec without any "probably" or "assuming that".

## Required output

At the end, write `specs/<feature>/spec.md` in the user's project (create the
directory if needed). Use the section structure below directly — do not depend
on a template file existing in the project. If the project already has
`specs/_template/spec.md` (e.g. after running `specsmith-init`), follow that
template's structure instead.

- Context and problem (2-3 sentences)
- Verifiable acceptance criteria (checklist)
- Out of scope (explicit)
- Data contracts (inputs, outputs, schemas)
- Edge cases mapped
- Decisions taken + rejected alternatives and why
- Open questions (if any remain, flag them as risks)

Once the spec is approved, follow the flow in `specs/README.md`:
spec.md approved → plan.md approved (declares the branch) → tasks.md → lifecycle kickoff (branch) → code (1 commit per task, checkpoint phase) → lifecycle close (tests/CI → push → PR draft, pause) — git mechanics per the dev-lifecycle skill.
