# Data sources and licensing

[English](DATA_LICENSE.en.md) · [简体中文](DATA_LICENSE.md)

This repository has no blanket licence covering every datum. Terms apply by source layer; `sources`
and `provenance` identify the origin of records and fields. This summary is not legal advice.

## OpenF1 derivatives

Circuit centrelines, overtakes, race-control events, speed profiles, pit-lane traces and DRS intervals
are calculated from OpenF1 data and distributed under
[CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/): attribution is required,
commercial use is excluded, and shared adaptations must use the same licence and identify changes.

- Source: https://openf1.org/
- Upstream licence: https://github.com/br-g/openf1/blob/main/LICENSE

## OpenStreetMap data

Geometry marked `osm` is © OpenStreetMap contributors and available under
[ODbL 1.0](https://opendatacommons.org/licenses/odbl/1-0/). Public use of a derivative database must
meet the attribution, Share-Alike and machine-readable database access requirements.

## Original annotations and production-aligned outputs

Original zones marked `official-map-annotation` were created by the project maintainer from
public official venue-map references using AI-assisted extraction followed by manual correction,
naming and review. To the extent the maintainer owns the licensable rights and the material has not
been mixed with another source, those independent original annotation
contributions are available under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/). Attribute
`F1 Seat Data contributors`, link this repository and indicate modifications.

`data/viewing-zones/*.json` contains production coordinates: polygons have been aligned to an OpenF1
centreline, while `position.track_s`, distance-to-track and some corner-view fields are calculated from
that centreline; some records also use OSM geometry. These production files are therefore
**mixed-licence datasets**:

- OpenF1 alignment and derived fields remain under CC BY-NC-SA 4.0;
- `osm` geometry remains under ODbL 1.0;
- CC BY 4.0 covers only independent original annotation contributions the maintainer can license,
  not each production JSON as a whole.

This grant does not cover official map artwork, logos, trademarks or third-party material the project
cannot license. Original maps, screenshots and PDFs are not distributed here, and annotations must not
be represented as official surveying or certification.

## Official factual references

Official ticket pages, venue maps and spectator guides are references for names, inventories, roofs,
screens, zone types and approximate positions. This repository publishes structured facts and project
annotations; it does not grant rights in the original pages, artwork or prose.

## Reuse checklist

1. Inspect `sources`, `provenance`, `confidence` and `validity`.
2. Retain OpenF1, OpenStreetMap and project-annotation attribution; use `provenance` to resolve fields.
3. Do not use OpenF1-derived data commercially.
4. Do not treat `unknown` as a negative fact or provisional geometry as surveying.
5. Do not label all of `data/viewing-zones/` as CC BY 4.0; preserve source-layer terms when combining data.
