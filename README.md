# shared-actions
Vultr shared workflows

## Secret scanning

Call this reusable workflow from a repository's workflow to scan its full Git
history for leaked credentials with Gitleaks:

```yaml
name: Secret Scan
on:
  pull_request:
  push:

jobs:
  secret-scan:
    uses: Vultr/shared-actions/.github/workflows/secrets-scan.yml@main
```

The workflow checks out full history and fails if Gitleaks detects a potential
secret. Optional inputs:

| Input | Type | Default | Description |
| --- | --- | --- | --- |
| `config` | string | `''` | Path to a Gitleaks configuration file in the caller repository. |
| `redact` | boolean | `true` | Redact detected secret values from output. |

The caller's `GITHUB_TOKEN` is used by default. Provide the optional
`github_token` secret only if a different token is needed.
