% Predictive Analytics: Multiple Regression
% DA 101, Dr. Ladd
% Week 11

# Multiple Regression

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

## Occam's Razor

## Multicollinearity

# Regression Diagnostics
