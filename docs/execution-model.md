# Execution Model

Each step:

- Runs as an isolated OS process
- Receives input via stdin or file
- Writes output to file
- Has strict timeout enforcement
- Produces stdout/stderr artifacts

The orchestrator:

- Tracks start and end timestamps
- Writes structured event logs
- Stops on first failure (default behavior)

This prioritizes transparency over hidden retry logic.
