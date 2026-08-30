# Cluster spherical observations using a mixture of Poisson kernel-based densities

Obtain predictions of membership for spherical observations based on a
mixture of Poisson kernel-based densities estimated by `pkbc`

## Usage

``` r
# S4 method for class 'pkbc'
predict(object, k, newdata = NULL)
```

## Arguments

- object:

  Object of class `pkbc`

- k:

  Number of clusters to be used.

- newdata:

  a data.frame or a matrix of the data. If missing the clustering data
  obtained from the `pkbc` object are classified.

## Value

Returns a list with the following components

- Memb: vector of predicted memberships of `newdata`

- Probs: matrix where entry (i,j) denotes the probability that
  observation i belongs to the k-th cluster.

## See also

[`pkbc()`](https://docs.ropensci.org/QuadratiK/reference/pkbc.md) for
the clustering algorithm.

## Examples

``` r
# generate data
dat <- rbind(matrix(rnorm(100), ncol = 2), matrix(rnorm(100, 5), ncol = 2))
res <- pkbc(dat, 2)

# extract membership of dat
predict(res, k = 2)
#>   [1] 2 1 2 1 2 1 2 2 2 2 2 2 2 2 2 2 2 2 2 1 2 2 2 2 2 2 2 2 1 1 1 2 1 2 2 2 2
#>  [38] 2 2 2 1 2 1 1 2 2 2 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1
#>  [75] 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1
# predict membership of new data
newdat <- rbind(matrix(rnorm(10), ncol = 2), matrix(rnorm(10, 5), ncol = 2))
predict(res, k = 2, newdat)
#> $Memb
#>  [1] 1 2 2 2 2 1 1 1 1 1
#> 
#> $Probs
#>             [,1]       [,2]
#>  [1,] 0.79214887 0.20785113
#>  [2,] 0.09155787 0.90844213
#>  [3,] 0.10633003 0.89366997
#>  [4,] 0.05939363 0.94060637
#>  [5,] 0.11831316 0.88168684
#>  [6,] 0.95577420 0.04422580
#>  [7,] 0.97150510 0.02849490
#>  [8,] 0.96104005 0.03895995
#>  [9,] 0.84807303 0.15192697
#> [10,] 0.95487786 0.04512214
#> 
 
```
