# Summarizing PKBD mixture Fits

Summary method for class "pkbc"

## Usage

``` r
# S4 method for class 'pkbc'
summary(object)
```

## Arguments

- object:

  Object of class `pkbc`

## Value

Display the logLikelihood values and within cluster sum of squares
(wcss) for all the values of number of clusters provided. For each of
these values the estimated mixing proportions are showed together with a
table with the assigned memberships.

## See also

[`pkbc()`](https://docs.ropensci.org/QuadratiK/reference/pkbc.md) for
the clustering algorithm.

## Examples

``` r
dat <- rbind(matrix(rnorm(100), 2), matrix(rnorm(100, 5), 2))
res <- pkbc(dat, 2:4)
summary(res)
#> Poisson Kernel-Based Clustering on the Sphere (pkbc) Results
#> ------------------------------------------------------------
#> 
#> Summary:
#>      nClust    LogLik     WCSS
#> [1,]      2  744.1161 4.978247
#> [2,]      3 1104.1246 4.049000
#> [3,]      4 1391.2432 4.000000
#> 
#> Results for 2 clusters:
#> Estimated Mixing Proportions (alpha):
#> [1] 0.2879791 0.7120209
#> 
#> Clustering table:
#> 
#> 1 2 
#> 1 3 
#> 
#> 
#> Results for 3 clusters:
#> Estimated Mixing Proportions (alpha):
#> [1] 0.25 0.25 0.50
#> 
#> Clustering table:
#> 
#> 1 2 3 
#> 1 1 2 
#> 
#> 
#> Results for 4 clusters:
#> Estimated Mixing Proportions (alpha):
#> [1] 0.25 0.25 0.25 0.25
#> 
#> Clustering table:
#> 
#> 1 2 3 4 
#> 1 1 1 1 
#> 
#> 
```
