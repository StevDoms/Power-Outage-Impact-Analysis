# Power Outage Impact Analysis

This project was completed as part of the DSC80.

This page can be viewed at https://stevdoms.github.io/Power-Outage-Impact-Analysis/

## Introduction
Our dataset contains the major power outage events in the United States between January 2000 and July 2016.

### Analysis Question
How does the cause category associate with the outage duration, numbers of customers affected and total price of electricity?

### Significance of Dataset & Question
Understanding how the causes category relate to power outage duration, impacted customer numbers, and electricity costs between 2000 and 2016 is crucial for assessing grid vulnerabilities, mitigating economic losses, and enhancing public safety. This analysis sheds light on the patterns that influence outage severity, guiding better resource allocation and policy decisions to fortify infrastructure and preparedness. It also empowers consumers with insights into outage-prone conditions, fostering awareness and proactive measures to minimize disruption during future outages.

### Dataset Details
Each observation contains a single power outage event. The dataset contains 1534 rows of data. The columns that we used includes Cause Category, Outage Duration, Customers Affected, and Total Price. Cause Category refers to the cause of the outage. Outage Duration refers to the length of the outage. Customers Affected refers to the number of customers affected by the outage. Total Price refers to cents per kilowatthour that customers pay during the outage.

## Data Cleaning & Exploratory Data Analysis

### Data Cleaning
The first step that we took was dropping any unnecessary rows and columns that do not contain any data to create a tidy dataset. The second step was quering the columns mentioned above to prepare it for analysis. The third step was checking for missing values within each column. It turns out that only the numerical variables have missing values. The last step was filling in those missing values. For columns with numerical variables (Outage Duration, Customers Affected, Total Price), we fill the missing values with 0. Because we fill in the numerical columns with 0, this might skew the central tendancy of the data which increases the error in our analysis. 

| CAUSE.CATEGORY     |   OUTAGE.DURATION |   CUSTOMERS.AFFECTED |   TOTAL.PRICE |
|:-------------------|------------------:|---------------------:|--------------:|
| severe weather     |              3060 |                70000 |          9.28 |
| intentional attack |                 1 |                    0 |          9.28 |
| severe weather     |              3000 |                70000 |          8.15 |
| severe weather     |              2550 |                68200 |          9.19 |
| severe weather     |              1740 |               250000 |         10.43 |

### Univariate Analysis

<iframe src="assets/OutageDurationDistribution.html" width=800 height=600 frameBorder=0></iframe>

The distribution of the Outage Duration is right skewed and most of the values are clustered within 0 - 2999 mins. The right-skewed distribution of Outage Duration indicates that the majority of recorded outage events have relatively shorter durations, predominantly falling within the range of 0 to 2999 minutes, with fewer instances of longer-lasting outages.

<iframe src="assets/CustomersAffectedDistribution.html" width=800 height=600 frameBorder=0></iframe>

The distribution of the Customers Affected is right skewed and most of the values are clustered within 0 - 149,000 people.

<iframe src="assets/TotalPriceDistribution.html" width=800 height=600 frameBorder=0></iframe>

The distribution of the Customers Affected is partially normally distributed.

### Bivariate Analysis

<iframe src="assets/OutageDurationByCause.html" width=800 height=600 frameBorder=0></iframe>

Based on the graph, most of the causes have an mean duration of outage which is closed to 0 mins, with the exception of severe weather, public appeal, and fuel supply emergency. The fuel supply emergency particularly stands out as it has the highest variance among other causes.

### Interesting Aggregates

| CAUSE.CATEGORY                |      mean |   median |   min |    max |
|:------------------------------|----------:|---------:|------:|-------:|
| equipment failure             |  1665.5   |    193   |     0 |  78377 |
| fuel supply emergency         | 10046.9   |   1440   |     0 | 108653 |
| intentional attack            |   414.55  |     30.5 |     0 |  21360 |
| islanding                     |   191.826 |     57.5 |     0 |   1254 |
| public appeal                 |  1468.45  |    455   |    30 |  11867 |
| severe weather                |  3787.27  |   2299   |     0 |  49320 |
| system operability disruption |   705.913 |    204   |     0 |  23187 |

This aggregate supports our graph indicating that some cause category have longer outage duration than others.

## Assessment of Missingness
This section focuses on determining the type of missingness on our specified columns. In particular, we will focus on determining NMAR and MAR. 
### NMAR Analysis
The columns which we are trying to determine whether the columns are NMAR are CUSTOMERS.AFFECTED, OUTAGE.DURATION and TOTAL.PRICE which contains missing values. Since CAUSE.CATEGORY has no missing values, we can use this column as a way to conduct MAR analysis torwards CUSTOMERS.AFFECTED, OUTAGE.DURATION and TOTAL.PRICE. Based on intuition, we may have reason to believe that of these columns are dependent on CAUSE.CATEGORY unless proven otherwise. In other words, the columns with missingness may be systematically linked to the reasons for the outage as this linkage might affect the probability of missingness. Moreover, it is unlikely that these columns are missing by design as the determinants from columns within the dataset does not guarentee predictions torwards missingness on a specific column.

### MAR Analysis
The columns CUSTOMERS.AFFECTED, OUTAGE.DURATION and TOTAL.PRICE contains missing values while CAUSE.CATEGORY contains no missing values and we can disprove that these columns are NMAR by proving MAR dependency on CAUSE.CATEGORY.

Hence we are interested to perform permutations tests on these three columns with CAUSE.CATEGORY to test their MAR Dependency by using the TVD, calculating the proportion of missing values to not missing values for each category. We conducted a hypothesis tests on these three columns with a significance level of 0.1.

#### MAR Analysis for OUTAGE.DURATION
Null Hypothesis: The missingness of OUTAGE.DURATION does not depend on CAUSE.CATEGORY
Alternative Hypothesis: The missingness of OUTAGE.DURATION depend on CAUSE.CATEGORY

<iframe src="assets/OD_bar_missing.html" width=800 height=600 frameBorder=0></iframe>
The graph above shows the distribution of the missigness OUTAGE.DURATION based on the categories of CAUSE.CATEGORY. We can see from the graph above how the missingness of OUTAGE.DURATION varies depending on different categories of CAUSE.CATEGORY. To confirm, we will conduct a permutation test.

<iframe src="assets/OutageDurationDistributionMissing.html" width=800 height=600 frameBorder=0></iframe>
P-value for column OUTAGE.DURATION: 0.006644518272425249

With a significance level of 0.1, we fail to reject the null hypothesis since the p-value we obtained from conducting 300 permutatioon tests resulted in a p-value of around 0.006 which is significantly lower than the significance value. This also clearly proven in the graph in which the cutoff value of our observed statistic shown as a red line is far away from the test statistic distribution. Hence OUTAGE.DURATION is considered to be MAR.

#### MAR Analysis for CUSTOMERS.AFFECTED
Null Hypothesis: The missingness of CUSTOMERS.AFFECTED does not depend on CAUSE.CATEGORY
Alternative Hypothesis: The missingness of CUSTOMERS.AFFECTED depend on CAUSE.CATEGORY

<iframe src="assets/CAM_bar_missing.html" width=800 height=600 frameBorder=0></iframe>
The graph above shows the distribution of the missigness CUSTOMERS.AFFECTED based on the categories of CAUSE.CATEGORY. Similar to OUTAGE.DURATION, notice how the graph above also indicates missingness of OUTAGE.DURATION varies depending on different categories of CAUSE.CATEGORY. To confirm, we will conduct a permutation test.

<iframe src="assets/CustomersAffectedDistributionMissing.html" width=800 height=600 frameBorder=0></iframe>
P-value for column CUSTOMERS.AFFECTED: 0.0033222591362126247

With a significance level of 0.1, we fail to reject the null hypothesis since the p-value we obtained from conducting 300 permutatioon tests resulted in a p-value of around 0.003 which is significantly lower than the significance value. This also clearly proven in the graph in which the cutoff value of our observed statistic shown as a red line is far away from the test statistic distribution. Hence CUSTOMERS.AFFECTED is considered to be MAR.


#### MAR Analysis for TOTAL.PRICE
Null Hypothesis: The missingness of TOTAL.PRICE does not depend on CAUSE.CATEGORY
Alternative Hypothesis: The missingness of TOTAL.PRICE depend on CAUSE.CATEGORY

<iframe src="assets/TPM_bar_missing.html" width=800 height=600 frameBorder=0></iframe>
The graph above shows the distribution of the missigness TOTAL.PRICE based on the categories of CAUSE.CATEGORY. Similar to OUTAGE.DURATION and CUSTOMERS.AFFECTED, notice how the graph above also indicates missingness of TOTAL.PRICE varies depending on different categories of CAUSE.CATEGORY. To confirm, we will conduct a permutation test.

<iframe src="assets/TotalPriceDistributionMissing.html" width=800 height=600 frameBorder=0></iframe>
P-value for column TOTAL.PRICE: 0.07641196013289037

With a significance level of 0.1, we fail to reject the null hypothesis since the p-value we obtained from conducting 300 permutatioon tests resulted in a p-value of around 0.07 which is lower than the significance value. Although this time the p-value is lower than the significance level of 0.01, changing the significance level to 0.05 or lower will change the outcome of the permutation test. But in our case, we will stick to a significane level of 0.1 and reject the null hypothesis. Notice in the graph in which the cutoff value of our observed statistic shown as a red line strays away from the majority of test statistic distribution. Hence CUSTOMERS.AFFECTED is considered to be MAR.

## Hypothesis Testing

We are conducting a permutation test to check whether the outage duration, numbers of customers affected and total price of electricity differs between 2 different causes namely severe weathers and intentional attack. We chose those 2 causes because they have the largest number of sample data which increases the accuracy of our testing. We think that comparing 2 causes is enough to provide a conclusive result because it allows for a focused and detailed comparison with a substantial amount of data, which enhances the robustness and conclusiveness of our analysis. Since we want to test it on 3 different variables, we will conduct the hypothesis test 3 times.

**Null Hypothesis**: The outage duration from severe weathers and intentional attack comes from the same distribution

**Alternative Hypothesis**: The outage duration from severe weathers is longer than the outage duration from intentional attack

**Test Statistics**: Difference between the group (severe weathers and intentional attack) mean

**Significance Level**: To fortify the reliability of our conclusion concerning diverse impacts, we have chosen a significance level of 5% for our randomized test. This deliberate choice aims to bolster the precision and validity of our test results.

The visualization depicted below illustrates the empirical distribution of our test statistics across 1000 permutations, with the observed test statistics denoted by the red line.

<iframe src="assets/HypothesisTestingDuration.html" width=800 height=600 frameBorder=0></iframe>

Based on the graph above, we obtain a p-value of 0.0 which is less than 0.05. This indicates that our observed statistic is not likely coincidental, and hence we **reject our null hypothesis**.

<iframe src="assets/HypothesisTestingCustomersAffected.html" width=800 height=600 frameBorder=0></iframe>

Based on the graph above, we obtain a p-value of 0.0 which is less than 0.05. This indicates that our observed statistic is not likely coincidental, and hence we **reject our null hypothesis**.

<iframe src="assets/HypothesisTestingTotalPrice.html" width=800 height=600 frameBorder=0></iframe>

Based on the graph above, we obtain a p-value of 0.135 which is higher than 0.05. This indicates that our observed statistic is likely coincidental, and hence we **fail to reject our null hypothesis**.

### Conclusion

Based on our hypothesis tests, we reject the null hypothesis for Outage Duration and numbers of Customers Affected while we fail to reject our null hypothesis for Total Price. In total, we reject 2 null while we fail to reject 1. Hence, we opt to reject the null that both cause come from the same distribution (cause category have no effect on the 3 variables). Although we cannot conclude that cause category cause those variables to increase, it is highly likely that there are some positive association between cause category and the numerical variables aforementioned.

## Model

### Framing the Problem

The goal of our analysis is to predict the **cause category** of an outage based on the **outage duration**, **numbers of customers affected**, **total price** of electricity during the outage, **NERC region**, and **climate category**. Since **cause category** is a categorical variable with 7 unique values, we are going to be performing a multiclass classification. We chose to predict the cause category because it allows for different strategies and interventions to be implemented in hopes to mitigate future outages. If severe weather is a prevalent cause, reinforcing infrastructure against extreme conditions might be a priority task to complete. We chose to use F_1 score with weighted average because it considers both the precision and recall, and also accounts for the cause imbalance. Since mitigation plans costs a lot of monetary value, we want to balance out the false positive and false negative to ensure that the mitigation targets the right causes. We don't use other metrics such as accuracy because the causes categories are unevenly distributed which would not provide a comprehensive understanding of the model. 

### Baseline Model

For our model, we used a decision tree classifier. We only specified the criterion to be 'entropy' as our hyperparameters, and as a result, our model uses splitter='best', max_depth=None, min_samples_split=2, min_samples_leaf=1, max_features=None. Our model takes in 3 quantitative variables which are outage duration, numbers of customers affected and total price and 2 nominal variables which are NERC region and climate category as our regressors to predict cause category which is a nominal variable. We performed one hot encoding for the NERC region and climate category by using the OneHotEncoder class from sklearn and kept all the quantitative categories as is.

We evaluated the performance of our baseline model using f1_score, and our model received an f1_score of 0.6118824440755535. This suggests that the harmonic mean of precision and recall to be 0.6118, indicating a reasonably good balance between precision and recall. As such, our current model is pretty good.

### Final Model

We used the exact same features that was used for the baseline model. We transformed both the nominal variables with One Hot Encoding. However, instead of leaving the quantitative variables as is, we applied StandardScalar() to the Total Price and Outage Duration and QuantileTransformer() to the numbers of customers affected. We applied StandardScaler() to Total Price and Outage Duration to standardize the scale and ensure that features with different magnitudes don’t dominate and aids the model in converging faster. This transformation also helps in normalizing distributions and reducing the impact of outliers, resulting in improved stability. We applied QuantileTransformer() for numbers of customers affected to transform the skewed distributions so that the feature becomes less sensitive to extreme values and better suited for the model. By enhancing these features comparability, these transformations would improve our overall model performance.

To standardize the comparison with the baseline model, we used a decision tree classifier for our model. We used GridSearchCV with 8 cross-validations to select the max_depth and min_samples_split hyperparameters. Based on this process, the hyperparameter that ended up performing best is max_depth=8 & min_samples_split=50, with criterion='entropy' (which is the same as the baseline model).

We evaluated the performance of our final model using f1_score, and our model received an f1_score of 0.6626287617698571. Our final model produced a higher f1 score than our baseline model which indicates an improvement in the final model's ability to balance precision and recall compared to the baseline model. This further suggests that the final model is better at capturing true positives while minimizing false positives and false negatives which results in a more reliable and accurate prediction of the cause category of outages.

### Fairness Analysis

We conducted a permutation test for groups which are outages above and below 24 hours. In addition, we used f1_score as our evaluation metric and a significance level of 5%.

**Null hypothesis**: My model is fair. The f1_score for outages above 24hours (1440minutes) is the same as f1_score for outages below 24hours, and any differences are due to random chance

**Alternative hypothesis**: My model is unfair. The f1_score is different for outages above and below 24 hours

**Test Statistic**: Absolute difference between the f1_score of outages above and below 24 hours

Based on our permutation test, we obtain a p-value of 0.0% which is less than our set threshold of 5%. Hence, we reject our null hypothesis, and conclude that there is a statistical difference between the f1_score of outages above and below 24 hours.
