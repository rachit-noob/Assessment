# Assessment

## Approach

### 1. Data Preprocessing

    a. Null Values
        1. Some cols have more than 81% of the values as null. Cannot fill these values without knowing about the cols. (with backfilling, etc.)
        2. Some cols have ~13% of the values as null.
        Not considering removing rows, since data points are less.
        
        Hence, Dropping cols with more than 80% null. And filling the rest. Median for Numeric, mode for cat.

    b. Outlier Removal 
        There were multiple ways to deal with outliers:
            1. Removing outliers using IQR, +3<=x>=-3 standard deviation, etc. But we lose information (and data is less)
            2. Capping the outliers, but then the data does not hold the correct information.
            3. Keeping the outliers.

            So I kept the outliers and handled it while feature scaling, using Roburst Scaler. Which handles the outlier data pretty well and the feature scaled data is not impacted by outliers.

    c. Imbalanced Dataset
        Method1 : Applying oversampling techniques like SMOTE. 
        Method2 : Keeping the data as it is. Since the ratio is 1:2

        I tried both the methods.
        
    d. Feature Scaling 
        Scaled the features using the Roburst Scaler method.
    
    e. Multicollinearity
        Handled multicollinearity between the independent features using the VIF. 
        A rule of thumb is that if VIF score is more than 10, we remove the col with highest VIF score iteratively.
        Iteratively removal of cols is necessary because else we might end up removing the cols which don't have high correlation.

    
    f. Feature Selection 
        For algo's like Logistic Regression and SVM, selected the top 75% highly important features using Lasso regression.


### 2. Model Building
    Models have been build using 5-Folds Cross Validation and Grid Search CV for optimized parameter tuning.

    a. Logistic Regression and SVM
        Performed an experiment to see how these models would perform
    
    But the performance of Logistic Regression and SVM was not great also because the relationship of the features and the distribution of data was not linear.
    Also, since the data size was less, so the potential issue that can occur is bias as well as variance. 
    Hence Ensemble approach was required.


    b.    ------------- Data without oversampling ------------------ 

        1. Decision Tree : Got an AUC score of around 72%
        2. Random Forest : Got an AUC score of around 76%
        3. XGBoost : Got an AUC score of around 77%


    c.    --------------- Oversampled Data ---------------------

        1. Decision Tree : Got an AUC score of around 82%
        2. Random Forest : Got an AUC score of around 89%
        3. XGBoost : Got an AUC score of around 90%

        A potential reason for better accuracy on oversampled data is because of high degree of data duplicacy in the minority class data.

        Both the Random forest model and XGBoost model performed well on Oversampled and Unsampled data.
        And the XGBoost model was performing slightly better.
        Hence trained a final XGBoost model.

    The final model is the averge of both the probability score of oversampled and unsampled XGBoost model.
    The average because the variance in probability was high and since oversampled data will slightly overfit, so to normalize it, took the average.


Constraints and Limitations : Due to hardware/software limitations, could not tune the parameters to its highest potential.

