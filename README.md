# Lint Actions PowerShell

[![Build status][build-badge]][build-status]
[![OpenSSF Scorecard][scorecard-badge]][scorecard-report]

## Introduction

Lints inline PowerShell script steps in GitHub Actions.

GitHub Actions workflows in the `.github/workflows` directory
and `action.yml` files for custom actions are linted using
[PSScriptAnalyzer][PSScriptAnalyzer] to check for common issues and best practices.

Issues found by PSScriptAnalyzer are emitted as [GitHub Actions workflow annotations][workflow-annotations].

## Examples

### Basic Usage

To lint PowerShell script steps in a GitHub Actions workflow using the default rules:

```yml
steps:
- uses: actions/checkout@v4
- uses: martincostello/lint-actions-powershell@v1
```

### Advanced Usage

```yml
steps:
- uses: actions/checkout@v4
  with:
    path: 'my-repo'
- uses: martincostello/lint-actions-powershell@v1
  with:
    annotations-title: 'lint-powershell'
    powershell-yaml-version: '0.4.12'
    psscriptanalyzer-version: '1.23.0'
    repo-path: 'my-repo'
    settings-path: 'my-repo/ScriptAnalyzerProfile.txt'
    treat-warnings-as-errors: true
```

## Inputs

### Optional

| **Name** | **Description** | **Default** |
| :------- | :-------------- | :---------- |
| `annotations-title` | The optional title to use for workflow annotations. | `'PSScriptAnalyzer'` |
| `powershell-yaml-version` | The optional version of the [powershell-yaml][powershell-yaml] module to install. | Latest |
| `psscriptanalyzer-version` | The optional version of the [PSScriptAnalyzer][PSScriptAnalyzer] module to install. | Latest |
| `repo-path` | The optional path to the repository containing the files to lint. | `github.workspace` |
| `settings-path` | An optional path to a file containing a user-defined profile containing settings for PSScriptAnalyzer. | [Default settings][default-settings] |
| `treat-warnings-as-errors` | Whether to treat warnings as errors. | `false` |

#### Default Settings

The default PSScriptAnalyzer settings used are equivalent to:

```powershell
@{
    IncludeDefaultRules = $true
    Severity = @("Error", "Warning")
}
```

## Outputs

None.

## Feedback

Any feedback or issues can be added to the issues for this project in [GitHub][issues].

## Repository

The repository is hosted in [GitHub][repo]: <https://github.com/martincostello/lint-actions-powershell.git>

## License

This project is licensed under the [Apache 2.0][license] license.

[build-badge]: https://github.com/martincostello/lint-actions-powershell/actions/workflows/lint.yml/badge.svg?branch=main&event=push
[build-status]: https://github.com/martincostello/lint-actions-powershell/actions?query=workflow%3Alint+branch%3Amain+event%3Apush "Continuous Integration for this project"
[default-settings]: #default-settings "The default settings for PSScriptAnalyzer"
[issues]: https://github.com/martincostello/lint-actions-powershell/issues "Issues for this project on GitHub.com"
[license]: https://www.apache.org/licenses/LICENSE-2.0.txt "The Apache 2.0 license"
[powershell-yaml]: https://www.powershellgallery.com/packages/powershell-yaml "powershell-yaml in PowerShell Gallery"
[PSScriptAnalyzer]: https://www.powershellgallery.com/packages/PSScriptAnalyzer "PSScriptAnalyzer in PowerShell Gallery"
[repo]: https://github.com/martincostello/lint-actions-powershell "This project on GitHub.com"
[scorecard-badge]: https://api.securityscorecards.dev/projects/github.com/martincostello/lint-actions-powershell/badge
[scorecard-report]: https://securityscorecards.dev/viewer/?uri=github.com/martincostello/lint-actions-powershell "OpenSSF Scorecard for this project"
[workflow-annotations]: https://docs.github.com/actions/writing-workflows/choosing-what-your-workflow-does/workflow-commands-for-github-actions "Workflow commands for GitHub Actions"
