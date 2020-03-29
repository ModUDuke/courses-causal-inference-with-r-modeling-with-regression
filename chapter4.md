---
title: 'Why Are Models So Common?'
description: 'If you want to find out the causes for something, the best option is probably an experiment. But that''s not always possible, and this chapter explores some reasons why. Then we wrap up this short course with a complex problem.'
--- 

## Using Modeling When Experiments Are Impossible
```yaml
type: VideoExercise 
key: 6a0ad3ba11
lang: r
xp: 50 
skills: 1 
  
video_link: //player.vimeo.com/video/231747210
```
  
--- 
## Why Use Models Instead of Experiments?
  
```yaml
type: PureMultipleChoiceExercise
key: 6a0ad3ba12
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
- [Creating a control and treatment group would require me to do something immoral and possibly illegal.]
  
  
`@feedback`
- A well run experiment is almost always more trustworthy than a model of that same causal effect. Maybe the experiment was right and your hypothesis was wrong, that's a big part of science! Try again.
- In some cases, you actually can use experimental techniques on historical data to find causalities. While you can't always do it, there are a lot of great techniques to find causality within past data (check out our other Casual Inference with R courses to find out more). Try again!
- In order to find a causal effect, you need to have a control group and a treatment group, whether it's in an experiment or another method. If you can't create both groups, then whatever you are modeling will not be for causal inference. Try again
- Correct. This is a great reason not to do something, no matter what it is! Like we mentioned in our videos, sometimes you just can't run an experiment if it involves harming others or destroying something valuable, so we need to look to creating really good models instead.
  
--- 
## Modeling the Impact of Government Stimulus
  
```yaml
type: VideoExercise 
key: 6a0ad3ba13
lang: r
xp: 50 
skills: 1 
  
video_link: //player.vimeo.com/video/231746794
```
  
---
## Analyzing the 2009 Stimulus
  
```yaml
type: PureMultipleChoiceExercise
key: 6a0ad3ba14
lang: r
xp: 50
skills: 1
```
  
True or false: The 2009 government stimulus worked and helped end the Great Recession.
  
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
type: VideoExercise 
key: 6a0ad3ba15
lang: r
xp: 50 
skills: 1 
  
video_link: //player.vimeo.com/video/379871850
```
  
  
---
## Red Wine: the Secret to Living Longer?
  
```yaml
type: NormalExercise
key: 6a0ad3ba16
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
key: 6a0ad3ba17
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
  
# 1) First, on your own explore this new dataset of over 6000 individuals with the str(), head(), and/or summary() commands:
  
  
  
  
# Good job. It looks like there is data on the number of individuals, the average number drinks they had per week, how much exercise they get per week, what kinds of drinks they have on average per week, whether they were male or female, and how old they were when they died during the survey.
  
  
# 2) Now, let's find out the average amount of the chemical resveratrol contained in each type of alcoholic drink - red wine, rosé wine, white wine, other wine (like champagne), beer, and liquor. Use the following line of code as a template to do these calculations for each type of drink and run them:
  
    mean.res.red.wine<-mean(Survey.Data$res.redwine)
    mean.res.rose.wine<-
    mean.res.white.wine<-
    mean.res.beer<-
    mean.res.liquor<-
  
# Good. It looks the red wines tested do indeed have about twice the resveratrol as rosé, and the white wines had almost no resveratrol at all. So looking at the treatment effects of these wines could prove interesting. And we also see that beer and liquor contain no resveratrol at all.
  
  
# 3) Now let's plot the average number of minutes of moderate to strenuous exercise in a week for the individuals in this study. Are they workout addicts, or lazy couch potatoes? Fill in the correct variables for "x" and "y" in the code below:
  
     ggplot(Survey.Data, aes(x=DrinkerLevel, y=activity, fill=DrinkerLevel))+geom_boxplot()
  
  
# Nice job.
  
# 4) Now let's run a regression model like we did in the last exercise. Let's test our final model to see if it predicts a different treatment effect than in the previous question. Remember, that model and that data said that red wine caused a 3.2 year increase in life expectancy, and exercise caused a 2.9 increase in life expectancy, but only the result on exercise was signficant. What will we see in this data and model? Regress the variables `total.res.red.wine` and `activity` on `Age`:
  
    lm.redwine.and.exercise<-lm()
    summary()
  
# 5) So that model only included red wine, since it has the most resveratrol of all wines (which we also see in our new data). What changes when we add other kinds of drinks with lower levels resveratrol to the model? Do they show a smaller treatment effect than red wine? Let's find out!  Add in `total.res.white.wine` and `total.res.rose.wine` to our model:
  
    lm.allwines.and.exercise<-
    summary()
  
# Good. We do see some different coefficients with the resveratrol levels in different types of wine, including a negative coefficient with white wine, which implies it takes many years off of your life! However, only red wine has a statistically significant coefficient in this model.
  
  
# 6) Now let's use the variable that captures the average total amount of resveratrol each respondent drank across all wine types, which is stored in the variable `total.res` , and let's also add the gender component (the variable `female`) that we now have in this data. Women tend to drink slightly more wine than men do in the U.S., so does including gender in our model affect its predictions?
  
    lm.totalres.and.exercise.and.gender<-
    summary()
  
# 7) Interesting. Being female does have a small negative coefficient, but it has a large standard error and a p-value of 0.3, making it not statistically significant.
  
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
success_msg("Nice work! This dataset has a lot more variables and participants than our first dataset, but at least some of the results seem to be holding up. The chemical resveratrol, common in red wines, does seem to show a positive impact on life expectancy. But we're not quite done. We do have some potential confounders to consider that might also be effecting life expectancy in these survey subjects, so let's look into that next.")
```
  
--- 
## Do We Have Problems with a Confounder?
  
```yaml
type: PureMultipleChoiceExercise
key: 6a0ad3ba18
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
key: 6a0ad3ba19
lang: r
xp: 100
skills: 1
```
  
We finish up with a final model based on all that we have discovered so far. Does this second, larger study support the theory that regular drinking of red wine, which has the chemical resveratrol in higher quantities than other drinks, will make you live a longer life? Let's find out!


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
    
  
# That's interesting. It seems that our coefficients have gone down a bit, and our statistical significance has increased on our coefficient for the resveratrol in red wine, but we didn't find any newly statistically significant coefficients. 
  
# 4) Does this mean that the variable `count` is a big confounder for our subsetted data? Answer with "yes" or "no":
  
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
success_msg("Great job! It really does look like our average treatment effect of resveratrol on life expectancy is positive and statistically significant, even when accounting for heavy wine drinkers, which would likely be our biggest potential confounder. Our model works!")
```

