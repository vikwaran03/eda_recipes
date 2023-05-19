# Exploring the popularity of different recipes 

### Introduction:

The dataset considered in this project is the result of merging two datasets that were originally scraped from [food.com](https://www.food.com/). The first dataset contained information regarding the different recipes, and the second contained reviews and ratings of those recipes. When these two datasets were merged, the resulting dataframe can be used to answer many such questions regarding how different recipes are preffered, based on various variables. Taking this into account, my project will focus on the following question: <br>

<center> <i>Do recipes that require more ingredients tend to have higher average_ratings than recipes that require less ingredients?</i> </center><br>


The initial dataframe that my project takes into account has shape (234429 rows × 18 columns), after merging. Of these 18 columns, my question is heavily on 3 columns: 'name' (recipe name), 'n_ingredients' (number of ingredients in recipe), and 'average_rating' (average rating of recipe). 

### Cleaning and EDA:

#### Data Cleaning
Steps taken to clean dataset for EDA:<br>
1. Grouping by recipe name and aggregating the average rating and number of ingredients for each recipe
2. Changing the data type of number of ingredients from float to int, since it is not possible to have fractions of an ingredient (ex. 0.5 carrot is still considered 1 ingredient, not 0.5 ingredient)
3. Rounding all values in average_rating to 2 decimal places for easier visualization
4. Creating another column for analysis purposes, 'amount_ing', which bins the number of ingredients used in a recipe to either less (<= 9 ingredients total) or more (>9 ingredients total). This step is crucial for the comparison addressed in the main question by splitting the number of ingredients into two groups. 

Head of the dataframe after cleaning for analysis:

|   n_ingredients |   average_rating | ingredients   |
|----------------:|-----------------:|:--------------|
|               3 |             4.75 | less          |
|               3 |             5    | less          |
|              14 |             4.78 | more          |
|              11 |             5    | more          |
|               4 |             5    | less          |


#### Univariate Analysis
<iframe src="assets/ua2.html" width=800 height=600 frameBorder=0></iframe>

The histogram shown above shows the distribution of the 'n_ingredients' column for univariate analysis. This plot is very interesting since it seems to follow a general normal bell curve, with a little right skew. 

#### Bivariate Analysis
<iframe src="assets/ba2.html" width=800 height=600 frameBorder=0></iframe>

The above box plot shows the statistics for two groups (less vs. more ingredients) when compared by the values of average_ratings. The bivariate analysis is between the 'amount_ing' column, which was created according to the steps listed above, and the 'average_rating' column. 


#### Interesting Aggregates

Result of Pivot Table: (first column is n_ingredients)

|   n_steps |         1 |       3 |       5 |       7 |       9 |
|----------:|----------:|--------:|--------:|--------:|--------:|
|         1 | nan       | 4.79517 | 4.76132 | 4.64794 | 4.78049 |
|         2 |   5       | 4.75346 | 4.7334  | 4.74516 | 4.73867 |
|         3 |   5       | 4.66067 | 4.73608 | 4.70277 | 4.72598 |
|         4 |   4.66667 | 4.72085 | 4.74327 | 4.6781  | 4.7213  |
|         5 |   4.25    | 4.70573 | 4.6857  | 4.65083 | 4.60845 |


The above pivot table has index values of n_ingredients, not shown in table, column values of n_steps. The actual values in the table are aggregate means of average_ratings for each grouping of (n_ingredients, n_steps) in the pivot table. With this table, we can look at how average rating values change based on different number of steps and amount of ingredient used. 
