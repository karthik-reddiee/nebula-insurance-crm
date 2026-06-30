# Artifact Trace — F0038 run 2026-06-30-d1dd91f7

Captures what this plan run (Phase B) read, wrote, generated, and omitted.
Updated incrementally; finalized at run close.

## Artifacts Read

Orchestration / framework:
- `agents/ROUTER.md`
- `agents/agent-map.yaml`
- `agents/docs/AGENT-USE.md`
- `agents/actions/plan.md`
- `agents/architect/SKILL.md`
- `CONSUMER-CONTRACT.md` (Feature Evidence Contract §8, §13)

Prior run evidence:
- `planning-mds/operations/evidence/runs/2026-06-30-dbc93ab5/` (Phase A base run — README, action-context, artifact-trace, gate-decisions as model + approval confirmation)

Product trackers / KG (slice via CLI, raw on demand):
- `planning-mds/knowledge-graph/*` (via `lookup.py F0038`; raw `feature-mappings.yaml`, `canonical-nodes.yaml`, `solution-ontology.yaml`, `coverage-report.yaml` on demand)

Feature folder + governing architecture:
- `planning-mds/features/F0038-neuron-day-at-a-glance-shell/PRD.md`
- `planning-mds/features/F0038-neuron-day-at-a-glance-shell/STATUS.md`
- `planning-mds/features/F0038-neuron-day-at-a-glance-shell/intake-brief.md`
- `planning-mds/features/F0038-neuron-day-at-a-glance-shell/F0038-S0001..S0008-*.md` (8 stories)
- `planning-mds/architecture/decisions/ADR-027-neuron-companion-a2a-orchestration.md`
- `planning-mds/architecture/c4-neuron-companion.md`
- `planning-mds/architecture/SOLUTION-PATTERNS.md`
- `planning-mds/architecture/data-model.md`
- `planning-mds/api/nebula-api.yaml`
- `planning-mds/BLUEPRINT.md` (§3 approved requirements, §4 architecture)

## Artifacts Created Or Updated

Base run files (this folder): `README.md`, `action-context.md`,
`artifact-trace.md`, `gate-decisions.md`, `commands.log`, `lifecycle-gates.log`.

ADRs:
- Created — `planning-mds/architecture/decisions/ADR-028-neuron-companion-persistence-and-outreach-authorization.md`
- Updated — `planning-mds/architecture/decisions/ADR-027-neuron-companion-a2a-orchestration.md` (ratified at F0038 Phase B; 4 Phase B follow-ups checked off with pointers)

JSON Schemas (`planning-mds/schemas/`, all created):
- `neuron-message-envelope.schema.json`, `neuron-zone-payload.schema.json`,
  `neuron-agent-card.schema.json`, `neuron-orchestration-plan.schema.json`,
  `renewal-needs-attention-item.schema.json`, `renewal-outreach-draft-request.schema.json`,
  `renewal-outreach-mock-send-request.schema.json`, `neuron-companion-telemetry-event.schema.json`

API contracts:
- Created — `planning-mds/api/neuron-api.yaml` (Neuron service surface)
- Updated — `planning-mds/api/nebula-api.yaml` (5 engine endpoints under `NeuronCompanion` tag; tag + version 0.6.0→0.7.0)

Architecture / data model / blueprint:
- Updated — `planning-mds/architecture/data-model.md` (§11 `neuron.*` operation store + ERD; v7.0)
- Updated — `planning-mds/BLUEPRINT.md` (§4.7 Neuron Companion architecture)

Authorization:
- Updated — `planning-mds/security/authorization-matrix.md` (§2.9a renewal:draft_outreach + outreach-commit exception)
- Updated — `planning-mds/security/policies/policy.csv` (Underwriter + Admin `renewal, draft_outreach`)

Feature folder:
- Updated — `planning-mds/features/F0038-neuron-day-at-a-glance-shell/README.md` (Architecture section, feature ERD Mermaid+ASCII, contracts table, status)

Knowledge graph:
- Updated — `planning-mds/knowledge-graph/canonical-nodes.yaml` (+33 nodes: 10 capability, 8 endpoint, 3 event, 1 policy_rule, 2 adr, 1 api_contract, 8 schema; ADR-027/028 rationale)
- Updated — `planning-mds/knowledge-graph/feature-mappings.yaml` (F0038 removed from `excluded_features`; full `feature:F0038` mapping + 8 `story:F0038-S000X` mappings)
- Regenerated — `planning-mds/knowledge-graph/coverage-report.yaml` (`--write-coverage-report`)

Trackers:
- Regenerated — `planning-mds/features/STORY-INDEX.md` (`generate-story-index.py`)

## Generated Evidence

Validator outputs recorded in `lifecycle-gates.log` (closeout section).

## Omissions And Waivers

- Feature evidence package (`evidence-manifest.json`, role reports,
  `latest-run.json`) intentionally NOT produced — plan runs before the feature
  evidence package exists; it is created later by `agents/actions/feature.md`.
- `feature-assembly-plan.md` intentionally NOT authored — deferred to the F0038
  `feature` action Step 0 per `plan.md` Deliverables Contract (see
  `gate-decisions.md` → Deliverable-scope reconciliation).
- `code-index.yaml` bindings intentionally NOT added — no `neuron/` implementation
  code exists yet at plan; code bindings are authored during the `feature` action.

## Run Environment

- Session working directory for framework-owned scripts: `nebula-agents`
  (sibling of `{PRODUCT_ROOT}`). `commands.log` records `cwd` as `{PRODUCT_ROOT}`
  for product-root commands and `nebula-agents` for framework-root commands.
- Session-setup checks run before this folder existed (and therefore not in
  `commands.log`): `python3 scripts/kg/validate.py` (exit 0) and
  `python3 scripts/kg/lookup.py F0038` (exit 0), both from `{PRODUCT_ROOT}`.
