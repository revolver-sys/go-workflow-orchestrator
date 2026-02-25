# go-workflow-orchestrator

A design-focused repository exploring the architecture of a manifest-driven workflow engine written in Go.

This project models a system that:

- accepts a job definition (manifest)
- executes processing steps sequentially
- isolates each step as an external module (e.g., Python)
- enforces timeouts and cancellation
- records structured audit events
- produces reproducible artifacts

The emphasis is on **orchestration**, not transformation logic.

---

## Design Principles

- Deterministic execution model
- Explicit state transitions
- Module isolation via separate processes
- Per-step deadlines
- Reproducible runs (artifacts + checksums)
- Structured audit logging
- Failure transparency over silent recovery

---

## Conceptual Architecture

Job Request
│
▼
Manifest Loader
│
▼
Runner (state machine)
│
├── Step 1 (exec module)
├── Step 2 (exec module)
└── Step N (exec module)
│
▼
Artifacts + Audit Log


---

## Failure Model

- A step failure stops execution.
- Timeouts are enforced at the process level.
- Each step writes stdout/stderr as artifacts.
- No implicit retries unless explicitly configured.

---

## Why This Exists

Many production systems fail not because of transformation logic,
but because of poor orchestration, weak isolation, or unclear state handling.

This repository focuses on the control plane:
- workflow supervision
- lifecycle modeling
- execution guarantees

---

## Documentation

Core design documents:

- [`docs/state-machine.md`](docs/state-machine.md) — explicit workflow state transitions
- [`docs/manifest-model.md`](docs/manifest-model.md) — manifest-driven execution model
- [`docs/execution-model.md`](docs/execution-model.md) — step isolation and process model
- [`docs/retry-policy.md`](docs/retry-policy.md) — retry classification and backoff design
- [`docs/audit-log.md`](docs/audit-log.md) — structured audit event model
- [`docs/run-layout.md`](docs/run-layout.md) — filesystem artifact layout
- [`docs/health-model.md`](docs/health-model.md) — health signal evaluation model
- [`docs/security-boundaries.md`](docs/security-boundaries.md) — trust and isolation boundaries

---

## Status

Architecture notes + minimal prototype in progress.
