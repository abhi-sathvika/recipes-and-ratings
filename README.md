# Recipe Analytics: Linking Complexity and User Ratings for Culinary Insights 

Authors: Preethi Manne & Abhi Sathvika Goriparthy

## Introduction
The dataset being analyzed contains detailed information about recipes from a popular online platform, offering a rich repository of culinary data. Each recipe is described by various attributes, including the number of steps required, the ingredients involved, the time needed to prepare, and its average rating by users. This dataset allows us to delve into user preferences and explore what factors make a recipe more appealing.

### Project Focus:
Our project focuses on answering this central question:
**"What is the relationship between the number of steps in a recipe and its average user rating?"**
This question is intriguing because it sheds light on how complexity in recipe preparation might influence user satisfaction. Does a simple recipe garner more favorable reviews, or do users appreciate the effort and detail of a complex recipe? Answering this can benefit chefs, culinary websites, and anyone looking to optimize recipe creation for higher ratings.

### Why It Matters
This question has practical implications for both recipe creators and consumers:
Recipe Creators: Insights from this analysis can help content creators design recipes that align with user preferences, maximizing engagement and positive feedback.
Consumers: Understanding these patterns helps readers find recipes that are more likely to meet their expectations, whether they value simplicity or complexity.

### Dataset Overview
For our analysis, we used two datasets, recipes and interactions. 

Relevant columns:
- n_steps: The number of steps required to prepare the recipe. This reflects the recipe's complexity.
- avg_rating: The average user rating of the recipe, a measure of its popularity and perceived quality.
- minutes: The total preparation time for the recipe, providing context to its complexity.

### Datasets Used
- Recipes: 83782 rows, 12 columns
- Interactions: 731927 rows, 5 columns

| Column             | Description                                                                                                                                                                                       |
| :----------------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `'name'`           | Recipe name                                                                                                                                                                                       |
| `'id'`             | Recipe ID                                                                                                                                                                                         |
| `'minutes'`        | Minutes to prepare recipe                                                                                                                                                                         |
| `'contributor_id'` | User ID who submitted this recipe                                                                                                                                                                 |
| `'submitted'`      | Date recipe was submitted                                                                                                                                                                         |
| `'tags'`           | Food.com tags for recipe                                                                                                                                                                          |
| `'nutrition'`      | Nutrition information in the form [calories (#), total fat (PDV), sugar (PDV), sodium (PDV), protein (PDV), saturated fat (PDV), carbohydrates (PDV)]; PDV stands for “percentage of daily value” |
| `'n_steps'`        | Number of steps in recipe                                                                                                                                                                         |
| `'steps'`          | Text for recipe steps, in order                                                                                                                                                                   |
| `'description'`    | User-provided description                                                                                                                                                                         |
| `'ingredients'`    | Text for recipe ingredients                                                                                                                                                                       |
| `'n_ingredients'`  | Number of ingredients in recipe                                                                                                                                                                   |

| Column        | Description         |
| :------------ | :------------------ |
| `'user_id'`   | User ID             |
| `'recipe_id'` | Recipe ID           |
| `'date'`      | Date of interaction |
| `'rating'`    | Rating given        |
| `'review'`    | Review text         |
