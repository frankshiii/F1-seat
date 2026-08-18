# Data sources and licensing

[English](DATA_LICENSE.en.md) | [简体中文](DATA_LICENSE.md)

This document applies to repository data and pipeline-generated publications. It is not legal
advice and does not replace any upstream licence or terms of service.

## The dataset as a whole is published under CC BY-NC-SA 4.0

**The published dataset (`web/data/*.json` and the public data exported from it) is provided
under [CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/). See
[LICENSE-DATA](LICENSE-DATA).**

Why that licence and not something looser: race action, speed profiles, centrelines and every
`track_s`, distance and view field computed from a centreline are derivatives of OpenF1, which
publishes under CC BY-NC-SA 4.0. Its ShareAlike clause requires derivatives to be distributed
under the same licence — an obligation triggered by distribution itself, regardless of whether
the use is commercial. Applying the strictest upstream licence to the whole set is the only way
to satisfy it in one step.

Two things must be held together:

1. **The project's code remains [MIT](LICENSE).** Commercially usable code does not make the
   bundled data commercially usable.
2. **A data licence cannot exceed its upstream.** The source layers below tell you what each
   category is derived from and what extra obligations it carries (for example, 89 stand names
   are additionally covered by ODbL). CC BY-NC-SA 4.0 is the project's grant over what it can
   license; it does not re-license anyone's upstream rights.

Original project annotations that are not mixed with another source may be used on looser terms
where the author separately agrees, but a complete production JSON is a mixed-source document and
**must not be described wholesale as CC BY 4.0**.

## Source layers

### Race action, telemetry-derived metrics and centrelines

Overtakes, positions, speeds and race-control events come from OpenF1. Published centrelines are
also derived by resampling, taking a multi-driver median and smoothing OpenF1 `location` traces.
Observed pit-lane traces and DRS-open intervals are likewise derived by joining OpenF1
`pit / car_data / location` records.
OpenF1 publishes its repository under **CC BY-NC-SA 4.0**. This project therefore distributes
those derivatives only as a non-commercial fan project with attribution. Contact OpenF1 before
commercial use, sublicensing or any use where the API-output terms are unclear.

- Source: https://openf1.org/
- Licence: https://github.com/br-g/openf1/blob/main/LICENSE

### OpenStreetMap stand names (names only; no geometry)

**No geometry in this dataset comes from OpenStreetMap any more.** All 600 viewing-zone
polygons are now project-owned annotations (557 `official-map-annotation`, 21 `official-map`)
plus 22 estimates derived from the MIT-licensed `bacinger/f1-circuits`. The pipeline no longer
calls the Overpass API.

What remains under ODbL is a set of **stand names**: 89 zones whose names were originally taken
from OSM `name` tags — monza 39, barcelona 17, silverstone 16, spielberg 9, shanghai 6, spa 1,
hungaroring 1.

That boundary is **self-describing in the data**: for any record whose `provenance.name`
contains `"osm"`, the name field is © OpenStreetMap contributors under **ODbL 1.0**; no other
field carries that obligation. Downstream users who take geometry, positions or action metrics
without those names do not touch ODbL at all.

These names have not been independently re-verified, and some are known to contradict the
official-map labels (at one circuit `Tribuna C` and `Tribuna G` appear to be swapped, and the
zone named `Tribuna E` carries the official label `F`) — meaning **some OSM names are simply
wrong**. Verifying and replacing them against official maps or ticketing pages is one of the
most useful contributions available; see CONTRIBUTING. This section is deleted once that is done.

- Attribution: https://www.openstreetmap.org/copyright
- Licence: https://opendatacommons.org/licenses/odbl/1-0/

### `circuit_alignment` SVGs and derived venue geometry

Twenty 2026 circuits currently use track, grandstand, GA and hospitality outlines generated from
local `circuit_alignment/*.svg` inputs. The project maintainer created these annotation layers from
public official circuit/venue maps using AI-assisted extraction followed by circuit-by-circuit manual
correction, naming and review. They are not third-party supplied SVG assets.

Official maps are local references for annotation and fact-checking. The project publishes annotation
coordinates and transformed results, not the official map artwork, screenshots or PDFs, and does not
claim survey-grade or official certification. Annotation provenance remains separate from OpenF1, OSM
and other source layers. Independent original annotations the maintainer can license and that have not
been mixed with another source may use CC BY 4.0. Production coordinates mapped to an OpenF1 centreline,
plus `track_s`, distances and view fields derived from it, remain under OpenF1's CC BY-NC-SA 4.0; `osm`
geometry remains under ODbL. A complete production JSON is therefore mixed-licence and must not be
described wholesale as CC BY 4.0.

- Pipeline source ID: `official-map-annotation`
- Local input: `circuit_alignment/<slug>.svg`
- Annotation method: official-map reference + AI-assisted extraction + manual correction and review
- Build command: `npm run build:svg-production`
- Current publication: 557 venue geometries across 20 circuits after rejecting outliers over 450 m
  from the circuit centreline

### Corner-number anchors

Corner labels are maintained separately in `pipeline/data/corner_anchors.json` as lap-length
fractions and projected onto OpenF1 centrelines during builds. Reviewed circuits cite official
maps; `bootstrap_pending_review` means a migrated baseline still awaits independent review.

- Current centrelines and x/y coordinates do not call or copy the MultiViewer circuits API.
- Migrated anchors are small annotation baselines, not survey data or official certification.
- Downstream users should retain pending status until review is complete.
- Contributors should use current official circuit maps and update source/review metadata.

The legacy migration source previously used was https://multiviewer.app/.

### Geographic circuit outlines

Madring's provisional outline and geographic alignment references for some circuits come from
`bacinger/f1-circuits` under the **MIT License**. Retain its provenance in derived data.

- Source: https://github.com/bacinger/f1-circuits
- Pinned snapshot and licence: `pipeline/vendor/`

### Official ticket pages, venue maps and spectator guides

These references are used only to verify inventories, names, roofs, view descriptions and rough
positions. Original PDFs, images, screenshots and satellite basemaps are not distributed with the
repository or website. Fact records preserve source URL, retrieval date, season and confidence;
that does not grant rights to the source artwork.

### Community-contributed facts

Firsthand observations, aliases, verification status and annotations retain source and confidence
metadata. Contributors must have permission to share any photos or other copyrighted material and
must state the allowed use.

## Reuse checklist

Before copying, redistributing or deploying data:

1. Inspect `sources`, `provenance`, `confidence` and `validity` in each document.
2. Keep OpenF1, OpenStreetMap and other upstream attribution and licence links.
3. Never interpret `unknown` as a negative fact.
4. Do not present provisional or low-confidence geometry as precise surveying.
5. Do not assume commercially usable code makes all bundled data commercially usable.
6. Resolve OpenF1's NonCommercial restriction and other upstream rights separately for commercial use.
7. `official-map-annotation` identifies project-maintained annotations, not official map artwork or
   certification. Open exports should license only content the project can license and keep OpenF1,
   OSM and other source layers separated.
