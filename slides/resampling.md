% Resampling and Permutation
% DA 101, Dr. Ladd

# How do you solve a problem like a T-Test?

## T-Tests rely on assumptions.

- Normality (Are both samples normally distributed?)
- Equality of Variance (Are the variables spread out roughly the same amount?)

## If either of these assumptions aren't met, our t-test could be misleading!

## "Parametric" hypothesis tests were designed to solve a problem before computers existed, but now there are other approaches.

# Resampling

## Resampling is simply drawing multiple random samples from observed data.

I can grab a sample of 5 observations. Then I can "resample" 5 more. Then 5 more, and so on and so on.

## First proposed in the 1960s, resampling procedures weren't practical until computing took off in the 1980s.

## Resampling is an umbrella term. It can include:

- The Bootstrap, used to assess the reliability of an estimated statistic
- Permutation Tests, used as an alternative to parametric hypothesis tests

## You can resample with or without *replacement*.

Replacement means an item is returned to the sample before the next draw (i.e. you could wind up with the same observation multiple times).

# Permutation Tests

## A permutation test solves the t-test problem!

It doesn't matter whether the samples are normally distributed or whether their variance is equal. There are no assumptions in a permutation test.

## *Permute* means to change the order of a set of values.

In a permutation test, you rearrange groups randomly to determine a permutation distribution.

## A permutation distribution embodies the *null hypothesis*.

It shows you what the distribution would look like if the difference between the groups was the result of random variation.

## You can create a permutation procedure to replace different kinds of statistical tests.

Let's look at the steps of a permutation test that would replace a two-sample t-test...

---

1. Randomly resample (without replacement) a group the same size at the first group.
2. From the remaining data, randomly resample (without replacement) a group the same size as the second group.
3. Calculate the difference in means between the two resamples. This is one permutation.
4. Repeat these steps as many times as you want to create a permutation distribution.
5. Compare the observed difference in the real groups to the permutation distribution.

## You can use the permutation distribution to calculate a p-value.
