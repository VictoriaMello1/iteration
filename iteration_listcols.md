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

Applying the function

``` r
mean_and_sd(list_norm_samples$a)
```

    ## # A tibble: 1 × 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1  1.25  4.92

``` r
mean_and_sd(list_norm_samples$b)
```

    ## # A tibble: 1 × 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1 0.690  9.30

``` r
mean_and_sd(list_norm_samples$c)
```

    ## # A tibble: 1 × 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1  18.8  4.55

``` r
mean_and_sd(list_norm_samples$d)
```

    ## # A tibble: 1 × 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1 -44.1  14.0

It is easier to apply the function when you use a loop function or a for
loop to keep track of all the elements of your input list and saves the
results of applying the function to the output list

``` r
output = vector("list", length = 4)

for (i in 1:4) {
  output[[i]] = mean_and_sd(list_norm_samples[[i]])
  
}
output # <-- can enter this in the Console to have output produced if not working here
```

    ## [[1]]
    ## # A tibble: 1 × 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1  1.25  4.92
    ## 
    ## [[2]]
    ## # A tibble: 1 × 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1 0.690  9.30
    ## 
    ## [[3]]
    ## # A tibble: 1 × 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1  18.8  4.55
    ## 
    ## [[4]]
    ## # A tibble: 1 × 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1 -44.1  14.0

# Use ‘map’ function – map(your data inputs, function you want to apply to the inputs)

This one line of code replaces the for loops we did above

``` r
output = map(list_norm_samples, mean_and_sd)

output = map(list_norm_samples, summary)
```
