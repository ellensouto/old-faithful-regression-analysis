# Geyser Eruption Prediction: Linear Regression Analysis of Old Faithful

## 1. Business Problem

Geysers are complex hydrothermal systems. For tourism and geological monitoring, predicting the duration of an eruption based on the preceding waiting time is a valuable task. The goal of this project is to model this relationship using the `faithful` dataset to provide reliable duration estimates and understand the underlying stochastic patterns.

## 2. Context

The analysis utilizes the `faithful` dataset from R, consisting of 272 observations.

* **Target Variable ():** `eruptions` (Duration of eruption in minutes).
* **Predictor Variable ():** `waiting` (Time interval between eruptions in minutes).

## 3. Analysis Assumptions

The validity of the Linear Regression Model (OLSM) was assessed based on:

* **Linearity:** Evaluated via scatter plots.
* **Normality of Residuals:** Tested via Shapiro-Wilk, Lilliefors, and Anderson-Darling tests.
* **Homoscedasticity:** Tested via the Breusch-Pagan test.
* **Independence:** Analyzed via the Durbin-Watson statistic.

## 4. Solution Strategy

The project follows a standard statistical inference workflow:

| Step | Description |
| --- | --- |
| **Exploratory Data Analysis** | Summary statistics and scatter plot visualization revealed two distinct clusters of activity. |
| **Model Estimation** | Fitting the OLS equation . |
| **Diagnostic Testing** | Verifying Gauss-Markov assumptions. Note: A violation of independence was detected. |
| **Inference & Interpretation** | Calculating , Pearson Correlation, and parameter significance (). |
| **Predictive Application** | Generating Point Estimates, Confidence Intervals, and Prediction Intervals for specific  values. |

## 5. Key Insights

* **Strong Correlation:** A Pearson correlation of **0.9008** indicates a very strong positive linear association.
* **Predictive Power:** The model explains **81.15%** of the variance ().
* **Incremental Impact:** For every 13 minutes of additional waiting time, the eruption duration increases by approximately 1 minute.
* **Independence Violation:** The Durbin-Watson test (DW = 2.56, ) suggests negative autocorrelation, implying that time-series dependencies exist that a simple linear model does not fully capture.

## 6. Technical Implementation (R Code)

### Model Fitting and Prediction

```r
# Simple Linear Model
fit <- lm(eruptions ~ waiting, data = faithful)

# Prediction for 80 minutes of waiting
new_data <- data.frame(waiting = 80)
predict(fit, new_data, interval = "prediction")

```

### Residual Diagnostics

```r
# Independence Test
library(car)
durbinWatsonTest(fit)

# Normality Tests
shapiro.test(residuals(fit))

```

## 7. Results Summary

The estimated prediction equation is:


For a wait time of **80 minutes**, the predicted eruption duration is **4.174 minutes**, with a 95% prediction interval of [3.196, 5.156].

## 8. Next Steps

* **Cluster Analysis:** Since the data shows two distinct groups (short/short vs long/long), a Mixture Model or K-means clustering could refine the predictions.
* **Time-Series Modeling:** Given the independence violation, an **ARIMA** or **Time-Series Regression** model should be explored to account for temporal dependencies between consecutive eruptions.
