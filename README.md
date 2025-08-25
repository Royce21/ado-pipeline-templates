# ADO Central Pipeline Templates

## Structure
- `pipelines/multi-stage.yml` – entrypoint used via `extends`
- `stages/ci.yml` – CI stage (dotnet/node)
- `stages/cd.yml` – CD stage (downloads `drop`, optional Azure step)
- `jobs/*.yml` – language-specific jobs
- `steps/*.yml` – reusable steps (add lint, code scan, publish tests)
- Repo structure (pipelines/, stages/, jobs/, steps/)

How to consume (the resources.repositories + extends snippet)

Parameters table

Versioning policy (tags + pinning)

Upgrade steps (bump tag in consumers)

## How to consume
```yaml
resources:
  repositories:
  - repository: templates
    type: github
    name: Royce21/ado-pipeline-templates
    ref: refs/tags/v1.0.0
    endpoint: github-templates-conn

extends:
  template: pipelines/multi-stage.yml@templates
  parameters:
    app_type: node   # or dotnet
    env: qa
    enable_deploy: true
    vmImage: ubuntu-latest
    artifact_name: drop
    service_connection: ""  # set AzureRM conn name to enable Azure step
