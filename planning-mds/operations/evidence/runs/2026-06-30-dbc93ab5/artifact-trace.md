# Artifact Trace — F0038 run 2026-06-30-dbc93ab5

Captures what this plan run (Phase A) read, wrote, generated, and omitted.

## Artifacts Read

Orchestration / framework:
- `agents/ROUTER.md`
- `agents/agent-map.yaml`
- `agents/docs/AGENT-USE.md`
- `agents/actions/plan.md`
- `agents/product-manager/SKILL.md`
- `CONSUMER-CONTRACT.md` (Feature Evidence Contract §8, §13)

Product trackers / KG (slice via CLI, raw on demand):
- `planning-mds/features/REGISTRY.md`
- `planning-mds/features/ROADMAP.md`
- `planning-mds/BLUEPRINT.md`
- `planning-mds/knowledge-graph/*` (via `lookup.py F0038`)

Feature folder:
- `planning-mds/features/F0038-neuron-day-at-a-glance-shell/PRD.md`
- `planning-mds/features/F0038-neuron-day-at-a-glance-shell/STATUS.md`
- `planning-mds/features/F0038-neuron-day-at-a-glance-shell/README.md`
- `planning-mds/features/F0038-neuron-day-at-a-glance-shell/GETTING-STARTED.md`
- `planning-mds/features/F0038-neuron-day-at-a-glance-shell/intake-brief.md`

## Artifacts Created Or Updated

Base run files (this folder): `README.md`, `action-context.md`,
`artifact-trace.md`, `gate-decisions.md`, `commands.log`, `lifecycle-gates.log`.

Planning artifacts (feature folder `planning-mds/features/F0038-neuron-day-at-a-glance-shell/`):
- Created — 8 story files:
  - `F0038-S0001-neuron-service-bootstrap.md`
  - `F0038-S0002-day-at-a-glance-shell-and-zone-dispatch.md`
  - `F0038-S0003-live-renewals-zone-read.md`
  - `F0038-S0004-stub-zones-inactive-payload.md`
  - `F0038-S0005-renewal-outreach-draft.md`
  - `F0038-S0006-mock-send-and-workflow-transition.md`
  - `F0038-S0007-crm-scope-guard.md`
  - `F0038-S0008-companion-telemetry-instrumentation.md`
- Updated — `PRD.md` (Related User Stories table; new `## Screen Layouts (ASCII)` section)
- Updated — `STATUS.md` (Story Checklist populated, header, Notes; **Story Signoff Provenance rows left untouched — append-only**)
- Updated — `README.md` (Stories table + total)

Trackers:
- Updated — `planning-mds/features/STORY-INDEX.md` (regenerated)
- Verified consistent (no edit needed) — `REGISTRY.md`, `ROADMAP.md`, `BLUEPRINT.md`

Not changed (intentionally):
- `planning-mds/knowledge-graph/*` — F0038 ontology bindings deferred to Phase B (architect); minimal stub already present.
- `GETTING-STARTED.md`, `intake-brief.md` — already complete from the skeleton commit.

## Generated Evidence

Validator outputs recorded in `lifecycle-gates.log` (closeout section). Raw
console captures held in the session scratchpad (`ev1.txt`..`ev7.txt`,
`vstories.txt`, `vtrackers.txt`).

## External Or Global Evidence References

None for this base run.

## Omissions And Waivers

- Feature evidence package (`evidence-manifest.json`, role reports, `latest-run.json`)
  is intentionally NOT produced: plan action runs before the feature evidence
  package exists; it is created later by `agents/actions/feature.md`.
- Phase B artifacts (assembly plan, ADRs, canonical-nodes/solution-ontology edits)
  are out of scope for this PHASE=A run.

## Run Environment

- Session working directory for framework-owned scripts: `nebula-agents`
  (sibling of `{PRODUCT_ROOT}`). `commands.log` records `cwd` as `{PRODUCT_ROOT}`
  for product-root commands and `nebula-agents` for framework-root commands to
  avoid absolute paths.
- Session-setup checks run before this folder existed (and therefore not in
  `commands.log`): `python3 scripts/kg/validate.py` (exit 0) and
  `python3 scripts/kg/lookup.py F0038` (exit 0), both from `{PRODUCT_ROOT}`.
