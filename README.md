# Recipe Analytics: Linking Recipe Complexity and User Ratings for Culinary Insights 

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


## Data Cleaning and Exploratory Data Analysis

We conducted the following data cleaning steps:

1. Left merge the recipes and interactions datasets on id and recipe_id.

   - The purpose of this step is to helps match the unique recipes with their rating and review. We did a left merge specifically to get all the recipes in the recipes dataset.

1. Checked data types of all the columns.

   - The purpose of this step is to help evaluate what data cleaning steps and data type conversion are needed.
   - | Column             | Description |
     | :----------------- | :---------- |
     | `'name'`           | object      |
     | `'id'`             | int64       |
     | `'minutes'`        | int64       |
     | `'contributor_id'` | int64       |
     | `'submitted'`      | object      |
     | `'tags'`           | object      |
     | `'nutrition'`      | object      |
     | `'n_steps'`        | int64       |
     | `'steps'`          | object      |
     | `'description'`    | object      |
     | `'ingredients'`    | object      |
     | `'n_ingredients'`  | int64       |
     | `'user_id'`        | float64     |
     | `'recipe_id'`      | float64     |
     | `'date'`           | object      |
     | `'rating'`         | float64     |
     | `'review'`         | object      |

1. Filled all ratings of 0 with np.nan.

   - Rating is typicaly on a scale from 1 to 5. 1 represents the lowest rating, while 5 represents the highest rating. Leaving missing ratings as is would affect the average rating column. While computing the average, the denominator would be higher, while the numerator would just add a 0, not changing it. So this would make the average smaller than it should be. Therfore, we repalce all the ratings of 0 with np.nan.

1. Added column `'average_rating'` containing average rating per recipe.

   - A recipe's overall rating is determined by averaging the ratings provided by multiple users, offering a more comprehensive evaluation of its quality.
  
1. Dropped duplicate values of the recipe name
   -  The purpose of this step is to ensure that there is only one average rating listed per recipe.
  


### Result of cleaned dataframe 

| name                                 |     id |   minutes |   contributor_id | submitted   |   n_steps |   n_ingredients |   recipe_id | date       |   avg_rating | Steps_Bin   |
|:-------------------------------------|-------:|----------:|-----------------:|:------------|----------:|----------------:|------------:|:-----------|-------------:|:------------|
| 0 carb   0 cal gummy worms           | 283618 |        45 |           134414 | 2008-02-02  |        15 |               3 |      283618 | 2008-04-25 |      4.75    | 10-20       |
| 0 point ice cream  only 1 ingredient | 480558 |       125 |          2283828 | 2012-06-05  |         5 |               3 |      480558 | 2012-09-09 |      5       | 0-10        |
| 0 point soup   ww                    | 391705 |        55 |            39835 | 2009-09-24  |         5 |              14 |      391705 | 2009-10-20 |      4.77778 | 0-10        |
| 0 point soup  crock pot              | 416980 |       305 |            39835 | 2010-03-18  |         2 |              11 |      416980 | 2010-03-30 |      5       | 0-10        |
| 007  martini                         | 429524 |         5 |           599450 | 2010-06-12  |         4 |               4 |      429524 | 2012-08-20 |      5       | 0-10        |



<iframe src="assets/avg_rating_distribution.html" width="800" height="600" frameborder="0"></iframe>


