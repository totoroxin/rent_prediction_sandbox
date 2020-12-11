# Socio-Spatial Characteristics and Neighborhood Rental Housing Prices in Six US Metro Cities

----

*Corresponding author email: zhang.1977@osu.edu*


## Background

In general, people tend to adopt dwelling features (for example, interior features like the numbers of bedrooms and bathrooms, furnishing conditions, views, and exterior features like building/community amenities and HOA services) to predict rental prices. However, **socio-spatial features, including location, demographics, social environments, local transportation, and characteristics of neighborhood-built environments, could be determinant factors of rental prices besides rental properties themselves.** These factors may also associate with the values of developed or under-development lands. Particularly in dense areas/cities like Manhattan, commute services, and city life features affect people’s housing choices with less car uses compared to suburban areas.

Because of the lack of environmental data relating to rental market data, **most projects of rental price prediction had overlooked the environmental factors** that only tested the housing interior features and using few of neighborhood features.

Therefore, the project has tested the importance of using the outside socio-spatial features under seven major categories (demographics, social engagement, natural environment, health service, neighborhood environments, living opportunities, and transportation conditions) to predict average rental prices for neighborhoods in six US metropolitan areas.

## Objectives

**1. Predict average neighborhood rental prices based on the neighborhood socio-spatial features**

For the average neighborhood housing price, the individual apartment features would be less important compared with its location and outside environments. The prediction results could provide an insight to estimate the general rental market value through socio-spatial data without local investigations. Landlords and investors can use such information for decision making on investing or renovating rental properties in a certain neighborhood. Meanwhile, the prediction models can assist residents in housing choices. Moreover, as the project has tested neighborhoods in six cities, we may apply the method to other areas/cities based on different business demands.

**2. Identify the key environmental features for increasing the neighborhood market values**

The project has examined over 40 types of socio-spatial features. It would help us to identify which of them affect the average neighborhood rents most (with the greatest predictive power) and in which directions. The results also provided insights for local government and communities for neighborhood improvements.

## Datasets

The project integrated the datasets from three sources: renthop open data for rents, AARP livability index API (https://livabilityindex.aarp.org/livability-sources) for socio-environmental features, and Google map API for location extractions that linked renthop data with AARP data.

**Target variable**

Average rental prices per neighborhoods in six metro cities: Boston, MA; Chicago, IL; Dallas-Fort Worth, TX; Los Angeles, CA; Miami, FL; New York, NY
Total sample (neighborhoods): 185

**Predictors**

The livability index contained two parts: overall livability ratings for seven categories and detailed feature ratings under each category. The overall ratings provided the weighted total scores measured from both feature metrics and policies; however, the detailed feature ratings were only generated from physical measurements/metrics without policies.

As the effects of policies (except housing policies) on rental prices were uncertain, the project split the predictors into two groups: overall ratings (seven variables) and 43 detailed features including demographics.

(For variable list, see Appendix Table 1.)

## Methods

### Socio-spatial data acquiring and wrangling ###
The link below contained the data acquiring, integration and cleaning process.
https://github.com/totoroxin/rent_prediction_sandbox/blob/master/AARP_renthop_data_integration.ipynb

### Data analyses and visualizations
![alt text](rents_barplot.png "Title")

![alt text](livabilities_six_cities.png "Title")

The link below contained data analyses and modeling process.
https://github.com/totoroxin/rent_prediction_sandbox/blob/master/rent_neigh_analysis.ipynb


## Model Selections and Results
#### 1. Using overall livability ratings to predict neighborhood average rents
- The results from the linear model showed the seven categories containing policy scores explained 47% variance of neighborhood average rents. Such general categories would be not accurate predictors, and the linear model was not an ideal choice.

- The results from the random forest model showed the prediction accuracy was 79.33% (1-MAE) with seven predictors. It was much better than the linear solution.

#### 2. Using detailed feature index to predict neighborhood average rents
As I considered the policy might not directly have effects on rents, and the existing physical conditions affected more on it, I extracted 43 detailed features from six categories (excluded housing cost itself) including demographics to explore the individual effects.
- The results from three methods (random forest, Ada boosting, and gradient boosting) showed the 43 features provided 82%-84% accuracies to predict neighborhood average rents.

- The most important feature we observed was **neighborhood transit accessibility**.

An example of the top part of a single decision tree from the random forest:
![alt text](small_tree.png "Title")

- Model improvement to reduce the number of features
I used a feature selection method for the random forest model to find out the key features that could explain most of the variance. It turned out that the number of features was reduced to nine out of 43, and the prediction accuracy had improved to 83.2%. Although it was not a dramatic improvement, it might reduce the workload for neighborhood feature data collection in the future.


## Conclusion
This project has demonstrated the way of **using socio-spatial characteristics to predict average neighborhood housing rental prices**. The results had documented over 80% accuracy that the outside environmental characteristics could predict the average neighborhood rents without using the apartment interior features. It indicated the location, social and neighborhood environments are the most important factors that affect the rental market among different areas, for example, transit accessibility. It would help investors, developers and residents to evaluate the rents associating with the neighborhood values, and to optimize the schema of improving environmental features with low costs.

The projected successfully **integrated different types of data, such as spatial and housing data, from three resources**. It also has compared several machine learning methods. Some of the distributions of socio-spatial features were skewed with high bias and low variance, but some of the distributions showed low bias and high variance. Therefore, it might explain that the bagging methods and the boosting methods had similar performances for this dataset.

The project remains future works such as adding interior features to predict the price of individual rental property instead of the average in the neighborhood and adding more locations/samples to accurate the predictive power of each feature as we only have less than two-hundred cases in this preliminary research. Also, considering the housing sale market, the predictive power of each feature may differ from the neighborhood rental market. However, we could adopt similar methods to explore sale values. It would provide investors with multiple dimensions to make business decisions.



## References
https://www.renthop.com/studies

https://livabilityindex.aarp.org/livability-sources 

https://towardsdatascience.com/feature-selection-using-random-forest-26d7b747597f


*Note: the author owns all copyright of this project.*
