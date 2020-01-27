---
title: 'A Detour Into Prediction Models'
description: 'Predictions about the future are not causal inference, but they are a big part of data science. We''ll practice one particular example in this chapter.' 
--- 


## Let's Code: Making Money for Space Travel
```yaml
type: VideoExercise 
key:
lang: r
xp: 50 
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
  
Thus, the predicted values are bounded between 0 and 1. Let's see what a probit model can do for predicting our data.
  
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
- The dataframe is called `Data`
  
`@sample_code`
```{r}
# 1) Run each of our 3 models one more time so we can look at the summary statistics, including the AIC values for the logit and probit models. In each of the following, fill in the R code below, where X is the dependent variable, Y is the independent variable, and Z is the name of the dataframe
  
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
  
```
 
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
  
  
  
---
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
  
  
---
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
    
  
