# Run Layout (Filesystem Artifacts)

Each job creates a dedicated run directory:
runs/<job_id>/
manifest.yaml
events.jsonl
input/
payload.bin
payload.sha256
step-01-<id>/
attempt-01/
stdout.log
stderr.log
out.bin
out.sha256
attempt-02/ (optional)
result/
result.bin
result.sha256

## Goals
- Debuggability: open one folder and see the full story.
- Reproducibility: artifacts + checksums.
- Separation: each step/attempt isolated.
- Operator-friendly: no hidden locations.

## Notes
- “bin” is generic (text, json, csv, etc.). The orchestrator does not assume domain semantics.
- Checksums support integrity checks and stable comparisons.
