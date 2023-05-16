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

The pivot table above looks at the distribution of average ratings (grouped together in intervals of 1 to better visualize any possible trends) for each `n_steps` value in the dataframe. This is interesting as it allows one to potentially point out any possible relationship between the two variable to further explore.

---
# NMAR Analysis

---
# Missingness Dependency Analysis


---
# Hypothesis Testing

As stated previously, we chose to explore the relationship between the number of steps in a recipe and the average rating of that recipe. To test this we set up the following permutation test:
**We define short recipes as recipes with less than 7 steps, medium recipes as recipes with less than 11 steps, and long recipes as those with 11 or more steps.** These values were chosen carefully as to split the number of recipes in each category evenly (roughly 33% of the data in each category).

**Null hypothesis:** There is no observable relationship between the number of steps in a recipe and the average rating of that recipe.
**Alternative hypothesis:** There is a relationship between the number of steps in a recipe and the average rating of that recipe.

**Test Statistic:** TVD between short, medium, and long recipes with the overall mean of `average_rating`.
**alpha = 0.05**

plot

**P-value = 0.01**
**Conclusion:** Because p-value = 0.01 < alpha level = 0.05, we reject the null hypothesis that there is no observable relationship between the number of steps in a recipe and the average rating of that recipe. There is statistically significant evidence that there is a relationship between the number of steps in a recipe and the average rating of that recipe. 


**Reasoning:** In order to test our question, we needed to run a permutation test as we do not have a sample (). Therefore, we chose to create three labels for the `n_steps` variable. As mentioned before, we split the data into the three categories in order to split the number of recipes in each category evenly (roughly 33% of the data in each category). This was done to unbiasedly split up the data for the permutation test. We chose an alpha level of 0.05 as this is a common alpha level for statistical tests. And because our p-value was less than the alpha level, we rejected the null hypothesis and stated that we had statistically significant evidence for the alternative hypothesis.
