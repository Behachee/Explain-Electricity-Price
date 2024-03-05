# QRT Challenge - Explain price electricity

### **Predict electricity prices from weather, energy and commercial data from France and Germany**

### Theo Belen-Halimi, Proud Chareesri, Federico Cruz, Charlotte Cupillard

### Introduction

Every day, a multitude of factors impact on the price of electricity. Local weather variations will affect both electricity generation and demand for instance. Long term phenomena, such as global warming, will also have a significant influence. Geopolitical events, such as the war in Ukraine, may affect in parallel the price of commodities, which are key inputs in electricity generation, knowing that each country relies on a particular energy mix (nuclear, solar, hydro, gas, coal, etc). Moreover, each country may import/export electricity with its neighbors through dynamical markets, like in Europe. These various elements make quite complex the modelisation of electricy price in a given country.

The dataset is from a challenge data: https://challengedata.ens.fr/participants/challenges/97/.
The aim is to model the electricity price from weather, energy (commodities) and commercial data for two European countries - France and Germany. We want to create a model that outputs from these explanatory variables a good estimation for the daily price variation of electricity futures contracts, in France and Germany. These contracts allow you to receive (or to deliver) a given amount of electricity at a specified price by the contract delivered at a specified time in the future (at the contract's maturity). Thus, futures contracts are financial instruments that give you some expected value on the future price of electricity under actual market conditions - here, we focus on short-term maturity contracts (24h). 

## Overview
This repository contains a series of Jupyter notebooks developed for a challenge aiming to model the electricity price variations in France and Germany based on weather, energy, and commercial data. The challenge emphasizes understanding the multifaceted influences on electricity prices, such as weather changes, geopolitical events, and energy market dynamics, to estimate daily price variations for electricity futures contracts.

## Challenge Description
Electricity prices are influenced by a myriad of factors including local weather variations, long-term phenomena like global warming, geopolitical events, and the dynamic nature of electricity future exchanges in Europe. This challenge focuses on modeling the electricity price from various explanatory variables for France and Germany, aiming not for prediction but for a precise estimation of daily price variations of short-term maturity electricity futures contracts based on current market conditions.

## Goals
The primary goal is to learn a model that can output a good estimation of the daily price variation of electricity futures contracts in France and Germany from explanatory variables including weather conditions, commodity price changes, and electricity usage metrics.

## Data Description
The dataset comprises daily data for France and Germany, including:
- Weather quantitative measurements (temperature, rain, wind)
- Energetic production (commodity price changes)
- Electricity use (consumption, exchanges between countries, import-export with Europe)

The provided data sets are split into training inputs (`X_train`), training outputs (`Y_train`), and test inputs (`X_test`), with `ID`, `DAY_ID`, and `COUNTRY` as key identifiers.

**Target variable and features:**

* Features for Germany and France (characterized by DE and FR)
* Target variable: electricity price
* Features: date, country, European gas, European coal, Carbon emissions futures, Temperature, Wind, Rainfall, Total electricity consumption, Imported electricity from Europe, Total daily electricity exchange between France and Germany, etc.
* Float and Integer Types (except for Country which is an object)

**Train set:**
* 1494 rows, 35 columns
* Float and Integer Types (except for Country which is an object)
* 12 Features with Null Values

## Notebooks Overview
1. **EDA.ipynb**: Initial exploration of the provided data sets, including statistical summaries and visualizations to understand the distributions of various features and the target variable.
2. **data_cleaning.ipynb**: Steps taken to clean the data, including handling missing values, outlier identification and treatment, and normalization of variables.
3. **DecisionTree.ipynb**: Implementation of a decision tree model to estimate daily electricity price variations.
4. **BaggingRegressor.ipynb**: Application of a bagging regressor model to improve predictions by combining the outputs of multiple decision trees.
5. **XGBRegressor.ipynb**: Use of XGBoost, an advanced gradient boosting model, for high-accuracy estimation of electricity price variations.

## Data Exploration
### Key Steps and Insights
- **Statistical Analysis**: Descriptive statistics to summarize the central tendency, dispersion, and shape of the dataset's distributions.
- **Correlation Analysis**: Identification of relationships between different variables and their impact on electricity prices.
- **Visual Exploration**: Use of histograms, scatter plots, and box plots to visualize data distributions and identify outliers.

## Data Cleaning
### Key Steps and Points
- **Handling Missing Values**: Strategies such as imputation or removal of rows/columns with missing data, depending on their impact on the dataset.
- **Outlier Detection and Treatment**: Identification of outliers using statistical methods or visual inspection and their treatment to prevent skewed analysis.
- **Normalization and Scaling**: Application of normalization or standardization techniques to ensure that numerical input variables have the same scale.
- **Feature Engineering**: Creation of new features that might improve the model's performance by capturing additional information from the data.
- **Encoding Categorical Variables**: Transformation of categorical variables into numerical representations to enable their use in the model.

## Evaluation
The models are evaluated based on Spearman's correlation between the model output and the actual daily price changes over the test dataset, aiming for a model that can closely estimate real-world electricity price variations.

### Models
<img width="1240" alt="Screenshot 2024-03-04 at 22 47 18" src="https://github.com/Behachee/Explain-Electricity-Price/assets/115945494/742fbeb7-9ad8-4983-8986-0e3a0e3e04c6">


### Can you explain the price of electricity?

Variable importance based on permutation 

* Why?
  * Impurity decrease has a tendency to inflate the importance of continuous features
  * We removed correlated predictors

* How?
  * Measure the prediction strength of each variable
  * Permute at random the j-th variable values of these data and pass this modified dataset to the RF again to obtain predictions
  * Compute the OOB-error on this modified dataset
  * The $V_i$ of $X_j$ is the difference between the benchmark score E and the one from the modified (permuted) dataset
  * The more the increase of OOB error is, the more important is the variable

* Variable importance
  * Electricity consumption after using all renewable energies in Germany
  * Wind power in Germany
  * Natural gas in France

## How to Use
1. Clone the repository to your local machine.
2. Ensure you have Jupyter Notebook or JupyterLab installed to run the notebooks.
3. Install necessary Python packages as listed in the `requirements.txt` file.
4. Open and run the notebooks in order, starting from `EDA.ipynb` to understand the data, followed by `data_cleaning.ipynb` for preprocessing, and finally the model notebooks.


