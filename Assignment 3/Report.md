## Introduction

This report addresses the issue of multicollinearity by using the concept of Principal Component Analysis (PCA). PCA is used as a technique to reduce the dimension and remediate the issue of multicollinearity in OLS regression. Multicollinearity exists when there are non-linear dependencies among the regressors. As a part of this report, we will analyze the stock portfolio dataset that has a total of 502 observations for 20 company stocks and a Vanguard index fund (VV). The dataset is continuous; however, in order to perform a detailed analysis of the data, we need to first perform a data wrangling exercise to ensure that the dataset is accurate and appropriate for the desired use.

## Log return:

We compute the log return of today’s stock price to the yesterday’s stock price. This exercise helps us to use the log-returns of individual stocks as a tool to explain the variation in log- returns of the index fund. This helps us to understand the security returns overall. In addition, log transformation is used to stabilize the variance.

## Correlation between the 20 individual stocks and market index with visualization:

We leveraged the PROC CORR in SAS to identify correlation between each individual stocks and the market index fund. Table 1 below shows the SAS output of the correlation. As indicated by the Table 1 below, all of the 20 variables have a positive correlation with the market index. The two stocks with highest correlation R values are “HON” and “MMM” – they have the R value of approximately 0.76. DPS seems to be the stock with lowest R value (approximately 0.44).

![image](https://cloud.githubusercontent.com/assets/26909910/25407078/fa5c74c8-29d6-11e7-9f05-98f4cadd139f.png)

![image](https://cloud.githubusercontent.com/assets/26909910/25407104/1b1fa446-29d7-11e7-8222-9eaf7e5c5bdb.png)

## Principal Component Analysis (PCA):

After identifying the correlation of each individual stock to the market index, we use the principal component analysis process to help reduce the dimension by setting up a set of new uncorrelated variables identified as Principal component and referred as Prin1, Prin2…….Prin20. It is important to note that each of the principal components is a linear combination of correlated variables from the individual stock. The principal components are then arranged in descending order based on the eigenvalue (a.k.a. importance) as shown in Table 2 below. Table 2 shows the eigenvalue in descending order, and highlights the difference, proportion, and cumulative value of each principal component.

Upon illustrating eigenvalues and corresponding difference, proportion, and cumulative in Table 1, we used scree plot to visualize the data. Based on the scree plot shown in Figure 2, the ‘elbow’ shape is visible when the curve flattens at 8 (i.e. when principal component is 8) on x- axis. Figure 2 makes it easy for us to conclude that the number of principal components to be used can be reduced to 8 by clearly showing the flatness at principal component 8. In addition, in Figure 3, we plotted the principal components against the proportion of variance, and we found that the first 8 principal components explain approximately 80% of the variance. Finally, the cumulative column of Table 2 also supports the findings presented in Figure 2 and 3 that the first 8 components account for 80% of the variation. Hence, we only select the first 8 principal components for this study.

![image](https://cloud.githubusercontent.com/assets/26909910/25407185/73cc6fb6-29d7-11e7-9562-610bd99705da.png)
![image](https://cloud.githubusercontent.com/assets/26909910/25407199/800964a0-29d7-11e7-875f-e4c0c55c4074.png)

![image](https://cloud.githubusercontent.com/assets/26909910/25407211/8afc59bc-29d7-11e7-8ce0-9cafeb1a4f01.png)
![image](https://cloud.githubusercontent.com/assets/26909910/25407298/d2c25a44-29d7-11e7-9225-cb7703ed5494.png)

![image](https://cloud.githubusercontent.com/assets/26909910/25407237/a14018ee-29d7-11e7-9cf1-26f567a9e320.png)
![image](https://cloud.githubusercontent.com/assets/26909910/25407248/a90e4988-29d7-11e7-9cfc-6926e9b68902.png)
