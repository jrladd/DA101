% Predictive Analytics: Multiple Regression
% DA 101, Dr. Ladd
% Week 11

# Multiple or *Multivariate* Regression

## Multiple Regression lets you add more independent variables.

Bivariate regression (the normal kind):

$Y=b_{0}+b_{1}x$

Multivariate regression:

$Y=b_{0}+b_{1}x_{1}+b_{2}x_{2}+b_{3}x_{3}+...$

## You can add more variables to the `fit()` function.

Let's use the `mtcars` dataset, which has more variables than `mpg`.

```r
carmodel <- linear_reg() %>%
      set_engine("lm") %>%
      fit(mpg~disp+hp+drat, data=mtcars)

#Let's talk about the results together:
summary(carmodel$fit)
```

## Once you have a model, you can predict new values!

```r
newvals <- tibble(disp=400,hp=145,drat=4.2)

predict(carmodel,newvals)
```

# How to Choose Predictor Variables

## There's no magic solution! You can try different options, but use your logic and don't just throw everything in there.

## Occam's Razor says that the simplest model is probably the best one.

![Think carefully about how many variables you add.](img/William_of_Ockham.png)

## As you add variables, $R^{2}$ will increase.

But think about *how much* it's increasing.

And use Adjusted $R^{2}$ for multivariate models. It accounts for adding more variables. 

## Avoid Multicollinearity: when two predictor variables correlate.

This will confuse the model and mess up your results! It could even result in *false* predictions.

## How do we find multicollinearity?

You can do a *pairwise* comparison of the variables you're thinking about. 

```r
library(GGally)

ggpairs(dataset, columns=c("var1","var2","var3"))
```

This will give you scatterplots and correlation coefficients to compare.

## You can consider categorical variables as predictors, too.

But in the coefficients, the first category will always be left out as the baseline.

All the remaining slopes are relative to that baseline!

Let's create an example using the `mpg` dataset.

## Challenge: Seattle Housing Data

Try to make an effective multivariate linear model to predict housing prices in Seattle.

Take a look at the dataset and logically choose some predictors. Check for multicollinearity before you run your model! When you're done, try to predict housing price based on some new data points you create.

Download [house_sales.tsv](../data/house_sales.tsv). You'll need to open this with `housing <- read_tsv("house_sales.tsv")`.

# Regression Diagnostics
