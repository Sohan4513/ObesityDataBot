# WeightDistributionBot

## **Overview**
This project analyzes **obesity-related factors** using data from the **CDC Behavioral Risk Factor Surveillance System (BRFSS)**. It includes **data wrangling, cleaning, and machine learning models** to predict obesity (_RFBMIS variable) using **logistic regression with ridge regularization**.

## **Dataset**
- The dataset used is in **XPT format** (LLCP2022.XPT), which is read using the `haven` package.
- Data is preprocessed by **removing missing values, filtering specific features, and selecting relevant predictors**.

## **Requirements**
Install the required R libraries before running the script:
```r
install.packages(c("haven", "tidyr", "tidymodels", "dplyr", "caret", "vip"))
```

## **Workflow**
### **1. Data Preprocessing**
- Load the dataset using `haven::read_xpt("LLCP2022.XPT")`
- Remove variables that introduce multicollinearity.
- Drop columns with **more than 40% missing values**.
- Filter out invalid/missing responses (e.g., `c(7, 9, 99)` codes).
- Convert the target variable **_RFBMIS (obesity status)** into a factor.

### **2. Splitting the Data**
- The dataset is split into **training (CDC_train) and test (CDC_test) sets** (50% split).

### **3. Training the Logistic Regression Model**
- Uses a **ridge regression model** (`glmnet`).
- Feature preprocessing includes:
  - Handling new levels in test data.
  - Converting categorical variables into dummy variables.
  - Scaling and normalizing predictors.
  - Removing zero-variance features.
- Cross-validation (`vfold_cv`) is used to tune the penalty parameter.

### **4. Model Evaluation**
- The best penalty is selected using **ROC AUC** as the metric.
- Predictions are made on the test set.
- Model accuracy and ROC AUC are computed.

## **Results**
- The script outputs:
  - **Logistic regression coefficients** as a visualization.
  - **Prediction accuracy** on the test set.
  - **ROC curve analysis** for model performance.

## **How to Run**
1. Ensure `LLCP2022.XPT` is in the working directory.
2. Run the R script in **RStudio** or an R environment.
3. Check the model’s performance metrics.

## **Future Improvements**
- Incorporate additional predictors.
- Compare different ML models (e.g., random forest, SVM).
- Optimize hyperparameters for better performance.

---
