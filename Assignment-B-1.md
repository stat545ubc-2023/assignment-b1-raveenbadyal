Assignment B1
================
Raveen Badyal
3-Nov-2023

These are the packages required for this assignment. The code below
loads the packages, assuming they have been installed first.

``` r
library(tidyverse)
```

    ## ── Attaching core tidyverse packages ──────────────────────── tidyverse 2.0.0 ──
    ## ✔ dplyr     1.1.3     ✔ readr     2.1.4
    ## ✔ forcats   1.0.0     ✔ stringr   1.5.0
    ## ✔ ggplot2   3.4.3     ✔ tibble    3.2.1
    ## ✔ lubridate 1.9.2     ✔ tidyr     1.3.0
    ## ✔ purrr     1.0.2     
    ## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
    ## ✖ dplyr::filter() masks stats::filter()
    ## ✖ dplyr::lag()    masks stats::lag()
    ## ℹ Use the conflicted package (<http://conflicted.r-lib.org/>) to force all conflicts to become errors

``` r
library(devtools)
```

    ## Loading required package: usethis

``` r
library(testthat)
```

    ## 
    ## Attaching package: 'testthat'
    ## 
    ## The following object is masked from 'package:devtools':
    ## 
    ##     test_file
    ## 
    ## The following object is masked from 'package:dplyr':
    ## 
    ##     matches
    ## 
    ## The following object is masked from 'package:purrr':
    ## 
    ##     is_null
    ## 
    ## The following objects are masked from 'package:readr':
    ## 
    ##     edition_get, local_edition
    ## 
    ## The following object is masked from 'package:tidyr':
    ## 
    ##     matches

### Exercise 1-2: Make and Document a Function

``` r
#' Pounds to Kilograms
#'
#' This function will take an input, in pounds, and return the conversion to kilograms rounded to 2 decimal points for conciseness. Only inputs greater than 0.02 can be inputted. If a smaller input is made, the function will specify that it can't compute the conversion.
#'
#' @param The argument for this function is lb. Lb is the symbol/abbreviation for pounds. This is a numeric argument. The inputs must be greater than 0.02.
#'
#' @return The function returns a number, kg, which is the converted inputted pounds into kilograms. The output is limited to two decimal places for conciseness.


lb_to_kg <- function(lb) {
  if(!is.numeric(lb)) {
    return('This function only works for numeric input.')
  }
  if(lb < 0.02) {
    return("Your input for lb is too small for this function")
  }
  kg <- round(lb / 2.20462, digits = 2)
  return (kg)
}
```

### Exercise 3: Include examples

The following examples are a few numeric inputs for lb, including inputs
with decimal places. I have included a smaller number, and a larger
number (1, 10). Also inputs with decimals places, one less than 1
(0.0343) and the second, much greater (1000.474745). At first, I limited
my function to two digits total. When I tested the below inputs with
that function, the larger number inputs were capped, and returned “454”.
I was able to see an error in the functionality of my function, and
changed the function so there was a limit on decimal places and not the
number of digits of the output.

``` r
lb_to_kg(0.0343)
```

    ## [1] 0.02

``` r
lb_to_kg(1)
```

    ## [1] 0.45

``` r
lb_to_kg(10)
```

    ## [1] 4.54

``` r
lb_to_kg(1000)
```

    ## [1] 453.59

``` r
lb_to_kg(1000.474745)
```

    ## [1] 453.81

The following examples are numeric inputs for lb, that are too small to
acheive a result as this function’s output is limited to 2 decimal
places.

``` r
lb_to_kg(0)
```

    ## [1] "Your input for lb is too small for this function"

``` r
lb_to_kg(0.019)
```

    ## [1] "Your input for lb is too small for this function"

``` r
lb_to_kg(0.002)
```

    ## [1] "Your input for lb is too small for this function"

The following examples are non-numeric inputs for lb.

``` r
lb_to_kg("Hi")
```

    ## [1] "This function only works for numeric input."

``` r
lb_to_kg(TRUE)
```

    ## [1] "This function only works for numeric input."

### Exercise 4: Test the Function

There is one test to determine if the function gives an error for inputs
less than 0.02. The next test tests if there will be a valid output for
0.02 to test the bounds of the function. Finally, for numbers, there is
a “normal” number to ensure the function will work on more usual inputs.
The last test is for a non-numeric input, to see if we will get the
correct error message.

``` r
test_that("Testing lb to kg conversion function", {
  expect_equal(lb_to_kg(0), "Your input for lb is too small for this function")
  expect_equal(lb_to_kg(0.02), 0.01)
  expect_equal(lb_to_kg(10), 4.54)
  expect_equal(lb_to_kg("hi"), "This function only works for numeric input.")
})
```

    ## Test passed 🎊
