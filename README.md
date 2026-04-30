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

**Primary Data:** [US Census Bureau Nonemployer Statistics (NES)](https://www.census.gov/programs-surveys/nonemployer-statistics/data/datasets.html)

**County Boundaries:** [US Census Bureau TIGER/Line Shapefiles](https://www.census.gov/geographies/mapping-files/time-series/geo/tiger-line-file.html)

| Dataset | Source | Years Used |
|---|---|---|
| Nonemployer Statistics County CSV | US Census Bureau NES | 2018 and 2023 |
| County Boundary Shapefile | US Census TIGER/Line | 2022 release |

- **Initial Data Projection:** NAD83 Geographic Coordinate System (EPSG 4269)
- **Final Map Projection:** NAD83 Geographic Coordinate System (EPSG 4269)

---

## Project Background

The gig economy has reshaped the American labor market over the past decade. Platforms like DoorDash, Amazon Flex, Instacart, and UPS independent contracting have created millions of new courier and delivery jobs — but these workers are classified as independent contractors, not employees. They appear in government data not as workers but as **nonemployer businesses** — sole proprietors with no paid staff.

The US Census Bureau's Nonemployer Statistics program captures these workers through annual county-level counts of establishments by industry. By filtering for **NAICS 492 — Couriers and Messengers**, we can track the geographic rise of gig delivery work across every US county from 2018 to 2023.

---

## Purpose

This map was created to visualize the dramatic geographic expansion of courier and messenger gig work across the United States between 2018 and 2023 — a period that includes the COVID-19 pandemic, which accelerated demand for delivery services nationwide.

The map asks: **where did the gig delivery economy surge most dramatically, and where did it not?** The answer reveals patterns of platform economy growth that connect to urban density, income levels, and infrastructure access.

---

## Mapmaking Process

The map was created using the following steps. Another mapper could follow these steps to recreate this map for any time period or industry code.

### 1. Data Download

- Downloaded county-level NES CSV files for 2018 and 2023 from the Census Bureau NES datasets page
- Downloaded the US county TIGER/Line shapefile (tl_rd22_us_county.zip) from the Census Bureau TIGER page
- Organized all raw files into a `data-raw` folder

### 2. Data Cleaning in Google Sheets

- Opened both NES CSV files in Google Sheets
- Filtered each file for **NAICS code 492** (Couriers and Messengers) — resulting in approximately 2,959 rows per year
- Created a **GEOID** column by combining the state FIPS code (padded to 2 digits) and county FIPS code (padded to 3 digits) using the formula:
