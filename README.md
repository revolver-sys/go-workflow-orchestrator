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

## Status

Architecture notes + minimal prototype in progress.
