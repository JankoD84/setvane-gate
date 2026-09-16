# setvane-gate — Review Mode

**Setvane Governance V1**
**Inherits: setvane-ecosystem-governance/.ai/process/review.md**

## MODE=REVIEW in setvane-gate

Review mode is read-only. No file mutations.

### Gate-Specific Review Scope

Review mode in setvane-gate MAY include:
- Reviewing policy definitions
- Reviewing decision engine logic
- Reviewing PolicyDecision schema
- Reviewing expiry and replay behavior
- Reviewing LLM integration boundaries (verifying no LLM can set `decision=ALLOW`)
- Reviewing fail-closed behavior

### Security Review Checklist

During review of Gate, verify:

| Check | Expected |
|-------|----------|
| LLM cannot set authoritative decision | CONFIRMED |
| Fail-closed on missing policy | CONFIRMED |
| Fail-closed on stale evidence | CONFIRMED |
| Scope mismatch → DENY | CONFIRMED |
| Expiry checked before emitting ALLOW | CONFIRMED |
| replay protection present | CONFIRMED |

### What Review Mode MUST NOT Do

- Modify policy files
- Execute Gate evaluation against live requests
- Commit or push files
