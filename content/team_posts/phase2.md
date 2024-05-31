---
title: "Project - Phase II"
date: 2024-05-28
draft: false
description: "Updates to Idea"
slug: "phase2post"
tags: ["authors", "config", "docs"]
authors:
  - "melody_yu"
  - "sierra_welsch"
  - "sonia_sheth"
  - "maggie_tong"
showAuthorsBadges: false
---

# Phase 1 Updates

In the first phase, we had the activist’s main functionally be posting for their area of interest and opinions on the protests so they can spread awareness and create dialogue with other activists. We kept this consistent in the second phase but fleshed out the concept more by centering their app interaction around posting and interacting with other activist posts. To organize this information, we implemented the idea of tags by relating them to causes that the activist is following. We also introduced the concept of updating protests so that those following it, whether it be an activist or journalist, can get real time data on user created protests. The activist’s main page will have a sidebar with all the protests within the database listed and then they will have the option to filter through the protests based on the location, time, or issue. They can also toggle from viewing protests to news articles with a similar filtering functionality.

The journalist’s main functionality within the first phase was to purely view data, protests and new articles. In the second phase, we are adding the ability of journalists to create posts where they can connect with activists to conduct interviews and poll users on issues. Journalists can also follow/star content of both sides of a protest, sources and articles useful for them and interviews they have scheduled in the rightmost panel.

There was not much change in the user stories for the politician between the first and second phase, they are able to select data based on different countries to view statistics on a global scale and observe trends based on this data. They are also able to view protests, news and country data but will not be able to post.

Our (mostly) finalized functionalities:
1. Protest Database: A searchable, filterable database of protests, allowing users to add, view, and update information about upcoming or past events.
2. Forum: A platform for activists, politicians, and journalists to share thoughts, insights, and engage in discussions related to activism and social issues. This will look similar to a chronological social media page (think Strava, Reddit), and will also have filtering abilities.
3. News Querying: A tool to help users search for current news relating to their topic of interest. They can also save news of interest.
4. Interactive Model: A tool that allows users to interact with the model we’ve created, providing insights or predictions related to activism and social movements.


## Data

Phase II team blog post sections cont’d:
Provide reasoning for Data Viz choices and interpret results in context of big questions of interest
Include information about preliminary implementation of ML model (e.g. difficulties, tasks remaining, etc.)

The model we focused on was the relationship between GDP per capita and protests per capita. We first accessed the complete database
of protests via the ACLED api, joining it with Global Bank Data (population and GDP per capita). We initially started with just a couple of European
countries, but realized that we needed a wider range of countries and GDP per capitas. We included democratic countries from five continents (North America, South America, Europe, Asia, and Australia).

### Worldwide GDP per Capita vs. Protests per Capita
![Alt Text](https://lh3.googleusercontent.com/pw/AP1GczPyITPd3s4OSpKnKKfhjw2BCS_WcIf7ecIM2gBzES4ulvKExynqBG9AanHTEoTMRRq7xlCxafoGWfeag7pvE-SWvIim7osb_EqwEcNZMcxu8W0PdjRm=w2400)

Upon looking at the worldwide graph, we added columns for each geographical area (Western, Asia, South America), and plotted per area as well.

### Western GDP per Capita vs. Protests per Capita
![Alt Text](https://lh3.googleusercontent.com/pw/AP1GczNS6yJxxBTQ4IntiRZWyQh9pjkqRhF6T64mYOiXeVp68SWbXgSirA0uSRXRqoCwtKMZ6KXe42xlc5d72yY8158fKoc5-awpa4NHSzOPrnBn_9ixB3tb=w2400)

In this graph we noticed an increase in events per capita per increase in gdp per capita up until gdp per capital reached 40k and then noticed another interval of increase from 40k to 60k.

### South America GDP per Capita vs. Protests per Capita
![Alt Text](https://lh3.googleusercontent.com/pw/AP1GczOtSPxumBytDU5wYYlqI0oZWn1IP8m9OjDa6M9T7dpf2gS2Bx9s2FWL99K65ZkPavrcjVgGD5-Ldj-hS__lHSmOm-6_OZ9DRGRof7SInJRap8kOXfES=w2400)

In this graph we noticed an obvious increase in events per capita per increase in gdp per capita up until gdp per capital reached 20k. This shows a positive correlation between gdp and number of protests which we found interesting as a 3rd world country.

### Asia GDP per Capita vs. Protests per Capita
![Alt Text](https://lh3.googleusercontent.com/pw/AP1GczMMVe45FPeLsKSlSTVElvy3yDc41bu_Jg0R_Crhir5m_qigUQys3q24gVuXe64cDctYRrLALWMcOTViFjc8caL6v9jtN47VeMYz6Rvi6xehLBErtVWN=w2400)

In this graph we noticed a slight increase in events per capita per increase in gdp per capita for each country respectively but there is not as much data for countries in Asia to state a clear relationship. 

### Poverty gap at $2.15 a day vs. Events per Capita
![Alt Text](https://lh3.googleusercontent.com/pw/AP1GczN_-nDF3_WPWkNWXXdJm8XFSPGR8EKjsadSHvc3c2ZwS-xqAdOAEZ5Do_udRhv5LCtW6ukKB8jXGG_v0Pt9tChqZn6xg8Nwfx3jZdsRK5xqz1h_XgGV=w2400)

In this graph we noticed there was not much of a clear relationship between people making less than or equal to $2.15 a day (in poverty) and number of protest events. This told us that this indicator is likely a bad measure of determining the amount of protests in an area.

### Public Trust of the Government vs GDP per Capita vs Events per Capita
![Alt Text](https://lh3.googleusercontent.com/pw/AP1GczOosJfgDw-773fBU1D5H0Mf6j-v06GR7ObsNaIYNKanw1jhfBK_e7JSCY0wcF7JLDv9p6DhX2ag4FK6V5hkhbP3OQ9J7v3M1evFbz_J6alVId7mwek0=w2400)

In this graph we noticed a linear increase in events per capita per increase in gdp per capita up per public trust percentage although there are some points that do not follow this patttern. This could indicate that public trust and gdp per capita together both are positively correlated with events per capita although it is not the clearest increasing shape of a line.

### Linear Regression
We decided to fit a linear regression model to our data (for the time being).

![Alt Text](https://lh3.googleusercontent.com/pw/AP1GczMYcVWov80nnXn7gSHc6-YGWUk59IUkHsuYPBYOW85OVEOenw9ZgpSUkNVqzF4jeNOefaWSBEeNFCbv1DCBdMWpVbsiUDDFkCH3lCBlV8h3S2Ap_yJP=w2400)
This analysis shows that when both public trust and GDP per capita are at zero, the number of protest events per capita is 4.7. Increasing public trust by one unit decreases the number of protests by 0.9%. Additionally, a one unit increase in public trust results in a 0.002% increase in GDP per capita. There appears to be a slight negative relationship between public trust and the number of protests, but the relationship between public trust and GDP per capita is minimal. To better understand these relationships, adding more relevant features to our model might strengthen the observed connections and increase the complexity of our model.Given that the current values do not show strong relationships, we might consider using a more complex model or combining features and fitting a quadratic curve to better represent our data in future phases of the project.



<!-- Activist Page
![Alt Text](https://lh3.googleusercontent.com/pw/AP1GczM7mlCdhIiJYA29e-HAUXbfFYMuLyzIE-FOB6-DnX0DNa_c3h77zc1qQjYIhBQR_qJMYjfD6puX4O_3AJJ1dI0_oaY-TlkShFc_6Z1kVJW9e8uWAcP6=w2400) -->



## Localized ER Diagrams

In the following below are the localized ER diagram for our various personas: Journalist, Activist, and Politician.

### Journalist ER

Journalist ER
![Alt Text](https://lh3.googleusercontent.com/pw/AP1GczON6egIFFCIp9Tjxc7mnC4aY7cyIWWUbcTL2ztVDJeQMa3Rz5lUL8eDdlpTE9iu9-u7fCFroXQOOUFALM5eygfb5e94ROZN4okmEzj06V8-6RGIJ9Eq=w2400)

### Activist ER

Activist ER
![Alt Text](https://lh3.googleusercontent.com/pw/AP1GczMHZYJOGd137eM6Yoy46PQ6eePLAr9UteEt0x8tLARW-ddCK0jKZrcKX7Y4SvGfcd3yUkovaw-PRwYAuvBC4OCTkegn-0Fl3viwxdLy20txChe1BJXE=w2400)

### Politician ER

Politician ER
![Alt Text](https://lh3.googleusercontent.com/pw/AP1GczPVCKmXqGAT1PIlMiZac1QPGdY0WTerpuC_6wHfmMlKtqNfYa1jhnGCSRmiyGbVf3FrMjmFFDDqV2jcUJkU3GpLjbLsOMVWLAcmZfLoW5JKs_VBSGYO=w2400)

## Global ER model

![Alt Text](https://lh3.googleusercontent.com/pw/AP1GczNLGqmiJEkCfXM_QGwBhC0moVwDNV8agDPr9VCofO9eV53qcyAm6VAXlvDCbOB8A_hU5jRRDGCX9AZ0n-4dlrTRB6VkKCZXbJeni5kBS-44fvY5SKZ4=w2400)

## SQL DDL for Global Data Model

![Alt Text](https://lh3.googleusercontent.com/pw/AP1GczNiSii5cuO1IIqk-EUHQSlHX7VZ7V3TdB1dQWTmPfEFiURUBFiWvzjpZjZKgcXPVJBcc5Utn7OYI2DeMLZs4YqzPiOdtOX3KtnKcwYMohy3JZVyhjaR=w2400)

## Draft WireFrames

Wireframes of each POC - the Journalist, Activist and Politician - were created to depict what various pages of our application will look like.

### Activist Page
![Alt Text](https://lh3.googleusercontent.com/pw/AP1GczM7mlCdhIiJYA29e-HAUXbfFYMuLyzIE-FOB6-DnX0DNa_c3h77zc1qQjYIhBQR_qJMYjfD6puX4O_3AJJ1dI0_oaY-TlkShFc_6Z1kVJW9e8uWAcP6=w2400)

### Politician Page
![Alt Text](https://lh3.googleusercontent.com/pw/AP1GczO7V58dsL9e37-fLE0xD7FK7YReCPdYZ9tffa-09xWY4CSCrk3-WJuK2Q9NbY6xqxzcSHLNZAJXXOiCxjufRasGxQhP54QWMrDDTNhAhliuKj_9pTYH=w2400)

### Journalist Page
![Alt Text](https://lh3.googleusercontent.com/pw/AP1GczM-kuouqoMCsbXfnG8TGw6uYCOToC-OTKp8g7i0nBKRCVVvYic_GvB8WN9Dh_8wpP7vQ6Mobqxd6TYoCrAhVp2QwTTNIzBOCZqm_wKemX9iJPJlKR9G=w2400)