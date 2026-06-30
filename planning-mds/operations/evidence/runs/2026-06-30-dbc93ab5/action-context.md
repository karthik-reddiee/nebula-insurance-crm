# Action Context

## Run Identity

- Action: `plan` (`agents/actions/plan.md`)
- Phase: `A` — Product Manager requirements
- Feature: `F0038`
- Feature mode: `existing`
- Run: `2026-06-30-dbc93ab5`
- Evidence profile: base run (non-feature) per Feature Evidence Contract §8
- Product root: `/home/gajap/uSandbox/repos/nebula/nebula-insurance-crm`
- Feature path: `planning-mds/features/F0038-neuron-day-at-a-glance-shell`
- Plan run folder: `planning-mds/operations/evidence/runs/2026-06-30-dbc93ab5`
- Feature index root: `planning-mds/operations/evidence/features/F0038-neuron-day-at-a-glance-shell` (NOT created during plan; created later by `agents/actions/feature.md`)
- Prior run: `None`

## Lifecycle Stage

Plan action — Phase A (PM requirements). Produces planning artifacts in the
feature folder plus this base run evidence package. No feature evidence package
is created at plan; `validate-feature-evidence.py` is not invoked during this run.

## Retrieval Posture

- Plan mode = `refinement` (FEATURE_MODE=existing): start_tier 2, max_auto_tier 3.
- KG `lookup.py F0038` returned an excluded skeleton stub (no mappings yet);
  raw feature folder + trackers are authoritative.
- Session setup checks (`kg/validate.py` exit 0; `lookup.py F0038`) were run
  before this folder was initialized; they are recorded in `artifact-trace.md`.

## Gates In Scope (Phase A)

- `G1 CLARIFICATION` (Step 1.5) — PM resolves open requirement questions with the user.
- `G2 TRACKER SYNC (A)` (Step 1.75) — REGISTRY / ROADMAP / BLUEPRINT / STORY-INDEX sync.
- `G3 PHASE A APPROVAL` (Step 2) — user reviews requirements; decision recorded in `gate-decisions.md`.

`G4 ONTOLOGY SYNC (B)` and `G5 PHASE B APPROVAL` are out of scope for this PHASE=A run.
