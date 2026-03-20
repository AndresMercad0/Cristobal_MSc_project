# Data Dictionary — 10_months_data_Cristobal

## Overview

This dataset contains **filtered raw data** from the Low-Cost QMUL Air Quality Monitoring Sensor Network, extracted for Cristobal's analysis. Each CSV file corresponds to a single node or reference station and includes only **metadata columns plus temperature, humidity, PM2.5, and PM10** (for low-cost nodes) or **metadata plus PM2.5** (for high-cost reference stations).

**Data Collection Period:** April 16, 2025 to February 15, 2026 (~10 months)

**Source:** Raw wide-format CSVs downloaded from a local database server at the QMUL IoT Lab (low-cost nodes 1–7) and the LondonAir API (high-cost reference stations TH2, TH7). No resampling, calibration, or gap-filling has been applied — data is preserved at original collection frequencies.

**Contact:** Andrés A. Mercado-Velázquez ([a.mercadovelazquez@qmul.ac.uk](mailto:a.mercadovelazquez@qmul.ac.uk))

---

## Study Locations

| NodeID | Site | Subsite | Exposure | Environment | Period | Latitude | Longitude |
|--------|------|---------|----------|-------------|--------|----------|-----------|
| node_1 | Queen Mary University of London | Peter Landin Building — Stefan's office (window) | Outdoor | Pedestrian open space | Full period | 51.523158 | −0.042900 |
| node_2 | Queen Mary University of London | Peter Landin Building — Stefan's office (room) | Indoor | Natural ventilation, occupied ×1 | Full period | 51.523176 | −0.042907 |
| node_3 | Queen Mary University of London | Mile End Road | Outdoor | Urban traffic roadside | Full period | 51.522530 | −0.042155 |
| node_4 | Queen Mary University of London | Engineering Building (adjacent room to Mile End Road) | Indoor | Mechanical ventilation, unoccupied | Full period | 51.522586 | −0.042202 |
| node_5 | King Edward Memorial Park | Glamis Rd & A1203 | Outdoor | Urban traffic roadside | Full period | 51.509477 | −0.050541 |
| node_6 | Queen Mary University of London | Engineering Building (window) → People's Palace (window) | Outdoor | Pedestrian open space | Full period* | 51.523036 → 51.523179 | −0.041493 → −0.041315 |
| node_7 | Queen Mary University of London | Engineering Building (room) → People's Palace (room) | Indoor | Mixed → Mechanical ventilation | Full period* | 51.523042 → 51.523192 | −0.041542 → −0.041298 |
| node_TH2_MER | Queen Mary University of London | Mile End Road | Outdoor | Roadside — Urban Traffic | Full period | 51.522530 | −0.042155 |
| node_TH7_KEMP | King Edward Memorial Park | Glamis Rd & A1203 | Outdoor | Roadside — Urban Traffic | Full period | 51.509477 | −0.050541 |

*\*Nodes 6 and 7 were relocated between June 16–19, 2025 due to institutional space repurposing. See [Node Relocation Event](#node-relocation-event) below.*

### Indoor–Outdoor Pairs

| Pair | Outdoor Node | Indoor Node | Location |
|------|-------------|-------------|----------|
| 1–2 | node_1 | node_2 | Stefan's office area |
| 3–4 | node_3 | node_4 | Mile End Road |
| 6–7 | node_6 | node_7 | Engineering Building → People's Palace |

### Co-location with Reference Stations

| Low-cost Node | Reference Station | Location |
|---------------|-------------------|----------|
| node_3 | node_TH2_MER (Tower Hamlets TH2) | QMUL Mile End Road |
| node_5 | node_TH7_KEMP (Tower Hamlets TH7) | King Edward Memorial Park |

---

## Sensor Categories

### Low-Cost Sensors — All 7 Nodes (~£10–100)

| Sensor Model | Manufacturer | Variables in this dataset | Units | Range | Sampling Frequency |
|-------------|-------------|--------------------------|-------|-------|-------------------|
| SHT45 | Sensirion | Temperature, Humidity | °C, % | −40 to +125 °C, 0 to 100% | 30 seconds |
| SPS30 | Sensirion | PM2.5, PM10 | μg/m³ | 0 to 1000 μg/m³ | 30 seconds |

### High-Cost Reference Stations — TH2 and TH7 (>£20,000)

| Station | Operator | Variables in this dataset | Units | Sampling Frequency |
|---------|----------|--------------------------|-------|-------------------|
| TH2 (QMUL Mile End Road) | Tower Hamlets Borough | PM2.5 | μg/m³ | 15 minutes |
| TH7 (King Edward Memorial Park) | Tower Hamlets Borough | PM2.5 | μg/m³ | 15 minutes |

---

## CSV Files Structure

### File Naming Convention

`{node_id}_filtered.csv`

### Files Included

| File | Node | Sensor Cost | Rows | Measurement Columns |
|------|------|-------------|------|---------------------|
| `node_1_filtered.csv` | node_1 | Low | ~660k | temperature, humidity, PM2.5, PM10 |
| `node_2_filtered.csv` | node_2 | Low | ~820k | temperature, humidity, PM2.5, PM10 |
| `node_3_filtered.csv` | node_3 | Low | ~525k | temperature, humidity, PM2.5, PM10 |
| `node_4_filtered.csv` | node_4 | Low | ~560k | temperature, humidity, PM2.5, PM10 |
| `node_5_filtered.csv` | node_5 | Low | ~516k | temperature, humidity, PM2.5, PM10 |
| `node_6_filtered.csv` | node_6 | Low | ~721k | temperature, humidity, PM2.5, PM10 |
| `node_7_filtered.csv` | node_7 | Low | ~706k | temperature, humidity, PM2.5, PM10 |
| `node_TH2_MER_filtered.csv` | node_TH2_MER | High | ~29k | PM2.5 |
| `node_TH7_KEMP_filtered.csv` | node_TH7_KEMP | High | ~29k | PM2.5 |

---

## Column Descriptions

### Metadata Columns (All Files)

| Column | Description | Data Type | Example |
|--------|-------------|-----------|---------|
| `timestamp_utc` | Timestamp in UTC, ISO 8601 format | String (YYYY-MM-DDTHH:MM:SSZ) | 2025-04-16T00:00:23Z |
| `node_id` | Unique identifier of the monitoring node | String | node_1 |
| `site` | Deployment site name | String | Queen Mary University of London |
| `subsite` | Specific location within the site | String | Mile End Road |
| `exposure` | Indoor or Outdoor | String | Outdoor |
| `environment` | Description of the microenvironment | String | Urban traffic roadside |
| `latitude` | Latitude (WGS84) | Numeric | 51.523158 |
| `longitude` | Longitude (WGS84) | Numeric | −0.042900 |

### Measurement Columns — Low-Cost Nodes (node_1 through node_7)

| Column | Sensor | Description | Units | Range | Precision |
|--------|--------|-------------|-------|-------|-----------|
| `temperature_low_sht45_celsius` | SHT45 (Sensirion) | Ambient temperature | °C | −40 to +125 | 2 decimal places |
| `humidity_low_sht45_percentage` | SHT45 (Sensirion) | Relative humidity | % | 0 to 100 | 2 decimal places |
| `pm2_5_low_sps30_ug_m3` | SPS30 (Sensirion) | PM2.5 mass concentration | μg/m³ | 0 to 1000 | ±10% |
| `pm10_low_sps30_ug_m3` | SPS30 (Sensirion) | PM10 mass concentration | μg/m³ | 0 to 1000 | ±10% |

### Measurement Columns — High-Cost Stations (node_TH2_MER, node_TH7_KEMP)

| Column | Station | Description | Units | Precision |
|--------|---------|-------------|-------|-----------|
| `pm2_5_high_met_one_ug_m3` | Met One Instruments (Tower Hamlets Borough) | PM2.5 reference measurement | μg/m³ | As reported by station |

---

## Data Quality and Processing Notes

### Temporal Information

- **Low-cost frequency**: 30 seconds
- **High-cost frequency**: 15 minutes (900 seconds)
- **Timezone**: All timestamps in UTC
- **Period**: April 16, 2025 to February 15, 2026

### Missing Data

Missing data points appear as empty cells. These occur naturally due to sensor interruptions, connectivity issues, or maintenance periods. **No gap-filling or NaN substitution has been applied.**

### Calibration Status

- **Low-cost (SHT45)**: Factory-calibrated temperature and humidity
- **Low-cost (SPS30)**: Factory-calibrated PM2.5 and PM10 (mass concentration in μg/m³)
- **High-cost (Met One)**: Continuously calibrated and QA/QC-validated reference measurements

### High-Cost Station Data Quality

| Station | Total Rows | PM2.5 NaN | PM2.5 Range (μg/m³) | PM2.5 Mean (μg/m³) |
|---------|-----------|-----------|---------------------|---------------------|
| node_TH2_MER | 29,282 | 2,187 (7.47%) | −5 to 97 | 7.59 |
| node_TH7_KEMP | 29,330 | 4,270 (14.56%) | −10 to 72 | 8.83 |

**Notes:**
- Occasional negative values in PM2.5 are artefacts of the reference instrumentation, not download errors.
- node_TH7_KEMP PM2.5 has 14.56% NaN, concentrated in Dec 2025 and Jan 2026 (probable instrument maintenance).

### Node Relocation Event

**Period:** June 16–19, 2025 (3-day data gap for nodes 6 and 7)

Nodes 6 and 7 were relocated due to institutional space repurposing at QMUL.

| Node | Spatial Continuity | Microenvironment Change | Analysis Recommendation |
|------|-------------------|------------------------|------------------------|
| node_6 (Outdoor) | HIGH — ~15 m displacement, same pedestrian area | Minimal | Unified analysis with relocation indicator |
| node_7 (Indoor) | MODERATE — ~15 m displacement, different building/HVAC | Significant — building and ventilation system changed | Segmented analysis with validation |

**Location changes:**
- **node_6**: Engineering Building window (51.523036, −0.041493) → People's Palace window (51.523179, −0.041315)
- **node_7**: Engineering Building room (51.523042, −0.041542) → People's Palace room (51.523192, −0.041298)

---

## Column Naming Convention

Column names follow the pattern: `{variable}_{cost}_{model}_{units}`

- **variable**: physical quantity (`temperature`, `humidity`, `pm2_5`, `pm10`)
- **cost**: sensor cost tier (`low`, `high`)
- **model**: sensor model (`sht45`, `sps30`, `met_one`)
- **units**: measurement unit (`celsius`, `percentage`, `ug_m3`)

---

## Institution

**Queen Mary University of London**
IoT2US Lab — http://iot.eecs.qmul.ac.uk/
School of Electronic Engineering & Computer Science

## Contact

**Andrés A. Mercado-Velázquez**
[a.mercadovelazquez@qmul.ac.uk](mailto:a.mercadovelazquez@qmul.ac.uk)

---

*This dataset contains filtered raw environmental measurements (temperature, humidity, PM2.5, PM10) from a network of 7 low-cost air quality monitoring nodes and 2 government reference stations deployed at Queen Mary University of London and King Edward Memorial Park, London, UK. Data covers approximately 10 months (April 2025 – February 2026).*
