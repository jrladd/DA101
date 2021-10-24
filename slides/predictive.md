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

## How do we test the mean of one variable?

The one-sample t-test:

```r
# Run the test to see if the mean of hwy
# is greater than 0.
t.test(mpg$hwy, mu=0, alternative="greater")
```

We can set the default mean (`mu`) to *any value*. Remember that the variable **must** be normally distributed.

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

# You Try It!

## Set Up

Install and load the `palmerpenguins` dataset. Then create a filtered dataset of only the Adelie penguins.

Make sure you've got `tidyverse` imported, too.

Ask yourself: what test or function would you run? How would you run it?

## Challenges

1. Are the flipper lengths of Adelie penguins normally distributed?

2. Are the flipper lengths of Adelie penguins significantly less than 190mm?

3. Is there a significant difference in the flipper length of Adelie penguins vs. Gentoo penguins?

4. Let's create a normally distributed variable with roughly the same mean and standard deviation as the flipper length of Adelie penguins, but with twice the number of observations.

# Understanding Correlation

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

## But first, more challenges!

1. What is the correlation coefficient between bill length and flipper length in the `penguins` dataset?

2. Is this correlation statistically significant?

3. Let's verify our result visually, with a scatter plot! Bonus: How would we see if species matters? And how would we visualize the trend?
