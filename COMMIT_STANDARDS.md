# Commit standards

We follow the [GDS Way styleguide](https://gds-way.digital.cabinet-office.gov.uk/standards/source-code/working-with-git.html#commits) for our commit standards.

This means that each commit:

- is self-contained
- only includes changes that achieve a specific step
- should be in a logical order

## Commit messages

Writing good commit messages is important. Not just for yourself, but for other developers on your project. This includes:

- new (or recently absent) developers who want to get up to speed on progress
- interested external parties who want to follow progress of the project
- people in the public (remember, we code in the open) who want to see our work, or learn from our practices
- any future developers (including yourself) who want to see why a change was made

A good commit message should:

- summarise the "what", providing a concise, scan-friendly headline that captures the essence of the change.
- explain the "why" by including details in the message body that clarify the motivation behind the change. While the code diff shows what changed, the reasoning often isn't apparent.
- follow a consistent format by using the imperative mood (e.g. "Add", "Fix", "Update") to give a clear, action-oriented description.

## Merging and squashing

When working on a feature branch, it's common for your branch to become outdated relative to its parent. We prefer to update your branch by rebasing rather than merging. Rebasing offers a cleaner, linear history on the parent branch, which is easier to follow. However:

- Coordinate with Reviewers/Team: Rebasing during an active code review can complicate the review process. Always check with your reviewer/team style guide before rebasing or tidying up commit histories.
- Use Squashing Judiciously: Squash commits when it makes sense to consolidate minor, related changes into one atomic commit. Just ensure that you retain enough detail in the commit message to explain the consolidated changes.
