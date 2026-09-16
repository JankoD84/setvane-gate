# AGENTS.md — setvane-gate

## Repository Identity

| Field | Value |
|-------|-------|
| Repository | setvane-gate |
| Profile | gate |
| Visibility | **Public** |
| Governance version | Setvane Governance V1 |
| Canonical governance | setvane-ecosystem-governance |
| Linear | DUL-742 |

## Authority Boundary

```
GATE = DETERMINISTIC POLICY EVALUATION + ALLOW / DENY / REQUIRE_APPROVAL
```

Gate is the **authoritative policy decision authority** for the Setvane ecosystem.

### Authorized

`EVALUATE` — `ALLOW` — `DENY` — `REQUIRE_APPROVAL`

All decisions are deterministic and code/policy driven. `REQUIRE_APPROVAL` is not
executable; approval triggers Gate re-evaluation and a new `ALLOW`.

### LLM Restriction

```
AI RECOMMENDATION != GATE DECISION
LLM OUTPUT        != AUTHORITATIVE ALLOW
```

An AI agent MUST NOT issue an authoritative `ALLOW` on behalf of Gate.

### Fail-Closed

Gate MUST emit `DENY` when policy is missing, malformed, evidence is missing or stale,
scope/target mismatch, or when the decision cannot be made deterministically.

## Security-Sensitive Components

Changes to the following require strong human review before merge:

- Decision engine
- Policy parser
- Authorization contract
- Expiry and replay prevention behavior

## Cross-Repo Role

setvane-gate is the **authoritative producer** of `PolicyDecision`.
setvane-gate is a consumer of `EvidenceEnvelope` and `ChangeProposal`.

## Execution Modes

**MODE=REVIEW** — inspect, analyze, report. No mutations.

**MODE=IMPLEMENTATION** — requires TASK_ID, EXPECTED_WORKTREE, EXPECTED_BRANCH,
BASE_SHA or BASE_REF, and SCOPE.
Security-sensitive changes require HIGH RISK flag and human review.
See `.ai/process/implementation.md`.

## Git Safety

Protected operations require explicit human approval.
Wrong repo/branch/worktree or unexpected dirty state → `SAFE_TO_EDIT=NO` → STOP + REPORT.

## Linear Binding

Every non-trivial implementation MUST carry a valid Linear task ID.

## Public Disclosure

This repository is **public**. All committed content MUST comply with public disclosure rules.

MUST NOT expose: secrets, tokens, private keys, internal IPs, internal hostnames,
customer data, private operational procedures.

## Canonical Reference

Full governance: `setvane-ecosystem-governance`

| Topic | Canonical file |
|-------|---------------|
| Gate profile | `setvane-ecosystem-governance/profiles/gate.md` |
| Policy decision contract | `setvane-ecosystem-governance/contracts/policy-decision-contract.md` |
| Authorization rules | `setvane-ecosystem-governance/.ai/governance/authorization.md` |
| Trust model | `setvane-ecosystem-governance/docs/trust-model.md` |
