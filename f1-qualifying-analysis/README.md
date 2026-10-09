# Formula 1 Qualifying Performance Analysis

A Python-based data engineering and analysis project that builds a modular pipeline for processing, validating, and comparing Formula 1 qualifying-session data across multiple Grand Prix events.

The project focuses on transforming raw lap-level CSV data into a consistent analytical structure, validating data quality, and preparing reliable performance metrics for driver and stint comparisons.

## Problem Statement

How can Formula 1 qualifying data be transformed into a reliable, standardized dataset for comparing driver performance across different Grand Prix events?

Raw racing data can contain missing lap times, pit-stop laps, interrupted sessions, inconsistent sector-time records, and incomplete stint information. If these issues are not handled carefully, performance comparisons can become misleading.

This project addresses these challenges through a structured data pipeline that preserves source files, standardizes lap-level observations, performs quality checks, and calculates performance metrics using defined eligibility rules.

## Project Objectives

- Build a repeatable pipeline for processing multiple qualifying-session datasets.
- Preserve source data and detect unintended file modifications.
- Normalize driver-specific lap data into a consistent analytical format.
- Validate lap times, sector records, lap boundaries, and stint information.
- Identify observations suitable for performance calculations.
- Generate driver- and stint-level performance metrics.
- Establish a foundation for comparing qualifying performance across sessions.

## Dataset Overview

The pipeline processes eight CSV files representing qualifying sessions from the following Grand Prix events:

- Bahrain Grand Prix
- Belgian Grand Prix
- Dutch Grand Prix
- Emilia Romagna Grand Prix
- Hungarian Grand Prix
- Italian Grand Prix
- Singapore Grand Prix
- Spanish Grand Prix

The source filenames attribute the datasets to TracingInsights.com. The notebook processes four driver records per session.

## Key data fields

The source data use driver-specific column names, where the driver identifier appears as a prefix.

Field| Description
"LAP"| Lap number
"*_TIME"| Recorded lap time for a driver
"*_POSITION"| Recorded driver position
"*_POSITION_CHANGE"| Recorded position change
"*_COMPOUND"| Tyre compound
"*_STINT"| Stint identifier
"*_PITSTOP"| Pit-stop indicator
"*_TIRE_LIFE"| Recorded tyre-life value
"*_S1", "*_S2", "*_S3"| Sector-time fields
"*_SECTOR_SUM"| Combined sector-time field
"*_STATUS"| Recorded lap or track status
"*_PERSONAL_BEST"| Personal-best indicator

For example, "VER_TIME" represents the lap-time field associated with the driver identifier "VER", while "VER_S1" represents the corresponding first-sector field.

Exact units, source definitions, and missing-value conventions should be confirmed against the original CSV files.

## Methodology and Program Logic

The notebook implements a staged workflow that separates data ingestion, integrity protection, normalization, validation, and performance analysis.

### 1. Data ingestion

The pipeline loads the qualifying CSV files and inspects their structure, including row counts, available columns, and driver-specific fields.

Driver columns are detected programmatically using the "_TIME" suffix, reducing the need to hardcode driver identifiers for every dataset.

### 2. Data integrity and source protection

The pipeline creates a protected working copy of the source datasets and records metadata such as file sizes and SHA-256 hashes.

The resulting manifest allows subsequent runs to check whether the expected files have changed. This supports reproducibility and helps identify unintended modifications to the input data.

### 3. Data normalization

The pipeline standardizes lap identifiers and converts the driver-oriented source data into a long-format analytical structure.

This organization makes it easier to group observations by driver, lap, and stint, and to apply consistent validation and calculation rules.

Rows without valid numeric lap identifiers are excluded from the normalized analytical dataset.

### 4. Data-quality auditing

The audit stage checks several aspects of data consistency:

- Sector-time availability and consistency with recorded sector totals.
- Lap boundaries and stint transitions.
- Missing lap-time observations.
- Stint completeness and the presence of recorded performance laps.

Potential issues are recorded as diagnostic information rather than automatically deleting every observation that triggers a warning.

### 5. Performance eligibility and validation

Before performance metrics are calculated, the pipeline applies eligibility rules to distinguish usable observations from laps that may distort comparisons.

The implemented rules identify missing lap times, laps with non-clear track status, and pit-stop laps. Sector anomalies are also tracked separately so their impact can be assessed without automatically excluding every affected lap.

Keeping data-quality diagnostics separate from performance eligibility makes the workflow easier to inspect and maintain.

### 6. Performance metrics

The pipeline calculates metrics at the stint and session levels, including:

- Fastest eligible lap times.
- Valid-lap counts.
- Lap-time variability.
- Lap-time trends.
- Driver comparison summaries.

The notebook also uses statistical methods, including linear regression, to examine patterns in lap times.

These measures describe observed performance in the available data; they do not independently establish why a driver was faster or slower.

### 7. Qualifying comparison

The final stage produces driver-level comparison summaries and qualifying-position assignments for the processed sessions.

This provides a consistent basis for examining the recorded qualifying results across the selected events.

## Key Outcomes

The notebook's saved execution outputs show that the implemented pipeline checkpoints completed successfully for the eight input sessions.

Validation stage| Reported result
Sessions processed| 8
Normalization checkpoints passed| 8/8
Data-audit checkpoints passed| 8/8
Performance-metrics checkpoints passed| 8/8
Qualifying-comparison checkpoints passed| 8/8

These results indicate that the saved pipeline execution completed its implemented checks across the selected datasets.

Important distinction: successful pipeline validation is not the same as a sporting finding. Claims about the fastest driver, the effect of tyre compounds, or the relationship between track conditions and lap times should be supported by the corresponding computed metrics and visualizations.

## Technology Stack

- Python — Pipeline implementation and analysis.
- Pandas — Tabular data processing and transformation.
- NumPy — Numerical operations.
- SciPy — Statistical and scientific computing.
- Jupyter Notebook / Google Colab — Interactive development and execution.
- Python standard library — File management, hashing, and JSON-based metadata.

## How to Run the Project

The current notebook uses Google Colab and Google Drive paths (Use CSV file downloaded from TracingInsights)

1. Open ""Qualifying_Race_Pipeline.ipynb"" (./Qualifying_Race_Pipeline.ipynb) in Google Colab.
2. Mount Google Drive when prompted.
3. Place the eight source CSV files in the configured data directory.
4. Check that the notebook's input and output paths match your directory structure.
5. Run the notebook cells in order.
6. Review the validation reports and performance summaries before interpreting the results.

## Dependencies

The notebook uses Python packages including:

- "pandas"
- "numpy"
- "scipy"

Google Colab's Drive integration is also required for the current path configuration.

A dependency file and configurable local paths would make the project easier to reproduce outside Google Colab.

## Limitations

- The current analysis covers eight selected qualifying sessions rather than the full Formula 1 calendar.
- Each source file contains four driver records, which limits the scope of driver comparisons.
- Results depend on the completeness and correctness of the supplied source data.
- Validation checks can identify defined data-quality problems but cannot guarantee that every source-data issue has been detected.
- Lap-time trends and comparisons are descriptive and do not independently establish causal relationships.
- The current workflow relies on Google Drive paths and requires configuration changes for local execution.

## Future Improvements

- Add a "requirements.txt" file and configurable input paths.
- Document dataset provenance, retrieval dates, units, and usage permissions.
- Export validated datasets and performance summaries for independent review.
- Add automated tests for normalization and validation logic.
- Include visualizations of lap-time distributions, sector performance, and driver comparisons.
- Expand the analysis to additional qualifying sessions and drivers.
- Add a data dictionary describing the exact columns, data types, and missing-value conventions.

## Repository

- "Project directory" (./)
- "Analysis notebook" (./Qualifying_Race_Pipeline.ipynb)
- "Main portfolio" (https://github.com/Mehaha-sys/data-ml-portfolio)

---

Author: "Mehaha-sys" (https://github.com/Mehaha-sys)

This project demonstrates a structured approach to data integrity, data validation, and performance analysis using Formula 1 qualifying data.
