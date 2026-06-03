# F0019 — Submission Quoting, Proposal & Approval Workflow — Status

**Overall Status:** Planning complete — Phase A + Phase B approved (G5 architecture approval, user, 2026-06-01; ADR-025 Accepted). Ready for the feature action; implementation not started (0/8 stories).
**Last Updated:** 2026-06-02

## Story Checklist

| Story | Title | Status |
|-------|-------|--------|
| F0019-S0001 | Activate downstream submission workflow | Planned |
| F0019-S0002 | Submission quote/proposal packet lifecycle | Planned |
| F0019-S0003 | Underwriting approval checkpoint | Planned |
| F0019-S0004 | Bind decision and policy handoff | Planned |
| F0019-S0005 | Decline and withdraw terminal decisions | Planned |
| F0019-S0006 | Submission archive and deactivate | Planned |
| F0019-S0007 | Downstream submission pipeline list & workflow visibility | Planned |
| F0019-S0008 | Downstream submission workflow timeline & audit trail | Planned |

**Total Stories:** 8 · **Completed:** 0 / 8

## Planning Decisions (Locked 2026-06-01, plan G1)

- **Lifecycle:** full downstream path through Bind (`InReview → Quoted → BindRequested → Bound`, + `Declined`/`Withdrawn`).
- **Approval:** single authorized approver (audit + reason; extensible to maker-checker / authority-limits later).
- **Archive:** in scope now — terminal-state-only, explicit lifecycle action, audit-preserving (replaces F0006 soft-delete).
- **Packet:** thin CRM coordination record — *recorded, never computed*; reuses F0034 attributes + F0020 documents.

## Refinement Guardrails

- F0006 remains closed at `ReadyForUWReview`; downstream submission transitions must remain disabled until F0019 stories explicitly turn them on (S0001 owns the deliberate boundary move).
- The first F0019 story (S0001) owns activation of `ReadyForUWReview -> InReview` and the downstream state machine, with direct reference to F0006 as the prior workflow boundary, plus authorization changes, UI exposure, and regression coverage.
- F0019 refinement is complete only when the implementation contract identifies the code path, authorization changes, UI exposure, and regression coverage that deliberately move the shared submission workflow beyond F0006.
- F0019 owns the replacement submission archive/deactivate contract for F0006's descoped soft delete: terminal states only, explicit lifecycle action, list visibility, and audit retention (S0006) — no generic CRUD delete.
- **CRM workflow, not underwriting workbench:** no rating/pricing/scoring/quote-comparison. Quote figures are recorded reference values, never computed (enforced via PRD non-goals, packet contract, story acceptance criteria, a Phase B architecture decision, and a boundary regression).

## Required Signoff Roles (Set in Planning)

| Role | Required | Why Required | Set By | Date |
|------|----------|--------------|--------|------|
| Quality Engineer | Yes | Workflow state machine, approval/bind behavior, idempotency, and the boundary regression require test validation. | Architect | 2026-06-01 |
| Code Reviewer | Yes | Workflow orchestration, approval logic, and the recorded-not-computed boundary require independent review. | Architect | 2026-06-01 |
| Security Reviewer | Yes | F0019 introduces approval authority (`submission:approve`) and archive (`submission:archive`) authorization deltas plus an audit-bearing approval decision record. | Architect | 2026-06-01 |
| Architect | Yes | Downstream state-machine activation, single-approver model, packet contract, and the CRM-not-workbench boundary are explicit architecture decisions (ADR-025). | Architect | 2026-06-01 |
| DevOps | No | No new runtime infra, background workers, or deployment changes; the F0018 bind handoff is an in-process eventual signal. Revisit only if implementation adds async infrastructure. | Architect | 2026-06-01 |

> Finalized by the Architect in Phase B (G4/G5). Governing decision: ADR-025.

## Story Signoff Provenance

| Story | Role | Reviewer | Verdict | Evidence | Date | Notes |
|-------|------|----------|---------|----------|------|-------|
| F0019-S0001 | Quality Engineer | - | N/A | - | - | Populate after story breakdown is created. |
| F0019-S0001 | Code Reviewer | - | N/A | - | - | Populate after story breakdown is created. |
