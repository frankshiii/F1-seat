# F1 Seat Data

[English](README.en.md) · [简体中文](README.md)

> ## Use the live app
>
> **[Open F1 Seat Selection: f1.shiqiqian.com →](https://f1.shiqiqian.com)**
>
> No installation and no ticket sales—compare circuit action, viewing-zone location, type, roof and view data.

Open data for F1 circuit maps, viewing-zone comparison and research. This repository publishes
structured datasets only. It does not contain the private `F1-track` product frontend, recommendation
logic, annotation workbench, production pipeline or deployment configuration.

The current snapshot covers all 22 rounds of the 2026 calendar and includes:

- circuit centrelines, corners, pit-lane traces and DRS intervals
- located overtakes, race-control events and 360-bin speed profiles for completed races since 2023
- grandstand, GA, Club / Hospitality and other viewing-zone geometry
- field-level provenance, confidence, season validity and review status

The release contains 600 raw viewing-zone records and 12,050 located overtakes. Madring has not yet
hosted its first F1 race, so it uses an explicitly provisional pre-race outline and contains no
fabricated heat data.

## How to use the live app

1. Pick a round on the Races screen; the next event includes a days-left badge.
2. Open the circuit and switch between Overtakes, Incidents and Speed. Only the top five corners for
   the active metric are labelled.
3. Zoom with desktop wheel/buttons and drag to pan; on mobile, pinch to zoom and use one finger to pan.
4. The red dashed rail is pit lane and the green dashed rail is DRS. Hover or tap the track for corner
   and local action details.
5. Filter viewing zones by Grandstand, GA, Club or Other, then inspect type, roof, view, distance and confidence.
6. Add two or three zones to Compare and adjust your overtaking, incident and roof preferences.

The map is a decision aid; it does not provide live prices, inventory or individual seat numbers.
`unknown` means unverified.

## Layout

```text
data/
├── circuits/<slug>.json       # circuit, corners, action records, speed and map features
├── viewing-zones/<slug>.json  # grandstand/GA/Club geometry and facts
└── index/
    ├── circuits.json          # calendar and availability
    └── tracks-mini.json       # lightweight paths and counts
schema/
├── circuit.schema.json
└── viewing-zones.schema.json
docs/
└── DATA_DICTIONARY.md
```

The circuit `slug` joins files, for example:

```text
data/circuits/suzuka.json
data/viewing-zones/suzuka.json
```

## How developers use the data

```js
const circuit = await fetch(
  "https://raw.githubusercontent.com/frankshiii/F1-seat/main/data/circuits/suzuka.json"
).then(response => response.json());
console.log(circuit.circuit.name, circuit.overtakes.length);
```

```python
import json
from pathlib import Path

circuit = json.loads(Path("data/circuits/suzuka.json").read_text())
zones = json.loads(Path("data/viewing-zones/suzuka.json").read_text())
print(circuit["circuit"]["name"], len(zones["grandstands"]))
```

## Coordinates and accuracy

- Published circuits and most viewing zones use telemetry Cartesian coordinates in decimetres.
- `s` is lap arclength measured from the start/finish line. Prefer it when joining layers; x/y values
  are not latitude/longitude.
- `confidence`, `validity` and `coverage` are part of the data contract. `unknown` never means “no”.
- `official-map-annotation` identifies project annotations created from official venue-map references
  using AI-assisted extraction followed by manual correction and review. It is not official artwork,
  survey data or certification.
- Original official maps, screenshots, PDFs and satellite basemaps are not distributed here.

See the [data dictionary](docs/DATA_DICTIONARY.en.md) for field-level notes.

## Sources and licensing

There is no blanket licence for every file. OpenF1 derivatives, OSM geometry and original project
annotations retain different terms. Production viewing-zone files in telemetry coordinates are also
mixed-licence data and must not be described wholesale as CC BY 4.0. Read
[DATA_LICENSE.en.md](DATA_LICENSE.en.md) and each viewing-zone
document's `sources` / `provenance` before reuse.

## Contributing

Open an issue with the circuit, applicable season, field, proposed value and a verifiable source. Do not
upload official map artwork, ticketing PDFs, satellite screenshots or other material without
redistribution rights. See [CONTRIBUTING.en.md](CONTRIBUTING.en.md).

F1 Seat Data is an independent, non-commercial fan-data project. It is not affiliated with, sponsored
by or endorsed by Formula 1, the FIA, promoters, circuits, ticket sellers, OpenF1 or OpenStreetMap.
