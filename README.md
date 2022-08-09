# Regression_Zillow_project


### Project Planning

Fri - Acquire, Prepare, Explore
Mon - Modeling, Test, Conclusion, Readme
Tue - Present



### Data Dictionary

#### Data Columns:
'bed' = bedroom
'bath' = bathroom
'sqft' = square footage of house
'tax_value' = home value
'yearbuilt'= year house was built
'fips' = county fips
'6037.0' = a fips number
'6059.0' =  a fips number
'6111.0' = a fips number

#### Model Columns:
LinReg_tr        Linear Regression for Train set
Poly_val         Polynomial Regression for Validate set
Poly_tr          Polynomial Regression for Train set
LassoLars_val    Lasso Lars for Validate set
LinReg_val       Linear Regression for Validate set
LassoLars_tr     Lasso Lars for Train set
GLM_val          Tweedie Regression for Validate set
GLM_tr           Tweedie Regression for Test set
Baseline_val     Baseline (mean) for Validate set
Baseline_tr      Baseline (mean) for Train set

### Steps to reproduce

You will need an env.py file that contains the hostname, username and password of the mySQL database that contains the zillow db. Store that env file locally in the repository.

Clone my repo and don't forget to confirm .gitignore is hiding your env.py file in case you accidently uplaod something

Library imports are pandas, matplotlib.pyplot, seaborn, scipy, numpy, sklearn('model_selection, 'metrics', 'linear_model', 'preprocessing', 'cluster') 


### Project Goals

The goal is to beat the baseline model in predicting logerror for Single-Family homes that had transactions in 2017


### Project Description

Housing is a billion dollar industry for investors and possibly the biggest purchase of a lifetime for some homeowners. Determining where and when to buy can have huge financial repercussions. We aim to help you make an informed decision!


### Initial Testing and Hypotheses

- Locationlocationlocataion. Is it really all about location?

- What catagorical valiables correlate with logerror?

- What continous variables correlate with  logerror?

### Report findings:
### Results
- Polynomial Regression of the Second Order gave the best results
- Standard and Robust scaling were about the same. Standard was .00002 better
- Model gives a 2.29% increase in accuracy

### Future work

I would like to build different models for single family homes and mansions. Although all the data is listed as Single Family Home, in reality, homes with 14 bedrooms are not marketed to the average single family consumer.

I would like to split the data based on land (0 bed/bath), home (1 bath, 1-5 bed), mansion (>5 bed)

Continue analyzing independent variables to find a stronger correlation with dependent variable

If I had more time I would run models with different hyperparameters to verify I had the best model available

## Detailed Project Plan

### Acquire

Requires:

    env.user
    env.password
    env.host

get_zillow_data()

    Function gets zillow first from save file inside folder, then, if no file exits, it will pull directly from mysql.

new_zillow_data()

    pulls data from mysql

### Cleaning

### NULLS

### YEAR BUILT
Regionidcity -- mode (categorical) \
Regionidzip -- mode (categorical)

### SIZE
Lotsizesquarefeet -- median (skewed data set, use median not mean) \
Lotsizesquarefeet -- dropped 7 rows with suspect values (extremely large and identical, acquire_to_py.df_6971) \
Calculatedfinishedsquarefeet -- median (skewed dataset, use median not mean) \
Finishedsquarefeet12 -- dropped due to strong similarities to 'lotsizesquarefeet' column

### TIME
Assessmentyear -- 2016 for all values \
Year built -- mode (essentially catagorical in this case)

### TAX
Tax_columns -- dropped to mitigate target leakage

### COUNT
Fullbathcnt -- was missing values. Bed and bath are complete columns. I can make a more 	      accurately filled column using data available.

Calculatedbathnbr -- was missing values. Bed and bath are complete columns. I can make a more accurately filled column using data available. 

### LOCATION
Censustractandblock -- dropped 1 row based on suspect number (started with a 4 not a 6). Based on how census blocks are derived, I think it highly unlikely that the census block is accurate. also note, in the rawcensustractandblock, all values start with 6


### Columns
36 columns had > 30% nulls and were subsequently dropped \
List: acquire_to_py.col_drop_too_many_nulls (is saved in notebook)

## Duplicates
121 rows were dropped for being duplicates by 'parcelid' \
List: acquire_to_py.duplicate_rows (is saved in notebook)


train, validate, test = prepare.split_telco_data()

    20% of data into test group
    30% of remaining data into validate group (30% of 80% = 24% of total data)
    70% of remaining data into train group (70% of 80% = 56% of total data)

target leakage

    data is further split to avoid target leakage

    x_train = train.drop(columns=['logerror'])
    y_train = train.logerror

    x_validate = validate.drop(columns=['logerror'])
    y_validate = validate.logerror

    x_test = test.drop(columns=['logerorr'])
    y_test = test.logerror


### Prep Zillow

- Cleans data
- Renames columns for ease
- Drops unnecessary columns


###  Split Zillow 

Data split:

    20% of data into test group
    30% of remaining data into validate group (30% of 80% = 24% of total data)
    70% of remaining data into train group (70% of 80% = 56% of total data)

Data is further split to avoid target leakage:
    
    x_train = train.drop(columns=['logerror'])
    y_train = train.logerror

    x_validate = validate.drop(columns=['logerror'])
    y_validate = validate.logerror

    x_test = test.drop(columns=['logerorr'])
    y_test = test.logerror



### Explore

- Locationlocationlocataion. Is it really all about location?

- What catagorical valiables correlate with logerror?

- What continous variables correlate with logerror


For example:

Visual:
    created stripplot, scatterplot, barplot, boxplot, and more
    
Statistical: 
      t-tests on clusters


Summary

Features based on visual analysis:

-Logerror is not strongly correlated with any location, catagorical variable, or continous variable. 

-Use clustering methods to see if clustering algorithum finds patters
- Cluster on 3 features
    -size
    -time sold
    -location

-Use clusters as features
    
    
 Features based on statistical analysis:
    Again, not a lot of strong correlation between independent variables and dependent variable. However, clustering algorithums were able to find statistically significant clusteres



### Scaling:

    I have scaled data set using two different methods. 


    Standard Scaling (mean of data = 0) 
    Robust Scaling - better at handling outliers
    


### Modeling

Select Evaluation Metric

- minimize rmse for logerror
- use abs value to +/- values don't cancel out

Evaluate Baseline

    The baseline is the mean of the absolute value of the target value.

Develop 4 Models:
Evaluate on Train
Evaluate on Validate 


Linear Regression
Polynomial Regression (degree = 2)
Lasso Lars (alpha = 1.0)
TweedieRegression (power=0, alpha=0)


### Evaluate Top Model on Test

Polynomial Regression (degree = 2)
- Model gives a 2.29% increase in accuracy























































































































