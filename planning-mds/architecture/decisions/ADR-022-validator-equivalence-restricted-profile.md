# ADR-022: Validator Equivalence and Restricted JSON Schema Profile

**Status:** Accepted
**Date:** 2026-05-06
**Owners:** Architect
**Related Features:** F0034
**Related ADRs:** ADR-001, ADR-020, ADR-021, ADR-023
**Related Schema Bundles:** `_shared/**`, `_unspecified/0.0.0`, `_legacy/<lob>/0.0.0`, `cyber/1.0.0`

## Context

ADR-001 established JSON Schema as a contract language for Nebula static schemas. F0034 extends that idea to runtime product bundles, but browser and backend validators are independent engines. Equivalence must be proven by profile restrictions, normalized errors, and parity tests, not assumed.

The existing static contracts in `planning-mds/schemas/**` remain JSON Schema draft-07 for now. Dynamic LOB bundle sources use JSON Schema 2020-12. OpenAPI remains 3.0.3 until a separate OpenAPI 3.1 migration ADR is accepted.

## Decision

LOB bundle source schemas use JSON Schema draft 2020-12 and must pass a restricted-profile linter before activation.

Allowed keywords:
- `type`
- `required`
- `properties`
- `additionalProperties: false`
- `$ref`
- `$defs`
- `$id`
- `$schema`
- `enum`
- `const`
- `minimum`
- `maximum`
- `exclusiveMinimum`
- `exclusiveMaximum`
- `minLength`
- `maxLength`
- `pattern`
- `minItems`
- `maxItems`
- `uniqueItems`
- `items` with a single subschema
- `minProperties`
- `maxProperties`
- whitelisted `format`: `email`, `uri`, `date`, `date-time`, `uuid`, `ipv4`
- `allOf` for constraint stacking

Forbidden keywords:
- `multipleOf` on non-integers
- `prefixItems`
- `propertyNames`
- `dependentRequired`
- `if` / `then` / `else`
- `patternProperties`
- `contains`, `minContains`, `maxContains`
- `dependentSchemas`
- `not`
- `contentSchema`, `contentMediaType`, `contentEncoding`
- `anyOf`
- `oneOf`
- custom keywords
- remote `$ref`
- any `format` outside the whitelist

`additionalProperties: true` is permitted only for `_legacy/**` pass-through bundles. `_unspecified/0.0.0` remains an empty-object bundle, not pass-through.

Money is represented as integer minor units. Decimal money validation using floating point or `multipleOf` on non-integers is rejected.

Runtime dispatch is resolver-first: the service resolves `lobProductVersionId`, validates `attributes` against exactly one bundle, then evaluates rules. `oneOf` and `discriminator` are allowed only in the OpenAPI projection as codegen metadata at the envelope level.

Both validation engines run in collect-all-errors mode. Parity is multiset equality on normalized `(code, pointer, keyword, schemaPath)` entries, including cardinality. Different message text is ignored because frontend copy owns messages.

The public validation error contract is `LobValidationProblemDetails`. It extends the RFC 7807 shape with `lobErrors[]` and does not reuse `ProblemDetails.errors`.

## Consequences

Positive:
- Schema authors get a portable subset that both engines can enforce consistently.
- OpenAPI 3.0.3 compatibility is explicit and checked by projection rules.
- Error handling becomes stable enough for UI field binding and tests.

Negative:
- Some valid JSON Schema 2020-12 features are intentionally unavailable.
- New keywords require either profile expansion plus parity evidence or a replacement ADR.
- Static schemas and dynamic bundle schemas remain on two draft tracks until a separate migration.

Invalid after this ADR:
- Using `oneOf`, `anyOf`, `not`, `prefixItems`, `propertyNames`, `dependentRequired`, `if/then/else`, remote references, or custom keywords inside runtime LOB bundles while the public contract remains OpenAPI 3.0.3.
- Comparing raw validator messages for parity.
- Putting LOB validation errors into `ProblemDetails.errors`.

## Framework References

Stage 1 framework work must produce or update:
- `agents/architect/references/extensible-attribute-architecture.md`
- `agents/schema-steward/SKILL.md`
- `agents/templates/api-contract-template.yaml`
