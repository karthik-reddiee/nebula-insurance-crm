# scripts/kg — Knowledge-Graph Toolchain

CLIs over `planning-mds/knowledge-graph/`. The framework-level reference for
the KG model is `nebula-agents/agents/docs/KNOWLEDGE-GRAPH.md`; this README
documents only what lives in this directory that isn't covered there yet.

## Semantic merge — `merge3.py` (F0006-S0001)

Three-way merge of one **curated** KG file by semantic record id, replacing
line-level git merges of KG YAML. Curated files: `canonical-nodes.yaml`,
`feature-mappings.yaml`, `code-index.yaml`.

```bash
# during an integration, from the repo root
python3 scripts/kg/merge3.py planning-mds/knowledge-graph/canonical-nodes.yaml \
  --base <merge-base-ref> --ours <target-ref> --theirs <source-ref> \
  [--dry-run] [--json report.json] [--full-validate]
```

Inputs are file paths or git refs. Exit codes: `0` clean merge (canonical
output written), `1` typed conflicts or constraint violation (nothing
written), `2` usage/input error.

**Merge semantics** (record = list element carrying `id`):

| Situation | Result |
|-----------|--------|
| Same content, different serialization | converges (canonicalize before compare) |
| Added/changed/deleted on one side only | kept |
| Added on both sides, identical | converges |
| Added on both sides, different | `DivergentInsert` |
| Deleted vs updated | `DeleteVsUpdate` |
| Changed differently — same scalar field | `DivergentUpdate` |
| Changed differently — different fields | field-level recursion, merges |
| Set-like list (default) changed on both sides | three-way set union, sorted |
| Ordered list (`states`, `transitions_to`, `rules`) reordered on both sides | `OrderedListConflict` |
| Merged result re-adds a duplicate id | `UniqueViolation` |
| Merge deletes a node something still references | `OrphanEdge` |
| `--full-validate`: validator fails on merged graph | `ConstraintViolation` (rolled back) |
| Similar names across different ids | `SemanticDuplicateWarning` (advisory) |

Every conflict names its **owning role** (`architect` for node/binding
kinds, `product-manager` for feature/story kinds, both for exclusions).
Output is all-or-nothing: one unresolved conflict blocks the whole file.
Object-form edge refs (`{id:, provenance:, confidence:}`) are references,
never record definitions.

Generated projections (`symbol-index.yaml`, `coverage-report.yaml`,
`unbound-but-referenced.yaml`, `decisions-index.yaml`) are **never merge
inputs** — regenerate them after merging the curated sources, and never
trust a textually clean git merge of them.

**ID-level diff** (used to prove the one-time canonicalization commit
changed nothing semantically, and handy before/after any KG edit):

```bash
python3 scripts/kg/merge3.py planning-mds/knowledge-graph/feature-mappings.yaml \
  --semantic-diff HEAD planning-mds/knowledge-graph/feature-mappings.yaml
```

## Canonical serialization (`kg_common.py`)

`canonicalize_document` / `canonical_dump` / `canonical_equal`: one
deterministic serializer for the curated files — priority-then-alphabetical
mapping keys, record lists sorted by `id`, scalar lists de-duplicated and
sorted, `ORDERED_LIST_FIELDS` (`states`, `transitions_to`, `rules`) keep
authored order. Idempotent; byte-stable across machines. The curated trio
was canonicalized once (no-semantic-change commit) so formatting noise can
never reappear in merges. If you add an order-significant list field to the
KG schema, register it in `ORDERED_LIST_FIELDS` — unregistered structures
conflict rather than silently union.

Tests: `scripts/kg/tests/test_merge3.py`.
