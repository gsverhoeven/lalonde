
<!-- README.md is generated from README.Rmd. Please edit that file -->
About `lalonde`
===============

[![Travis-CI Build Status](https://travis-ci.org/jjchern/lalonde.svg?branch=master)](https://travis-ci.org/jjchern/lalonde) [![AppVeyor Build Status](https://ci.appveyor.com/api/projects/status/github/jjchern/lalonde?branch=master&svg=true)](https://ci.appveyor.com/project/jjchern/lalonde) [![CRAN\_Status\_Badge](http://www.r-pkg.org/badges/version/lalonde)](https://cran.r-project.org/package=lalonde)

The Lalonde datasets are widely used in the causal inference literature. The current package makes loading such datasets in R easier. I found myself calling the following command

``` r
haven::read_dta("http://www.nber.org/~rdehejia/data/nsw_dw.dta")
```

in several R projects. It might be easier to just type `lalonde::nsw_dw`.

Data and Source
===============

-   NSW Data Files (Lalonde Sample)
    -   `lalonde::nsw`
    -   These files contain the treated and control units from the male sub-sample from the National Supported Work Demonstration as used by Lalonde in his paper.
-   NSW Data Files (Dehejia-Wahha Sample)
    -   `lalonde::nsw_dw`
    -   Based on pre-intervention variables, Dehejia-Wahha extract a further subset of Lalonde's NSW experimental data, a subset containing information on RE74 (earnings in 1974).
-   Non-experimental Comparison Data Files:
    -   `lalonde::psid_controls`
    -   `lalonde::psid_controls2`
    -   `lalonde::psid_controls3`
    -   `lalonde::cps_controls`
    -   `lalonde::cps_controls2`
    -   `lalonde::cps_controls3`
-   All the datasets are available in `txt` and `dta` format from Dehejia's [website](http://users.nber.org/~rdehejia/nswdata2.html)

Installation
============

``` r
# install.packages("devtools")
devtools::install_github("jjchern/lalonde")
```

Usage
=====

The datasets print nicely in the tidyverse:

``` r
library(tidyverse)

lalonde::nsw
#> # A tibble: 722 x 10
#>           data_id treat   age education black hispanic married nodegree
#>             <chr> <dbl> <dbl>     <dbl> <dbl>    <dbl>   <dbl>    <dbl>
#>  1 Lalonde Sample     1    37        11     1        0       1        1
#>  2 Lalonde Sample     1    22         9     0        1       0        1
#>  3 Lalonde Sample     1    30        12     1        0       0        0
#>  4 Lalonde Sample     1    27        11     1        0       0        1
#>  5 Lalonde Sample     1    33         8     1        0       0        1
#>  6 Lalonde Sample     1    22         9     1        0       0        1
#>  7 Lalonde Sample     1    23        12     1        0       0        0
#>  8 Lalonde Sample     1    32        11     1        0       0        1
#>  9 Lalonde Sample     1    22        16     1        0       0        0
#> 10 Lalonde Sample     1    33        12     0        0       1        0
#> # ... with 712 more rows, and 2 more variables: re75 <dbl>, re78 <dbl>

lalonde::nsw_dw
#> # A tibble: 445 x 11
#>                 data_id treat   age education black hispanic married
#>                   <chr> <dbl> <dbl>     <dbl> <dbl>    <dbl>   <dbl>
#>  1 Dehejia-Wahba Sample     1    37        11     1        0       1
#>  2 Dehejia-Wahba Sample     1    22         9     0        1       0
#>  3 Dehejia-Wahba Sample     1    30        12     1        0       0
#>  4 Dehejia-Wahba Sample     1    27        11     1        0       0
#>  5 Dehejia-Wahba Sample     1    33         8     1        0       0
#>  6 Dehejia-Wahba Sample     1    22         9     1        0       0
#>  7 Dehejia-Wahba Sample     1    23        12     1        0       0
#>  8 Dehejia-Wahba Sample     1    32        11     1        0       0
#>  9 Dehejia-Wahba Sample     1    22        16     1        0       0
#> 10 Dehejia-Wahba Sample     1    33        12     0        0       1
#> # ... with 435 more rows, and 4 more variables: nodegree <dbl>,
#> #   re74 <dbl>, re75 <dbl>, re78 <dbl>
```

Combine the treatment group from `lalonde::nsw_dw` with a non-experimental comparison group from the Panel Study of Income Dynamics (PSID):

``` r
lalonde::nsw_dw %>% 
    filter(treat == 1) %>% 
    bind_rows(lalonde::psid_controls)
#> # A tibble: 2,675 x 11
#>                 data_id treat   age education black hispanic married
#>                   <chr> <dbl> <dbl>     <dbl> <dbl>    <dbl>   <dbl>
#>  1 Dehejia-Wahba Sample     1    37        11     1        0       1
#>  2 Dehejia-Wahba Sample     1    22         9     0        1       0
#>  3 Dehejia-Wahba Sample     1    30        12     1        0       0
#>  4 Dehejia-Wahba Sample     1    27        11     1        0       0
#>  5 Dehejia-Wahba Sample     1    33         8     1        0       0
#>  6 Dehejia-Wahba Sample     1    22         9     1        0       0
#>  7 Dehejia-Wahba Sample     1    23        12     1        0       0
#>  8 Dehejia-Wahba Sample     1    32        11     1        0       0
#>  9 Dehejia-Wahba Sample     1    22        16     1        0       0
#> 10 Dehejia-Wahba Sample     1    33        12     0        0       1
#> # ... with 2,665 more rows, and 4 more variables: nodegree <dbl>,
#> #   re74 <dbl>, re75 <dbl>, re78 <dbl>
```
