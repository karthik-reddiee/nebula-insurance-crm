# ADR-020: LOB Extensible Attribute Architecture

**Status:** Accepted
**Date:** 2026-05-06
**Owners:** Architect
**Related Features:** F0034
**Related ADRs:** ADR-001, ADR-018, ADR-021, ADR-022, ADR-023
**Related Schema Bundles:** `_unspecified/0.0.0`, `_legacy/<lob>/0.0.0`, `_bridge/<lob>/<from>-to-<to>/0.0.0`, `cyber/1.0.0`

## Context

Nebula has stable lifecycle entities for submissions, renewals, policies, policy versions, and policy endorsements. Those entities have a shared core shape, but product-specific underwriting attributes vary by line of business. Adding columns or custom forms for each product would make F0019 and later coverage/reporting work keep rediscovering the same extension problem.

ADR-018 already makes `Policy` a parent row with immutable `PolicyVersion` snapshots. That split is the anchor for policy-level product attributes: attributes are frozen on the version, not stored as an independent mutable source on the policy parent.

## Decision

Variant product attributes are extension data, not core entity columns.

Attribute carriers are:
- `Submission`
- `Renewal`
- `PolicyVersion`
- `PolicyEndorsement`

`Policy` is not an independent attribute carrier. Policy-facing APIs may accept product attributes in create and endorsement flows, but persistence lands on the `PolicyVersion` row produced by the write. Policy read models expose current attributes by following `Policy.CurrentVersionId -> PolicyVersion`.

Each attribute carrier gets:
- `lob_product_version_id uuid NOT NULL`, immutable per row except the approved triage transition and governed migration paths.
- `attributes_json jsonb NOT NULL DEFAULT '{}'`, mutable only while the owning workflow permits same-version attribute edits.

The product registry uses these records:
- `lob_product`: product identity, product kind, code, line of business, display metadata.
- `lob_product_version`: deterministic product version id, status, semver, activation metadata, signature key id, signature.
- `lob_schema_bundle`: one resolved bundle per `(productVersionId, stage)` for `submission`, `policy`, `endorsement`, and `renewal`.
- `lob_bundle_activation_event`: append-only activation, deprecation, retirement, and rollback history.

Product version status values are `Draft`, `Active`, `Deprecated`, `Retired`, and `Internal`. `Internal` is reserved for system-managed sentinels that must resolve historical rows but must not appear in tenant availability bootstrap listings.

Product kind drives sentinel behavior:
- `Standard`: user-pickable active product versions such as `cyber/1.0.0`.
- `Unspecified`: `_unspecified/0.0.0`, used only for Submission/Renewal rows with `lineOfBusiness IS NULL` and `attributes_json = {}`.
- `Legacy`: `_legacy_<lob>/0.0.0`, pass-through bundles for pre-registry non-null LOB rows. Creates and attribute/version-changing writes are blocked; core-only writes may proceed when the version and attributes are unchanged.
- `Bridge`: `_bridge_<lob>_<from>_to_<to>/0.0.0`, steward-authored migration aid used only by approved migration or endorsement paths.

The line-of-business invariant is enforced in two layers:
- Database triggers assert the carrier row's `lineOfBusiness` matches the pinned product version's product line of business. The `_unspecified` exception is allowed only for null-LOB Submission/Renewal rows.
- Application middleware resolves product kind/status before validation and emits deterministic error codes such as `LOB_PRODUCT_MISMATCH` or `LEGACY_SENTINEL_WRITE_BLOCKED`.

Product codes and ids are deterministic. The namespace literal is:

```text
NEBULA_LOB_NAMESPACE=7be9dc8e-e507-4c41-bcf7-8f1ddbb0d9c6
```

Seed constants:
- `_unspecified/0.0.0`: `aa901058-2402-5370-9978-66eb184066be`
- `cyber/1.0.0`: `48f5f86a-7396-50bf-92dd-a3a36fe63c20`
- `_legacy_cyber/0.0.0`: `4ffc79e6-4e32-5d39-a82c-891b6034ab9e`

All activated bundles are signed with HMAC-SHA256. Each `lob_product_version` row stores `signature_key_id`, so key rotation is rolling: new activations use the new key id, older rows can be re-signed in batches, and old keys retire only after no row references them.

Queryable product attributes require explicit projections. Projections use a restricted dot-path grammar, an explicit SQL type cast, and either generated stored columns or expression indexes. Default GIN indexing on `attributes_json` is rejected.

## Consequences

Positive:
- New LOB attributes do not require platform columns or fixed product forms.
- Historical rows render because every row pins a resolvable product version, including sentinels.
- Policy version history remains immutable and compatible with ADR-018.
- Query performance remains reviewable because projections are explicit.

Negative:
- Compile-time safety for product attributes moves to bundle validation and generated types.
- Migrations must seed all per-LOB legacy sentinels before strict invariants are enabled.
- Operational activation needs signatures, status transitions, and audit rows, not simple file copy.

Invalid after this ADR:
- Adding LOB-specific underwriting fields directly to Submission, Renewal, Policy, PolicyVersion, or PolicyEndorsement without an approved core/extension classification.
- Storing independent `Policy.attributes_json` as a write source.
- Filtering on unprojected JSON paths in production queries.

## Framework References

Stage 1 framework work must produce or update:
- `agents/architect/references/extensible-attribute-architecture.md`
- `agents/templates/entity-model-template.md`
- `agents/templates/feature-template.md`
- `agents/templates/feature-assembly-plan-template.md`

