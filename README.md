# Monthly Water Balance - GEE
 
## Notebook Summary

- **File:** `Monthly_Water_Balance-GEE.ipynb`
- **Purpose:** Compute and visualize a basin-scale water balance using Google Earth Engine (GEE). The notebook runs a simple water-balance model over a user-selected HydroBASINS basin and a point of interest, producing time-series and spatial summaries.
- **Key features:**
	- Interactive map (via `geemap`) to select a basin and point of interest from HydroBASINS.
	- Uses TerraClimate (`IDAHO_EPSCOR/TERRACLIMATE`) inputs (precipitation, PET, runoff) and custom assets for water-holding capacity and recession constants.
	- Implements a monthly water-balance iteration (via `otherfunctions.water_balance`) to compute variables such as effective precipitation, AET, soil storage, percolation, baseflow and water yield.
	- Produces point-level `pandas` dataframes, annual and monthly spatial composites, plots, and video thumbnail URLs for visual inspection.
- **Requirements:**
	- Python packages: `earthengine-api`, `geemap`, `pandas`, `matplotlib` and supporting IPython widgets.
	- The helper module `otherfunctions` (provides `water_balance`, `ee_array_to_df`, `determine_period`).
	- An authenticated GEE account and access to the `ee-jvg` project assets used in the notebook.
- **How to run (high-level):**
	1. Authenticate and initialize GEE in the notebook (`ee.Authenticate()` then `ee.Initialize(project='ee-jvg')`).
	2. Open the interactive map and click a basin/point of interest (required before continuing).
	3. Set the analysis period and warm-up years, then run the cells sequentially.
	4. Inspect resulting dataframes, plots, and exported image collections/video thumbnails.
- **Notes & caveats:**
	- The notebook includes a `SystemExit` guard that stops execution until a basin/point is selected interactively.
	- A warm-up period (recommended ~5 years) is advised for model equilibration.
	- Converting large multi-year results to a point dataframe can fail for very long simulations (the notebook warns about ~>11 years monthly output causing large data retrievals).
	- **Based on:** Implementation of the Thornthwaite-Mather procedure to map groundwater recharge — Google Earth Engine community tutorial: https://developers.google.com/earth-engine/tutorials/community/groundwater-recharge-estimation

