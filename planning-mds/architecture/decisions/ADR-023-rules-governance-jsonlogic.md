# ADR-023: JsonLogic Rules Governance

**Status:** Accepted
**Date:** 2026-05-06
**Owners:** Architect
**Related Features:** F0034
**Related ADRs:** ADR-020, ADR-021, ADR-022
**Related Schema Bundles:** `_shared/rules/**`, `cyber/1.0.0`

## Context

JSON Schema covers structural validation well, but product bundles also need cross-field and contextual rules such as relationship checks between limits, deductibles, and control answers. Those rules must not become an untyped second platform.

## Decision

LOB bundle rules use JsonLogic with a governed envelope.

Each rule has:
- `id`
- `code`
- `pointer`
- `severity`
- `expression`
- optional `description`

Runtime context is deterministic:

```json
{
  "data": {},
  "core": {},
  "context": {}
}
```

`data` is the `attributes_json` subtree. `core` is the stable entity core used by the write path. `context` is a bounded set of externally resolved facts declared by the bundle, such as current workflow stage or product metadata.

Custom operations live under `_shared/rules/operations/`. A custom operation must include a TypeScript implementation, a .NET implementation, fixture cases, and parity tests before a bundle can depend on it.

Rule evaluation happens after schema validation and before domain workflow validation. A schema-invalid payload does not proceed to rules. Rule failures use the same `lobErrors[]` envelope with `code = RULE_FAILED` unless a rule declares a more specific stable code.

Rule depth is limited to 8. Rule evaluation has per-request timeouts and emits OpenTelemetry spans matching the F0034 telemetry contract.

## Consequences

Positive:
- Cross-field product logic is portable across frontend and backend.
- Custom operations are reviewed and versioned as shared primitives.
- Rule errors bind to fields through the same normalized error channel as schema errors.

Negative:
- Product stewards cannot add arbitrary executable code.
- Stateful or external-context checks still belong in domain services when they exceed the bounded context model.
- Rule parity becomes a required CI gate.

Invalid after this ADR:
- Embedding ad hoc JavaScript or C# expressions in product bundles.
- Adding custom JsonLogic operations in only one runtime.
- Running rules before schema validation.

## Framework References

Stage 1 framework work must produce or update:
- `agents/architect/references/extensible-attribute-architecture.md`
- `agents/schema-steward/references/rules-governance.md`
- `agents/templates/feature-template.md`

