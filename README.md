
# assignmentB2QilinSong

`assignmentB2QilinSong` provides `count_all_missing_by_group()` to
summarize missing values by group. Given a data frame or tibble and a
grouping column, the function returns one row per group and the number
of missing values in each remaining column.

## Installation

Install version 0.1.0 from GitHub using `devtools`:

``` r
# Install devtools if needed:
# install.packages("devtools")

devtools::install_github(
  "UBC-STAT545-F2026/assignmentB2QilinSong",
  ref = "0.1.0"
)
```

## Usage

Load the package:

``` r
library(assignmentB2QilinSong)
```

### Count missing values by group

Count missing values in each column of the `airquality` dataset by
month. Supply the grouping column, `Month`, without quotation marks.

``` r
count_all_missing_by_group(datasets::airquality, Month)
#> # A tibble: 5 × 6
#>   Month Ozone Solar.R  Wind  Temp   Day
#>   <int> <int>   <int> <int> <int> <int>
#> 1     5     5       4     0     0     0
#> 2     6    21       0     0     0     0
#> 3     7     5       0     0     0     0
#> 4     8     5       3     0     0     0
#> 5     9     1       0     0     0     0
```

Each output row represents a month. The `Month` column identifies the
group, while the remaining columns report the number of missing values
within that month. The grouping column itself is excluded from the
missing-value counts.

### Use the pipe operator

The dataset can also be piped into the function. This produces the same
result as the previous example.

``` r
datasets::airquality |> count_all_missing_by_group(Month)
#> # A tibble: 5 × 6
#>   Month Ozone Solar.R  Wind  Temp   Day
#>   <int> <int>   <int> <int> <int> <int>
#> 1     5     5       4     0     0     0
#> 2     6    21       0     0     0     0
#> 3     7     5       0     0     0     0
#> 4     8     5       3     0     0     0
#> 5     9     1       0     0     0     0
```

### Retain grouping in the output

By default, `.groups = "drop"` returns an ungrouped result. Set
`.groups = "keep"` to retain grouping by month in the output.

``` r
count_all_missing_by_group(
  datasets::airquality,
  Month,
  .groups = "keep"
)
#> # A tibble: 5 × 6
#> # Groups:   Month [5]
#>   Month Ozone Solar.R  Wind  Temp   Day
#>   <int> <int>   <int> <int> <int> <int>
#> 1     5     5       4     0     0     0
#> 2     6    21       0     0     0     0
#> 3     7     5       0     0     0     0
#> 4     8     5       3     0     0     0
#> 5     9     1       0     0     0     0
```

## Acknowledgements

The function and initial documentation and tests were provided in the
STAT 545B Assignment B2 pre-baked materials. For this assignment, they
were turned into a R package.
