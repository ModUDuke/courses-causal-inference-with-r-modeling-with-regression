---
title: 'Modeling for Causal Inference with Regression'
description: 'This brief course will introduce you to modeling for causal inference, with practice using different kinds of regression models'
free_preview: true
---

## The Basics of Modeling Behavior
```yaml
type: VideoExercise 
key: 812b575a73
lang: r
xp: 50 
skills: 1 
video_link: //player.vimeo.com/video/231746347
```

---
## Discrete Choice Analysis
```yaml
type: VideoExercise 
key: 09bccc78e5
lang: r
xp: 50 
skills: 1 
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
type: VideoExercise
key: 601a2a817d
lang: r
xp: 50
skills: 1
video_link: "//player.vimeo.com/video/379871879"
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
# Think back to how often you eat ice cream, how much your friends eat ice cream, how much ice cream you've eaten as a kid growing up, and how often you see people eating ice cream around town, or people picking up some ice cream at the store. People might get ice cream for lots of reasons, from celebrating birthdays to cooling down on a hot summer's day. Or if you are a little kid, because you begged your parents for it!
  
# So we don't know yet how to predict what makes people eat ice cream, but we can start by imagining an initial model, and then we can try to find some data to help us get a more analytical sense of what drives eating lots of ice cream.
  
# 1a) First off, let's think about how much ice cream you personally eat in a single month, on average. Remember, you might expect to eat more during the hot months of summer than during the winter (or vice versa!), but start by taking a guess at how much you eat in an average month during the year. Let's measure it in pints (about 500ml). How many pints of ice cream do you think you eat in a month? 
  
  
  
# 1b) And now, in the space below, multiply that by 12 to see how much ice cream that would be in a year.
  
  
  
# 2a) Okay. Now let's think about other adults, and how much you think they might eat on average per month. How much ice cream do you think the average adult person eats, measured in pints (about 500ml) per month?
  
  
  
# 2b) And now, in the space below, multiply that by 12 to see how much ice cream an average adult would eat in a year.
  
  
  
  
# 3a) Kids love ice cream, as we all know, and you may think that kids eat more ice cream than older people do (on average). How much ice cream do you think the average child eats per month, measured in pints per year?
  
  
  
# 3b) And now, in the space below, multiply that by 12 to see how much ice cream an average kid would eat in a year.
  
  
  
  
# 4a) So let's use these numbers to do a simple equation to calculate how much ice cream a family of 4 would eat in an entire year (assuming this family has 2 adults and 2 children). Just plug your predicted numbers from above into this equation to provide our first model:
  
    total.ice.cream.per.family = 2*(your adult consumption per year) + 2* (your child consumption per year)
  
# 4b) And now let's find out the answer by actually running that equation in R. What number do you get?
  


  
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
key: 4d2f015161
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
key: 97284a3dbe
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
  
        model<-###.#### +#.####*children -#.####*age
  
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
  
