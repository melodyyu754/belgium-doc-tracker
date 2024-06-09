---
title: "Project - Phase IV"
date: 2024-06-10
draft: false
description: "Rallify - Final Application"
slug: "phase3post"
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

### Machine Learning Models

#### Model 1 - Linear Regression

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

μ₁' = (1/N) * Σ x₁ 

μ₂' = (1/N) * Σ x₂ 

    Where:
    - N = number of countries in the cluster
    - Σ denotes the sum over all countries in the cluster

5. Repeat: Repeat steps 3 and 4 until the cluster centers (μ) no longer change significantly (or until a maximum number of iterations is reached).

