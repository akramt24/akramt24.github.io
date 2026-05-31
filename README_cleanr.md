
# cleanr

cleanr is an R package that provides simple, lightweight helper
functions for common data cleaning tasks. It is designed for anyone who
works with messy real-world datasets and wants quick, reliable tools to
understand and clean their data before analysis.

## Installation

``` r
remotes::install_github("ADC-405-S26/cleanr")
```

## Functions

cleanr has three main functions:

- `describe_na()` — summarizes missing values in each column of a data
  frame, showing the count and percentage of NAs. Use this as your first
  step when exploring a new dataset.

- `standardize_names()` — converts all column names to lowercase
  snake_case by replacing spaces and special characters with
  underscores. This makes column names safe to use in R without
  backticks.

- `remove_outliers()` — removes rows where a numeric column contains
  extreme values, using either the IQR fence method or the Z-score
  method. Note: always inspect removed rows before discarding, as
  extreme values may be data entry errors rather than true outliers.

## Example

``` r
library(cleanr)

# Step 1: See where the missing values are
describe_na(messy_data)
#>     variable n_missing pct_missing
#> 1 first_name         1          20
#> 2  last_name         1          20
#> 3        age         1          20
#> 4     salary         0           0

# Step 2: Clean the column names
df <- data.frame("First Name" = 1, "Last-Name!" = 2, check.names = FALSE)
standardize_names(df)
#>   first_name last_name
#> 1          1         2

# Step 3: Remove outliers from a numeric column
df2 <- data.frame(x = c(1, 2, 3, 4, 100))
remove_outliers(df2, col = "x", method = "iqr")
#>   x
#> 1 1
#> 2 2
#> 3 3
#> 4 4
```

## Dataset

cleanr includes a built-in dataset called `messy_data`, a small data
frame with missing values and an extreme salary outlier, designed to
help you practice all three functions right away.
