# Action Context

## Run Identity

- Action: `plan` (`agents/actions/plan.md`)
- Phase: `B` — Architect architecture
- Feature: `F0038`
- Feature mode: `existing`
- Run: `2026-06-30-d1dd91f7`
- Evidence profile: base run (non-feature) per Feature Evidence Contract §8
- Product root: `/home/gajap/uSandbox/repos/nebula/nebula-insurance-crm`
- Feature path: `planning-mds/features/F0038-neuron-day-at-a-glance-shell`
- Plan run folder: `planning-mds/operations/evidence/runs/2026-06-30-d1dd91f7`
- Feature index root: `planning-mds/operations/evidence/features/F0038-neuron-day-at-a-glance-shell` (NOT created during plan; created later by `agents/actions/feature.md`)
- Prior run: `2026-06-30-dbc93ab5` (Phase A — PM requirements, approved at G3)

## Lifecycle Stage

Plan action — Phase B (Architect architecture). Phase A (`2026-06-30-dbc93ab5`)
is complete and operator-approved (G3, 2026-06-30T11:35). This run produces the
architecture artifacts (ADR ratification + Phase B follow-ups, data model, API
contracts, JSON schemas, authorization delta, BLUEPRINT §4, feature README
ERD/C4) and completes the F0038 KG ontology bindings. No feature evidence
package is created at plan; `validate-feature-evidence.py` is not invoked.

## Phase Compatibility

`PHASE=B` + `FEATURE_MODE=existing` → architect updates architecture artifacts
and finalizes ontology bindings. The feature folder already contains `PRD.md`,
8 stories, and a populated `STATUS.md` skeleton, satisfying the `existing`
precondition.

## Retrieval Posture

- Plan mode = `refinement` (FEATURE_MODE=existing): start_tier 2, max_auto_tier 3.
- KG `lookup.py F0038` returns an `excluded` skeleton stub — Phase B authors the
  full mapping that moves F0038 out of `excluded_features`. Raw feature folder,
  intake brief, ADR-027, and the C4 doc are authoritative.
- `kg/validate.py` exit 0 confirmed before this folder was initialized.

## Governing Prior Decisions (read, not re-litigated)

- `intake-brief.md` — signed-off stakeholder source (locked decisions L1–L8). The
  architect must not invent rules beyond it.
- `ADR-027-neuron-companion-a2a-orchestration.md` — Accepted (operator direction);
  this run is its explicit Phase B ratification/refinement checkpoint and executes
  its four unchecked Phase B follow-ups.
- `c4-neuron-companion.md` — existing C4 view for the companion.

## Gates In Scope (Phase B)

- `G4 ONTOLOGY SYNC (B)` (Step 3.5) — feature-mappings / canonical-nodes /
  solution-ontology aligned with the assembly plan; `kg/validate.py` and
  `--check-drift` exit 0.
- `G5 PHASE B APPROVAL` (Step 4) — operator reviews architecture; decision
  recorded in `gate-decisions.md`. Cannot be self-approved.

`G1`/`G2`/`G3` were completed by the Phase A run (`2026-06-30-dbc93ab5`).

## Deliverable-Scope Reconciliation (noted at run start)

The operator prompt (`plan-operator-friendly.md`) lists `feature-assembly-plan.md`
among Phase B deliverables. `agents/actions/plan.md` → Deliverables Contract
states the assembly plan is **not** a plan deliverable (it belongs to
`agents/actions/feature.md` Step 0), and `agents/agent-map.yaml` wires
`feature-assembly-planning` to the `feature`/`build` actions, not `plan`. Per the
prompt's own conflict-resolution rule (raw artifacts/action doc win), this run
follows `plan.md`: it produces the architecture spec and KG bindings and does
**not** author `feature-assembly-plan.md`. Reconciliation logged in
`gate-decisions.md`.
