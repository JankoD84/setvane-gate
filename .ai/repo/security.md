# setvane-gate — Security

**Setvane Governance V1**

## Security-Critical Repository

setvane-gate is the policy authority for the Setvane ecosystem.
Defects in Gate can result in unauthorized execution or unauthorized denial.
Both outcomes have security implications.

## Security-Sensitive Components

Changes to the following components MUST receive strong human review before merge:

| Component | Risk |
|-----------|------|
| Decision engine | Incorrect decisions — unauthorized ALLOW or erroneous DENY |
| Policy parser | Malformed policy accepted or valid policy rejected |
| Authorization contract | PolicyDecision schema — affects all consumers |
| Expiry behavior | Stale decisions accepted or fresh decisions wrongly rejected |
| Replay prevention | Replay attacks through reused decisions |

These changes MUST be flagged `HIGH RISK` in implementation reports.

## LLM Non-Delegation Enforcement

Any code path that allows an LLM to determine the value of `decision` in a PolicyDecision
MUST be treated as a critical security defect and reported immediately.

## Public Repository Rules

setvane-gate is public. The following MUST NOT appear in any committed file:

- Secrets, API keys, tokens, private keys
- Internal IP addresses or hostnames
- Customer data
- Internal incident details
- Unpublished vulnerability details

Policy rules and Gate decision logic may be public.

## Git Safety

Protected operations require explicit human approval.
Wrong repo/branch/worktree or unexpected dirty state:
```
SAFE_TO_EDIT = NO
ACTION = STOP + REPORT
```
