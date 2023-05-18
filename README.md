# Exploring the popularity of different recipes

### Introduction:

The dataset considered in this project is the result of merging two datasets that were originally scraped from [food.com](https://www.food.com/). The first dataset contained information regarding the different recipes, and the second contained reviews and ratings of those recipes. When these two datasets were merged, the resulting dataframe can be used to answer many such questions regarding how different recipes are preffered, based on various variables. Taking this into account, my project will focus on the following question: <br>

<center> <i>How does the number of ingredients used affect the average rating of any given recipe?</i> </center><br>

The initial dataframe that my project takes into account has shape (234429 rows × 18 columns), after merging. Of these 18 columns, my question is heavily on 3 columns: 'name' (recipe name), 'n_ingredients' (number of ingredients in recipe), and 'average_rating' (average rating of recipe). 

### Cleaning and EDA:

#### Data Cleaning
Steps taken to clean dataset for EDA:<br>
1. Grouping by recipe name and aggregating the average rating and number of ingredients for each recipe
2. Changing the data type of number of ingredients from float to int, since it is not possible to have fractions of an ingredient (ex. 0.5 carrot is still considered 1 ingredient, not 0.5 ingredient)
3. Rounding all values in average_rating to 2 decimal places for easier visualization
4. Creating another column for analysis purposes, 'amount_ing', which bins the number of ingredients used in a recipe to either less (<= 9 ingredients total) or more (>9 ingredients total). This step is crucial for the comparison addressed in the main question by splitting the number of ingredients into two groups. 

Head of the dataframe before cleaning for analysis:

|   n_ingredients |   average_rating | ingredients   |
|----------------:|-----------------:|:--------------|
|               3 |             4.75 | less          |
|               3 |             5    | less          |
|              14 |             4.78 | more          |
|              11 |             5    | more          |
|               4 |             5    | less          |

Head of dataframe after cleaning for analysis:

#### Univariate Analysis

<iframe src="eda_recipes/assets/ua1.html" width=800 height=600 frameBorder=0></iframe>

#### Bivariate Analysis


#### Interesting Aggregates