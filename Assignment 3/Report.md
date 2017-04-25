## Introduction

This report addresses the issue of multicollinearity by using the concept of Principal Component Analysis (PCA). PCA is used as a technique to reduce the dimension and remediate the issue of multicollinearity in OLS regression. Multicollinearity exists when there are non-linear dependencies among the regressors. As a part of this report, we will analyze the stock portfolio dataset that has a total of 502 observations for 20 company stocks and a Vanguard index fund (VV). The dataset is continuous; however, in order to perform a detailed analysis of the data, we need to first perform a data wrangling exercise to ensure that the dataset is accurate and appropriate for the desired use.

## Log return:

We compute the log return of today’s stock price to the yesterday’s stock price. This exercise helps us to use the log-returns of individual stocks as a tool to explain the variation in log- returns of the index fund. This helps us to understand the security returns overall. In addition, log transformation is used to stabilize the variance.

## Correlation between the 20 individual stocks and market index with visualization:

We leveraged the PROC CORR in SAS to identify correlation between each individual stocks and the market index fund. Table 1 below shows the SAS output of the correlation. As indicated by the Table 1 below, all of the 20 variables have a positive correlation with the market index. The two stocks with highest correlation R values are “HON” and “MMM” – they have the R value of approximately 0.76. DPS seems to be the stock with lowest R value (approximately 0.44).

![image](https://cloud.githubusercontent.com/assets/26909910/25407358/09da9ed8-29d8-11e7-8341-40ab008112fe.png)

Table 1: Correlation of twenty individual stocks with the market index

![image](https://cloud.githubusercontent.com/assets/26909910/25407400/282997ae-29d8-11e7-9779-1021daa3a80b.png)

Figure 1: Correlation bar chart of twenty individual stocks with the market index

## Principal Component Analysis (PCA):

After identifying the correlation of each individual stock to the market index, we use the principal component analysis process to help reduce the dimension by setting up a set of new uncorrelated variables identified as Principal component and referred as Prin1, Prin2…….Prin20. It is important to note that each of the principal components is a linear combination of correlated variables from the individual stock. The principal components are then arranged in descending order based on the eigenvalue (a.k.a. importance) as shown in Table 2 below. Table 2 shows the eigenvalue in descending order, and highlights the difference, proportion, and cumulative value of each principal component.

Upon illustrating eigenvalues and corresponding difference, proportion, and cumulative in Table 1, we used scree plot to visualize the data. Based on the scree plot shown in Figure 2, the ‘elbow’ shape is visible when the curve flattens at 8 (i.e. when principal component is 8) on x- axis. Figure 2 makes it easy for us to conclude that the number of principal components to be used can be reduced to 8 by clearly showing the flatness at principal component 8. In addition, in Figure 3, we plotted the principal components against the proportion of variance, and we found that the first 8 principal components explain approximately 80% of the variance. Finally, the cumulative column of Table 2 also supports the findings presented in Figure 2 and 3 that the first 8 components account for 80% of the variation. Hence, we only select the first 8 principal components for this study.

![image](https://cloud.githubusercontent.com/assets/26909910/25407474/6cc119b4-29d8-11e7-9eb8-606d4e4f58fe.png)

Table 2: Eigenvalue of the correlation matrix

![image](https://cloud.githubusercontent.com/assets/26909910/25407493/805cda12-29d8-11e7-9b4c-d4a8b103c10e.png)

Figure 2: Scree plot of the eigenvalue and principal component

![image](https://cloud.githubusercontent.com/assets/26909910/25407514/9269c7b0-29d8-11e7-9755-32d5d4f2c64f.png)

Figure 3: Scree plot of the cumulative proportion and proportion explained by principal component

## Eigenvectors Plot:

Upon selecting the first 8 principal components, we plot the first two principal components in Figure 4 below. Figure 4 shows that the first two principal components account for about 56% of the stock return variance. Figure 4 also helps us to visualize the spread of the stock data on the plot.

![image](https://cloud.githubusercontent.com/assets/26909910/25407567/c290673c-29d8-11e7-8158-d996b4f211e1.png)

Figure 4: First two principal components ‘ relative variance chart

## Test-Train Data:

Leveraging the uniform random sample generator to split the data set in 70-30 training-test datasets, we were able to split the stock data into 70% training dataset composed of train- response variable, and 30% test dataset not containing the train-response variable. In order to evaluate the predictive accuracy of the model, we will fit our model using the training dataset and evaluate the out-of-sample performance using the test dataset. Table 3 below shows a frequency table of the test-train split.

![image](https://cloud.githubusercontent.com/assets/26909910/25407595/de75381a-29d8-11e7-87d6-29814961da58.png)

Table 4: Test-Train split frequency table

## Model building:

Using the test-train data above, we were able to deduce our first model to be the following:

    Model 1 (Individual stocks=predictors & train_response=response):
    
    train_response (log-return vv) = 0.0000864 + 0.01769* return_AA + 0.03198* return_BAC + 0.00111 * return_BHI 
    + 0.04907 * return_CVX + 0.04674 * return_DD + 0.03642 * return_DOW + 0.03670* return_DPS + 0.04849 * return_GS 
    + 0.00948 * return_HAL + 0.00359* return_HES + 0.12213 * return_HON + 0.02712 * return_HUN + 0.00902 * return_JPM 
    + 0.07903* return_KO + 0.09796* return_MMM + 0.01673 * return_MPC + 0.02911 * return_PEP + 0.03776 * return_SLB 
    + 0.07587 * return_WFC + 0.05467* return_XOM


We need to evaluate Model 1 to check for predictive accuracy. Therefore, we will perform an analysis of variance process, and calculate the regression standard error and coefficient of determination to evaluate the relationship between the predictor and response variables.
 
ANOVA table in Table 5 shows the p-value less than 0.0001. This confirms the non-zero slope of the model. The adjusted R-squared value of 0.89 in Table 6 indicates the model variance of 89%. Detailed values of all parameter estimates are presented in Table 7 below. We further test the model accuracy, and goodness-of-fit by using the residual plot for the model. Figure 5 below shows the residual plots for the model.


![image](https://cloud.githubusercontent.com/assets/26909910/25407666/36338f7a-29d9-11e7-8d9f-a38dd604450a.png)

Table 5: Test-Train ANOVA Table

![image](https://cloud.githubusercontent.com/assets/26909910/25407672/39b28836-29d9-11e7-907d-142415e9732f.png)

Table 6: Coefficient of Determination

![image](https://cloud.githubusercontent.com/assets/26909910/25407680/3e45d9b6-29d9-11e7-88cb-49bb72bc2b98.png)

Table 7: Parameter Estimates for Model1

Table 7 includes a VIF column that helps to detect the non-pairwise correlation. VIF values in Table 7 indicate that the model does not have a serious multicollinearity issues. Generally speaking, a model is said to have high multicollinearity if the VIF values of the model is greater than 5. VIF value higher than 5 generally mean that the multicollinearity level in the model is
 
higher than acceptable, and is seriously flawed. However, a VIF value of 3 or higher does indicate a fairly mild multicollinearity issue, and Model1 shows multiple instances of higher than 3 VIF value. Therefore, even though the model does not have serious multicollinearity issue, it does suffer from some level of multicollinearity.

![image](https://cloud.githubusercontent.com/assets/26909910/25407861/fb056404-29d9-11e7-97b6-2fd9f9963f13.png)

Figure 5: Residual Plot for Model1

## Predictive Accuracy and Goodness-of-fit:

After performing the residual analysis, and evaluating the VIF of the model, we calculated mean square error and mean absolute error for both, train and test, datasets. Table 8 below shows the MES and MAE output for Model1, which further confirms that Model 1 is fairly an accurate depiction for both, train and test, datasets. Negligible difference in the MAE and MSE for train and test datasets makes it evident that the Model1 works well in both scenarios.

![image](https://cloud.githubusercontent.com/assets/26909910/25407909/27065a2c-29da-11e7-8d4f-4677a850ea72.png)

Table 8: MAE and MSE for train and test datasets

## Model 2 (8 principal components=predictor & train_response=response):

        Model2:

        train_response (log-return VV) = 0.00075978+0.00231*Prin1+0.00032245*Prin2+0.00070635*Prin3
        +0.00030481*Prin4-0.00017356*Prin5+0.00000315*Prin6-0.00010331*Prin7-0.00040760*Prin8


We performed the similar steps as performed in Model1 to compute the ANOVA table, Coefficient determination, residual plot analysis, and VIF evaluation using parameter estimates for Model2. Tables 9 thru 12 present the ANOVA table, Coefficient determination, residual plot analysis, and VIF evaluation using parameter estimates in order.

![image](https://cloud.githubusercontent.com/assets/26909910/25407958/59c52718-29da-11e7-8d79-25a35635eb29.png)

Table 9: ANOVA table for Model2

ANOVA table above shows the p-value less than 0.0001, which is similar to the p-value of Model1. This confirms the non-zero slope of the model. Similarly, Adjusted R-squared presented in Table 10 shows the model variance of about 89% for Model2, which is very close to the model variance of Model1 with a total of 20 predictor variables. We further test the model accuracy, and goodness-of-fit by using the residual plot for the model below.

![image](https://cloud.githubusercontent.com/assets/26909910/25407986/6ea914c8-29da-11e7-9fe2-56f9e2fd30a0.png)

Table 10: Coefficient determination table for Model2

![image](https://cloud.githubusercontent.com/assets/26909910/25408002/7d33d3fc-29da-11e7-986d-3868b7c6bb94.png)

Table 11: Parameter Estimates table for Model2

![image](https://cloud.githubusercontent.com/assets/26909910/25408014/89e83962-29da-11e7-927b-c1eb981a25f8.png)

Table 12: Residual plots for Model2

Similar to what we presented in Model1, Table 11 includes a VIF column that helps to detect the non-pairwise correlation. VIF values in Table 11 indicate that the model does not have any multicollinearity issues. Generally speaking, a model is said to have high multicollinearity if the VIF values of the model is greater than 5. VIF value higher than 5 generally mean that the multicollinearity level in the model is higher than acceptable, and is seriously flawed. However, a VIF value of 3 or higher does indicate a fairly mild multicollinearity issue, and Model1 shows multiple instances of higher than 3 VIF value, but Model2 does not show any indication of higher than 1 VIF value. Therefore, Model2 does not have any multicollinearity issue whatsoever. In addition, the residual plots shown in Table 12 indicate that the model is approximately normally distributed, and possesses constant variance. Hence, Model2 passes the initial adequacy and viability test. We further test the predictive accuracy of the model using the mean square error and mean absolute error for Model2. Table 13 below shows the calculation of MSE and MAE for Model2:

![image](https://cloud.githubusercontent.com/assets/26909910/25408061/b23e9b22-29da-11e7-8b86-a61787b8b018.png)

Table 13: MSE and MAE for Model2

The MSE and MAE for both, train and test, datasets have a negligible difference between the two. Therefore, this further confirms that Model2 is an accurate depiction for both, train and test, datasets. Negligible difference in the MAE and MSE for train and test datasets makes it evident that the Model2 works well in both scenarios.

## Conclusion:

In this report leveraging the principal component analysis process, we evaluated two different OLS regression models – Model1 and Model2. We started by selecting the principal components, and verifying with reasoning that 8 principal components is an ideal number of principal coefficients to perform the analysis. We then built two models one with 20 predictor variables (Model1) and other with 8 predictor variables (Model2). Model1 used all stock log- returns against the market index log-returns (VV), and had multicollinearity issues. There were multiple instances when the VIFs of Model1 exceeded 3. Whereas, the second model – Model2 – with only 8 total predictor variables used the first 8 principal components, and totally eliminated the multicollinearity issue. Therefore, we verified and presented in action PCA’s ability to eliminate multicollinearity issues through this exercise.

