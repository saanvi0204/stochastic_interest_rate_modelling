# 📈📉 Stochastic Interest Rate Modelling and Prediction

> This project implements and analyses the Cox–Ingersoll–Ross (CIR) stochastic interest rate model for yield curve modelling and prediction.

## Overview

The goal is to calibrate CIR model parameters using Treasury yield data, reconstruct the term structure of interest rates, evaluate predictive performance across multiple maturities, and investigate extensions beyond the classical single-factor specification.

Key objectives include:

* Understanding the dynamics of short-rate models
* Estimating CIR parameters from market data
* Reconstructing yield curves using calibrated models
* Evaluating predictive performance
* Extending the model to a multi-factor setting
* Analysing practical limitations of affine term structure models

---

## Mathematical Background

The CIR model describes the evolution of the instantaneous short rate as:

$$
dr_t = \kappa(\theta-r_t)dt + \sigma\sqrt{r_t},dW_t
$$

where:

* $\kappa$ = mean reversion speed
* $\theta$ = long-run mean level
* $\sigma$ = volatility parameter
* $W_t$ = standard Brownian motion

A key advantage of the CIR model is that it preserves non-negative interest rates under the Feller condition:

$$
2\kappa\theta \ge \sigma^2
$$

---

## Dataset

The repository includes all datasets required to reproduce the results.

### Training Data

**train_data.csv**

Used for:

* Parameter estimation
* Model calibration
* Yield curve fitting

### Test Data

**test_data.csv**

Used for:

* Out-of-sample evaluation
* Yield reconstruction
* Performance assessment

### Short-Rate Test Data

**test_data_3M.csv**

Contains the 3-month Treasury yield used as a proxy for the instantaneous short rate during out-of-sample prediction.

---

## Methodology

### 1. Data Preparation

* Treasury yield data loaded and cleaned
* Missing values handled
* Yield curves organised by maturity

### 2. Exploratory Data Analysis

* Yield behaviour across maturities analysed
* Correlation structure examined
* Yield curve dynamics visualised

### 3. CIR Process Simulation

* Simulated short-rate paths generated
* Mean-reverting behaviour verified
* Positivity of rates maintained

### 4. Exact MLE Calibration

Parameters estimated using Exact Maximum Likelihood Estimation:

* Mean reversion speed ((\kappa))
* Long-run mean ((\theta))
* Volatility ((\sigma))

### 5. Yield Curve Calibration

The CIR bond pricing framework was used to map short rates into market-observed yields.

### 6. Hybrid Calibration

A hybrid approach combining statistical estimation and yield-curve fitting was implemented to improve practical performance.

### 7. Yield Reconstruction & Prediction

Model-generated yields were compared against observed market yields across:

* 6M maturity
* 9M maturity
* 1Y maturity
* 2Y maturity

### 8. Two-Factor CIR Extension

A Longstaff–Schwartz style two-factor CIR framework was implemented to capture additional sources of yield-curve variation.

### 9. Model Evaluation

Performance assessed using:

* R² Score
* Mean Squared Error (MSE)
* Root Mean Squared Error (RMSE)
* Visual yield curve comparisons

---

## Key Findings

### Single-Factor CIR Model

* Successfully captures the mean-reverting nature of interest rates.
* Produces strong yield reconstructions for short and intermediate maturities.
* Demonstrates reasonable out-of-sample predictive capability.
* Performance deteriorates for longer maturities due to limited model flexibility.

### Two-Factor CIR Model

* Captures additional yield curve dynamics.
* Improves representation of complex term-structure movements.
* Provides a richer framework than the single-factor specification.

---

## Limitations

The classical CIR model has several practical limitations:

* Assumes a single source of interest rate risk.
* Limited flexibility for complex yield curve movements.
* Difficulty fitting long-end maturities accurately.
* Parameters assumed constant through time.
* Ignores macroeconomic and regime-dependent effects.

---

## Repository Structure

```text
.
├── data/
│   ├── train_data.csv
│   ├── test_data.csv
│   └── test_data_3M.csv
│
├── cir_model.ipynb
├── requirements.txt
└── README.md
```

---

## Installation

Clone the repository:

```bash
git clone https://github.com/saanvi0204/stochastic_interest_rate_modelling.git
cd stochastic_interest_rate_modelling
```

Install dependencies:

```bash
pip install -r requirements.txt
```

---

## Running the Project

Open the notebook:

```bash
jupyter notebook cir_model.ipynb
```

or upload the notebook to Google Colab and run all cells sequentially.

All required datasets are already included in the repository.

---


## Results

The notebook contains:

* Calibration outputs
* Simulated CIR paths
* Yield curve reconstructions
* Prediction performance metrics
* Two-factor model calibration
* Comparative analysis and critical discussion

All figures, outputs, and interpretations are included within the notebook.

---

## Environment

The notebook was developed and tested in Google Colab using Python 3.11.

---

## References

1. Cox, J. C., Ingersoll, J. E., & Ross, S. A. (1985). *A Theory of the Term Structure of Interest Rates*. Econometrica.

2. Longstaff, F. A., & Schwartz, E. S. (1992). *Interest Rate Volatility and the Term Structure: A Two-Factor General Equilibrium Model*.

3. Hull, J. C. *Options, Futures, and Other Derivatives*.

4. Brigo, D., & Mercurio, F. *Interest Rate Models: Theory and Practice*.
