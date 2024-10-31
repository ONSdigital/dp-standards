# Repository standards

Here is a list of repository standards we have for our repositories. Much of the below is automated by our `dp-cli` tool for creating repositories but is documented here for completeness.

## Contents

- [naming conventions](#naming-conventions)
- [visibility](#visibility)
- [repository documentation](#repository-documentation)
- [permissions](#permissions)

## Naming conventions

Repositories should be named with the prefix `dis-` to distinguish them as belonging to `Dissemination`. This helps to identify our repositories amongst the many that are part of ONSDigital.

Historical repositories have the prefix `dp-` as they belonged to `Digital Publishing`.

## Visibility

We aim to work in the open where possible and so the majority of our repositories should be `public`.

Repositories should be marked as `private` if they reveal details of:

- ONS infrastructure
- ONS security mitigations

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

Every repository should have a README file in the root directory. This should include:

- how to run the service locally, if applicable
- details of environmental configuration

## Permissions

Below describes the standard approach for permissions in our repositories.

### Collaborators and Teams

Our standard approach is as follows:

| Team                     | Permission |
|--------------------------|------------|
| Dissemination            | write      |
| Dissemination Tech Leads | admin      |
| Responsible teams        | maintain   |
| Security                 | read       |

Responsible teams will be those teams responsible for the repository code. This may be more than one team in the case of shared responsibility.

Users should be given direct collaborator access to repositories and this should be removed on repository creation.

### Branch permissions

Depending on the branching strategy of the repository, there may be a variety of protected branches. These could include `master`, `main`, `develop`, as well as locked version branches for older versions of libraries we are maintaining. The majority of those should follow these rules:

- requires a pull request before merging
- requires 1 review of pull request before merging
- status checks from CI must pass before merging
- signed commits must be used
- bypassing is not allowed
- no force pushing
- no deletions
