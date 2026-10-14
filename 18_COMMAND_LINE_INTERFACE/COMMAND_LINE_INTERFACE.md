# Command Line Interface — DJANGO_HEALTH_CHECK

**Upstream:** https://github.com/bmihelac/django-health-check

## Anticloud CLI

```bash
# Install
pip install anticloud-django-health-check

# Run offline with PAX inference
anticloud-django-health-check --offline --pax-local

# Run with AIOSS logging
anticloud-django-health-check --aioss-log ./ledger.jsonl

# Single binary (after build)
./django_health_check --config config.yaml
```

## Options

| Flag | Description |
| --- | --- |
| `--offline` | Disable all network calls |
| `--pax-local` | Use local PAX inference at 127.0.0.1:11434 |
| `--aioss-log PATH` | Write AIOSS audit chain to PATH |
| `--encrypt` | Enable AES-256 at rest for output files |
| `--gpu` | Force GPU inference |
| `--cpu` | Force CPU inference |
| `--config PATH` | Load configuration from YAML file |
