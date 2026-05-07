# ADR-021: Dynamic Form Engine With RHF, AJV, and shadcn Widget Registry

**Status:** Accepted
**Date:** 2026-05-06
**Owners:** Architect
**Related Features:** F0034
**Related ADRs:** ADR-020, ADR-022, ADR-023
**Related Schema Bundles:** `cyber/1.0.0`, `_unspecified/0.0.0`, `_legacy/<lob>/0.0.0`

## Context

F0034 needs dynamic product forms that render from schema metadata, validate in the browser, and stay visually consistent with the Nebula frontend. General-purpose schema form libraries would reduce initial coding but would make widget behavior, layout, theme coverage, and pin-during-edit behavior harder to govern.

## Decision

Nebula uses a custom dynamic form engine built on:
- React Hook Form for field state and controlled edit lifecycle.
- AJV for client-side JSON Schema validation.
- The existing shadcn-style component system and a local widget registry for rendering.

The engine renders `<DynamicAttributePanel>` for product attributes. The panel is embedded inside existing Submission, Policy, Endorsement, and Renewal screens; it is not a standalone product admin app.

The form binds to `(productVersionId, stage)` at open time and remains pinned to that version for the edit session. If a new product version is activated while a form is open, the current form keeps its original bundle. The user sees the new version only after reopening or starting a new workflow.

The widget registry is explicit. Each `ui.schema.json` widget name must map to a shipped frontend widget and option schema. Bundle activation fails if a bundle references an unknown widget, unknown option, or layout primitive that is not in the meta-schema.

The MVP widget vocabulary is intentionally narrow:
- text
- textarea
- number
- money-minor
- select
- multi-select
- checkbox
- date
- section
- read-only summary

Heavy domain widgets such as vehicle schedules or tower visualizers require a paired frontend deploy before a bundle can activate them.

Theme and accessibility coverage are part of the widget contract. Each widget must have light and dark theme smoke coverage and form-level keyboard/focus coverage before a bundle depending on it can be activated.

## Consequences

Positive:
- The form engine stays aligned with Nebula's existing frontend system.
- Data-schema-only product changes can ship without a frontend deploy when they use known widgets.
- Pin-during-edit avoids mid-session schema drift and validation surprises.

Negative:
- Nebula owns form rendering code and widget governance.
- New complex widgets require product, frontend, and schema-steward coordination.
- Form behavior must be covered by component, integration, and Playwright tests.

Invalid after this ADR:
- Using RJSF, JSONForms, Formily, or another schema form engine for F0034 product attributes without a replacement ADR.
- Letting activation introduce unknown widget names or UI options.
- Rebinding an open edit form to a newly activated product version.

## Framework References

Stage 1 framework work must produce or update:
- `agents/architect/references/dynamic-form-engine.md`
- `agents/templates/screen-spec-template.md`
- `agents/templates/api-contract-template.yaml`

