# Nutrition Research Project
Our journey began with a simple yet profound question: How does the nutritional value of a recipe influence its cooking time? Through meticulous analysis of a sizable number of recipes, we've embarked on a quest to unravel the intricate relationship between the healthiness of dishes and the time they take to prepare.

## Introduction
The "Recipes & Ratings" dataset consists of a collection of recipes, each accompanied by detailed information including cooking time, nutritional values, and other relevant attributes. By leveraging this dataset, we aim to uncover insights that could potentially influence dietary choices and cooking habits.

For the purpose of this analysis, we define healthy recipes as those that align with specific nutritional guidelines, such as lower amounts of saturated fats, sugars, and sodium, while being higher in fiber, vitamins, and minerals. Unhealthy recipes, on the other hand, are characterized by higher levels of saturated fats, sugars, sodium, and calories, offering lower nutritional value per serving.

It's important to note that this distinction is somewhat simplified for the purposes of this project. The actual healthiness of a recipe can depend on various factors, including individual dietary needs and overall eating patterns.

The central question of our project is: Is there a statistically significant difference in average cooking times between healthy and unhealthy recipes?

This question is grounded in the broader context of dietary choices and meal preparation habits. Understanding whether healthier recipes require more or less time to prepare compared to their unhealthy counterparts could have implications for public health initiatives, dietary advice, and individuals' willingness to adopt healthier eating habits.

The dataset contains 234429 rows, each representing a unique recipe. For our analysis, the following columns are particularly relevant:

- id: An identification number for each unique recipe.
- minutes: The total time required to prepare and cook the recipe in minutes.

## Data Cleaning and Exploratory Data Analysis

### Data Cleaning

Our data cleaning process consisted of the following changes:

- Merging the two datasets, one of which contained the recipes and the other reviews, using the recipe 'id' column which was common amongst them.
- Replacing all instances of the value 0 in the 'rating' column with np.nan. This step was important because ratings are only typically given on a scale starting from 1 so a value of 0 most likely means that it was missing. Making this change allowed us to explore missing mechanisms later in the project.
- Dropping columns that we did not consider necessary for our analysis. These columns included 'name', 'contributor_id', 'submitted', 'tags', 'description', 'user_id', 'date', 'review', 'steps', and 'ingredients'.
- Grouping the recipes by their ID to calculate average rating of each unique recipe and adding that series to our existing dataframe.
- Extracting information of the "Percent Daily Value" of the various nutritional content from the 'nutrition' column and storing it in seperate columns namely, 'calories', 'total_fat', 'sugar', 'sodium', 'protein', 'saturated_fat', and 'carbohydrates'.

Here are the first 5 rows of our cleaned dataset:

| id | minutes | n_steps | n_ingredients | rating | avg_rating | calories | total_fat | sugar | sodium | protein | saturated_fat | carbohydrates |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| 333281.0 | 40.0 | 10.0 | 9.0 | 4.0 | 4.0 | 138.4 | 10.0 | 50.0 | 3.0 | 3.0 | 19.0 | 6.0 |
| 453467.0 | 45.0 | 12.0 | 11.0 | 5.0 | 5.0 | 595.1 | 46.0 | 211.0 | 22.0 | 13.0 | 51.0 | 26.0 |
| 306168.0 | 40.0 | 6.0 | 9.0 | 5.0 | 5.0 | 194.8 | 20.0 | 6.0 | 32.0 | 22.0 | 36.0 | 3.0 |
| 306168.0 | 40.0 | 6.0 | 9.0 | 5.0 | 5.0 | 194.8 | 20.0 | 6.0 | 32.0 | 22.0 | 36.0 | 3.0 |
| 306168.0 | 40.0 | 6.0 | 9.0 | 5.0 | 5.0 | 194.8 | 20.0 | 6.0 | 32.0 | 22.0 | 36.0 | 3.0 |

### Univariate Analysis

Most of the recipes have a score of 5. This pattern may indicate that the recipes in the dataset have been well-received overall. Also, notice that there are no ratings less than the integer value 1, since we replaced the values 0 with np.nan earlier in our data cleaning process.

<iframe
  src="assets/plotly_hist.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

### Bivariate Analysis

There is a positive association between the total fat content (PDV) and calories in recipes, indicating that recipes with higher fat content typically have higher calorie content. The total fat, however, does not rise proportionally to the number of calories until a certain threshold, suggesting that other substances might also make a substantial contribution to the calorie content.

<iframe
  src="assets/plotly_scat.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

### Interesting Aggregates

The categorization into 'low fat,' 'medium fat,' and 'high fat' is based on predefined nutritional criteria that classify recipes according to their total fat content.

Low Fat: Recipes with a total fat content that is less than 5% of the daily value (PDV).
Medium Fat: Recipes with a total fat content that falls within a moderate range of PDV, say 5-20% PDV.
High Fat: Recipes where the total fat content exceeds a higher percentage of PDV, such as more than 20% PDV.

The mean ratings are very close across categories, hovering around 4.6, with a consistent median of 5.0, suggesting a generally high and similar level of satisfaction among all fat content categories. The 'count' indicates that 'high fat' recipes are the most frequent in this dataset, followed by 'medium fat' and 'low fat'. This analysis revealed that users' average satisfaction does not significantly vary across these categories.

|            | mean | median | count |
|---|---|---|---|
| low fat    | 4.59 | 5.0    | 9055  |
| medium fat | 4.61 | 5.0    | 26624 |
| high fat   | 4.63 | 5.0    | 39405 |

## Assessment of Missingness

### NMAR Analysis

### Missingness Dependency

## Hypothesis Testing

**Null Hypothesis**: On average, healthier recipes and unhealthy recipes have a statistically insignificant difference in average cooking times.

**Alternate Hypothesis**: On average, healthier recipes and unhealthy recipes have a statistically significant difference in average cooking times.

**Test Statistic**: µ2 - µ1

**Significance Level**: 5% or 0.05

***p*-value**: 0.0786

**Conclusion**: Since the *p*-value is greater than 0.05, we can conclude that there is no statistically significant difference in cooking times between healthy and unhealthy recipes. Therefore, we fail to reject the null hypothesis.





