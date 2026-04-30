# Courier Nation: The Gig Economy Surge in Delivery Work (2018–2023)

## Project Contents

* [Data Source](#data-source)
* [Project Background](#project-background)
* [Purpose](#purpose)
* [Mapmaking Process](#mapmaking-process)
* [Map Summary](#map-summary)
* [Final Project Link](#final-project-link)

---

## Data Source

Primary Data: [US Census Bureau Nonemployer Statistics (NES)](https://www.census.gov/programs-surveys/nonemployer-statistics/data/datasets.html)

County Boundaries: [US Census Bureau TIGER/Line Shapefiles](https://www.census.gov/geographies/mapping-files/time-series/geo/tiger-line-file.html)

| Dataset | Source | Years Used |
|---|---|---|
| Nonemployer Statistics County CSV | US Census Bureau NES | 2018 and 2023 |
| County Boundary Shapefile | US Census TIGER/Line | 2022 release |

- Initial Data Projection: NAD83 Geographic Coordinate System (EPSG 4269)
- Final Map Projection: NAD83 Geographic Coordinate System (EPSG 4269)

---

## Project Background

The gig economy has reshaped the American labor market over the past decade. Platforms like DoorDash, Amazon Flex, Instacart, and UPS independent contracting have created millions of new courier and delivery jobs, but these workers are classified as independent contractors, not employees. They appear in government data not as workers but as nonemployer businesses. 

The US Census Bureau's Nonemployer Statistics program captures these workers through annual county-level counts of establishments by industry. By filtering for 'NAICS 492 — Couriers and Messengers', we can track the geographic rise of gig delivery work across every US county from 2018 to 2023.

---

## Purpose

This map was created to visualize the dramatic geographic expansion of courier and messenger gig work across the United States between 2018 and 2023 — a period that includes the COVID-19 pandemic, which accelerated demand for delivery services nationwide.

The map asks: where did the gig delivery economy surge most dramatically, and where did it not? The answer reveals patterns of platform economy growth that connect to urban density, income levels, and infrastructure access.

---

## Mapmaking Process

The map was created using the following steps. Another mapper could follow these steps to recreate this map for any time period or industry code.

### 1. Data Download

- Downloaded county-level NES CSV files for 2018 and 2023 from the Census Bureau NES datasets page
- Downloaded the US county TIGER/Line shapefile (tl_rd22_us_county.zip) from the Census Bureau TIGER page
- Organized all raw files into a `data-raw` folder

### 2. Data Cleaning in Google Sheets

- Opened both NES CSV files in Google Sheets
- Filtered each file for NAICS code 492 (Couriers and Messengers) — resulting in approximately 2,959 rows per year
- Created a GEOID column by combining the state FIPS code (padded to 2 digits) and county FIPS code (padded to 3 digits) using the formula: =TEXT(A2,"00")&TEXT(B2,"000")
- Kept only columns: GEOID, ST, CTY, ESTAB (renamed to ESTAB_2023 and ESTAB_2018)
- Combined both years into a single sheet
- Calculated percent change using: =(ESTAB_2023 - ESTAB_2018) / ESTAB_2018 * 100
- - Saved the final merged file as `couriers_final.csv` in the `data-clean` folder

### 3. QGIS — Joining Data to Shapefile

- Opened QGIS and loaded the county shapefile `tl_rd22_us_county.shp`
- Added `couriers_final.csv` as a delimited text layer with 'no geometry'
- Set project CRS to EPSG 4269 (NAD83)
- Joined the CSV to the shapefile via Layer Properties → Joins using GEOID as the join key
- Verified the join by opening the attribute table and confirming PCT_CHANGE columns appeared

### 4. QGIS — Styling the Choropleth

- Opened Layer Properties → Symbology
- Changed from Single Symbol to Graduated
- Set Value field to `couriers_final_PCT_CHANGE`
- Applied YlOrRd (Yellow to Red) color ramp
- Set classification mode to Natural Breaks (Jenks) with 5 classes
- Clicked Classify to generate breaks
- Grey color applied to counties with no data

### 5. QGIS — Print Layout

- Created a new Print Layout named `courier-nation-map`
- Added map canvas, title, subtitle, legend, scale bar, north arrow, and metadata text box
- Legend labels edited to: Decline, Low Growth, Moderate Growth, High Growth, Very High Growth
- Metadata included: author, projection, data source, NAICS code, software used

### 6. Export

- Exported at 150 DPI → `courier-nation-1200px.png`
- Exported at 400 DPI → `courier-nation-8000px.png`
- Both saved to `maps` folder

---

## Map Summary

The map reveals that courier and messenger gig work grew across nearly every region of the United States between 2018 and 2023. Growth was strongest in suburban counties surrounding major metro areas, reflecting the expansion of last-mile delivery infrastructure. Rural counties showed more modest growth or no change, consistent with limited platform availability in low-density areas. A small number of counties experienced declines, potentially reflecting market consolidation among delivery platforms.

The five-year period captured by this map includes the COVID-19 pandemic (2020–2021), which dramatically accelerated consumer demand for delivery services and likely accounts for a significant portion of the growth visible in the map.

---

## Final Project Link

[View the final map online](https://raktimakalita54-blip.github.io/courier-nation-map/)
