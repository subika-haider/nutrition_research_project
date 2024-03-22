# Nutrition Research Project
Our journey began with a simple yet profound question: How does the nutritional value of a recipe influence its cooking time? Through meticulous analysis of a sizable number of recipes, we've embarked on a quest to unravel the intricate relationship between the healthiness of dishes and the time they take to prepare.

## Introduction
The "Recipes & Ratings" dataset consists of a collection of recipes, each accompanied by detailed information including cooking time, nutritional values, and other relevant attributes. By leveraging this dataset, we aim to uncover insights that could potentially influence dietary choices and cooking habits.

For the purpose of this analysis, we define healthy recipes as those that align with specific nutritional guidelines, such as lower amounts of saturated fats, sugars, and sodium, while being higher in fiber, vitamins, and minerals. Unhealthy recipes, on the other hand, are characterized by higher levels of saturated fats, sugars, sodium, and calories, offering lower nutritional value per serving.

It's important to note that this distinction is somewhat simplified for the purposes of this project. The actual healthiness of a recipe can depend on various factors, including individual dietary needs and overall eating patterns.

The central question of our project is: Is there a statistically significant difference in average cooking times between healthy and unhealthy recipes?

This question is grounded in the broader context of dietary choices and meal preparation habits. Understanding whether healthier recipes require more or less time to prepare compared to their unhealthy counterparts could have implications for public health initiatives, dietary advice, and individuals' willingness to adopt healthier eating habits.

The dataset contains 234429 rows, each representing a unique recipe. For our analysis, the following columns are particularly relevant:

- `id`: An identification number for each unique recipe.
- `minutes`: The total time required to prepare and cook the recipe in minutes.
- `n_steps`: The number of steps needed for the recipe.
- `n_ingredients`: The number of ingredients needed to prepare the recipe.
- `rating`: The rating of each recipe.
- `avg_rating`: The average rating of each unique recipe.
- `calories`: The total number of calories in each recipe.
- `total_fat`: The percentage of the daily value of total fat needed by the average person.
- `sugar`: The percentage of the daily value of sugar needed by the average person.
- `sodium`: The percentage of the daily value of sodium needed by the average person.
- `protein`: The percentage of the daily value of sodium needed by the average person.
- `saturated_fat`: The percentage of the daily value of saturated fat needed by the average person.
- `carbohydrates`: The percentage of the daily value of carbohydrates needed by the average person.

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

The column we decided to assess the missingness of is the `avg_rating` column. The other two columns we selected are the `n_steps` and the `n_ingredients` columns. We suspect a potential link between the missingness of `avg_rating` and n_steps` because recipes with more number of steps might me more complex and therefore, less people might try and rate them.

However, we do not suspect any logical link between the missingness of the `n_ingredients` and the `avg_rating` columns.

## Hypothesis Testing

**Null Hypothesis**: On average, healthier recipes and unhealthy recipes have a statistically insignificant difference in average cooking times.

**Alternate Hypothesis**: On average, healthier recipes and unhealthy recipes have a statistically significant difference in average cooking times.

**Test Statistic**: µ2 - µ1

**Significance Level**: 5% or 0.05

***p*-value**: 0.0786

**Conclusion**: Since the *p*-value is greater than 0.05, we can conclude that there is no statistically significant difference in cooking times between healthy and unhealthy recipes. Therefore, we fail to reject the null hypothesis.

## Framing a Prediction Problem

**Prediction Problem**: Predict the number of calories in a recipe.

**Prediction Problem Type**: Regression

**Response Variable**: `calories`. It is a metric that reflects the energy content of a recipe which is crucial for dietary planning and health assessments.

**Features to Use**:
- `n_ingredients`: Total number of ingredients in a recipe.
- Nutritional information: Specifically `total_fat`, `sugar`, `sodium`, `protein`, `saturated_fat`, and `carbohydrates`.
- `n_steps`: Number of preparation steps as an indicator of recipe complexity.

**Evaluation Metric**: Root Mean Squared Error (RMSE) since it is a balanced choice between penalizing large errors and maintaining interpretability in the same units as the target variable.

**Model Choice**: Random Forest Regressor since it can handle a mix of numerical and categorical features and for how robust it is to outlier values.

**Preprocessing Steps**:
- Impute missing values in nutritional information using median values.
- Encode any categorical variables not listed above with one-hot encoding.
- Scale numerical features to a standard range or distribution.

## Baseline Model

**Features**:
- `n_ingredients`: Quantitative (number of ingredients)
- `total_fat`: Quantitative (total fat content)

**Model Assessment**: The RMSE score of our model came out to be approximately 288 which indicates that, on average, the model's predictions deviate from the actual values of calorie content of recipes by 288 units. Since this number is too high, we would classify the performance of this model as average.

## Final Model

**Use of `n_ingredients`**: The number of ingredients suggests the complexity of a recipe, potentially affecting its calorie count.

**Use of `total_fat`**: Since fats are calorically dense, the total fat content is a direct indicator of a recipe's caloric value. We used this feature as-is to preserve its direct relationship with the target variable.

**Use of `RandomForestRegressor`**: Chosen for their ability to handle complex data structures and reduce overfitting, making them suitable for predicting calories, which likely involves intricate interactions among ingredients.

**Hyperparameter Tuning with `GridSearchCV`**: This systematic approach identified the best model settings by evaluating various combinations of hyperparameters across different subsets of the data, optimizing for accuracy as measured by the negative RMSE.

The strategic selection of features and optimization of model parameters lead to a final model that more accurately captured the underlying patterns in the data, resulting in better performance compared to the simpler, less tailored baseline model.

## Fairness Analysis

**Choice of Group X**: Recipes with a number of ingredients less than or equal to the median number of ingredients in the training dataset.

**Choice of Group Y**: Recipes with a number of ingredients greater than the median.

**Evaluation Metric**:
- Root Mean Squared Error (RMSE) for evaluating prediction error.
- R² Score for assessing the proportion of variance in the dependent variable that is predictable from the independent variable(s).

**Null Hypothesis**: The model is fair (For a low number of ingredients vs high number of ingredients and low fat vs high fat, RMSE and R^2 are similar).

**Alternate Hypothesis**: The model is unfair (For a low number of ingredients vs high number of ingredients and low fat vs high fat RMSE and R^2 are not similar). 

**Test Statistic**: The difference in RMSE and R² scores between the two groups

**Significance Level**: 5% or 0.05

***p*-value**: 0.835

**Conclusion**: Based on the analysis, there appears to be evidence enabling us to reject the null hypothesis, suggesting that the model may not be fair according to the defined metrics.









