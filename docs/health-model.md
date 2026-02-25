# Health Model

The orchestrator must decide whether a workflow run (and each step execution) is healthy using explicit signals.

## Goals
- Avoid “it seems fine” heuristics.
- Detect hangs, partial failures, and degraded dependencies.
- Produce explainable, auditable decisions.

## Signals

### Process-level
- process started successfully
- exit status / exit code
- timeout (deadline exceeded)
- stdout/stderr captured as artifacts

### System-level (optional in v1)
- disk space threshold for run artifacts
- CPU/memory pressure (best-effort signal)

### Dependency-level (optional)
- DNS resolution check (if required by a step)
- TCP dial check to a declared dependency
- HTTP probe (if the module depends on an API)

## Health decision rules (v1)
- A step is **healthy** if it completes before timeout and exits with code 0.
- A step is **unhealthy** if it times out or exits non-zero.
- The job is **healthy** only if all steps are healthy.

## Degraded state (v2)
Introduce `Degraded` when:
- job succeeds but with retries
- dependency probes are slow but passing
- warning thresholds exceeded

Degraded is still `Succeeded`, but annotated in audit events.

## Audit requirements
Every health decision must be recorded in `events.jsonl` with:
- signal summary (exit_code / timeout / probe results)
- decision (ok/fail/degraded)
- pointers to artifacts
