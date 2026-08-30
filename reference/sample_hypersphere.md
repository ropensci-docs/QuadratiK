# Generate random sample from the hypersphere

Generate a random sample from the uniform distribution on the
hypersphere.

## Usage

``` r
sample_hypersphere(d, n_points = 1)
```

## Arguments

- d:

  Number of dimensions.

- n_points:

  Number of sampled observations.

## Value

Data matrix with the sampled observations.

## Examples

``` r
x_sp <- sample_hypersphere(3,100)
```
