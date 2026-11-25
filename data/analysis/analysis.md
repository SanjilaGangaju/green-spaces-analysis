# Analysis: Green Space Proximity to Major Roads

## Objective

Quantify how many mapped parks and gardens in Pokhara Metropolitan City intersect a 100-metre buffer around mapped major roads.

## Input Layers

| Layer | File | Description |
|---|---|---|
| Parks | `data/processed/parks_utm44.gpkg` | OSM park polygons, clipped and reprojected |
| Gardens | `data/processed/gardens_utm44.gpkg` | OSM garden polygons, clipped and reprojected |
| Major roads | `data/processed/major_roads_utm44.gpkg` | OSM major roads, clipped and reprojected |
| Road buffer | `data/processed/roads_buffer_100m.gpkg` | Dissolved 100 m buffer around major roads |

## Output Layers

| Layer | File | Description |
|---|---|---|
| Parks near roads | `data/processed/parks_near_roads.gpkg` | Parks intersecting the buffer |
| Gardens near roads | `data/processed/gardens_near_roads.gpkg` | Gardens intersecting the buffer |

## Results

| Category | Total | Within buffer | Outside buffer | Percentage within |
|---|---:|---:|---:|---:|
| Parks | 73 | 19 | 54 | 26.03% |
| Gardens | 14 | 8 | 6 | 57.14% |
| Combined | 87 | 27 | 60 | 31.03% |

**Calculation:** Percentage = (features intersecting buffer ÷ total features) × 100

- Parks: 19 ÷ 73 × 100 = 26.03%
- Gardens: 8 ÷ 14 × 100 = 57.14%
- Combined: 27 ÷ 87 × 100 = 31.03%

## Key Findings

1. **Roughly one in three** mapped green spaces (27 of 87) intersects the 100 m major-road buffer.
2. **Gardens are more road-adjacent than parks:** 57.14% of gardens intersect the buffer compared with 26.03% of parks.
3. **Most parks lie away from major roads:** 54 of 73 parks (73.97%) do not intersect the buffer.
4. The garden sample is small (14 features), so its percentage is sensitive to individual features.

## Interpretation

The results describe spatial proximity only. A green space intersecting the buffer is near a major road, but this does not confirm pedestrian accessibility, entrance location, noise exposure or environmental quality.

## Caveats

- Counts are feature-based, not area-based; a large park and a small garden are weighted equally.
- Partial intersection counts as "within buffer".
- Results depend on the completeness of OpenStreetMap data for Pokhara.
