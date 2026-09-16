# setvane-gate — Development

**Setvane Governance V1**

## Development Workflow

### Implementation Tasks

All implementation tasks MUST:
1. Carry a valid Linear task ID
2. Declare expected worktree, branch, and base SHA or base ref
3. Pass pre-mutation checklist
4. Leave changes uncommitted for review

Security-sensitive component changes MUST carry a HIGH RISK flag in the implementation report.

### Validation Commands

```bash
git --no-optional-locks status --short --branch
git diff --check
```

If a test suite or linter exists, run and report results.

### Policy Testing

Policy rules MUST be tested against both positive and negative cases.
A policy change without corresponding test coverage MUST be flagged as incomplete.

### LLM Integration Guardrail

Any integration of LLM capabilities into Gate MUST preserve the deterministic
decision boundary. The `decision` field in PolicyDecision MUST always be set by
deterministic policy code, never by LLM output.

### Future Skills

When implemented, per-repo gate skills will be added to `.agents/skills/`:
- `validate-policy`
- `evaluate-policy`
- `explain-decision`
