## Introduction:

This report explains the regression models for the home sale price of a defined sample population of houses using the housing data of Ames population from 2,930 observations between the year 2006 and 2010. There are a total of 82 variables – including 20 continuous, 23 nominal, 23 ordinal, and 14 discrete – involved in this study. For the purpose of this study I have limited the sample population to small family houses -- eliminating apartment complex, warehouses, and condominiums data.

Upon limiting the target sample population to the “typical” family houses, I split the dataset into two parts – train and test. I used 70% of sample data to train and 30% of sample data to test. After the train/test exercise, I used the automated variable selection techniques such as: Adjusted R-square, MaxR, Mallow’s Cp, forward, stepwise, and backward selection techniques, to test and compare the models’ attributes and performance based on different sets of variables. After selecting the variables, I computed the R-square, AIC, BIC, MSE, and MAE to determine which of the models fit the in-sample and out-of-sample data best. Finally, I assigned a grading matrix to grade the predictive accuracy of the models and determine material significance.

## Sample population:

The sample population for this study includes all small family houses that were built after year 1950, have a basement, have a gross living area square foot less than 800 sq. ft., consist of a paved driveway, doesn’t have a swimming pool, doesn’t have an irregular lot shape, are under a “normal” sale condition, and contain all public utilities. These features were defined for the purpose of this study to fit the requirement of a “typical” sample. This exercise aims to deduce the price of the type of house defined above, and were, hence, not included in the sample. 

I used the waterfall method in SAS to narrow down the population data to the given “typical” data set. The data output with excluded rows are presented below in Table 1 using waterfall technique in SAS. The waterfall exercise dropped my sample size to 1431 houses from the original pool of 2,930 observations. Meaning, about 45% of the houses did not qualify the “typical” house type required by the study. It is also important to note that SAS dropped 330 houses and named them “Missing” during the course of data. These houses are also not included in the sample data and left out for the purpose of this study as out-of-scope observations.

![image](https://cloud.githubusercontent.com/assets/26909910/25404979/c3b8632a-29cf-11e7-829d-14e2564a4400.png)

## Train/Split data for cross-validation:

Upon generating study-specific sample population based on the waterfall technique, I split the sample population into two categories – train and test. I used the 70% of sample observations data to train the data, and 30% of sample observations data to test the data. This exercise enabled me to cross validate the models, gauge their predictive accuracy for out of sample data, and identify the strength of models overall. There are many factors (variables) affecting the sale price of the houses in this study. Out of the 82 variables used in this data set, not every variable carries the same weight, some variables are more important than the others. Therefore, it is imperative to select appropriate variables to achieve the objective of the study. In order to run the train/test step in SAS, I had to make sure that all variables are in a format that SAS can read for the train/test process. Therefore, I transformed the nominal variable “CentralAir”, discrete variable “Fireplaces”, discrete variable “Garagecars”, and ordinal variables “Bsmtcond” and “Bsmtqual” into binary variables. The variables were then presented and analyzed using the train/test frequency table shown in Table 2 below.

![image](https://cloud.githubusercontent.com/assets/26909910/25405055/f761b492-29cf-11e7-8716-30db6806e4ff.png)
   #### Table 2: Train-Test Frequency Table

## Automated variable selection and Model Identification:

Even though we only have 82 variables in total and it is fairly feasible to manually pick the variables that seem to make the greatest impact, it is a good idea to leverage SAS tools and use the automated variable selection process to see how the variables impact the models, and cross validate the models and compare and contrast the models’ fit. Therefore, we used Adjusted R-square, MaxR, Mallow’s Cp, Forward, Stepwise and Backward selection techniques, and prepared a model based on each selection technique.

1.	Model_AdjR2 (Adjusted R-square Technique):

Computation of adjusted r-square aids the ability to make a decision on how many predictor variables to use in preparing a model. Adjusted r-squared also helps to make out-of-sample prediction, and accounts for the complexity of a model by comparing models of different sizes. I started off with using Proc reg to select the best 10 variables based on adjusted r-square selection technique. The output of the process is presented in Table 3. The best model without any criterion for adjusted r-square model, as shown in Table 3, has 12 variables and an adjusted r-square value of 0.8749, and r-square value of 0.8769. However, when I assign “start” and “stop” points of 3, and 8, respectively, the model changes its attributes. Table 4 below shows a detailed list of all possible models when I assign “start” and “stop” criterion to the adjusted r- squared selection technique. Based on the data in Table 4 below, the best model is the model with 8 variables that has an adjusted r-square value of 0.8713 and r-square value of 0.8727.


    Model_AdjR2: 
    train_response = Central_air Garage_ind GrLivArea TotalBsmtSF LotArea LotFrontage MasVnrArea
    YearBuilt GarageArea OverallQual OverallCond FullBath
    
![image](https://cloud.githubusercontent.com/assets/26909910/25405120/41bc1258-29d0-11e7-9329-fe62b4a402a7.png)
   #### Table 3: Ten best models using the Adjusted R-squared technique without specific criterion

![image](https://cloud.githubusercontent.com/assets/26909910/25405126/47811634-29d0-11e7-8c15-a4a049f18d6f.png)
   #### Table 4: Best model using the Adjusted R-squared technique with specific criterion

2.	Model_MaxR (MaximumR Technique):

Unlike the adjusted r-square variable selection technique, the maximumr selection technique, as insinuated by the name of the technique itself, searches for the maximum value of r and the optimum model. The maximumr technique starts with a single variable with maximum r- squared value, and adds additional variables increasing the value of the r-squared. The optimum value is determined by identifying the variables combination that produces the maximum value of r-squared. The maxr selection technique ran every single variable in steps 1 through 16, and after completing the step 16 – i.e. running all 16 variables, the technique produced the optimum model. The detail of the models including analysis of variance, parameter estimates, standard error, and F-value are presented in Table 5 below.

    Model_MaxR: 
    train_response = -1403425 + 371*good_basement_ind + 25512*central_air 
    + 800*fireplace_ind + (-11946)*garage_ind + 70*GrLivArea + 43*TotalBsmtSF + (-4)*LotArea
    + 63*LotFrontage + 36*MasVnrArea + 636*YearBuilt 
    + 41*GarageArea + 15232*OverallQual + 8903*OverallCond + (-12003)*FullBath
    
![image](https://cloud.githubusercontent.com/assets/26909910/25405267/cd88e694-29d0-11e7-8a03-fde177cd0b8e.png)

![image](https://cloud.githubusercontent.com/assets/26909910/25405272/d1788430-29d0-11e7-9eac-2a9788ede944.png)
   #### Table 5: ANOVA and Parameter Estimates model using the MaxR technique
   
3.	Model_MCp (Mallows’ CP):

Colin Lingwood coined Mallows’ CP, Mallows’ CP takes into account the mean square error of fitted value, and measures the bias that exist in the reduced model when compared to the full model. I used the output from Proc reg with CP selection technique and the start and stop criteria of 3 and 8 respectively to compute the best ten models. Table 6 below shows the output along with all ten models. Based on the output presented in Table 6, I deduced the following model from Mallows’ CP selection technique:

    Model_MCp: 
    train_response = GrLivArea TotalBsmtSF LotArea MasVnrArea YearBuilt GarageArea OverallQual OverallCond

![image](https://cloud.githubusercontent.com/assets/26909910/25405346/083a8d88-29d1-11e7-9d50-2b1594e29e03.png)
   #### Table 6: Ten best models using the Mallows’ CP selectin technique
   
4.	Model_F (Forward Selection Technique):

The forward selection model technique is one of the techniques under the broader umbrella of selection technique called “Greedy variable selection” technique. The forward selection technique uses a nested F-test to select the variables, and keeps adding variable to the model until the next variable doesn’t meet the pre-stated selection criteria (the SLENTRY parameter). I used the forward selection technique to select the variables and got for the output an ANOVA table and Parameter estimates with other indicators presented in Table 8 and a summary of forward selection procedure shown in Table 7. I used 0.15 as the SLENTRY parameter to perform this analysis. Upon performing the analysis presented in Table 8 and 7, I could deduce the following model as the best model from forward selection technique:


    Model_F: 
    train_response = -1465734 + 25738*central_air + 70*GrLivArea + 41*TotalBsmtSF 
    + 2*LotArea + 38*MasVnrArea + 664*YearBuilt + 38*GarageArea + 15304*OverallQual
    + 8808*OverallCond + (-12559)*FullBath

![image](https://cloud.githubusercontent.com/assets/26909910/25405429/3fd6d17a-29d1-11e7-9e7a-205926dc5b5f.png)
   #### Table 7: Summary of Backward variable selection process

![image](https://cloud.githubusercontent.com/assets/26909910/25405449/54a65454-29d1-11e7-8a04-626df2892c33.png)
   #### Table 8: ANOVA and Parameter Estimates model using the Forward technique
   
5.	Model_B (Backward Selection Technique):

Similar to the Forward selection technique discussed above, backward selection technique also falls under the broader variable selection technique called “Greedy variable selection” technique. However, the selection in this technique, as the name suggests, is backward.
Meaning, the method begins computing by selecting all predictor variables, and eliminates the variables (one at a time) until the predetermined condition is met (i.e. the SLSTAY value). I used a SLSTAY value of 0.1 to compute and select variables using the backward selection technique. The output is presented in Table 9 and 10. Table 8 shows the ANOVA table and Parameter estimates, and Table 10 shows the summary of backward selection process and the associated variables. Using the output from this analysis, I deduced the following model:

    Model_B: 
    train_response = -1465734 + 25738*central_air + 70*GrLivArea + 41*TotalBsmtSF 
    + 2*LotArea + 38*MasVnrArea + 664*YearBuilt + 38*GarageArea + 15304*OverallQual 
    + 8808*OverallCond + (-12559)*FullBath
    
 
![image](https://cloud.githubusercontent.com/assets/26909910/25405523/8f4e2122-29d1-11e7-81dc-aa68018b34ff.png)
   #### Table 9: ANOVA and Parameter Estimates model using the backward technique

![image](https://cloud.githubusercontent.com/assets/26909910/25405557/aa590266-29d1-11e7-88c4-6c4ed0fb8555.png)
   #### Table 10: Summary of Backward variable selection process
   
6.	Model_S (Stepwise Selectin Technique):

The third leg of the broader “Greedy Variable Selection” technique is Stepwise selection technique. The stepwise selection technique uses a similar assessment and selection technique but differs in a way that the stepwise method requires two criteria entry, SLSTAY and SLSENTRY – one for the entrance and the other for the removal of the variables. The inter-correlation between the predictor variables influence the order of entry and removal. I used SLSTAY value of 0.1 and SLENTRY value of 0.5 (similar to the ones used in forward and backward selection) to compute the F-statistic for stepwise selection technique. Table 12 shows the ANOVA table and parameter estimates for stepwise selection and Table 11 shows the summary of the stepwise selection process and variables used in the process. Using the output from this analysis, I deduced the following model for the stepwise selection technique.

    Model_S: 
    train_response = -1465734 + 25738*central_air + 70*GrLivArea + 41*TotalBsmtSF 
    + 2*LotArea + 38*MasVnrArea + 664*YearBuilt + 38*GarageArea + 15304*OverallQual
    + 8808*OverallCond + (-12559)*FullBath
    
 ![image](https://cloud.githubusercontent.com/assets/26909910/25405832/95a2f448-29d2-11e7-9e60-e3c4558d6c10.png)
   #### Table 11: Summary of Stepwise variable selection process

![image](https://cloud.githubusercontent.com/assets/26909910/25405838/9b03a86a-29d2-11e7-9180-c962d06390f9.png)
   #### Table 12: ANOVA and Parameter Estimates model using the stepwise technique
   
## Analysis of Models and comparison of output:

All of the greedy variables selection methods (Forward, Backward, and Stepwise) produced	the	same		optimum	model	[i.e.	(train_response	=		-1465734		+ 25738*central_air + 70*GrLivArea + 41*TotalBsmtSF + 2*LotArea + 38*MasVnrArea + 664*YearBuilt + 38*GarageArea + 15304*OverallQual + 8808*OverallCond + (- 12559)*FullBath)]. In the metrics variable selection methods, however, the Adjusted R-squared selection method and Mallows’ CP produced same optimum model [i.e. (train_response = GrLivArea TotalBsmtSF LotArea MasVnrArea YearBuilt GarageArea OverallQual OverallCond)], and MaxR selection method produced a  different  optimum		model			[i.e.		(Model_MaxR:			train_response		=		-1403425		+ 371*good_basement_ind			+		25512*central_air		+	800*fireplace_ind	+	(- 11946)*garage_ind	+		70*GrLivArea		+		43*TotalBsmtSF	+	(-4)*LotArea		+ 63*LotFrontage		+		36*MasVnrArea	+     636*YearBuilt     +     41*GarageArea     + 15232*OverallQual + 8903*OverallCond + (-12003)*FullBath)]. The MaxR selection method introduced the “good_basement_ind” predictor variable that was excluded  by all other selection methods. The MaxR is the only variable selection method that included all of the 16 variables, all other methods ruled out the “good_basement_ind” variable in their optimum models.

## Predictive accuracy using adjusted R-squared, AIC, BIC, MSE, and MAE computation of each model:

Now that I have identified optimum models for each selection method, I could group the ones that have same optimum models into one group. Therefore, we get the following model group after grouping the ones with same optimum model from the six models above:

    MODEL – 1 = Model_AdjR & Model_MCp 
    MODEL – 2 = Model_F + Model_B + Model_S 
    MODEL – 3 = Model_MaxR

In order to verify the predictive accuracy of the three models above, I calculated R- square, AIC, BIC, MSE and MAE for each of the three models. 

***Model - 1:*** Table 13 and 14 below show Adjusted R-squared, AIC, and BIC for Model_AdjR and Model_MCp, both of which has the same set of predictor variables.


![image](https://cloud.githubusercontent.com/assets/26909910/25405973/15de4af4-29d3-11e7-9588-cd9eb2156ddb.png)
   #### Table 13: Adjusted R-squared, AIC, and BIC for Model - 1

![image](https://cloud.githubusercontent.com/assets/26909910/25405984/232ba530-29d3-11e7-87ff-fdd1490c32f9.png)
   #### Table 14: MAE and MSE for Model-1 and test sample

***Model – 2:*** Table 15 and 16 below show Adjusted R-squared, AIC, and BIC for Model_F, Model_B and Model_S, all of which have the same set of predictor variables.

![image](https://cloud.githubusercontent.com/assets/26909910/25406056/76ed1910-29d3-11e7-95b9-7d568695bbfe.png)
   #### Table 15: Adjusted R-squared, AIC, and BIC for Model - 2

![image](https://cloud.githubusercontent.com/assets/26909910/25406063/7baecb42-29d3-11e7-8d69-f905b0620a67.png)
   #### Table 16: MAE and MSE for Model-2 and test sample


***Model – 3:*** Table 17 and 18 below show Adjusted R-squared, AIC, and BIC for Model_MaxR.

![image](https://cloud.githubusercontent.com/assets/26909910/25406069/7fa764f2-29d3-11e7-8cdd-5f53448c7fbd.png)
   #### Table 17: Adjusted R-squared, AIC, and BIC for Model - 3

![image](https://cloud.githubusercontent.com/assets/26909910/25406073/84ddda1e-29d3-11e7-9221-390f9cb9b637.png)
   #### Table 18: MAE and MSE for Model-3 and test sample

Based on the output from Table 13-Table 18, despite Model-3 having the lowest AIC and BIC, and highest Adjusted R-squared and R-square, I would like to pick Model-2 (i.e. the group of Model_F, Model_B, and Model_S) as the optimum model. Model-2 seems to fit both training and test data well with very less discrepancy between the two. Between the three models, Model-2 demonstrated an overall goodness-of-fit and optimum variable selection.

## Multicollinearity for Chosen Model (i.e. Model 2):

As shown in Table 19 below the predictor variable with higher VIF has a VIF of 3.28 (which is less than 10); therefore, there is no multicollinearity in the chosen optimum model (i.e. Model-2).

![image](https://cloud.githubusercontent.com/assets/26909910/25406317/445eb12e-29d4-11e7-9fa0-60ea0d31f0f0.png)
   #### Table 19: Parameter Estimates of Model – 2 (optimum model)
   
## Multicollinearity for Model-1 & Model-3:

As presented in Table 20 and 21 below none of the variables in both tables have a  VIF greater than 10; therefore, there is no issue of multicollinearity in any of the above six models.

![image](https://cloud.githubusercontent.com/assets/26909910/25406379/74d9458a-29d4-11e7-9845-45098cf39302.png)
   #### Table 20: Parameter Estimates of Model – 1 (Model_AdjR & Model_MCp)

![image](https://cloud.githubusercontent.com/assets/26909910/25406392/7bab943a-29d4-11e7-935e-cc7bf2919549.png)
   #### Table 21: Parameter Estimates of Model – 3 (Model_MaxR)
   
## Operational Validation:

About 64% of the data, as shown in the Table 22 below, were in Grade 1, which means that from the 100% of the predicted data about 64% of the predicted values were within the 10% of the actual value. Similarly, about 82% of the predicted values were within the 15% of the actual values. Therefore, the developed model  and selected variables proved to be a fairly accurate prediction of the actual values.

![image](https://cloud.githubusercontent.com/assets/26909910/25406498/d98e56dc-29d4-11e7-8e85-6f8bcc0f0cac.png)
   #### Table 22: Operational Prediction Validation via Grade for Model 2 (optimum model)

## Summary:

I started with narrowing down the population data to sample data that only  included what was needed to accomplish the original objective, i.e. to predict the  sale price of a typical single-family house. I then used different automated variables selection methods to select the optimum variables. Upon testing different variables on different models, I was able to decide on Model 2 – a combination of all three Greedy variable selection methods – as the optimum model. After deciding the optimum model, I checked for multicollinearity, and ensured that the model was  free of multicollinearity. Finally, I proved the statistical and material (business) significance of the model by grading the predicted values against the actual values. Therefore, the Model 2 is a very useful model for the business to rely on in order to make important decisions.
