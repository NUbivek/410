## Introduction:

This report explains the regression models for the home sale price of a defined sample population of houses using the housing data of Ames population from 2,930 observations between the year 2006 and 2010.  There were a total of 82 variables – including 20 continuous, 23 nominal, 23 ordinal, and 14 discrete – involved in this study.

For the purpose of this study I have limited the sample population to small family houses -- eliminating apartment complex, warehouses, and condominiums data. There are many factors affecting the sale price of the houses in this study. However, I will be taking two major predictor variables – GSF of living area above the ground level, and GSF of the basement – to build the regression models for the home sale price. I used the goodness of fit (GOF) using the output from SAS. I, then, compared the simple and multiple regression models. In conclusion, based on my analysis, I was able to deduce the model that worked the best for our response variable (y). 


## Sample population:

The sample population for this study includes all small family houses that were built after year 1950, have a basement, have a gross living area square foot less than 800 sq. ft., consist of a paved driveway, doesn’t have a swimming pool, doesn’t have an irregular lot shape, are under a “normal” sale condition, and contain all public utilities. These features were defined for the purpose of this study to fit the requirement of a “typical” sample. This exercise aims to deduce the price of the type of house defined above, and were, hence, not included in the sample. I used the waterfall method in SAS to narrow down the population data to the given “typical” data set. The data output with excluded rows are presented below in Table 1 using waterfall technique in SAS. The waterfall exercise dropped my sample size to 1431 houses from the original pool of 2,930 observations. Meaning, about 45% of the houses did not qualify the “typical” house type required by the study. It is also important to note that SAS dropped 330 houses and named them “Missing” during the course of data. These houses are also not included in the sample data and left out for the purpose of this study as out-of scope observations.

![image](https://cloud.githubusercontent.com/assets/26909910/25399075/32f3b208-29bc-11e7-9f42-7a1813724fcf.png)
   #### Table 1: A detailed list of drop conditions to deduce the Sample size.

## Predictor variables:

This study now have four key variables that will help determine the Sale Price of the houses that are a part of the study. Therefore, the correlation coefficients of four continuous predictor variables – First Floor SF, Living area SF, Basement SF, and Lot Area SF – and one discrete variable – Year built – with sale price is computed using Pearson product-moment correlation coefficient in SAS. The correlation coefficients helped identify the linear relationship between the response variable (Y) – Sale Price – and regressor variables (Xi). An illustration of the correlation coefficient table validating above findings is presented in Table 2. In addition, the linear relationship between the regressor and each response variable is shown with the help of scatter plots in figure 1, 2, 3, 4, and 5.

![image](https://cloud.githubusercontent.com/assets/26909910/25399300/00bd4b36-29bd-11e7-8540-7a1611d6f331.png)
   #### Table 2: Correlation coefficients for potential predictor variable with sale price.
   
Table 2 above indicates that the general living area (GrLivArea) regressor variable has the highest correlation of 0.80906, and the total basement area (TotalBsmtSF) has the second highest correlation of 0.62147 with the response variable (SalePrice). Due to the strength of the correlation between the two regressor variables and the response variable, the general living area and total basement area are chosen as two predictor variables for this study.

As stated above, the data in the Table 2 is plotted in scatter plot to get an overall understanding of the situation. Plotting the data in the scatter plot helps the analysts to understand the extent of correlation and spread of data of the variables in the group.

![image](https://cloud.githubusercontent.com/assets/26909910/25400061/6f877724-29bf-11e7-9f4d-6443bca96fb9.png)
   #### Figure 1: Scatter Plot of correlation between sale price and first floor area 

![image](https://cloud.githubusercontent.com/assets/26909910/25400101/89d25c66-29bf-11e7-84eb-fbd7b2ed5acc.png)
   #### Figure 2: Scatter Plot of correlation between sale price and general living area 
   
![image](https://cloud.githubusercontent.com/assets/26909910/25400225/ea0f4cc4-29bf-11e7-9d38-a3c301bdf81b.png)
   #### Figure 3: Scatter Plot of correlation between sale price and lot area 
   
![image](https://cloud.githubusercontent.com/assets/26909910/25400282/04b73c80-29c0-11e7-88ae-29fdd13d09b8.png)
   #### Figure 4: Scatter Plot of correlation between sale price and year the house was built 
   
![image](https://cloud.githubusercontent.com/assets/26909910/25400313/1e879e3e-29c0-11e7-84ca-555598c97e58.png)
   #### Figure 5: Scatter Plot of correlation between sale price and total basement area 
   
## Linear Regression Models:

### Model I: Simple linear regression model (General Living Area as Predictor)

![image](https://cloud.githubusercontent.com/assets/26909910/25400410/78214864-29c0-11e7-919c-136768bf94c7.png)
   #### Figure 6: Regression line between sale price and general living area 

I used scatter plot to fit the data to the simple regression model in Figure 6. The single linear regression model of the response variable SalePrice and the predictor variable general living area (GrLivArea) above indicates that the majority of the houses in the sample are below 30,000 sq. ft.. Table 3 below shows the Analysis of Variance (ANOVA) and Goodness-Of-Fit (GOF) of the simple linear regression model above. The ANOVA table below confirm that the above predictor variable – General living area – is a strong predictor to explain the variation and hence predict the response variable – SalePrice -- with an overall F test of regression effect and p-value less than 0.0001. In addition, Table 3 also shows the Goodness-Of-Fit (GOF) with R-square value of 0.6546; meaning that the predictor variable general living area is able to explain about 65% of variance in the response variable sale price.

![image](https://cloud.githubusercontent.com/assets/26909910/25400511/dad9e772-29c0-11e7-8113-798debc5c0e6.png)
   #### Table 3: ANOVA, GOF, Coefficient of Variance with Parameter Estimates Table

![image](https://cloud.githubusercontent.com/assets/26909910/25400542/f105892a-29c0-11e7-8c9a-b9fa45ce05a6.png)
   #### Figure 7: Scatter Plot of Residual vs. Predicted Value 
   
Upon drafting the ANOVA and GOF, I plotted the residuals against the predicted value in a scatter plot. The scatter plot analysis of residual and predicted value yielded in a bow shape pattern. The bow shape indicates the proportion between 0 and 1 -- as shown in above figure 7, and states that the predicted value does not validate the homoscedasticity assumption. This refutation of the validation demands for a transformation application.

Plotting the residuals in a Q-Q plot further tests the model. The Q-Q plot shows some deviation from the normality assumption. However, the Q-Q plot also shows evidences of the outliers that disproportionately affect the validity of the model. Therefore, despite the refutation of the validation shown in Figure 8, it is worthwhile to develop the regression model. Hence, based on the parameter estimates from Table 3, I can deduce the model to be the following:

     Model I Simple Regression Model: 
     Sale Price = 8850.43758 + 122.05274 * General Living Area
      
     (Where: Sale Price= Y, B0=8850.43758, B1=122.05274, and General Living Area = X)


### Model II: Simple linear regression model (Total Basement Area as Predictor)

As described above in the introduction section, we use the second predictor variable – total basement area – to develop a second model. Figure 8 below shows a positive correlation between the two variables, and the subsequent Table 4 shows the ANOVA, GOF, and Parameter estimates.

![image](https://cloud.githubusercontent.com/assets/26909910/25400911/11c3cb3a-29c2-11e7-87a3-ecedf0fe87d7.png)
   #### Figure 8: Regression line between total basement size and sale price 

![image](https://cloud.githubusercontent.com/assets/26909910/25400936/2aa43dd8-29c2-11e7-80a4-be6428444a6d.png)
   #### Table 4: ANOVA, GOF, Coefficient of Variance, and Parameter estimates Table

The above Table 4 also confirms what we identified in Model I development process, that the overall F test for regression effect and the p-value is less than 0.0001. This data validates that the second predictor variable – Total basement square footage -- is also a strong predictor in explaining the variation of sales price. In addition, the table also shows the GOF with R-square of 0.3862, showing about 38% of variation in sale price by the Total basement square footage.

Upon deriving the coefficient of variance, ANOVA table, GOF and Perimeter estimates, the model is further analyzed with the help of residuals for sale price.

![image](https://cloud.githubusercontent.com/assets/26909910/25400965/471f3968-29c2-11e7-8398-d6e5bd9ee980.png)
   #### Figure 9: Scatter Plot of Residual vs. Total basement square footage 

It is evident in the scatter plot above that the residual has less of a pattern when compared to the residual in model. Nevertheless, the plot still shows a funnel like pattern, which indicates that the variance is an increasing function of y and hence, does not confirm the homoscedasticity assumption above. The plot supports the initial idea and the need for some form of transformation. However, similar to the tests in Model I, it is helpful to analyze the Q-Q Plot of Residuals for Sale Price against the total basement square footage in addition to the scatter plot of residuals for sale price. Upon plotting in a Q-Q plot I am able to decipher that the model has outliers that impacted the scatter plot above. Therefore, it is still worth to build the model.

![image](https://cloud.githubusercontent.com/assets/26909910/25401002/6887b9c2-29c2-11e7-8be0-d7d0a09c59dd.png)
   #### Figure 10: Q-Q Plot of Residuals for sale price
   
Hence, based on the parameter estimates from Table 4, I can deduce the Model II to be the following:

        Model II Simple Regression Model: 
        Sale Price = 59189 + 120.51837*Total Basement Area
        
        (Where: Sale Price= Y, B0=59189, B1=120.51837, and Total Basement Area = X)

### Model III: Multiple Linear Regression Model (General Area & Total Basement Area)

In order to generate a multiple regression model involving general area and total basement area as the predictor variables to predict the response variable, the two predictors need to be combined. Table 4 below shows a detailed breakdown of the ANOVA analysis, GOF test, Coefficient of variance, and parameter estimates for the combined predictor variables. The ANOVA result in a similar overall F test for regression effect and the p-value of <0.0001 as indicated in previous individual ANOVA analyses. This indicates that the general living area and basement square footage combined are also strong predictors in explaining the variation in sales price. Due to the misleading nature of R-square in situation such as this one, it is imperative that adjusted R squared be considered as an additional checkpoint. Table 5 shows the R square value per of 0.7653, which means that the 76% of the variation in sales price is explained by model with two predictor variables combined. 

![image](https://cloud.githubusercontent.com/assets/26909910/25401068/a50af68e-29c2-11e7-9bc1-3da93272a15f.png)
   #### Table 4: ANOVA, GOF, Coefficient of Variance, and Parameter estimates Table

Hence, the multiple regression model based on the above table 5 can be deduced as:

      Model III Multiple Regression Model: 
      Sale Price = -38516 +100.84822 * General Living Area + 70.13335*Total Basement Area
      
      (Where: Sale Price= Y, B0=-38516, B1=100.84822, B2=70.13335, General Living Area=X1and Total Basement Area = X2)

It is important to note in here that the multiple linear regression model fit better than the simple linear regression models in this instance. As stated above in individual analysis sections for each models, the overall F-test, R squared, and Root mean squared error for each model indicate the fit of the model. For example, the R-squared of the multiple linear regression above is 0.7656, and as discussed above, it implies a tentative 76% variation in sales price; whereas, the individual models resulted in 38% and 65% variation in sales price. However, it is also pivotal to iterate that this might not always be the case. More predictor variables don’t necessarily mean a better fit. Therefore, it is always important to go through the exercise of adopting different methods and techniques to double and triple check the fit options using the tools discussed here.

## Outlier Identification

As an experiment, I am dropping additional outliers from the sample population defined earlier in this report. Below are the two additional criteria I’ve set to drop the additional outliers.

1.	General living area square footage greater than 3000: I am dropping the houses with greater than 3000 square footage because, as shown in Figure 9, there aren’t many houses over 3000 square footage, and the ones that are over 3000 square footage has disproportionally skewed the result of the model. Therefore, it is safe to assume that the model is going to depict the sales price of the houses more accurately if these outliers were to be dropped.

2.	Total basement area square footage greater than 2000: Similar to the bullet number 1 where the houses with above 3000 square footage were dropped, the houses with the total basement area greater than 2000 can also be dropped for the same reason i.e. there aren’t many houses with over 2000 square footage in basement area, and the model is going to be more accurate if these outliers were to be transformed using Log where the distribution is usually closer to normality. 

## Model comparison after and before log transformation:

### Model IV: Multiple Linear Regression Model (General Living Area)

The log transformation of the sales price is now used to construct a simple linear regression model using the general area as predictor variable. Figure 11 shows the scatter plot of the log price and general living area.

![image](https://cloud.githubusercontent.com/assets/26909910/25401177/033e25a0-29c3-11e7-8bde-991eebd51508.png)
   #### Figure 11: Regression line between log sale price and general living area

In addition, ANOVA, GOF, Coefficient of Variance, and Parameter estimates analyses are conducted and the results are presented in Table 5 below. The below table show that the R square value for model IV is 0.6912, which is higher than model I.  Hence, the increase in the value of R square, along with other indicators (overall F-test and MSE) indicates that model IV is a better fit than model I. 

      Model IV:
      Log (Sale Price) = 11.2797+0.000555987 * General Living Area
      
      (Where: log (Sale Price)= Y, B0=11.2797, B1=0.000555987, General Living Area=X)

![image](https://cloud.githubusercontent.com/assets/26909910/25401255/3fedae12-29c3-11e7-83e9-b020c6c2f87f.png)
   #### Table 5: ANOVA, GOF, Coefficient of Variance, and Parameter estimates Table
   
Model IV: Simple Linear Regression Model (Total Basement Area)

The log transformation of the sales price is used again to construct a simple linear regression model using the total basement area as predictor variable. Figure 12 shows the scatter plot of the log sale price and total basement area.

![image](https://cloud.githubusercontent.com/assets/26909910/25401302/64d17a24-29c3-11e7-8d6b-f4d88b0c0fa4.png)
   #### Figure 12: Regression line between log sale price and total basement area
   
Similar to the model IV, ANOVA, GOF, Coefficient of Variance, and Parameter estimates analyses are conducted and the results are presented in Table 6 below. The below table show that the R square value for model V is 0.3513, which is higher than model II.  Hence, the increase in the value of R square, along with other indicators (overall F-test and MSE) indicates that model V is a better fit than model II. 

![image](https://cloud.githubusercontent.com/assets/26909910/25401400/7f2263ac-29c3-11e7-8a32-99c6f94a779e.png)
   #### Table 6: ANOVA, GOF, Coefficient of Variance, and Parameter estimates Table
   
      Model V:
      Log (Sale Price) = 11.54817+0.00001844 * Total Basement Area
      
      (Where: log (Sale Price)= Y, B0=11.54817, B1=0.00001844, Total Basement Area =X)

### Model VI: Multiple Linear Regression Model with Log Sales Price
   #### (General Area & Total Basement Area)

In order to generate a multiple regression model with the transformed log sale price involving general area and total basement area as the predictor variables to predict the response variable, the two predictors need to be combined. Table 7 below shows a detailed breakdown of the ANOVA analysis, GOF test, Coefficient of variance, and parameter estimates for the combined predictor variables, and log sales price.

![image](https://cloud.githubusercontent.com/assets/26909910/25401483/be85c340-29c3-11e7-977c-5c7cf25a9fd3.png)
   #### Table 7: ANOVA, GOF, Coefficient of Variance, and Parameter estimates Table


Therefore, the multiple regression model for log sale price can be deduced as:

      Model VI Multiple Regression Model: 
      Sale Price = 11.06629 + 0.00047674* General Living Area + 0.00027493 *Total Basement Area
      
      (Where: log (Sale Price)= Y, B0=-11.06629, B1=0.00047674, B2=0.00027493, General Living Area=X1and Total Basement Area = X2)

The log sale price multiple linear regression model fit better than the two log sale price simple linear regression models. As previously stated in the regular (not transformed version), individual analysis sections for each models, the overall F-test, R squared, and Root mean squared error for each model indicate the fit of the model. And just as the regular not transformed version, the R-squared of the multiple linear regression had the highest variation in sales price. Not only the multiple linear regression of log sale price out run the individual simple linear regression models with log sale prices, the multiple linear regression of log sale price outstripped all models above, including the regular multiple regression model. 


## Conclusion

A series of activities were performed in this study to identify a model that would best fit the data. After analyzing the individual simple regression model of the two major predictor variables – General living area and total basement area – a multiple linear regression model was prepared by combining the two predictor variables. The analyses led to curtail the extreme outliers from the model, and improvise the model by focusing on the typical houses defined in the sample. A log sales price was then computed and simple individual linear regression were calculated to fit the two predictor variables with log sale prices. Finally, a multiple linear regression of log sale price was computed by combining the two predictor variables. Upon pursuing all the steps described above, I was able to conclude that the multiple linear regression with log prices was the best fit model. Therefore, I would use the multiple regression with log prices model (Model VI) to predict the sale price of the typical houses in the given area of Ames, Iowa.

Log transformation are, in general, very helpful to make the highly skewed data sets, comparatively less skewed. As shown in the examples above, the log transformation helps to better utilize the data by getting rid of the noise (outliers) and focusing on the area where the majority of data lies. Therefore, it is very helpful to make the data interpretable and usable in real life scenario. There are times when one might consider to log transform the predictor variables instead of the response variable; however, these situations are rare and occur only when non-linearity is the only problem. Among the assumptions, when all assumptions are met but non-linearity is not (which is rare) log transformations of the predictor variable might fix the issue. Therefore, it is a rare situation but comes in handy when all other doors are shut.


