# action-job-preamble #

[![GitHub Build Status](https://github.com/cisagov/action-job-preamble/workflows/build/badge.svg)](https://github.com/cisagov/action-job-preamble/actions)

A GitHub Action to apply the standard permissions monitoring and
runner hardening.  This Action is intended to be applied at the
beginning of every GitHub Actions job.

## Usage ##

### Inputs ###

| Name | Description | Interpreted Type | Default | Required |
|------|-------------|------------------|---------|:--------:|
| actions_permissions_config | A JSON string containing the permissions configuration to use for permissions monitoring.  In the case of cisagov you will usually want to set this to `${{ vars.ACTIONS_PERMISSIONS_CONFIG }}` so it agrees with our organization-wide GitHub Actions permissions configuration.  See [the documentation for the GitHubSecurityLab/actions-permissions/monitor action](https://github.com/GitHubSecurityLab/actions-permissions/tree/main/monitor#configuration) for more details. | `string` | n/a | yes |
| harden_runner_egress_policy | The egress policy to use for runner hardening.  See [step-security/harden-runner](https://github.com/step-security/harden-runner) for more details and valid values. | `string` | `audit` | no |

### Outputs ###

None.
<!--
| Name | Description | Output Type |
|------|-------------|-------------|
| output_name | The output's description. | `output_type` |
-->

### Sample GitHub Actions workflow ###

This GitHub Action only makes changes to the runner and therefore
requires no permissions.

```yml
---
name: The workflow

on:
  pull_request:
  push:

jobs:
  my_job:
    # This job does not need any permissions.
    permissions: {}
    runs-on: ubuntu-latest
    steps:
      - name: Apply standard cisagov job preamble
        uses: cisagov/action-job-preamble@develop
        with:
          actions_permissions_config: ${{ vars.ACTIONS_PERMISSIONS_CONFIG }}
```

## Contributing ##

We welcome contributions!  Please see [`CONTRIBUTING.md`](CONTRIBUTING.md) for
details.

## License ##

This project is in the worldwide [public domain](LICENSE).

This project is in the public domain within the United States, and
copyright and related rights in the work worldwide are waived through
the [CC0 1.0 Universal public domain
dedication](https://creativecommons.org/publicdomain/zero/1.0/).

All contributions to this project will be released under the CC0
dedication. By submitting a pull request, you are agreeing to comply
with this waiver of copyright interest.
