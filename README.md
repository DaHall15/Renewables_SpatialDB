> # Renewable Energy Group Project

**Analyzing siting options for renewables in the Massachusetts towns of Bernardston, Northfield, and Gill**

_Daniel Hall, Binghui Li, Fletcher Harrington_  
_3/20/2024_

## Objectives

The primary objectives for this project:

- Acquire spatial data for focus area describing land cover, wind speed, irradiance, and elevation
- Create database and table schema for data sources and normalize as necessary
- Analayze suitability of lands in focus area for renewable energy siting

## Data

Data sources so far are as follows:

| Name             | Source  | Data type | format      | Resolution               | link (if applicable)                                        |
| ---------------- | ------- | --------- | ----------- | ------------------------ | ----------------------------------------------------------- |
| Solar Irradiance | NREL    | raster    | jpg, 300dpi | 4km x 4km                | nrel.gov/gis/solar-resource-maps.html                       |
| NLCD 2021        | USGS    | raster    | tif         | 30m                      | mrlc.gov/                                                   |
| Wind Speed       | MassGIS | vector    | shp         | 250m x 250m              | mass.gov/info-details/massgis-data-modeled-wind-speed-grids |
| Land Elevation   | USGS    | raster    | tif         | 1 km x 1 km (30 arc sec) | topotools.cr.usgs.gov/gmted_viewer/viewer.htm               |
| Town Boundaries  | MassGIS | vector    | shp         | n/a                      | maps.massgis.digital.mass.gov/MassMapper/MassMapper.html    |

## Data Processing

- All spatial data was reprojected to EPS:26986
- All spatial data was clipped to the merged town boundaries
- Centroids and Lat/lng coordinates were created for gridded datasets

### Planned Table Schemas

**Towns**: town_id (int primary ID serial), town_name (varchar 255), geom

**Land Use 2016**: OBJECTID (int primary ID serial), covercode (int), covername (varchar 255), geom

**Wind Speed**: OBJECTID (int primary ID serial), SPD30 (int), Geom (Shape), X_COORD (int), Y_COORD (int)

**Solar Irradiance**: OBJECTID (int primary ID serial), Band1 - Solar Irradiance (float)

**Elevation**: OBJECTID (int primary ID serial), Band 1 - Elevation (float)

### Data Examples

<img src="DataScreenShots/windspeed_towns.png" alt="windspeed" style ="width: 800px"></img>  
Windspeed

<img src="DataScreenShots/landcover_towns.png" alt="landcover" style ="width: 800px"></img>  
Landcover


### Data Normalization 
- Wind Speed : Once imported into database, non-essential fields were dropped using the three following queries in pgAdmin :
```
ALTER TABLE windspeed
DROP COLUMN x_coords;

ALTER TABLE windspeed
DROP COLUMN x_coords;

ALTER TABLE windspeed
DROP COLUMN objectid;
```