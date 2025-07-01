# Medical Data Visualizer

## Description

This project analyzes a dataset of medical examination records to identify potential correlations between various health factors and the presence of cardiovascular disease (CVD). The analysis is performed using Python with libraries such as pandas, numpy, matplotlib, and seaborn within a Jupyter Notebook (`medical.ipynb`).

The primary goals are to preprocess the data, engineer relevant features, and generate visualizations (a categorical plot and a heatmap) to better understand patterns and relationships in the data concerning CVD.

## Dataset

The analysis uses the `medical_examination.csv` dataset. This dataset contains information from medical examinations of patients, including:

*   **id:** Unique identifier for each patient.
*   **age:** Age of the patient in days.
*   **sex:** Patient's sex (1 - female, 2 - male).
*   **height:** Height in cm.
*   **weight:** Weight in kg.
*   **ap_hi:** Systolic blood pressure.
*   **ap_lo:** Diastolic blood pressure.
*   **cholesterol:** Cholesterol level (1: normal, 2: above normal, 3: well above normal).
*   **gluc:** Glucose level (1: normal, 2: above normal, 3: well above normal).
*   **smoke:** Smoking status (0: no, 1: yes).
*   **alco:** Alcohol intake (0: no, 1: yes).
*   **active:** Physical activity (0: no, 1: yes).
*   **cardio:** Presence or absence of cardiovascular disease (0: no, 1: yes).

## Analysis Steps

The Jupyter Notebook (`medical.ipynb`) performs the following key steps:

1.  **Data Loading:** Imports the `medical_examination.csv` dataset into a pandas DataFrame.
2.  **Feature Engineering:**
    *   Calculates Body Mass Index (BMI) using the `weight` and `height` columns.
    *   Adds an `overweight` column: `1` if BMI is greater than 25, `0` otherwise.
3.  **Data Normalization:**
    *   Normalizes the `cholesterol` column: `0` if the original value is 1 (normal), `1` if the original value is greater than 1 (above normal / well above normal).
    *   Normalizes the `gluc` (glucose) column: `0` if the original value is 1 (normal), `1` if the original value is greater than 1 (above normal / well above normal).
4.  **Categorical Plot Generation:**
    *   Creates a DataFrame suitable for categorical plotting by melting columns like `cholesterol`, `gluc`, `smoke`, `alco`, `active`, and `overweight` against the `cardio` status.
    *   Generates a bar plot using `seaborn.catplot` to show the counts of these features, grouped by their values and whether cardiovascular disease is present (`cardio` = 0 or 1).
5.  **Heatmap Generation:**
    *   Cleans the data by filtering out improbable or outlier values:
        *   Diastolic blood pressure (`ap_lo`) must be less than or equal to systolic blood pressure (`ap_hi`).
        *   Height and weight are filtered to be within their 2.5th and 97.5th percentiles.
    *   Calculates the Pearson correlation matrix for the cleaned dataset.
    *   Generates a heatmap of this correlation matrix using `seaborn.heatmap`, with annotations and the upper triangle masked for clarity.

## Visualizations

The notebook produces two main visualizations:

1.  **Categorical Plot:**
    *   This plot displays the distribution of key categorical features (cholesterol, glucose, smoking, alcohol, physical activity, overweight) for patients with and without cardiovascular disease. It helps visualize how these factors differ between the two groups.
2.  **Heatmap:**
    *   This plot shows the pairwise correlations between all numerical features in the cleaned dataset. Values range from -1 to 1, indicating the strength and direction of linear relationships. This is useful for identifying which factors are correlated with each other and with the presence of CVD.

## How to Run

To run the analysis:

1.  Ensure you have Python installed.
2.  Install the necessary libraries:
    ```bash
    pip install pandas numpy matplotlib seaborn scipy
    ```
3.  Download or place the `medical_examination.csv` file in the same directory as the `medical.ipynb` notebook, or update the file path in the notebook accordingly.
4.  Open `medical.ipynb` in a Jupyter Notebook environment (e.g., Jupyter Lab, VS Code with Jupyter extension).
5.  Run the cells in the notebook sequentially from top to bottom.

## Dependencies

The project relies on the following Python libraries:

*   **pandas:** For data manipulation and analysis, especially DataFrame operations.
*   **numpy:** For numerical operations, particularly for creating the heatmap mask.
*   **matplotlib:** For basic plotting functionalities (seaborn builds upon it).
*   **seaborn:** For creating enhanced statistical visualizations (categorical plot and heatmap).
*   **scipy:** (Implicitly used for `pearsonr` if `df.corr()` uses it, or generally useful in data analysis contexts, though not directly called in the provided snippet for Pearson correlation, pandas handles it.)

## Output

Running the notebook will:

*   Print the shape of the dataset and the first few rows.
*   Print the distribution (value counts) of the 'overweight', 'cholesterol', and 'gluc' columns after processing.
*   Display the categorical plot.
*   Display the correlation heatmap.
*   Print a final "Analysis complete!" message.
