# Recipe Analysis
Exploring the Relationship Between the Rating of Recipes and the Number of Ingredients and the Number of Steps

# Introduction: <br>
[Food.com](https://www.food.com/) is an online platform where people can view various types of food recipes and communicate about their food preparation experience. Based on the recipe, users have the chance to leave their ratings and reviews on specific recipes. And these recipes can be characterized by some of their quantitative features such as the number of ingredients that need to be prepared, the total number of steps for the entire process, the number of times estimated to prepare the recipe, etc. Thus, some interesting questions can be raised to explore the relationship between these features and their rating, and a prediction model using regression, for example, can be established to train and fit for recipe rating analysis.

This project will explore whether or not the number of ingredients and the number of steps for a recipe affect its rating. The key question that is being asked here is: **How does the number of ingredients and the number of steps in a recipe affect its rating?** This question is important, especially for people who love cooking and trying to design a new recipe, as such a relationship provides a helpful insight into how complexity influences satisfaction. If fewer ingredients or less number of steps correlate to a relatively high rating, the recipe designer might focus more on simplicity. On the other hand, if more ingredients correlate to a relatively high rating, designing complex recipes may be worth the effort.

The data from two datasets, `RAW_recipes` and `RAW_interactions` will be cleaned, assessed, and used for model construction. These datasets were originally scraped and used in a recommender system research paper, ["Generating Personalized Recipes from Historical User Preferences"](https://cseweb.ucsd.edu/~jmcauley/pdfs/emnlp19c.pdf), by Majumder et al.

`RAW_recipes` contains 83782 rows where each row represents a unique recipe and 12 columns where each column represents a unique descriptive feature. `RAW_interactions`, on the other hand, contains 731927 rows where each row represents a user commenting on a recipe (observation) and 5 columns on rating details. After the merge operation, there are 234429 rows, and the relevant columns are as follows:

| Column | Description |
| ----------- | ----------- |
| `'n_ingredients'` | Number of ingredients in recipe |
| `'n_steps'` | Number of steps in recipe |

# Data Cleaning and Exploratory Data Analysis <br>
## Data Cleaning <br>
1. After loading two datasets, a left merge operation is performed on the recipes dataset and the interactions dataset with respect to the recipe id to avoid accidentally dropping any recipe and keep all recipes in the data, observing that it is possible for some recipes have no rating or multiple ratings.
2. Due to missing input of rating, ratings of zero are replaced with `np.NaN`.
3. The average rating per recipe is calculated (especially for recipes that has multiple ratings) and added as a column which can be used as a feature.
4. The head of the resulting cleaned data frame for relevant columns is shown as follows: <br>

|    | name                                 |   n_ingredients |   n_steps |   rating |   filled_ratings |
|---:|:-------------------------------------|----------------:|----------:|---------:|-----------------:|
|  0 | 1 brownies in the world    best ever |               9 |        10 |        4 |                4 |
|  1 | 1 in canada chocolate chip cookies   |              11 |        12 |        5 |                5 |
|  2 | 412 broccoli casserole               |               9 |         6 |        5 |                5 |
|  3 | 412 broccoli casserole               |               9 |         6 |        5 |                5 |
|  4 | 412 broccoli casserole               |               9 |         6 |        5 |                5 |

## Univariate Analysis <br>

<iframe
  src="assets/q2_ing_distri.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

<br>
Based on the histogram above, most recipes tend to use between 8 to 12 ingredients, with a peak density of around 10 ingredients. The distribution is right-skewed, showing that fewer recipes use a very large number of ingredients.

<iframe
  src="assets/q2_steps_distri.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

<br>
Based on the histogram above, most recipes have between 5 and 15 steps, with the highest density around 10 steps. The distribution is right-skewed, showing that recipes with more than 20 steps are relatively less common.

## Bivariate Analysis <br>

<iframe
  src="assets/q2_ingre_rating.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

<br>
Based on the scatter plot above, recipes with fewer than 10 ingredients generally have a slight decline in average ratings. As the number of ingredients increases beyond 10, the average rating starts to improve. Specifically, recipes with more than 20 ingredients generally have higher average ratings. Thus, this may indicate that more complex recipes are rated higher by users.

## Interesting Aggregates <br>

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

This is a portion (first 10 rows and first 10 columns) of the pivot table of `n_ingredients ` and `n_steps ` on average rating. For recipes with fewer ingredients, their average rating remains relatively high, especially for simpler recipes with fewer steps. Thus, this indicates that simpler recipes with fewer steps and ingredients tend to be highly rated while increasing steps for recipes with few ingredients tend to lower the ratings.

# Assessment of Missingness <br>
## NMAR Analysis <br>

Due to the data generating process and the intention of people leaving reviews, the missingness mechanism for the column `rating` is Not Missing at Random (NMAR). People who are super unsatisfied or extremely satisfied tend to give ratings at two extreme ends, while people who think the recipe is just ok or have an indifferent attitude might have no strong intention to do so, and thus, are less likely  to leave some ratings. In other words, the chance that a rating is missing depends on the actual missing rating itself.

## Missingness Dependency <br>
Since the column of rating is missing many values,  we will perform permutation tests to analyze the dependency of its missingness on other columns.

1. Dependency of rating missingness on the number of steps:
Null Hypothesis: The missingness of ratings does NOT depend on the number of steps
Alternative Hypothesis: The missingness of ratings does depend on the number of steps
Test Statistic: The absolute difference between the mean of n_steps when the rating is missing and the mean of n_steps when the rating is not missing
Significance Level: 0.01
After finding the observed test statistic is around 1.68 and a list of sample test statistics from 500 repetitions of shuffling, the p_value is 0.0, thus we reject the null hypothesis and conclude that the missingness of rating depends on the number of steps

<iframe
  src="assets/q3_steps_permu.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

The distribution of the number of steps when the rating is missing and the distribution of the number of steps when the rating is not missing is shown below, for better visualization, separate distributions are attached.

<iframe
  src="assets/q3_steps_stacked.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

<iframe
  src="assets/q3_steps_unstacked1.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

<iframe
  src="assets/q3_steps_unstacked2.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

2. Dependency of rating missingness on the amount of time:
Null Hypothesis: The missingness of ratings does NOT depend on the amount of time
Alternative Hypothesis: The missingness of ratings does depend on the amount of time
Test Statistic: The absolute difference between the mean of minutes when the rating is missing and the mean of minutes when the rating is not missing
Significance Level: 0.01
After finding the observed test statistic is around 122.70 and a list of sample test statistics from 500 repetitions of shuffling, the p_value is 0.022, thus we do not reject the null hypothesis and conclude that the missingness of rating does not depend on minutes.

<iframe
  src="assets/q3_minutes_permu.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

The distribution of the amount of time when the rating is missing and the distribution of the amount of time when the rating is not missing is shown below, for better visualization, separate distributions are attached.

<iframe
  src="assets/q3_minutes_unstacked1.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

<iframe
  src="assets/q3_minutes_unstacked2.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

# Hypothesis Testing <br>

# Framing a Prediction Problem <br>

# Baseline Model <br>

# Final Model <br>

# Fairness Analysis <br>
