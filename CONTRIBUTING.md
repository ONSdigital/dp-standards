# Contributing

## What is a standard?

A standard could be a way of working across the development team or applying the same solution to a common problem to software built on the digital publishing platform.

The idea of a standard is to be implemented across all software development teams to assist the development of software, to maintain consistency, robustness and security to how and what we develop.

If it doesn't make sense for an idea to be applied across teams it is **not** a standard, it may instead be a guide or documentation specific to the repository you're working in.

### Can standards change?

Yes they can, even though it is expected that this shouldn't happen frequently as we should have previously thought through any new standards; however we are liable to not knowing what we do not know and therefore we should be allowed to change any standards when new knowledge is gained.

## How to contribute?

Contributing to digital publishing development standards may begin with an idea to resolve a problem discussed in one of the guilds, investigative work into how best to solutionalise a problem within your team, e.g. API versioning, changes to ci/cd workflows. Remember a solution to a problem doesn't necessarily mean it should be a standard, so how do we hit the right balance and to prevent too much bureaucracy?

Consider how we would rollout the standard across teams. A good way to approach this, is to think about how to allow developers to fall naturally into following this standard without becoming an expert; this is known as ["falling into the pit of success"](https://blog.codinghorror.com/falling-into-the-pit-of-success/) and if it is done well, the standard becomes the default approach without consulting documentation.

Examples of this could be writing boiler plate code in libraries for reuse in application code or updating tooling to assist the creation of new repositories or using story templates to enable users as a starting point to fill in acceptance criteria for work etc.

### Process of Contributing

It is expected that some level of discussion has occurred across teams or with technical leads before following the below process, one may use a PR in this repository to help further this discussion.

#### Creating documentation for standard

- Create feature branch that will contain your new standard or updates to existing standard: `git checkout -b feature/example-standard`
- Create/update standard; if it is a new standard that does not touch on existing standards then a new markdown file should be created and added to the root [README.md list of contents](./README.md#contents)
- Once happy with feature branch, create pull request
- Standard needs approval from at least 1 technical lead and another developer (this can also be a technical lead)

When creating the documentation, think about links to relevant specifications or other resources that may assist developers when reading up on how to implement the standard.

#### Peer reviewing standard in pull request

It is reasonable to challenge the pull request merit to becoming a standard or changing existing standards (whether that is updating existing standards or removing it altogether). Does it make sense that this is rolled out to all development teams and if yes then how could this be done with little to no impact (this is where I refer back to "falling into the pit of success").

- Review pull request considering the above statement
- Consult technical leads if unsure
- Follow normal pull request procedure, leaving comments to improve documentation

Pull requests will need at least one technical lead approval before it can be merged so responsibility does not soley lie with developers.

#### Pre-commit

We encourage the use of [pre-commit](https://pre-commit.com/) locally, this reduces the amount of common mistakes and engineers can just focus on reviewing the actual changes.

```sh
# Install pre-commit
brew install pre-commit
# This will enable pre-commit to run every time you git commit
pre-commit install
```

If you want to do an adhoc run of pre-commit

⚠️ This will only run on files that are staged in git

```sh
pre-commit run --all-files
```

If you want to commit and skip checks

```sh
git commit --no-verify -m "some message"
```

#### Markdown linting

This respository uses [markdown linting](https://github.com/DavidAnson/markdownlint-cli2) for all PRs.

To install:

```sh
    brew install markdownlint-cli2
```

To run:

```sh
    markdownlint-cli2 **/*.md
```
