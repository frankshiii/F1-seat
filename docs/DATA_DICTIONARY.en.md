# Data dictionary

[English](DATA_DICTIONARY.en.md) · [简体中文](DATA_DICTIONARY.md)

## Circuit documents

- `circuit.geometry.points`: centreline `[x, y]` coordinates, normally in telemetry decimetres.
- `circuit.corners`: corner number, display label, centre and lap position.
- `circuit.map_features.pit_lane`: pit-lane traces observed during races.
- `circuit.map_features.drs_zones`: intervals derived from DRS status and location samples.
- `overtakes[].s`: overtake position measured along the lap.
- `incidents[].turn`: corner explicitly named in race control; coordinates are not invented.
- `speed_profile`: mean and P95 speed in 360 lap bins.
- `coverage`: included seasons, sessions and normalization method.

## Viewing-zone documents

- `schema_version`: currently `1.0.0`.
- `coordinate_system`: coordinate type, units and alignment method.
- `sources`: source records referenced elsewhere in the document.
- `grandstands[].geometry`: zone polygon and geometry source ID.
- `grandstands[].position`: centre, lap position and distance to the circuit.
- `grandstands[].view`: estimated visible corners, method, screen and notes.
- `grandstands[].features`: roof, seating and accessibility status.
- `grandstands[].provenance`: field-level source IDs.
- `grandstands[].confidence`: 0–1 confidence for geometry, name, roof and view.
- `grandstands[].validity`: applicable season and last verification date.
- `grandstands[].extensions.zone_type`: `grandstand`, `general_admission`, `hospitality`,
  `fan_zone` or `unknown`.

## Interpretation

- `unknown` means unverified, not false.
- `provisional` is suitable for preview but not surveying claims.
- Interpret distances using the document's `coordinate_system.units`.
- Multiple nearby polygons with the same name may be sections of one stand and can be merged by clients.
