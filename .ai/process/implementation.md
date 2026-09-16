# setvane-gate — Implementation Mode

**Setvane Governance V1**
**Inherits: setvane-ecosystem-governance/.ai/process/implementation.md**

## MODE=IMPLEMENTATION in setvane-gate

All canonical implementation rules apply. This file adds gate-specific constraints.

## Required Envelope Fields

```
TASK_ID:             # Linear task ID
MODE:                IMPLEMENTATION
REPOSITORY:          setvane-gate
EXPECTED_WORKTREE:   # expected Git worktree root
EXPECTED_BRANCH:     # e.g., main
BASE_SHA:            # expected HEAD SHA; use BASE_REF instead when appropriate
BASE_REF:            # explicit base ref; one of BASE_SHA or BASE_REF is required
SCOPE:               # specific files or subsystems
OUT_OF_SCOPE:        # explicitly excluded
ALLOWED_MUTATIONS:   # specific changes permitted
VALIDATION:          # at minimum: git diff --check
PROTECTED_OPERATIONS: # default: all (merge, rebase, etc.)
```

## Pre-Mutation Checklist

Before any file mutation:

1. Actual repository identity and repository root match setvane-gate?
2. Actual Git worktree root matches EXPECTED_WORKTREE?
3. On expected branch?
4. HEAD matches BASE_SHA or BASE_REF?
5. No unexpected dirty state?
6. Valid Linear task ID present?
7. Mutations within SCOPE?
8. Does change touch decision engine, policy parser, authorization contract,
   or expiry/replay behavior? (if yes: HIGH RISK, requires human review before merge)

If any check fails → `SAFE_TO_EDIT=NO` → STOP + REPORT.
Do not auto-switch repositories, branches, or worktrees.

## Gate-Specific Constraints

An implementation task in setvane-gate MUST NOT:

- Add an LLM output path that sets `decision` in PolicyDecision
- Remove or weaken fail-closed behavior
- Remove expiry or replay checks
- Reduce the determinism of policy evaluation

## Validation

```bash
git --no-optional-locks status --short --branch
git diff --check
```

Run policy tests if available. Report coverage gaps.

## Post-Mutation

Leave changes uncommitted. Report changed files and risk level.
Flag any security-sensitive component changes as HIGH RISK.
Human review is required before merge for HIGH RISK changes.
