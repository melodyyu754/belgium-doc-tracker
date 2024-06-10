---
title: "Project - Phase IV"
date: 2024-06-10
draft: false
description: "Rallify - Final Application"
slug: "phase4post"
tags: ["authors", "config", "docs"]
authors:
  - "melody_yu"
  - "sierra_welsch"
  - "sonia_sheth"
  - "maggie_tong"
showAuthorsBadges: false
---

## Phase 4

### A Data-Driven Full-Stack Platform Empowering Political Protest Movements

### Executive Summary

Rallify is a full-stack application designed to empower political protest movements by fostering community, facilitating organization, and providing data-driven insights for effective action. The platform offers a suite of tools tailored to the unique needs of activists, journalists, and politicians, addressing critical challenges in coordination, communication, and strategic planning.

Key Features & Benefits:

- Community Forum: A dynamic hub where users can connect, share experiences, ask questions, and exchange ideas, fostering a sense of solidarity and collaboration across geographical boundaries. This feature enables the organic growth of movements, providing a space for knowledge-sharing and mutual support.
- Protest Database: A comprehensive, searchable repository of protests worldwide, filterable by cause, location, date, and other relevant criteria. This tool empowers activists to discover relevant events, coordinate with other groups, and identify potential allies, maximizing the impact of their efforts.
- Data-Driven Insights: Rallify leverages machine learning models to analyze protest data and provide actionable insights. These insights can help activists understand trends, predict turnout, and tailor their strategies for maximum effectiveness.

By addressing the core challenges faced by political protest movements, Rallify empowers activists to build stronger communities, organize more effectively, and make data-driven decisions that drive real-world change.

### Problem Statement

#### Activists

Activists are passionate individuals dedicated to driving social change, but they often face significant challenges in organizing and amplifying their efforts. Traditional methods of communication and coordination are often fragmented, insecure, and lack the reach needed to mobilize large groups effectively.

Rallify directly addresses these challenges by providing activists with a platform to connect with like-minded individuals, organize protests and events, and access data-driven insights to inform their advocacy efforts.

#### Politicians

Politicians need to understand and respond to the concerns of their constituents, especially those expressed through political protests. However, gaining accurate and timely insights into the scale, sentiment, and potential impact of protests can be difficult. Traditional methods of gauging public opinion are often slow, expensive, and prone to bias.

Rallify's machine learning models provide politicians with data-driven predictions about protest occurrence, enabling them to make informed decisions, tailor their responses, and engage in meaningful dialogue with their constituents.

#### Journalists

Journalists play a crucial role in informing the public about political protests and their impact on society. However, they often face challenges in accessing reliable information, verifying sources, and connecting with activists on the ground. Traditional news cycles can be slow to react to rapidly evolving situations, and journalists may struggle to provide nuanced coverage of complex issues.

Rallify offers journalists a centralized platform to access verified information about protests worldwide, connect with activists directly, and gain a deeper understanding of the issues driving these movements. The platform's data-driven insights can also help journalists provide more in-depth analysis and reporting.

### Technology Stack

Rallify's technical architecture uses a containerized approach using Docker to ensure modularity, scalability, and ease of deployment. The application is divided into three primary containers:

- Database (MySQL): A robust relational database for storing and managing protest-related data, ensuring data integrity and efficient querying.
- API (Flask): A Python-based RESTful API that handles data interactions and business logic, including integration with machine learning models for data-driven insights.
- Frontend App Container (Streamlit): A Python-based web application providing an intuitive user interface for accessing and visualizing protest data, as well as interacting with the API's functionalities.

The Flask API acts as the middleman between the SQL database and the frontend application. The API communicates with the SQL database through well-defined routes including select, update, delete, and inserts statements for data retrieval and/or modification. These routes are then invoked by the frontend application, which formats and presents the data in a user-friendly manner.

This modular architecture allows for independent scaling of each component and facilitates seamless deployment across different environments. The use of Docker containers streamlines the development process and ensures consistent behavior across local development machines and production servers.

### Database Model

The GlobalProtests database models a global network of political protests, their participants, and related information. Key entities and relationships include:

Core Entities:

- users: Represents individuals (activists, politicians, journalists) with different roles and affiliations. Linked to countries and posts/comments they create.
- protests: Details on specific protests, including location, date, description and links to the creator, country, and cause.
- posts: Forum posts created by users to discuss causes and protests.
- country: Stores country-level data, such as protests per capita, population, GDP per capita, unemployment rate, urbanization rate, and inflation rate, to facilitate analysis of protests in context.
- cause: Defines the social or political issue a protest is addressing.

Relationships:

- protests-users: Tracks who created each protest.
- protests-country: Associates protests with their geographic location.
- protests-cause: Links protests to their underlying causes.
- posts-users: Indicates who authored each forum post.
- posts-cause: Associates posts with the cause they discuss.
- user_interests: Records users' interests to personalize their experience.
- users-country: Associates a user with their home country

#### Database Model: Looking Ahead

GlobalProtests includes some additional entities and relationships for additional functionality. Ultimately, these were features planned, but cut given time constraints. Yet, the foresight to leave them in the final database allows for seamless and rapid development of features in the future.

Entities:

- news-articles: Details news article reporting on current and past protest around the world
- comments: Represents a comment for a post

Relationships:

- protest_attendence: Many to Many relationship representing the protests each user has attended and the users who have attended each specific protest
- protest_likes: Many to Many relationship representing the protests each user has ‘liked/saved’ and the users who have liked specific posts
- news_likes: Many to Many relationship representing the users who have liked specific news articles and each news article a user has ‘liked/saved’

#### Database Model Evolution

Prior to designing our initial data model, our team spent adequate time planning our user stories and the functionalities we wanted to serve. Hence, our first data model was very concrete. Additional updates to the model included the addition / removal of some simple attributes, such as adding a publication date to the news articles and splitting name for the user into first name and last name. Other than that, all the relationships and core entities remained the same.

### Machine Learning Models

#### Model 1 - Linear Regression

For predicting the number of protest events and protest events per 100,000 people in a desired country we chose four key features: public trust of their government, GDP per capita, whether the country is Western, Asian, or South American, and population. These features are used in our linear regression model.

- Public Trust in the Government: This reflects citizens’ confidence in their government, distinguishing countries based on political and social trust metrics.
- GDP per Capita: This indicates economic prosperity and helps group countries with similar economic structures and living standards.
- Region: This indicates where this country is located in the world to identify groups of countries of similar economic structure, government, and culture. The country is classified as one of Western (The US, Canada, and European countries), Asian (countries in Asia), and South American (countries in South America).
- Population: This indicates the population of the country to better indicate how many people could protest.

##### How does our linear regression model work?

1. Initialization:

- Add an interaction term between GDP per capita and public trust due to them being highly correlated to capture how these features interact in predicting protests events per capita
- Add and transform additional polynomial features up to the 3rd degree for public trust, GDP per capita, and population to capture the nonlinear relationships between these features and protests events per capita
- All of these features are combined into a single matrix and linear regression is used for fitting the model to this data, outputting the line of best fit

2. Predict: Takes in each of the features the user is supposed to input (public trust, GDP per capita, and region), standardizes them, and puts each feature value into a vector to correspond to the slopes of the line of best fit. The vector includes the following values:

- public trust percentage (scaled)
- GDP per capita (scaled)
- Population (scaled)
- Polynomial features (to the 2nd and 3rd degree) of public trust percentage scaled, gdp per capita scaled, and population scaled
- Categorical features encoded as 1 for the selected region and 0 for others (Western, Asian, and South American)

It multiplies the input vector with the line of best fit vector (coefficients) to get the predicted value (estimated events per 100,000 people).
TODO: Insert image here
Residuals vs. Predicted Values: The points are randomly scattered around y = 0 (residuals = 0) which is good but the spread is much wider for predicted values above 0 than below indicating heteroscedasticity.
TODO: Insert image here
Residual vs. Index: We did not notice a pattern in the residuals so we believe the no autocorrelation assumption can be met.
TODO: Insert image here
Y vs Predicted Values: the points are relatively clustered around the line y = predicted_values but some are widely spread above and below this line (weakly clustered). Despite this, overall, this line captures the linear trend shown.
TODO: Insert image here
Histogram of Residuals Plot: The residuals are skewed to the left which indicates heteroscedasticity. This means the standard deviations of a predicted variable, monitored over different values of an independent variable or as related to prior time periods, are non-constant. Going forward, to address this in my model I would look into implementing the weighted least squares method into my model. This method assigns weights to each data point based on the estimated variance of the residuals. These weights are inversely proportional to the estimated variance of the residual for that point. Data points with higher estimated variance (farther away from the predicted line) receive lower weights and data points with lower estimated variance (closer to the predicted line) receive higher weights to give less emphasis to data points with high variance and more emphasis to those with lower variance. This should address the issue of non-constant variance (heteroscedasticity).
TODO: Insert image here
Residual vs. Public Trust Percentage: Most of the residuals are centered around 0 but there are a few outliers in which my model overpredicts and underpredicts when public trust percentage is high. This could be due to not having enough data that included very high public trust in government percentages (5-10 standard deviations above the mean). But, it also makes sense that the model does not predict data that has public trust percentages 5-10 standard deviations above and below the mean very well.
TODO: Insert image here
Residuals vs GDP per Capita: Most of the residuals are centered around 0 but there are a few outliers in which my model mostly underpredicted the value when gdp per capita becomes 10-30 standard deviations above the mean. (ASK ABOUT THIS) This could be due to not having enough training data that included very high gdp per capita values. But, it also makes sense that the model does not predict data that has public trust percentages 10-30 standard deviations above and below the mean very well.
TODO: Insert image here
Residuals vs Western: Since this feature is categorical, it makes sense that the residuals are only scattered at x = 0 and x = 1 and are centered around 0 with a relatively even spread. This implies homoscedasticity.
TODO: Insert image here
Residuals vs Asia: Since this feature is categorical, it makes sense that the residuals are only scattered at x = 0 and x = 1. While most of the residuals are centered around residuals = 0 and have an even spread, the spread of residuals is much wider when predicting a country to be not asian vs asian. This could be due to a training data imbalance of not having as many Asian countries information.
TODO: Insert image here
Residuals vs South America: Since this feature is categorical, it makes sense that the residuals are only scattered at x = 0 and x = 1. While most of the residuals are centered around 0 for the residuals where x = 0, there are more residuals below 0 than above 0 where x = 1 which means my model is over predicting but these points are not that far from residuals = 0. This could be due to a training data imbalance not having as many South American countries information.
TODO: Insert image here
Residuals vs Population: Most of the residuals are centered around 0 and despite there being a few clusters of outliers where population is very high above the mean, the residuals are still relatively centered around 0.

#### Model 2 - K-Means Clustering

We chose to do K-Means Clustering to determine what countries were most similar to each other and to predict what countries an inputted country's data is most similar to. We used the factors GDP per capita and Protests per 100,000 people to cluster.

Code snippet:
![image](https://i.ibb.co/zh6FX5q/Screenshot-2024-06-10-at-12-38-07-AM.png)

The steps of K-Means Clustering:

1. Choose K: The user starts by deciding how many clusters they want to find. Let's say they choose K=3.
2. Initial Centers: Randomly select K points (3 in our case) from the dataset. These initial centers are represented as μ₁, μ₂, and μ₃, where each μ is a pair of coordinates (GDP per capita, protests per 100,000 people).
3. Assign Countries: For each country (x), calculate its distance to each cluster center (μ) using the Euclidean distance formula:

- distance(x, μ) = √((x₁ - μ₁)² + (x₂ - μ₂)²)

4. Move Centers: For each cluster, calculate the new center (μ') by taking the average (mean) of the GDP per capita and protests per 100,000 people for all countries in the cluster:

μ₁' = (1/N) \* Σ x₁

μ₂' = (1/N) \* Σ x₂

    Where:
    - N = number of countries in the cluster
    - Σ denotes the sum over all countries in the cluster

5. Repeat: Repeat steps 3 and 4 until the cluster centers (μ) no longer change significantly (or until a maximum number of iterations is reached).

### Challenges and Lessons Learned

- Data Insertion: We mocked most of our data up in Mockeroo, however, it took a few tries of mocking up to get the inserts to run in DataGrip. There was an error with the data types for dates which requires a re-mock of all the data with dates.
- Button 404/500 Errors: Throughout development of the update and delete buttons, we experienced a lot of 404 errors. Initially, we didn’t know what this meant, however, we learned that it meant that the SQL statements in the routes being called didn’t work as intended. Sometimes this meant the particular attribute being looked for wasn’t being selected, that there was a formatting issue in the SQL statement, or a small naming issue with the query. we learned to look in the my-sql docker container for more info on the error and to log the output of the route/response for debugging.
- General SQL - API - Frontend Connection: We ran into so many overall issues when running our containers to connect the project together. Beginning errors typically involved the container not loading and we had trouble debugging when this happened. However, we stopped having this issue when we got more familiar with the environment and were able to read the error messages on docker. One of the errors we encountered initially was a ‘numpy’ error but after reviewing the ‘requirements.txt’ file and its purpose the issue was resolved by rebuilding with ‘docker compose build’.
- New Visions during Development: As development progressed, we changed our vision for how the user would be able to update / delete posts. Originally, we had two pages on the side bar for this functionality, but decided to switch gears and created a ‘My posts’ and ‘My protests’ page with buttons for deleting and updating. These led to a major change in our front end and more routes needed for our backend. But ultimately, with so little time, we wasted some of it on our original vision, which was scrapped. In the future, it would be best to flesh out user experience more before getting started on implementing it.
- Lack of Abstraction: Many of our front end pages are similar in the fact that they use the same function, create_card(), but simply have different routes being called. Originally, we thought it would be easier to ignore abstraction because of time constraints. However, it just lead to more time being spent on trying to find bugs/errors. If the code was abstracted, the same function would be used everywhere and we wouldn’t have had to comb through each file trying to find the tiny differences which led to an error.
- ML Feature Selection: When trying to choose features to fit our model, we noticed that while gdp per capita and public trust were good predictors of protest events per capita these features had a high correlation value. Linear regression assumes the features are independent of each other, so using these features would violate the assumption of multicollinearity. To ensure we were not violating this assumption, I added an interaction term between these two features to account for their relationship in predicting the target value.
- ML Accuracy: When we first trained our model our r2 score which reflects the accuracy of our model was relatively low with a simple linear regression model. I tried to experiment with transforming the numeric features to a higher degree to help capture the nonlinear behaviors of our data. This ended up improving the r2 score in predicting protest events dramatically (0.41) but increased the prevalence of heteroscedasticity in our model which is when the variance of the residuals (difference between the predicted and real y values) in a regression model is not constant across all predicted values of the dependent variable.
- Team Development + Merge Conflicts: Rapid development in a small team posed as an issue as it led to us as developers working on the same files, changing different functionality as times. This led to merge conflicts which had to be resolved in a tedious manner. Furthermore, some lack of communication and merging/commiting led to us writing the same route twice without the other knowing.

### Future Development
- New Articles Page: A page for journalists to view and filter for specific new articles related to their area of interest(s)
- Saved Protest/Posts: The ability for an activist/journalist to save protests/new articles that they are interested in via a like button and view their liked items on a separate page or under their profile.
- Commenting: The ability for a user to comment on a post and view all comments.
Protest Attendance: Display the users attending / who have attended a protest via an additional information button
- Abstracting Code: There are a few areas in which functions are similar and could be abstracted out to include parameters passed in.
