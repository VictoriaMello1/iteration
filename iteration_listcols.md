Iteration and listcols
================

Set seed for reproducibility:

``` r
set.seed(12345)
```

# Lists

``` r
vec_numeric = 1:4
vec_char = c("my", "name", "is", "vicky")

tibble(
  num = vec_numeric,
  char = vec_char
)
```

    ## # A tibble: 4 × 2
    ##     num char 
    ##   <int> <chr>
    ## 1     1 my   
    ## 2     2 name 
    ## 3     3 is   
    ## 4     4 vicky

Different stuff with different lengths

``` r
l = list(
    vec_numeric = 1:5,
    vec_char = LETTERS,
    matrix(1:10, nrow = 5, ncol = 2),
    summary = summary(rnorm(100))
)
```

Accessing lists:

``` r
l$vec_char # <-- extracting the character vector
```

    ##  [1] "A" "B" "C" "D" "E" "F" "G" "H" "I" "J" "K" "L" "M" "N" "O" "P" "Q" "R" "S"
    ## [20] "T" "U" "V" "W" "X" "Y" "Z"

``` r
l[[1]] # <-- shows you what the 1st element in the list is (replace w diff numbers to see different elements)
```

    ## [1] 1 2 3 4 5

``` r
l[["summary"]] 
```

    ##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
    ## -2.3804 -0.5901  0.4837  0.2452  0.9004  2.4771

# Loops!

``` r
list_norm_samples = 
  list(
    a = rnorm(20, 1, 5),
    b = rnorm(20, 0, 7),
    c = rnorm(20, 20, 5),
    d = rnorm(20, -45, 13)
  )
```

Using the mean and sd function from functions unit:

``` r
mean_and_sd = function(x) {
  
  if (!is.numeric(x)) {
    stop("Argument x should be numeric")
  } else if (length(x) == 1) {
    stop("Cannot be computed for length 1 vectors")
  }
  
  mean_x = mean(x)
  sd_x = sd(x)

   tibble(
    mean = mean_x, 
    sd = sd_x
  )
}
```
