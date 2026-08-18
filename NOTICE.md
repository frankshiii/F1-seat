# Notices and attribution

[English](NOTICE.md) | [简体中文](NOTICE.zh-CN.md)

F1 Seat Selection is an independent, non-commercial fan project. It is not affiliated with,
authorized by, sponsored by, or endorsed by Formula 1, the FIA, race promoters, circuits, ticket
sellers, OpenF1, or OpenStreetMap.

The project's original software code is available under the [MIT License](LICENSE). That software
license does not replace or broaden the separate terms that apply to the datasets and upstream
materials listed below.

Formula 1, F1, Grand Prix, circuit names, event names and related marks belong to their respective
owners. Names are used only to identify the events and locations described by the project.

## Data attribution

- Race and telemetry source: [OpenF1](https://openf1.org/), licensed by its publisher under
  [CC BY-NC-SA 4.0](https://github.com/br-g/openf1/blob/main/LICENSE).
- Stand names on 89 zones: © [OpenStreetMap contributors](https://www.openstreetmap.org/copyright),
  available under the Open Database License (ODbL). No geometry is OSM-derived; the obligation
  applies only to records whose `provenance.name` contains `"osm"`.
- Grandstand, GA and hospitality geometry identified as `official-map-annotation` is a
  project-maintained annotation layer created from official venue-map references with AI-assisted
  extraction and manual review. It is not official map artwork or official certification.
- Circuit centrelines are adaptations calculated from OpenF1 location data and remain subject to
  OpenF1's CC BY-NC-SA 4.0 terms. Observed pit-lane and DRS layers are also derived from OpenF1.
  Turn labels are maintained as a separate, source-linked annotation layer; some migrated anchors
  are explicitly marked as pending independent review.
- Geographic circuit outlines used by the pipeline:
  [bacinger/f1-circuits](https://github.com/bacinger/f1-circuits), MIT License.

Official seating maps, promoter PDFs, satellite imagery and other copyrighted reference material are
used only in the local annotation and verification workflow and are not intentionally distributed with
this project. Published annotations should not be presented as copies of, or substitutes for, those maps.
See [DATA_LICENSE.en.md](DATA_LICENSE.en.md) for the source-by-source reuse notes.
