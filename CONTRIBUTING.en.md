# Contributing data

[English](CONTRIBUTING.en.md) · [简体中文](CONTRIBUTING.md)

> **Generated files in this repository do not accept direct pull requests, but public data-correction issues are welcome.**
> No code, Git or JSON knowledge is required; maintainers integrate verified corrections into the data source and regenerate this repository.

The quickest way to contribute:

1. [Open the grandstand correction form](https://github.com/frankshiii/F1-seat/issues/new?template=stand-correction.yml).
2. Choose the circuit and affected fields, then enter the applicable season or attendance date.
3. State the current value, proposed value and verifiable source separately; mark any uncertainty.
4. Submit the issue. A maintainer will review it, update the source data and publish it in a later mirror.

For a whole circuit, a new circuit or a structured batch, use the
[circuit data proposal form](https://github.com/frankshiii/F1-seat/issues/new?template=circuit-data.yml).

The highest-value current task is verifying the 89 stand names whose `provenance.name` contains
`"osm"`, using a current official page or a dated firsthand observation.

## Useful contributions

- grandstand/GA/Club names, aliases, zone types and season validity
- roof, screen, accessibility and firsthand observations
- geometry offsets, corner labels, pit-lane or DRS interval corrections
- broken sources, confidence and provenance fixes

## Do not submit

- official map artwork, ticket PDFs, satellite screenshots or paid-database exports
- bulk guesses without a source and applicable season
- generated-file-only changes with no explanation of the underlying data correction

Submit only material you have the right to share. Automatic extraction requires human review;
unknown facts remain `unknown` rather than being guessed.
