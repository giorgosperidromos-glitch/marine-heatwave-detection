**English | [Ελληνικά](README.el.md)**

# Marine Heatwaves in the Patraikos Gulf and Ionian Sea (1982–2026) from Satellite SST Data

*Ανίχνευση και ανάλυση θαλάσσιων καυσώνων στον Πατραϊκό Κόλπο και το Ιόνιο με δορυφορικά δεδομένα SST*

> Developed in collaboration with my brother, **Panagiotis Peridromos**, an undergraduate student of Oceanography and Marine Biosciences at the University of the Aegean.

## Overview

This project detects and analyzes Marine Heatwave (MHW) episodes with satellite Sea Surface Temperature (SST) data from the Copernicus Marine Service, at two scales:

- a **reference point in the Patraikos Gulf** (Patras area), analysed as a daily time series;
- a **wider spatial region in the Ionian Sea**, off Kyllini–Kefalonia–Araxos (west of the Gulf entrance), analysed grid cell by grid cell.

Marine heatwaves are detected with the Hobday et al. (2016, 2018) definition, using a fixed 30-year baseline (1982–2011), and results are described for 1982 – 23 July 2026.

![Marine heatwave days per year, Gulf of Patras](figures/mhw_days_per_year.png)

## Key results

**Patraikos Gulf (reference point)**

- 149 marine heatwave events were detected.
- Marine-heatwave days per year rise clearly over time: mostly low until 2011, above 100 days in most years after 2018.
- **2024 is the record year with 246 heatwave days** (2025: 168, 2023: 166).
- The most intense event by peak intensity occurred in **June 2007** (4.27 °C above climatology, 15 days). 2024 has two of the three most intense events: March–April (36 days, 4.13 °C, category Extreme) and July–October (83 days, 4.09 °C).
- The longest events are winter episodes (126 days Nov 2015–Mar 2016; 124 days Nov 2024–Mar 2025) with lower intensity (1.8–2.8 °C). They probably reflect a general shift of temperatures above the old climatology rather than discrete heatwaves.

![SST, climatology and threshold with detected events](figures/mhw_timeseries.png)

**Ionian Sea (spatial analysis)**

- The mean number of heatwave days per year in the study area increased from **23.6 (1982–2011)** to **154 (2016–2025)**.
- The signal is spatially fairly uniform (146–167 days per grid cell in 2016–2025), which points to a large-scale warming signal rather than a local feature.
- The increase is largest in the north-west of the region (open sea) and smallest near the eastern coast. The cause has not been investigated.

![Heatwave days per year per grid cell](figures/mhw_days_per_pixel.png)

**Sensitivity to the baseline period**

Using a 1982–2025 baseline instead of 1982–2011 reduces the number of detected events from 149 to 77 and the total number of heatwave days by about 56%. The overall pattern (upward trend, 2024 as the record year, now with 157 days) is unchanged, so the qualitative findings are robust while the absolute numbers depend on the baseline.

![Sensitivity to the baseline period](figures/mhw_baseline_sensitivity.png)

**Statistical assessment of the trend (annual heatwave days, 1982–2025, baseline 1982–2011)**

- **Cox–Stuart test:** in all 22 pairs of years (first half vs second half of the series) the later year has more heatwave days (p < 10⁻⁶ at the Gulf of Patras and in the Ionian area mean).
- **Least-squares regression:** on average **+3.7 heatwave days per year, every year** at the Gulf of Patras (95% CI 2.9–4.5, R² = 0.65) and +4.4 for the Ionian area mean (95% CI 3.4–5.3, R² = 0.67). With the 1982–2025 baseline the Patras slope is smaller (+1.95, 95% CI 1.37–2.53), so the magnitude depends on the baseline.
- **Quadratic term:** significant in an F-test (p ≈ 0.001 in both series), so the increase is not linear but accelerating, and the linear slope is an average rate.
- **Period comparison:** median annual heatwave days rose from 18 (1982–2011) to 131 (2016–2025) at the Gulf of Patras and from 10 to 151 in the Ionian area (Mann–Whitney p ≈ 10⁻⁵, two-sample Kolmogorov–Smirnov D = 0.87 and 0.90). Because the threshold was computed from 1982–2011, those years have about 10% exceedance by construction, so this comparison measures the size of the shift rather than providing independent confirmation.
- **Residual check:** the lag-1 autocorrelation of the linear model's residuals is 0.42 at the Gulf of Patras (approximate 95% band ±0.30), partly because of the curvature. For the quadratic model it is 0.25.

![MHW days per year with linear and quadratic fits](figures/mhw_days_trend.png)

## Data

- **Source:** [Copernicus Marine Service](https://data.marine.copernicus.eu)
- **Dataset:** `cmems_SST_MED_SST_L4_REP_OBSERVATIONS_010_021` — Mediterranean Sea High Resolution L4 Sea Surface Temperature Reprocessed
- **Resolution:** 0.05°, daily
- **Period:** 1 January 1982 – 23 July 2026 (end of the dataset at time of download)
- **Variable:** `analysed_sst` (Kelvin, converted to °C)
- **Reference point:** 21.68–21.78 °E, 38.20–38.30 °N (the returned extent contains about 2×2 grid cells, which are averaged)
- **Spatial region:** 20.77–21.45 °E, 37.90–38.30 °N (7×13 grid cells, part of it land)

## Methodology

1. Daily climatology and the 90th-percentile threshold are computed from the **1982–2011** baseline.
2. A marine heatwave is a period above the threshold lasting at least **5 consecutive days** (default `xmhw` parameters).
3. Events are categorised as Moderate / Strong / Severe / Extreme (Hobday et al., 2018).
4. Heatwave days per year are the days that fall inside a detected event. 2026 is excluded from annual statistics because it is incomplete.
5. A sensitivity test repeats the analysis with a 1982–2025 baseline.
6. The trend in annual heatwave days is assessed with the Cox–Stuart test and with linear and quadratic least-squares regression (95% confidence interval for the slope, F-test for the quadratic term, residual autocorrelation). The periods 1982–2011 and 2016–2025 are compared with the Mann–Whitney and two-sample Kolmogorov–Smirnov tests.

Implemented with [`xmhw`](https://github.com/coecms/xmhw), an xarray-based implementation of the marine heatwave algorithm of Eric Oliver.

## Repository structure

```
├── ocean_analysis.ipynb   # Full analysis (data download + detection + figures)
├── figures/               # Figures used in this README
├── requirements.txt       # Python dependencies
├── LICENSE                # MIT
├── README.md              # This file (English)
├── README.el.md           # Greek version
└── data/                  # Created on first run (git-ignored)
```

## Installation and usage

```bash
git clone https://github.com/giorgosperidromos-glitch/marine-heatwave-detection.git
cd marine-heatwave-detection
pip install -r requirements.txt
copernicusmarine login        # free account at data.marine.copernicus.eu
```

Open `ocean_analysis.ipynb` in Jupyter/JupyterLab and run all cells. The data (a few MB) are downloaded automatically in the first cells.

## Limitations

- A single data product (L4 reprocessed, 0.05°, interpolated). There is no validation against in-situ data or another product, and no check of homogeneity over the 44 years. Coastal grid cells are more uncertain.
- Results depend strongly on the baseline period, especially because the sea is warming.
- The "reference point" is an average of about 4 grid cells close to the coast.
- Maximum intensity per grid cell is determined by a single event, and the event count depends on how events are split or merged. Heatwave days per year are a more reliable indicator.
- The trend tests assume independent annual values, but annual heatwave days are serially dependent (lag-1 residual autocorrelation 0.42 for the linear model at the Gulf of Patras), so the p-values of the linear regression are optimistic. The slope and its confidence interval are the more informative results.
- The period comparison (Mann–Whitney, Kolmogorov–Smirnov) is partly circular, because the threshold was defined from 1982–2011.
- No attribution (e.g. to atmospheric heatwaves or local hydrography) was tested.
- The bounding box of the spatial analysis includes land, which has no valid data.

## References

- Hobday, A.J. et al. (2016). A hierarchical approach to defining marine heatwaves. *Progress in Oceanography*, 141, 227–238. doi:10.1016/j.pocean.2015.12.014
- Hobday, A.J. et al. (2018). Categorizing and naming marine heatwaves. *Oceanography*, 31(2), 162–173. doi:10.5670/oceanog.2018.205
- Pastor, F., Paredes-Fortuny, L. & Khodayar, S. (2024). Mediterranean marine heatwaves intensify in the presence of concurrent atmospheric heatwaves. *Communications Earth & Environment*. doi:10.1038/s43247-024-01982-8

## Authors

- **Georgios Peridromos** — Mathematics graduate, University of Patras (Statistics direction)
- **Panagiotis Peridromos** — student of Oceanography and Marine Biosciences, University of the Aegean

## License

MIT License — free use, modification and distribution, with attribution to the original author.

## Contact

Georgios Peridromos — giorgosperidromos@gmail.com
