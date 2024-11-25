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



### Univariate Graph Analysis

<iframe src="assets/n-steps-distribution.html" width="800" height="600" frameborder="0"></iframe>

Analysis: This histogram displays the distribution of number of steps in recipes, showing a significant concentration of ratings near 10-15 steps. The trend indicates that most entities have fewer steps, while recipes with many steps are relatively rare, suggesting a right skew in the data.

### Bivariate Graph Analysis

<iframe src="assets/n-steps-bivariate-distribution.html" width="800" height="600" frameborder="0"></iframe>

Analysis: The graph shows that the recipes with ratings 3 and 4 have lower number of steps, while the recipes with ratings 1, 2, and 5 have higher number of steps. This suggests that typically recipes with fewer number of steps tend to have higher ratings and vice versa. 

### Interesting Aggregates

| Steps_Bin   |   Average_Rating_Mean |   Count |   Rating_StdDev |
|:------------|----------------------:|--------:|----------------:|
| 0-10        |               4.62423 |   51793 |        0.632202 |
| 10-20       |               4.6232  |   26641 |        0.65224  |
| 20-30       |               4.63654 |    4199 |        0.671727 |
| 30-40       |               4.68632 |     716 |        0.637707 |


This pivot table summarizes the data by grouping the "Number_of_Steps" column into bins (e.g., "0-10", "10-20", etc.) and calculating aggregate statistics for each bin. Here's the significance of each column:

- **Average_Rating_Mean**: Shows the average rating for each step range, providing insight into how ratings vary across different activity levels.
- **Count**: Indicates the number of entries (or observations) in each bin, reflecting the distribution of data across step ranges.
- **Rating_StdDev**: Displays the standard deviation of ratings within each bin, highlighting the variability or consistency of ratings for a given step range.

This table shows the relationships between step levels and ratings, such as whether higher step counts are associated with better ratings and if certain bins have more consistent feedback.



## Assessment of Missingness

- ‘Rating’ is a column that is Not Missing At Random (NMAR). This is because if people felt really strongly about a specific recipe, they are more likely to report their rating. On the other hand, if people do not have a strong opinion about a recipe, they are more likely to not share their rating. Therefore, the rating column is dependent on its own value. 
- Additional data that we can collect to make the missingness of ‘rating’ MAR is the popularity of the recipe. For example, we can collect the number of views for that recipe. The higher the number of views, the more likely people have tried and rated a recipe and vice versa. Therefore, the missingness of ‘rating” is dependent on an entirely different column, “popularity of recipe”.
  


### Rating on n_steps:

- **Null Hypothesis**: Rating is not MAR dependent on the n_steps column.

- **Alternative Hypothesis**: Rating is MAR dependent on the n_steps column.

- **Test Statistic**: Difference in means

- **Results**: The results show a p-value of 0.0, which is less than the significance level at 0.05. Since the p-value is extremely small, we can reject the null hypothesis, so Rating is MAR dependent on the n_steps column.


<iframe src="assets/nsteps-missing-dependency.html" width="800" height="600" frameborder="0"></iframe>



### Rating on minutes

- **Null Hypothesis**: Rating is not MAR dependent on the minutes column.

- **Alternative Hypothesis**: Rating is MAR dependent on the minutes column.

- **Test Statistic**: Difference in means

- **Results**: The results show a p-value of 0.06, which is greater than the significance level at 0.05. Since the p-value is greater, we can fail to reject the null hypothesis of, so Rating is not MAR dependent on the minutes column.


<iframe src="assets/minutes-missing-dependency.html" width="800" height="600" frameborder="0"></iframe>



## Hypothesis Testing

- **Null Hypothesis**: There is no association between the number of steps and the average rating of a recipe.

- **Alternative Hypothesis** : There is an association between the number of steps and the average rating of a recipe.

- **Test Statistic**: Difference in means

- **Significance Level**: 0.05
  
- **Result**: The null hypothesis was rejected with a statistically significant result (p-value = 0.0), indicating an association. However, the observed difference in means (-0.0197) was very small, suggesting the association is weak or negligible.

- **Justification**: We chose the difference in means between the two groups as our test statistic because we are interested in comparing the central tendencies of the ratings for recipes with fewer steps (0-20) versus those with more steps (20-40). The observed difference in means is −0.0197. A permutation test is appropriate in this case because we do not have any information about the population distribution, and we aim to assess whether the observed difference could have occurred by chance under the null hypothesis. The practical purpose of this analysis is to help people make informed decisions when selecting recipes. If a recipe has a high number of steps, its rating could influence whether someone decides to try it. For instance, if a complex recipe with many steps has a high rating, people might feel more motivated to follow it, trusting that the effort is worthwhile. Conversely, if the rating is low, they may opt for simpler alternatives. Understanding this relationship can guide users toward recipes that best match their preferences and willingness to invest time.



## Framing a Prediction Problem 
