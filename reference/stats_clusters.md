# Descriptive statistics for the clusters identified by the Poisson kernel-based clustering.

Method for objects of class `pkbc` which computes some descriptive for
each variable with respect to the detected groups.

Method for objects of class `pkbc` which computes descriptive statistics
for each variable with respect to the detected groups.

## Usage

``` r
stats_clusters(object, ...)

# S4 method for class 'pkbc'
stats_clusters(object, k)
```

## Arguments

- object:

  Object of class `pkbc`.

- ...:

  possible additional inputs

- k:

  Number of clusters to be used.

## Value

List with computed descriptive statistics for each dimension.

## Details

The function computes mean, standard deviation, median, inter-quantile
range, minimum and maximum for each variable in the data set given the
final membership assigned by the clustering algorithm.

## See also

[`pkbc()`](https://docs.ropensci.org/QuadratiK/reference/pkbc.md) for
the clustering algorithm.

## Examples

``` r
#We generate three samples of 100 observations from 3-dimensional
#Poisson kernel-based densities with rho=0.8 and different mean directions
dat<-matrix(rnorm(300),ncol=3)

#Perform the clustering algorithm
pkbc_res<- pkbc(dat, 3)
stats_clusters(pkbc_res, 3)
#> [[1]]
#>            Group 1    Group 2     Group 3     Overall
#> mean   -0.53360502  0.2185515 0.007405148  0.04344402
#> sd      0.34258917  0.5269849          NA  0.58084656
#> median -0.55364837  0.2151044 0.007405148  0.07318718
#> IQR     0.53206272  0.9127813 0.000000000  0.93759633
#> min    -0.99487956 -0.9642025 0.007405148 -0.99487956
#> max     0.07466077  0.9873736 0.007405148  0.98737364
#> 
#> [[2]]
#>           Group 1    Group 2   Group 3    Overall
#> mean    0.1608868 -0.1893987 0.8593866 -0.0983452
#> sd      0.3330494  0.6198886        NA  0.5890662
#> median  0.1009154 -0.3009186 0.8593866 -0.1183249
#> IQR     0.5036676  0.9810143 0.0000000  1.0017535
#> min    -0.4511650 -0.9888086 0.8593866 -0.9888086
#> max     0.7908170  0.9928995 0.8593866  0.9928995
#> 
#> [[3]]
#>            Group 1     Group 2    Group 3    Overall
#> mean   -0.62082799  0.09072061 -0.5112727 -0.0789555
#> sd      0.29913303  0.50819936         NA  0.5547490
#> median -0.65141402  0.08038502 -0.5112727 -0.1405382
#> IQR     0.47845791  0.77660008  0.0000000  0.8655454
#> min    -0.95185464 -0.99561644 -0.5112727 -0.9956164
#> max    -0.09110684  0.96905979 -0.5112727  0.9690598
#> 

```
