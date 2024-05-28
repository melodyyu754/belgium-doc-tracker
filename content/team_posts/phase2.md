---
title: "Project - Phase 2"
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

## Phase 1 Updates

Any updates to your Phase I proposal that you decided to make during Phase II work
Did you modify/change a persona or user story?
Did you find a new data set that you plan to use for ML modeling?

## Data

Phase II team blog post sections cont’d:
Provide reasoning for Data Viz choices and interpret results in context of big questions of interest
Include information about preliminary implementation of ML model (e.g. difficulties, tasks remaining, etc.)

The model we focused on was the relationship between GDP per capita and protests per capita. We first accessed the complete database
of protests via the ACLED api, joining it with Global Bank Data (population and GDP per capita). We initially started with just a couple of European
countries, but realized that we needed a wider range of countries and GDP per capitas. We included democratic countries from five continents (North America, South America, Europe, Asia, and Australia).

Worldwide GDP per Capita vs. Protests per Capita
![Alt Text](https://lh3.googleusercontent.com/pw/AP1GczPyITPd3s4OSpKnKKfhjw2BCS_WcIf7ecIM2gBzES4ulvKExynqBG9AanHTEoTMRRq7xlCxafoGWfeag7pvE-SWvIim7osb_EqwEcNZMcxu8W0PdjRm=w2400)

Upon looking at the worldwide graph, we added columns for each area (Western, Asia, South America), and plotted per area as well.

Western GDP per Capita vs. Protests per Capita
![Alt Text](https://lh3.googleusercontent.com/pw/AP1GczNS6yJxxBTQ4IntiRZWyQh9pjkqRhF6T64mYOiXeVp68SWbXgSirA0uSRXRqoCwtKMZ6KXe42xlc5d72yY8158fKoc5-awpa4NHSzOPrnBn_9ixB3tb=w2400)

South America GDP per Capita vs. Protests per Capita
![Alt Text](https://lh3.googleusercontent.com/pw/AP1GczOtSPxumBytDU5wYYlqI0oZWn1IP8m9OjDa6M9T7dpf2gS2Bx9s2FWL99K65ZkPavrcjVgGD5-Ldj-hS__lHSmOm-6_OZ9DRGRof7SInJRap8kOXfES=w2400)

Asia GDP per Capita vs. Protests per Capita
![Alt Text](https://lh3.googleusercontent.com/pw/AP1GczMMVe45FPeLsKSlSTVElvy3yDc41bu_Jg0R_Crhir5m_qigUQys3q24gVuXe64cDctYRrLALWMcOTViFjc8caL6v9jtN47VeMYz6Rvi6xehLBErtVWN=w2400)

We decided to fit a linear regression model to our data (for the time being).

Activist Page
![Alt Text](https://lh3.googleusercontent.com/pw/AP1GczM7mlCdhIiJYA29e-HAUXbfFYMuLyzIE-FOB6-DnX0DNa_c3h77zc1qQjYIhBQR_qJMYjfD6puX4O_3AJJ1dI0_oaY-TlkShFc_6Z1kVJW9e8uWAcP6=w2400)

Politician Page
![Alt Text](https://lh3.googleusercontent.com/pw/AP1GczO7V58dsL9e37-fLE0xD7FK7YReCPdYZ9tffa-09xWY4CSCrk3-WJuK2Q9NbY6xqxzcSHLNZAJXXOiCxjufRasGxQhP54QWMrDDTNhAhliuKj_9pTYH=w2400)

Journalist Page
![Alt Text](https://lh3.googleusercontent.com/pw/AP1GczM-kuouqoMCsbXfnG8TGw6uYCOToC-OTKp8g7i0nBKRCVVvYic_GvB8WN9Dh_8wpP7vQ6Mobqxd6TYoCrAhVp2QwTTNIzBOCZqm_wKemX9iJPJlKR9G=w2400)

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
![Alt Text](https://lh3.googleusercontent.com/pw/AP1GczON6egIFFCIp9Tjxc7mnC4aY7cyIWWUbcTL2ztVDJeQMa3Rz5lUL8eDdlpTE9iu9-u7fCFroXQOOUFALM5eygfb5e94ROZN4okmEzj06V8-6RGIJ9Eq=w2400)

## Global ER model

![Alt Text](https://lh3.googleusercontent.com/pw/AP1GczNLGqmiJEkCfXM_QGwBhC0moVwDNV8agDPr9VCofO9eV53qcyAm6VAXlvDCbOB8A_hU5jRRDGCX9AZ0n-4dlrTRB6VkKCZXbJeni5kBS-44fvY5SKZ4=w2400)

## SQL DDL for Global Data Model
![Alt Text](https://lh3.googleusercontent.com/pw/AP1GczNiSii5cuO1IIqk-EUHQSlHX7VZ7V3TdB1dQWTmPfEFiURUBFiWvzjpZjZKgcXPVJBcc5Utn7OYI2DeMLZs4YqzPiOdtOX3KtnKcwYMohy3JZVyhjaR=w2400)

## Draft WireFrames

Wireframes of each POC - the Journalist, Activist and Politician - were created to depict what various pages of our application will look like.

### Journalist Page

### Activist Page

### Politician Page
