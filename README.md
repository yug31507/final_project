# final_project
# Air Quality Data Analysis Pipeline

## 1. Overview

This Python script performs automated data cleaning, normalization, advanced statistical grouping, intra-group correlation analysis, and visualization on air quality monitoring datasets (such as UCI Air Quality datasets). 

Unlike interactive menu-driven scripts, this pipeline executes directly from start to finish, making it ideal for automated batch processing, Jupyter Notebooks, or script execution via terminal.

---

## 2. Key Steps & Functionality

### A. Data Loading and Normalization
* Reads semicolon-separated CSV files (`airquality.csv`).
* Automatically drops empty or unnecessary index columns (`^Unnamed`).
* Resolves European-style decimal notation by replacing commas (`,`) with dots (`.`).
* Converts columns to numeric types while handling text/corrupted values gracefully.
* Replaces standard environmental sensor error flags (`-200.0`) with `NaN` (missing values).

### B. Feature Engineering & Temporal Processing
* Converts date columns into standard datetime objects (`%d/%m/%Y`).
* Extracts month names (`Month`) to enable seasonal aggregations.
* Bins continuous temperature data (`T`) into categorical groups:
  * **Cold:** `<10°C`
  * **Mild:** `10-20°C`
  * **Warm:** `20-30°C`
  * **Hot:** `>30°C`

### C. Multi-Column Groupby Operations (> 2 Times)
The script performs three distinct multi-column groupby operations using `['Month', 'Temp_Group']` to analyze interaction effects between weather and pollution:
1. **Mean Aggregation:** Calculates average levels of $\text{CO(GT)}$ and Benzene $[\text{C6H6(GT)}]$ across every combination of Month and Temperature Group.
2. **Extreme Values (Aggregates):** Computes maximum and minimum values for Temperature ($T$) and Relative Humidity ($RH$) per group.
3. **Intra-Group Correlation:** Dynamically calculates the Pearson correlation coefficient between Carbon Monoxide and Benzene *inside* each specific Month/Temperature segment.

### D. Visualizations
* **Correlation Heatmap:** Generates a Seaborn heatmap displaying pairwise Pearson correlations across all numeric sensor parameters.
* **Grouped Bar Plot:** Visualizes average pollutant trends across months, broken down by temperature categories using custom color palettes.




