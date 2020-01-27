---
title: 'Confounders in Modeling'
description: 'In this chapter we'll look at the problems of confounders when using models for causal inference.'
--- 

## Confounders in Discrete Choice Analysis
```yaml
type: VideoExercise 
key: 059e8eb292
lang: r
xp: 50 
skills: 1 
  
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
  
Someone doing a Big Data analysis tells you the following. "I included over 1,000 variables in my analysis. Since I have so many control variables, so I do not have to worry about confounders." Do you agree?
  
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
type: VideoExercise 
key: 4608217f1d
lang: r
xp: 50 
skills: 1 
  
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
type: VideoExercise 
key: 0dd082cdd9
lang: r
xp: 50 
skills: 1 
  
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
## Let's Code: Income Inequality at FutureChew
```yaml
type: VideoExercise 
key:
lang: r
xp: 50 
skills: 1 
  
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
      
  
# 4) Because this variable is both statistically significant and different from the other variables, can we say that it's the single cause behind the wage imbalance between women and men at FutureChew? Answer "yes" or "no"
  
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
  
    Log of your salary at FutureChew =  intercept +#####*years of experience -###### (if female) 
  
    
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

