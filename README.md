#**Problem description**
Following the 7.8 Mw Gorkha Earthquake on April 25, 2015, Nepal carried out a massive household survey using 
mobile technology to assess building damage in the earthquake-affected districts. The primary goal 
of this survey is to identify beneficiaries eligible for government assistance for housing reconstruction, 
it also collected other useful socio-economic information. 

We are to predict the ordinal variable damage_grade, which represents a level of damage to the building that was hit by the earthquake.
There are 3 grades of the damage:
-	1 represents low damage
-	2 represents a medium amount of damage
-	3 represents almost complete destruction


The dataset mainly consists of information on the buildings' structure and their legal ownership. Each row in the dataset represents a specific building in the region that was hit by Gorkha earthquake.


There are 39 columns in this dataset, where the building_id column is a unique and random identifier. The remaining 38 features are described in the section below. Categorical variables have been obfuscated random lowercase ascii characters. The appearance of the same character in distinct columns does not imply the same original value.


**Approach to the problem:
The dataset contains 4 numerical variables and rest all are categorical variables.
Since the dataset is massive and we have many features, we may have to select and analyse which features are important to our target variables.
Since, we have to predict the damage_grade, the scene is pretty clear that we have to apply classification analysis.**

EDA and Data Processing:
1)	The dataset has no missing values.
2)	The dataset has high number of categorical / flag variables.
3)	We build a countplot to check the distribution of target variable, to see whtehr is imbalanced is not. It is not clear but later in the modelling we will take to avoid it, if there is a presence.

Feature selection:
This data requires feature selection as we have a large number of features and data points. Hence, we will do statistical tests for feature selection.
We do chi-square tests for comparing categorical data with categorical data or in other words to see if our categorical features have any impact on the severity of the damage/ damage_grade.
We do kruskal tests to check relationship between numerical data and the categorical damage_grade to check if the numerical effects the categorical data.
We then remove the unwanted or irrelevant features to remove unwanted noise in the dataset.

Splitting and modelling the data:

Since the categorical variables have low number of categories and that too they have ordinal data, we can go ahead with label encoding as the chances of bias will be low since the number of categories in each feature are less.
We can go by dummification, but that will be a nightmare because geo_level_id 1,2,3 are all ordinal data. It will create additional categories.
Getting the First result after base modelling:
We apply random forest and gradient boosting since they are good at tacking data imbalance.
Since, the model is going to be evaluated on F1 score, then accuracy score is not a credible metric for evaluation.
For a good F1 score, we need to be very careful of the data imbalance and true positives and false negatives.
So, for this we check the confusion matrix, and see that the data is imbalanced.
So, we apply smote to balance the data and get a better F1 score.


Conclusion:
I got an F1 score of 0.73 on this dataset, which was ranked 319 out of 2774 participants.

