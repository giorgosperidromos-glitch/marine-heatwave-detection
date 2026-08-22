**English | [Ελληνικά](README.el.md)**

# Detection and Analysis of Marine Heatwaves in the Eastern Mediterranean using Satellite SST Data

*Ανίχνευση και Ανάλυση Θαλάσσιων Καυσώνων στην Ανατολική Μεσόγειο με Δορυφορικά Δεδομένα SST*

## Description

This project detects and analyzes Marine Heatwave (MHW) episodes at two geographic scales: (a) at a
reference point in the Patraikos Gulf (Patras area), and (b) across a wider spatial region in the
Ionian Sea, off Kyllini-Kefalonia-Araxos (west of the Patraikos Gulf entrance). Satellite Sea Surface
Temperature (SST) data from the Copernicus Marine Service is used throughout.

The analysis applies the established Hobday et al. (2016, 2018) methodology for defining and detecting
marine heatwaves, examining both temporal trends (2014-2026) and spatial patterns of intensity/frequency
across the study region.

## Objectives

- Detect marine heatwave episodes at a reference point (Patraikos Gulf, Patras area)
- Analyze frequency/intensity trends of heatwaves from 2014-2026
- Spatial analysis in the Ionian Sea (off Kyllini-Kefalonia-Araxos): identify regions with higher
  heatwave intensity/frequency
- Compare recent years (2024-2026) against the historical baseline

## Data

- **Source**: [Copernicus Marine Service](https://data.marine.copernicus.eu)
- **Dataset**: `SST_MED_SST_L4_REP_OBSERVATIONS_010_021` — Mediterranean Sea High Resolution L4 SST Reprocessed
- **Resolution**: 0.05° spatial resolution, daily data
- **Period**: January 2014 – July 2026
- **Variable**: `analysed_sst` (sea surface temperature, Kelvin -> converted to Celsius)

## Methodology

Marine heatwave detection follows the **Hobday et al. (2016, 2018)** method:

1. Compute the climatology baseline (mean temperature per day-of-year, multi-year average)
2. Compute the heatwave threshold (90th percentile)
3. Identify periods where observed temperature exceeds the threshold for **at least 5 consecutive
   days**
4. Classify severity category (moderate / strong / severe / extreme)

Implemented using the [`xmhw`](https://github.com/coecms/xmhw) library (an xarray-based implementation
of the original algorithm by Eric Oliver).

## Repository Structure

```
├── ocean_analysis.ipynb        # Main analysis notebook (data download + full analysis)
├── requirements.txt            # Required libraries
├── LICENSE                     # License (MIT)
├── README.md                   # This file (English)
├── README.el.md                # Greek version
├── data/                       # Data folder (not pushed to GitHub - see .gitignore)
└── old_scripts/                # Intermediate development scripts (not pushed to GitHub)
```

## Installation & Usage

### 1. Clone the repository
```bash
git clone <repository-url>
cd <folder-name>
```

### 2. Install dependencies
```bash
pip install -r requirements.txt
```

### 3. Copernicus Marine Service account
A free account is required at [data.marine.copernicus.eu](https://data.marine.copernicus.eu).
After installing `copernicusmarine`, log in:
```bash
copernicusmarine login
```

### 4. Run
Open `ocean_analysis.ipynb` in Jupyter/JupyterLab and run the cells in order (data download happens
automatically from the first cells of the notebook).

## Key Findings

- Multiple marine heatwave episodes were detected in the study region over the period 2014-2026
- **2024** stood out as a record year, with the most intense episode (21 days, March-April 2024) and
  the longest-duration episode (46 days, August-September 2024) of the study period
- Spatial analysis in the Ionian Sea (Kyllini-Kefalonia-Araxos) showed increased heatwave intensity
  toward the eastern part of the grid, close to the Patraikos Gulf entrance, possibly due to more
  limited water exchange in the more enclosed waters
- Findings are consistent with the international literature characterizing the Mediterranean as a
  climate change hotspot, with increasing frequency/intensity of marine heatwaves

## Limitations

- The bounding box of the spatial analysis includes portions of land (coastline), which appear as
  areas without valid data (NaN) - confirmed via data quality checks
- The climatology baseline is based on ~12 years of data; the official Hobday definition recommends
  at least a 30-year period for a fully representative baseline

## References

- Hobday, A.J. et al. (2016). "A hierarchical approach to defining marine heatwaves." *Progress in
  Oceanography*.
- Hobday, A.J. et al. (2018). "Categorizing and naming marine heatwaves." *Oceanography*, 31(2), 162-173.
- Pastor, F., Paredes-Fortuny, L. & Khodayar, S. (2024). "Mediterranean marine heatwaves intensify in
  the presence of concurrent atmospheric heatwaves." *Communications Earth & Environment*.

## License

This project is licensed under the [MIT License](https://opensource.org/licenses/MIT) - free use,
modification, and distribution, with attribution to the original author.

## Contact

Georgios Peridromos
e-mail: giorgosperidromos@gmail.com
