# Exoplanet Candidate Classification

A machine learning project exploring whether confirmed exoplanets can be distinguished from false-positive detections using a minimal set of measurements from NASA's Kepler Objects of Interest (KOI) dataset.

The project investigates how individual astronomical measurements contribute to classification and establishes a baseline model that can be used to explore simpler, more interpretable feature sets.

## Research Question

Can a machine learning model distinguish confirmed exoplanets from false-positive detections using the smallest practical number of measurements from NASA's KOI table? If so, which measurements provide the most useful discriminatory information?

The Kepler mission identified many objects of interest from transit signals observed around stars. However, not every detected signal corresponds to a confirmed planet. Some are classified as false positives because other astrophysical phenomena or observational effects can produce similar signals.

This project explores whether a limited set of measured planetary, stellar, and transit-related properties can help distinguish confirmed objects from false positives.

Rather than treating every available column as equally useful, the analysis examines the predictive value of individual measurements and builds a baseline classification model.

## Why This Problem Matters

Astronomical catalogues can contain hundreds of columns describing an object, its host star, and its observed transit signal. Using every available feature can increase model complexity and make the reasoning behind predictions harder to communicate.

Identifying a smaller, informative set of measurements could help:

- Simplify machine learning models.
- Improve interpretability by highlighting useful physical measurements.
- Reduce dependence on unnecessary or redundant variables.
- Make future classification workflows easier to maintain.
- Investigate the trade-off between model simplicity and predictive performance.

The objective is not simply to maximize accuracy. It is to understand how much useful classification information can be retained while reducing the number of input measurements.

## Dataset

The project uses "kepler_koi_dr25.csv", a CSV dataset based on the Kepler Objects of Interest catalogue.

Dataset file: ""data/kepler_koi_dr25.csv"" (./data/kepler_koi_dr25.csv)

The notebook initially loads a dataset containing 8,054 rows and 141 columns. It then restricts the classification task to confirmed objects and false positives, excluding objects labelled as candidates.

Dataset stage| Observations
Original dataset| 8,054
Confirmed objects| 2,731
False positives| 3,965
Binary classification dataset| 6,696
Candidate objects excluded| 1,358
Measurements retained for baseline model| 23

The dataset contains a mixture of object identifiers, classification labels, transit measurements, signal characteristics, and host-star properties.

## Main measurement categories

Category| Examples| Purpose
Transit characteristics| "koi_period", "koi_duration", "koi_depth"| Describe the observed transit signal
Orbital and geometric properties| "koi_impact", "koi_incl", "koi_dor"| Describe aspects of the transit geometry and orbit
Signal strength| "koi_model_snr", "koi_num_transits"| Describe signal quality and repeated observations
Stellar properties| "koi_steff", "koi_slogg", "koi_srad", "koi_smass"| Describe the host star
Derived planetary properties| "koi_prad", "koi_teq", "koi_insol"| Describe estimated planet size and environmental properties

The notebook starts with 26 candidate measurements and removes three that are completely missing or have no usable variation in the filtered dataset, leaving 23 features for the baseline model.

For exact column definitions, units, and provenance, refer to the source catalogue documentation and the project's data dictionary.

## Methodology and Program Logic

The notebook follows a sequence of data preparation, feature investigation, and supervised classification.

### 1. Preserve the source dataset

The original CSV is treated as read-only. A separate working copy is created for analysis so that preprocessing does not overwrite the source file.

### 2. Inspect the dataset

The notebook examines the dataset's dimensions, column data types, missing-value counts, missing-value percentages, and number of unique values.

It also inspects the available disposition labels to understand the classification problem before building the model.

### 3. Define the classification target

The original catalogue contains three dispositions:

- "CONFIRMED"
- "FALSE POSITIVE"
- "CANDIDATE"

For this experiment, the notebook retains only confirmed objects and false positives.

The target is encoded as a binary variable:

- "1" — Confirmed
- "0" — False positive

Candidate objects are excluded because the experiment focuses on distinguishing the two specified classes rather than performing three-class classification.

### 4. Select candidate measurements

The notebook defines 26 candidate features drawn from transit, signal, stellar, and derived planetary measurements.

It then removes measurements that are entirely missing or have no usable variation in the filtered dataset, resulting in 23 retained features.

This initial filtering removes unusable variables. It does not, by itself, establish which subset of features is sufficient for strong predictive performance.

### 5. Evaluate individual measurements

Each retained measurement is evaluated individually using the area under the receiver operating characteristic curve (ROC-AUC).

This provides an initial way to compare how well a single measurement separates confirmed objects from false positives.

The analysis also records the percentage of missing values for each feature.

Individual-feature ROC-AUC is a useful screening method, but it does not account for all interactions between measurements. A feature that is only moderately predictive on its own may still contribute useful information when combined with other features.

### 6. Train the baseline classifier

The notebook trains a logistic regression model using a scikit-learn pipeline containing:

1. Median imputation for missing feature values.
2. Standardization using "StandardScaler".
3. Logistic regression for binary classification.

The data is divided into training and test sets using an 80:20 split, with stratification to preserve the class proportions. The split uses a fixed random seed for reproducibility.

The resulting dataset contains 5,356 training observations and 1,340 test observations.

### 7. Evaluate model performance

The model is evaluated using:

- Accuracy: Overall proportion of correct predictions.
- Precision: Proportion of predicted confirmed objects that are actually confirmed.
- Recall: Proportion of confirmed objects correctly identified.
- F1-score: Balance between precision and recall.
- ROC-AUC: Ability to rank confirmed objects above false positives across classification thresholds.
- Confusion matrix: Breakdown of correct and incorrect classifications.

The notebook also examines the fitted logistic regression coefficients to identify which features have the largest absolute coefficients in the standardized model.

Coefficient magnitude can help interpret the fitted model, but it should not be treated as a definitive feature-selection method or proof of physical causation.

## Results

The saved notebook output reports the following baseline performance on the held-out test set:

Metric| Result
Accuracy| 87.9%
Precision| 82.7%
Recall| 89.0%
F1-score| 85.7%
ROC-AUC| 94.4%

Interpreting the results

The baseline model correctly classifies a substantial proportion of the held-out observations. Its recall of 89.0% indicates that it identifies most of the confirmed objects in the test set, while its precision of 82.7% indicates that some objects predicted as confirmed are actually false positives.

The ROC-AUC of 0.944 indicates strong separation between the two classes in terms of the model's predicted scores on this test set.

These results establish a useful baseline for investigating whether a smaller number of measurements can achieve comparable performance.

Confusion matrix

The saved confusion matrix is:

Actual class| Predicted false positive| Predicted confirmed
False positive| 691| 102
Confirmed| 60| 487

This shows that the model correctly identifies 691 false positives and 487 confirmed objects. It misclassifies 102 false positives as confirmed and 60 confirmed objects as false positives.

These errors matter because the consequences of incorrectly accepting a false positive may differ from those of failing to identify a confirmed object.

## Current Findings and the Minimal-Feature Goal

The current notebook establishes three useful starting points:

1. A binary classification dataset containing 6,696 confirmed and false-positive observations.
2. A screening procedure that ranks individual measurements using ROC-AUC.
3. A logistic regression baseline using 23 measurements, with a reported test ROC-AUC of 0.944.

The central research question remains open: what is the smallest set of measurements that maintains acceptable predictive performance?

Answering that question requires comparing models trained on progressively smaller feature subsets and evaluating their performance on data not used to select those features.

A suitable next step would be to test feature-selection strategies, compare performance at different feature counts, and identify a compact subset that balances model simplicity, precision, recall, and ROC-AUC.

The goal should be to find a practical balance between predictive quality and the number of measurements required, rather than assuming that fewer features are automatically better.

## Technology Stack

- Python
- Pandas
- NumPy
- scikit-learn
- Jupyter Notebook
- Google Colab

## How to Run the Project

The notebook currently uses Google Colab and Google Drive paths.

1. Open ""Exoplanet_Candidate_Classification.ipynb"" (./Exoplanet_Candidate_Classification.ipynb) in Google Colab.
2. Mount Google Drive when prompted.
3. Place "kepler_koi_dr25.csv" in the configured project directory.
4. Check the notebook's file paths and update them if necessary.
5. Run the notebook cells in order.
6. Review the feature-ranking table, model evaluation metrics, and confusion matrix.

## Dependencies
- Pandas
- NumPy
- scikit-learn

## Limitations

- The experiment considers confirmed objects and false positives, excluding the candidate class.
- The current baseline uses 23 measurements and does not yet demonstrate the smallest sufficient feature subset.
- Single-feature ROC-AUC scores do not capture all interactions between features.
- Performance estimates depend on the selected dataset, preprocessing choices, and train-test split.
- High predictive performance does not establish that a measurement causes a particular classification.
- Catalogue fields that encode prior disposition decisions or the results of the vetting process must be excluded from predictive features to prevent target leakage.
- The model's predictions should not be interpreted as independent astronomical confirmation of an exoplanet.

## Future Improvements

- Implement systematic feature selection and compare progressively smaller feature subsets.
- Evaluate performance using cross-validation and a held-out test set that remains untouched during feature selection.
- Compare logistic regression with other suitable classifiers.
- Examine feature correlations and redundancy.
- Investigate precision-recall trade-offs and the consequences of different classification thresholds.
- Document the complete data dictionary, units, missing-value conventions, and dataset provenance.
- Make the data paths configurable so the notebook can run outside Google Colab.

## Project Files

- "Analysis notebook" (./Exoplanet_Candidate_Classification.ipynb)
- "Dataset directory" (./data/)
- "KOI dataset" (./data/kepler_koi_dr25.csv)
- "Main portfolio" (https://github.com/Mehaha-sys/data-ml-portfolio)

## Data Source

The dataset is based on the Kepler Objects of Interest catalogue. Consult the "NASA Exoplanet Archive KOI table documentation" (https://exoplanetarchive.ipac.caltech.edu/docs/API_kepcandidate_columns.html) for official column descriptions and definitions.

---

#### Author: "Mehaha-sys" (https://github.com/Mehaha-sys)

This project explores interpretable binary classification of astronomical catalogue data, with an emphasis on understanding feature usefulness and reducing model complexity.
