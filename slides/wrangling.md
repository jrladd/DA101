% Data Wrangling with dplyr
% DA 101, Dr. Ladd
% Week 3

# First, Let's Review

## In-Class Exercise

1. Create a new .R file
1. Install and import the ggplot2 library
2. Make sure to add comments as you go!
2. Find the `mpg` dataset, view it, and get a summary
3. Select a column from `mpg` and get its mean and median
4. Create a basic scatterplot of two `mpg` variables (columns)

## All this and more in [Chapter 4](https://r4ds.had.co.nz/workflow-basics.html) of our textbook!

# Wrangling Data

## Tibbles are special Data Frames

```r
library(tidyverse)

library(nycflights13)

flights
```

## Every variable (column) has a data type.

- int: integers
- dbl: doubles, floats, or real numbers
- chr: character, or string
- dttm: date-times
- lgl: logical, True or False
- fctr: factors (categorical variables)
- date: dates

# Filtering and Selecting

## Filter lets you get a subset of observations (rows).

```r
filter(flights, month==1, day==1)
```

or with dplyr's special "pipe" notation:

```r
flights %>%
	filter(month==1, day==1)
```

These two are the same!

## You can save `dplyr` outputs to variables.

```r
dec25 <- filter(flights, month == 12, day == 25)
```

## `filter()` uses standard comparisons.

- `>`: greater than
- `>=`: greater than or equal to
- `<`: less than
- `<=`: less than or equal to
- `!=`: not equal
- `==`: equal (note the double equals sign!)

## `filter()` also uses logical operators to combine comparisons.

& "and", | "or", and ! "not"

![](img/transform-logical.png)

## Logical operators can also be combined.

```r
filter(flights, month == 11 | month == 12)

nov_dec <- filter(flights, month %in% c(11, 12))

filter(flights, !(arr_delay > 120 | dep_delay > 120))

filter(flights, arr_delay <= 120, dep_delay <= 120)
```

## Null values are never part of the filter!

It's because they are never "true". You must ask for them explicitly with `is.na()`.

```r
df <- tibble(x = c(1, NA, 3))

filter(df, x > 1)

filter(df, is.na(x) | x > 1)
```

## You try it!

Work through the exercise in the textbook, section 5.2.4

## Arrange lets you sort rows.

```r
arrange(flights, year, month, day)

arrange(flights, desc(dep_delay))
```

## Select lets you get a set of variables (columns).

```r
select(flights, year, month, day)

select(flights, year:day)

select(flights, -(year:day))
```

See the [textbook](https://r4ds.had.co.nz/transform.html#select) for additional tips.

## Rename lets you rename columns.

```r
rename(flights, tail_num = tailnum)
```

## Mutate lets you add new columns based on existing ones.

```r
mutate(flights,
  gain = dep_delay - arr_delay,
  hours = air_time / 60,
  gain_per_hour = gain / hours
)
```

Transmute does the same thing but only keeps the new variables.

## You Try It!

Exercises 5.3.1, 5.4.1, 5.5.2

# Summarizing and Grouping

## Summarize lets you get summary statistics.

```r
summarize(flights, delay = mean(dep_delay, na.rm = TRUE))
```

Other summary functions: `median(), min(), max(), sd(), range()`.

## Groupby lets you group data, to get summaries for each group.

```r
by_month <- group_by(flights, year, month)
summarize(by_month, delay = mean(dep_delay, na.rm = TRUE))
```

## The pipe lets you "stack" multiple `dplyr` operations.

```r
delays_by_month <- flights %>%
	group_by(year, month) %>%
	summarize(delay = mean(dep_delay, na.rm=TRUE))
```

```r
delays <- flights %>%
  group_by(dest) %>%
  summarize(
    count = n(),
    dist = mean(distance, na.rm = TRUE),
    delay = mean(arr_delay, na.rm = TRUE)
  ) %>%
  filter(count > 20, dest != "HNL")
```
