# Methodology

## 1. Study Area

Pokhara Metropolitan City, Gandaki Province, Nepal. The municipal boundary (`Pokhara_boundary.gpkg`) defines the analysis extent.

## 2. Data Collection

| Dataset | Source | Raw file |
|---|---|---|
| Provincial boundaries | Administrative boundary data | `data/raw/gandaki (2).gpkg` |
| Parks | OpenStreetMap via QuickOSM (`leisure=park`) | `data/raw/pokhara_parks.gpkg` |
| Gardens | OpenStreetMap via QuickOSM (`leisure=garden`) | `data/raw/pokhara_gardens.gpkg` |
| Major roads | OpenStreetMap via QuickOSM | `data/raw/pokhara_major_roads.gpkg` |
| Trunk roads | OpenStreetMap via QuickOSM (`highway=trunk`) | `data/raw/pokhara_trunks.gpkg` |
| Minor roads | OpenStreetMap via QuickOSM | `data/raw/pokhara_minor_roads.gpkg` |
| Building footprints | OpenStreetMap | Used for the detailed urban map |

## 3. Data Preparation

### 3.1 Clipping
All layers were clipped to the Pokhara boundary using **Vector → Geoprocessing → Clip**.

Outputs: `*_clipped.gpkg` in `data/processed/`.

### 3.2 Reprojection
Clipped layers were reprojected from EPSG:4326 (WGS 84) to **EPSG:32644 (WGS 84 / UTM zone 44N)** using **Reproject Layer**, so that distances are measured in metres.

Outputs: `*_utm44.gpkg` in `data/processed/`.

## 4. Analysis

### 4.1 Buffer
A **100-metre buffer** was generated around major roads using **Vector → Geoprocessing → Buffer** with the *Dissolve result* option enabled, producing a single merged buffer polygon.

Output: `data/processed/roads_buffer_100m.gpkg`

### 4.2 Spatial Selection
**Extract by Location** was used with the *intersects* predicate to select parks and gardens that touch or overlap the buffer.

Outputs:
- `data/processed/parks_near_roads.gpkg`
- `data/processed/gardens_near_roads.gpkg`

### 4.3 Statistics
Feature counts of the input and extracted layers were compared to calculate the percentage of green spaces intersecting the buffer. Results are documented in [`data/analysis/analysis.md`](../data/analysis/analysis.md).

## 5. Cartography

A two-scale thematic map was designed in **QGIS Print Layout**:
- City-wide overview of parks, gardens, road network and the buffer.
- Detailed urban inset including building footprints.

Exports: `maps/Pokhara Green Space Analysis.pdf` and `maps/PokharaGreenSpace.png`.

## 6. Workflow Summary

```
Raw OSM data ──► Clip to Pokhara ──► Reproject (EPSG:32644)
                                            │
                     Major roads ──► 100 m dissolved buffer
                                            │
          Parks / Gardens ──► Extract by Location (intersects)
                                            │
                           Count & percentage statistics
                                            │
                              Print Layout thematic map
```

## 7. Limitations

- OpenStreetMap data may not include every existing park, garden or road.
- The analysis uses feature counts rather than green-space area.
- A polygon intersecting the buffer does not mean the entire green space is within 100 metres.
- Road proximity does not establish pedestrian access, noise exposure or environmental quality.
