--- 
title       : 'Modeling for Causal Inference with Regression'
description : 'This brief course will introduce you to modeling for causal inference, with practice using different kinds of regression models'
free_preview: true


--- 
## The Basics of Modeling Behavior
```yaml
type:VideoExercise 
key:812b575a73
lang:r
xp:50 
skills:1 

video_link: //player.vimeo.com/video/231746347
```

---
## Discrete Choice Analysis
```yaml
type:VideoExercise 
key:09bccc78e5
lang:r
xp:50 
skills:1 

video_link: //player.vimeo.com/video/231746571
```

--- 

## Examples of Discrete Choice Analysis 

```yaml
type: PureMultipleChoiceExercise
key: 4dfa681543
lang: r
xp: 50
skills: 1
```

Which of the following are examples where we might apply discrete choice analysis?

A) Learning the effect of a new cancer drug on life expectancy
B) Learning whether giving people informational brochures affects whether they take prescription drugs as prescribed, such as whether they take antibiotics for the entire duration of the prescription or whether they stop early once they feel that symptoms have disappeared.
C) Learning whether a certain plant thrives under warmer or colder weather.
D) Learning the effect of the income tax on whether people participate in the labor market or not.

`@hint`

`@possible_answers`
- A
- B
- C
- D
- A and C
- [B and D]

`@feedback`
- We might hope this drug works, but we're looking for examples of when people make choices. Try again.
- There is another answer that also qualifies, so try again.
- We are looking for examples of when humans make choices. Try again.
- There is another answer that also qualifies, so try again.
- In (A) and (C) we are still interested in causal effects, but now there are no people making decisions, so discrete choice analysis (usually) will not apply.
- Correct! These are both situations where a person is making a discrete choice. In (B) they are decided whether to take the drug as prescribed. In (D) they are deciding whether to participate in the labor market. Hence we can use discrete choice analysis to study the causal effects of various policies. In (A) and (C) we are still interested in causal effects, but now there are no people making decisions, so discrete choice analysis (usually) will not apply.



## OVERALL NOTE: I FEEL LIKE OUR CODING QUESTIONS SHOULD DEFAULT TO END WITH PEOPLE WRITING OUT AN ALGORITHM/MODEL BASED ON THEIR REGRESSION COEFFICIENTS. IT'S A MODELING CHAPTER, SO EACH CODING QUESTION SHOULD END WITH A MODEL, NOT JUST A VALUE. 

## OR AT LEAST, IT SHOULD PHRASE THE LAST QUESTION AS "THIS MODEL STATES THAT THE CAUSAL EFFECT OF X ON Y IS Z DOLLARS/POINTS"


--- 
## Let's Code: Kids Love Ice Cream
```yaml
type:VideoExercise 
key:
lang:r
xp:50 
skills:1 

video_link: //player.vimeo.com/video/379871879
```

--- 
## Kids Love Ice Cream: Part 1 - A Theory Before Data

You have been newly hired as a data analyst for ConsumerCore Inc., and your very first assignment is to go through a small dataset to learn about food consumption trends in Gluttown, Michigan. You want to spend a little time just thinking about the big picture, and to imagine some of the factors that you think will be important when it comes to how much ice cream people eat around Gluttown. After all, if people are making some discrete choices about when to eat ice cream, and maybe little kids love ice cream so much that they are the biggest causes of ice cream consumption in town. Could that be true? Let's spend a few minutes coming up with a simple theoretical model to get us started.


```yaml
type: NormalExercise
key: c28b49d735
lang: r
xp: 100
skills: 1
```
`@instructions`
- 1) Estimate your personal ice cream consumption per month and over a year.
- 2) Estimate the average adult's ice cream consumption per month and over a year.
- 3) Estimate the average child's ice cream consumption per month and over a year.
- 4) Use these numbers to calculate the average annual ice cream consumption for a family of 4.

`@hint`

`@pre_exercise_code`
```{r}

```

`@sample_code`
```{r}
Think back to how often you eat ice cream, how much your friends eat ice cream, how much ice cream you've eaten as a kid growing up, and how often you see people eating ice cream around town, or people picking up some ice cream at the store. People might get ice cream for lots of reasons, from celebrating birthdays to cooling down on a hot summer's day. Or if you are a little kid, because you begged your parents for it!

So we don't know yet how to predict what makes people eat ice cream, but we can start by imagining an initial model, and then we can try to find some data to help us get a more analytical sense of what drives eating lots of ice cream.

1a) First off, let's think about how much ice cream you personally eat in a single month, on average. Remember, you might expect to eat more during the hot months of summer than during the winter (or vice versa!), but start by taking a guess at how much you eat in an average month during the year. Let's measure it in pints (about 500ml). How many pints of ice cream do you think you eat in a month? 



1) And now, in the space below, multiply that by 12 to see how much ice cream that would be in a year.



2) Okay. Now let's think about other adults, and how much you think they might eat on average per month. How much ice cream do you think the average adult person eats, measured in pints (about 500ml) per month?



And now, in the space below, multiply that by 12 to see how much ice cream an average adult would eat in a year.




3) Kids love ice cream, as we all know, and you may think that kids eat more ice cream than older people do (on average). How much ice cream do you think the average child eats per month, measured in pints per year?



And now, in the space below, multiply that by 12 to see how much ice cream an average kid would eat in a year.




4) So let's use these numbers to do a simple equation to calculate how much ice cream a family of 4 would eat in an entire year (assuming this family has 2 adults and 2 children). Just plug your predicted numbers from above into this equation to provide our first model:

  total.ice.cream.per.family = 2*(your adult consumption per year) + 2* (your child consumption per year)

And now let's find out the answer by actually running that equation in R. What number do you get?


```

`@solution`
```{r}


```

`@sct`
```{r}
ex() %>% check_error()
success_msg("Great! That equation is our first model for ice cream consumption for an average family of 4 people in Gluttown, Michigan, and the calculated value is a predicted outcome. If you're like a lot of people, you hink kids eat more ice cream than adults, and you may even be assuming that children would eat ice cream all of the time if they could! Is it anywhere close to correct? Next, let's look at some data to see what a data-driven model can tell us about a family's ice cream consumption.")
```

--- 

## If Kids Drive Ice Cream Consumption, What Is Our Counterfactual?

```yaml
type: PureMultipleChoiceExercise
key: 
lang: r
xp: 50
skills: 1
```

If we are trying to use a model to estimate a causal effect, we need to have a clear counterfactual. Let's say we think kids eat more ice cream than adults, and we have a dataset that shows a list of families, how many kids they have, and how much ice cream they ate in total. What would a good counterfactual be to help us test the effect of having children on a family's ice cream consumption?

`@hint`

`@possible_answers`
- The difference between what children eat and what adults eat is positive (kids eat more)
- The difference between what children eat and what adults eat is negative (kids eat less)
- [The difference between what children eat and what adults eat is 0]

`@feedback`
- We may think that's ultimately true, but for a counterfactual, we need to define what would happen if kids have no effect at all. Try again.
- We may think that's the opposite of what we expect, but that's not really what a counterfactual is. For a counterfactual, we need to define what would happen if kids have no effect at all. Try again.
- Correct! Let's assume that children and adults eat exactly the same amount. That way, we can look for either a positive or negative treatment effect of children on a family's ice cream consumption.


--- 
## Kids Love Ice Cream: Part 2 - Data Discovery


```yaml
type: NormalExercise
key: c28b49d735
lang: r
xp: 100
skills: 1
```

You have been newly hired as a data analyst for ConsumerCore Inc., and your very first assignment is to go through a small dataset to learn about food consumption trends in Gluttown, Michigan. The topic is way too complicated to do a good experiment on, and ConsumerCore doesn't have anything like data from a really good survey to help you find out about the discrete choices that people make about how much ice cream to eat. 

Even though you don't have experimental or survey data, you decide to look at something fun in their data, and you see that there is information about the consumption of ice cream by 20 families in the town. Perhaps you can use these to find people's "revealed preferences" about ice cream. In other words, when people have a free choice about how much ice cream they eat, measuring that amount will reveal their personal preferences about ice cream, and that can be a useful way to find out out about people and the discrete choices they make, especially if they under-report how much ice cream they eat on surveys!

You start by finding out how much ice cream a household consume in a year by using the dataset `icecream` on 20 households.The data dictionary is below.

Data Dictionary:
   `consumption` - ice cream consumption (in pints)
   `children` - number of children in the family 
   `age` - average age of the children 

 
`@instructions`
- 1) Get a quick sense of the variable names and variable types 
- 2) Show the descriptive statistics of `consumption`, `children`, and `age`. 
- 3) What's the maximum number of children in a family for this sample?

`@hint`
- Use the `summary` function to generate a table of summary statistics about `icecream`.

`@pre_exercise_code`
```{r}
set.seed(1234)
children <- round(rnorm(20,3,4),0)
children[children<=0] <-0
age <- round(rnorm(20,7,5),0)
age[age<0] <-1
u <- rnorm(20,0,5)
consumption <- 100 + 4*children-3*age+u
icecream <- data.frame(consumption, children, age)
```


`@sample_code`
```{r}
# 1) First, let's take a quick glance at how the data is formatted. We can do this by looking at the first 6 observations with the head() command, so insert the name of our dataframe, icecream, into the head() command:



# Good. Now that you can see the names of variables and some of their values, we need to calculate some key summary statistics.

# 2a) We want the descriptive statistics of ice cream consumption, number of children in the family, and average age of the children. For each of these solutions, use the `summary` command to generate a table of summary statistics on each variable. We've done the first one for you, so select the following code and hit the "Run Code" button:

   summary(icecream$consumption)

# 2b) Woah, that's a lot of pints for a typical family in a year. Now repeat this command, but for the variable `children`:



# 2c) Okay, the median number of children is 1, which sounds pretty normal. Now repeat the summary command again, but for the variable `age`:



# 3) Good, it looks like the kids are as old as, well, kids. Now let's find out how many children are in our biggest family. If it's a number like 99, it's probably a typo and we should ignore it. You can use the `max` command to find this, or you can just type the answer in. The format for the max command is max(dataframe$variable):




# 4) To finish up, let's run a plot to see a visual representation of the data on two of the variables, the number of children in the families (on the x axis) and the amount of ice cream they eat (on the y axis). First let's just plot the points with the `plot()` command. Fill in (x,y) with our variables for the number of children and the amount of ice cream consumption in our dataframe `icecream`:

    plot(x,y)

Now let's plot a simple fit line to the plot with the abline() command:

    abline(x,y)
    
    
```

`@solution`
```{r}
head(icecream)
summary(icecream$children)
summary(icecream$age)
max(icecream$children)
plot(icecream$children, icecream$consumption)
abline(icecream$children, icecream$consumption)
```

`@sct`
```{r}
ex() %>% check_error()
success_msg("Great job. One data point to note is our max value for children in a family. As you can see in both our max() command and our plot, the largest family in this sample is unusually big, as it has 13 children in it. Descriptive statistics can help us detect extreme values. 13 children in a household seems like a lot. But is this observation an outlier? An outlier may result from variability or it may indicate measurement error (i.e., the survey participant writes down a wrong number). If it's the latter, we can exclude this observation from data. However, we are not sure whether this is the case. After all, there is a reality show featuring a family with 19 children. So, 13 children could be possible.")
```



--- 

## Kids Love Ice Cream: Part 3 - Using OLS to Find Modeling Factors 


```yaml
type: NormalExercise
key: de1f3cbf85
lang: r
xp: 100
skills: 1
```
It can be a bit difficult to decide where to start looking for connections, so let's begin with a question to help us frame the situation. Since we can guess that kids love ice cream, and that kids may eat more ice cream as they get older, does our data show any relationship between total ice cream consumption and the ages and number of children in a family?  Let's find the correlation between the number of children, their ages, and family ice cream consumption through a basic linear regression.

Data Dictionary:
   `consumption` - ice cream consumption (in pints)
   `children` - number of children in the family 
   `age` - average age of the children 

`@instructions`
- 1) Use the `lm` function to create a linear regression of children and age on ice cream consumption.
- 2) Use the `summary` function to generate a table of summary statistics about that regression.
- 3) Create an equation for a model of family ice cream consumption based on our results.

`@hint`
- The first step is to put the output of your `lm` command into a dataframe like this: regression<-with(dataframe, lm(outcome ~ variable1+variable2))
- Then output the summary statistics of that dataframe with summary(Solution1)

`@pre_exercise_code`
```{r}
set.seed(1234)
children <- round(rnorm(20,3,4),0)
children[children<0] <-0
age <- round(rnorm(20,7,5),0)
age[age<0] <-1
u <- rnorm(20,0,5)
consumption <- 100 + 4*children-3*age+u
icecream <- data.frame(consumption, children, age)
```

`@sample_code`
```{r}
# 1) The first step is to generate the results of a linear regression that looks at the correlation between our demographic variables and total ice cream consumption by each family. First use the `lm` function to create a linear regression of children and age on outcome variable, ice cream consumption:

# Note: If you've never run a regression with multiple independent variables in R before, the format for the lm() function is: lm(outcome ~ variable1+variable2))

      regression<-


# 2) Great. Now run the summary() function on `regression` to look at the correlation. Note the y intercept shows the base level of ice cream eaten in families with no children: 

      

# Now, let's stop and think. Are there any quick ways to look at these summary command results and determine how well our regression fits the data? If our data is a strange shape (e.g. not a normal distribution), then our linear model might not really match the various ups and downs in the data.

# One thing we can look do is look at a statistical test called the F-statistic. The F-statistic is very handy because it starts with the assumption that the variables have no effect (i.e. have a coefficient of 0), and provides a test to see if our combined group of coefficients is statistically different from that. It is similar to a t-statistic, but instead of checking the fit of a single variable, the F-statistic tests a group of variables.  Like in the t-statistic, we hope our F-statistic will have a p-value equal to or under .05. We won't worry about the actual value of the F-statistic, but we do want to make sure its p-value shows that it has statistical significance.


# 3) So, based on the results of the summary() command, what is the p-value on the F-statistic of our regression? Be precise and don't round!

    Solution3<-

```


`@solution`
```{r} 
regression<-lm(consumption~age+children)
summary(regression)
Solution3<-5.115e-11
```


`@sct`
```{r}
ex() %>% check_error()
ex() %>% check_object("regression") %>% check_equal()
ex() %>% check_object("Solution3") %>% check_equal()
success_msg("Nice job. ")
```


--- 

## Kids Love Ice Cream: Part 4 - Understanding the Output Table

```yaml
type: NormalExercise
key: 495f3df509
lang: r
xp: 100
skills: 1
```
Running a regression is the easy part, and before we can finish our argument for causality, we need to interpret our regression in the context of our theoretical framework, central question, and the limitations of our data. So let's break down the numbers and look at what they can (or can't) tell us about our main question about the impact of kids on a family's ice cream consumption.

`@instructions`
- 1) Run the summary() command on our model 
- 2) What's the coefficient on `children`?
- 3) What's the standard error of this estimate?
- 4) Fill out a model for ice cream consumption using these coefficients

`@hint`


`@pre_exercise_code`
```{r}
set.seed(1234)
children <- round(rnorm(20,3,4),0)
children[children<0] <-0
age <- round(rnorm(20,7,5),0)
age[age<0] <-1
u <- rnorm(20,0,5)
consumption <- 100 + 4*children-3*age+u
icecream <- data.frame(consumption, children, age)
model<-lm(consumption ~ children+age)

```



`@sample_code`
```{r}
# 1) There are several relationships we could choose to understand better, but let's start with a single but important one. What does our regression help illuminate between the number of children in a family and its total ice cream consumption?

# First, run the summary() command again on our equation of our first regression, `model`.




# 2) What is the coefficient on `children`? Don't round the number.

      Solution2<-

# Nice going. This result gives us an estimate for how many pints of ice cream each child eats in a family.


# 3) But what is the standard error for this coefficient? Now type in the standard error for regression on `children` below. Don't round the number:

      Solution3<-

      
# 4) Fill in the blanks of the following equation to create a model for family ice cream consumption based on our regression results from Solution2 (and don't round the numbers!):

      model<-###.#### + #.####*children - #.####*age

```

`@solution`
```{r}
summary(model)
Solution2<-3.5469
Solution3<-0.3380
model<-100.2988 + 3.5469*children - 3.2950*age
```

`@sct`
```{r}
ex() %>% check_error()
ex() %>% check_object("Solution2") %>% check_equal()
ex() %>% check_object("Solution3") %>% check_equal()
success_msg("Good work! Our coefficient on `children` has an error margin of roughly +/- 0.3, or a little less than 10%. It would be great if that error margin were smaller, and sometimes it's hard to tell at a glance whether that standard error should change our interpretation about the strength of our results.") 
```


---
## Kids Love Ice Cream: Part 5 - Statistical Significance Checks

```yaml
type: NormalExercise
key: a451f86d7c
lang: r
xp: 100
skills: 1
```


There are several numbers that the summary() function generates that that can help us decide whether our coefficients are statistically significant, so let's look at 3 of them: the t-statistic, the p-value, and the $R^$2 value. 

- **Interpreting t-statistics**
- A t-statistic of 0 is the worst case scenario. It means that we should have zero confidence in the statistical significance of our regression coefficient.
- In contrast, a t-statistic larger than +/-2 usually means that you can have over 95% confidence in your coefficient's significance, and the larger the t-statistic, the more confidence you can have in your coefficient's predictive power. 
- **Interpreting p-values**
- A p-values range from 0 to 1, and express the likelihood that our results are due to chance.
- Typically, p-values under 0.05 are considered statistically significant
- **Interpreting $R^2$ values**
- 0% indicates that the model explains none of the variability of the response data around its mean. 
- 100% indicates that the model explains all the variability of the response data around its mean. 

`@instructions`
- 1) Examine the t-statistic for our estimated effect of the number of children in a family on ice cream consumption
- 2) Examine the p-value for that estimate
- 3) Examine the R-squared value of our model
- 4) Determine what the R-squared value tells us about this model
- 5) Determine what the p-value tells us about this model
- 6) Choose the variable that is best at predicting family ice cream consumption

`@hint`
- **Interpreting t-statistics**
- A t-statistic of 0 is the worst case scenario. It means that we should have zero confidence in the statistical significance of our regression coefficient.
- In contrast, a t-statistic larger than +/-2 usually means that you can have over 95% confidence in your coefficient's significance, and the larger the t-statistic, the more confidence you can have in your coefficient's predictive power. 
- **Interpreting p-values**
- A p-values range from 0 to 1, and express the likelihood that our results are due to chance.
- Typically, p-values under 0.05 are considered statistically significant
- **Interpreting $R^2$ values**
- 0% indicates that the model explains none of the variability of the response data around its mean. 
- 100% indicates that the model explains all the variability of the response data around its mean. 


`@pre_exercise_code`
```{r}
set.seed(1234)
children <- round(rnorm(20,3,4),0)
children[children<0] <-0
age <- round(rnorm(20,7,5),0)
age[age<0] <-1
u <- rnorm(20,0,5)
consumption <- 100 + 4*children-3*age+u
icecream <- data.frame(consumption, children, age)
model<-lm(consumption ~ children+age)
summary(model)
```

`@sample_code`
```{r}
# We calculate the t-statistic by dividing the regression coefficient by its standard error—it's a quick way to help us see how precise our regression coefficient is. It can be positive or negative, but for now you can ignore the sign and look at the size of the result to learn about how statistically significant our coefficient is.

# 1) What's the t-statistic for the coefficient on `children`? Don't round the number.

      Solution1<-

# Nice. That is pretty far from 0 for a t-statistic, so we can very safely say that this is a statistically significant result.


# 2) Another test we can use is the p-value, which is a more common (and misused!) statistic that returns a value between 0 and 1. Let's see if our p-value is under 0.05, which is a standard goal for significance. What's the p-value for our coefficient on `children`? Don't round the number.

      Solution2<-

# Good. It's very safe to interpret that as a very strong sign of statistical significance!

# You now want to make sure that your regression closely represents what's happening in  your actual data. So we'll run another test of model fit by looking at the $R^2$ coefficient. The $R^2$ coefficient of determination is a statistical measure of how well a linear regression line approximates the real data points by telling you how much of the scattering of data points around the mean is explained by the model, from 0% - 100%.

# Of course, it's not always that simple if your data is nonlinear or on a subject that's generally hard to predict, so we can't always assume that a high $R^2$ is better than a low $R^2$. 


# 3) In this case, R-squared is a useful term, which is termed "Multiple R Squared" in this table to distinguish it from a different measure called Adjusted R Squared. What is the Multiple R-squared value is of this model? Don't round the number.

      Solution3<-
      
# So, we have calculated a p-value on our coefficients and an R-squared value for our model.

# A high R-squared value (close to 100%) means our model explains nearly all of the variance near the mean.
# A low R-squared value (close to 0%) means our model explains almost none of the variance near the mean.
# A p-value at or under 0.5 means our model is statistically significant.
# A p-value above 0.5 means that our model is not trustworthy.

# 4) Based on our R-squared values, would you say that our model explains the variation in the data? Type in "Yes", "No", or "Maybe" for Solution4:

      Solution4<-""


# 5) Based on our p-value for our coefficient on `children`, would you say that our model is statistically significant? Type in "Yes", "No", or "Maybe" for Solution5:

      Solution5<-""


# 6) Finally, what variable best predicts the amount of ice cream consumption per family?

      Solution6<-


```

`@solution`
```{r}
Solution1<-10.49
Solution2<-5.115e-11
Solution3<-0.9384
Solution4<-"Yes"
Solution5<-"Yes"
Solution6<-children
```

`@sct`
```{r}
ex() %>% check_error()
ex() %>% check_object("Solution1") %>% check_equal()
ex() %>% check_object("Solution2") %>% check_equal()
ex() %>% check_object("Solution3") %>% check_equal()
ex() %>% check_object("Solution4") %>% check_equal()
ex() %>% check_object("Solution5") %>% check_equal()
ex() %>% check_object("Solution6") %>% check_equal()
success_msg("Good work! Our t-statistic is 10.10, well above the 2 that reflects 95% confidence in our coefficient. In addition, our p-value of 0.00000005115 is well below our 0.05 goal. Finally, our $R^$2 value says that the data explains 93.8% of the variability in the data. We can have extreme confidence that our calculated coefficient on `children` is statistically significant. And because it's not 0, we can disprove our counterfactual, so we can say that this is a true average treatment effect of children on a family's ice cream consumption. Well, at least based on this little dataset, that is!")
```


--- 
## Let's Code: Income Inequality at FutureChew
```yaml
type:VideoExercise 
key:
lang:r
xp:50 
skills:1 

video_link: //player.vimeo.com/video/379871871
```


--- 
## Income Inequality at FutureChew: Part 1 - Starting Straight From the Data

```yaml
type: NormalExercise
key: 95ac91e75f
lang: r
xp: 100
skills: 1
```

Food-focused software company FutureChew is growing, and sometimes with success comes unwanted attention. In FutureChew's recent investor information packet, some average employee salary data was provided, and a financial analyst noticed that women at FutureChew seemed to earn less than men. The financial analyst ran a regression on the company salaries that they said proves that FutureChew discriminates against women.

The Director tells you that the company tries to ignore an employee's age when setting their salary, so you assume that's true and think about a model that bases income just on education, experience, and gender. So let's check out whether these variables seem to be correlated with salary in our data.

Data dictionary:

   `salary` - annual salary
   `female` - 1 if female
   `age` - age
   `exp` - work experience in years
   `educ` - education in years

`@instructions`
- 1) Take a look at the structure of the dataset and some initial variable values.
- 2) Take a guess at which 2 variables will be the most correlated.
- 3) Take a guess at which 2 variables will be the least correlated.
- 4) See how close your guesses were by looking at a correlation matrix.

`@hint`


`@pre_exercise_code`
```{r}
set.seed(123)
female <- rbinom(210,1,0.5)
age <- round(rnorm(210,40,8),0)
age[age<19] <- 19
exp <- age-25-rnorm(210,0,4)
exp[exp<0] <- 0
exp[exp>35] <-35
u <- rnorm(210,0,1)
data <- data.frame(female,age,exp)
data$educ <- round(rnorm(210,17,2),0)
data$educ[data$educ<11] <- 11
data$educ[data$educ>22] <- 22
loginc <- 8+.11*data$educ+0.09*data$exp-.5*female+u
loginc[loginc<9] <-9
data$salary<-exp(loginc)
data$salary<-round(data$salary,2)
```

`@sample_code`
```{r}

# 1) Let's start off by looking at the variables we have in the dataset from the FutureChew HR department. Let's find out what factors we can consider in our model by looking at the variable names and types in our dataset using the str(), head(), and/or summary() commands:





# Good. It looks like we have data on employee ages, years of work experience (`exp`), whether they are female or male, the number of years of education they have (`educ`), and their salaries (`salary`). There's also a variable called `loginc` that is the logarithmic value of their salary, but we can ignore that one.

# Now that we know what variables are in the dataframe, and have heard from the reporter that women tend to have lower salaries than men at FutureChew, let's take a moment step back and think about what our variables mean in a more general sense. We have variables that measure how much education someone has, how old they are, how much work experience they have, how much money they make, and whether they are male or female. Before we start digging into the numbers, let's think about a mental model of which of these factors are more likely to be connected than others. Which of the variables in our dataset do you think are likely to be highly correlated? Which are likely to have very little correlation?

# 2) Write down the pair of variables that you guess will be the most correlated into the blank spaces for `most.correlated`:

      most.correlated<-" " and " "

# 3)  Now write down the pair of variables you think will be the least correlated into the blank spaces for `least.correlated`:

      least.correlated<-" " and " "      


# 4) Now that you've thought about what a few parts of a person's life tend to be connected (and unconnected) to each other, let's see what our correlations are in our dataset through a correlation matrix. Run the cor() command on our dataframe `data`, and look for the highest and lowest correlation coefficients:

    cor()
    

```

`@solution`
```{r}
cor(data)
```

`@sct`
```{r}
ex() %>% check_error()
success_msg("Good work!  Did you guess correctly which pair of variables had the highest and lowest correlations? And do you see the correlation between `female` and `salary`?  We don't know if we can trust any of these numbers yet, but perhaps these results can lead to interesting questions. Let's keep going.")
```


--- 

## If FutureChew Pays Women Less, What Is Our Counterfactual?

```yaml
type: PureMultipleChoiceExercise
key: 
lang: r
xp: 50
skills: 1
```

If we are trying to use a model to estimate a causal effect, we need to have a clear counterfactual. Let's say we think that for one reason or another, women at FutureChew get paid less for the same jobs as men. What would a good counterfactual be to help us test the effect of gender on salaries at FutureChew?

`@hint`

`@possible_answers`
- In a regression of an "is female" variable on salary, the coefficient for the "is female" variable will be negative.
- [In a regression of an "is female" variable on salary, the coefficient for the "is female" variable will be 0.]
- In a regression of an "is female" variable on salary, the coefficient for the "is female" variable will be positive.

`@feedback`
- We may think that's ultimately true, but for a counterfactual, we need to define what would happen if being female has no effect at all on salaries. Try again.
- Correct. A good counterfactual would be to assume that being male or female has no affect on salaries, which we will see as a correlation of 9 0 in a regression.
- A counterfactual is not the opposite of what we may expect to find, it's what would happen if our "treatment" has no effect on the outcome. IN this case, the "treatment" is being female, so think about what coefficient that would be in a regression output table and try again.




--- 
## Income Inequality at FutureChew: Part 2 - Adjusting For Bias In Salary Numbers

```yaml
type: NormalExercise
key: 95ac91e75f
lang: r
xp: 100
skills: 1
```

Let's return to the data about salaries at FutureChew, and let's get a better sense of the distribution of salaries there. Are salaries pretty equal across the company, or are they bunched at the top or bottom? Are the worst-paid employees quite poor, or are they getting rich too? Let's start off by looking at a basic chart of salaries, look at the salaries of the best and worst paid employees, and decide if there's a good strategy for dealing with any bias in the salary distribution that might affect our analysis and interpretation.

`@instructions`
- 1) Sort the salaries in the dataframe from smallest to largest.
- 2) Look at the top 10 salaries and bottom 10 salaries at FutureChew.
- 3) Consider if wide range of salaries is a problem for interpretation.
- 4) Create a new variable to store log values of salaries to aid analysis.

`@hint`


`@pre_exercise_code`
```{r}
set.seed(123)
female <- rbinom(210,1,0.5)
age <- round(rnorm(210,40,8),0)
age[age<19] <- 19
exp <- age-25-rnorm(210,0,4)
exp[exp<0] <- 0
exp[exp>35] <-35
u <- rnorm(210,0,1)
data <- data.frame(female,age,exp)
data$educ <- round(rnorm(210,17,2),0)
data$educ[data$educ<11] <- 11
data$educ[data$educ>22] <- 22
loginc <- 8+.11*data$educ+0.09*data$exp-.5*female+u
loginc[loginc<9] <-9
data$salary<-exp(loginc)
data$salary<-round(data$salary,2)
data$log.salary<-log(data$salary)
```

`@sample_code`
```{r}

We've looked at some of the summary statistics of our dataframe `data`, but it will be helpful for our understanding of the range of salaries at FutureChew to see what the top 10 salaries are, and what the bottom 10 salaries are. If we have a really wide range of salaries, we need to worry about the bias that a few really high salaries (or a few really low salaries) might be making to our understanding of this data about the company.

# To begin with, let's run a simple histogram of salaries at FutureChew. How many people are getting paid near the bottom of the scale, and how many people are getting the maximum pay. Is it pretty evenly distributed? Run the hist() command on `data$salary` below to see:

    hist(data$salary)
    
# Ouch. That looks pretty skewed, but it's hard to tell what's really going on. There are a few simple things we can do.

# 1) Let's start by creating a sorted version of the `salary` variable. We can do this with the `sort` command, so fill in the command with the `salary` variable from our dataframe `data`:

    sorted.salary<-sort()

# Good. By default, R puts the lowest values at the top, and the highest values at the bottom, which we'll need to know for the following steps.
    
    
# 2a) Now let's take a look at the bottom 10 values of `sorted.salary`, which should now be at the top of the list. Let's use the head() command. Put in our variable `sorted.salary` where it says `X` in the command below:

    head(X, 10)

# Good. Those are all about the same, and that amount looks like they may be for poorly paid summer interns.


# 2b) Let's look at the top 10 salaries now. These should be at the bottom of the list, so let's use the tail() command, which has the same basic format as the head() command. Put our variable `sorted.salary` where it says `X` in the command below:

    tail(X, 10)
    
# Nice going.   


# 3) If you take a closer look at those numbers, you'll see that there are 2 people who make over $1 million, and all of the Top 10 make more than $500,000. That's a big range, and income is an example where large and small outliers can add complications to our analysis and interpretation. After all, a company of barely-paid workers that is owned by a single mega-billionaire would have a very skewed salary structure, and if they increased everyone's pay by 20%, it would make a vastly larger monetary benefit to the CEO compared to the workers. So we we should adjust how we look at the salary numbers.

#  Let's do a common tactic when looking at incomes by using the log values of the salaries, not the salaries themselves. As opposed to the exponential curve, where exponential changes to salaries would start of making relatively small differences but then quickly make them absolutely enormous, with log values we do the inverse. This means that small changes in log values start off making a big difference, but those differences become smaller over time. 

# Using a log version of our salaries makes some real world sense, because a salary increase from $0-$50,000 will make a much bigger difference in someone's life than adding an additional $50k to the salary of a millionaire. So let's convert the salaries to their log values, which is a common technique to help us avoid the complications that very large outlier salaries might add to our calculations.


# 4) Let's create a new variable within our dataframe `data` with these log values of our salaries. It is a simple command, so simply fill in our salary variable in for the `X` below:

    data$log.salary<-log(X)
    

```


`@solution`
```{r}
    hist(data$salary)
sorted.salary(sort(data$salary))
head(sorted.salary,10)
tail(sorted.salary,10)
data$log.salary<-log(data$salary)
```

`@sct`
```{r}
ex() %>% check_error()
success_msg("Nice job! Once again, these log values are harder to interpret as real-world salaries, and their changes are harder to interpret in terms of real-world changes, but this is a common technique for dealing with certain kinds of data where the range and scale can mislead you and your interpretation. Let's start using these log versions of salaries to keep our investigation going.")
```

--- 
## Income Inequality at FutureChew: Part 3 - Is there a problem?

```yaml
type: NormalExercise
key: 95ac91e75f
lang: r
xp: 100
skills: 1
```

This salary controversy is not news to FutureChew's Director of Human Resources. The Director doesn't think it's due to their company hiring policies, but she's not sure exactly what's going on. She knows it would be highly unethical to run an experiment that randomly changed people's salaries, so she's looking to models for an understanding of the situation. She also knows that it will be complicated, and the answer might not be completely clear. She hires you to be a consultant to look at the data and help her understand what's going on.

Let's start by looking at a model for the employee salaries at FutureChew. Here is a dataset `data` has 210 observations. Is the financial analyst correct? Does FutureChew have a gender inequality problem?

`@instructions`
- 1) Run a regression of gender, experience, and education on salaries at FutureChew, and look at the summary statistics
- 2) Identify the variable with the largest effect (either positive or negative)
- 3) Decide if that coefficient is statistically significant
- 4) Decide if that variable is enough to explain the variation in salaries at FutureChew

`@hint`


`@pre_exercise_code`
```{r}
set.seed(123)
female <- rbinom(210,1,0.5)
age <- round(rnorm(210,40,8),0)
age[age<19] <- 19
exp <- age-25-rnorm(210,0,4)
exp[exp<0] <- 0
exp[exp>35] <-35
u <- rnorm(210,0,1)
data <- data.frame(female,age,exp)
data$educ <- round(rnorm(210,17,2),0)
data$educ[data$educ<11] <- 11
data$educ[data$educ>22] <- 22
loginc <- 8+.11*data$educ+0.09*data$exp-.5*female+u
loginc[loginc<9] <-9
data$salary<-exp(loginc)
data$salary<-round(data$salary,2)
data$log.salary<-log(data$salary)
```

`@sample_code`
```{r}

# 1) We can use regression to help us determine the coefficients for each of these factors in an employee's income. Regress the independent variables `female`,`age`, `exp`, and `educ` on our new dependent variable `log.salary`, and run the summary() command to learn about the results.

      Solution1<-lm(X ~ A + B + C, Data=Z)
      summary()

# Great. The regression coefficient estimate in the (Intercept) row is suggesting that there's a positive relationship between these variables and someone's wage at FutureChew. Now let's dig down and find out more about what this regression can (or can't) tell us.
 

# 2) Which variable has a negative effect on salary?

     Solution2<-""


# 3) Is that coefficient statistically significant? Take a look at the p-value on that line. If it's below .05, we should say that it is significant. Enter "yes" or "no" as Solution3:

    Solution3<-""
    

#4) Because this variable is both statistically significant and different from the other variables, can we say that it's the single cause behind the wage imbalance between women and men at FutureChew? Answer "yes" or "no"

    Solution4<-""

```


`@solution`
```{r}
Solution1<-lm(salary ~ female + age + exp + educ, data)
summary(Solution1)
Solution2<-"female"
Solution3<-"yes"
Solution4<-"no"

```

`@sct`
```{r}
ex() %>% check_error()
success_msg("Good work! The data overall shows a positive correlation of age, experience, and education on an employee's wage, but it seems that the company does tend to pay their women less: this regression says that being female seems to put a downward pressure on your income. So the negative correlation we saw in the raw data does indeed seem to be a flag for gender discrimination. And the p-value on our `Age` estimate is nearing 1, so it is very not statistically significant. But this is a complex situation, and this initial regression may be masking other dynamics in the data. So before we declare `female` to be the single cause of lower wages for women at FutureChew, let's keep digging into the data.")
```



---

## Income Inequality at FutureChew: Part 4 - Omitted Variable Bias

```yaml
type: NormalExercise
key: ec90db4f0a
lang: r
xp: 100
skills: 1
```

As we know, we don't want to omit any variables in our regression that might be affecting outcomes, because that would create a bias in our results. However, we can also be clever and use the "omitted variable bias" as a tool to check whether our first guess at important factors was correct. 

If we remove a variable and nothing changes in our estimate, then that variable was probably not necessary. If we omit a variable and our estimate does change, the size and direction of the difference can show us more about the relationships between the variables, namely which ones are pushing our estimates up or down in any significant way. 

`@instructions`
- 1) Run a regression on the data that omits the variable `female`.
- 2) How does that change affect the coefficient for experience?
- 3) How does that change affect the coefficient for education?


`@hint`


`@pre_exercise_code`
```{r}
set.seed(123)
female <- rbinom(210,1,0.5)
age <- round(rnorm(210,40,8),0)
age[age<19] <- 19
exp <- age-25-rnorm(210,0,4)
exp[exp<0] <- 0
exp[exp>35] <-35
u <- rnorm(210,0,1)
data <- data.frame(female,age,exp)
data$educ <- round(rnorm(210,17,2),0)
data$educ[data$educ<11] <- 11
data$educ[data$educ>22] <- 22
loginc <- 8+.11*data$educ+0.09*data$exp-.5*female+u
loginc[loginc<9] <-9
data$salary<-exp(loginc)
data$salary<-round(data$salary,2)
data$log.salary<-log(data$salary)
```

`@sample_code`
```{r}

# Overall, the data shows a positive correlation experience, and education on an employee's hourly wage, but a negative correlation with being female. That first regression says that being female seems to put a downward pressure on your income, and it seems that the age of women at FutureChew is likely unrelated to their pay. 

# Let's see if our coefficients for that regression change (or don't change) if we **omit** a variable from the regression. If the coefficients don't change at all, then that variable is probably not affecting the overall dynamic for wages at FutureChew. But if the coefficients do change, then we should look deeper into that variable to learn more about what's going on in the data we have.

# 1) In this case, let's remove our gender variable from the regression to see if that makes any difference at all. Omit `female` from the regression, and just regress `age`, `exp`, and `educ` on `log.salary`. Then use the summary() command to see the results.

     Solution1<-
     summary()


# Nice job. Our intercept and coefficients have changed, although `age` still looks to be very non-statistically significant in this regression. So let's look closer at how the other coefficients have changed. 

# 2) In our original regression that included `female`, the coefficient for `exp` was 0.078503. What is the coefficient on `exp` now that we've omitted `female`? Don't round the number.

     Solution2<-

# Interesting. That's slightly lower than before.

# 3) Likewise, our original coefficient for education was 0.055333. What is the coefficient on `educ` now that we've omitted `female`? Don't round the number.

     Solution3<-

# Good job. That's also slightly lower and less statistically significant than before.



```




`@solution`
```{r}
Solution1 <- lm(salary ~ exp + educ, data)
summary(Solution1)
Solution2<-0.074001
Solution3<-0.051125

```

`@sct`
```{r}
ex() %>% check_error()
ex() %>% check_object("Solution2") %>% check_equal()
ex() %>% check_object("Solution3") %>% check_equal()
success_msg("Good work! Here, when we look just our dataset without a consideration of gender, the variables for education and experience aren't quite as correlated with salary as they are when we factor in gender through the variable `female`.  As we can see, those correlations with salary increase when we include our `female` variable in the regression, which is interesting. Why would including women's salaries bring those correlations up?  One potential interpretation is that for women to earn the same salary, they need to have more experience and education, so therefore when we focus on including `female`, we see higher correlations. That dynamic is hidden when we look at company salaries without the variable `female`. In addition, the fact that these correlations actually changed at all is a sign that `female` does indeed affect our outcome variable of `salary`. So it seems that FutureChew might really have an issue with gender bias in their salaries.")
```




---

## Income Inequality at FutureChew: Part  5 - Dealing With Multicollinearity 

```yaml
type: NormalExercise
key: 9398c86a31
lang: r
xp: 100
skills: 1
```

But there's more to this than just gender, education, and experience. There's also the factor of the employee's age: they might be surprisingly young for their education and experience, or they might be much older but still very new to the profession. However, we know that many of these variables will run in parallel: the older you are, the more likely you are to have more experience and more education. If we look at the details, are these variables actually functioning very differently from each other? Or are they so similar that we can drop one from our regression to reduce our standard errors and make our lives simpler?

`@instructions`
- 1) Run our regression model of FutureChew salaries with just our gender and experience variables.
- 2) If multicollinearity is a problem, drop a collinear variable and run another regression without it.

`@hint`


`@pre_exercise_code`
```{r}
set.seed(123)
female <- rbinom(210,1,0.5)
age <- round(rnorm(210,40,8),0)
age[age<19] <- 19
exp <- age-25-rnorm(210,0,4)
exp[exp<0] <- 0
exp[exp>35] <-35
u <- rnorm(210,0,1)
data <- data.frame(female,age,exp)
data$educ <- round(rnorm(210,17,2),0)
data$educ[data$educ<11] <- 11
data$educ[data$educ>22] <- 22
loginc <- 8+.11*data$educ+0.09*data$exp-.5*female+u
loginc[loginc<9] <-9
data$salary<-exp(loginc)
data$salary<-round(data$salary,2)
data$log.salary<-log(data$salary)
```


`@sample_code`
```{r}

# 1) Let's start by running our regression model of the effect of experience, education, and gender on salaries at FutureChew. Insert the correct variable and dataframe names below:

    Solution1<-lm(A ~ B + C + D, Z)
    summary()


# Good. Take a look again at the coefficients and our standard errors. Are there any coefficients that share similar sizes and signs? Sometimes, it makes sense to reduce the number of variables in your regression model if multiple variables are basically duplicating each others coefficients and increasing our standard errors, and when you have a large number of variables, it can help in interpretation. In this case, since education and experience are co-linear, they are basically giving us the same information as each other in our regression. We can save ourselves some complication, and hopefully reduce our standard error, by picking one of these two co-linear variables to drop from the regression. 

# However, you should not just drop any variable: it's better to ground your data science choices on your theoretical understanding of the larger system instead of just chasing the lowest p-values.

# But which one should we drop? If we have to pick one, in this case it may be best to pick experience over education. Why? Partially because it is more statistically significant (education has a p-value around .10), but we could always just be comfortable with reporting a coefficient with a larger p-value if we think it's still reflecting something important. The better reason is because of real-world framework that this data (partially) reflects. While it would be bad if employees were punished in salaries if they either have a lot of education or have a lot of experience, the bigger practical worry in a company is probably that long-term female employees keep getting passed over for promotion despite their years of hard work, which is going to be picked up more accurately in the experience variable than in education.  So let's stick with `exp` in our regression as we try to find a final answer on whether FutureChew pays their female employees less.


# 2) Now, re-run the regression without `educ` to give us our final model for salaries at FutureChew.

	Solution2<-
	summary()
	
	

```

`@solution`
```{r}
Solution1<-lm(salary ~ female + exp + educ, data)
	summary(Solution1)
Solution2<-lm(salary ~ female + exp, data)
	summary(Solution2)
```

`@sct`
```{r}
ex() %>% check_error()
ex() %>% check_object("Solution1") %>% check_equal()
ex() %>% check_object("Solution2") %>% check_equal()
success_msg("Nice job! Now let's move on to analyzing our estimated average treatment effect of gender on salaries at FutureChew.")
```



---

## Income Inequality at FutureChew: Part  6 - Our Average Treatment Effect

```yaml
type: NormalExercise
key: 9398c86a31
lang: r
xp: 100
skills: 1
```

We have looked at the HR data from FutureChew, converted salaries to their log versions, removed variables that are statistically insignificant, looked for omitted variable bias, and dealt with colinearity to reduce our standard errors. So now it's time to use our final, simplified regression model to calculate the Average Treatment Effect of being female on salaries at FutureChew. What is our estimate of it's actual impact on salaries?


`@instructions`
- 1) Run our final, simplified regression model of the effect of gender on salaries at FutureChew.
- 2) Write out our model for salaries at FutureChew using our selected coefficients.
- 3) Write out our Average Treatment Effect.

`@hint`


`@pre_exercise_code`
```{r}
set.seed(123)
female <- rbinom(210,1,0.5)
age <- round(rnorm(210,40,8),0)
age[age<19] <- 19
exp <- age-25-rnorm(210,0,4)
exp[exp<0] <- 0
exp[exp>35] <-35
u <- rnorm(210,0,1)
data <- data.frame(female,age,exp)
data$educ <- round(rnorm(210,17,2),0)
data$educ[data$educ<11] <- 11
data$educ[data$educ>22] <- 22
loginc <- 8+.11*data$educ+0.09*data$exp-.5*female+u
loginc[loginc<9] <-9
data$salary<-exp(loginc)
data$salary<-round(data$salary,2)
data$log.salary<-log(data$salary)
```


`@sample_code`
```{r}

# 1) Let's run our final regression model, which regresses the independent variables for experience and gender on the dependent variable, the log version of salaries at FutureChew. Fill in the command correctly below:

    model<- 
	
	
# 2) So let's fill in the coefficients on our model of salaries at FutureChew from the coefficients of that regression. (side note: this is not a line of R code, but it is still a representation of our model).

  Log of your salary at FutureChew =  intercept + #####*years of experience - ###### (if female) 

  
# 3) And what does that model say our ATE of being female is on your salary at FutureChew (in log terms)? Be precise and don't round!

  ATE <- -0.311018
  
  
  
```

`@solution`
```{r}
model<-lm(log.salary ~ female + exp, data)
	summary(model)
ATE<- -0.311018
```

`@sct`
```{r}
ex() %>% check_error()
ex() %>% check_object("Solution1") %>% check_equal()
ex() %>% check_object("ATE") %>% check_equal()
success_msg("Nice job! In the end, our data supports a model for salaries that uses a combination of gender and experience as its variables. It's a little harder to interpret log values of our salaries, but it still scales up quickly as salaries increase, which means that the effect of gender discrimination at FutureChew leads to big treatment effects on the salaries of the top executives. For example, at the low end, it means a salary of $10,900, once we subtract log(.3) from it, becomes $8,100. That $1,800 decrease probably means a lot to people at that pay scale, even if the overall numerical difference is not especially large in the labor market. But at the higher end, it means a salary of $597,000, once we subtract log(.3) from it, becomes $442,000. So that log(.3) is now accounting for a $150,000 decrease in pay! Future Chew does indeed need to do a lot more work to solve their gender inequality problems.")
```


--- 
## Confounders in Discrete Choice Analysis
```yaml
type:VideoExercise 
key:059e8eb292
lang:r
xp:50 
skills:1 

video_link: //player.vimeo.com/video/231746457
```

--- 

## Lots of Variables vs. Confounders in Discrete Choice Analysis 

```yaml
type: PureMultipleChoiceExercise
key: d81765e7b7
lang: r
xp: 50
skills: 1
```

Someone says "I included over 1,000 variables in my analysis. Since I have so many control variables, I do not have to worry about confounders." Do you agree?

`@hint`

`@possible_answers`
- Maybe
- Yes
- [No]

`@feedback`
- There is a yes or no answer for this. Try again.
- That's incorrect. What if there are key elements to the causal chain that were left out by chance or omission? Try again.
- Correct! The total number of variables you include generally has no relationship to whether you have to worry about confounders or not. All of these 1,000 variables might be just randomly generated numbers from the computer. In that case it's actually worse to include them than to leave them out! What matters is the substantive interpretations of these variables, and whether they measure all variables that might have a causal effect on outcomes.


---
## How Do People Choose Healthcare Plans?
```yaml
type:VideoExercise 
key:4608217f1d
lang:r
xp:50 
skills:1 

video_link: //player.vimeo.com/video/231746698
```

--- 

## Policy Questions About Health Insurance 

```yaml
type: PureMultipleChoiceExercise
key: fe92309865
lang: r
xp: 50
skills: 1
```

What policy questions might we be able to answer if we knew people's preferences over health insurance plans?

A) The effect of lowering health insurance premiums on the number of unemployed people.
B) Whether people care more about having prescription drugs covered or having contraceptive use covered.
C) Whether having health insurance makes people healthier.

`@hint`

`@possible_answers`
- A
- B
- C
- [A and B]
- A and C
- B and C

`@feedback`
- This is indeed one of the questions we could answer, but it's not the only valid one listed. Try again.
- This is indeed one of the questions we could answer, but it's not the only valid one listed. Try again.
- (C) is about the impact of having insurance on outcomes. If we only know people's preferences over insurance plans, we still don't have any data on health *outcomes* and hence preference data alone isn't enough to learn about the effect of insurance on outcomes. Try again.
- Correct. In (A) we are specifically interested in computing a counterfactual policy prediction: What would happen to market shares of each health plan——including the 'outside option' of not getting any health insurance plan and hence going uninsured—-if we changed plan premiums. (C) however is about the impact of having insurance on outcomes. If we only know people's preferences over insurance plans, we still don't have any data on health *outcomes* and hence preference data alone isn't enough to learn about the effect of insurance on outcomes.
- (C) is about the impact of having insurance on outcomes. If we only know people's preferences over insurance plans, we still don't have any data on health *outcomes* and hence preference data alone isn't enough to learn about the effect of insurance on outcomes. Try again.
- (C) is about the impact of having insurance on outcomes. If we only know people's preferences over insurance plans, we still don't have any data on health *outcomes* and hence preference data alone isn't enough to learn about the effect of insurance on outcomes. Try again.



--- 
## Reading the Data to Find Preferences
```yaml
type:VideoExercise 
key:0dd082cdd9
lang:r
xp:50 
skills:1 

video_link: //player.vimeo.com/video/231746940
```

--- 

## Reading the Coefficient Estimates 
```yaml
type: PureMultipleChoiceExercise
key: a4c08d7b61
lang: r
xp: 50
skills: 1
```

In the data presented in that last video, we saw the results of conditional logit models that showed that people disliked premiums about twice as much as they disliked out-of-pocket costs: the coefficients were -0.4330 and -0.2127 respectively. Now suppose that instead of these coefficients of -0.4330 and -0.2127, and ignoring any confidence intervals for now, that the values we saw were -0.4330 and -0.4227? What would we conclude?

`@hint` 

`@possible_answers`
- The data is inconsistent with the argument that rational people want the lowest overall cost for healthcare.
- [The data is consistent with argument that rational people want the lowest overall cost for healthcare.]
- The data are not sufficient to draw a conclusion either way.

`@feedback`
- Take another look at the number. In this question, the numbers are 0.0003 apart. Is that really enough difference to conclude that the preferences are different?
- Correct. If the coefficient estimates are roughly the same, then that means people care about these two characteristics roughly the same. And that is exactly what we would expect a rational person to think. Now, you could actually justify (C) as being correct, since I didn't tell you what the new confidence intervals / standard errors were! This is something we have to worry about in any finite sample, but here I'm ignoring it just for simplicity.
- If the confidence intervals were sufficiently large, then we would have to say that we can't tell either way. But here we are looking at the difference in coefficients while ignoring any confidence intervals, so try again.


--- 
## Let's Code: Making Money for Space Travel
```yaml
type:VideoExercise 
key:
lang:r
xp:50 
skills:1 

video_link: //player.vimeo.com/video/379871855
```

---
## Making Money for Space Travel, Part 1 - Exploring Predictions, Not Causality

```yaml
type: NormalExercise
key: f723ff2d39
lang: r
xp: 100
skills: 1
```
Statistical tools like regression can be used for finding causality under the right conditions, but more often they are used to create predictions, and predictions are not exactly like causal inferences. When someone can't argue that they've accounted for all confounders, and therefore can't claim to infer causality, they might still be able to use their data to get a pretty good sense of where future data may go, and that can be very useful for designing experiments to find causal links. So in this series of questions, we'll explore what some basic prediction methods might look like with non-normal data, and we'll look at how the predictions are different than causal inference.

Inspirational tech and business leader Aaron Musk is promising to deliver low cost "space tourism" to the world by building new space rockets with seats for normal people to buy and fly up into 1 hour orbit of the Earth, all while being piloted by highly trained astronaut monkeys. Musk's new company is called ApeX, and the idea is so cool and popular that you can see their logo can be seen everywhere. However, the company is secretly struggling for money, and almost all of its revenues come from merchandise sales from its millions of fans.

It has only had a website store for the last few years, but it has recently tried out some "pop-up" stores in the shopping malls of big cities. These are temporary stores selling their products, but ApeX is wondering whether the in-person nature of stores is changing what people buy. In particular, are people more likely to buy different items in different kinds of stores?

So part of ApeX's business needs are to find out how people decide to buy their products either in a store at the mall, on their computers, or on their cell phones, and to see how the location may vary depending on the price of the items. This will help ApeX create marketing strategies for each of those different platforms, and hopefully fund those monkey-piloted space rockets in just a couple of years.

Let's take a look at some of their observational data to help them model how their fans choose to buy items at different prices. The data set `Data` shows a single day's worth of purchases at the web store, the mobile store, and the pop-up stores. It contains 3 variables and over 17,000 observations. The data dictionary is below.

Data Dictionary:

   `ID` - subject identifier
   `payment` - choice of payment (store, mobile online, or web online)
   `value` - value of transaction in dollars

`@instructions`
- 1) Look at the basic summary statistics and structure of the dataframe.
- 2) Look at a graph of the data in aggregate to see if it forms a normal distribution.
- 3) Look at a graph of the data to see if we have any patterns of when people buy souvenirs in a store, on a phone, or on a computer.
- 4) Create a table that shows the average purchase price by the type of payment, along with the standard errors.

`@hint`


`@pre_exercise_code`
```{r}
library(plyr)
set.seed(123)

#Dataframe
ID <- 1:17400
payment <- c(rep("store",6000),rep("mobile",7000),rep("web",4400))
payment <- sample(payment, replace = FALSE)
value <- rep(NA,17400)
reward <- rep(NA,17400)
Data <- data.frame(ID,payment,value,reward)
Data$value[Data$payment == "store"] <- abs(round(rnorm(6000,16,50), digits=2))
Data$value[Data$payment == "mobile"] <- abs(round(rnorm(7000,150,40), digits=2))
Data$value[Data$payment == "web"] <- abs(round(rnorm(4400,100,30), digits=2))

# Item included in fan reward program can also influence payment choice
Data$reward[Data$payment == "store"] <- rbinom(6000,1,0.1)
Data$reward[Data$payment == "mobile"] <- rbinom(7000,1,0.5)
Data$reward[Data$payment == "web"] <- rbinom(4400,1,0.2)
Data$value[Data$value<1] <-.99
```


`@sample_code`
```{r}
# 1) We have a dataset that has merchandise transactions that includes in-store, mobile, and web payments. First, let's get a basic sense of our data by using the summary(), head(), and str() commands on the dataframe `Data`:



# It looks like the dataframe has an ID number for each transaction, a number assigned for the 3 locations of "store", "mobile", and "web", the value of each transaction, and some binary variable for rewards, which we'll ignore.

# 2) Second, let's take a look at the range of prices that people have paid on all of the stores just to see if they form a normal distribution (a bell curve), which is often a requirement for standard statistical analyses:

    plot(Data$value)

# That's definitely not a normal distribution. All together, these purchases form a uniform distribution, and there isn't any way to distinguish the prices paid in the pop-up stores from the mobile stores from the web stores. So let's try breaking these out by store type.

# 3) If we graph the results, can we see if there are any obvious trends that show a relationship between the price of an item and how people pay for it? Run the following R code to see (in-store is marked as Payment Type 1, mobile is marked as Payment Type 2, and web is marked as Payment Type 3): 

	  plot(Data$value, Data$payment, xlab="Item Cost", ylab="Payment Type")

# Interesting. Items purchased in stores are mostly middle-value transactions, mobile and online payments are used more frequently for lower value transactions, and web purhcases seem to be used for all levels of transactions.


# 4) Now create a 3 by 3 table that contains averages of `value` by `payment` in the first column and the standard deviations of `value` by `payment` in the second column. Provide the R code below. 

# Note: the format to do this with dplyr is: ddply(dataframe, ~variable1, variable2, mean=mean (value), sd=sd(value))

    ddply(dataframe, ~variable1, variable2, mean=mean (value), sd=sd(value))


```

`@solution`
```{r}
plot(Data$value)
plot(Data$value, Data$payment, xlab="Item Cost", ylab="Payment Type")
ddply(Data, ~payment, summarise, mean = mean (value), sd = sd(value))
```

`@sct`
```{r}
ex() %>% check_error()
success_msg("Good work! You can see the wide spread of purchase prices for the pop-up stores (#1), the mobile app (#2), and the web store (#3), but you should also notice that the average value of items purchased in each location are quite different. This means that ApeX might be able to optimize the matches between how much people want to spend and where they want to spend it. Let's try making some predictive models to see if we can guess where to sell some new products with different price points.")
```



---

##  Making Money for Space Travel,  Part 2 - Linear Probability Model

```yaml
type: NormalExercise
key: 8aa7765019
lang: r
xp: 100
skills: 1
```

ApeX is coming out with 2 new souvenirs: a $10 bumper sticker that they plan to be exclusively sold in their physical pop-up stores, and a $200 wooden model of the ApeX rocket for sale both online and in stores.

The company is trying to predict how people are likely to buy these two items: will the $10 bumper stickers be a good match for the prices people typically pay in stores, or should they be sold only online? Will people want to see the more expensive wooden rocket model in a store before they buy it? Let's look at their data and use a few different prediction models to make an educated guess.

Data Dictionary:

   `ID` - subject identifier
   `payment` - choice of payment (store, mobile, or web)
   `value` - value of transaction in dollars

`@instructions`
- 1) Create a dummy variable called `online` that with binary values to mark whether someone paid in-store or a via mobile/web.
- 2) Run a linear probability regression of our independent variable `value` on our dependent variable `online`
- 3) What is this model's regression coefficient for `value`?
- 4) Is that statistically significant?
- 5) Run a prediction with this model for items priced at $10 and $200.
- 6) What's the probability for buying a $10 online?
- 7) What's the probability for buying a $10 item in a pop-up store?
- 8) What's the probability for buying a $200 item online?

`@hint`


`@pre_exercise_code`
```{r}
set.seed(123)
#Dataframe
ID <- 1:17400
payment <- c(rep("store",6000),rep("mobile",7000),rep("web",4400))
payment <- sample(payment, replace = FALSE)
value <- rep(NA,17400)
reward <- rep(NA,17400)
Data <- data.frame(ID,payment,value,reward)
Data$value[Data$payment == "store"] <- abs(round(rnorm(6000,16,50), digits=2))
Data$value[Data$payment == "mobile"] <- abs(round(rnorm(7000,150,40), digits=2))
Data$value[Data$payment == "web"] <- abs(round(rnorm(4400,100,30), digits=2))

# Qualifying purchase for reward program can also influence payment choice
Data$reward[Data$payment == "store"] <- rbinom(6000,1,0.1)
Data$reward[Data$payment == "mobile"] <- rbinom(7000,1,0.5)
Data$reward[Data$payment == "web"] <- rbinom(4400,1,0.2)
Data$value[Data$value<1] <-.99

```

`@sample_code`
```{r}
# 1) Create a new dummy variable `online` with values 1 or 0 that describe whether the person used online or not. In other words, `online` is 0 if the person used a web or mobile online, 1 if he/she used store. Then, add this variable `online` to the dataset `Data`. Provide the R code below.

    online <- rep(1,17400)
    online[which(Data$payment == "store")] <- 0
    Data$online <- online

# Then we can estimate how the value of transaction influence the probability of using store or online. One way to estimate this probability is to use Linear Probability Model (LPM). LPM works like a normal linear regression model, but the dependent variable is binary. This gives us a way to have a "yes" or "no" answer to the research question we are asking in the regression. In this case, our question is "Did people buy products"

# 2) Regress `online` on `value`, and then look at summary results. 

	  lpm<-lpm<-lm(X ~ Y, data=Z)
	  summary()
	  
# 3) What's the coefficient on the independent variable, `value`? Don't round the number.

    coefficient.lpm<-
    
# 4) Is that coefficient statistically significant? Fill in "yes" or "no" below.

    lpm.is.significant<-""

# The coefficient on `value` is 0.0059 (0.57%), which is the change in the probability that a person buys something online for an $1 increase in transaction value.  A predicted value $\widehat{online}$ is the predicted probability that the dependent variable `online` equals one, given `value`.

    $P(\widehat{online = 1}) = 0.06465 +  0.005924 \times value$

# 5) Let's use the predict() function with this linear probability model and two specific prices for potential items: $10 and $200. That code is provided below:

    predict(lpm, data.frame(value = c(10,200)), type = "response")

# 6) What is the probability of someone buying a $10 item online?

     solution3<-

# 7) If that's the probability for buying it online, what does that mean the probability is for buying a $10 item in a pop-up store in a mall?

     solution4<-
     
# 8) What does this model say is the probability of someone buying a $200 item online?

     solution5<-

     
```

## NOT SURE IF SOLUTIONS WORK FOR 3 AND 4
  
`@solution`
```{r}
online <- rep(1,17400)
online[which(Data$payment == "store")] <- 0
Data$online <- online
lpm<-lm(online ~ value, data=Data)
summary(lpm)
coefficient.lpm<-
lpm.is.significant<-"yes"
predict(lpm, data.frame(value = c(10,200)), type = "response")
probability.online.if.value.10<-12
probability.popup.if.value.10<-88
probability.online.if.value.200<-125
```

`@sct`
```{r}
ex() %>% check_error()
success_msg("Good work! Linear probability models are often the easiest to interpret because they generate a simple, straight line of predicted outcomes. However, they're not always the best choice to end with. For example, the math behind this model doesn't automatically stop when the probability hits 0 or 1. You should see that for a $10 transaction, the expected probability of paying online is 13% . For a transaction with $200 value, your expected probability of buying online should be 125%. That's not very helpful, because that second number is a problem: how can a probability larger than 100%? That's impossible. This is the problem with the Linear Probability Model (LPM). The model can actually produce probabilities outside [0,1]. So let's look at 2 other kinds of models to help us avoid this potential issue.")
```



---
##  Making Money for Space Travel,  Part 3 - Trying A Non-Linear Logit Model

```yaml
type: NormalExercise
key: cbe1960334
lang: r
xp: 100
skills: 1
```

To avoid the potential issue of getting negative probabilities generated by a linear probability model, analysts and researchers often turn to range of numbers that must be greater than 0 by definition: logarithms. So next we will take a look at a common pair of modeling approaches that use logarithms to guarantee positive probabilities: logistic regression models, also known as "logit" models, and probabilistic regression models, also known as "probit" models. Of course, while we know we'll actually be getting positive probabilities from them, they are a little harder to immediately understand because they use logarithms rather than regular numbers, and each of these two methods has its strengths and weaknesses. 

Let's start by trying a logit model, which you will often see when your data has binary values of 0 or 1 in your independent variables. In logit regression, the predicted values are calculated using: 

$P (Y = 1|X) = \frac{1}{1+e^{-(\hat{\beta_{0}}+\hat{\beta_{1}}X)}}$

So let's see if a logit model has a better fit to our data than the Linear Probability Model did.


Data Dictionary:

   `ID` - subject identifier
   `payment` - choice of payment (store, mobile online, or web online)
   `value` - value of transaction in dollars

`@instructions`
- 1) Run a logit regression of our independent variable `value` on our dependent variable `online`
- 2) What is this model's regression coefficient for `value`?
- 3) Is that statistically significant?
- 4) Run a prediction with this model for items priced at $40 and $125.
- 5) What's the probability for buying a $40 item online?
- 6) What's the probability for buying a $40 item  in a pop-up store?
- 7) What's the probability for buying a $125 item online?
- 8) What's the probability for buying a $125 item in a pop-up store?

`@hint`


`@pre_exercise_code`
```{r}
set.seed(123)
#Dataframe
ID <- 1:17400
payment <- c(rep("store",6000),rep("mobile",7000),rep("web",4400))
payment <- sample(payment, replace = FALSE)
value <- rep(NA,17400)
reward <- rep(NA,17400)
Data <- data.frame(ID,payment,value,reward)
Data$value[Data$payment == "store"] <- abs(round(rnorm(6000,16,50), digits=2))
Data$value[Data$payment == "mobile"] <- abs(round(rnorm(7000,150,40), digits=2))
Data$value[Data$payment == "web"] <- abs(round(rnorm(4400,100,30), digits=2))

# Qualifying purchase for reward program can also influence payment choice
Data$reward[Data$payment == "store"] <- rbinom(6000,1,0.1)
Data$reward[Data$payment == "mobile"] <- rbinom(7000,1,0.5)
Data$reward[Data$payment == "web"] <- rbinom(4400,1,0.2)
Data$value[Data$value<1] <-.99

online <- rep(1,17400)
online[which(Data$payment == "store")] <- 0
Data$online <- online
myprobit<-glm(online ~ value, family = binomial(link = "probit"), data = Data)
mylogit<-glm(online ~ value, family = binomial(link = "logit"), data = Data)
lpm<-lm(online ~ value, data=Data)

```


`@sample_code`
```{r}
# There are 2 commonly paired ways of making predictions that return non-linear predictions, which might fit our particular dataset a bit better than our previous linear model. So we will start with a logit model.

# 1) Try it for yourself and run a logit regression of `online` on `value`. Fill in the R code below, where X is the dependent variable, Y is the independent variable, and Z is the name of the dataframe:

    Solution1<-glm(X~Y, family = binomial(link="logit", data = Z))
    summary()
    
# 2) What's the coefficient on the independent variable? Don't round the number.

    coefficient.logit<-
    
# 3) Is that coefficient statistically significant? Fill in "yes" or "no" below.

    logit.is.significant<-""

# Once again, that coefficient is very small, and is arguably too small to make a real world difference in marginal cases. But it is very statistially significant, so we can be confident that it's a real statistical relationship. So let's use this model to make some predictions about how likely someone is going to buy something at a certain price in the online and pop-up mall stores.

# 4) Let's run the predict() function again to find out this model's probability of purchasing items at two price points, this time a $40 t-shirt and a $125 photo signed by Aaron Musk himself:

  predict(mylogit, data.frame(value = c(40,125)), type = "response")

# 5) Using a logit model, what's the expected probability of paying online for a $40 transaction? Provide the R code below.

    probability.online.if.value.40<-

# 6) So what's the expected probability they will buy it in a pop-up store at the mall? 

    probability.popup.if.value.40<-

# 7) How will the probability of paying online change if the value of transaction is $125? Provide the R code below.

    probability.online.if.value.125<-

# 8) So what's the expected probability they will buy it in a pop-up store at the mall? 

    probability.popup.if.value.125<-
    






```

## NOT SURE IF SOLUTIONS 2 AND 3 WORK

`@solution`
```{r}
mylogit<-glm(online ~ value, family = binomial(link = "logit"), data = Data)
	summary(mylogit)
coefficient.logit<-
logit.is.significant<-"yes"
predict(mylogit, data.frame(value = c(40,125)), type = "response")
probability.online.if.value.40<-14
probability.popup.if.value.40<-86
probability.online.if.value.125<-96
probability.popup.if.value.15<-4

```

`@sct`
```{r}
ex() %>% check_error()
ex() %>% check_object("Solution1") %>% check_equal()
ex() %>% check_object("Solution2") %>% check_equal()
ex() %>% check_object("Solution3") %>% check_equal()
success_msg("Good work! Now we see that the predicted probabilities fall within 0 and 1, if just barely for the most expensive items. And it looks like the cheapest items are more likely to sell in the pop-up stores at the mall, and the most expensive items are basically guaranteed to only be purchased online. Now let's try using a probit model as well, which is commonly compared to a logit model.")
```




---

##  Making Money for Space Travel,  Part 4 - Trying A Non-Linear Probit Model Instead

```yaml
type: NormalExercise
key: ed84d2c77d
lang: r
xp: 100
skills: 1
```

There's another kind of probability model that we should check before we're done called a probit model, and it's often done as a counterpart to logit models, so let's try that too. In probit regression, the predicted values are calculated using as a cumulative probability distribution function of standard normal distribution, which starts out at 0 and maxes out at 1, like this:
 
$P (Y = 1|X) = \phi(\hat{\beta_{0}}+\hat{\beta_{1}}X)$

Thus, thepredicted values are bounded between 0 and 1. Let's see what a probit model can do for predicting our data.

Data Dictionary:

   `ID` - subject identifier
   `payment` - choice of payment (store, mobile online, or web online)
   `value` - value of transaction in dollars

`@instructions`
- 1) Run a probit regression of our independent variable `value` on our dependent variable `online`
- 2) What is this model's regression coefficient for `value`?
- 3) Is that statistically significant?
- 4) Run a prediction with this model for items priced at $65 and $75.
- 5) What's the probability for buying a $65 item online?
- 6) What's the probability for buying a $65 item in a pop-up store?
- 7) What's the probability for buying a $75 item online?
- 8) What's the probability for buying a $75 item in a pop-up store?

`@hint`


`@pre_exercise_code`
```{r}
set.seed(123)
#Dataframe
ID <- 1:17400
payment <- c(rep("store",6000),rep("mobile",7000),rep("web",4400))
payment <- sample(payment, replace = FALSE)
value <- rep(NA,17400)
reward <- rep(NA,17400)
Data <- data.frame(ID,payment,value,reward)
Data$value[Data$payment == "store"] <- abs(round(rnorm(6000,16,50), digits=2))
Data$value[Data$payment == "mobile"] <- abs(round(rnorm(7000,150,40), digits=2))
Data$value[Data$payment == "web"] <- abs(round(rnorm(4400,100,30), digits=2))

# Qualifying purchase for reward program can also influence payment choice
Data$reward[Data$payment == "store"] <- rbinom(6000,1,0.1)
Data$reward[Data$payment == "mobile"] <- rbinom(7000,1,0.5)
Data$reward[Data$payment == "web"] <- rbinom(4400,1,0.2)
Data$value[Data$value<1] <-.99

online <- rep(1,17400)
online[which(Data$payment == "store")] <- 0
Data$online <- online
# INCLUDE ANSWER FROM PREVIOUS QUESTION HERE
```


`@sample_code`
```{r}

# 1) Now, run a probit regression of `online` on `value`. Fill in the R code below, where X is the dependent variable, Y is the independent variable, and Z is the name of the dataframe:

    myprobit<-glm(X ~ Y, family = binomial(link = "probit"), data = Z)
	  summary()

# 2) What's the coefficient on the independent variable? Don't round the number.

    coefficient.probit<-
    
# 3) Is that coefficient statistically significant? Fill in "yes" or "no" below.

    probit.is.significant<-""

# 4) And just like our other two models, the coefficient is tiny, but we'll work with this model to see what kind of shopping behavior it predicts. Let's run the predict() function one more time, this time with our probit model and with two new item prices, a $65 hooded sweatshirt and a $75 bottle of ApeX branded wine.

    predict(myprobit, data.frame(value = c(65,75)), type = "response")

# 5) Using probit, what's the expected probability of buying something online for a $65 transaction? 

    probability.online.if.value.65<-

# 6) So what's the expected probability they will buy a $65 item in a pop-up store at the mall? 

    probability.popup.if.value.65<-

# 7) What probability does probit give you of buying something online if the value of transaction is $75?

    probability.online.if.value.75<-

# 8) So what's the expected probability they will buy it in a pop-up store at the mall? 

    probability.popup.if.value.75<-
    






```

`@solution`
```{r}
myprobit<-glm(online ~ value, family = binomial(link = "probit"), data = Data)
summary(myprobit)
coefficient.probit<-
probit.is.significant<-"yes"
predict(myprobit, data.frame(value = c(65,75)), type = "response")
probability.online.if.value.65<-42
probability.popup.if.value.65<-58
probability.online.if.value.75<-55
probability.popup.if.value.75<-45
```

`@sct`
```{r}
ex() %>% check_error()
success_msg("Good work! This probit is very, very close to our logit model, and just like the logit and linear probability models, it basically says that the more expensive a product is, the more likely it will be purchased online. But as we have checked different price values, the more we check for predictions for prices around $65-$75, the more the odds get closer to 50%. So maybe there's a price in each model where there is balance point between online and in-person store purchases. Let's do one last check of model fit before we make any conclusions, though.")
```

---
# Making Money for Space Travel,  Part 5 - Checking Model Fits with AIC Values

```yaml
type: NormalExercise
key: 
lang: r
xp: 100
skills: 1
```

To see whether the logit or the probit model fits our data the best, let's look again at the AIC values for each. Once again, the model with the highest AIC value has the best fit (even if that value is still negative!). Which model fits the data best, according to the AIC values?

`@pre_exercise_code`
```{r}
set.seed(123)
#Dataframe
ID <- 1:17400
payment <- c(rep("store",6000),rep("mobile",7000),rep("web",4400))
payment <- sample(payment, replace = FALSE)
value <- rep(NA,17400)
reward <- rep(NA,17400)
Data <- data.frame(ID,payment,value,reward)
Data$value[Data$payment == "store"] <- abs(round(rnorm(6000,16,50), digits=2))
Data$value[Data$payment == "mobile"] <- abs(round(rnorm(7000,150,40), digits=2))
Data$value[Data$payment == "web"] <- abs(round(rnorm(4400,100,30), digits=2))

# Qualifying purchase for reward program can also influence payment choice
Data$reward[Data$payment == "store"] <- rbinom(6000,1,0.1)
Data$reward[Data$payment == "mobile"] <- rbinom(7000,1,0.5)
Data$reward[Data$payment == "web"] <- rbinom(4400,1,0.2)
Data$value[Data$value<1] <-.99

online <- rep(1,17400)
online[which(Data$payment == "store")] <- 0
Data$online <- online
# INCLUDE ANSWER FROM PREVIOUS QUESTION HERE
```

`@hint`

`@sample_code`
# 1) Run each of our 3 models one more time so we can look at the summary statistics, including the AIC values for the logit and probit models. In each o

# Generic form for a linear probability model:

    lpm<-lm(X ~ Y, data=Z)
    summary(lpm)

# Generic form for a logit regression model: 

    mylogit<-glm(X~Y, family = binomial(link="logit", data = Z))
    summary()

# Generic form for probit regression model:

    myprobit<-glm(X ~ Y, family = binomial(link = "probit"), data = Z)
	  summary()

# 2) The logit and probit models had better fits than the linear probability model, and between logit and probit models, the one with the highest AIC value is probably the one that provides the closest fit to all of the data points in our dataframe. Which model has the highest AIC value? Enter in "logit" or "probit" below:

    Highest.AIC<-""


`@solution`
```{r}
lpm<-lm(online ~ value, data=Data)
mylogit<-glm(online ~ value, family = binomial(link = "logit"), data = Data)
myprobit<-glm(online ~ value, family = binomial(link = "probit"), data = Data)
Highest.AIC<-"probit"
```

`@sct`
```{r}
ex() %>% check_error()
success_msg("Great job! The probit model has a very slightly higher AIC value, which means it technically is the closest match to our data. However, all 3 models had regression coefficients for our independent variable, `value`, that were similarly small but extremely statistically signficant. So now let's make a decision on what these three prediction models are telling us.")
```



--
## Do Our Data Identify The Cause Of Our Outcomes?

```yaml
type: PureMultipleChoiceExercise
key: 
lang: r
xp: 50
skills: 1
```

To summarize what we found in the ApeX purchasing data, we tried multiple models to help us predict how consumers might want to purchase ApeX's newest fan products, a $10 bumper sticker and a $200 wooden rocket model. The results of these models can be seen in the graph to the right.

We found that the logit and probit models matched the data better than our linear probability model, and that logit and probit models always gives us a probability between 0 and 100%. All of the models seem to meet up around a single point, where we can interpret our customers are making the basic choice between buying something in person and buying it online.

Now that we have run these predictive models, would you say that our data provide enough information to tell us what exactly about the pop-up stores *causes* consumers buy to less expensive items in pop-up stores than they do online?

`@hint`

`@sample_data`
```{r}
set.seed(123)
#Dataframe
ID <- 1:17400
payment <- c(rep("store",6000),rep("mobile",7000),rep("web",4400))
payment <- sample(payment, replace = FALSE)
value <- rep(NA,17400)
reward <- rep(NA,17400)
Data <- data.frame(ID,payment,value,reward)
Data$value[Data$payment == "store"] <- abs(round(rnorm(6000,16,50), digits=2))
Data$value[Data$payment == "mobile"] <- abs(round(rnorm(7000,150,40), digits=2))
Data$value[Data$payment == "web"] <- abs(round(rnorm(4400,100,30), digits=2))

# Qualifying purchase for reward program can also influence payment choice
Data$reward[Data$payment == "store"] <- rbinom(6000,1,0.1)
Data$reward[Data$payment == "mobile"] <- rbinom(7000,1,0.5)
Data$reward[Data$payment == "web"] <- rbinom(4400,1,0.2)
Data$value[Data$value<1] <-.99

online <- rep(1,17400)
online[which(Data$payment == "store")] <- 0
Data$online <- online

lpm<-lm(online ~ value, data=Data)
myprobit<-glm(online ~ value, family = binomial(link = "probit"), data = Data)
mylogit<-glm(online ~ value, family = binomial(link = "logit"), data = Data)

value <- Data$value
plot(value,online,xlab = "value of transaction",ylab="probability of buying online")
curve(predict(myprobit,data.frame(value=x),type="resp"),add=TRUE,col="red")
curve(predict(mylogit,data.frame(value=x),type="resp"),add=TRUE,col="blue")
curve(predict(lpm, data.frame(value=x),type="resp"),add=TRUE,col="green")
legend("bottomright",legend = c("Probit","Logit"),col=c("red","blue"),inset = c(0.1,0.1),lwd=1)
```


`@possible_answers`
- Yes
- [No]

`@sct`
```{r}
msg1= "No, try again."
msg2= "That's correct, we cannot tell the reasons why people prefer to buy less expensive items in person and more expensive items online. This is one of the reasons that we cannot claim that this is a causal effect. We clearly have confounding variables that we are not accounting for. But we do have a prediction that our consumers' behavior was changing between $70-$80 purchases, and perhaps that insight will allow us to conduct experiments or gather more observational data in the future to try to learn about the causality involved."
ex() %>% check_mc(2, feedback_msgs = c(msg1, msg2))
```


--
## Making a Decision About ApeX Merchandizing

```yaml
type: PureMultipleChoiceExercise
key: 
lang: r
xp: 50
skills: 1
```

To summarize what we found in the ApeX purchasing data, we tried multiple models to help us predict how consumers might want to purchase ApeX's newest fan products, a $10 bumper sticker and a $200 wooden rocket model. The results of these models can be seen in the graph to the right:

We found that the probit model matches the data better than our logit model, and it always gives us a probability between 0 and 100%. The probit model predicts that people are about 10% likely to buy a $10 item online, but 100% likely to buy it online if it costs $200.

All 3 models seem to show a tipping point around $70 where people start to become more likely to buy items online rather than in-person at a pop-up store at the mall. So what would you advise ApeX to do with their in-store segment?

`@hint`

`@sample_data`
```{r}
set.seed(123)
#Dataframe
ID <- 1:17400
payment <- c(rep("store",6000),rep("mobile",7000),rep("web",4400))
payment <- sample(payment, replace = FALSE)
value <- rep(NA,17400)
reward <- rep(NA,17400)
Data <- data.frame(ID,payment,value,reward)
Data$value[Data$payment == "store"] <- abs(round(rnorm(6000,16,50), digits=2))
Data$value[Data$payment == "mobile"] <- abs(round(rnorm(7000,150,40), digits=2))
Data$value[Data$payment == "web"] <- abs(round(rnorm(4400,100,30), digits=2))

# Qualifying purchase for reward program can also influence payment choice
Data$reward[Data$payment == "store"] <- rbinom(6000,1,0.1)
Data$reward[Data$payment == "mobile"] <- rbinom(7000,1,0.5)
Data$reward[Data$payment == "web"] <- rbinom(4400,1,0.2)
Data$value[Data$value<1] <-.99

online <- rep(1,17400)
online[which(Data$payment == "store")] <- 0
Data$online <- online

lpm<-lm(online ~ value, data=Data)
myprobit<-glm(online ~ value, family = binomial(link = "probit"), data = Data)
mylogit<-glm(online ~ value, family = binomial(link = "logit"), data = Data)

value <- Data$value
plot(value,online,xlab = "value of transaction",ylab="probability of buying online")
curve(predict(myprobit,data.frame(value=x),type="resp"),add=TRUE,col="red")
curve(predict(mylogit,data.frame(value=x),type="resp"),add=TRUE,col="blue")
curve(predict(lpm, data.frame(value=x),type="resp"),add=TRUE,col="green")
legend("bottomright",legend = c("Probit","Logit"),col=c("red","blue"),inset = c(0.1,0.1),lwd=1)
```


`@possible_answers`
- The most expensive things have a 100% probability of being purchased, so only sell the most expensive items
- There is a tipping point around $70, so only sell items over $70
- [There is a tipping point around $70, so only sell items under $70]
- It's the monkeys that people like, so only sell monkey-related items

`@sct`
```{r}
msg1= "This is a mis-interpretation of the numbers. They don't show that $200 items have a 100% chance of being purchased, they show that $200 items have a 100% chance of being purchased on the web or mobile stores. Try again."
msg2= "Items over $70 are more likely to be purchased online, so this answer is not playing to the strengths of the pop-up stores. Try again."
msg3= "Correct! There is something about the pop-up stores that lead to purchases of items under $70, so having more of these items in pop-up stores is playing to the expressed preferences of the customers. These data don't tell us exactly why that is, but this is where the data are leading us. We would need another project, likely with customer surveys, to narrow down the exact reasons why we see this behavior."
msg4= "These data don't exactly tell us why people like to buy less expensive items at pop-up stores and more expensive items online, much less that they're doing it for the monkeys. Try again."
ex() %>% check_mc(3, feedback_msgs = c(msg1, msg2, msg3, msg4))
```
  





--- 
## Using Modeling When Experiments Are Impossible
```yaml
type:VideoExercise 
key:4c6f64e320
lang:r
xp:50 
skills:1 

video_link: //player.vimeo.com/video/231747210
```

--- 
## Why Use Models Instead of Experiments?

```yaml
type: PureMultipleChoiceExercise
key: 
lang: r
xp: 50
skills: 1
```

What is the best reason to use a model to find causality instead of a randomized control experiment?

`@hint`

`@possible_answers`
- I already tried an experiment that did not give me the expected result, so I want to try modeling instead.
- My treatment happened in the past, so I can't create a new experiment to test it in the future.
- A control group doesn't make sense with my topic, so I will use modeling instead.
- Creating a control and treatment group would require me to do something immoral and possibly illegal.


`@feedback`
- A well run experiment is almost always more trustworthy than a model of that same causal effect. Maybe the experiment was right and your hypothesis was wrong, that's a big part of science! Try again.
- In some cases, you actually can use experimental techniques on historical data to find causalities. While you can't always do it, there are a lot of great techniques to find causality within past data (check out our other Casual Inference with R courses to find out more). Try again!
- In order to find a causal effect, you need to have a control group and a treatment group, whether it's in an experiment or another method. If you can't create both groups, then whatever you are modeling will not be for causal inference. Try again
- Correct. This is a great reason not to do something, no matter what it is! Like we mentioned in our videos, sometimes you just can't run an experiment if it involves harming others or destroying something valuable, so we need to look to creating really good models instead.

--- 
## Modeling the Impact of Government Stimulus

```yaml
type:VideoExercise 
key:cc7e8a6309
lang:r
xp:50 
skills:1 

video_link: //player.vimeo.com/video/231746794
```

---
## Analyzing the 2009 Stimulus

```yaml
type: PureMultipleChoiceExercise
key: 0a16d28c74
lang: r
xp: 50
skills: 1
```

True or false: The 2009 stimulus worked and helped end the Great Recession.

`@hint`

`@possible_answers`
- We have proved that it did work
- The data shows it had no effect
- [I can't tell either way]

`@feedback`
- It's a good and important question, but unfortunately since we cannot observe the counterfactual outcome, the answer is not clear. Macroeconomists are still working to overcome this very difficult problem! (hint: put on your serious scientist hat and try again).
- It's a good and important question, but unfortunately since we cannot observe the counterfactual outcome, the answer is not clear. Macroeconomists are still working to overcome this very difficult problem! (hint: put on your serious scientist hat and try again)
- It's a good and important question, but unfortunately since we cannot observe the counterfactual outcome, the answer is not clear. Macroeconomists are still working to overcome this very difficult problem!


--- 
## Let's Code: Red Wine - The Secret to Living Longer?
```yaml
type:VideoExercise 
key:
lang:r
xp:50 
skills:1 

video_link: //player.vimeo.com/video/379871850
```


---
## Red Wine: the Secret to Living Longer?

```yaml
type: NormalExercise
key: 326e16239a
lang: r
xp: 100
skills: 1
```

Red wine has resveratrol, a substance that reduces the risk for heart disease. Moderate consumption of red wine is believed to promote longevity. Jenny is very health-conscious and wants to figure out whether red wine is a longevity promoter. She is interested in examining the effect of wine consumption on longevity. She doesn't have the capacity to run a huge medical experiment herself, so she decides to instead download some public data and develop some models to see what she can learn. The data set `Data.wine` contains 4 variables and 60 observations. The data dictionary is below.

Data Dictionary:
   `ID` - subject identifier
   `Wine`- drinking level (light, moderate, and heavy)
   `Age` - age at death
   `Exercise` - hours spent on exercise per week
   
`@instructions`
- 1) Get a sense of the variable names, types, and values in our dataset.
- 2) Create a box plot that compares the amount a person drinks to how long they live.
- 3) Run a regression to see the connection between wine consumption and the average age at death.
- 4) Does the amount you exercise affect this relationship between wine drinking and lifespan?
- 5) Run a regression on wine consumption and lifespan that compensates for exercise level.

`@hint`


`@pre_exercise_code`
```{r}
library(plyr)
library(ggplot2)
set.seed(123)
#Dataframe
Wine <- c(rep("light",30),rep("moderate",20),rep("heavy",10))
Wine <- factor(sample(Wine,replace = FALSE),levels = c("light","moderate","heavy"))
ID <- 1:60
Age <- rep(NA,60)
Exercise <- rep(NA,60)
Data.wine <- data.frame(ID,Wine,Age,Exercise)
#moderate drinkers live longer, heavy drinkers live the least
Data.wine$Age[Data.wine$Wine=="light"] <- round(rnorm(30,78,10),0)
Data.wine$Age[Data.wine$Wine=="moderate"] <- round(rnorm(20,85,6),0)
Data.wine$Age[Data.wine$Wine=="heavy"] <- round(rnorm(10,75,6),0)

#Moderate drinkers also exercise more 
Data.wine$Exercise <- round((Data.wine$Age + 10)/10 + rnorm(60,0,1),0)
Data.wine$Exercise[Data.wine$Exercise<0] <- 0

col <- rep("red",60)
col[Data.wine$Wine=="light"] <- "green"
col[Data.wine$Wine=="moderate"] <- "orange"
col[Data.wine$Wine=="heavy"] <- "yellow"
```




`@sample_code`
```{r}
# Plotting the Age at Death among Different Drinking Levels

# 1) The primary outcome of interest is difference in age at death (`Age`) among different drinking levels (`Wine`).  The first 6 observations is below:

	head(Data.wine)

# 2) Let's create a box plot that plots the primary outcome as a function of drinking level using ggplot. Is there any evidence of a relationship between the two variables? Run the R code below.

	ggplot(Data.wine, aes(x=Wine, y=Age, fill=Wine))+geom_boxplot()

# The mean values of age at death look different, but are they? Let's use linear regression (lm) to find out. 

# 3) Regress `Age` on `Wine` and print the summary statistics. Please provide the R code below.



# Hours of Exercise among Different Drinking Levels

# The results from simple regression show that moderate wine consumption is associated with longer life expectancy. However, can we draw the conclusion that moderate consumption of red wine promotes longevity? Moderate wine consumers may be more health-conscious and have better self-control. The might have other healthy habits (i.e., physical exercise) that contribute to longevity. 

# 4) Let's create a 3 by 3 table that contains averages of `Exercise` by drinking level in the first column and the standard deviations of `Exercise` by drinking level in the second column. Run the R code below. 

  ddply(Data.wine,~Wine, summarise, mean = mean (Exercise), sd = sd(Exercise))

# Interesting. It looks like moderate drinkers also exercise more hours per week than light drinkers or heavy drinkers.

# 5) Now, let's control for hours spent on exercise per week (`Exercise`) in the linear regression. Run a multiple linear regression of `Age` on `Wine` and `Exercise`, and then look at the summary statistics. Please provide the R code below.

	Solution5<-
  summary(Solution5)

```



`@solution`
```{r}
ggplot(Data.wine, aes(x=Wine, y=Age, fill=Wine))+geom_boxplot()
Solution2<-lm(Age ~ Wine, Data.wine)
	summary(Solution2)
ddply(Data.wine,~Wine, summarise, mean = mean (Exercise), sd = sd(Exercise))
Solution5<-lm(Age ~ Wine + Exercise, Data.wine)
	summary(Solution5)
```

`@sct`
```{r}
ex() %>% check_error()
success_msg("Good work! The base group (light drinkers) is represented by the intercept. We saw that light drinkers have an average life span of about 79 years. In addition, as we saw in the table we generated, moderate consumers spend the most time on exercise. And when we ran our model, the regression coefficient of the effect of red wine and exercise on moderate drinkers is 3.2010, indicating the expected life of moderate drinkers is 3.2010 years longer than that of light drinkers. The p-value of this coefficient is just above .05, suggesting the difference in expected life between those two groups is almost significant at 5% significance level, but not quite.  This implies that wine consumption cannot explain the age differences between moderate drinkers and light drinkers. However, the coefficient on `Exercise` is significantly positive at 1% significance level. Thus, longevity is driven mostly by physical activity instead of wine consumption in this case.")
```



---
## Does This Model Hold Up Under Pressure?

```yaml
type: NormalExercise
key: 326e16239a
lang: r
xp: 100
skills: 1
```

We've seen that people who drink moderate amounts of red wine also tend to exercise more than others, and while these moderate drinkers do live longer than light and heavy wine drinkers, that seems to be due to their level of exercise, not their wine drinking. But when we look closer at wine drinkers, can we really argue that our model accounts for all possible variables? Does a wine with half the resveratrol have half the treament effect? Is the effect the same for both men and women? Let's see how this model holds up when we add two new sets of information:

The new dataframe `Survey.Data` has information about red wines, white wines (which have nearly none of the chemical resveratrol), and rose wines (which have about half as much resveratrol as red wine). Is it really the resveratrol making the difference? If so, then we should see that rose wines, with 1/2 of the resveratrol as red wines, should have 1/2 the treatment effect of red wines.

To model this, we will use new data from a large national health survey that includes over 6000 individuals who admit to having least one drink per week and who have died since they began the survey. The alcoholic drinks included in this survey could be wine, beer, or hard liquor, and the dataframe counts how many glasses of each alcoholic beverage the individuals drink per week, and the amount of resveratrol that is in each glass (based on the brand and type consumed). We also have data on their level of physical activity, age at death, and gender.


Data Dictionary for the dataframe `Survey.Data`:
  
  `ID` - subject identifier
  `Wine`- drinking level (light, moderate, and heavy)
  `Age` - age at death
  `Exercise` - hours spent on exercise per week
  `Female` - has value of 1 if participant is female
  
  `DrinkerLevel` - descriptive text of average drinks per week
  `light.drinker.count` - number of subjects who drank less than 5 drinks per week on average
  `moderate.drinker.count` - number of subjects who drank between 5-12 drinks per week on average
  `heavy.drinker.count` - number of subjects who drank 13+ drinks per week on average
    
  `count` - average number of alcoholic drinks per week for each individual 
  `wine.count` - average number of glasses of wine of all types per week
  `wine.count.red` - average number of glasses of red wine per week
  `wine.count.rose` - average number of glasses of rose wine per week
  `wine.count.white` - average number of glasses of white wine per week
  `beer.count` - average number of glasses of beer per week
  `liquor.count` - average number of glasses of hard alcohol (whisky, gin, vodka, etc) per week 

  `res.red.wine` - average milligrams of reseveratrol per glass of red wine
  `res.white.wine` - average milligrams of reseveratrol per glass of white wine
  `res.rose.wine` - average milligrams of reseveratrol per glass of rose wine
  `res.beer` - average milligrams of reseveratrol per glass of beer
  `res.liquor` - average milligrams of resveratrol per glass of liquor
  
  `total.res.red.wine` - total average resveratrol consumed via red wine per week
  `total.res.white.wine` - total average resveratrol consumed via white wine per week
  `total.res.rose.wine` - total average reseveratrol consumed via rose wine per week
  `total.res.beer` - total average reseveratrol consumed via beer per week
  `total.res.liquor` - total average resveratrol consumed via liquor per week
  `total.res` - the total average mg of resveratrol from all drinks per week 
  
  
`@instructions`
- 1) Explore the dataset on your own.
- 2) Look at the means of our key variables of interest.
- 3) Run a plot of the amount of exercise our participants got per week.
- 4) Run an initial regression model of red wine consumption and exercise on lifespan in this new dataset.
- 5) See what happens when we add the additional drink types in this dataset to our model.
- 6) See what happens when we add gender as a variable to our model.
- 7) Write out the estimated Average Treatment Effect produced by this model.


`@hint`


`@pre_exercise_code`
```{r}
library(plyr)
set.seed(123)

#Survey.Data version

# generating distribution of drinks of any type per week 
# light is 0-4, moderate is 5-12, heavy is 13+

count<-rbeta(6135,1.12,11)
count<-round((count*75),0)
ID <- c(1:6135)
Age <- rep(NA,6135)
activity<-rbeta(6135,3.5,11)
activity<-activity*400
Survey.Data<-data.frame(ID,Age,count,activity)
Survey.Data$female<-rbinom(6135,1,.55)


Survey.Data$DrinkerLevel[Survey.Data$count>=0 & Survey.Data$count<=4]<-"light"
Survey.Data$DrinkerLevel[Survey.Data$count>=5 & Survey.Data$count<=12]<-"moderate"
Survey.Data$DrinkerLevel[Survey.Data$count>=13]<-"heavy"

Survey.Data$activity[Survey.Data$DrinkerLevel=="light"]<-Survey.Data$activity[Survey.Data$DrinkerLevel=="light"]*.90
Survey.Data$activity[Survey.Data$DrinkerLevel=="heavy"]<-Survey.Data$activity[Survey.Data$DrinkerLevel=="heavy"]*.45


light.drinker.count=sum(Survey.Data$DrinkerLevel=="light")+0
moderate.drinker.count=sum(Survey.Data$DrinkerLevel=="moderate")+0
heavy.drinker.count=sum(Survey.Data$DrinkerLevel=="heavy")+0

Survey.Data$wine.count<-Survey.Data$count*0.3333333
Survey.Data$wine.count.red<-round(Survey.Data$wine.count*.42,2)
Survey.Data$wine.count.rose<-round(Survey.Data$wine.count*.17,2)
Survey.Data$wine.count.white<-round(Survey.Data$wine.count*.41,2)

Survey.Data$beer.count<-round(Survey.Data$count*0.3548387,2)
Survey.Data$liquor.count<-round(Survey.Data$count*0.311828,2)

Survey.Data$res.red.wine<-sample(rnorm(Survey.Data$wine.count.red,.27,.06))
Survey.Data$res.rose.wine<-sample(rnorm(Survey.Data$wine.count.rose,.12,.03))
Survey.Data$res.white.wine<-sample(rnorm(Survey.Data$wine.count.white,.04,.01))

Survey.Data$total.res.red.wine<-(Survey.Data$wine.count.red*Survey.Data$res.red.wine)
Survey.Data$total.res.white.wine<-(Survey.Data$wine.count.white*Survey.Data$res.white.wine)
Survey.Data$total.res.rose.wine<-(Survey.Data$wine.count.rose*Survey.Data$res.rose.wine)
Survey.Data$total.res<-((Survey.Data$total.res.red.wine) + (Survey.Data$total.res.white.wine) + (Survey.Data$total.res.rose.wine))

Survey.Data$res.beer<-0
Survey.Data$res.liquor<-0
Survey.Data$total.beer.res<-0
Survey.Data$total.liquor.res<-0

Survey.Data$Age <- round(sample(rnorm(6135,78,10)))

Survey.Data$Age<-(Survey.Data$Age*((Survey.Data$res.red.wine+Survey.Data$res.rose.wine)/10))+Survey.Data$Age-Survey.Data$res.white.wine*5

```

`@sample_code`
```{r}
# So we've seen one dataset that shows (if we can trust our data) that a moderate amount of red wine drinking, combined with exercise, will make you live longer on average than people who don't do those things. But does this finding hold up if we test it against new, more in-depth data?

# Luckily for us, rosé wines are wines that are halfway between red and white wines. They are pink in color, and tend to have about half of the resveratrol as red wines. And at the far end, white wines have almost no resveratrol at all. So let's test our model against data that not only has red wine, but also includes rosé wine, white wine, other wine (such as champagne), beer, and liquor, as well as some basic male/female gender data.

#1) First, on your own explore this new dataset of over 6000 individuals with the str(), head(), and/or summary() commands:




# Good job. It looks like there is data on the number of individuals, the average number drinks they had per week, how much exercise they get per week, what kinds of drinks they have on average per week, whether they were male or female, and how old they were when they died during the survey.


#2) Now, let's find out the average amount of the chemical resveratrol contained in each type of alcoholic drink - red wine, rosé wine, white wine, other wine (like champagne), beer, and liquor. Use the following line of code as a template to do these calculations for each type of drink and run them:

  mean.res.red.wine<-mean(Survey.Data$res.redwine)
  mean.res.rose.wine<-
  mean.res.white.wine<-
  mean.res.beer<-
  mean.res.liquor<-

# Good. It looks the red wines tested do indeed have about twice the resveratrol as rosé, and the white wines had almost no resveratrol at all. So looking at the treatment effects of these wines could prove interesting. And we also see that beer and liquor contain no resveratrol at all.


#3) Now let's plot the average number of minutes of moderate to strenuous exercise in a week for the individuals in this study. Are they workout addicts, or lazy couch potatoes? Fill in the correct variables for "x" and "y" in the code below:

   ggplot(Survey.Data, aes(x=DrinkerLevel, y=activity, fill=DrinkerLevel))+geom_boxplot()


# Nice job.

#4) Now let's run a regression model like we did in the last exercise. Let's test our final model to see if it predicts a different treatment effect than in the previous question. Remember, that model and that data said that red wine caused a 3.2 year increase in life expectancy, and exercise caused a 2.9 increase in life expectancy, but only the result on exercise was signficant. What will we see in this data and model? Regress the variables `total.res.red.wine` and `activity` on `Age`:

  lm.redwine.and.exercise<-lm()
  summary()

#5) So that model only included red wine, since it has the most resveratrol of all wines (which we also see in our new data). What changes when we add other kinds of drinks with lower levels resveratrol to the model? Do they show a smaller treatment effect than red wine? Let's find out!  Add in `total.res.white.wine` and `total.res.rose.wine` to our model:

  lm.allwines.and.exercise<-
  summary()

# Good. We do see some different coefficients with the resveratrol levels in different types of wine, including a negative coefficient with white wine, which implies it takes many years off of your life! However, only red wine has a statistically significant coefficient in this model.


#6) Now let's use the variable that captures the average total amount of resveratrol each respondent drank across all wine types, which is stored in the variable `total.res` , and let's also add the gender component (the variable `female`) that we now have in this data. Women tend to drink slightly more wine than men do in the U.S., so does including gender in our model affect its predictions?

  lm.totalres.and.exercise.and.gender<-
  summary()

#7) Interesting. Being female does have a small negative coefficient, but it has a large standard error and a p-value of 0.3, making it not statistically significant.

# So, based on our data and our model, what is the causal treatment effect of drinking red wine on how long you live? Be precise and don't round!  

average.treatment.effect<-

```

`@solution`
```{r}
mean.res.red.wine<-mean(Survey.Data$res.red.wine)
mean.res.rose.wine<-mean(Survey.Data$res.rose.wine)
mean.res.white.wine<-mean(Survey.Data$res.white.wine)
mean.res.beer<-mean(Survey.Data$res.beer)
mean.res.liquor<-mean(Survey.Data$res.liquor)

lm.redwine.and.exercise<-lm(Age~total.res.red.wine+activity, Survey.Data)
summary(lm.redwine.and.exercise)
  lm.allwines.and.exercise<-lm(Age~total.res.red.wine+total.res.white.wine+total.res.rose.wine+activity, Survey.Data)
  summary(lm.allwines.and.exercise)
lm.totalres.and.gender<-lm(Age~total.res+female+activity, Survey.Data)
 summary(lm.totalres.and.gender)

average.treatment.effect<-7.520962
```

`@sct`
```{r}
ex() %>% check_error()
success_msg("")
```

--- 
## Do We Have Problems with a Confounder?

```yaml
type: PureMultipleChoiceExercise
key: 4dfa681543
lang: r
xp: 50
skills: 1
```


The results of the previous exercise were not as clear as we were hoping: instead of seeing red wine with a positive treatment effect, rose wine with a smaller positive treatment effect, and white wine with no effect, we only saw a single positive effect for red wine. But this was with a more complex dataset than we had for our very first question about the impact of resveratrol on life expectancy. Perhaps we have a problem with a confounding variable that is affecting our model. Which of the following variables do you think might be confounding the impact of resveratrol on life expectancy?

`@hint`

`@possible_answers`
- [count (the average number of drinks per week)]
- female (what gender the participants are)
- activity (average minutes of exercise per week)
- Age (the lifespan of the participants)

`@feedback`
-  Correct! Imagine that one of our subjects, Suzy, has 1 drink/week with .30 mg total resveratrol in it, but another subject, Johnny, drinks 30+ glasses of alcohol to get the same amount of resveratrol. We should probably think that Johnny's extra 29 alcoholic drinks per week are affecting his overall health in a way that may confound our treatment effect. So let's try working on that issue to see if it changes our analysis.
-  Gender can often be a factor to look at, but if you look at our sample you'll see we have roughly a 50/50 split between men and women, so that is probably not the first place to look for issues. Try again.
-  Activity may be important, but there is another variable that can impact the amount of resveratrol that our participants may be ingesting. Try again.
-  This is our outcome variable, and it's unlikely that people's lifespan has a complicated reverse-causal effect on resveratrol's effect on lifespan, so try again.


---
## Finishing Up with A Final Model

```yaml
type: NormalExercise
key: 326e16239a
lang: r
xp: 100
skills: 1
```


Data Dictionary for the dataframe `Survey.Data`:
  
  `ID` - subject identifier
  `Wine`- drinking level (light, moderate, and heavy)
  `Age` - age at death
  `Exercise` - hours spent on exercise per week
  `Female` - has value of 1 if participant is female
  
  `DrinkerLevel` - descriptive text of average drinks per week
  `light.drinker.count` - number of subjects who drank less than 5 drinks per week on average
  `moderate.drinker.count` - number of subjects who drank between 5-12 drinks per week on average
  `heavy.drinker.count` - number of subjects who drank 13+ drinks per week on average
    
  `count` - average number of alcoholic drinks per week for each individual 
  `wine.count` - average number of glasses of wine of all types per week
  `wine.count.red` - average number of glasses of red wine per week
  `wine.count.rose` - average number of glasses of rose wine per week
  `wine.count.white` - average number of glasses of white wine per week
  `beer.count` - average number of glasses of beer per week
  `liquor.count` - average number of glasses of hard alcohol (whisky, gin, vodka, etc) per week 

  `res.red.wine` - average milligrams of reseveratrol per glass of red wine 
  `res.white.wine` - average milligrams of reseveratrol per glass of white wine 
  `res.rose.wine` - average milligrams of reseveratrol per glass of rose wine 
  `res.beer` - average milligrams of reseveratrol per glass of beer 
  `res.liquor` - average milligrams of resveratrol per glass of liquor 
  
  `total.res.red.wine` - total average resveratrol consumed via red wine per week
  `total.res.white.wine` - total average resveratrol consumed via white wine per week
  `total.res.rose.wine` - total average reseveratrol consumed via rose wine per week
  `total.res.beer` - total average reseveratrol consumed via beer per week
  `total.res.liquor` - total average resveratrol consumed via liquor per week
  `total.res` - the total average mg of resveratrol from all drinks per week 
  
  `total.res` - the total average milligrams of resveratrol from all drinks per week 

`@instructions`
- 1) Re-examine the basic statistics on the amount of drinks our participants are having per week.
- 2) Subset our data to exclude outliers.
- 3) Run our model again on this subsetted data.
- 4) Decide if the average number of drinks per week is a confounding variable.
- 5) Write out our final model.
- 6) Write out the estimated Average Treatment Effect of drinkin red wine on how long someone lives
  
`@hint`


`@pre_exercise_code`
```{r}
library(plyr)
set.seed(123)

#Survey.Data version

# generating distribution of drinks of any type per week 
# light is 0-4, moderate is 5-12, heavy is 13+

count<-rbeta(6135,1.12,11)
count<-round((count*75),0)
ID <- c(1:6135)
Age <- rep(NA,6135)
activity<-rbeta(6135,3.5,11)
activity<-activity*400
Survey.Data<-data.frame(ID,Age,count,activity)
Survey.Data$female<-rbinom(6135,1,.55)

Survey.Data$DrinkerLevel[Survey.Data$count>=0 & Survey.Data$count<=4]<-"light"
Survey.Data$DrinkerLevel[Survey.Data$count>=5 & Survey.Data$count<=12]<-"moderate"
Survey.Data$DrinkerLevel[Survey.Data$count>=13]<-"heavy"

Survey.Data$activity[Survey.Data$DrinkerLevel=="light"]<-Survey.Data$activity[Survey.Data$DrinkerLevel=="light"]*.90
Survey.Data$activity[Survey.Data$DrinkerLevel=="heavy"]<-Survey.Data$activity[Survey.Data$DrinkerLevel=="heavy"]*.45


light.drinker.count=sum(Survey.Data$DrinkerLevel=="light")+0
moderate.drinker.count=sum(Survey.Data$DrinkerLevel=="moderate")+0
heavy.drinker.count=sum(Survey.Data$DrinkerLevel=="heavy")+0

Survey.Data$wine.count<-Survey.Data$count*0.3333333
Survey.Data$wine.count.red<-round(Survey.Data$wine.count*.42,2)
Survey.Data$wine.count.rose<-round(Survey.Data$wine.count*.17,2)
Survey.Data$wine.count.white<-round(Survey.Data$wine.count*.41,2)

Survey.Data$beer.count<-round(Survey.Data$count*0.3548387,2)
Survey.Data$liquor.count<-round(Survey.Data$count*0.311828,2)

Survey.Data$res.red.wine<-sample(rnorm(Survey.Data$wine.count.red,.27,.06))
Survey.Data$res.rose.wine<-sample(rnorm(Survey.Data$wine.count.rose,.12,.03))
Survey.Data$res.white.wine<-sample(rnorm(Survey.Data$wine.count.white,.04,.01))

Survey.Data$total.res.red.wine<-(Survey.Data$wine.count.red*Survey.Data$res.red.wine)
Survey.Data$total.res.white.wine<-(Survey.Data$wine.count.white*Survey.Data$res.white.wine)
Survey.Data$total.res.rose.wine<-(Survey.Data$wine.count.rose*Survey.Data$res.rose.wine)
Survey.Data$total.res<-((Survey.Data$total.res.red.wine) + (Survey.Data$total.res.white.wine) + (Survey.Data$total.res.rose.wine))

Survey.Data$total.res<-((Survey.Data$res.red.wine) + (Survey.Data$res.white.wine) + (Survey.Data$res.rose.wine))
Survey.Data$res.beer<-0
Survey.Data$res.liquor<-0

Survey.Data$Age <- round(sample(rnorm(6135,78,10)))

Survey.Data$Age<-(Survey.Data$Age*((Survey.Data$res.red.wine+Survey.Data$res.rose.wine)/10))+Survey.Data$Age-Survey.Data$res.white.wine*5

mean.res.red.wine<-mean(Survey.Data$res.red.wine)
mean.res.rose.wine<-mean(Survey.Data$res.rose.wine)
mean.res.white.wine<-mean(Survey.Data$res.white.wine)
mean.res.beer<-mean(Survey.Data$res.beer)
mean.res.liquor<-mean(Survey.Data$res.liquor)

```
   
`@sample_code`
```{r}

# 1) Since we think that the number of alcoholic drinks consumed might be confounding the effect of resveratrol on lifespan, let's subset our sample to exclude the highest drinkers. But where should we make the cutoff? Let's revisit the summary statistics on the variable `count` in the datframe `Survey.Data` to see what our mean, median, and standard deviations are:




# 2) You should see that our median number of drinks is 5, and the 3rd quartile (or 3 standard deviations from the mean) is 10. There are lots of ways to subset our sample based on `count`, but using the 3rd quartile seems like a good choice here. It means that we will keep 75% of our original sample, and will exclude the heaviest 25% of drinkers. So let's subset our dataframe `Survey.Data` into a new dataframe called `Drink.Study` based on that 3rd quartile cutoff value of 10. Fill in the correct dataframe name, variable name, and value below to create the new subsetted dataframe:

  Drink.Study<-Survey.Data[which(DATAFRAME$VARIABLE<=X),]
  
  
# 3) Now let's try running our key regression again to see if our coefficients have changed, and if any have now become statistically significant after removing the heaviest drinkers from our sample:

  subset.model<-lm()
  summary()
  

# 4) That's interesting. It seems that our coefficients have gone down a bit, and our statistical significance has increased on our coefficient for the resveratrol in red wine, but we didn't find any newly statistically significant coefficients. 

# Does this mean that the variable `count` is a big confounder for our subsetted data? Answer with "yes" or "no":

  count.is.a.confounder.for.subset<-""
  
  
# 5) The increased significance of this subsetted sample means we can have more confidence in this model than in our initial model on this dataset. Now let's write out the revised model based on the coefficients of our statistically significant variables for the impact of drinking on how long you live: the first value is our base average lifespan and the second is our coefficient for res.redwine. Note that this is not a line of R code, but is still a representation of our model:

  lifespan = XXXXXXX + YYYYYYY*glasses of red wine


# 6) And based on this model, what is the average treatment effect of drinking red wine on lifespan for an average drinker in our sample? Be precise and don't round!


  ATE<-


```

`@solution`
```{r}
  Drink.Study<-Survey.Data[which(Survey.Data$count<=10),]
subset.model<-lm(Age~total.res, Drink.Study)
  summary(subset.model)
count.is.a.confounder.for.subset<-"no"
ATE<-
```

`@sct`
```{r}
ex() %>% check_error()
success_msg("Great job!")
```

