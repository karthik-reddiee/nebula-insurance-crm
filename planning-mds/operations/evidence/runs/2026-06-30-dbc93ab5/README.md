# Plan Run — F0038 2026-06-30-dbc93ab5

Base run evidence package for the `plan` action, Phase A (PM requirements),
`FEATURE_MODE=existing`. Per Feature Evidence Contract §8 this is the
non-feature base path; it carries the six base files only and no feature
evidence package.

## Status

`complete` — Phase A approved (G3) by operator on 2026-06-30.

## Evidence Index

Planning artifacts produced/updated by this run live in the feature folder, not
in this run folder:

- `planning-mds/features/F0038-neuron-day-at-a-glance-shell/PRD.md` (updated: Related User Stories + `## Screen Layouts (ASCII)`)
- `planning-mds/features/F0038-neuron-day-at-a-glance-shell/STATUS.md` (updated: Story Checklist + notes; provenance rows untouched)
- `planning-mds/features/F0038-neuron-day-at-a-glance-shell/README.md` (updated: Stories table)
- Stories authored this run:
  - `.../F0038-S0001-neuron-service-bootstrap.md`
  - `.../F0038-S0002-day-at-a-glance-shell-and-zone-dispatch.md`
  - `.../F0038-S0003-live-renewals-zone-read.md`
  - `.../F0038-S0004-stub-zones-inactive-payload.md`
  - `.../F0038-S0005-renewal-outreach-draft.md` (mutation — interaction contract)
  - `.../F0038-S0006-mock-send-and-workflow-transition.md` (mutation — interaction contract)
  - `.../F0038-S0007-crm-scope-guard.md`
  - `.../F0038-S0008-companion-telemetry-instrumentation.md`
- `planning-mds/features/STORY-INDEX.md` (regenerated)
- Trackers already carrying F0038 (verified consistent): `planning-mds/features/REGISTRY.md`, `planning-mds/features/ROADMAP.md`, `planning-mds/BLUEPRINT.md`
- KG: minimal F0038 stub in `planning-mds/knowledge-graph/feature-mappings.yaml` (unchanged — full bindings deferred to Phase B)

Base run files (this folder): `README.md`, `action-context.md`,
`artifact-trace.md`, `gate-decisions.md`, `commands.log`, `lifecycle-gates.log`.

## Validation Summary

Plan-action exit validation (see `lifecycle-gates.log` for per-invocation detail):

| # | Validator | Result |
|---|-----------|--------|
| 1 | `validate-stories.py {FEATURE_PATH}` | PASS (exit 0) |
| 2 | `generate-story-index.py` | PASS (exit 0) |
| 3 | `validate-trackers.py` | tracker-consistency PASS; overall exit 1 — **pre-existing, F0038-unrelated** relocated-evidence drift (operator-acknowledged) |
| 4 | `kg/validate.py --write-coverage-report` | SKIPPED — KG unchanged this run |
| 5 | `kg/validate.py` | PASS (exit 0) |
| 6 | `kg/validate.py --check-drift` | PASS (exit 0) |
| 7 | `validate_templates.py` | PASS (exit 0) |

`validate-feature-evidence.py` was correctly NOT run — no feature evidence package exists at plan.

## Open Follow-ups

- **Pre-existing, out-of-scope:** `validate-trackers.py` exit 1 from relocated feature-evidence packages (F0023, F0035/run 2026-05-24-c92b16b6, run 2026-06-03-7e8e0ddc) referencing `/mnt/c/...` absolute paths + missing artifacts. Needs a separate remediation effort (re-anchor paths / re-close those features); not part of F0038.
- **Phase B (Architect):** ADRs (persistence home, message envelope, zone-dispatch/head contract, token forwarding, component registry), engine endpoints, Casbin `renewal:draft_outreach`, and full KG bindings — a separate later plan run (gates G4/G5).
