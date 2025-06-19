# Atmospheric CO₂ Shift Detection and Future Forecasting

This repository contains the code and resources for a predictive modeling study focused on detecting regime shifts and forecasting future levels of atmospheric carbon dioxide (CO₂).

## Project Overview

Atmospheric CO₂ is a critical driver of global climate change. Understanding its historical trends, identifying significant shifts in its behavior, and accurately forecasting future levels are crucial for scientists, policymakers, and the public to anticipate future risks and guide climate action. This project aims to:

* **Analyze atmospheric CO₂ data** to detect major trend changes, known as "regime shifts."
* **Forecast future CO₂ levels** for the next five years.

This study leverages various time series and machine learning models to achieve these objectives, providing insights into the accelerating rise of CO₂ levels.

## Data

The dataset used in this study is the `co2_mm_mlo.csv` file, which contains monthly mean atmospheric CO₂ in parts per million (ppm) from the Global Monitoring Laboratory (GML) of the National Oceanic and Atmospheric Administration (NOAA).

**Dataset Details:**

* **Source:** Global Monitoring Laboratory (GML) of NOAA
* **Period:** March 1958 – Present (April)
* **Dimensions:** 806 rows × 8 columns (as of the last update)
* **Columns:**
    * `year`: Year of observation.
    * `month`: Month of observation.
    * `decimal date`: Decimal representation of the date.
    * `average` (renamed to `co2`): Monthly mean CO₂ in ppm.
    * `deseasonalized`: Deseasonalized CO₂ values.
    * `ndays`: Number of days measured in the month.
    * `sdev`: Standard deviation of daily values in the month.
    * `unc`: Uncertainty of the monthly mean.

### Data Preprocessing

The `project.ipynb` notebook includes the following data cleaning and preparation steps:

1.  **Renaming Columns:** The 'average' column is renamed to 'co2' and 'decimal date' to 'decimal_date' for easier access.
2.  **Date Indexing:** A 'date' column is created from 'year' and 'month', and the DataFrame is indexed by this 'date' column.
3.  **Handling Missing Values:** Missing values (represented as -99.99) in the 'co2' column are replaced with `pd.NA` and then interpolated using a time-based method. Any remaining `NA` values are dropped.

## Methodology

The project follows a comprehensive workflow involving data acquisition, preprocessing, change-point detection, and predictive modeling.

### Change-Point Detection

The study utilizes the **PELT (Pruned Exact Linear Time)** algorithm for change-point detection. This algorithm is applied to identify significant shifts or anomalies in the CO₂ time series, which can signal critical climate or policy events.


Method: PELT (Pruned Exact Linear Time) for change-point detection on trend and residuals. fast and scalable, making it suitable for long time series like CO₂ data.
It automatically splits the time series into segments that are as homogeneous as possible.
A penalty parameter controls sensitivity
Significance: Regime shifts often align with major climate events, economic changes, or policy milestones

![image](https://github.com/user-attachments/assets/5b51cea9-daef-4c0a-bc08-34931bd163e8)

### Major changes by setting up threshold ( Major and Low)

<img width="742" alt="image" src="https://github.com/user-attachments/assets/89d20b85-b619-4c13-b816-11c6decb132d" />


### Event Based Validation


<img width="688" alt="image" src="https://github.com/user-attachments/assets/c438a76b-f068-4943-a518-fdfa025c6c91" />



### Predictive Modeling

A variety of models, including classical time series models and machine learning models, were employed for forecasting:

**Classical Time Series Models:**

* **Holt-Winters Exponential Smoothing:** Used for its ability to capture trend and seasonality.
* **SARIMA (Seasonal AutoRegressive Integrated Moving Average):** A powerful model for seasonal time series data.
* **ARIMA (AutoRegressive Integrated Moving Average):** Applied to capture trends.

**Machine Learning Models:**

* **LSTM (Long Short-Term Memory) Neural Networks:** A type of recurrent neural network well-suited for sequence prediction.
* **ANN (Artificial Neural Networks):** General-purpose neural networks for pattern recognition.
* **Random Forest Regressor:** An ensemble learning method for regression tasks.

### Evaluation Metrics

The performance of the predictive models was evaluated using:

* **MAE (Mean Absolute Error):** Measures the average magnitude of the errors.
* **RMSE (Root Mean Squared Error):** Measures the square root of the average of the squared errors.

## Results


The evaluation of the models yielded the following key findings:

* **Holt-Winters, SARIMA, LSTM, and ANN** generally provided the best forecast accuracy.
* **Random Forest** tended to overfit the training data and performed poorly on test forecasts.
* **ARIMA** successfully captured the trend in the data but struggled to account for seasonality, leading to less accurate forecasts.
* **Holt-Winters and ANN** demonstrated good generalization capabilities to unseen data.

## Limitations

The study acknowledges the following limitations:

* **Algorithm Scope:** Only the PELT algorithm was used for change-point detection. Exploring other algorithms could provide additional insights.
* **Data Length for Seasonal Models:** Some detected regimes were too short (e.g., only 1 month as noted in `project.ipynb` output: "Not enough data in latest regime for seasonal HW: only 1 months."), which limited the applicability of seasonal models like Holt-Winters for those segments.
* **Hyperparameter Tuning:** Hyperparameters were not exhaustively tuned, which might have impacted model performance.

## How to Run the Project

To replicate the analysis and forecasting, follow these steps:

1.  **Clone the repository:**
    ```bash
    git clone [https://github.com/mahfuzur-mafu/atmosphericCO2-shiftdetection-forecast.git](https://github.com/mahfuzur-mafu/atmosphericCO2-shiftdetection-forecast.git)
    cd atmosphericCO2-shiftdetection-forecast
    ```

2.  **Install dependencies:**
    Ensure you have Python installed. Then, install the required libraries using pip:
    ```bash
    pip install pandas numpy matplotlib statsmodels scikit-learn tensorflow
    ```
    *(Note: `tensorflow` might require specific setup depending on your system. Refer to TensorFlow's official documentation for detailed installation instructions.)*

3.  **Download the dataset:**
    Place the `co2_mm_mlo.csv` file in the root directory of the cloned repository.

4.  **Run the Jupyter Notebook:**
    Open the `project.ipynb` notebook using Jupyter Notebook or JupyterLab:
    ```bash
    jupyter notebook project.ipynb
    ```
    Execute the cells sequentially to perform data loading, preprocessing, model training, and forecasting.

## Future Work

* Explore additional change-point detection algorithms.
* Implement more rigorous hyperparameter tuning for all models.
* Investigate the impact of external factors (e.g., volcanic eruptions, major policy changes) on CO₂ trends and regime shifts.
* Develop a more robust method for handling short regimes in seasonal modeling.

---



