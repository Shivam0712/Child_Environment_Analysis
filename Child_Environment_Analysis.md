# Impact analysis of child's environment on school performance in SAT.

## Introduction:

There is a known connection between school performance and the environment that a child is exposed to, including environmental conditions that may affect health, exposure to violence which affects stress level, and socioeconomic features, including income, which may determine the ability of a student to get help. Nonetheless, the modeling of school performance is difficult, as measures of performance may be biased and environmental features hard to measure.

In spite of that, in this notebook we attempt to model performance, measures through the SAT score, of NYC students as a function of exposure to crime, measured through reports of crimes in school, living conditions, measured through the incidence of respiratory and drug related issues in the area, and optionally income.

The analysis is at the PUMA level. All data are accessible through NYC open data, the NY state open data portal (NY.gov).

**Figure : Distribution plot of Major Crimes and Average Major Crimes in Schools**
1. In the above plot the left distribution shows the distribution of major crimes in schools and the right distribution shows the average of major crimes in schools.
2. In the left distribution, both 25 percentile and 75 percentile line lies at zero showing number of major crimes in most of the school is 0 and in only few schools it is more than 0.
3. In the right distribution the mean line at 0.2 shows the average number of major crimes in schools is about ~0.2.

**Figure: Plot of school's SAT math score and SAT overall average score as function of crime statistics.**
1. The above 4 plots shows school's SAT math and SAT avg. vs number of major crimes and avg. number of major crimes in schools.
2. As we can see in the above plots, as number of major crimes is increasing the range of SAT scores is decreasing with fairly same mean.
3. The above plots show a non-linear relationship between SAT scores and Major crimes.
4. As number of average major crimes increases the SAT scores are fairly above 400. A linear relationship is still tough here.
5. The distribution of both SAT scores across both crime statistics are almost similar signaling high collinearity between variables.

**Figure: Locations of Schools in New York City**
1. The above plot shows locations of all the schools we have in our data for Crime and SAT Score.
2. As we can see in the plot the schools are distributed across the whole city.

**Figure: Choropleth showing locations of schools and hospital facilities across different PUMA's of NYC**
1. The above figure shows different polygons of PUMA's in NYC and the orange and blue dots shows locations of schools and hospital facilities respectively.
2. The schools and hospitals are fairly distributed across PUMA's and are not concentrated in specific regions.
3. Few PUMA's does not have either hospital facilities or schools or both. Thus, we will loose some PUMA's when we join all the data.

**Model and Figure: Puma avg. overall score in SAT vs puma avg. math score in SAT**
1. The above plot shows the puma avg. score in SAT overall compared against puma avg. score in math with a best fit line obtained from the model above.
2. From the plot we can see there is a high linear collinearitry between both the variables.
3. The collinearity is further supported by the best fit line and model which is able to expalin 99% variation(R-Square) in overall score using the math score.
4. the coefficient of 0.9674 without intercept shows that the correlation between the variable is very strong.

**All the numbers in the above plot are PUMA level average of schools parameters in the particular feature**
**Figure: Plots to show relations of PUMA's average SAT scores in schools with PUMA's average crime statistics in schools.**
1. The above plots show relations of PUMA's average SAT scores in schools( Maths score and overall average) with PUMA's average crime statistics in schools ( Number of Major Crimes, Average number of Major Crimes and Average Number of Non-criminal crimes).
2. As we can see in left 2 columns of plot we have a weak linear relation where the scores increases with increase in crime statistics(Avg. Major Crimes and avg. Non-Criminal Crimes).
3. It is hard to describe relation of SAT scores and Number of major crimes.

**All the numbers in the above plot are Puma level average of schools parameters in the particular feature**
**Figure: Plots to show relations of PUMA's average SAT scores in schools with PUMA's average asthma and drugs ratio.**
1. The above plots show relations of PUMA's average SAT scores ( Maths score and overall average) in schools with PUMA's average discharge statistics( ratio of asthma related discharge and ratio of drugs related discharge).
2. As we can see in left column of plot we have a weak negative linear relation where the scores decreases with increase in asthma ratio statistics.
3. It is hard to describe relation of SAT scores and drug ratio.

**Figure: Covariance matrix of all features in School dataset**

1. The above plot shows the covariance of all statistics in school data, each cell represents the correlation between the variables reflected by its row position and column positions.
2. As can be seen in the above plot, avg. of crime statistics have very strong correlation amongst them. Thus, for modelling only few of the relevant features amongst these should be used.
3. SAT scores and avg. crime statistics have positive yet weak correlations.

**Figures: Choropleths showing distribution of different features by PUMA.**

1. The above 7 choropleths shows the distribution of 2 SAT score features(SAT MAth And SAT Overall Average), 3 crime features( No.of major crimes in schools, Avg. no.of major crimes in schools and No. of non criminal crimes in schools) and 2 discharge features( Ratio of Asthma related cases and Ratio of Drugs related cases) by PUMA.

2. As can be seen in the top 2 choropleths, they look almost similar due to high corelation between SAT math score and SAT overall average scores. Middle Staten Isalnd peaks in both the scores and Bronx lacks the most.

3. In the middle row, again all the 3 choropleths showing crime statistics look similar with avg. of avg. major cimes in school and avg. of non criminal crimes in school peaking in Queens near jackson hieghts, and avg. of major crimes in school peaking in greenwich village. Lower Staten Island and bronx lacks in each of the 3 features.

4. The bottom 2 choropleths showing discharge statistics are fairly dissimilar to each other. Ratio of Asthma related cases peaks in bottom Bronx and ratio of Drugs related cases peaks in bottom staten island.

5. It is difficult to establish similarity across the rows of above choropleths, as each row shows choropleths of different type of features which are uncorrelated to each other.

**Model Results:**
1. From the summary of the above linear model, the R2 shows that crime related variables are able to describe 49% variation in the SAT Math Score.
2. None of the feature shows a strong performance in explaining the variation in SAT score as all the features have high p-value. The lowest p-value is for MajorN showing that at best, this can be a feature which can explain some variation in SAT score with significance.
3. The highest and lowest coefficient are for number of property crimes and number of other crimes as -1.88429 and 2.4117. The interpretation of these score means that for a unit deviation in number of property crimes there is a deviation in SAT math score equal to -1.88429 times the standard deviation of SAT math score. Similarly for a unit deviation in number of other crimes a deviation in SAT math score equal to 2.4117 times the standard deviation in SAT math score . But, as these 2 variable does not have a significant p-value scores, these realtions cannot be considered as statistically significant relations.

**Model Results:**
1. The addition of asthmaRatio and drugRatio features in the prior linear model have improved the model's capability to explain the variation in SAT math score and has increased to 65%( R2 improved from 0.49 to 0.654).
2. The adjusted R2 has also improved from 0.29 to 0.47 reflecting that the increase in R2 is not just because of addition of degree of freedoms.
3. In the new model some features ( MajorN PropN OthN and asthmaRatio) shows a strong performance in explaining the variation in SAT score as all these features have p-value lower than 0.1. The lowest p-value is for asthmaRatio, showing it has strong relation with the SAT math feature.

