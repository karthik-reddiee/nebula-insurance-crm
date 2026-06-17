# Operations Telemetry

Committed, durable telemetry streams (diffable, portable across machines/CI), distinct
from the gitignored local dev telemetry under `.kg-state/`.

## `usage.jsonl` — harness usage / cache-cost stream

Append-only normalized **turn events** produced by `scripts/kg/kg_usage.py ingest`, one
per LLM turn, harness-agnostic:

```json
{"tool":"turn","source":"harness","harness":"claude-code|codex|...","session_id":"...",
 "msg_id":"...","ts":"...","model":"...","is_sidechain":false,
 "payload":{"input_tokens":N,"output_tokens":N,"cache_read_tokens":N,"cache_write_tokens":N}}
```

Ingestion is an explicit command — there is no harness-specific auto-trigger. Feed
locations are **not** auto-resolved; point `--input-dir` at the harness's own session
store:

```bash
# Claude Code transcripts
python3 scripts/kg/kg_usage.py ingest --source claude-code --input-dir ~/.claude/projects/<slug>
# Codex rollouts (searched recursively)
python3 scripts/kg/kg_usage.py ingest --source codex --input-dir ~/.codex/sessions
# any tool emitting the normalized contract above
python3 scripts/kg/kg_usage.py ingest --source jsonl --input <feed>.jsonl
```

Re-ingest is idempotent (dedup by `msg_id`). Read the metrics with
`scripts/kg/kg_usage.py report` or `scripts/kg/eval.py` (both pick this file up; `eval.py`
globs `.kg-state/**` **and** `planning-mds/operations/telemetry/**`).
