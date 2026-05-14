# F0018 — Policy Lifecycle & Policy 360 — Status

**Overall Status:** Done (Archived)
**Last Updated:** 2026-04-22

## Story Checklist

| Story | Title | Status |
|-------|-------|--------|
| F0018-S0001 | Policy list with search and filtering | Done |
| F0018-S0002 | Create policy (manual, import-lite, F0019 bind-hook contract) | Done |
| F0018-S0003 | Policy detail and profile edit | Done |
| F0018-S0004 | Policy 360 composed workspace | Done |
| F0018-S0005 | Immutable policy version snapshots and version history | Done |
| F0018-S0006 | Policy endorsement events and term changes | Done |
| F0018-S0007 | Policy cancellation (mid-term and flat) | Done |
| F0018-S0008 | Policy reinstatement within LOB-configurable window | Done |
| F0018-S0009 | Policy renewal linkage (predecessor / successor) | Done |
| F0018-S0010 | Policy activity timeline and audit trail | Done |
| F0018-S0011 | Policy summary projection for Account 360 | Done |

## Required Signoff Roles (Set in Planning)

| Role | Required | Why Required | Set By | Date |
|------|----------|--------------|--------|------|
| Quality Engineer | Yes | Workflow transition matrix, version/endorsement/cancellation/reinstatement semantics, ABAC scope coverage, reinstatement-window enforcement, rail-isolation tests, expiration-job idempotency. | Product Manager | 2026-04-18 |
| Code Reviewer | Yes | Policy aggregate modeling, version snapshot immutability, coverage-line materialization, atomic endorsement transactions, fallback-contract consumption. | Product Manager | 2026-04-18 |
| Security Reviewer | Yes | New `policy:*` Casbin actions, sensitive-data classification, reinstatement authority gate, cancellation reason-code governance, cross-role visibility on a hub entity. | Product Manager | 2026-04-18 |
| DevOps | Yes | New Policies / PolicyVersions / PolicyEndorsements / PolicyCoverageLines / CarrierRef migrations, index plan, CarrierRef seed, denormalized `AccountDisplayNameAtLink` backfill on policy rows, daily expiration job scheduling. | Product Manager | 2026-04-18 |
| Architect | Yes | New ADR(s) for policy aggregate + versioning + reinstatement-window category; extension of ADR-009 `WorkflowSlaThreshold` for `PolicyReinstatementWindow`; API-contract authority on `POST /api/policies/from-bind` hook consumed by F0019; integration surface with F0007 / F0016 / F0020. | Product Manager | 2026-04-18 |

## Story Signoff Provenance

| Story | Role | Reviewer | Verdict | Evidence | Date | Notes |
|-------|------|----------|---------|----------|------|-------|
| F0018-S0001 | Quality Engineer | Codex feature runner / Quality Engineer | PASS | `planning-mds/operations/evidence/f0018/g2-self-review-2026-04-22.md` | 2026-04-22 | PM closeout confirms story closed as Done. |
| F0018-S0001 | Code Reviewer | Codex feature runner / Code Reviewer | PASS | `planning-mds/operations/evidence/f0018/g3-code-review-2026-04-22.md` | 2026-04-22 | PM closeout confirms story closed as Done. |
| F0018-S0001 | Security Reviewer | Codex feature runner / Security Reviewer | PASS | `planning-mds/operations/evidence/f0018/g3-security-review-2026-04-22.md` | 2026-04-22 | PM closeout confirms story closed as Done. |
| F0018-S0001 | DevOps | Codex feature runner / DevOps | PASS | `planning-mds/operations/evidence/f0018/runtime-preflight-2026-04-22.md` | 2026-04-22 | PM closeout confirms story closed as Done. |
| F0018-S0001 | Architect | Codex feature runner / Architect | PASS | `planning-mds/operations/evidence/f0018/g2-self-review-2026-04-22.md` | 2026-04-22 | PM closeout confirms story closed as Done. |
| F0018-S0002 | Quality Engineer | Codex feature runner / Quality Engineer | PASS | `planning-mds/operations/evidence/f0018/g2-self-review-2026-04-22.md` | 2026-04-22 | PM closeout confirms story closed as Done. |
| F0018-S0002 | Code Reviewer | Codex feature runner / Code Reviewer | PASS | `planning-mds/operations/evidence/f0018/g3-code-review-2026-04-22.md` | 2026-04-22 | PM closeout confirms story closed as Done. |
| F0018-S0002 | Security Reviewer | Codex feature runner / Security Reviewer | PASS | `planning-mds/operations/evidence/f0018/g3-security-review-2026-04-22.md` | 2026-04-22 | PM closeout confirms story closed as Done. |
| F0018-S0002 | DevOps | Codex feature runner / DevOps | PASS | `planning-mds/operations/evidence/f0018/runtime-preflight-2026-04-22.md` | 2026-04-22 | PM closeout confirms story closed as Done. |
| F0018-S0002 | Architect | Codex feature runner / Architect | PASS | `planning-mds/operations/evidence/f0018/g2-self-review-2026-04-22.md` | 2026-04-22 | PM closeout confirms story closed as Done. |
| F0018-S0003 | Quality Engineer | Codex feature runner / Quality Engineer | PASS | `planning-mds/operations/evidence/f0018/g2-self-review-2026-04-22.md` | 2026-04-22 | PM closeout confirms story closed as Done. |
| F0018-S0003 | Code Reviewer | Codex feature runner / Code Reviewer | PASS | `planning-mds/operations/evidence/f0018/g3-code-review-2026-04-22.md` | 2026-04-22 | PM closeout confirms story closed as Done. |
| F0018-S0003 | Security Reviewer | Codex feature runner / Security Reviewer | PASS | `planning-mds/operations/evidence/f0018/g3-security-review-2026-04-22.md` | 2026-04-22 | PM closeout confirms story closed as Done. |
| F0018-S0003 | DevOps | Codex feature runner / DevOps | PASS | `planning-mds/operations/evidence/f0018/runtime-preflight-2026-04-22.md` | 2026-04-22 | PM closeout confirms story closed as Done. |
| F0018-S0003 | Architect | Codex feature runner / Architect | PASS | `planning-mds/operations/evidence/f0018/g2-self-review-2026-04-22.md` | 2026-04-22 | PM closeout confirms story closed as Done. |
| F0018-S0004 | Quality Engineer | Codex feature runner / Quality Engineer | PASS | `planning-mds/operations/evidence/f0018/g2-self-review-2026-04-22.md` | 2026-04-22 | PM closeout confirms story closed as Done. |
| F0018-S0004 | Code Reviewer | Codex feature runner / Code Reviewer | PASS | `planning-mds/operations/evidence/f0018/g3-code-review-2026-04-22.md` | 2026-04-22 | PM closeout confirms story closed as Done. |
| F0018-S0004 | Security Reviewer | Codex feature runner / Security Reviewer | PASS | `planning-mds/operations/evidence/f0018/g3-security-review-2026-04-22.md` | 2026-04-22 | PM closeout confirms story closed as Done. |
| F0018-S0004 | DevOps | Codex feature runner / DevOps | PASS | `planning-mds/operations/evidence/f0018/runtime-preflight-2026-04-22.md` | 2026-04-22 | PM closeout confirms story closed as Done. |
| F0018-S0004 | Architect | Codex feature runner / Architect | PASS | `planning-mds/operations/evidence/f0018/g2-self-review-2026-04-22.md` | 2026-04-22 | PM closeout confirms story closed as Done. |
| F0018-S0005 | Quality Engineer | Codex feature runner / Quality Engineer | PASS | `planning-mds/operations/evidence/f0018/g2-self-review-2026-04-22.md` | 2026-04-22 | PM closeout confirms story closed as Done. |
| F0018-S0005 | Code Reviewer | Codex feature runner / Code Reviewer | PASS | `planning-mds/operations/evidence/f0018/g3-code-review-2026-04-22.md` | 2026-04-22 | PM closeout confirms story closed as Done. |
| F0018-S0005 | Security Reviewer | Codex feature runner / Security Reviewer | PASS | `planning-mds/operations/evidence/f0018/g3-security-review-2026-04-22.md` | 2026-04-22 | PM closeout confirms story closed as Done. |
| F0018-S0005 | DevOps | Codex feature runner / DevOps | PASS | `planning-mds/operations/evidence/f0018/runtime-preflight-2026-04-22.md` | 2026-04-22 | PM closeout confirms story closed as Done. |
| F0018-S0005 | Architect | Codex feature runner / Architect | PASS | `planning-mds/operations/evidence/f0018/g2-self-review-2026-04-22.md` | 2026-04-22 | PM closeout confirms story closed as Done. |
| F0018-S0006 | Quality Engineer | Codex feature runner / Quality Engineer | PASS | `planning-mds/operations/evidence/f0018/g2-self-review-2026-04-22.md` | 2026-04-22 | PM closeout confirms story closed as Done. |
| F0018-S0006 | Code Reviewer | Codex feature runner / Code Reviewer | PASS | `planning-mds/operations/evidence/f0018/g3-code-review-2026-04-22.md` | 2026-04-22 | PM closeout confirms story closed as Done. |
| F0018-S0006 | Security Reviewer | Codex feature runner / Security Reviewer | PASS | `planning-mds/operations/evidence/f0018/g3-security-review-2026-04-22.md` | 2026-04-22 | PM closeout confirms story closed as Done. |
| F0018-S0006 | DevOps | Codex feature runner / DevOps | PASS | `planning-mds/operations/evidence/f0018/runtime-preflight-2026-04-22.md` | 2026-04-22 | PM closeout confirms story closed as Done. |
| F0018-S0006 | Architect | Codex feature runner / Architect | PASS | `planning-mds/operations/evidence/f0018/g2-self-review-2026-04-22.md` | 2026-04-22 | PM closeout confirms story closed as Done. |
| F0018-S0007 | Quality Engineer | Codex feature runner / Quality Engineer | PASS | `planning-mds/operations/evidence/f0018/g2-self-review-2026-04-22.md` | 2026-04-22 | PM closeout confirms story closed as Done. |
| F0018-S0007 | Code Reviewer | Codex feature runner / Code Reviewer | PASS | `planning-mds/operations/evidence/f0018/g3-code-review-2026-04-22.md` | 2026-04-22 | PM closeout confirms story closed as Done. |
| F0018-S0007 | Security Reviewer | Codex feature runner / Security Reviewer | PASS | `planning-mds/operations/evidence/f0018/g3-security-review-2026-04-22.md` | 2026-04-22 | PM closeout confirms story closed as Done. |
| F0018-S0007 | DevOps | Codex feature runner / DevOps | PASS | `planning-mds/operations/evidence/f0018/runtime-preflight-2026-04-22.md` | 2026-04-22 | PM closeout confirms story closed as Done. |
| F0018-S0007 | Architect | Codex feature runner / Architect | PASS | `planning-mds/operations/evidence/f0018/g2-self-review-2026-04-22.md` | 2026-04-22 | PM closeout confirms story closed as Done. |
| F0018-S0008 | Quality Engineer | Codex feature runner / Quality Engineer | PASS | `planning-mds/operations/evidence/f0018/g2-self-review-2026-04-22.md` | 2026-04-22 | PM closeout confirms story closed as Done. |
| F0018-S0008 | Code Reviewer | Codex feature runner / Code Reviewer | PASS | `planning-mds/operations/evidence/f0018/g3-code-review-2026-04-22.md` | 2026-04-22 | PM closeout confirms story closed as Done. |
| F0018-S0008 | Security Reviewer | Codex feature runner / Security Reviewer | PASS | `planning-mds/operations/evidence/f0018/g3-security-review-2026-04-22.md` | 2026-04-22 | PM closeout confirms story closed as Done. |
| F0018-S0008 | DevOps | Codex feature runner / DevOps | PASS | `planning-mds/operations/evidence/f0018/runtime-preflight-2026-04-22.md` | 2026-04-22 | PM closeout confirms story closed as Done. |
| F0018-S0008 | Architect | Codex feature runner / Architect | PASS | `planning-mds/operations/evidence/f0018/g2-self-review-2026-04-22.md` | 2026-04-22 | PM closeout confirms story closed as Done. |
| F0018-S0009 | Quality Engineer | Codex feature runner / Quality Engineer | PASS | `planning-mds/operations/evidence/f0018/g2-self-review-2026-04-22.md` | 2026-04-22 | PM closeout confirms story closed as Done. |
| F0018-S0009 | Code Reviewer | Codex feature runner / Code Reviewer | PASS | `planning-mds/operations/evidence/f0018/g3-code-review-2026-04-22.md` | 2026-04-22 | PM closeout confirms story closed as Done. |
| F0018-S0009 | Security Reviewer | Codex feature runner / Security Reviewer | PASS | `planning-mds/operations/evidence/f0018/g3-security-review-2026-04-22.md` | 2026-04-22 | PM closeout confirms story closed as Done. |
| F0018-S0009 | DevOps | Codex feature runner / DevOps | PASS | `planning-mds/operations/evidence/f0018/runtime-preflight-2026-04-22.md` | 2026-04-22 | PM closeout confirms story closed as Done. |
| F0018-S0009 | Architect | Codex feature runner / Architect | PASS | `planning-mds/operations/evidence/f0018/g2-self-review-2026-04-22.md` | 2026-04-22 | PM closeout confirms story closed as Done. |
| F0018-S0010 | Quality Engineer | Codex feature runner / Quality Engineer | PASS | `planning-mds/operations/evidence/f0018/g2-self-review-2026-04-22.md` | 2026-04-22 | PM closeout confirms story closed as Done. |
| F0018-S0010 | Code Reviewer | Codex feature runner / Code Reviewer | PASS | `planning-mds/operations/evidence/f0018/g3-code-review-2026-04-22.md` | 2026-04-22 | PM closeout confirms story closed as Done. |
| F0018-S0010 | Security Reviewer | Codex feature runner / Security Reviewer | PASS | `planning-mds/operations/evidence/f0018/g3-security-review-2026-04-22.md` | 2026-04-22 | PM closeout confirms story closed as Done. |
| F0018-S0010 | DevOps | Codex feature runner / DevOps | PASS | `planning-mds/operations/evidence/f0018/runtime-preflight-2026-04-22.md` | 2026-04-22 | PM closeout confirms story closed as Done. |
| F0018-S0010 | Architect | Codex feature runner / Architect | PASS | `planning-mds/operations/evidence/f0018/g2-self-review-2026-04-22.md` | 2026-04-22 | PM closeout confirms story closed as Done. |
| F0018-S0011 | Quality Engineer | Codex feature runner / Quality Engineer | PASS | `planning-mds/operations/evidence/f0018/g2-self-review-2026-04-22.md` | 2026-04-22 | PM closeout confirms story closed as Done. |
| F0018-S0011 | Code Reviewer | Codex feature runner / Code Reviewer | PASS | `planning-mds/operations/evidence/f0018/g3-code-review-2026-04-22.md` | 2026-04-22 | PM closeout confirms story closed as Done. |
| F0018-S0011 | Security Reviewer | Codex feature runner / Security Reviewer | PASS | `planning-mds/operations/evidence/f0018/g3-security-review-2026-04-22.md` | 2026-04-22 | PM closeout confirms story closed as Done. |
| F0018-S0011 | DevOps | Codex feature runner / DevOps | PASS | `planning-mds/operations/evidence/f0018/runtime-preflight-2026-04-22.md` | 2026-04-22 | PM closeout confirms story closed as Done. |
| F0018-S0011 | Architect | Codex feature runner / Architect | PASS | `planning-mds/operations/evidence/f0018/g2-self-review-2026-04-22.md` | 2026-04-22 | PM closeout confirms story closed as Done. |

---

## PM Closeout - 2026-04-22

**Final Overall Status:** Done; archive transition approved.  
**Implementation Run ID:** `5ab6f922-bf43-4702-9393-ea8a88c213b8`  
**Primary Evidence:** `planning-mds/operations/evidence/f0018/g45-signoff-2026-04-22.md`

### Final Story Status

| Story | Final Status | Evidence |
|-------|--------------|----------|
| F0018-S0001 | Done | `planning-mds/operations/evidence/f0018/g45-signoff-2026-04-22.md` |
| F0018-S0002 | Done | `planning-mds/operations/evidence/f0018/g45-signoff-2026-04-22.md` |
| F0018-S0003 | Done | `planning-mds/operations/evidence/f0018/g45-signoff-2026-04-22.md` |
| F0018-S0004 | Done | `planning-mds/operations/evidence/f0018/g45-signoff-2026-04-22.md` |
| F0018-S0005 | Done | `planning-mds/operations/evidence/f0018/g45-signoff-2026-04-22.md` |
| F0018-S0006 | Done | `planning-mds/operations/evidence/f0018/g45-signoff-2026-04-22.md` |
| F0018-S0007 | Done | `planning-mds/operations/evidence/f0018/g45-signoff-2026-04-22.md` |
| F0018-S0008 | Done | `planning-mds/operations/evidence/f0018/g45-signoff-2026-04-22.md` |
| F0018-S0009 | Done | `planning-mds/operations/evidence/f0018/g45-signoff-2026-04-22.md` |
| F0018-S0010 | Done | `planning-mds/operations/evidence/f0018/g45-signoff-2026-04-22.md` |
| F0018-S0011 | Done | `planning-mds/operations/evidence/f0018/g45-signoff-2026-04-22.md` |

### Signoff Provenance

| Role | Verdict | Reviewer | Date | Evidence |
|------|---------|----------|------|----------|
| Architect | PASS | Codex feature runner | 2026-04-22 | `planning-mds/operations/evidence/f0018/g2-self-review-2026-04-22.md` |
| DevOps | PASS | Codex feature runner | 2026-04-22 | `planning-mds/operations/evidence/f0018/runtime-preflight-2026-04-22.md` |
| Quality Engineer | PASS | Codex feature runner | 2026-04-22 | `planning-mds/operations/evidence/f0018/g2-self-review-2026-04-22.md` |
| Code Reviewer | PASS | Codex feature runner | 2026-04-22 | `planning-mds/operations/evidence/f0018/g3-code-review-2026-04-22.md` |
| Security Reviewer | PASS | Codex feature runner | 2026-04-22 | `planning-mds/operations/evidence/f0018/g3-security-review-2026-04-22.md` |

### Mitigation Notes

- Repaired before signoff: `/policies/from-bind` no longer returns 501 and now accepts the OpenAPI contract request.
- Repaired before signoff: policy create and lifecycle mutation paths now enforce scoped account/broker visibility before writes.
- Repaired before signoff: dashboard renewal aging handles LOB-specific SLA threshold rows without duplicate-key failures.

### Deferred Non-Blocking Follow-ups

- Add policy-specific integration tests for `/policies/from-bind` and scoped write-denial paths.
- Replace count-based policy-number allocation with a dedicated sequence-row implementation when concurrent policy creation is hardened.

### Orphaned Story Review

No orphaned stories. All F0018 stories are closed as Done with required role signoff evidence.
