## Introduction

This report addresses the issue of multicollinearity by using the concept of Principal Component Analysis (PCA). PCA is used as a technique to reduce the dimension and remediate the issue of multicollinearity in OLS regression. Multicollinearity exists when there are non-linear dependencies among the regressors. As a part of this report, we will analyze the stock portfolio dataset that has a total of 502 observations for 20 company stocks and a Vanguard index fund (VV). The dataset is continuous; however, in order to perform a detailed analysis of the data, we need to first perform a data wrangling exercise to ensure that the dataset is accurate and appropriate for the desired use.

## Log return:

We compute the log return of today’s stock price to the yesterday’s stock price. This exercise helps us to use the log-returns of individual stocks as a tool to explain the variation in log- returns of the index fund. This helps us to understand the security returns overall. In addition, log transformation is used to stabilize the variance.

## Correlation between the 20 individual stocks and market index with visualization:

We leveraged the PROC CORR in SAS to identify correlation between each individual stocks and the market index fund. Table 1 below shows the SAS output of the correlation. As indicated by the Table 1 below, all of the 20 variables have a positive correlation with the market index. The two stocks with highest correlation R values are “HON” and “MMM” – they have the R value of approximately 0.76. DPS seems to be the stock with lowest R value (approximately 0.44).

![image](https://cloud.githubusercontent.com/assets/26909910/25407078/fa5c74c8-29d6-11e7-9f05-98f4cadd139f.png)
