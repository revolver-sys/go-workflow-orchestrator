# Manifest Model

A workflow run is defined by a manifest.

Example conceptual structure:

```yaml
version: 1
name: example-pipeline
steps:
  - id: step1
    exec: ["python3", "module.py"]
    timeout_sec: 10
