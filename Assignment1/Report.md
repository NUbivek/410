## Introduction:

This report explains the regression models for the home sale price of a defined sample
population of houses using the housing data of Ames population from 2,930 observations
between the year 2006 and 2010. There were a total of 82 variables – including 20 continuous,
23 nominal, 23 ordinal, and 14 discrete – involved in this study.

For the purpose of this study I have limited the sample population to small family houses --
eliminating apartment complex, warehouses, and condominiums data. There are many factors
affecting the sale price of the houses in this study. However, I will be taking two major predictor
variables – GSF of living area above the ground level, and GSF of the basement – to build the
regression models for the home sale price. I used the goodness of fit (GOF) using the output
from SAS. I, then, compared the simple and multiple regression models. In conclusion, based on
my analysis, I was able to deduce the model that worked the best for our response variable (y).

## Sample population:

The sample population for this study includes all small family houses that were built after year
1950, have a basement, have a gross living area square foot less than 800 sq. ft., consist of a
paved driveway, doesn’t have a swimming pool, doesn’t have an irregular lot shape, are under a
“normal” sale condition, and contain all public utilities. These features were defined for the
purpose of this study to fit the requirement of a “typical” sample. This exercise aims to deduce
the price of the type of house defined above, and were, hence, not included in the sample. I used
the waterfall method in SAS to narrow down the population data to the given “typical” data set.

The data output with excluded rows are presented below in Table 1 using waterfall technique in
SAS. The waterfall exercise dropped my sample size to 1431 houses from the original pool of
2,930 observations. Meaning, about 45% of the houses did not qualify the “typical” house type
required by the study. It is also important to note that SAS dropped 330 houses and named them
“Missing” during the course of data. These houses are also not included in the sample data and
left out for the purpose of this study as out-of scope observations.

![image](https://cloud.githubusercontent.com/assets/26909910/25399075/32f3b208-29bc-11e7-9f42-7a1813724fcf.png)
   ### Table 1: A detailed list of drop conditions to deduce the Sample size.

## Predictor variables:

This study now have four key variables that will help determine the Sale Price of the houses that
are a part of the study. Therefore, the correlation coefficients of four continuous predictor
variables – First Floor SF, Living area SF, Basement SF, and Lot Area SF – and one discrete
variable – Year built – with sale price is computed using Pearson product-moment correlation coefficient in SAS. The correlation coefficients helped identify the linear relationship between
the response variable (Y) – Sale Price – and regressor variables (Xi). An illustration of the
correlation coefficient table validating above findings is presented in Table 2. In addition, the
linear relationship between the regressor and each response variable is shown with the help of
scatter plots in figure 1, 2, 3, 4, and 5.

