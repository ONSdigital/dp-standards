# Repository standards

Here is a list of repository standards we have for our repositories. Much of the below is automated by our [dp-cli](https://github.com/ONSdigital/dp-cli) tool for creating repositories but is documented here for completeness.

## Contents

- [Naming conventions](#naming-conventions)
- [Visibility](#visibility)
- [Repository documentation](#repository-documentation)
- [Permissions](#permissions)

## Naming conventions

Repositories should be named with the prefix `dis-` to distinguish them as belonging to `Dissemination`. This helps to identify our repositories amongst the many that are part of ONSDigital.

Historical repositories have the prefix `dp-` as they belonged to `Digital Publishing`.

### Branch naming

#### Protected branches

`main`: This is the 'live' branch and is the single source of truth showing the release history for the repo.
`develop`: This branch is present on repos that have opted to adopt a GitFlow branching strategy and is the integration branch where fixes and features are integrated prior to a release branch being cut

`master` has been historically used in older repositories and should be migrated to `main` when feasible.

#### Development branches

`feature/*` - for features
`fix/*` - for fixes
`hotfix/*` - for hotfixes from `main`
`release/*` - for cutting releases

## Visibility

We aim to work in the open where possible and so the majority of our repositories should be `public`.

Repositories should be marked as `private` if they reveal details of:

- ONS infrastructure
- encrypted secrets files

### GitHub Copilot

If a repo is `private` then GitHub Copilot and similar tools should be excluded from reading the content in the repository.

## Repository documentation

### CODEOWNERS

Every repository should have a CODEOWNERS file in it's `.github` folder. This should show the responsible team(s) for that repository.

### CONTRIBUTING

Every repository should have a CONTRIBUTING file in the root directory. This should make clear to engineers how they can contribute to that repository, including:

- branching strategy
- commit approach
- merging strategy

### LICENSE

Every repository should have a LICENSE file in the root directory. As standard we use the MIT licencse.

### PULL_REQUEST_TEMPLATE

Every repository should have a PULL_REQUEST_TEMPLATE file in it's `.github` folder. This should make clear how pull requests are documented for that repository.

### README

Every repository should have a README file in the root directory.

For applications, this should include:

- how to run the service locally, if applicable
- details of environmental configuration
- dependencies required to run in order to develop locally
- where appropriate, a link to the docker-compose stack to run it with other services

### Makefile

Every repository should use a Makefile for running:

- tests
- builds
- linters
- running application

Where possible, these should be consistent across applications / libraries. Some common targets include:

- build: used to build the project ready for deployment
- debug: used to build and run the project locally often watching for local changes and rebuilding to aid in local development
- lint: runs all linters and other static code analysis tools for the project
- test: runs unit and integration tests for the project
- test-component: runs component tests for the project

### Dockerfile

All applications should have local dockerfile for running in a local docker environment. The naming convention for this is `Dockerfile.local`.

## Permissions

Below describes the standard approach for permissions in our repositories.

### Collaborators and Teams

Our standard approach is as follows:

| Team                     | Permission |
|--------------------------|------------|
| Dissemination            | write      |
| Dissemination Tech Leads | admin      |
| Responsible teams        | maintain   |

Responsible teams will be those teams responsible for the repository code. This may be more than one team in the case of shared responsibility.

Users must not be given direct collaborator access to repositories and this should be removed on repository creation.

### Branch permissions

Depending on the branching strategy of the repository, there may be a variety of protected branches. These could include `master`, `main`, `develop`, as well as locked version branches for older versions of libraries we are maintaining. The majority of those should follow these rules:

- requires a pull request before merging
- requires 1 review of pull request before merging
- status checks from CI must pass before merging
- signed commits must be used
- bypassing is not allowed
- no force pushing
- no deletions
