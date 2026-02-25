# Security Boundaries

This project is an orchestration/control-plane design. It deliberately avoids embedding domain-specific data logic.

## Trust boundaries
- **Orchestrator (Go)**: control plane — scheduling, timeouts, audit, artifacts, state.
- **Modules (external processes)**: data plane — transformation logic, treated as untrusted executables.
- **Runtime environment**: OS-level isolation and permissions enforce boundaries.

## Principles
- Modules run with the least privileges possible.
- Module inputs/outputs are treated as opaque artifacts.
- No implicit network access assumptions: if a step requires network, it must be declared and auditable.
- Secrets must not be stored in manifests or artifacts by default.

## Filesystem safety
- Each job has a dedicated workspace directory.
- Each step/attempt writes only inside its workspace.
- Artifacts are append-only once written (practically enforced by convention in v1).

## Logging & privacy
- Audit events record operational facts (timings, exit codes, artifact pointers).
- Do not log payload contents by default.
- Prefer hashes and sizes over content.

## Non-goals
- This project is not a sandbox or container runtime.
- This project does not implement encryption, key management, or data anonymization.
Those belong to the surrounding platform.
