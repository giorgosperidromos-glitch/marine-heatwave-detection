**English | [Ελληνικά](README.el.md)**

# Marine Heatwaves in the Patraikos Gulf and Ionian Sea (1982–2026) from Satellite SST Data

*Ανίχνευση και ανάλυση θαλάσσιων καυσώνων στον Πατραϊκό Κόλπο και το Ιόνιο με δορυφορικά δεδομένα SST*

> Developed in collaboration with my brother, **Panagiotis Peridromos**, an undergraduate student of Oceanography and Marine Biosciences at the University of the Aegean.

## Overview

This project detects and analyzes Marine Heatwave (MHW) episodes using satellite Sea Surface Temperature (SST) data from the Copernicus Marine Service at two scales:

- A **reference point in the Patraikos Gulf** (Patras area), analyzed as a daily time series.
- A **wider spatial region in the Ionian Sea**, off Kyllini–Kefalonia–Araxos (west of the Gulf entrance), analyzed grid cell by grid cell.

Marine heatwaves are detected following the Hobday et al. (2016, 2018) definition, using a fixed 30-year baseline period (1982–2011). The results cover the period from 1982 to 23 July 2026.

![Marine heatwave days per year, Gulf of Patras](figures/mhw_days_per_year.png)

## Key results

**Patraikos Gulf (reference point)**

- A total of 149 marine heatwave events were detected.
- Marine heatwave days per year show a clear upward trend over time: mostly low until 2011, exceeding 100 days in most years after 2018.
- **2024 set the record with 246 heatwave days** (2025: 168, 2023: 166).
- The most intense event by peak intensity occurred in **June 2007** (4.27 °C above climatology, lasting 15 days). 2024 experienced two of the three most intense events: March–April (36 days, 4.13 °C, categorized as Extreme) and July–October (83 days, 4.09 °C).
- The longest events were winter episodes (126 days, Nov 2015–Mar 2016; 124 days, Nov 2024–Mar 2025) with lower intensity (1.8–2.8 °C). These likely reflect a general shift in temperatures above the historical climatology rather than discrete heatwaves.

![SST, climatology and threshold with detected events](figures/mhw_timeseries.png)

**Ionian Sea (spatial analysis)**

- The mean number of heatwave days per year in the study area increased from **23.6 (1982–2011)** to **154 (2016–2025)**.
- The signal is spatially fairly uniform across the region (146–167 days per grid cell during 2016–2025), pointing to a large-scale warming signal rather than a localized feature.
- The increase is most pronounced in the northwest of the region (open sea) and smallest near the eastern coast. The underlying causes have not been investigated.

![Heatwave days per year per grid cell](figures/mhw_days_per_pixel.png)

**Sensitivity to the baseline period**

Using a 1982–2025 baseline instead of 1982–2011 reduces the number of detected events from 149 to 77 and decreases the total number of heatwave days by about 56%. Nevertheless, the overall pattern (an upward trend with 2024 remaining the record year, now with 157 days) remains unchanged. This demonstrates that while absolute numbers depend on the choice of baseline, the qualitative findings are robust.

![Sensitivity to the baseline period](figures/mhw_baseline_sensitivity.png)

## Data

- **Source:** [Copernicus Marine Service](https://data.marine.copernicus.eu)
- **Dataset:** `cmems_SST_MED_SST_L4_REP_OBSERVATIONS_010_021` — Mediterranean Sea High Resolution L4 Sea Surface Temperature Reprocessed
- **Resolution:** 0.05°, daily
- **Period:** 1 January 1982 – 23 July 2026 (end of the dataset at the time of download)
- **Variable:** `analysed_sst` (Kelvin, converted to °C)
- **Reference point:** 21.68–21.78 °E, 38.20–38.30 °N (the retrieved extent contains approximately 2×2 grid cells, which are averaged)
- **Spatial region:** 20.77–21.45 °E, 37.90–38.30 °N (7×13 grid cells, part of which covers land)

## Methodology

1. Daily climatology and the 90th-percentile threshold are computed using the **1982–2011** baseline.
2. A marine heatwave is defined as a period above the threshold lasting at least **5 consecutive days** (default `xmhw` parameters).
3. Events are categorized as Moderate / Strong / Severe / Extreme (Hobday et al., 2018).
4. Heatwave days per year correspond to total days that fall within detected events. 2026 is excluded from annual statistics as the year is incomplete.
5. A sensitivity analysis repeats the procedure using the 1982–2025 baseline.

Implemented with [`xmhw`](https://github.com/coecms/xmhw), an xarray-based Python implementation of the marine heatwave algorithm by Eric Oliver.

## Repository structure