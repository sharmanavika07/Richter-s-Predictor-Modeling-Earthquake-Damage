Problem description
We're trying to predict the ordinal variable damage_grade, which represents a level of damage to the building that was hit by the earthquake. There are 3 grades of the damage:
•	1 represents low damage
•	2 represents a medium amount of damage
•	3 represents almost complete destruction


The dataset mainly consists of information on the buildings' structure and their legal ownership. Each row in the dataset represents a specific building in the region that was hit by Gorkha earthquake.


There are 39 columns in this dataset, where the building_id column is a unique and random identifier. The remaining 38 features are described in the section below. Categorical variables have been obfuscated random lowercase ascii characters. The appearance of the same character in distinct columns does not imply the same original value.

Feature Description:
•	geo_level_1_id, geo_level_2_id, geo_level_3_id (type: int): geographic region in which building exists, from largest (level 1) to most specific sub-region (level 3). Possible values: level 1: 0-30, level 2: 0-1427, level 3: 0-12567.
•	count_floors_pre_eq (type: int): number of floors in the building before the earthquake.
•	age (type: int): age of the building in years.
•	area_percentage (type: int): normalized area of the building footprint.
•	height_percentage (type: int): normalized height of the building footprint.
•	land_surface_condition (type: categorical): surface condition of the land where the building was built. Possible values: n, o, t.
•	foundation_type (type: categorical): type of foundation used while building. Possible values: h, i, r, u, w.
•	roof_type (type: categorical): type of roof used while building. Possible values: n, q, x.
•	ground_floor_type (type: categorical): type of the ground floor. Possible values: f, m, v, x, z.
•	other_floor_type (type: categorical): type of constructions used in higher than the ground floors (except of roof). Possible values: j, q, s, x.
•	position (type: categorical): position of the building. Possible values: j, o, s, t.
•	plan_configuration (type: categorical): building plan configuration. Possible values: a, c, d, f, m, n, o, q, s, u.
•	has_superstructure_adobe_mud (type: binary): flag variable that indicates if the superstructure was made of Adobe/Mud.
•	has_superstructure_mud_mortar_stone (type: binary): flag variable that indicates if the superstructure was made of Mud Mortar - Stone.
•	has_superstructure_stone_flag (type: binary): flag variable that indicates if the superstructure was made of Stone.
•	has_superstructure_cement_mortar_stone (type: binary): flag variable that indicates if the superstructure was made of Cement Mortar - Stone.
•	has_superstructure_mud_mortar_brick (type: binary): flag variable that indicates if the superstructure was made of Mud Mortar - Brick.
•	has_superstructure_cement_mortar_brick (type: binary): flag variable that indicates if the superstructure was made of Cement Mortar - Brick.
•	has_superstructure_timber (type: binary): flag variable that indicates if the superstructure was made of Timber.
•	has_superstructure_bamboo (type: binary): flag variable that indicates if the superstructure was made of Bamboo.
•	has_superstructure_rc_non_engineered (type: binary): flag variable that indicates if the superstructure was made of non-engineered reinforced concrete.
•	has_superstructure_rc_engineered (type: binary): flag variable that indicates if the superstructure was made of engineered reinforced concrete.
•	has_superstructure_other (type: binary): flag variable that indicates if the superstructure was made of any other material.
•	legal_ownership_status (type: categorical): legal ownership status of the land where building was built. Possible values: a, r, v, w.
•	count_families (type: int): number of families that live in the building.
•	has_secondary_use (type: binary): flag variable that indicates if the building was used for any secondary purpose.
•	has_secondary_use_agriculture (type: binary): flag variable that indicates if the building was used for agricultural purposes.
•	has_secondary_use_hotel (type: binary): flag variable that indicates if the building was used as a hotel.
•	has_secondary_use_rental (type: binary): flag variable that indicates if the building was used for rental purposes.
•	has_secondary_use_institution (type: binary): flag variable that indicates if the building was used as a location of any institution.
•	has_secondary_use_school (type: binary): flag variable that indicates if the building was used as a school.
•	has_secondary_use_industry (type: binary): flag variable that indicates if the building was used for industrial purposes.
•	has_secondary_use_health_post (type: binary): flag variable that indicates if the building was used as a health post.
•	has_secondary_use_gov_office (type: binary): flag variable that indicates if the building was used fas a government office.
•	has_secondary_use_use_police (type: binary): flag variable that indicates if the building was used as a police station.
•	has_secondary_use_other (type: binary): flag variable that indicates if the building was secondarily used for other purposes.
Approach to the problem:
The dataset contains 4 numerical variables and rest all are categorical variables.
Since the dataset is massive and we have many features, we may have to select and analyse which features are important to our target variables.
Since, we have to predict the damage_grade, the scene is pretty clear that we have to apply classification analysis.

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
I got a score of 0.70 on this dataset, which was ranked 406 out of 1670 participants. But there is a lot of room for improvement.

