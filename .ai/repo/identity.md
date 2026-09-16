# setvane-gate — Repository Identity

**Setvane Governance V1**
**canonical_governance_version: v1**
**canonical_governance_source: setvane-ecosystem-governance**

## Identity

| Field | Value |
|-------|-------|
| Name | setvane-gate |
| Profile | gate |
| Visibility | public |
| Role | Deterministic policy authority |
| Contract role | PolicyDecision producer |

## Purpose

setvane-gate evaluates ChangeProposals and EvidenceEnvelopes against deterministic policy.
It emits bounded PolicyDecisions: `ALLOW`, `DENY`, or `REQUIRE_APPROVAL`.

Gate does not execute changes. Gate does not delegate authoritative decisions to AI.

## Inheritance

Inherits all governance invariants from:
1. Company / Wildcode Global Safety
2. Setvane Product Governance (setvane-ecosystem-governance, v1)

This file adds only setvane-gate specializations.
