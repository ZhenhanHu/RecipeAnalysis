# Exploring the Relationship Between the Rating of Recipes and the Number of Ingredients and the Number of Steps

# Introduction: <br>
This project will explore whether or not the number of ingredients and the number of steps in a recipe affect its rating. The key question that is being asked here is: *How does the number of ingredients and the number of steps in a recipe affect its rating?* This question is important, especially for people who love cooking and trying to design a new recipe, as such a relationship provides a helpful insight into how complexity influences satisfaction. For example, If fewer ingredients correlate to a relatively high rating, the recipe designer might focus more on simplicity. On the other hand, if more ingredients correlate to a relatively high rating, designing complex recipes may be worth the effort.

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
