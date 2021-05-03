# Movie-Data-Analysis
Master's program group assignment 
* Source data is pulled from https://www.kaggle.com/rounakbanik/the-movies-dataset

# Project Description:
* Created a logistic regression model in R to predict the likelihood of producing a great movie using variables such as movie runtime, genre, budget, etc. and determine which variables are most important in producting a great movie.
* Prepped data on 45k movies from the Full Movie Lens Dataset.
* Used dummy variables to break up genres into separate variables. 

# Introduction
The purpose of this report is to predict the likelihood of producing a great movie using variables like a
movie’s genre, its runtime, and its budget. To create this model, we imported data from the Movies Dataset
from Kaggle and created a logistic regression to predict success. Using this model, we show that certain
genres (like foreign films and family-related genres) and the runtime have a statistically significant effect on
a film being great, while a film’s budget has a negative, but negligible impact on greatness.
In this report, we will define a “great movie” as one that has a 7.5 or higher vote average within the dataset.
This threshold is above the center of the distribution shown below, and we believe it is a reasonably high
value to benchmark the critical success of a film.

![alt text](https://github.com/edonnally/Movie-Data-Analysis/blob/main/Average%20Movie%20Vote%20Score.PNG)

# EDA
In order to build the best model possible, we needed to refine the data we used before trying to get some
insights. We only included movies that exceeded 100 votes, revenues greater than 0, budgets greater than 0,
and runtimes that are greater than 0 but less than 360 minutes. This cleaning was done to ensure that the
movies we analyzed were properly vetted by consumers, and that our data would not be skewed by outliers.
These filters refined our dataset from over 45,000 observations to just above 13,000 observations.

Another part of the cleaning process was creating specific genre categories for our analysis. This was done
because there were 17 separate genres, and often they overlapped in terms of content (family and animation,
for example). So for this project, we created the following aggregated genre values:
• “familyplus” - either a comedy or animation or family film
• “actionpacked” - either an action or crime or thriller film
• “serious” - either a war film or documentary or history film
• “misc” - either a music film or TV movie

Additionally, we created a variable called budgetmillion, which as the name suggests, is the budget variable
divided by one million.
The runtime variable measures the length of each movie in minutes. The budget variable is the total budget
of the movie in dollars. We broke up genres into several different variables using dummy variables (binary 1s
or 0s). Rather than deal with the multitude of genres found in the data, we created new variables combining
genres that you might commonly see together; Familyplus is a combination of animation or family or comedy.
Serious is a combination of war or documentary or history. Misc is a combination of music or TVmovie.
Finally, actionpacked is a combination of action or adventure or crime or thriller. The final variable, foreign,
is a dummy variable used to see if the movie was produced outside of the United States. Shown below is a
graph that depicts the counts of each type of genre found in the data we used along with a table showing
statistics about our numeric variables:

![alt text](https://github.com/edonnally/Movie-Data-Analysis/blob/main/Count%20of%20Movies%20by%20Genre.PNG)

![alt text](https://github.com/edonnally/Movie-Data-Analysis/blob/main/Table1.PNG)

# Regression
The final model we came up with included familyplus, serious, actionpacked, runtime, budget and foreign.
The respective coefficients can be found in the table shown below. Nearly all these variables produced
statistically significant coeffecients; only foreign had a p-value that was slighly above .05. While these
coefficients are not directly interpretable to predict ratings, their sign (positive or negative) does indicate
the relationship each variable has with ratings. Familyplus, actionpacked, budget, and foreign all have a
negative relationship. Serious and runtime are the only two positive variables.

![alt text](https://github.com/edonnally/Movie-Data-Analysis/blob/main/Coefficient%20Table.PNG)

# Marginal Effects
This shows that making a serious movie with a relatively longer runtime ought to increase the probability
of making a well-rated film. The other variables in the model, however, will tend to decrease the chances of
making a well-rated movie if they are realized; The marginal effect on the probability of making a successful
movie if it is foreign (not produced by an American company) is –20.72% and the marginal effect of adding
an additional 1 million dollars to the budget of a movie from 5 million to 6 million is -.0061%. These effects
are shown below:

![alt text](https://github.com/edonnally/Movie-Data-Analysis/blob/main/MarginalEffects.PNG)


# Limitations

While this model does offer some useful insights, we realize that it has certain limitations. For example,
it does seem odd that a variable like budget is negative, but it is our theory that budget is likely small
and negative due to an abundance of well-reviewed smaller movies that have only a few ratings compared
to larger-budget films that have a lower rating due to a larger aggregation of reviews. The model seems
to suggest that decreasing the budget will lead to a higher rating, but we would argue that this negative
relationship merely indicates that high ratings cannot be achieved by throwing money at the production of
the movie.
We may also have an endogeneity issue with our model because we are basing the success of a movie on
the average vote rather than other measures that are available to us (like revenue, profit, or other metrics).
We decided against including variables like actors, directors, revenue, production companies due to these
variables being too cumbersome for a logistic model and their likelihood to create even more endogeneity
issues (popular actors and directors could create a feedback loop of good ratings). That being said, there
are likely still insights we could gain from using more variables like these and their absence in our model
could be confounding.
In a perfect world, we would obtain experimental data on these variables by creating nearly identical cuts
of movies and showing them to control groups, measuring the difference in ratings between cuts that have
a slightly different runtime, budget, tone, and other features. This would allow us to have a true baseline
for our analysis, as we would not have to depend on observational data and the presence of confounding
variables.
# Recommendations

Despite the limitations of our model, the significance of our findings ought not be overlooked. As previously
stated, budget does not have a positive relationship with high ratings according to our model; we interpret
this to mean that it is in the interest of our future movie-maker to spend only what is absolutely necessary
to realize their artistic vision. Expensive CGI or effects, if not necessary, will likely not add value to a movie
in itself. Additionally, going overboard on marketing expenses will likely not result in a higher rated movie.
Also, making a “Serious” movie, according to our model, is the best route to go in order to achieve the best
ratings. Choosing a historical setting or one having to do with war increases the probability that a movie
will be well-reviewed, so it is in the best interest of our future movie-maker to seek out stories that have
these elements. Likewise, a family movie performs slightly below other film types. That does not mean that
a director set on creating a children’s film should not make one; rather, it is something that he or she should
keep in mind and not be disappointed if it does not rate well.
As we have mentioned before, we excluded actors and directors from the analysis due to endogeneity issues.
Those factors, in essence, reflect an important factor to evaluating works of art. Quantifying greatness is a
hard task, and even though we think this model works well, it does not encapsulate what makes a movie
great: unique ideas, chemistry between actors, and an overall vision. Any future director or production
company must take these factors into account when creating their next magnum opus.

