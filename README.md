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




