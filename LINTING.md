# Linting Standard

This standard outlines the minimum [linting](https://en.wikipedia.org/wiki/Lint_(software)) and code style/format checking expectations for Dissemination repos.

## Context

Linting is a key element of our wider approach to maintaining and improving the quality of our code while also improving the efficiency of our software development workflows. Linters enable us to automate many of the checks that would otherwise be completed manually by PR reviewers, thereby shifting left to reduce the delay in the feedback loop and reducing the effort for the reviewer. Furthermore, formatters in combination with linters enable coding conventions and style guides to be codified and automatically checked, further improving the peer review efficiency and removing personal preference and debate during peer reviews about minor style conventions.

## Scope of application

This standard applies to all Dissemination repos that are targeted to live operational use. Live operational use covers any code deployed to a production environment as well as any code used to build, test, debug or support this code.

Prototypes, proof-of-concepts (POCs) and alpha code bases are excluded as quality and longevity are not a priority in these cases however these standards can still be used to guide best practice when building them.

### Existing code bases

Existing, live operational code bases that do not meet the current linting standard are handled differently depending on strategic value and life expectancy of the code in question. In general, applying linters to repos with a short life expectancy will not benefit from a positive return on the effort investment required to bring the code up to standard.

The following categories of live operational code bases are exempt from this linting standard:

1. All legacy Java code bases as these would require too great an effort to bring up to standard and have a limited life expectancy.
2. All applications that are part of a product that has received sunset approval under the [sunsetting policy](https://confluence.ons.gov.uk/x/UQMwDQ).

All other existing, live operational code bases should be updated to meet this standard at or prior to the point of next code change.

## Inclusion in workflow

In order to ensure linters (and other static code analysis tools) are not forgotten, these tools must be run automatically as part of the standard workflow for all teams. This must occur before a pull request can be approved and block the merging of the pull request until resolved. There are a number of options for achieving this including the Concourse CI PR jobs or using GitHub Actions.

Some teams may also wish to use [pre-commit](https://github.com/pre-commit/pre-commit) hooks to allow for linters to run before code is committed to provide earlier feedback. As pre-commit hooks are dependent on `pre-commit` being installed, this approach should only be used in combination with a guaranteed, remote executed method.

## Base linters and formatters

The following sections outline the minimum, base requirement for linters and formatters that should be used. Linters and formatters are specified for each of the common languages and frameworks used and signpost default configurations where applicable.

These tools are a minimum standard and teams may choose to add additional tools where desired.

### MegaLinter

:test_tube: **EXPERIMENTAL:** We are currently trialling adoption of MegaLinter as a standard, see [dis-design-system-go](https://github.com/onsdigital/dis-design-system-go#linting) for an example implementation. Discuss with your tech lead before adopting with your repos.

[MegaLinter](https://megalinter.io/) is a docker based linting toolbox that combines many different language specific linters and provides a common summary output.

> [!NOTE]
>
> * Autofixing should not be enabled in CI unless fixes can be automatically written back to the repository.
> * The normal language specific linters should still be used.

### Go

* [golangci-lint](https://golangci-lint.run/) (a multi-linter, see [recommended configuration](https://github.com/ONSdigital/dp-cli/blob/main/project_generation/content/templates/base-app/.golangci.yml.tmpl) for more details of the recommended linters to enable)

### Python

* [ruff](https://github.com/astral-sh/ruff)
* [pylint](https://github.com/pylint-dev/pylint) is currently recommended until such time as ruff supports all pylint rules

Recommended configuration can be found in the [python template repo](https://github.com/ONSdigital/ons-python-template).

### JavaScript

* [eslint](https://eslint.org/)
* [prettier](https://prettier.io/) (use the `--check` flag on PR to check that the files are formatted)

### CSS/SASS/SCSS

* [stylelint](https://stylelint.io/)

### HTML

* [djlint](https://www.djlint.com/)

### Terraform

* [tflint](https://github.com/terraform-linters/tflint)
* [terraform validate](https://developer.hashicorp.com/terraform/cli/commands/validate)
* [terraform fmt](https://developer.hashicorp.com/terraform/cli/commands/fmt) (use the `-check` flag on PR to check that the files are formatted)
* [checkov](https://www.checkov.io/)
* [trivy](https://github.com/aquasecurity/trivy)

Recommended configuration can be found in the [terraform template repo](https://github.com/ONSdigital/dis-aws-terraform-stack-template).

### Markdown

* [markdownlint](https://github.com/DavidAnson/markdownlint)

### OpenAPI (formerly Swagger) specifications

* [redocly-cli](https://github.com/Redocly/redocly-cli)

### AsyncAPI specifications

* [asyncapi validate](https://www.asyncapi.com/docs/tools/cli/usage#asyncapi-validate-spec-file)

### Java

As all of our Java codebases are legacy with a limited lifespan, we have decided not to introduce linters to these repos if they did not have them already. If at any point in the future new Java codebases are developed, then this standard should be updated with the agreed linting recommendations.

The most common convention within the existing codebases that have it is using [checkstyle](https://github.com/apache/maven-checkstyle-plugin). We recommend using the Sun standard (`sun_checks.xml`) as a default.

### Secrets detection

The following tools prevent secrets being committed to the repo.

* [GitHub secret scanning](https://docs.github.com/en/code-security/secret-scanning/enabling-secret-scanning-features) - it is required that all public repos have both secret scanning and push protection enabled

Optionally, you may wish to also use [gitleaks](https://github.com/gitleaks/gitleaks).

### Other languages and frameworks

Where your codebase uses a language or framework not specified in this standard, then it is strongly recommended that you research and identify appropriate linters to be used by your repo.

If your project introduces a new language or framework, or identifies a common gap in the base linters recommended, then a PR should be raised to extend this standard to address the gap.
