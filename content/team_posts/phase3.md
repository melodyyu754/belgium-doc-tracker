---
title: "Project - Phase III"
date: 2024-05-28
draft: false
description: "Development of our application!"
slug: "phase3post"
tags: ["authors", "config", "docs"]
authors:
  - "melody_yu"
  - "sierra_welsch"
  - "sonia_sheth"
  - "maggie_tong"
showAuthorsBadges: false
---

# Phase 3 Updates

## Overview

During this phase of the project, we started the development of the final application model. With a clear vision of our app's design, we started creating mock data, constructing pages using Streamlit, and building our backend API. On the machine learning side, we significantly enhanced our initial model, improving its R² score from 0.1 to 0.33. Additionally, we began developing our second machine learning model (k-means clustering).

## Data Model

### Updates/Modifications to our data model

During this phase for our data model, we mostly made minor changes. We fixed some issues with our data model (cascading issues), we made country name the primary key of country, we added an article name and publication date for a news article.

### Bulleted list of all tables and if data will be sourced or generated

- table: Sourced/Generated
- cause: Generated
- country: Sourced
- users: Generated
- protests: Generated
- news_articles: Generated
- posts: Generated
- comments: Generated
- protest_attendance: Generated
- protest_likes: Generated
- news_likes: Generated
- user_interests: Generated

### Why is so much of our data generated?

The majority of our data in the proof of concept is mock data. This is because our application is designed to be a self-sustaining, user-driven platform where activists, journalists, and politicians contribute and share information about political protests. Consequently, the core data, such as protest events and user-generated posts, is intended to be supplied by our users. However, the country data is real and up-to-date, sourced from the World Bank API, reflecting the most recent information available from 2022.

## Machine Learning Models

### ML Model 1 and Explanation
For predicting the number of protests events per capita in a desired country we chose three key features: public trust of their government, GDP per capita, and whether the country is Western, Asian, or South American. These features are used in our linear regression model.

- Public Trust in the Government: This reflects citizens' confidence in their government, distinguishing countries based on political and social trust metrics.
- GDP per Capita: This indicates economic prosperity and helps group countries with similar economic structures and living standards.
- Region: This indicates where this country is located in the world to identify groups of countries of similar economic structure, government, and culture. The country is classified as one of Western (The US, Canada, and European countries), Asian (countries in Asia), and South American (countries in South America).

How does our linear regression model work?
1. Initialization: 
* Use cross validation to split the data into training and testing sets 
* Add an interaction term between GDP per capita and public trust due to them being highly correlated to capture how these features interact in predicting protests events per capita
* Add additional polynomial features (to the 2nd and 3rd degree) for public trust and GDP per capita to capture non-linear relationships between these features and protests events per capita
* All of these features are combined into a single matrix (training data) and linear regression is used for fitting the model to this data, outputing the line of best fit 
2. Predict: Takes in each of the features the user is supposed to input (public trust, GDP per capita, and region), standardizes them, and puts each feature value into a vector to correspond to the slopes of the line of best fit. The vector includes the following values:
* Scaled public trust percentage
* Scaled GDP per capita
* Polynomial features (to the 2nd and 3rd degree) of both features
* Categorical features encoded as 1 for the selected region and 0 for others
It multiplies the input vector with the line of best fit vector (coefficients) to get the predicted value (estimated events per capita).

![alt text](https://i.imgur.com/aR7LPxs.png)
Residual vs. Index: I did not notice much of a pattern in the residuals so I believe the no autocorrelation assumption can be met.
![alt text](https://i.imgur.com/DD4HUpK.png)
Residual vs. Public Trust Percentage: Most of the residuals are centered around 0 but there are a few outliers in which my model underpredict when public trust percentage is high. This could be due to not having enough training data that included high public trust percentages.
![alt text](https://i.imgur.com/pkilmdV.png)
Residuals vs GDP per Capita: Most of the residuals are centered around 0 but there is 1 outlier in which my model underpredict when gdp per capita is extremely above average. This could be due to not having enough training data that included very high gdp per capita values.
![alt text](https://i.imgur.com/y5MpPHv.png)
Residuals vs Western: Since this feature is categorical, it makes sense that the residuals are only scattered at x = 0 and x = 1 and are centered around 0.
![alt text](https://i.imgur.com/pukWP8W.png)
Residuals vs Asia: Since this feature is categorical, it makes sense that the residuals are only scattered at x = 0 and x = 1. While most of the residuals are centered around 0 for the residuals where x = 0 above and below 0 on the y axis, the spread of residuals is much wider when predicting a country to be not asian vs asian. This could be due to a training data imbalance of not having as many Asian countries information. 
![alt text](https://i.imgur.com/t9JbJBF.png)
Residuals vs South America: Since this feature is categorical, it makes sense that the residuals are only scattered at x = 0 and x = 1. While most of the residuals are centered around 0 for the residuals where x = 0, there are more residuals below 0 than above 0 where x = 1 which means my model is underpredicting. This could be due to a training data imbalance not having as many South American countries information. 
![alt text](https://i.imgur.com/dJqL43P.png)
Residuals vs Public Trust x GDP per Capita: Most of the residuals are centered around 0 but there are 3 outliers where public trust x gdp per capita are very high and my model underpredicts. This makes sense as a similiar relationship was shown in the residuals vs GDP per Capita graph, showing that GDP per Capita influences the residuals behavior in this graph.

### ML Model 2 and Explanation

For clustering countries using the k-means algorithm, we chose three key features: GDP per capita, protests per capita, and public trust in the government. These features were also used in our linear regression model.

- GDP per Capita: This indicates economic prosperity and helps group countries with similar economic structures and living standards.
- Protests per Capita: This measures social and political stability, helping to differentiate countries based on civic engagement and unrest levels.
- Public Trust in the Government: This reflects citizens' confidence in their government, distinguishing countries based on political and social trust metrics.

How does k-means clustering work?

1. Initialization: Randomly select kkk initial centroids.
2. Assignment: Assign each data point to the nearest centroid.
3. Update: Recalculate centroids by averaging the data points in each cluster.
4. Convergence: Repeat the assignment and update steps until centroids stabilize or a set number of iterations is reached.

#### Cluster results

Cluster 0
['Brazil' 'Chile' 'Colombia' 'Costa Rica' 'Estonia' 'Greece' 'Hungary'
'Japan' 'Latvia' 'Lithuania' 'Mexico' 'Poland' 'Portugal' 'Slovenia']

Cluster 1
['France' 'Iceland' 'Israel' 'Italy' 'Spain' 'Sweden']

Cluster 2
['Ireland' 'Luxembourg' 'Norway']

Cluster 3
['Australia' 'Austria' 'Belgium' 'Canada' 'Denmark' 'Finland' 'Germany'
'Netherlands' 'Switzerland' 'United Kingdom' 'United States']

![alt text](https://lh3.googleusercontent.com/pw/AP1GczMvL5DE6k3tmitaXrLGjrCzXYRyCYbADulf5dvGrDsNCkVMULCPHdxjPpUlKxM5MvfHROvDvh6Q0_5gIAsLdz0im3pUkwqEXnFhA4FEuko7xISke-Qx=w2400)

## API Routes

### Posts

GET “api/post/”

- Gets all posts

PUT “api/post/{postId}”

- Updates the post at the given post id.

POST “api/post”

- Creates a new post

DELETE “api/post/{postId}”

- Deletes a post at the given post id.

### Protests

GET “api/protest/”

- Gets all protests

PUT “api/protest/{protestId}”

- Updates the protest at the given protest id.

POST “api/protest”

- Creates a new protest

DELETE “api/protest/{protestId}”

- Deletes a protest at the given protest id.

### Users

POST “api/user/saved_protest”

- Adds a protest to a user’s saved protest table

### Countries

GET “api/country/”

- Gets all countries

### Machine Learning

POST “api/ml/model1”

- Makes a call to the model 1 python script that makes a prediction

POST “api/ml/model2”

- Makes a call to the model 2 python script that makes a prediction

## Streamlit Application

Provide screenshots of the mocked up app and results of the implemented functionality, including calling the ML model.

1. Home page select user
![image](https://i.imgur.com/Pi4ftz6.png)
2. View posts

3. Update/delete post page

Screenshots to come (sorry!) - stay tuned for demo.
