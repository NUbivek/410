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

