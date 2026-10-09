# Video Game Commercial Performance Analysis

An exploratory data analysis project investigating the relationship between video game commercial performance, gameplay characteristics, review ratings, and sentiment metrics.

The project brings together information about video games to explore how commercial success relates to player experience and critical reception.

## Research Question

What factors are associated with the commercial performance of video games, and can gameplay characteristics, review ratings, and sentiment metrics provide useful insights into those patterns?

Commercial success is not necessarily explained by a single factor. Sales may vary with platform, genre, release timing, critical reception, player sentiment, and the gameplay experience itself.

This project explores these relationships using structured game records enriched with review and sentiment-related measurements.

## Objectives

- Explore patterns in video game commercial performance.
- Investigate relationships between sales, ratings, and gameplay characteristics.
- Examine how critic and user reception relate to commercial outcomes.
- Explore whether sentiment metrics provide additional insight beyond numerical review scores.
- Identify patterns, limitations, and opportunities for further analysis.

## Dataset

The primary dataset is ""completed_records_plus_sentiment_metrics.csv"" (./data/completed_records_plus_sentiment_metrics.csv).

It contains completed video game records enriched with sentiment-related metrics. The dataset is intended to support analysis across commercial, gameplay, rating, and review dimensions.

The file is reported in a related public dataset repository as containing approximately 3,002 game records and 45 variables. Exact column names, units, missing-value patterns, and source attribution should be confirmed against the version used in this project.

## Main analytical dimensions

- Commercial performance: Sales-related measurements, where available.
- Game characteristics: Genre, platform, and other descriptive attributes.
- Ratings: Numerical measures of critic and user reception.
- Gameplay: Completion, difficulty, and playtime-related measurements, where available.
- Sentiment: Metrics derived from review text or review sentiment classifications.

## Methodology and Program Logic

The analysis follows a data-driven workflow.

### 1. Data preparation

Load the prepared game records, inspect the available variables, and assess data quality before analysis.

### 2. Feature exploration

Examine the commercial, gameplay, rating, and sentiment variables to understand their distributions and identify patterns worth investigating.

### 3. Comparative analysis

Compare commercial outcomes across relevant game characteristics and examine relationships between sales, ratings, gameplay measurements, and sentiment.

### 4. Sentiment analysis

Investigate the available sentiment-related metrics to explore how review tone and reception correspond with commercial performance.

The precise sentiment-generation methods and aggregation rules should be documented according to the notebook implementation.

### 5. Interpretation

Summarize the observed patterns and distinguish descriptive associations from causal explanations. Any numerical conclusions should be supported by the notebook's actual calculations and visualizations.

## Key Findings

The final findings should report the strongest patterns established by the analysis, supported by relevant statistics and charts.

Important questions include:

- Which game categories or platforms show different commercial outcomes?
- How do critic ratings and user ratings relate to sales?
- Do sentiment metrics reveal patterns not captured by numerical ratings alone?
- Which relationships remain meaningful after considering dataset limitations?

Specific conclusions and numerical results should be added after verifying the notebook's outputs.

## Technology Stack

The exact libraries should be confirmed against the notebook. The project dataset supports a workflow involving Python-based data manipulation, statistical analysis, and visualization.

## How to Run

1. Open ""Video_Game_Commercial_Performance_Analysis.ipynb"" (./Video_Game_Commercial_Performance_Analysis.ipynb).
2. Download or clone the repository.
3. Place the dataset in the expected "data/" directory.
4. Update any notebook paths that depend on Google Drive or a particular local environment.
5. Install the required dependencies and run the notebook cells in order.
6. Review the generated tables, visualizations, and statistical results.

## Limitations

- The analysis is limited by the completeness and coverage of the available game records.
- Sentiment metrics depend on the source reviews, the methods used to calculate sentiment, and the coverage of those reviews.
- Associations between ratings, sentiment, and sales do not establish causation.
- Missing data, platform differences, and release-period effects may affect comparisons.
- Conclusions should not be generalized beyond the available data without further validation.

## Future Improvements

- Document every dataset column, its units, and its source.
- Add reproducible dependency and environment instructions.
- Compare critic and user sentiment using consistent measures.
- Evaluate whether sentiment metrics add useful information beyond existing ratings.
- Include clearly labelled visualizations and quantified findings.
- Add robustness checks for missing data and differences between platforms or genres.

## Project Files

- "Analysis notebook" (./Video_Game_Commercial_Performance_Analysis.ipynb)
- "Dataset directory" (./data/)
- "Processed dataset" (./data/completed_records_plus_sentiment_metrics.csv)
- "Main portfolio" (https://github.com/Mehaha-sys/data-ml-portfolio)

---

#### Author: "Mehaha-sys" (https://github.com/Mehaha-sys)
