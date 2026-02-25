# Workflow State Machine

## States

- Pending
- Running
- StepRunning
- StepFailed
- Succeeded
- Failed

## Properties

- Transitions are explicit.
- No implicit recovery.
- Failure is terminal unless retry policy is defined.
- State progression is monotonic.

This model ensures deterministic behavior and audit clarity.
