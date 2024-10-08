# Recipe Analysis
Exploring the Relationship Between the Rating of Recipes and the Number of Ingredients and the Number of Steps <br>
[Full Report](https://zhenhanhu.github.io/RecipeAnalysis/) <br>
By Zhenhan Hu

# Introduction: <br>
[Food.com](https://www.food.com/) is an online platform where people can view various types of food recipes and communicate about their food preparation experience. Based on the recipe, users have the chance to leave their ratings and reviews on specific recipes. And these recipes can be characterized by some of their quantitative features such as the number of ingredients that need to be prepared, the total number of steps for the entire process, the number of times estimated to prepare the recipe, etc. Thus, some interesting questions can be raised to explore the relationship between these features and their rating, and a prediction model using regression, for example, can be established to train and fit for recipe rating analysis.

This project will explore whether or not the number of ingredients and the number of steps for a recipe affect its rating. The key question that is being asked here is: **How does the number of ingredients and the number of steps in a recipe affect its rating?** This question is important, especially for people who love cooking and trying to design a new recipe, as such a relationship provides a helpful insight into how complexity influences satisfaction. If fewer ingredients or less number of steps correlate to a relatively high rating, the recipe designer might focus more on simplicity. On the other hand, if more ingredients correlate to a relatively high rating, designing complex recipes may be worth the effort.

The data from two datasets, `RAW_recipes` and `RAW_interactions` will be cleaned, assessed, and used for model construction. These datasets were originally scraped and used in a recommender system research paper, ["Generating Personalized Recipes from Historical User Preferences"](https://cseweb.ucsd.edu/~jmcauley/pdfs/emnlp19c.pdf), by Majumder et al.

`RAW_recipes` contains **83782 rows** where each row represents a unique recipe and 12 columns where each column represents a unique descriptive feature. `RAW_interactions`, on the other hand, contains **731927 rows** where each row represents a user commenting on a recipe (observation) and 5 columns on rating details. After the merge operation, there are **234429 rows**, and the relevant columns are as follows:

| Column | Description |
| ----------- | ----------- |
| `'n_ingredients'` | Number of ingredients in recipe |
| `'n_steps'` | Number of steps in recipe |
| `'minutes'` | Minutes to prepare recipe |
| `'rating'` | Rating given |

# Data Cleaning and Exploratory Data Analysis <br>
## Data Cleaning <br>
1. After loading two datasets, a left merge operation is performed on the recipes dataset and the interactions dataset with respect to the recipe id to avoid accidentally dropping any recipe and keep all recipes in the data, observing that it is possible for some recipes have no rating or multiple ratings.
2. Due to missing input of rating, ratings of zero are replaced with `np.NaN` as valid ratings typically ranging between 1 and 5.
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

Based on the histogram above, most recipes tend to use between 8 to 12 ingredients, with a peak density of around 9 ingredients. The distribution is right-skewed, showing that fewer recipes use a very large number of ingredients.

<iframe
  src="assets/q2_steps_distri.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

Based on the histogram above, most recipes have between 5 and 15 steps, with the highest density around 10 steps. The distribution is right-skewed, showing that recipes with more than 20 steps are relatively less common.

## Bivariate Analysis <br>

<iframe
  src="assets/q2_ingre_rating.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

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

Due to the data generating process and the intention of people leaving reviews, the missingness mechanism for the column `rating` is **Not Missing at Random (NMAR)**. People who are super unsatisfied or extremely satisfied tend to give ratings at two extreme ends, while people who think the recipe is just ok or have an indifferent attitude might have no strong intention to do so, and thus, are less likely  to leave some ratings. In other words, the chance that a rating is missing depends on the actual missing rating itself.

## Missingness Dependency <br>
Since the column of rating is missing many values,  we will perform permutation tests to analyze the dependency of its missingness on other columns. <br>

1. Dependency of rating missingness on the number of steps: <br>
**Null Hypothesis**: The missingness of ratings does NOT depend on the number of steps <br>
**Alternative Hypothesis**: The missingness of ratings does depend on the number of steps <br>
**Test Statistic**: The absolute difference between the mean of `n_steps` when the rating is missing and the mean of `n_steps` when the rating is not missing <br>
**Significance Level**: 0.01 <br>
After finding the observed test statistic is around 1.68 and a list of sample test statistics from 500 repetitions of shuffling, **the p_value is 0.0**, thus we reject the null hypothesis and the result implies that the missingness of rating depends on the number of steps <br>

<iframe
  src="assets/q3_steps_permu.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

The distribution of the number of steps when the rating is missing and the distribution of the number of steps when the rating is not missing is shown below, for better visualization, separate distributions are attached. <br>

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

<br>

2. Dependency of rating missingness on the amount of time: <br>
**Null Hypothesis**: The missingness of ratings does NOT depend on the amount of time <br>
**Alternative Hypothesis**: The missingness of ratings does depend on the amount of time <br>
**Test Statistic**: The absolute difference between the mean of minutes when the rating is missing and the mean of minutes when the rating is not missing <br>
**Significance Level**: 0.01 <br>
After finding the observed test statistic is around 122.70 and a list of sample test statistics from 500 repetitions of shuffling, **the p_value is 0.024**, thus we do not reject the null hypothesis and the result implies that the missingness of rating does not depend on minutes. <br>

<iframe
  src="assets/q3_minutes_permu.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

The distribution of the amount of time when the rating is missing and the distribution of the amount of time when the rating is not missing is shown below, for better visualization, separate distributions are attached. <br>

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

**Null Hypothesis**: The number of ingredients does not have any effect on the recipe rating. In other words, the average rating is the same regardless of the number of ingredients

**Alternative Hypothesis**: The number of ingredients does affect the recipe rating. In other words, recipes with different numbers of ingredients have different average ratings.

**Test Statistic**: The absolute difference between the mean of the recipe group with a lower number of ingredients and the mean of the recipe group with a higher number of ingredients.

**Significance Level**: 0.05

Explanation: As we can see the distribution of the number of ingredients in the "Univariate Analysis" Section, we can make a comparison between two groups, the ones with a low number of ingredients (less than 9 ingredients), and the ones with a high number of ingredients (9 ingredients or more). Thus, a plausible test statistic would be the absolute difference in the mean ratings among these two groups. The mean is a common measure of central tendency and provides a summary of the typical rating for each group, but we use the absolute difference in mean instead of just the difference in mean as it allows us to capture any difference between the two groups, regardless of direction. We are measuring the extent to which the two groups are distinct in terms of their ratings by focusing on the magnitude of the difference.

<iframe
  src="assets/q4_ingre_permu.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

The observed test statistic is 0.008 and a permutation test with 500 repetitions is conducted and resulting in a **p_value of 0.0**, with the significance level of 0.05, thus we reject the null hypothesis. This implies that the number of ingredients may affect the recipe rating.

# Framing a Prediction Problem <br>
As we saw a positive correlation between the number of ingredients and average ratings in the "Bivariate Analysis" Section, as well as the proven existing relationship between these two columns in the "Hypothesis Test" Section, we can address the problem of **how to predict recipe rating based on these relevant features we explored?**

The **response variable** is `filled_ratings` as it is a good representation of the rating for each recipe, and being able to predict it helps us to understand user preferences and predict recipe success. The **feature variables** can be the number of ingredients and the number of steps. Since the feature columns and response variables are all numerical/quantitative, a **regression** model can be built to fit and train. 

Lastly, we can use **RMSE** to evaluate the model performance because it penalizes large errors more heavily. Note: RMSE is the square root of MSE, which means RMSE has the same units as the dependent variable, and thus makes it easier to interpret in the context of the problem.
Additionally, we can compute **R^2** to assess the proportion of variance in ratings that the predictor model explains.

**Time of Prediction**: The number of ingredients and the number of steps are features available before the rating is posted, thus, the 'time of prediction' concern can be addressed.

# Baseline Model <br>
A Linear Regression is built as the baseline model, two features are used, `n_ingredients` and `n_steps` as described as follows:

| Column           | Description                     | Type          |
| :--------------  | ------------------------------: | ------------: | 
| `'n_ingredients'`| Number of ingredients in recipe | quantitative  |
| `'n_steps'`      | Number of steps in recipe       | quantitative  |

The baseline model performance is not good since the R^2 for the training dataset and the testing dataset are around 4.02e-05 and 4.27e-07, respectively, which indicates the model poorly explains the variance in the target variable; and the RMSE for the training dataset and the testing dataset are around 0.50 and 0.49 respectively, which also indicates bad performance with the average magnitude of the prediction errors being high.

# Final Model <br>
Two new features are considered in the new model, `minutes` and `submitted` as described as follows:  <br>

| Column          | Description                     |
| :-------------- | ------------------------------: |
|`'minutes'`| Minutes to prepare recipe |
| `'submitted'`   | Date recipe was submitted       | 


Adding the new feature on the time to prepare the recipe since the time it takes to prepare a recipe could also affect its rating, for example, shorter recipes may be more favored to people with limited time, while more complex, longer recipes might be favored by those who enjoy cooking. Such a feature is related to people's preferences and thus makes it a valuable predictor for ratings.  <br>
Adding the new feature on the date the recipe was submitted and its year is extracted, as might reveal some food cooking trends over history, for example, some old recipes might be outdated or no longer favored by contemporary people.  <br>
`minutes` and `submitted` complement `n_ingredients` and `n_steps` by providing more nuanced information. While the number of ingredients and steps tells us about the recipe’s complexity itself, the time to prepare and the era of submission tell us about how that complexity is perceived by people and how external factors such as trends might influence the rating.  <br>

**Modeling Algorithm: Ridge Regression**  <br>
Besides using vanilla linear regression with features standardized in the baseline model, I tried Ridge Regression as the modeling algorithm instead as it added an L2 regularization term to penalize large coefficients. Since the number of ingredients and the number of steps have some correlation, using Ridge helps to eliminate multicollinearity and prevents overfitting, thus making better predictions on unseen data

**Best Hyperparameter and Selection Method**  <br>
The hyperparameter alpha, which controls the strength of regularization, is tuned here. As a result, the hyperparameter that performs the best is when alpha = 0.1. GridSearchCV is used to find the best hyperparameters and 5-fold cross-validation is performed to select the potential value for alpha from [0.01, 0.05, 0.1, 1.0]

**Performance Evaluation** <br>
R^2 on Train improved from 4.02e-05 to 0.0028  <br>
R^2 on Test improved from 4.27e-07 to 0.0015  <br>
RMSE on Train reduced 0.0006  <br>
RMSE on Test reduced 0.0003  <br>

# Fairness Analysis <br>
To perform a “fairness analysis” of my Final Model from the previous step, we can ask the question “does my model perform worse for individuals in Group X than it does for individuals in Group Y?”

**Two groups**:
Since the median submitted date for recipes is around the year of 2009, here, we can define our two groups to be:
“old recipes”: recipes before 2009
“new recipes”: recipes after 2009

**Evaluation Metric**:
Since both RMSE and R^2 are valid evaluation metrics, we will use RMSE here.

**Null Hypothesis**: Our model is fair. Its precision for old recipes and new recipes is roughly the same, and any differences are due to random chance.

**Alternative Hypothesis**: Our model is unfair. Its RMSE for old recipes is lower than its precision for new recipes.

**Test Statistic**: Difference between the RMSE among the rating predictions among the two groups

**Significance Level**: 0.05

Since the alternative hypothesis is on the direction of the RMSE of predictions for old recipes is lower than the RMSE of predictions for new recipes, and the test statistic is calculated by old_RMSE - new_RMSE, we want to find the proportion of the sampled test statistics that even extreme toward the lower end of the observed test statistic, however, after permutation of 100 times, the p_value found is 0.0, with a significance level of 0.05, we reject the Null Hypothesis, and the model might not be fair with respect to the submitted time.

<iframe
  src="assets/q8_rmse_permu.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>
