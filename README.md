# Data Mining Final Project Report - Fatality Analysis
# Elena Gillis (emg3sc), Kanika Dawar (kd2hr), Varshini Sriram (vs4vx)

## 1. The Problem

### Introduction
Every year a large number of highway crashes occur that involve one or more fatalities per crash. There are
numerous factors that contribute to the situation, which can be influenced in order to impact the outcome. In
this project, we aim to identify the main factors of a fatal crash, predict the number of deaths, and contribute to
the understanding of the effectiveness of motor vehicle safety standards and highway safety programs.

### Descriptive Analysis
● Fatality Analysis Reporting System (FARS) is a nationwide census providing public yearly data
regarding fatal injuries suffered in motor vehicle traffic crashes. This data is critical to understanding the
characteristics of the environment, trafficway, vehicles, and persons involved in the crash.
● We aim to analyze data ranging from 2015-2017 obtained from National Highway Traffic Safety
Administration (NHTSA) website to help understand the factors contributing to car crashes and
subsequently influence the system to reduce the number of motor vehicle crashes and deaths on our
nation's highways. The data provides us with details of variables such as no of pax, drunk drivers,
vision, speed, etc which play an important role in helping us understand the chances of a fatal accident
occurring and what can and should be changed to impact the outcome.
● External events such as national holidays, dance and music concerts, etc. which have not been
explicitly taken into account could potentially have a significant impact and lead to bias in the analysis

### Normative Analysis
● Once the factors leading to fatal accidents are identified, measures can be taken to improve the road
regulations and safety conditions leading to fewer accidents and subsequently, to fewer fatalities

### Stakeholders
● NHTSA, General Public, Insurance Companies

### Impact
● Fewer casualties in vehicle crashes
● Reduction of economic loss

## 2. Objectives and Metrics

### Objectives
● Predict total fatal crashes for the year 2018
● Classify a fatal car crash into levels of accident severity - low/mid/high based on number of casualties
● Understand the most important factors for a car crash involving fatalities

### Metrics
● Mean Square error in prediction
● Misclassification error
● Relevance of factors identified with general government consensus

## 3. State-of-the-Art
● The following data sources were already investigated for traffic fatality analysis: NHTSA’s FARS,
FastFARS (FF), and Monthly Fatality Counts (MFC). FARS is a census of fatal traffic crashes. The FF
program is an Early Fatality Notification System to capture fatality counts from States more rapidly and
in real-time. The MFC data provides monthly fatality counts by State through sources that are
independent of the FastFARS or FARS systems.
● Data mining methods such as Time Series Analysis and Regression Techniques were applied to the
traffic data to predict fatality rates, to understand where crashes happen most often, what conditions
correlate with collisions and which road users are most vulnerable. [8]
● The methods have been evaluated using MSE. Ridge Regression proved to be the most successful
method in terms of predicting fatalities. ARIMA model worked best for forecasting fatality rates. [8]
● It’s hard to predict the fatalities in a car crash because of the wide number of factors involved. Even if
we identify the factors, it is hard to anticipate the predicted conditions. Incorporating the external factors
and enforcing safety regulations that are coherent with the factors identified makes it a difficult problem.
[9] [10]

## 4. Hypotheses and Approach

### Hypotheses
● We anticipate that factors such as usage of safety equipment, drunk driving, seasonality and light
conditions are the most common factors contributing to increased fatality rates.
● Data mining methods such as Decision Trees (Random Forest) will produce a better classification
accuracy compared to K-Nearest Neighbors and Support Vector Machine when applied to the data to
predict accident severity.
● Adding a seasonality factor to the model developed for monthly fatality will help explain peaks in
fatalities and better outlier detection.

### Data
● FARS - Reporting system by the NHTSA for fatal accidents - now provided for public use in the form of
CSV files and SAS database with additional information about specific environment variables.
● Bias in the data: Data might not accurately represent all crashes, another layer of non-fatal accidents
would have given more ground threshold in terms of the importance of factors and severity of an
accident. The lack of familiarity and understanding with the reporting system might have lead to
unintentional human errors (missing data, incomprehensible values, duplication, etc.).

### Methods
● Random Forest, K-Nearest Neighbors and Support Vector Machine for classification of the accident
severity level.
● Time Series Modeling for total fatal crashes prediction.
● Mostly only Exploratory Data Analysis has been done on traffic data and so there are not enough
resources to tell if any of the above methods have been applied to make predictions. We aim to explore
all the methods learnt in class and pick the method with the best outcome.

### Evaluation Setup
● Using Random Forest we perform feature selection and identify the most important variables that
contribute to higher numbers of fatalities.
● Using time series forecasting, we will predict the number of fatal crashes annually and compare the
result for 2018 when the FARS data is released.
● We will use cross-validation to check for misclassification error while predicting accident severity (ROC
curves, TPR and FPR trade-off).
● Ideally, we would have liked to classify severity into an extra level - a non-severe accident, but dataset
does not have that level because measurement by FARS is only for fatal accidents.
● Given that all methods work with minimal error, the models should be good predictors of the outcome
and, serve our initial intentions of contributing to understanding the factors leading to fatal crashes.

## 5. Approach and Results

### Problem
There are many factors that may influence the number of fatalities in each crash, as a result, historical data
from past crashes is collected by FARS in order to identify these factors. Vehicle crashes can be reduced by
studying the crash data and detailing the factors behind traffic fatalities. Nonetheless, since specific
combinations of these variables result in different levels of crash severity, it is difficult to anticipate all these
factors to come into play all at ones. In this project, we try to identify the most important factors that contribute
to fatal crashes and try to predict such results for future accidents.

### Data
We worked with the data from FARS ranging from 2015-2017. The data came from three separate datasets for
each year - accident cases, vehicles involved in the accident and person records for fatalities. We discovered
that all three datasets had the same number of unique accident cases for each year and combined the data
based on Year and Case Number. The total number of accidents over a span of three years is 101533. The
response variable selected was the number of fatalities per accident. The number of fatalities per accident in
our data ranged from 1-13. We converted this response variable to a categorical variable - accident severity
with three levels: low, medium and high. Low corresponds to one fatality per accident, medium corresponds to
two fatalities per accident and high corresponds to over two fatalities per accident. We discovered that the
distribution of levels in the categorical response suffered from severe class imbalance - Low severity (93%),
Medium severity (6%) and High severity (1%).

### Exploratory Data Analysis
The main datasets that we used were accidents data, to which we appended persons and vehicles data
aggregated on year and case number. When performing exploratory data analysis we checked trends in
response variable in relation to individual regressors. We discovered that more accidents (and more fatalities)
were happening during the weekdays and at night time. There are also more fatalities that happened in an
urban setting and close to main roadways. Most fatalities are recorded to have occurred in crashes that were
not classified as collisions with other motor vehicles in transport, nonetheless, when another vehicle was
involved, there were significantly more crashes and more fatalities in two-vehicle accidents. We could also
observe that there were more accidents and fatalities in crashes that involved young drivers (under the age of
24) and senior drivers (over the age of 65). To observe the patterns in the causes of crash data we created a
table that summarized accidents and fatalities per cause and saw that most fatalities happened on roadways,
in speeding crashes, on junctions or intersections, and involved driving under intoxication. However, when we
sorted these values by the ratio of the number of fatalities and accidents we saw that most fatalities per crash
occurred in crashes involving police pursuit, large trucks, interstate crashes, and drowsy or intoxicated drivers.

(![Alt text](us-car-crash-analysis/images/EDA1.png?raw=true "Title")
(![Alt text](us-car-crash-analysis/images/EDA2.png?raw=true "Title")
