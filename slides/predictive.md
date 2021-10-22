% Predictive Analytics: Regression
% DA 101, Dr. Ladd
% Week 9

# Let's start by building on our hypothesis tests.

## How do we test whether the means of two groups are the same?

The two-sample t-test: (This one is review!)

```r
# First filter some data
mpg_filtered <- filter(mpg, class=="minivan"|class=="pickup")

# Then run the test
t.test(hwy~class,mpg_filtered)
```

## How do we test the mean of a single group?

The one-sample t-test:

```r
# Run a t-test with just one variable or group
minivans <- filter(mpg, class=="minivan")

# Then run the test
t.test(minivans$hwy)
```

## How do we know if a variable is normally distributed?

The Shapiro-Wilk test:

```r
shapiro.test(mpg$hwy)
```

**Important note**: the variable likely has a normal distribution if the p-value is *higher* than .05. Always compare with a histogram!

## Can we make our own normally-distributed variable?

Let's try out `rnorm()`. It takes 3 parameters: the number of observations, the mean, and the standard deviation.

```r
# A normally-distributed variable of 100 values, with mean of 5 and sd of 2
v1 <- rnorm(100, mean=5, sd=2)

# Let's look at this one:
ggplot(,aes(v1)) +
  geom_histogram()

# And we can test to make sure it's normally distributed:
shapiro.test(v1)
```

How would you make a variable with 200 values and a mean of 23?

## Understanding Correlation

## Let's think about how we look at the relationship of two variables.

## Remember the Pearson correlation coefficient?

```r
cor(mpg$displ,mpg$cty)
```

This tells us the strength of the correlation, but is this correlation *statistically significant*?

## There's a test for this, too!

The correlation test:

```r
cor.test(mpg$displ,mpg$cty)
```

Now we know the variables are correlated, and we know that this correlation is statistically significant. But we can learn more about the *nature* of the relationship...

# Understanding relationships with Linear Regression
