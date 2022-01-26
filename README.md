This is an analysis of the wellness data from Kaggle. 

There is little information about the specifics of the survey (who, what, or why) but the survey was uploaded recently and appears to have been done by 3 wellness websites, so I assume it is a web survey. Timestamps indicate the survey was started in 2015 and is still ongoing. Two of the websites are English language and one French so I am guessing it is some of their potential customers, which may skew the data to people who are wealthier and/ or more interested in wellness.

Exploratory analysis
The data has roughly 16,000 responses, twenty-four columns, and no null values. Timestamp is irrelevant so I dropped that and converted the few objects to numbers to make analysis easier. Most of the results are on a 10 point likert scale though some are five or two points. One confusing aspect of the data is the work-life-balance result is a result of all the questions so it is to some extent, by definition, collinear with all the data points. It is unclear what the formula for producing this score is.
Collinearity seems limited between the various responses other than the work_life_balance score noted earlier.

I wanted to examine categorical data so I focused on the Sufficient_Income result as it is a binary result and should have interesting correlations with the other responses. 73% of the respondents said they have sufficient income so any predictive algorithm should have a result greater than 73%.

The highest correlations with Sufficient_Income were Work_Life_Balance (40%), To_Do_Completed (20%), and Places_Visited (17%).

Data cleaning

To allow more analysis I replaced the categorical variables (Gender and Age) with numbers and 1 wrongly filed data point was converted to a mean.

Analysis

I conducted a train_test_split on the data, stratified the data to account for the imbalance in the independent variable, and then fit the model to a decision tree. With the decision tree we have increased the predictability up to 77% though it does include the slightly collinear Work_Life_Balance feature. When feature importance is measured Work_Life_Balance appears to account for 95% of the decision tree results.
I also tried logistic regression on the data set and received failure to converge errors at up to 1000 iterations. Lower numbers of iterations did not result . Interestingly, cross validation of the training data showed a predictability of 1 in all 5 folds of the data. This seems surprising given the relatively low correlations with other data.

Results

The basic results are the general catchall Work_Life_Balance feature appears to be the most significant in predicting the sufficient income variable and that logistic regression has questionably high chance of predicting who has sufficient income.
Future analysis
There are several things further I would like to do with this data. One would be removing Work_Life_Balance from the analysis and another would be turning Daily_Stress into the dependent variable and seeing what is most predictive of Daily_Stress. I also want to try these analyses using the K nearest neighbor method.
