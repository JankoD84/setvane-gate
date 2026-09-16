# setvane-gate — Authority

**Setvane Governance V1**
**Inherits: setvane-ecosystem-governance/profiles/gate.md**

## Authority

```
GATE = DETERMINISTIC POLICY EVALUATION + ALLOW / DENY / REQUIRE_APPROVAL
```

## Decision Bounds

Gate MUST emit only these decisions:

| Decision | Meaning |
|----------|---------|
| `ALLOW` | Action permitted within stated scope and expiry |
| `DENY` | Action not permitted |
| `REQUIRE_APPROVAL` | Non-executable; approval triggers Gate re-evaluation and a new `ALLOW` |

No other decision values are valid. Human approval does not directly unlock execution;
only a new, current, matching, unexpired `ALLOW` is executable.

## Determinism Requirement

Gate decisions MUST be deterministic and code/policy driven.

An LLM output MUST NOT be accepted as an authoritative `ALLOW` decision.

AI MAY: explain policies, summarize rationale, suggest new rules for human review.
AI MUST NOT: independently issue authoritative `ALLOW`.

## Fail-Closed Requirement

Gate MUST emit `DENY` when:

- Policy missing, malformed, or incompatible
- Required evidence missing or stale
- Scope mismatch between proposal and policy
- Target mismatch between proposal and policy
- Authorization expired or not yet valid
- Decision cannot be made deterministically

## Execution Boundary

Gate evaluates and decides. Gate does NOT execute.

```
GATE DECISION != EXECUTION RESULT
```

The execution actor is separate from Gate. Gate's PolicyDecision authorizes execution;
it does not perform execution. Rollback is a distinct privileged action and requires
its own PolicyDecision in V1.
