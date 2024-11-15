# Linting Standard

This standard outlines the minimum [linting](https://en.wikipedia.org/wiki/Lint_(software)) expecations for Dissemination repos.

## Context

Linting is a key element of our wider approach to maintaining and improving the quality of our applications while also improving the efficiency of our software development workflows. Linters enable us to automate many of the checks that would otherwise be completed manually by PR reviewers, thereby shifting left to reduce the delay in the feedback loop and reducing the effort for the reviewer. Furthermore, linters, in combination with formatters, codify coding conventions and style guides, removing person preference and debate during peer reviews about minor style conventions.

## Scope of Application

This standard applies to all Dissemination repos that are targetted to live operational use. Live operational use covers any code deployed to a production environment as well as any code used to build, test, debug or support this code.

Prototypes, proof-of-concepts (POCs) and alpha code bases are excluded as quality and longevity are not a priority in these cases.

### Existing code bases

Existing, live operational code bases that do not meet the current linting standard are handled differently depending on strategic value and life expectancy of the code in question. In general, applying linters to repos with a short life expectancy will not benefit from a positive return on the effort investment required to bring the code up to standard.

The following categories of live operational code bases are exempt from this linting standard:

1. All legacy Java code bases as these would require too great an effort to bring up to standard and have a limited life expectancy.
2. All applications that are part of a product that has received sunset approval under the sunsetting policy.

All other existing, live operational code bases should be updated to meet this standard at or prior to the point of next code change.

## Base linters

The following sections outline the minimum, base requirement for linters that should be used. Linters are specified for each of the common languages and frameworks used and signpost default configurations where applicable.

These linters are a minimum standard and teams may choose to add additional linters where desired.

### Megalinter

:test_tube: **EXPERIMENTAL:** We are currently trialling adoption of Megalinter as a standard. Discuss with your tech lead before adopting with your repos.

Megalinter is a docker based linting toolbox that combines many different language specific linters and provides a common summary output.

The normal language specific linters should still be used

### Go

* golangci-lint (a multi-linter, see [recommended configuration](https://github.com/ONSdigital/dp-cli/blob/main/project_generation/content/templates/base-app/.golangci.yml.tmpl) for more details of the specific, recommended linters)

### Python

* Ruff
* Black
* Magpie

Recommended configuration can be found in the [python template repo](https://github.com/ONSdigital/ons-python-template).

### JavaScript

* Eslint
* prettier

### CSS/SASS/SCSS

* stylelint

### HTML

* djlint

### Terraform

* tf-lint
* tf-fmt
* checkov

Recommended configuration can be found in the [terraform template repo](https://github.com/ONSdigital/dis-aws-terraform-stack-template).

### Java

As all of our Java codebases are legacy with a limited lifespan, we have decided not to introduce linters to these repos. If at any point in the future new Java codebases are developed, then this standard should be updated with the agreed linting recommendations.

### Other languages and frameworks

Where your codebase uses a language or framework not specified in this standard, then it is strongly recommended that you research and identify appropriate linters to be used by your repo.

If your project introduces a new language or framework, or identifies a common gap in the base linters recommended, then a PR should be raised to extend this standard to address the gap.
