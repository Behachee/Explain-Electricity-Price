# QRT Challenge - Explain price electricity

### **Predict electricity prices from weather, energy and commercial data from France and Germany**

### Theo Belen-Halimi, Proud Chareesri, Federico Cruz, Charlotte Cupillard

### Introduction

Every day, a multitude of factors impact on the price of electricity. Local weather variations will affect both electricity generation and demand for instance. Long term phenomena, such as global warming, will also have a significant influence. Geopolitical events, such as the war in Ukraine, may affect in parallel the price of commodities, which are key inputs in electricity generation, knowing that each country relies on a particular energy mix (nuclear, solar, hydro, gas, coal, etc). Moreover, each country may import/export electricity with its neighbors through dynamical markets, like in Europe. These various elements make quite complex the modelisation of electricy price in a given country.

The dataset is from a challenge data: https://challengedata.ens.fr/participants/challenges/97/.
The aim is to model the electricity price from weather, energy (commodities) and commercial data for two European countries - France and Germany. We want to create a model that outputs from these explanatory variables a good estimation for the daily price variation of electricity futures contracts, in France and Germany. These contracts allow you to receive (or to deliver) a given amount of electricity at a specified price by the contract delivered at a specified time in the future (at the contract's maturity). Thus, futures contracts are financial instruments that give you some expected value on the future price of electricity under actual market conditions - here, we focus on short-term maturity contracts (24h). 

### Dataset description

**Target variable and features:**

* Features for Germany and France (characterized by DE and FR)
* Target variable: electricity price
* Features: date, country, European gas, European coal, Carbon emissions futures, Temperature, Wind, Rainfall, Total electricity consumption, Imported electricity from Europe, Total daily electricity exchange between France and Germany, etc.
* Float and Integer Types (except for Country which is an object)

**Train set:**
* 1494 rows, 35 columns
* Float and Integer Types (except for Country which is an object)
* 12 Features with Null Values

### EDA

You can find the EDA part in the file "exploration".
The EDA was really important to visualise the outliers, distribution, and correlation between independant variables.


### Feature engineering

**Removing features:**
* Highly correlated features:

**Deal with missing values:**
* Input missing value with KNN imputer

**Clustering:**
* Create 5 clusters for the dataset
* Create 6 clusters for Nuclear Productions

**Adding Features:**
* XX_NON_RENEWABLE = XX_COAL + XX_GAS + XX_LIGNITE + XX_NUCLEAR
* XX_RENEWABLE = XX_HYDRO + XX_SOLAR + XX_WINDPOW
* XX_EXCESS_ENERGY = XX_NON_RENEWABLE + XX_RENEWABLE - XX_CONSUMPTION
* XX_WIND_SQCB = (XX_WIND - XX-WIND.min()) ^ ⅔

**Encoding:**
* Countries (FR and DE)

**Polynomial Features:**
* Creating polynomial feature of degree 3

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
