# transcoding-processing-time-Regression

# Table Of Content
1. [Introduction](#my_first_title)
2. [Method](#my-second-title)
3. [Result](#my-third-title)
4. [Usage](#my-fourth-title)


## **Introduction**


This ReadMe is aimed at explaining the methodology that was chosen to analyze and do the regression for a data set concerning video transcoding. 
Regression techniques were used to predict the transcoding processing time. 



## **Method**

### **Preprocessing and Data Prepration**

As the first step in the data processing and preparation, rows with missing data were checked to be removed, but no missing rows were found. 
Then numerical and categorical data were split. Categorical data are just codec, the category and the o_codec.
All their values were counted and plotted against utime, which is our target parameter to understand how much they are correlated.
Then all categorical parameters were treated as dummies.
All other parameters are numerical data, and they were presented in histograms. An outlier detection function was applied to identify and remove any outliers, but none were found.
From the histograms we can see that the duration, i, frames and p follow a log shape.
Hence, the log of these parameters was taken, and their original parameters were dropped along with the id. The correlation between all variables was applied.
Any two variables having a correlation more than 0.95, one of them was removed.


![Capture](https://user-images.githubusercontent.com/75788150/178162257-42b5d95b-cb40-4fcf-bac6-6a16805f9408.PNG)





It ended up that log_p, height, size and
o_width were dropped.
Finally, as the last step of preprocessing all
variables were standardized along with the
target variable (utime) and after that utime
was also dropped.


### **Training - Test Set**


The data was split then into a training and test set to apply the different classification methods
and test their accuracy. By default, the test set was set to be 30% of the total data. For each
model, I defined the Model Structure itself and Parameterization space by which the greedy
search(gs) approach can iteratively examine through the defined space of parameters and pick
up the best parameter which can give us the minimum amount of error
(Objective_Function(J)). By defining the cross-validation (cv) equal to 3 in greedy search,
probability of over-fitting will decrease significantly.




## **Result**



![Capture](https://user-images.githubusercontent.com/75788150/178162285-97382f10-94de-457e-afaa-4d2ce61e8b6e.PNG)


![Capture](https://user-images.githubusercontent.com/75788150/178162301-3030364b-78c1-497e-bdce-fdb470122154.PNG)



Different regression models were applied to the final standardized data. Looking at the above results we can see that the random forest model is giving us the lowest possible mean absolute error (MAE), while the leaner regression is giving the worst results.
The negative MAE was applied to directly see which is the highest results. Due to the slight difference between the train and test results in the random forest there’s a slight overfitting, which can be neglected.




### ** Linear Regression Analysis**

Plotting the error against the normal distribution for the linear regression, we can see that the error is not following a perfect normal distribution and heteroscedasticity is present in below figure, which is a
result of the large range of observed values or due to the presence of outliers. The model that was followed to remove outliers was from the 0.5 to the 0.95 quantile. Maybe increasing the scale for the outlier removal from the 0.25 till the 0.75 quantile would fix the residuals to an extent.
Due to the presence of heteroscedasticity, the p-values are relatively small (6.191366558121906e-78 for the Kolmogorov-Smirnov Test and 0 for the D’Agostino Test).


![Capture](https://user-images.githubusercontent.com/75788150/178162351-3be60d25-23af-4c42-8e90-77623de491ab.PNG)




Also looking at the confidence interval for the different variables we can see that some of them can have a value that ranges from negative to positive values,
which is not a very determined coefficient with a specific effect toward the target

![Capture](https://user-images.githubusercontent.com/75788150/178162370-532f9859-99a3-4d12-8c23-0552db1baa05.PNG)









### **Random Forest Analysis**

In Random Forest model the residuals follow more the normal distribution shape, except for a few points, where they are far(figure below) . 
This explained by the same concepts explained above in the linear regression model analysis. Also, the p values were not that high (8.536372510233588e-184 for the Kolmogorov-Smirnov Test and 0 for the D’Agostino Test),
because some data have not been scaled properly during the standardization. 


![Capture](https://user-images.githubusercontent.com/75788150/178162434-7f71be01-7c4a-4a30-9035-96ba80588717.PNG)





## **Usage**

