---
title: "Phase 3 Reflection"
date: 2024-05-17
draft: false
description: "Reflection for Individual Phase 3 Assignment"
# slug: "first"
tags: ["authors", "config", "docs"]
authors:
  - "sierra_welsch"
showAuthorsBadges : false
---

## Phase 3: Reflection
This week of the dialogue was very fun. I really enjoyed our time in Luxembourg and I felt I got closer to a lot more of my classmates on the trip. Dr. Gerber, some of my peers, and I went on a 6 mile hike South of Luxembourg on Saturday and I really enjoyed it. Although I enjoy going for walks and being out in nature, I had never hiked before so I was nervous about how long the hike was but it felt like it was over before I knew it. We saw so many beautiful views of fields, greenery, and the hills of Luxembourg. I think it might have been my favorite day on this dialogue so far. On Sunday, I went biking under the bridge close to the hotel which was also a lot of fun. I had not biked in a while so it was nice to try again, despite having fallen twice! I am glad that we got to spend the weekend in Luxembourg,  celebrate Sonia and Sydney's birthday, and have a few days off to truly explore.

## Contributions
For phase 3, I worked on implementing the first machiene learning model. I helped experiment with the features we had in our dataset to see which best predicted protest events per capita. I noticed that two features that helped predict had a high correlation value when I computed the correlation matrix, so I had to define these features as an interaction term in our training matrix and experimented with rasing certain features to the 2nd and 3rd degree to capture the non linear patterns in our data. These contributions yielded a r2 score of 0.32 which although isnt high was something I thought was decent considering our target value. I also helped integrate the routes to insert the line of best fit coefficients and my data in csv files into the database and retrieve these values. 