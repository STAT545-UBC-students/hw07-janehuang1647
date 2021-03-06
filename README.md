<!-- README.md is generated from README.Rmd. Please edit that file -->
This is the repository for ZHENYI HUANG's HW07.
===============================================

Please refer to the following table for easy access:

| List of the Files                                                                                  |
|----------------------------------------------------------------------------------------------------|
| [R script file](https://github.com/STAT545-UBC-students/hw07-janehuang1647/tree/master/R)          |
| [Description files](https://github.com/STAT545-UBC-students/hw07-janehuang1647/tree/master/man)    |
| [Test files](https://github.com/STAT545-UBC-students/hw07-janehuang1647/tree/master/tests)         |
| [Vignettes file](https://github.com/STAT545-UBC-students/hw07-janehuang1647/tree/master/vignettes) |

*NOTE*:

-   This package is originally developed by @jennybc, please check here for the original GitHub repository [foofactor](https://github.com/jennybc/foofactors).

-   This is a toy package created for expository purposes. It is not meant to actually be useful. If you want a package for factor handling, please see [forcats](https://cran.r-project.org/package=forcats).\*\*

### foofactors

Factors are a very useful type of variable in R, but they can also drive you nuts. This package provides some helper functions for the care and feeding of factors.

### Installation

``` r
devtools::install_github("STAT545-UBC-students/hw07-janehuang1647")
```

### Quick demo

Binding two factors via `fbind()`:

``` r
library(foofactors)
a <- factor(c("character", "hits", "your", "eyeballs"))
b <- factor(c("but", "integer", "where it", "counts"))
```

Simply catenating two factors leads to a result that most don't expect.

``` r
c(a, b)
#> [1] 1 3 4 2 1 3 4 2
```

The `fbind()` function glues two factors together and returns factor.

``` r
fbind(a, b)
#> [1] character hits      your      eyeballs  but       integer   where it 
#> [8] counts   
#> Levels: but character counts eyeballs hits integer where it your
```

Often we want a table of frequencies for the levels of a factor. The base `table()` function returns an object of class `table`, which can be inconvenient for downstream work. Processing with `as.data.frame()` can be helpful but it's a bit clunky.

``` r
set.seed(1234)
x <- factor(sample(letters[1:5], size = 100, replace = TRUE))
table(x)
#> x
#>  a  b  c  d  e 
#> 25 26 17 17 15
as.data.frame(table(x))
#>   x Freq
#> 1 a   25
#> 2 b   26
#> 3 c   17
#> 4 d   17
#> 5 e   15
```

The `freq_out()` function returns a frequency table as a well-named `tbl_df`:

``` r
freq_out(x)
#> # A tibble: 5 x 2
#>   x         n
#>   <fct> <int>
#> 1 a        25
#> 2 b        26
#> 3 c        17
#> 4 d        17
#> 5 e        15
```

The `factor_check()` function returns a stopping message if the input is not a factor:

``` r
factor_check(x)
```

The `freorder()`function returns a factor in a descending order:

``` r
freorder(x)
#>   [1] a d d d e d a b d c d c b e b e b b a b b b a a b e c e e a c b b c a
#>  [36] d b b e e c d b d b c d c b d a b d c a c c d a e e a b a b d b c a c
#>  [71] a e a d a c b a b d e c a c a e b b a e a e a a a c b a b d
#> attr(,"scores")
#>  a  b  c  d  e 
#> -1 -2 -3 -4 -5 
#> Levels: e d c b a
```

The `fset_level()` function sets levels to the order in which they appear in the data, i.e. set the levels “as is”:

``` r
y <- c("apple","coconut","banana")
yfx <- factor(y)
#check bothe the level of the original factor and after the fset_level() function.
levels(yfx) # the levels is ordered in alphabetical order
#> [1] "apple"   "banana"  "coconut"
levels(fset_level(yfx))  # the level is ordered in the order of the original factor.
#> [1] "apple"   "coconut" "banana"
```

The `df_read()` then read the data from the file and retating the factor levels.

``` r
(a <- df_read ("gapminderTest.txt"))
#> [1] list.testing...c.A..B..C..E..
#> <0 rows> (or 0-length row.names)
# check its structure to see whether the factor level retained.
str(a)
#> 'data.frame':    0 obs. of  1 variable:
#>  $ list.testing...c.A..B..C..E..: logi
```

The `df_write()` write a dataframe into the file. we can write the above dataframe to file

``` r

    df_write(a, "./gapMinderTest.txt")
```
