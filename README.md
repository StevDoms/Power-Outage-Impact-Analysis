# Power Outage Impact Analysis

This project was done as part of UCSD's DSC80 class.

## Introduction
Our dataset contains the major power outage events in the United States between January 2000 and July 2016.

### Analysis Question
How does the category of cause and climate category associate with the outage duration, numbers of customers affected and total price of electricity?

### Significance of Dataset & Question
Understanding how the causes and climate categories relate to power outage duration, impacted customer numbers, and electricity costs between 2000 and 2016 is crucial for assessing grid vulnerabilities, mitigating economic losses, and enhancing public safety. This analysis sheds light on the patterns that influence outage severity, guiding better resource allocation and policy decisions to fortify infrastructure and preparedness. It also empowers consumers with insights into outage-prone conditions, fostering awareness and proactive measures to minimize disruption during future outages.

### Dataset Details
Each observation contains a single power outage event. The dataset contains 1534 rows of data. The columns that we used includes Climate Category, Cause Category, Outage Duration, Customers Affected, and Total Price. Climate Category referes to the climate condition when the outage happened. Cause Category refers to the cause of the outage. Outage Duration refers to the length of the outage. Customers Affected refers to the number of customers affected by the outage. Total Price refers to cents per kilowatthour that customers pay during the outage.

## Data Cleaning & Exploratory Data Analysis

### Data Cleaning
The first step that we took was dropping any unnecessary rows and columns that do not contain any data to create a tidy dataset. The second step was quering the columns mentioned above to prepare it for analysis. The third step was checking for missing values within each column. The last step was filling in those missing values. For columns with numerical variables (Outage Duration, Customers Affected, Total Price), we fill the missing values with 0. For columns with categorical variables (Climate Category, Cause Category), we fill the missing values through probabilistic imputation. Because we fill in the numerical columns with 0, this might skew the central tendancy of the data which increases the error in our analysis. 
