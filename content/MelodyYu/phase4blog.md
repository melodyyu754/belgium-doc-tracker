---
title: "Phase 4: Final Week in Belgium"
date: 2024-06-10
draft: false
description: "Mines, Energy, and Rallify"
# slug: "first"
tags: ["authors", "config", "docs"]
authors:
  - "melody_yu"
showAuthorsBadges: false
---

## Phase 4: Final Stretch of the Project

It's been a fun last week, with lots of time working on the project! This has definitely been my favorite phase of the project, as I've enjoyed seeing the frontend of the app really come together. We have made massive improvements to the visuals and functionality of our project from our Phase 3 demo, and I am excited to be able to show it off during the presentation.

This week, I learned about and used K-Means Clustering to cluster the countries we have in our database. I chose the features GDP per capita and Protests per 100,000 people because it felt the most intuitive and useful for users - the clusters make sense, and they are what we trained our linear regression model on as well. I really enjoyed building out the UI with the maps - plotly and streamlit have some awesome built-in tools.

I also helped with the creation of the 'cards' - instead of displaying all of our data in a dataframe in Streamlit, we created custom cards and looped through the data. We created update and delete buttons on each card (that belonged to the logged in user) for more intuitive use. When the update button was clicked, it redirected to an Update page that was preloaded with the correct data.

Overall, I really enjoyed working on this project. It was really cool to see the entire project come together, and I feel like I have a good grasp on the codebase and how everything interacts.

### Resume

Rallify (MySQL, Flask, Streamlit)
- Developed a data-driven, containerized web application empowering political protests globally.
- Implemented key features enabling international comparison, k-means clustering, and customizable filtering of data.

### Model 2 notebook
<a href="./model2.ipynb" download>Link Text</a>
