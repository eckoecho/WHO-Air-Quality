# World Health Organization (WHO) Air Quality



In a world facing escalating pollution challenges, air quality degradation compromises essential aspects of our existence. This analysis holds significance for individuals who prioritize a high quality of life and rely on clean air, encompassing not only concerned citizens but also policymakers.


The source of this data comes from Kaggle, an open-source website for datasets and insights. This particular data can be found here: [Kaggle, World Air Quality Index (AQI)](https://www.kaggle.com/datasets/adityaramachandran27/world-air-quality-index-by-city-and-coordinates)


This dataset is composed of information collected by the World Health Organization (WHO). The columns in our dataset indicate the key features that influence air qualities within cities around the world.  The features contain lexicon which readers may not be familiar with but are addressed in the accompanying table diagram.

**Data Dictionary:**
| Term | Definition |
| --- | --- |
| **AQI** | Air Quality Environment |
| **Carbon Monoxide (CO)**| CO is a colorless, odorless gas that is produced by the incomplete burning of fossil fuels. High levels of CO can be toxic to humans and can cause headaches, dizziness, and nausea
| **Ozone** | Ozone is a gas that can form in the atmosphere through a chemical reaction between sunlight and other pollutants. High levels of ozone can be harmful to human health, particularly for those with respiratory issues.|
| **NO2** | Nitrogen Dioxide, which is a reddish-brown gas and one of the main pollutants in the atmosphere. It is primarily emitted from combustion processes, such as vehicle engines, power plants, and industrial activities. |
| **PM2.5** | PM2.5 refers to tiny particles or droplets in the air that are 2.5 micrometers or less in width. They can be harmful to human health when inhaled, especially in high concentrations.|

There are 16695 rows, and 14 columns (13 features) in our dataset.

My target's, `AQI Category`, values are defined as below. For the sake of simplicity, I've binned these 3 columns as "Good", "Moderate", and "Unhealthy", combining "Unhealthy for Sensitive Groups", "Very Unhealthy", "Hazardous" as simply "Unhealthy". These categories become more apparent when examining the results of our machine learning models, which you'll find in this README's Recommendation section.

<img width="1079" alt="Screenshot 2023-07-06 at 12 35 52 AM" src="https://github.com/eckoecho/Project-2/assets/43970023/abcf9ceb-f322-4333-9835-d7e80b5abaa3">

[Source](https://www.airnow.gov/aqi/aqi-basics/#:~:text=AQI%20values%20at%20or%20below,as%20AQI%20values%20get%20higher)


# Exploratory Data Analysis (EDA)

## AQI Value vs. PM2.5 AQI Value

When comparing features, the most prominent influencer of air quality is the PM2.5 levels within a city. In the scatterplot, we can see higher levels of PM2.5 are only present when the air quality dips into the unhealthy air quality. Smaller levels of PM2.5 ranging from 0 to 100 are toleratable to be considered in the good and moderate air qualities. Therefore, reducing or eliminating PM2.5 levels within a city improves the air quality. However, if these actions aren't possible individuals should check a city's PM2.5 levels to consider where they fall in the spectrum of air quality.

<img width="850" alt="Screenshot 2023-07-07 at 8 07 31 AM" src="https://github.com/eckoecho/Project-2/assets/43970023/d4f47613-7c7f-47ea-b0e0-664949b002b0">

## AQI Value vs. CO AQI Value

Carbon Monoxide (CO) AQI Values also play a significant in the air quality. Presence of CO levels don't necessarily indicate that air quality is unhealthy, rather the quantity of CO levels in the air is the key factor.  CO levels below 1.5 are still considered tolerable to moderate and good air qualities.  However, good air qualities reading indicate the CO levels need to be at .75 and below.  CO levels at 1.5 and above contribute to an unhealthy air quality. It should be noted, it is possible to have lower levels of CO and still be grouped into the unhealthy air quality.

<img width="565" alt="Screenshot 2023-07-07 at 8 54 16 AM" src="https://github.com/eckoecho/Project-2/assets/43970023/957e9a40-7b44-4538-9fb1-0d6b1a484a61">


# Recommended Model

While other models, such as the Decision Tree and the tuned Decision Tree, may appear to have better F1 training and testing scores of 1, this actually indicates that the models are overfit and will not accurately predict new data.

My recommendation is to use the Random Forest model with PCA (Principal Component Analysis) because it achieves the best F1 scores. The F1 score considers both precision and recall. The Random Forest model with PCA achieves a testing F1 score of 1 for predicting good air quality, 0.98 for moderate air quality, and 0.93 for unhealthy air quality. The tuned Random Forest model also demonstrates good F1 scores on its testing data. However, when predicting "Unhealthy" air quality, its F1 score drops to 0.01. This is likely due to the limited number of "Unhealthy" data points compared to the number of good or moderate data points.

By incorporating PCA, the model is able to effectively reduce the dimensionality of the input data while retaining important features. This helps in capturing the underlying patterns and relationships within the data, leading to improved predictive performance.

Overall, the Random Forest model with PCA and my EDA findiings offers a robust and effective solution for accurately predicting air quality categories, making it a valuable tool for addressing questions on the air quality of a city and related decisions on the key indicators for policymakers.
