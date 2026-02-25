# Audit Log

The system must answer:

- What ran?
- In what order?
- With what inputs?
- For how long?
- With what outputs?
- Why did it fail?
- What was retried?

## Format
Use append-only JSON Lines (`events.jsonl`).
One event per line. No mutation.

## Minimal event fields
- `ts` (RFC3339Nano)
- `type` (job_start, step_start, step_ok, step_fail, job_ok, job_fail, attempt_start, attempt_fail, attempt_ok)
- `job_id`
- `step_id` (optional)
- `data` (freeform object)

## Example events

```json
{"ts":"2026-02-25T20:00:00.000Z","type":"job_start","job_id":"...","data":{"manifest":"demo","version":1}}
{"ts":"2026-02-25T20:00:01.000Z","type":"step_start","job_id":"...","step_id":"upper","data":{"timeout_sec":5}}
{"ts":"2026-02-25T20:00:01.500Z","type":"step_ok","job_id":"...","step_id":"upper","data":{"duration_ms":500,"out":"step-01-upper/out.txt"}}
{"ts":"2026-02-25T20:00:02.000Z","type":"job_ok","job_id":"...","data":{"result":"result.txt"}}
