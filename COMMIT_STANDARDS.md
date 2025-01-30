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

A good commit message briefly summarises the "what" for scanning purposes, but also includes the "why". If the "what" in the message is not enough, the diff is there as a fallback. This is not true for the "why" of a change - this can be much harder or impossible to reconstruct, but is often of great significance.

## Merging and squashing

When working on a feature branch, your branch may become out of date with it's parent. To update your branch we prefer a rebase here to a merge commit as we prefer a clean and straight history on the parent branch. However, this can be difficult for reviewers to track changes if done in between reviews. Please check with your reviewer before doing so. This is also true for tidying up commit histories and messages.
