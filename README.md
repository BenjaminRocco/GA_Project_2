# Project 2 - Ames Housing Data and Kaggle Challenge

# Problem Statement: 

1. The purpose of this project is to create and iteratively refine a multi-linear-regression (MLR) model.
1. Success will be measured by the $\textbf{R}^2$ values of train and test scores and how optimal the value becomes as a result of fitting (the absolute difference between these values being close to $0$). 
1. Finally, we will upload predictions with the lowest Root-Mean-Square-Error (RMSE) to the Kaggle competition submission portal, where these scores will be compared with our classmate's scores to decide upon who created the best model. 
1. In class, we will provide insights through reporting and presentation.
1. In conclusion, the finding of this project will be of particular interest to those considering a first-time home purchase, in order to make the best decision possible and taking all the relevant factors into consideration. 

# Folder Organization

## Main `project_2` directory has `README.md` file and `Project_2_GA_Presentation.pdf` the `.pdf` version of the Microsoft Office Powerpoint presentation. 

## Subdirectories include `code`, `datasets`, and `images`. 

### `code`

Coding files consist of two files: 
- `Munging_EDA_FeatureEngineering.ipynb` includes all data munging, EDA, and feature engineering.
- `Modeling_And_ErrorMetrics.ipynb` includes all train-test split, modeling, and error metric and final export code. 

### `datasets`

Includes all datasets submitted to the Kaggle competition predicting housing prices from an unknown dataset, some variation of `mean_submission_<unique_tag>.csv`

### `images`

Include images from `Munging_EDA_FeatureEngineering.ipynb` as well as images formatted specifically for the sole purpose of use within the powerpoint presentation. Please note some images were edited further within powerpoint for presentation friendly features.  

# Sections of `Munging_EDA_FeatureEngineering.ipynb`

## Imports

### Import Data - Train from train.csv and Test from test.csv

Find a sample mean and upload to Kaggle as a template for future Kaggle submission for the in-class competition.

## Data Munging and Exploratory Data Analysis (EDA) 

### Data Munging - Drop Null values from certain numerical columns with minimal footprint so as to not completely compromise dataset. 

The purpose of this is to allow for training on data, fill certain columns with values when Null values are too numerous (Front Lot).

### Exploratory Data Analysis - Survey variables to ascertain which ones are highly correlated with `Sales Price` and which ones are normal variables (Gaussian distribution in histogram)

Use these variables as features for our train-test-split. Feature Engineer and create dummy variables for other relevant varables (houses built after 2000, external quality of house, etc.)

# Sections of `Modeling_And_ErrorMetrics.ipynb`

## Train-Test-Split on Train Data

Our baseline prediction from our null model was a mean housing price of around $181\text{k-}182\text{k}.$

### We use `LinearRegression(), Lasso(), Ridge()`

Scaling, Polynomial Features, and other modeling methods are utilized. 

## Metrics

### MAE and RMSE, among other metrics are utilized to evaluate model performance. 

Our best models utilized the following variable features and resulted in the following $\textbf{R}^2$ values and error metrics:

#### Ridge: 

features = ['Overall Qual', 'Gr Liv Area', 'Garage Area', 'Garage Cars','Total Bsmt SF','1st Flr SF','Year Built','Year Remod/Add','Full Bath','Garage Yr Blt','TotRms AbvGrd','Mas Vnr Area','Fireplaces','BsmtFin SF 1','Wood Deck SF','Open Porch SF','After 2000','Exter Qual','Overall Qual','Gr Liv Area Times Garage Area','Kitchen Qual_Ex','Kitchen Qual_Fa','Kitchen Qual_Gd','Kitchen Qual_TA','Total Bsmt SF Times 1st Flr SF','Heating QC_Ex','Heating QC_Fa','Heating QC_Gd','Heating QC_TA',]

$\alpha = 422.9242874389499$
The train score for ridge model is $0.9263867855343225$
The test score for ridge model is $0.9243491533316479$
$0.2\%$ difference
RMSE Ridge | $21103.620038900877$

Kaggle Score: $24618.45763$ Score

#### Lasso: 

features = ['Overall Qual', 'Gr Liv Area', 'Garage Area', 'Garage Cars','Total Bsmt SF','1st Flr SF','Year Built','Year Remod/Add','Full Bath','Garage Yr Blt','TotRms AbvGrd','Mas Vnr Area','Fireplaces','BsmtFin SF 1','Wood Deck SF','Open Porch SF','After 2000','Exter Qual','Overall Qual','Gr Liv Area Times Garage Area','Kitchen Qual_Ex','Kitchen Qual_Fa','Kitchen Qual_Gd','Kitchen Qual_TA','Total Bsmt SF Times 1st Flr SF','Heating QC_Ex','Heating QC_Fa','Heating QC_Gd','Heating QC_TA','1st Flr SF Times 2nd Flr SF','Neighborhood_NridgHt','Neighborhood_Timber','Bsmt Full Bath','Neighborhood_StoneBr','Neighborhood_Somerst','Neighborhood_NoRidge','Not Kitchen Qual_TA','Not Heating QC_TA','Not Neighborhood_OldTown']

The train score for lasso model is $0.9282990792350672$
The test score for lasso model is $0.927615791511294$
$0.07\%$ difference

MAE Ridge | $15345.579003147821$
MAE Lasso | $14448.11988434666$

RMSE Ridge | $20622.708586182438$
RMSE Lasso | $20642.96030481706$

Kaggle score : $23322.66654$ lowest RMSE yet proceeded with Lasso.

In conclusion, the most superior model ended up being Lasso as it resulted in the best Kaggle submission (least RMSE). Please see the training log (titled `Project 2 Notes Training Log`) for more details regarding the iterative process. 

## Use predict method for Test Data `kaggle_data`

### The data is in numpy array format until passed and converted into dataframe for `ridge.predict` and `lasso.predict` methods.

We then successfully export the data as a `.csv` file for the Kaggle competition upload.
