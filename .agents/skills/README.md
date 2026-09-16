# setvane-gate — Skills

Skills define workflows within established authority. Skills do NOT grant permission.

## Available Skills

None implemented yet. Planned:

| Skill | Purpose |
|-------|---------|
| validate-policy | Validate a policy definition against Gate schema |
| evaluate-policy | Trace a policy evaluation against a given input (non-authoritative, for analysis) |
| explain-decision | Explain a PolicyDecision in human-readable terms |

These will be added as `.md` files in this directory when implemented.

## Critical: explain-decision Skill Constraint

The `explain-decision` skill produces an explanation of a decision.
It MUST NOT produce or modify a PolicyDecision.
It MUST NOT be used as a substitute for a deterministic Gate evaluation.

## Shared Skills

| Skill | Source |
|-------|--------|
| governance-review | `setvane-ecosystem-governance/.agents/skills/governance-review.md` |
| governance-implementation | `setvane-ecosystem-governance/.agents/skills/governance-implementation.md` |
| cross-repo-change | `setvane-ecosystem-governance/.agents/skills/cross-repo-change.md` |

## Skill Contract

A skill MUST NOT:
- Issue an authoritative `ALLOW` PolicyDecision
- Override deterministic policy evaluation
- Grant permission to execute privileged actions
