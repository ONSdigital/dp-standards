# Code Licensing

This standard outlines the requirements for appropriate licensing for open source code repositories (e.g. public git repositories) maintained by Dissemination.

This standard is broadly similar to the [GDS Way Licensing guidance](https://gds-way.digital.cabinet-office.gov.uk/manuals/licensing.html#licensing) and follows the [UK Government Licensing Framework](https://www.nationalarchives.gov.uk/information-management/re-using-public-sector-information/uk-government-licensing-framework/).

## Repositories MUST Include an Open Source Licence

All public git repositories MUST be covered by appropriate licensing as specified by a LICENCE file(s) containing the licence text(s) in full and a Licence section in the README with a link(s) to the LICENCE file(s) clearly stating what licence(s) apply and, where there are multiple, what is covered by each licence. See [Readme notice notice](#readme-notice-wording) for an example.

The appropriate licence will depend on the contents of the repo:

* Code: All source code repositories MUST be published under the MIT License as the default standard (see exception noted below)
* Documentation: All documentation only repositories MUST be published under the Open Government Licence v3 (OGL3)
* Mixed Code and Documentation (e.g. code that generates static documentation sites): All repos containing a mix of code and documentation, where the documentation is not documentation about the code in the same repo, MUST be published under the MIT License for the code and under the OGL3 licence for the documentation
* Mixed Code and Open Data: All repos containing a mix of code and open data (this excludes "fake" data for test purposes) MUST be published under the MIT License for the code and under the OGL3 licence for the data by default (see exception noted below)
* Mixed Code and Government Assets: All repos containing a mix of code and government assets (e.g. logos) MUST be published under the MIT License for the code and under the OGL3 licence for the assets

MIT Exception: Where a repository incorporates third-party components with restrictive "copyleft" or specific attribution requirements (e.g., GPL, Apache 2.0, or BSD), an alternative Open Source Initiative (OSI) approved licence MUST be applied to the code to ensure legal compatibility while maintaining maximum re-use potential.

OGL3 Exception: Where a repository incorporates data from third-parties with restrictive "copyleft" or specific attribution requirements, this MUST be noted with the original or an alternative legally compatible licence included.

## Repositories MUST State Crown Copyright

All work created by civil servants and contractors for the ONS is Crown Copyright.

All repositories MUST include a copyright notice that reads:

```text
Copyright (c) {YEAR} Crown Copyright (Office for National Statistics)
```

The `{YEAR}` MUST be the first year that the code was published (i.e. made public).

The copyright notice MUST appear in the licence file.

It is RECOMMENDED to include the copyright notice in the readme.

It is NOT RECOMMENDED to extend the copyright date each year using a range. The crown copyright for published literary work, which includes code, is 50 years from the end of copyright year. The functional repository lifespan is expected to be significantly shorter so therefore extending the licence range by a year is wasted effort.

### Example copyright notice

The following is an example copyright notice as it must appear in the licence file:

```text
Copyright (c) 2025 Crown Copyright (Office for National Statistics)
```

## Readme notice wording

The readme MUST state the the repo is under Crown Copyright, clearly state the licensing and link to the appropriate licence files.

The following is the RECOMMENDED default wording:

```markdown
Copyright (c) {{YEAR}} [Crown Copyright](http://www.nationalarchives.gov.uk/information-management/re-using-public-sector-information/copyright-and-re-use/crown-copyright/) (Office for National Statistics)

Unless stated otherwise, the codebase is released under the [MIT License](./LICENCE.md).
```

Repositories containing a mix of code and other categories of files will need to modify this default wording to make it clear where the MIT License does not apply. For example, the following might be used for a documentation site like the Developer Hub:

```markdown
Copyright (c) {{YEAR}} [Crown Copyright](http://www.nationalarchives.gov.uk/information-management/re-using-public-sector-information/copyright-and-re-use/crown-copyright/) (Office for National Statistics)

Unless stated otherwise, the codebase is released under the [MIT License](./LICENCE.md). This covers both the codebase and any sample code in the documentation.

The documentation site content is released under the [Open Government Licence v3.0](https://www.nationalarchives.gov.uk/doc/open-government-licence/version/3/).
```
