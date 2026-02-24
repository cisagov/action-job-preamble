# action-job-preamble #

[![GitHub Build Status](https://github.com/cisagov/action-job-preamble/workflows/build/badge.svg)](https://github.com/cisagov/action-job-preamble/actions)
[![License](https://img.shields.io/github/license/cisagov/action-job-preamble)](https://spdx.org/licenses/)
[![CodeQL](https://github.com/cisagov/action-job-preamble/workflows/CodeQL/badge.svg)](https://github.com/cisagov/action-job-preamble/actions/workflows/codeql-analysis.yml)

A GitHub Action to apply the standard permissions monitoring, runner
hardening, GitHub status checking, and output the workflow context.
This Action is intended to be applied at the beginning of every GitHub
Actions job.

## Usage ##

### Inputs ###

| Name | Description | Interpreted Type | Default | Required |
| ---- | ----------- | ---------------- | ------- | :------: |
| check_github_status | A Boolean (`"true"`/`"false"`) value indicating whether or not to check GitHub status using the [crazy-max/ghaction-github-status](https://github.com/crazy-max/ghaction-github-status) GitHub action. | `bool` | `false` | no |
| harden_runner | A Boolean (`"true"`/`"false"`) value indicating whether or not to harden the runner using the [step-security/harden-runner](https://github.com/step-security/harden-runner) GitHub action. | `bool` | `true` | no |
| harden_runner_egress_policy | The egress policy to use for runner hardening.  Valid values are audit and block.  See [step-security/harden-runner](https://github.com/step-security/harden-runner) for more details. | `string` | `audit` | no |
| monitor_permissions | A Boolean (`"true"`/`"false"`) value indicating whether or not to monitor GitHub permission requests using the [GitHubSecurityLab/actions-permission/monitor](https://github.com/GitHubSecurityLab/actions-permission/monitor) GitHub action. | `bool` | `true` | no |
| output_workflow_context | A Boolean (`"true"`/`"false"`) value indicating whether or not to output the workflow context using the [crazy-max/ghaction-dump-context](https://github.com/crazy-max/ghaction-dump-context) GitHub action. | `bool` | `false` | no |
| permissions_monitoring_config | A JSON string containing the configuration to use for permissions monitoring.  In the case of cisagov you will usually want to set this to `${{ vars.ACTIONS_PERMISSIONS_CONFIG }}` so it agrees with our organization-wide GitHub Actions permissions monitoring configuration.  See [the documentation for the GitHubSecurityLab/actions-permissions/monitor action](https://github.com/GitHubSecurityLab/actions-permissions/tree/main/monitor#configuration) for more details. | `string` | `""` | no |

### Outputs ###

None.
<!--
| Name | Description | Output Type |
| ---- | ----------- | ----------- |
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
        uses: cisagov/action-job-preamble@f3e1d43556bc9fef1fa4d6f27fa88b1b5c82c788 # v1.2.0
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
