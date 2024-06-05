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

TODO: (Sierra) What features are we using for the ML model? Provide reasonable explanation why those features are the chosen ones. Discuss any major/surprising issues found during model exploration.

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


![A cute cat](assets/output.jpg)


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
2. View posts
3. Update/delete post page

Screenshots to come (sorry!) - stay tuned for demo.
