# Analysis of food.com Recipes
Project for DSC 80 at University of California San Diego

Authors: Joey Kaminsky and Ishaan Chadha

---
# Introduction

The following dataset was downloaded from [food.com](https://www.food.com) as two datasets: one containing receipes and their specific attributes and another with ratings and their reviews of recipes. We merged these datasets into one to be able to answer the following question: is there a relationship between the number of steps in a recipe and the average rating of that recipe?

This is an important question in the world of cooking. From this question, we can gain some insight as to whether the number of steps in a recipe factors into its rating. This can influence cooks to edit the number of steps in their new recipes in the hopes of a greater rating by reviewers.

After cleaning the data, this dataset has 234,429 rows and 26 columns (234,429 rows and 18 columns prior to cleaning the data). In order to get familiar with the dataset, here are some important columns that will be mentioned:

- `name`: name of the recipe
- `id`: the id of a recipe, where the same recipe has the same value for this column 
- `n_steps`: the number of steps in the recipe
- `user_id`: reviewer of the recipe `user_id`
- `rating`: the rating given for the recipe by the reviewer, `user_id`
- `average_rating`: the mean rating of a recipe `id`; recipes with the same `id` have the same value for this column

---
# Data Cleaning
<iframe src="assets/table.html" width=800 height=600 frameBorder=0></iframe>



There is a list of data cleaning steps that were followed in order to make the analysis of the relationship between the number of steps in a recipe and its average rating easier and more accurate.

* **Merging Dataframes:**
   The merging of the `recipes_df` and `interactions_df` dataframes allows for a comprehensive analysis by combining recipe information with interaction data. It ensures that the average rating of each recipe can be accurately calculated and associated with the corresponding recipe.

* **Handling Missing Ratings:**
   By replacing zero values in the `rating` column with 'NaN', we distinguish between missing ratings and zero ratings. This step ensures that the calculation of the average rating is not skewed by zero values and allows for a more accurate assessment of the relationship between the number of steps and the average rating.

* **Calculating Average Ratings:**
   The calculation of the average rating for each recipe provides a single value representing the overall rating. This average rating serves as a metric to measure the recipe's quality and popularity, allowing for comparisons and analysis based on the aggregated ratings.

* **Cleaning the name Column:**
   Cleaning the `name` column by removing leading and trailing white spaces has a negligible effect on the analysis of the relationship between the number of steps and the average rating. It ensures data consistency and avoids potential inconsistencies in subsequent analyses.

* **Cleaning the submitted Column:**
   Converting the `submitted` column to a datetime format ensures that temporal information can be properly analyzed, but it has no direct impact on assessing the relationship between the number of steps and the average rating.

* **Cleaning the tags Column:**
   Cleaning the `tags` column ensures that the tags are transformed into a suitable format for analysis. However, the 'tags' column is not directly related to the analysis of the relationship between the number of steps and the average rating.

* **Cleaning the nutrition Column:**
   The cleaning of the `nutrition` column and extracting specific nutrition values have no direct impact on analyzing the relationship between the number of steps and the average rating. These nutrition values may be useful for exploring other aspects of the dataset.

* **Cleaning the steps Column:**
   Cleaning the `steps` column by splitting the string into a list of individual steps and removing unnecessary characters allows for a structured analysis of recipe steps. It enables us to make sure that the `n_steps` column has correct data and is in accordance with the the number of steps listed in teh `steps` column. This ensures that the data is accurate, which is crucial for assessing the relationship with the average rating.

* **Cleaning the description Column:**
   Cleaning the `description` column by replacing missing values with 'MISSING' has no direct impact on the analysis of the relationship between the number of steps and the average rating. However, it ensures that missing descriptions are appropriately identified and handled.

* **Cleaning the ingredients Column:**
    Cleaning the `ingredients` column by splitting the string into a list of individual ingredients and removing unnecessary characters has no direct impact on analyzing the relationship between the number of steps and the average rating. It facilitates structured analysis of the ingredients but does not influence the relationship.

* **Cleaning the date Column:**
    Converting the `date` column to a datetime format ensures proper handling of temporal information. While it may be relevant for other time-related analyses, it does not directly affect the analysis of the relationship between the number of steps and the average rating.

* **Cleaning the review Column:**
    Cleaning the `review` column by replacing HTML entities ensures the readability and consistency of the review text. This cleaning step is not directly related to analyzing the relationship between the number of steps and the average rating.

* **Dropping the recipe_id Column:**
    Dropping the `recipe_id` column after the merge operation does not affect the analysis of the relationship between the number of steps and the average rating.
    
Overall, by following these steps and cleaning the data, we made the analysis of the relationship between the number of steps in a recipe and its average rating easier and more accurate.

---
# Univariate Analysis #
<iframe src="assets/univariate-plot.html" width=800 height=600 frameBorder=0></iframe>

In this analysis, we examine the box plot representation of the "n_steps" column, which provides insights into the distribution of step lengths in recipes. The box plot reveals that, on average, recipes tend to have around 6 to 13 steps. The box plot's median line represents the middle value of the dataset, showing that recipes typically have a step count of 9. A lower fence of 1 and an upper fence of 23 indicates that the length for almost all recipes lies between 1 and 23 steps. However, outliers are observed with step counts reaching 100, suggesting the presence of a few recipes with significantly more complex procedures.

---
# Bivariate Analysis
<iframe src="assets/bivariate-plot.html" width=800 height=600 frameBorder=0></iframe>

The plot above is a scatter plot of n_steps versus average rating (where duplicate `id` rows were dropped as `n_steps` and `average_rating` are the same for the same recipe). From the scatter plot, we can see a general trend where recipes with more steps have a lower proportion of recipes with a low `average_rating` compated to recipes with less steps; this would also convey that recipes with more steps have a higher proportion of recipes with a higher average rating compared to recipes with less steps. This graph, therefore, possibly indicates that--with further analysis needing to prove it--recipes with more steps, on average, are more likely to have a higher average rating.

---
# Data Aggregate
<iframe src="assets/pivot_table_steps.html" width="800" height="300" frameborder="0"></iframe>
The pivot table above looks at the distribution of average ratings (grouped together in intervals of 1 to better visualize any possible trends) for each `n_steps` value in the dataframe. This is interesting as it allows one to potentially point out any possible relationship between the two variable to further explore. Note that the column for 71 steps is all 0's; this is due to the fact that the only recipe with 71 steps had no review, so we replaced the `np.NaN` values with 0's.

---
# NMAR Analysis

The missingness in the `description` column could potentially be classified as NMAR based on the premise that the description might not be required since the recipe name itself could be self-explanatory.

Reasoning:
If users perceive that the recipe name adequately conveys the essential information about the dish, they may choose not to provide a description. In such cases, the missingness in the `description` column would be driven by the nature of the recipe itself rather than random or observable factors, suggesting the presence of NMAR.

Additional Data and Strategies:
1. Recipe Complexity Measures: Obtaining additional data or create new variables that capture the complexity or novelty of each recipe. This could include metrics such as specific culinary techniques required. Analyzing the relationship between recipe complexity and missingness in the `description` column could provide insights into whether the missingness is related to the inherent characteristics of the recipes.

2. User Experience and Expertise: Gathering information about the contributors' culinary experience, expertise, or familiarity with the specific cuisine. Contributors with more experience might be less likely to provide descriptions for recipes they are already familiar with, assuming that others would understand the recipe based on the name alone. Exploring this relationship between contributor expertise and missingness in the `description` column could help identify potential MAR patterns.

3. Recipe Category or Type: Categorizing or classifying the recipes based on their type, such as appetizers, main courses, desserts, etc. can help us explore whether missingness in the `description` column varies across different recipe categories. If there are consistent patterns within specific categories, it could provide insights into the missingness mechanism and help assess the MAR assumption.

By incorporating these additional data and strategies, it may be possible to explore alternative explanations for the missingness in the `description` column and evaluate whether the missingness can be considered MAR rather than NMAR. This deeper understanding can guide appropriate data handling techniques and mitigate potential biases caused by missing values during subsequent analysis.

---
# Missingness Dependency Analysis
<iframe src="assets/emperical_dist_description_n_steps.html" width="800" height="600" frameborder="0"></iframe>


<iframe src="assets/emperical_dist_description_rating.html" width="800" height="600" frameborder="0"></iframe>

---
# Hypothesis Testing

As stated previously, we chose to explore the relationship between the number of steps in a recipe and the average rating of that recipe. To test this we set up the following permutation test:

**We define short recipes as recipes less than 9 steps and long recipes as those with 9 or more steps.** This value was chosen carefully as to split the number of recipes in each category evenly (roughly 50% of the data in each category).

**Null hypothesis:** There is no observable relationship between the number of steps in a recipe and the average rating of that recipe.

**Alternative hypothesis:** There is a relationship between the number of steps in a recipe and the average rating of that recipe.




**Test Statistic:** Absolute difference in mean of `average_rating` between short and long recipes.

**alpha = 0.05**

<iframe src="assets/perm-test-steps.html" width=800 height=600 frameBorder=0></iframe>


**P-value = 0.001**

**Conclusion:** Because p-value = 0.001 < alpha level = 0.05, we reject the null hypothesis that there is no observable relationship between the number of steps in a recipe and the average rating of that recipe. There is statistically significant evidence that there is a relationship between the number of steps in a recipe and the average rating of that recipe. 




**Reasoning:** In order to test our question, we needed to run a permutation test as we do not have both the population and a sample from that population. We only have two samples (short and long recipes) and no population. To run the permutation test, we chose to create two labels for the `n_steps` variable. As mentioned before, we chose 9 steps in order to split the number of recipes in each category evenly (roughly 50% of the data in each category). This unbiasedly split up the data for the permutation test. Because we are comparing two values (mean `average_rating` for short and long recipes), it is best for our test statistic to look at the absolute value of the difference between these two means. We chose an alpha level of 0.05 as this is a common alpha level for statistical tests. And because our p-value was less than the alpha level, we rejected the null hypothesis and stated that we had statistically significant evidence for the alternative hypothesis. 
