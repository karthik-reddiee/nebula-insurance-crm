# OpenAPI 3.0.3 Projection Matrix for LOB Bundles

**Feature:** F0034
**Status:** Accepted baseline
**Last Updated:** 2026-05-06
**Source:** `planning-mds/architecture/lob-extensible-attribute-plan.md` Section 2.3 and ADR-022

LOB bundle sources use JSON Schema 2020-12. The public API contract remains OpenAPI 3.0.3, so generated product branches must project into the OpenAPI 3.0 schema subset without semantic loss. Keywords marked `Reject` are forbidden in bundles while the public contract remains OpenAPI 3.0.3.

| 2020-12 source | 3.0.3 equivalent or reject | Semantic-loss flag |
|---|---|---|
| `type` single primitive | `type` | No |
| `type: ["T", "null"]` | `type: T` plus `nullable: true`; generator-only conversion for static compatibility | No when exactly one non-null type |
| `required` | `required` | No |
| `properties` | `properties` | No |
| `additionalProperties: false` | `additionalProperties: false` | No |
| `additionalProperties: true` in `_legacy/**` only | `additionalProperties: true` | No for legacy pass-through only |
| `$ref` local | `$ref` after bundle resolution or local component emission | No |
| `$defs` | Emitted as named `components.schemas` or inlined | No |
| `$id` | Dropped from projected branch metadata; retained in source bundle | No runtime loss because resolver uses source bundle |
| `$schema` | Dropped from OpenAPI projection | No runtime loss because resolver uses source bundle |
| `enum` | `enum` | No |
| `const` | Single-value `enum` | No |
| `minimum` / `maximum` | `minimum` / `maximum` | No |
| `exclusiveMinimum` / `exclusiveMaximum` numeric | `exclusiveMinimum` / `exclusiveMaximum` numeric | No |
| `minLength` / `maxLength` | `minLength` / `maxLength` | No |
| `pattern` | `pattern` | No |
| `minItems` / `maxItems` | `minItems` / `maxItems` | No |
| `uniqueItems` | `uniqueItems` | No |
| `items` single subschema | `items` | No |
| `prefixItems` | Reject | Yes if allowed; tuple array semantics do not project cleanly into OpenAPI 3.0.3 |
| `minProperties` / `maxProperties` | `minProperties` / `maxProperties` | No |
| `propertyNames` | Reject | Yes if allowed; OpenAPI 3.0.3 support is not portable enough for generated clients |
| `dependentRequired` | Reject | Yes if allowed; enforce through runtime 2020-12 validation and JsonLogic if needed |
| `format` whitelist | `format` | No, with RequireFormatValidation enforced at runtime |
| `allOf` | `allOf` | No |
| `if` / `then` / `else` | Reject | Yes if allowed; use runtime source validation and generated docs note, or move condition to JsonLogic |
| `multipleOf` on integer | `multipleOf` | No |
| `multipleOf` on non-integer | Reject | No allowed loss; money uses integer minor units |
| `patternProperties` | Reject | No allowed loss; forbidden by ADR-022 |
| `contains` / `minContains` / `maxContains` | Reject | No allowed loss; forbidden by ADR-022 |
| `dependentSchemas` | Reject | No allowed loss; forbidden by ADR-022 |
| `not` | Reject | No allowed loss; forbidden by ADR-022 |
| `contentSchema` / `contentMediaType` / `contentEncoding` | Reject | No allowed loss; forbidden by ADR-022 |
| `anyOf` | Reject | No allowed loss; forbidden by ADR-022 |
| `oneOf` inside bundle | Reject | No allowed loss; forbidden inside bundles |
| OpenAPI envelope `oneOf` | Generated at envelope level only, keyed by `lobProductVersionId` | No runtime loss; resolver still dispatches by id |
| OpenAPI `discriminator` | Generated at envelope level only | No runtime loss; codegen metadata only |
| Custom keywords | Reject | No allowed loss; forbidden by ADR-022 |
| Remote `$ref` | Reject | No allowed loss; bundles are resolved before serving |

## Projection Rule

The OpenAPI generator must fail if a source bundle contains an allowed runtime keyword that this matrix marks `Reject`, unless a follow-up ADR either forbids that keyword in the profile or migrates the public contract to OpenAPI 3.1.

The Stage 0 decision is to forbid `prefixItems`, `propertyNames`, `dependentRequired`, and `if/then/else` while OpenAPI remains 3.0.3. No fifth ADR is required because the restricted profile now rejects every semantic-loss keyword instead of permitting runtime-only source semantics that generated clients cannot represent.
