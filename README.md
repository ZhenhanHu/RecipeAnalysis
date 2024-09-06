# Exploring the Relationship Between the Rating of Recipes and the Number of Ingredients and the Number of Steps

# Introduction: <br>
Food.com is an online platform where people can view various types of food recipes and communicate about their food preparation experience. Based on the recipe, users have the chance to leave their ratings and reviews on specific recipes. And these recipes can be characterized by some of their quantitative features such as the number of ingredients that need to be prepared, the total number of steps for the entire process, the number of times estimated to prepare the recipe, etc. Thus, some interesting questions can be raised to explore the relationship between these features and their rating, and a prediction model using regression, for example, can be established to train and fit for recipe rating analysis.

This project will explore whether or not the number of ingredients in a recipe affects its rating. The key question that is being asked here is: **How does the number of ingredients in a recipe affect its rating?** This question is important, especially for people who love cooking and trying to design a new recipe, as such a relationship provides a helpful insight into how complexity influences satisfaction. If fewer ingredients correlate to a relatively high rating, the recipe designer might focus more on simplicity. On the other hand, if more ingredients correlate to a relatively high rating, designing complex recipes may be worth the effort.

The data from two datasets, `RAW_recipes` and `RAW_interactions` will be cleaned, assessed, and used for model construction. These datasets were originally scraped and used in a recommender system research paper, "Generating Personalized Recipes from Historical User Preferences", by Majumder et al.

`RAW_recipes` contains 83782 rows where each row represents a unique recipe and 12 columns where each column represents a unique descriptive feature. `RAW_interactions`, on the other hand, contains 731927 rows where each row represents a user commenting on a recipe (observation) and 5 columns on rating details. After the merge operation, there are 234429 rows, and the relevant columns are as follows:

| Column | Description |
| ----------- | ----------- |
| `'n_ingredients'` | Number of ingredients in recipe |
| `'n_steps'` | Number of steps in recipe |

# Data Cleaning and Exploratory Data Analysis <br>
## Data Cleaning <br>

## Univariate Analysis <br>

## Bivariate Analysis <br>

## Interesting Aggregates <br>


# Assessment of Missingness <br>
## NMAR Analysis

## Missingness Dependency

# Hypothesis Testing <br>

# Framing a Prediction Problem <br>

# Baseline Model <br>

# Final Model <br>

# Fairness Analysis <br>





<iframe
  src="assets/ingredients_distribution.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

Pivot_Table <br>

|   n_steps       |         1 |       2 |       3 |       4 |       5 |         6 |       7 |         8 |       9 |      10 |
|   n_ingredients |           |         |         |         |         |           |         |           |         |         |
|----------------:|----------:|--------:|--------:|--------:|--------:|----------:|--------:|----------:|--------:|--------:|
|               1 | nan       | 5       | 5       | 4.66667 | 4.25    | nan       | 4.95    | nan       | 5       | 5       |
|               2 |   4.7     | 4.71341 | 4.72757 | 4.78113 | 4.68368 |   4.81823 | 4.76103 |   4.74605 | 4.74012 | 4.548   |
|               3 |   4.78911 | 4.74635 | 4.65962 | 4.71857 | 4.71068 |   4.72856 | 4.75734 |   4.74538 | 4.71384 | 4.7622  |
|               4 |   4.709   | 4.74795 | 4.71195 | 4.70171 | 4.69749 |   4.6734  | 4.71801 |   4.65344 | 4.64221 | 4.70003 |
|               5 |   4.76297 | 4.7365  | 4.72298 | 4.7412  | 4.6805  |   4.654   | 4.70792 |   4.67625 | 4.69646 | 4.70421 |
|               6 |   4.73031 | 4.67918 | 4.70561 | 4.68746 | 4.67638 |   4.69962 | 4.686   |   4.64681 | 4.6802  | 4.63206 |
|               7 |   4.64944 | 4.70959 | 4.69154 | 4.66642 | 4.63702 |   4.66255 | 4.67411 |   4.69768 | 4.67997 | 4.60956 |
|               8 |   4.60763 | 4.7175  | 4.66443 | 4.68083 | 4.67262 |   4.65222 | 4.64312 |   4.65429 | 4.67395 | 4.58978 |
|               9 |   4.74444 | 4.7079  | 4.70515 | 4.70614 | 4.5998  |   4.61561 | 4.65887 |   4.65809 | 4.67642 | 4.68378 |
|              10 |   4.70981 | 4.71408 | 4.7534  | 4.62624 | 4.60412 |   4.65969 | 4.63623 |   4.65124 | 4.62158 | 4.65477 |
