# Power Outage Impact Analysis

This project was done as part of UCSD's DSC80 class.

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

### Bivariate Analysis

<iframe src="assets/OutageDurationByCause.html" width=800 height=600 frameBorder=0></iframe>

Based on the graph, most of the causes have an mean duration of outage which is closed to 0 mins, with the exception of severe weather, public appeal, and fuel supply emergency. The fuel supply emergency particularly stands out as it has the highest variance among other causes.

### Interesting Aggregates

