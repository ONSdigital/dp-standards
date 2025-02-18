# Licensing Standard

This standard outlines the requirements for copyright notices and licensing for all public version control repositories (e.g. git repositories).

This standard is broadly similar to the [GDS Way Licensing guidance](https://gds-way.digital.cabinet-office.gov.uk/manuals/licensing.html#licensing) and follows the [UK Government Licensing Framework](https://www.nationalarchives.gov.uk/information-management/re-using-public-sector-information/uk-government-licensing-framework/).

## Copyright notice

The copyright notice must appear in the licence file and may optionally be included in the readme.

### Copyright holder

The copyright holder must be '[Crown Copyright](https://www.nationalarchives.gov.uk/information-management/re-using-public-sector-information/uk-government-licensing-framework/crown-copyright/)' and may optionally be followed by '(Office for National Statistics)'.

### Year

The year should be the year the repository was first published.

The copyright notice does not need to be extended each year. While the duration can be extended using a range from the first publication to the latest update (e.g. `2025-2026`), the functional repository lifespan is likely to be shorter than the relatively long copyright duration.

### Example copyright notice

The following is an example copyright notice as it must appear in the licence file:

```text
Copyright (c) 2025 Crown Copyright (Office for National Statistics)
```

## Code licence

We release our code, including code examples, under the [MIT License](https://opensource.org/license/MIT) unless the repository includes third party code released under a different licence. The licence should be included in full in a `LICENCE` or `LICENCE.md` file.

The copyright line of the licence file should match the copyright notice guidance above.

## Non-code licence

Non-code assets in our repositories, such as documentation and example data, should be released under the [Open Government Licence v3](https://www.nationalarchives.gov.uk/doc/open-government-licence/version/3/).

The repository readme should state the Open Government Licence v3 applies and include a link to the licence on the National Archives website. See [Readme notice](#readme-notice) for an example.

## Readme notice

The readme should state the the repo is under Crown Copyright, clearly state the licensing and link to the appropriate licence files.

The following is the recommended wording:

```markdown
Copyright (c) {{YEAR}} [Crown Copyright](http://www.nationalarchives.gov.uk/information-management/re-using-public-sector-information/copyright-and-re-use/crown-copyright/) (Office for National Statistics)

Unless stated otherwise, the codebase is released under the [MIT License](./LICENCE.md). This covers both the codebase and any sample code in the documentation.

Documentation, example data and other non-codebase contents are available under the terms of the [Open Government Licence v3.0](https://www.nationalarchives.gov.uk/doc/open-government-licence/version/3/).
```
