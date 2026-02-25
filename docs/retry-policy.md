# Retry Policy

Retries must be explicit, bounded, and observable.

## Goals
- Improve resilience against transient failures (network, short stalls).
- Avoid hiding real data/logic errors behind automatic retries.
- Keep behavior deterministic and explainable.

## Non-goals
- “Make it always succeed.”
- Retry without recording attempts.

## Classification
A step failure is classified as:

- **Retryable**: timeouts, temporary network errors, dependency unavailable
- **Non-retryable**: invalid input, deterministic script failure, schema violation

In this notebook, classification is conceptually supported via:
- exit codes
- error signatures (stderr patterns)
- explicit manifest flag (force retry or force fail)

## Policy parameters
- `max_attempts` (default: 1)
- `backoff` (fixed or exponential)
- `retry_on` (timeout | exit_code | stderr_pattern)

Example (conceptual):

```yaml
steps:
  - id: fetch
    exec: ["python3", "fetch.py"]
    timeout_sec: 10
    retry:
      max_attempts: 3
      backoff_ms: 500
      retry_on: ["timeout", "exit_code:75"]
