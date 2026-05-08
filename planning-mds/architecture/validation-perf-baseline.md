# Validation Performance Baseline

**Feature:** F0034
**Status:** Baseline artifact published; numeric dynamic-validator baseline pending F0034-S0004 harness
**Last Updated:** 2026-05-06
**Source:** `planning-mds/architecture/lob-extensible-attribute-plan.md` Section 10

## Baseline Scope

This artifact records the performance gates that F0034 implementation must satisfy and the current repository state that affects measurement. The current frontend package does not yet include direct `ajv`, `ajv-formats`, `ajv-errors`, or `react-hook-form` dependencies, and the backend projects do not yet include `JsonSchema.Net` or `JsonLogic.Net`. Because the dynamic validation engines are introduced by F0034, the numeric dynamic-validator baseline is captured by F0034-S0004 when those dependencies and fixtures are added.

Existing static request validation remains on the non-variant track. F0034 does not migrate static `planning-mds/schemas/**` contracts or non-variant FluentValidation rules to the dynamic LOB validator.

## Required Measurements

| Metric | Baseline (Q2 2026) | Target | Measurement Owner |
|---|---|---|---|
| Bootstrap payload size for active bundles per tenant | Not captured in this planning run | <= 500 KB gzipped | F0034-S0002 / F0034-S0006 |
| Schema validation latency, frontend warm | Not captured until AJV dependency lands | p95 <= 5 ms | F0034-S0004 |
| Schema validation latency, backend warm | Not captured until JsonSchema.Net dependency lands | p95 <= 10 ms | F0034-S0004 |
| Rule evaluation latency | Not captured until JsonLogic dependencies land | p95 <= 5 ms FE / <= 10 ms BE | F0034-S0004 |
| Dynamic form initial render, Cyber submission | Not captured until DynamicAttributePanel lands | <= 300 ms on mid-tier laptop | F0034-S0005 |
| Projection-backed portfolio query | Not captured until generated projections land | p95 <= 50 ms at 100K rows | F0034-S0003 / F0034-S0006 |
| Bundle compile time | Not captured until bundle compiler lands | <= 30 s | F0034-S0002 / F0034-S0006 |
| Schema resolver startup cost | Not captured until resolver lands | <= 2 s for 50 active bundles | F0034-S0002 |

## Merge Rule

F0034 implementation cannot exit Phase C with any `Not captured` row above. The first implementation PR that introduces a dynamic validator, resolver, bundle compiler, projection generator, or dynamic form renderer also adds its benchmark command and writes p50, p95, and p99 results into this file.

## Telemetry Rule

Runtime instrumentation must emit these OpenTelemetry spans:
- `lob.resolver.resolve`
- `lob.middleware.lob_consistency`
- `lob.validation.schema`
- `lob.validation.rules`

Span attributes include `lob.product_version_id`, `lob.stage`, `lob.schema_hash`, and error count where applicable. Production dashboards plot p95 against the targets above by `(productVersionId, stage)`.

