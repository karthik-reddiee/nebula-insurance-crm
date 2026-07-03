# F0038 — Neuron Day-at-a-Glance Shell — Status

**Overall Status:** Planned — Phase A approved (plan run `2026-06-30-dbc93ab5`) and Phase B architecture **approved** (plan run `2026-06-30-d1dd91f7`, G5 operator approval 2026-06-30). Ready for the `feature` action (after the AI Engineer role buildout prerequisite).
**Last Updated:** 2026-06-30

> Phase A (PM requirements) complete + approved (G3). Phase B (architecture)
> authored at plan run `2026-06-30-d1dd91f7`: ADR-027 ratified + ADR-028 (persistence
> schema, cross-store write consistency, outreach authorization), `neuron.*` data
> model, Neuron + engine API contracts, 8 JSON schemas, `renewal:draft_outreach`
> Casbin rule, BLUEPRINT §4.7, feature ERD/C4, and full KG ontology bindings
> (G4 ontology sync PASSED). **G5 operator approval granted 2026-06-30.** The Story
> Signoff Provenance rows remain placeholders until reviews run during the `feature`
> action (rows are append-only audit history).

## Story Checklist

| Story | Title | Status |
|-------|-------|--------|
| F0038-S0001 | Neuron service bootstrap (runtime + registries + versioned orchestration) | Not Started |
| F0038-S0002 | Day-at-a-Glance shell + zone-dispatch + message/component envelope | Not Started |
| F0038-S0003 | Live Renewals zone (needs-attention list + drill context) | Not Started |
| F0038-S0004 | Stub zones — inert "not yet active" payload | Not Started |
| F0038-S0005 | Renewal outreach draft (generate-on-click, persist, edit in-chat) | Not Started |
| F0038-S0006 | Mock-send (commit `Identified → Outreach`, fake SMTP) | Not Started |
| F0038-S0007 | CRM-scope guard (out-of-scope → polite redirect) | Not Started |
| F0038-S0008 | Companion telemetry (baseline timestamps + minimal secondary metrics) | Not Started |

## Required Signoff Roles (Set in Planning)

| Role | Required | Why Required | Set By | Date |
|------|----------|--------------|--------|------|
| Quality Engineer | Yes | Acceptance-criteria + telemetry/workflow-transition validation. | Architect | TBD |
| Code Reviewer | Yes | Independent review of zone-dispatch, draft write, and mock-send logic. | Architect | TBD |
| Security Reviewer | Yes | Token forwarding (on-behalf-of), new Casbin `renewal:draft_outreach`, audit/provenance, prompt-injection surface, and no model-generated markup execution. | Architect | TBD |
| AI Engineer | Yes | `neuron/` bootstrap, classifier, A2A-aligned internal delegation, versioned YAML orchestration, specialist head registry, message/component contract, prompt provenance, and scope guard. | Architect | TBD |
| DevOps | Yes | First runnable Neuron service likely changes runtime/env/container/health-check contracts; confirm exact scope during plan. | Architect | TBD |
| Architect | Yes | Persistence/envelope/head-contract/A2A-profile/token-forwarding/component-contract/orchestration ADRs require explicit approval. | Architect | TBD |

## Story Signoff Provenance

| Story | Role | Reviewer | Verdict | Evidence | Date | Notes |
|-------|------|----------|---------|----------|------|-------|
| F0038-S0001 | Quality Engineer | - | N/A | - | - | Populate after story breakdown is created in the plan run. |
| F0038-S0001 | Code Reviewer | - | N/A | - | - | Populate after story breakdown is created in the plan run. |

## Notes

- Source of truth for scope: [`intake-brief.md`](./intake-brief.md) (signed off 2026-06-29).
- This feature is **not blocked on F0021** (interim timeline-event home + mock-send now).
- **G1 product decision (2026-06-30):** the non-live zones (Tasks, Pipeline, Broker activity) are **shown as visible "not yet active" stubs**, not hidden until live — resolving the intake brief's lone open micro-decision (§5 "confirm vs hiding-until-live"). This advertises the multi-head pathway and sets up F0040's "flip a stub to live."
- **G1 decisions:** 8 fine-grained vertical slices (vs coarser bundling); personas reused from `nebula-personas.md` (no new persona files). Plan run `2026-06-30-dbc93ab5`, base evidence at `planning-mds/operations/evidence/runs/2026-06-30-dbc93ab5/`.
- KG: F0038 feature-mapping remains a minimal stub in `feature-mappings.yaml` (`excluded_features`); full ontology bindings are authored by the architect in Phase B (per plan-action ownership split).
