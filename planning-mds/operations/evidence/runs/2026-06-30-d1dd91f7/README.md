# Plan Run — F0038 2026-06-30-d1dd91f7

Base run evidence package for the `plan` action, Phase B (Architect
architecture), `FEATURE_MODE=existing`. Per Feature Evidence Contract §8 this is
the non-feature base path; it carries the six base files only and no feature
evidence package.

## Status

`complete` — Phase B architecture **APPROVED** by operator (G5, 2026-06-30). G4
ontology sync passed; exit validation complete (one acknowledged pre-existing
tracker exception). The operator also requested and received the template-drift
fix in `agents/templates/prompts/evidence-contract/plan-operator-friendly.md`
(framework workstream; `validate_templates.py` re-run exit 0).

## Evidence Index

Architecture artifacts produced/updated by this run live in
`planning-mds/architecture/`, `planning-mds/api/`, `planning-mds/schemas/`,
`planning-mds/knowledge-graph/`, `planning-mds/BLUEPRINT.md`, and the feature
folder — not in this run folder. The authoritative list is maintained in
`artifact-trace.md`; summary pointers:

- `planning-mds/architecture/decisions/ADR-027-neuron-companion-a2a-orchestration.md` (ratified at Phase B; follow-ups executed)
- `planning-mds/architecture/decisions/ADR-028-*` (new Phase B ADR — cross-store write consistency / neuron persistence; see artifact-trace)
- `planning-mds/architecture/data-model.md` (neuron.* operation schema)
- `planning-mds/api/*.yaml` (engine reads/writes + mock-send; neuron message/action endpoints)
- `planning-mds/schemas/*.json` (message envelope, agent card manifest, YAML plan)
- `planning-mds/BLUEPRINT.md` §4 (Neuron companion architecture)
- `planning-mds/features/F0038-neuron-day-at-a-glance-shell/README.md` (feature ERD + C4)
- `planning-mds/knowledge-graph/feature-mappings.yaml` (F0038 promoted out of `excluded_features`; 8 story bindings)
- `planning-mds/knowledge-graph/canonical-nodes.yaml` (new shared Neuron semantics)

Base run files (this folder): `README.md`, `action-context.md`,
`artifact-trace.md`, `gate-decisions.md`, `commands.log`, `lifecycle-gates.log`.

## Validation Summary

Full per-invocation detail in `lifecycle-gates.log`.

| # | Validator | Result |
|---|-----------|--------|
| G4a | `kg/validate.py --write-coverage-report` | PASS (exit 0) |
| G4b | `kg/validate.py` | PASS (exit 0) — features 28, stories 137, **0 uncovered** |
| G4c | `kg/validate.py --check-drift` | PASS (exit 0) |
| 1 | `validate-stories.py {FEATURE_PATH}` | PASS (exit 0; non-blocking INVEST warns) |
| 2 | `generate-story-index.py` | PASS (exit 0; STORY-INDEX regenerated) |
| 3 | `validate-trackers.py` | tracker-consistency PASS (`errors: 0`); overall exit 1 — **pre-existing, F0038-unrelated** relocated-evidence drift (operator-acknowledged) |
| 4 | `kg/validate.py --write-coverage-report` | PASS (exit 0) |
| 5 | `kg/validate.py` | PASS (exit 0) |
| 6 | `kg/validate.py --check-drift` | PASS (exit 0) |
| 7 | `validate_templates.py` | PASS (exit 0) |

`validate-feature-evidence.py` correctly NOT run — no feature evidence package at plan.

## Open Follow-ups

- **Pre-existing, out-of-scope:** `validate-trackers.py` exit 1 from relocated
  feature-evidence packages (F0023, F0035, runs referencing `/mnt/c/...`).
  Carried forward from run `2026-06-30-dbc93ab5`; not part of F0038.
- **Template/action drift (this run):** RESOLVED. Per operator direction,
  `agents/templates/prompts/evidence-contract/plan-operator-friendly.md` was
  repaired so it no longer lists `feature-assembly-plan.md` as a Phase B
  plan-action deliverable (re-aligned with `plan.md` / `agent-map.yaml`;
  `validate_templates.py` re-run exit 0). Framework workstream, separate from the
  F0038 product artifacts.
