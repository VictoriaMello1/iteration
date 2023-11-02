Writing Functions
================

``` r
library(tidyverse)
library(rvest)
```

    ## 
    ## Attaching package: 'rvest'

    ## The following object is masked from 'package:readr':
    ## 
    ##     guess_encoding

``` r
library(p8105.datasets)
```

Set seed for reproducibility:

``` r
set.seed(12345)
```

# Z score functions

Z scores subtract the mean and divide by the standard deviation

``` r
x_vec = rnorm(20, mean = 5, sd = .3)
```

Compute Z score for x_vec:

``` r
(x_vec - mean(x_vec)) / sd(x_vec)
```

    ##  [1]  0.6103734  0.7589907 -0.2228232 -0.6355576  0.6347861 -2.2717259
    ##  [7]  0.6638185 -0.4229355 -0.4324994 -1.1941438 -0.2311505  2.0874460
    ## [13]  0.3526784  0.5320552 -0.9917420  0.8878182 -1.1546150 -0.4893597
    ## [19]  1.2521303  0.2664557

Lets create a Function to do this Z score instead!

``` r
z_scores = function(x) {
  
  if (!is.numeric(x)) {
    stop("Argument x should be numeric")
  } else if (length(x) == 1) {
    stop("Z scores cannot be computed for length 1 vectors")
  }
  
  z = mean(x) / sd(x)
  
  z
}
```

if you tried to access this z variable it will not be in your global
library - it will only exist inside this function – good practice to
specify these arguments to make LOUD error messages when your function
does not work properly

Check this function works:

``` r
z_scores(x_vec)
```

    ## [1] 20.07731

# Multiple outputs

Write a function that returns mean and st dev from a sample of numbers

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

Check if this function works:

``` r
mean_and_sd(x_vec)
```

    ## # A tibble: 1 × 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1  5.02 0.250

# Start getting means an SDs

``` r
x_vec = rnorm(n = 30, mean = 5, sd = .5)

tibble(
    mean = mean(x_vec), 
    sd = sd(x_vec)
  )
```

    ## # A tibble: 1 × 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1  5.12 0.625

Lets write a funciton that uses ‘n’, a true mean, and true SD as inputs

``` r
sim_mean_sd = function(n_obs, mu, sigma) {
  x_vec = rnorm(n = n_obs, mean = mu, sd = sigma)
  
tibble(
    mean = mean(x_vec), 
    sd = sd(x_vec)
  )
}
```

if i wanted to make this function have a contstant value for mean or sd
i would specify this in the first line EX: sim_mean_sd = function(n_obs,
mu = 2, sigma = .5)  
– then you would only need to specify the n_obs for the function to work
bc mu and sigma are preset

Testing this sim_mean_sd function:

``` r
sim_mean_sd(n_obs = 30, mu = 5, sigma = .5)
```

    ## # A tibble: 1 × 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1  5.12 0.590

``` r
sim_mean_sd(30, 5, .5)
```

    ## # A tibble: 1 × 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1  5.12 0.517

``` r
sim_mean_sd(n_obs = 50, mu = 10, sigma = .5)
```

    ## # A tibble: 1 × 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1  9.99 0.566

if you do not explicity name mu = 5 etc in the () then R assumes you are
putting the numbers in the correct order you specified in the actual
function
