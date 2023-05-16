# Analysis of food.com Recipes
Project for DSC 80 at University of California San Diego

---
# Introduction

The following dataset was downloaded from [food.com](https://www.food.com) as two datasets: one containing receipes and their specific attributes and another with ratings and their reviews of recipes. We merged these datasets into one to be able to answer the following question: is there a relationship between the number of steps in a recipe and the average rating of that recipe?. 

---
# Data Cleaning

---
# Univariate Analysis

---
# Bivariate Analysis
<iframe src="assets/bivariate-plot.html" width=800 height=600 frameBorder=0></iframe>

The plot above is a scatter plot of n_steps versus average rating (where duplicate `id` rows were dropped as `n_steps` and `average_rating` are the same for the same recipe). From the scatter plot, we can see a general trend where recipes with more steps have a lower proportion of recipes with a low `average_rating` compated to recipes with less steps; this would also convey that recipes with more steps have a higher proportion of recipes with a higher average rating compared to recipes with less steps. This graph, therefore, possibly indicates that--with further analysis needing to prove it--recipes with more steps, on average, are more likely to have a higher average rating.

---
# Data Aggregates
<iframe src="assets/pivot_table_steps.html" width="800" height="600" frameborder="0"></iframe>

---
# NMAR Analysis

---
# Missingness Dependency Analysis

---
# Hypothesis Testing
