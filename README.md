# The Ames Housing Sales Price Prediction Challenge

# Problem Statement: 

1. The purpose of this project is to create and iteratively refine a multi-linear-regression (MLR) model.
1. Success will be measured by the $\textbf{R}^2$ values of train and test scores and how optimal the value becomes as a result of fitting (the absolute difference between these values being close to $0$). 
1. Finally, we upload predictions with the lowest Root-Mean-Square-Error (RMSE) to the Kaggle competition submission portal, where these scores will be compared with other competitors scores to decide upon who created the best model. 
1. We provide insights through reporting and presentation.
1. In conclusion, the finding of this project will be of particular interest to those considering a first-time home purchase, in order to make the best decision possible and taking all the relevant factors into consideration.

Ultimately, we recommend deciding upon a first-time home purchase by overall quality, square footage, numbers of various rooms, and other factors most highly correlated with sales price. Our model is highly accurate with a root-mean-squared-error of $23k$ dollars of actual housing price and we delve into more detail within the actual `.ipynb` notebooks found in this repo. 

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

### Import Data - Train from `train.csv` and Test from `test.csv`

Find a sample mean and upload to Kaggle as a template for future Kaggle submission for the in-class competition.

## Data Munging and Exploratory Data Analysis (EDA) 

### Data Munging - Fill Null values from certain numerical columns with median values from overall column. Typically the mean values may be used for normally distributed variables; however, in our case some of these variables are not normally distributed and are either left-skewed or right-skewed, thus, we fill with median values and have zero null values for the modeling stage.  

### Exploratory Data Analysis - Survey variables to ascertain which ones are highly correlated with `Sales Price` and which ones are normal variables (Gaussian distribution in histogram)

Use these variables as features for our train-test-split. Feature Engineer and create dummy variables for other relevant varables (houses built after the year `2000`, external quality of house, etc.). We go into more detail within the notebook as to why we chose these values for feature engineering and their significance in determining housing prices. 

# Sections of `Modeling_And_ErrorMetrics.ipynb`

## Train-Test-Split on Train Data

Our baseline prediction from our null model was a mean housing price of around $181\text{k-}182\text{k}.$

### We use `LinearRegression(), Lasso(), Ridge()`

Scaling, Polynomial Features, and other modeling methods are utilized. 

## Metrics

### MAE and RMSE, among other metrics are utilized to evaluate model performance. 

Our best models utilized the following variable features and resulted in the following $\textbf{R}^2$ values and error metrics:

#### Ridge: 

(See `Munging_EDA_FeatureEngineering.ipynb` for variable details.)

features = ['Overall Qual', 'Gr Liv Area', 'Garage Area', 'Garage Cars','Total Bsmt SF','1st Flr SF','Year Built','Year Remod/Add','Full Bath','Garage Yr Blt','TotRms AbvGrd','Mas Vnr Area','Fireplaces','BsmtFin SF 1','Wood Deck SF','Open Porch SF','After 2000','Exter Qual','Overall Qual','Gr Liv Area Times Garage Area','Kitchen Qual_Ex','Kitchen Qual_Fa','Kitchen Qual_Gd','Kitchen Qual_TA','Total Bsmt SF Times 1st Flr SF','Heating QC_Ex','Heating QC_Fa','Heating QC_Gd','Heating QC_TA',]

$\alpha = 422.92$
The train score for ridge model is $0.926$
The test score for ridge model is $0.924$
$0.2\%$ difference
RMSE Ridge | $21103.620$

Kaggle Score: $24618.458$ Score

#### Lasso: 

features = ['Overall Qual', 'Gr Liv Area', 'Garage Area', 'Garage Cars','Total Bsmt SF','1st Flr SF','Year Built','Year Remod/Add','Full Bath','Garage Yr Blt','TotRms AbvGrd','Mas Vnr Area','Fireplaces','BsmtFin SF 1','Wood Deck SF','Open Porch SF','After 2000','Exter Qual','Overall Qual','Gr Liv Area Times Garage Area','Kitchen Qual_Ex','Kitchen Qual_Fa','Kitchen Qual_Gd','Kitchen Qual_TA','Total Bsmt SF Times 1st Flr SF','Heating QC_Ex','Heating QC_Fa','Heating QC_Gd','Heating QC_TA','1st Flr SF Times 2nd Flr SF','Neighborhood_NridgHt','Neighborhood_Timber','Bsmt Full Bath','Neighborhood_StoneBr','Neighborhood_Somerst','Neighborhood_NoRidge','Not Kitchen Qual_TA','Not Heating QC_TA','Not Neighborhood_OldTown']

The train score for lasso model is $0.928$
The test score for lasso model is $0.927$
$0.001\%$ difference

MAE Lasso | $14448.1199$

RMSE Lasso | $20642.9603$

Kaggle score : $23322.667$ lowest RMSE yet proceeded with Lasso.

In conclusion, the most superior model ended up being Lasso as it resulted in the best Kaggle submission (least RMSE). Each of these models were only slightly overfit. Please see the training log (titled `Project 2 Notes Training Log`) for more details regarding the iterative process. 

## Use predict method for Test Data `kaggle_data`

### The data is in numpy array format until passed and converted into dataframe for `ridge.predict` and `lasso.predict` methods.

We then successfully export the data as a `.csv` file for the Kaggle competition upload.
