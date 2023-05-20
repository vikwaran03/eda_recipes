<title> Exploring the popularity of different recipes </title>

# Exploring the popularity of different recipes 

### Introduction:

The dataset considered in this project is the result of merging two datasets that were originally scraped from [food.com](https://www.food.com/). The first dataset contained information regarding the different recipes, and the second contained reviews and ratings of those recipes. When these two datasets were merged, the resulting dataframe can be used to answer many such questions regarding how different recipes are preffered, based on various variables. Taking this into account, my project will focus on the following question: <br>

<center> <i>Do recipes that require more ingredients tend to have higher average_ratings than recipes that require less ingredients?</i> </center><br>


The initial dataframe that my project takes into account has shape (234429 rows × 18 columns), after merging. Of these 18 columns, my question is heavily dependent on 3 columns: 'name' (recipe name), 'n_ingredients' (number of ingredients in recipe), and 'average_rating' (average rating of recipe). 

### Cleaning and EDA:

#### Data Cleaning:
Steps taken to clean dataset for EDA:<br>
1. Grouping by recipe name and aggregating the average rating and number of ingredients for each recipe
2. Changing the data type of number of ingredients from float to int, since it is not possible to have fractions of an ingredient (ex. 0.5 carrot is still considered 1 ingredient, not 0.5 ingredient)
3. Rounding all values in average_rating to 2 decimal places for easier visualization
4. Creating another column for analysis purposes, 'amount_ing', which bins the number of ingredients used in a recipe to either less (<= 9 ingredients total) or more (>9 ingredients total). This step is crucial for the comparison addressed in the main question by splitting the number of ingredients into two groups. 
5. The only columns necessary for analysis is the 'n_ingredients', 'average_rating', and 'ingredients' column, and since these columns are all cleaned, there is no need to unnecessarily clean other columns since it is not required for analysis. 

Head of the dataframe after cleaning for analysis:

|   n_ingredients |   average_rating | ingredients   |
|----------------:|-----------------:|:--------------|
|               3 |             4.75 | less          |
|               3 |             5    | less          |
|              14 |             4.78 | more          |
|              11 |             5    | more          |
|               4 |             5    | less          |


#### Univariate Analysis:
<iframe src="assets/ua2.html" width=800 height=600 frameBorder=0></iframe>

The histogram shown above shows the distribution of the 'n_ingredients' column for univariate analysis. This plot is very interesting since it seems to follow a general normal bell curve, with a little right skew. 

#### Bivariate Analysis:
<iframe src="assets/ba2.html" width=800 height=600 frameBorder=0></iframe>

The above box plot shows the statistics for two groups (less vs. more ingredients) when compared by the values of average_ratings. The bivariate analysis is between the 'amount_ing' column, which was created according to the steps listed above, and the 'average_rating' column. It seems as though both groups seem to have somewhat of the same trend as seen by the similarities in the corresponding box plots. 


#### Interesting Aggregates:

Result of Pivot Table: (first column is n_ingredients)

|   n_steps |         1 |       3 |       5 |       7 |       9 |
|----------:|----------:|--------:|--------:|--------:|--------:|
|         1 | nan       | 4.79517 | 4.76132 | 4.64794 | 4.78049 |
|         2 |   5       | 4.75346 | 4.7334  | 4.74516 | 4.73867 |
|         3 |   5       | 4.66067 | 4.73608 | 4.70277 | 4.72598 |
|         4 |   4.66667 | 4.72085 | 4.74327 | 4.6781  | 4.7213  |
|         5 |   4.25    | 4.70573 | 4.6857  | 4.65083 | 4.60845 |


The above pivot table has index values of n_ingredients, not shown in table, and column values of n_steps. The actual values in the table are aggregate means of average_ratings for each grouping of (n_ingredients, n_steps) in the pivot table. With this table, we can look at how average rating values change based on different number of steps and amount of ingredient used. 

### Assessment of Missingness:

#### NMAR Analysis:
It is plausible that the 'rating' column in the dataset is NMAR (Not Missing at Random), since users who may have not been satisfied by a recipe, may tend to not leave a rating, hence the values are NaN and are dependent on the missing values themselves. Collecting data regarding whether or not someone would repeat the recipe or share the recipe may give way to MAR missingess, since there is possibility that users who gave lower ratings are more likely not to share or repeat a recipe, compared to users who gave higher ratings. Hence, the missingness depends on the the new share/repeat data collected. 

#### Missingness Dependency:

After running missingness mechanism permutation tests, it can be concluded that the missingnes of values in the 'average_rating' column in the dataset does not depend on the 'minutes' column, since we fail to reject the null hypothesis in the permutation test. This relationship can also be shown via the horizantal barchart below, where you can see that there is no clear relationship between missing and not missing 'average_rating' values in comparison with several 'minute' values. 

<iframe src="assets/miss2.html" width=800 height=600 frameBorder=0></iframe>

### Hypothesis Testing:

#### Running a Permutation Test:

Considering the main project question listed above, we can test this question by running a permutation test with the following hypotheses:

Null Hypothesis: The proportion of recipes that use “less” ingredients have the same distribution of 5 star average ratings as recipes that use “more” ingredients, and any observed differences in our sample are due to random chance. 

Alternative Hypothesis: The proportion of recipes that use “less” ingredients do not have the same distribution of 5 star average ratings as recipes that use “more” ingredients. Observed differences in our samples cannot be explained by random chance alone. 

After running the permutation test according to the null hypothesis stated above, we fail to reject the null at alpha = 0.10 (10% significance level). The corresponding p-values is 0.98, which can be visualized by the histogram plotted below.

<iframe src="assets/ptest.html" width=800 height=600 frameBorder=0></iframe>

