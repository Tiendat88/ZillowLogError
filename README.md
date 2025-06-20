Zillow Home Value Prediction
Overview
This Jupyter notebook analyzes property and transaction data from Zillow to predict the log-error between Zillow's estimated home prices (Zestimate) and actual sale prices. The log-error is defined as log(Zestimate) - log(SalePrice). The analysis uses PySpark for data preprocessing and modeling, scikit-learn for evaluation, and Tkinter for a simple GUI to query predictions. The goal is to assist in improving Zillow's home value estimation by modeling the log-error.
Objectives

Data Preparation: Combine property data (properties_2016.csv, properties_2017.csv) and transaction data (train_2016_v2.csv, train_2017.csv) to create a unified dataset.
Data Cleaning: Handle outliers in the logerror column using Z-score thresholding and encode categorical variables.
Modeling: Build a Linear Regression model to predict logerror using property features.
Evaluation: Assess model performance using Mean Absolute Error (MAE) and Root Mean Square Error (RMSE).
Prediction Interface: Provide a Tkinter-based GUI to query the average predicted log-error for a specific year and month.

Features

Data Preprocessing: Joins large datasets, removes outliers, extracts temporal features (year, month, day) from transactiondate, and encodes categorical variables (propertycountylandusecode, propertyzoningdesc).
Modeling: Uses Linear Regression for its simplicity, speed, and interpretability, with hyperparameter tuning via cross-validation.
Evaluation: Computes MAE and RMSE to evaluate prediction accuracy.
GUI: Includes a Tkinter interface to input a year and month and retrieve the average predicted log-error.
Scalability: Leverages PySpark for efficient processing of large datasets.

Prerequisites
Ensure you have the following installed:

Python 3.6 or higher
Jupyter Notebook
Apache Spark (for PySpark)
Libraries listed in requirements.txt

Installation

Clone or download the repository.
Install the required dependencies by running:pip install -r requirements.txt


Ensure the datasets (properties_2016.csv, properties_2017.csv, train_2016_v2.csv, train_2017.csv) are available in the specified directory or update the file paths in the notebook.
Configure Apache Spark for PySpark by setting up SPARK_HOME and adding it to your system path.

Usage

Open the Jupyter notebook:jupyter notebook zillow_home_Apolo_ver2.ipynb


Run the cells sequentially to:
Load and join the property and transaction datasets for 2016 and 2017 using PySpark.
Clean the data by removing outliers in logerror (Z-score > 3 or < -3) and encoding categorical variables.
Extract temporal features from transactiondate and assemble features for modeling.
Train a Linear Regression model with hyperparameter tuning using cross-validation.
Evaluate the model using MAE and RMSE, saving results to model_results.txt and model_results_cross.txt.
Launch a Tkinter GUI to input a year and month and view the average predicted log-error.


Outputs include:
model_results.txt: MAE and RMSE for the initial Linear Regression model.
model_results_cross.txt: MAE and RMSE for the cross-validated model.
A Tkinter GUI for querying predicted log-error by year and month.



Dataset
The datasets include:

properties_2016.csv and properties_2017.csv: Property features (e.g., bathroomcnt, bedroomcnt, yearbuilt, taxvaluedollarcnt) for 2016 and 2017, with 2,985,217 rows each and 58 columns.
train_2016_v2.csv and train_2017.csv: Transaction data with parcelid, logerror, and transactiondate for 2016 (90,275 rows) and 2017 (77,613 rows).
Combined dataset: Joins property and transaction data, resulting in a dataset with 60 columns.

File Structure

zillow_home_Apolo_ver2.ipynb: Jupyter notebook containing the analysis, modeling, and GUI code.
properties_2016.csv, properties_2017.csv, train_2016_v2.csv, train_2017.csv: Input datasets (not included; must be provided).
model_results.txt: Stores MAE and RMSE for the initial model.
model_results_cross.txt: Stores MAE and RMSE for the cross-validated model.
requirements.txt: Lists required Python libraries.
README.md: This documentation file.

Dependencies
See requirements.txt for the list of required Python libraries.
Notes

Outlier Handling: Outliers in logerror are replaced with the mean value if their Z-score exceeds 3 or is below -3.
Feature Selection: All non-logerror columns are used as features after encoding categorical variables and extracting temporal features.
Model Choice: Linear Regression is chosen for its simplicity and interpretability, though more complex models (e.g., Random Forest, Gradient Boosting) could improve performance.
Hyperparameter Tuning: Cross-validation is used to tune regParam, elasticNetParam, and fitIntercept for the Linear Regression model.
GUI: The Tkinter interface allows users to input a year and month to retrieve the average predicted log-error, with input validation for months (1-12).
Performance: The model achieves an MAE of ~0.054 and RMSE of ~0.089, indicating reasonable accuracy with minimal large errors.

Troubleshooting

Missing datasets: Ensure all four CSV files are in the correct directory or update the file paths in the notebook.
PySpark errors: Verify Spark installation and configuration (SPARK_HOME, Python compatibility). Check for warnings about native libraries (e.g., JNIBLAS, JNILAPACK) and ensure dependencies are installed.
GUI issues: Ensure Tkinter is installed (pip install tk). If the GUI fails to launch, check for network-related errors in PySpark (e.g., Operation timed out).
High MAE/RMSE: Consider feature engineering, handling missing values, or using a more complex model to improve performance.
Outlier handling: Adjust the Z-score threshold if too many or too few outliers are being replaced.

License
This project is for educational purposes and provided as-is without any warranty.
