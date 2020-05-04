---
title: 's04: `dplyr` Exercise'
output: 
  html_document:
    keep_md: true
    theme: paper
---

<!---The following chunk allows errors when knitting--->



**When you make an Rmd file for participation or homework, be sure to do this**:

1. Change the file output to both html and md _documents_ (not notebook).
  - See the `keep_md: TRUE` argument above.

2. `knit` the document. 

3. Stage and commit the Rmd and knitted documents.


# Intro to `dplyr` syntax

Load the `gapminder` and `tidyverse` packages.
    - This loads `dplyr`, too.

Hint: You can add the `suppressPackageStartupMessages()` function around the 
      `library()` command to keep your output looking nice!
    

```r
# load your packages here:
library()
library(dplyr)
library(tidyverse)
```
    

## `select()`

1. Make a data frame containing the columns `year`, `lifeExp`, `country` from 
the `gapminder` data, in that order.


```r
select(gapminder, country, continent, year, lifeExp)
```

```
## Error in select(gapminder, country, continent, year, lifeExp): object 'gapminder' not found
```

2. Select all variables, from `country` to `lifeExp`.


```r
# This will work:
select(gapminder, country, continent, year, lifeExp)
```

```
## Error in select(gapminder, country, continent, year, lifeExp): object 'gapminder' not found
```

```r
# Better way:
select(gapminder, country:lifeExp)
```

```
## Error in select(gapminder, country:lifeExp): object 'gapminder' not found
```

3. Select all variables, except `lifeExp`.


```r
select(gapminder, -lifeExp)
```

```
## Error in select(gapminder, -lifeExp): object 'gapminder' not found
```

4. Put `continent` first. Hint: use the `everything()` function.


```r
select(gapminder, continent, everything())
```

```
## Error in select(gapminder, continent, everything()): object 'gapminder' not found
```

5. Rename `continent` to `cont`.


```r
# compare
select(gapminder, cont = continent, everything())
```

```
## Error in select(gapminder, cont = continent, everything()): object 'gapminder' not found
```

```r
rename(gapminder, cont = continent)
```

```
## Error in rename(gapminder, cont = continent): object 'gapminder' not found
```

```r
rename_all(gapminder, toupper)
```

```
## Error in tbl_vars_dispatch(x): object 'gapminder' not found
```

```r
gapminder_new <- rename(gapminder, cont = continent)
```

```
## Error in rename(gapminder, cont = continent): object 'gapminder' not found
```

```r
gapminder_new
```

```
## Error in eval(expr, envir, enclos): object 'gapminder_new' not found
```


```r
mtcars
```

```
##                      mpg cyl  disp  hp drat    wt  qsec vs am gear carb
## Mazda RX4           21.0   6 160.0 110 3.90 2.620 16.46  0  1    4    4
## Mazda RX4 Wag       21.0   6 160.0 110 3.90 2.875 17.02  0  1    4    4
## Datsun 710          22.8   4 108.0  93 3.85 2.320 18.61  1  1    4    1
## Hornet 4 Drive      21.4   6 258.0 110 3.08 3.215 19.44  1  0    3    1
## Hornet Sportabout   18.7   8 360.0 175 3.15 3.440 17.02  0  0    3    2
## Valiant             18.1   6 225.0 105 2.76 3.460 20.22  1  0    3    1
## Duster 360          14.3   8 360.0 245 3.21 3.570 15.84  0  0    3    4
## Merc 240D           24.4   4 146.7  62 3.69 3.190 20.00  1  0    4    2
## Merc 230            22.8   4 140.8  95 3.92 3.150 22.90  1  0    4    2
## Merc 280            19.2   6 167.6 123 3.92 3.440 18.30  1  0    4    4
## Merc 280C           17.8   6 167.6 123 3.92 3.440 18.90  1  0    4    4
## Merc 450SE          16.4   8 275.8 180 3.07 4.070 17.40  0  0    3    3
## Merc 450SL          17.3   8 275.8 180 3.07 3.730 17.60  0  0    3    3
## Merc 450SLC         15.2   8 275.8 180 3.07 3.780 18.00  0  0    3    3
## Cadillac Fleetwood  10.4   8 472.0 205 2.93 5.250 17.98  0  0    3    4
## Lincoln Continental 10.4   8 460.0 215 3.00 5.424 17.82  0  0    3    4
## Chrysler Imperial   14.7   8 440.0 230 3.23 5.345 17.42  0  0    3    4
## Fiat 128            32.4   4  78.7  66 4.08 2.200 19.47  1  1    4    1
## Honda Civic         30.4   4  75.7  52 4.93 1.615 18.52  1  1    4    2
## Toyota Corolla      33.9   4  71.1  65 4.22 1.835 19.90  1  1    4    1
## Toyota Corona       21.5   4 120.1  97 3.70 2.465 20.01  1  0    3    1
## Dodge Challenger    15.5   8 318.0 150 2.76 3.520 16.87  0  0    3    2
## AMC Javelin         15.2   8 304.0 150 3.15 3.435 17.30  0  0    3    2
## Camaro Z28          13.3   8 350.0 245 3.73 3.840 15.41  0  0    3    4
## Pontiac Firebird    19.2   8 400.0 175 3.08 3.845 17.05  0  0    3    2
## Fiat X1-9           27.3   4  79.0  66 4.08 1.935 18.90  1  1    4    1
## Porsche 914-2       26.0   4 120.3  91 4.43 2.140 16.70  0  1    5    2
## Lotus Europa        30.4   4  95.1 113 3.77 1.513 16.90  1  1    5    2
## Ford Pantera L      15.8   8 351.0 264 4.22 3.170 14.50  0  1    5    4
## Ferrari Dino        19.7   6 145.0 175 3.62 2.770 15.50  0  1    5    6
## Maserati Bora       15.0   8 301.0 335 3.54 3.570 14.60  0  1    5    8
## Volvo 142E          21.4   4 121.0 109 4.11 2.780 18.60  1  1    4    2
```

## `arrange()`

1. Order by year.


```r
arrange(gapminder, year)
```

```
## Error in arrange(gapminder, year): object 'gapminder' not found
```

2. Order by year, in descending order.
or use - as another option


```r
arrange(gapminder, desc(year))
```

```
## Error in arrange(gapminder, desc(year)): object 'gapminder' not found
```

3. Order by year, then by life expectancy.


```r
arrange(gapminder, year, lifeExp)
```

```
## Error in arrange(gapminder, year, lifeExp): object 'gapminder' not found
```


## Piping, `%>%`

Note: think of `%>%` as the word "then"!

Demonstration:

Here I want to combine `select()` Task 1 with `arrange()` Task 3.

### Base R method

This is how I could do it by *nesting* the two function calls:


```r
# Nesting function calls can be hard to read
arrange(select(gapminder, year, lifeExp, country), year, lifeExp)
```


```r
gap_sel <- select(gapminder, year, lifeExp, country)
arrange(gap_sel, year, lifeExp)
```

### tidyverse method

Now using with pipes:


```r
# alter the below to include 2 "pipes"
gapminder %>% 
  select(year, lifeExp, country) %>% 
  arrange(year, lifeExp)
```

```
## Error in eval(lhs, parent, parent): object 'gapminder' not found
```

```r
arrange(select(gapminder, year, lifeExp, country), year, lifeExp)
```

```
## Error in select(gapminder, year, lifeExp, country): object 'gapminder' not found
```


# Back to Guide 

Return to guide at the section on *Relational/Comparison and Logical Operators in R*.


# Transforming datasets

## `filter()`

1. Only take data with population greater than 100 million.


```r
gapminder %>%
  filter(pop > 1000000)
```

```
## Error in eval(lhs, parent, parent): object 'gapminder' not found
```

2. Your turn: of those rows filtered from step 1., only take data from Asia.


```r
gapminder %>%
  filter(pop > 10000000, continent == "Asia")
```

```
## Error in eval(lhs, parent, parent): object 'gapminder' not found
```

3. Repeat 2, but take data from countries Brazil, and China. 


```r
gapminder %>%
  filter(pop > 10000000, country %in% c("Brazil", "China"))
```

```
## Error in eval(lhs, parent, parent): object 'gapminder' not found
```

## `mutate()` (10 min)

The `mutate()` function _creates_ new columns in the tibble by transforming other variables. Like `select()`, `filter()`, and `arrange()`, the `mutate()` function also takes a tibble as its first argument, and returns a tibble. 

The general syntax is:

```
mutate(tibble, NEW_COLUMN_NAME = CALCULATION)
```

Let's get: 

- GDP by multiplying GPD per capita with population, and
- GDP in billions, named (`gdpBill`), rounded to two decimals.


```r
gapminder %>%
  mutate(grossGDP = gdpPercap * pop,
gdpBill = (grossGDP / 1000000000) %>% round (2))
```

```
## Error in eval(lhs, parent, parent): object 'gapminder' not found
```

Notice the backwards compatibility! No need for loops!

Try the same thing, but with `transmute` (drops all other variables). 


```r
gapminder %>%
  transmute(gdpBill = (pop * gdpPercap/ 1000000000) %>% round (2))
```

```
## Error in eval(lhs, parent, parent): object 'gapminder' not found
```

The `if_else` function is useful for changing certain elements in a data frame.

Example: Suppose Canada's 1952 life expectancy was mistakenly entered as 68.8 in the data frame, but is actually 70. Fix it using `if_else` and `mutate`. 

Replace life expectancy for Bangladesh with NA_real_.


```r
gapminder %>%
  mutate(lifeExp = if_else(country == "Canada" & year == 1952,
                           70,
                           lifeExp)) %>% filter(country == "Canada")
```

```
## Error in eval(lhs, parent, parent): object 'gapminder' not found
```

```r
gapminder %>% 
mutate(lifeExp = if_else(country == "Bangladesh",
                           NA_real_,
                           lifeExp)) %>% filter(country == "Bangladesh")
```

```
## Error in eval(lhs, parent, parent): object 'gapminder' not found
```


Your turn: Make a new column called `cc` that pastes the country name followed by the continent, separated by a comma. (Hint: use the `paste` function with the `sep=", "` argument).




```r
These functions we've seen are called __vectorized functions__—they are designed 
to work with vectors and do their computation on each element of the vector(s).

## git stuff

Now is a good time to knit, commit, push!


# Back to Guide Again

Let's head back to the guide at the section on `summarize()`.


# Exercises for grouped data frames

Let's do some practice with grouping (and ungrouping) and summarizing data frames!

1. (a) What's the minimum life expectancy for each continent and each year? (b) Add the corresponding country to the tibble, too. (c) Arrange by min life expectancy.
```

```
## Error: <text>:1:7: unexpected symbol
## 1: These functions
##           ^
```

```r
gapminder %>% 
  group_by(FILL_THIS_IN) %>% 
  FILL_THIS_IN(min_life = min(lifeExp))
```

```
## Error in eval(lhs, parent, parent): object 'gapminder' not found
```


2. Let's compute the mean Agreeableness score across items for each participant 
in the `psych::bfi` dataset. Be sure to handle `NA`!


```r
psych::bfi %>%
  as_tibble() %>% 
  select(A1:A5) %>% 
  rowwise() %>% 
  mutate(A_mean = mean(c(A1, A2, A3, A4, A5), na.rm = TRUE)) %>% 
  ungroup()
```

```
## # A tibble: 2,800 x 6
##       A1    A2    A3    A4    A5 A_mean
##    <int> <int> <int> <int> <int>  <dbl>
##  1     2     4     3     4     4    3.4
##  2     2     4     5     2     5    3.6
##  3     5     4     5     4     4    4.4
##  4     4     4     6     5     5    4.8
##  5     2     3     3     4     5    3.4
##  6     6     6     5     6     5    5.6
##  7     2     5     5     3     5    4  
##  8     4     3     1     5     1    2.8
##  9     4     3     6     3     3    3.8
## 10     2     5     6     6     5    4.8
## # … with 2,790 more rows
```

Now compute mean scores for the other Big Five traits, as well as 
`sd` and `min` scores for reach person.



** There are a few other ways to do this sort of computation.**

`rowMeans()` computes the mean of each row of a data frame. We can use it by
putting `select()` inside of `mutate()`:


```r
psych::bfi %>% 
  as_tibble() %>% 
  select(A1:A5) %>% 
  mutate(A_mn = rowMeans(select(., A1:A5)),
         A_mn2 = rowMeans(select(., starts_with("A", ignore.case = FALSE))))
```

```
## # A tibble: 2,800 x 7
##       A1    A2    A3    A4    A5  A_mn A_mn2
##    <int> <int> <int> <int> <int> <dbl> <dbl>
##  1     2     4     3     4     4   3.4   3.4
##  2     2     4     5     2     5   3.6   3.6
##  3     5     4     5     4     4   4.4   4.4
##  4     4     4     6     5     5   4.8   4.8
##  5     2     3     3     4     5   3.4   3.4
##  6     6     6     5     6     5   5.6   5.6
##  7     2     5     5     3     5   4     4  
##  8     4     3     1     5     1   2.8   2.8
##  9     4     3     6     3     3   3.8   3.8
## 10     2     5     6     6     5   4.8   4.8
## # … with 2,790 more rows
```

Some functions are **vectorized**, so you don't need `rowwise()`. 
For example, `pmin()` computes the "parallel min" across the vectors it receives:


```r
psych::bfi %>% 
  as_tibble() %>% 
  select(A1:A5) %>% 
  mutate(A_min = pmin(A1, A2, A3, A4, A5))
```

```
## # A tibble: 2,800 x 6
##       A1    A2    A3    A4    A5 A_min
##    <int> <int> <int> <int> <int> <int>
##  1     2     4     3     4     4     2
##  2     2     4     5     2     5     2
##  3     5     4     5     4     4     4
##  4     4     4     6     5     5     4
##  5     2     3     3     4     5     2
##  6     6     6     5     6     5     5
##  7     2     5     5     3     5     2
##  8     4     3     1     5     1     1
##  9     4     3     6     3     3     3
## 10     2     5     6     6     5     2
## # … with 2,790 more rows
```


3. Calculate the growth in population since the first year on record 
_for each country_ by rearranging the following lines, and filling in the 
`FILL_THIS_IN`. Here's another convenience function for you: `dplyr::first()`. 

```
mutate(rel_growth = FILL_THIS_IN) %>% 
arrange(FILL_THIS_IN) %>% 
gapminder %>% 
knitr::kable()
group_by(country) %>% 
```




4. Determine the country, on each continent, that experienced the 
**sharpest 5-year drop in life expectancy**, sorted by the drop, by rearranging 
the following lines of code. Ensure there are no `NA`'s. A helpful function to 
compute changes in a variable across rows of data (e.g., for time-series data) 
is `tsibble::difference()`:

```
drop_na() %>% 
ungroup() %>% 
arrange(year) %>% 
filter(inc_life_exp == min(inc_life_exp)) %>% 
gapminder %>% 
mutate(inc_life_exp = FILL_THIS_IN) %>% # Compute the changes in life expectancy
arrange(inc_life_exp) %>% 
group_by(country) %>% 
group_by(continent) %>% 
knitr::kable()
```




# Bonus Exercises

If there's time remaining, we'll practice with these three exercises. 
I'll give you a minute for each, then we'll go over the answer.

1. In `gapminder`, take all countries in Europe that have a GDP per capita 
   greater than 10000, and select all variables except `gdpPercap`. 
   (Hint: use `-`).

2. Take the first three columns of `gapminder` and extract the names.

3. In `gapminder`, convert the population to a number in billions.

4. Take the `iris` data frame and extract all columns that start with 
   the word "Petal". 
    - Hint: take a look at the "Select helpers" documentation by running the 
      following code: `?tidyselect::select_helpers`.

5. Filter the rows of `iris` for Sepal.Length >= 4.6 and Petal.Width >= 0.5.

Exercises 4. and 5. are from 
[r-exercises](https://www.r-exercises.com/2017/10/19/dplyr-basic-functions-exercises/).
